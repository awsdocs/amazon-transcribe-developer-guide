# Using the Retry Client<a name="retry-client-example"></a>

The following is a sample application that uses the retry client to transcribe audio from either a file or your microphone\. You can use this application to test the client, or you can use it as a starting point for your own applications\.

To run the sample, do the following:
+ Copy the retry client to your workspace\. See [Streaming Retry Client Code](streaming-client.md#streaming-retry-client)\.
+ Copy the retry client interface to your workspace\. Implement the interface, or you can use the sample implementation\. See [Streaming Retry Client Interface Code](streaming-client.md#streaming-client-interface)\.
+ Copy the sample application to your workspace\. Build and run the application\.

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

public class SampleApp {
    private static final String endpoint = "endpoint";
    private static final Region region = region;
    public static void main(String args[]) throws URISyntaxException, ExecutionException, InterruptedException, LineUnavailableException, FileNotFoundException {
        /**
         * Create Transcribe streaming retry client using AWS credentials.
         */
        TranscribeStreamingRetryClient client = new TranscribeStreamingRetryClient(getCredentials(), endpoint, region);

        StartStreamTranscriptionRequest request =  StartStreamTranscriptionRequest.builder()
                .languageCode(LanguageCode.language.toString())
                .mediaEncoding(encoding)
                .mediaSampleRateHertz(sample rate)
                .build();
        /**
         * Start real-time speech recognition. The Transcribe streaming java client uses the Reactive-streams 
         * interface. For reference on Reactive-streams: 
         *     https://github.com/reactive-streams/reactive-streams-jvm
         */
        CompletableFuture<Void> result = client.startStreamTranscription(
                /**
                 * Request parameters. Refer to API documentation for details.
                 */
                request,
                /**
                 * Provide an input audio stream.
                 * For input from a microphone, use getStreamFromMic().
                 * For input from a file, use getStreamFromFile().
                 */
                new AudioStreamPublisher(
                        new FileInputStream(new File("FileName"))),
                /**
                 * Object that defines the behavior on how to handle the stream
                 */
                new StreamTranscriptionBehaviorImpl());

        /**
         * Synchronous wait for stream to close, and close client connection
         */
        result.get();
        client.close();
    }
    
    private static class AudioStreamPublisher implements Publisher<AudioStream> {
    private final InputStream inputStream;

        private AudioStreamPublisher(InputStream inputStream) {
            this.inputStream = inputStream;
        }

        @Override
        public void subscribe(Subscriber<? super AudioStream> s) {
            if (currentSubscription == null) {
                this.currentSubscription = new SubscriptionImpl(s, inputStream);
            } else {
                this.currentSubscription.cancel();
                this.currentSubscription = new SubscriptionImpl(s, inputStream);
            }
            s.onSubscribe(currentSubscription);
        }
    }
}
```