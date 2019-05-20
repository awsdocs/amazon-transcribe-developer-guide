# Streaming Retry Client<a name="streaming-client"></a>

 You can use the following code in your applications to handle retry logic for Amazon Transcribe streaming transcription\. The code provides tolerance for intermittent failures in the connection to Amazon Transcribe\. There are two parts of the client: an interface that you implement for your application, and the retry client itself\.

## Streaming Retry Client Code<a name="streaming-retry-client"></a>

This code implements a streaming retry client\. It manages the connection to Amazon Transcribe and retries sending data when there are errors on the connection\. For example, if there is a transient error on the network, this client resends the request that failed\.

The retry client has two properties that control the behavior of the client\. You can set:
+ The maximum number of times that the client should attempt before failing\. Reduce this value to make your application stop retrying sooner when there are network issues\. The default is 10\.
+ The time in milliseconds that the client should wait between retries\. Longer times raise the risk of losing data, shorter times raise the risk of your application being throttled\. The default is 100 milliseconds\.

The following is the client\. You can copy this code to your application or use it as a starting point for your own client\.

```
/**
 * COPYRIGHT:
 *
 * Copyright 2018-2019 Amazon.com, Inc. or its affiliates. All Rights Reserved.
 *
 * Licensed under the Apache License, Version 2.0 (the "License").
 * You may not use this file except in compliance with the License.
 * A copy of the License is located at
 *
 *     http://www.apache.org/licenses/LICENSE-2.0
 *
 * or in the "license" file accompanying this file. This file is distributed
 * on an "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either
 * express or implied. See the License for the specific language governing
 * permissions and limitations under the License.
 */
package com.amazonaws.transcribestreaming.retryclient;

/**
 * Build a client wrapper around the Amazon Transcribe client to retry 
 * on an exception that can be retried.
 */
public class TranscribeStreamingRetryClient {

    private static final int DEFAULT_MAX_RETRIES = 10;
    private static final int DEFAULT_MAX_SLEEP_TIME_MILLS = 100;
    private int maxRetries = DEFAULT_MAX_RETRIES;
    private int sleepTime = DEFAULT_MAX_SLEEP_TIME_MILLS;
    private final TranscribeStreamingAsyncClient client;
    List<Class<?>> nonRetriableExceptions = Arrays.asList(BadRequestException.class);

    private static final Logger log = LoggerFactory.getLogger(TranscribeStreamingRetryClient.class);
    /**
     * Create a TranscribeStreamingRetryClient with given credential and configuration
     * @param creds Creds to use for transcription
     * @param endpoint Endpoint to use for transcription
     * @param region Region to use for transcriptions
     * @throws URISyntaxException if the endpoint is not a URI
     */
    public TranscribeStreamingRetryClient(AwsCredentialsProvider creds,
                                          String endpoint, Region region) throws URISyntaxException {
        this(TranscribeStreamingAsyncClient.builder()
                .overrideConfiguration(
                        c -> c.putAdvancedOption(
                                SdkAdvancedClientOption.SIGNER,
                                EventStreamAws4Signer.create()))
                .credentialsProvider(creds)
                .endpointOverride(new URI(endpoint))
                .region(region)
                .build());
    }

    /**
     * Initiate TranscribeStreamingRetryClient with TranscribeStreamingAsyncClient
     * @param client TranscribeStreamingAsyncClient
     */
    public TranscribeStreamingRetryClient(TranscribeStreamingAsyncClient client) {
        this.client = client;
    }

    /**
     * Get Max retries
     * @return Max retries
     */
    public int getMaxRetries() {
        return maxRetries;
    }

    /**
     * Set Max retries
     * @param  maxRetries Max retries
     */
    public void setMaxRetries(int maxRetries) {
        this.maxRetries = maxRetries;
    }

    /**
     * Get sleep time
     * @return sleep time between retries
     */
    public int getSleepTime() {
        return sleepTime;
    }

    /**
     * Set sleep time between retries
     * @param sleepTime sleep time
     */
    public void setSleepTime(int sleepTime) {
        this.sleepTime = sleepTime;
    }

    /**
     * Initiate a Stream Transcription with retry.
     * @param request StartStreamTranscriptionRequest to use to start transcription
     * @param publisher The source audio stream as Publisher
     * @param responseHandler StreamTranscriptionBehavior object that defines how the response needs to be handled.
     * @return Completable future to handle stream response.
     */

    public CompletableFuture<Void> startStreamTranscription(final StartStreamTranscriptionRequest request,
                                                            final Publisher<AudioStream> publisher,
                                                            final StreamTranscriptionBehavior responseHandler) {

        CompletableFuture<Void> finalFuture = new CompletableFuture<>();

        recursiveStartStream(rebuildRequestWithSession(request), publisher, responseHandler, finalFuture, 0);

        return finalFuture;
    }

    /**
     * Recursively call startStreamTranscription() to be called till the request is completed or till we run out of retries.
     * @param request StartStreamTranscriptionRequest
     * @param publisher The source audio stream as Publisher
     * @param responseHandler StreamTranscriptionBehavior object that defines how the response needs to be handled.
     * @param finalFuture final future to finish on completing the chained futures.
     * @param retryAttempt Current attempt number
     */
    private void recursiveStartStream(final StartStreamTranscriptionRequest request,
                                      final Publisher<AudioStream> publisher,
                                      final StreamTranscriptionBehavior responseHandler,
                                      final CompletableFuture<Void> finalFuture,
                                      final int retryAttempt) {
        CompletableFuture<Void> result = client.startStreamTranscription(request, publisher,
                getResponseHandler(responseHandler));
        result.whenComplete((r, e) -> {
            if (e != null) {
                log.debug("Error occured:", e);

                if (retryAttempt <= maxRetries && isExceptionRetriable(e)) {
                    log.debug("Retriable error occurred and will be retried.");
                    log.debug("Sleeping for sometime before retrying...");
                    try {
                        Thread.sleep(sleepTime);
                    } catch (InterruptedException e1) {
                        log.debug("Unable to sleep. Failed with exception: ", e);
                        e1.printStackTrace();
                    }
                    log.debug("Making retry attempt: " + (retryAttempt+1));
                    recursiveStartStream(request, publisher, responseHandler, finalFuture, retryAttempt + 1);
                } else {
                    log.error("Encountered unretriable exception or ran out of retries. ");
                    responseHandler.onError(e);
                    finalFuture.completeExceptionally(e);
                }
            } else {
                responseHandler.onComplete();
                finalFuture.complete(null);
            }
        });
    }
    private StartStreamTranscriptionRequest rebuildRequestWithSession(StartStreamTranscriptionRequest request) {
            return StartStreamTranscriptionRequest.builder()
                    .languageCode(request.languageCode())
                    .mediaEncoding(request.mediaEncoding())
                    .mediaSampleRateHertz(request.mediaSampleRateHertz())
                    .sessionId(UUID.randomUUID().toString())
                    .build();
    }

    /**
     * StartStreamTranscriptionResponseHandler implements subscriber of transcript stream
     * Output is printed to standard output
     */
    private StartStreamTranscriptionResponseHandler getResponseHandler(
            StreamTranscriptionBehavior transcriptionBehavior) {
        final StartStreamTranscriptionResponseHandler build = StartStreamTranscriptionResponseHandler.builder()
                .onResponse(r -> {
                    transcriptionBehavior.onResponse(r);
                })
                .onError(e -> {
                    //Do nothing here. Don't close any streams that shouldn't be cleaned up yet.
                })
                .onComplete(() -> {
                    //Do nothing here. Don't close any streams that shouldn't be cleaned up yet.
                })

                .subscriber(event -> transcriptionBehavior.onStream(event))
                .build();
        return build;
    }

    /**
     * Check if the exception can be retried.
     * @param e Exception that occurred
     * @return True if the exception is retriable
     */
    private boolean isExceptionRetriable(Throwable e) {
        e.printStackTrace();
        if (nonRetriableExceptions.contains(e.getClass())) {
            return false;
        }
        return true;
    }
    public void close() {
        this.client.close();
    }

}
```

## Streaming Retry Client Interface Code<a name="streaming-client-interface"></a>

This interface is similar to the response handler used in the getting started example\. It implements the same event handlers\. Implement this interface to use the streaming retry client\.

```
/**
 * COPYRIGHT:
 *
 * Copyright 2018-2019 Amazon.com, Inc. or its affiliates. All Rights Reserved.
 *
 * Licensed under the Apache License, Version 2.0 (the "License").
 * You may not use this file except in compliance with the License.
 * A copy of the License is located at
 *
 *     http://www.apache.org/licenses/LICENSE-2.0
 *
 * or in the "license" file accompanying this file. This file is distributed
 * on an "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either
 * express or implied. See the License for the specific language governing
 * permissions and limitations under the License.
 *
 */
package com.amazonaws.transcribestreaming.retryclient;

/**
 * Defines how a stream response should be handled.
 * You should build a class implementing this interface to define the behavior.
 */
public interface StreamTranscriptionBehavior {
    /**
     * Defines how to respond when encountering an error on the stream transcription.
     * @param e The exception
     */
    void onError(Throwable e);

    /**
     * Defines how to respond to the Transcript result stream.
     * @param e The TranscriptResultStream event
     */
    void onStream(TranscriptResultStream e);

    /**
     * Defines what to do on initiating a stream connection with the service.
     * @param r StartStreamTranscriptionResponse
     */
    void onResponse(StartStreamTranscriptionResponse r);


    /**
     * Defines what to do on stream completion
     */
    void onComplete();
}
```

The following is an example implementation of the `StreamTranscriptionBehavior` interface\. You can use this implementation or use it as a starting point for your own implementation\.

```
/**
 * COPYRIGHT:
 *
 * Copyright 2018-2019 Amazon.com, Inc. or its affiliates. All Rights Reserved.
 *
 * Licensed under the Apache License, Version 2.0 (the "License").
 * You may not use this file except in compliance with the License.
 * A copy of the License is located at
 *
 *     http://www.apache.org/licenses/LICENSE-2.0
 *
 * or in the "license" file accompanying this file. This file is distributed
 * on an "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either
 * express or implied. See the License for the specific language governing
 * permissions and limitations under the License.
 *
 */
package com.amazonaws.transcribestreaming.retryclient;

/**
 * Defines how a stream response should be handled.
 * You should build a class implementing this interface to define the behavior.
 */
public interface StreamTranscriptionBehavior {
    /**
     * Defines how to respond when encountering an error on the stream transcription.
     * @param e The exception
     */
    void onError(Throwable e);

    /**
     * Defines how to respond to the Transcript result stream.
     * @param e The TranscriptResultStream event
     */
    void onStream(TranscriptResultStream e);

    /**
     * Defines what to do on initiating a stream connection with the service.
     * @param r StartStreamTranscriptionResponse
     */
    void onResponse(StartStreamTranscriptionResponse r);


    /**
     * Defines what to do on stream completion
     */
    void onComplete();
}
```

### Next step<a name="retry-client-next"></a>

[Using the Retry Client](retry-client-example.md)