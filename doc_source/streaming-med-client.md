# HTTP/2 streaming retry client<a name="streaming-med-client"></a>

You can use the following code in your applications to handle retry logic for Amazon Transcribe Medical streaming transcription\. The code provides tolerance for intermittent failures in the connection to Amazon Transcribe Medical\. There are two parts of the client: an interface that you implement for your application, and the retry client itself\.

## Streaming retry client code<a name="streaming-med-retry-client-med"></a>

This code implements a streaming retry client\. It manages the connection to Amazon Transcribe Medical and retries sending data when there are errors on the connection\. For example, if there is a transient error on the network, this client resends the request that failed\.

The retry client has two properties that control the behavior of the client\. You can set:
+ The maximum number of times that the client should attempt before failing\. Reduce this value to make your application stop retrying sooner when there are network issues\. The default is 10\.
+ The time in milliseconds that the client should wait between retries\. Longer times raise the risk of losing data, shorter times raise the risk of your application being throttled\. The default is 100 milliseconds\.

The following is the client\. You can copy this code to your application or use it as a starting point for your own client\.

```
public class TranscribeStreamingRetryClient {

    private static final int DEFAULT_MAX_RETRIES = 10;
    private static final int DEFAULT_MAX_SLEEP_TIME_MILLS = 100;
    private static final Logger log = LoggerFactory.getLogger(TranscribeStreamingRetryClient.class);
    private final TranscribeStreamingAsyncClient client;
    List<Class<?>> nonRetriableExceptions = Arrays.asList(BadRequestException.class);
    private int maxRetries = DEFAULT_MAX_RETRIES;
    private int sleepTime = DEFAULT_MAX_SLEEP_TIME_MILLS;

    /**
     * Create a TranscribeStreamingRetryClient with given credential and configuration
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
     */

    public TranscribeStreamingRetryClient(TranscribeStreamingAsyncClient client) {
        this.client = client;
    }

    /**
     * Get Max retries
     */
    public int getMaxRetries() {
        return maxRetries;
    }

    /**
     * Set Max retries
     */
    public void setMaxRetries(int maxRetries) {
        this.maxRetries = maxRetries;
    }

    /**
     * Get sleep time
     */
    public int getSleepTime() {
        return sleepTime;
    }

    /**
     * Set sleep time between retries
     */
    public void setSleepTime(int sleepTime) {
        this.sleepTime = sleepTime;
    }

    /**
     * Initiate a Stream Transcription with retry.
     */

    public CompletableFuture<Void> startStreamTranscription(final StartStreamTranscriptionRequest request,
                                                            final Publisher<AudioStream> publisher,
                                                            final StreamTranscriptionBehavior responseHandler) {

        CompletableFuture<Void> finalFuture = new CompletableFuture<>();

        recursiveStartStream(rebuildRequestWithSession(request), publisher, responseHandler, finalFuture, 0);

        return finalFuture;
    }

    /**
     * Recursively call startStreamTranscription() until the request is completed or we run out of retries.
     *
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
                    log.debug("Making retry attempt: " + (retryAttempt + 1));
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
     *
     */
    private boolean isExceptionRetriable(Throwable e) {
        e.printStackTrace();

        return nonRetriableExceptions.contains(e.getClass());
    }

    public void close() {
        this.client.close();
    }

}
```

## Streaming retry client interface code<a name="streaming-med-client-interface"></a>

This interface is similar to the response handler used in the getting started example\. It implements the same event handlers\. Implement this interface to use the streaming\-med retry client\.

```
package com.amazonaws.transcribestreaming;

import software.amazon.awssdk.services.transcribestreaming.model.StartStreamTranscriptionResponse;
import software.amazon.awssdk.services.transcribestreaming.model.TranscriptResultStream;

/**
 * Defines how a stream response should be handled.
 * You should build a class implementing this interface to define the behavior.
 */
public interface StreamTranscriptionBehavior {
    /**
     * Defines how to respond when encountering an error on the stream transcription.
     */
    void onError(Throwable e);

    /**
     * Defines how to respond to the Transcript result stream.
     */
    void onStream(TranscriptResultStream e);

    /**
     * Defines what to do on initiating a stream connection with the service.
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
package com.amazonaws.transcribestreaming.retryclient;


import com.amazonaws.transcribestreaming.retryclient.StreamTranscriptionBehavior;
import software.amazon.awssdk.services.transcribestreaming.model.Result;
import software.amazon.awssdk.services.transcribestreaming.model.StartStreamTranscriptionResponse;
import software.amazon.awssdk.services.transcribestreaming.model.TranscriptEvent;
import software.amazon.awssdk.services.transcribestreaming.model.TranscriptResultStream;

import java.util.List;

/**
 * Implementation of StreamTranscriptionBehavior to define how a stream response should be handled.
 *
 * COPYRIGHT:
 *
 * Copyright 2018 Amazon.com, Inc. or its affiliates. All Rights Reserved.
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
public class StreamTranscriptionBehaviorImpl implements StreamTranscriptionBehavior {


    @Override
    public void onError(Throwable e) {
        System.out.println("=== Failure Encountered ===");
        e.printStackTrace();
    }

    @Override
    public void onStream(TranscriptResultStream e) {
        // EventResultStream has other fields related to the the timestamp of the transcripts in it.
        // Please refer to the javadoc of TranscriptResultStream for more details
        List<Result> results = ((TranscriptEvent) e).transcript().results();
        if (results.size() > 0) {
            if (results.get(0).alternatives().size() > 0)
                if (!results.get(0).alternatives().get(0).transcript().isEmpty()) {
                    System.out.println(results.get(0).alternatives().get(0).transcript());
                }
        }
    }

    @Override
    public void onResponse(StartStreamTranscriptionResponse r) {

        System.out.println(String.format("=== Received Initial response. Request Id: %s ===", r.requestId()));
    }

    @Override
    public void onComplete() {
        System.out.println("=== All records stream successfully ===");
    }
```

### Next step<a name="retry-client-med-next"></a>

[Using the HTTP/2 retry client](retry-client-med-example.md)