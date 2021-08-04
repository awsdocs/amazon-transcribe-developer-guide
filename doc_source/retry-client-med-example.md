# Using the HTTP/2 retry client<a name="retry-client-med-example"></a>

The following is a sample application that uses the retry client to transcribe audio from either a file or your microphone\. You can use this application to test the client, or you can use it as a starting point for your own applications\.

To run the sample, do the following:
+ Copy the retry client to your workspace\. See [Streaming retry client code](streaming-med-client.md#streaming-med-retry-client-med)\.
+ Copy the retry client interface to your workspace\. Implement the interface, or you can use the sample implementation\. See [Streaming retry client interface code](streaming-med-client.md#streaming-med-client-interface)\.
+ Copy the sample application to your workspace\. Build and run the application\.

```
public class StreamingRetryApp {
    private static final String endpoint = "endpoint";
    private static final Region region = Region.US_EAST_1;
    private static final int sample_rate = 28800;
    private static final String encoding = " ";
    private static final String language = LanguageCode.EN_US.toString();

    public static void main(String args[]) throws URISyntaxException, ExecutionException, InterruptedException, LineUnavailableException, FileNotFoundException {
        /**
         * Create Amazon Transcribe streaming retry client.
         */

        TranscribeStreamingRetryClient client = new TranscribeStreamingRetryClient(EnvironmentVariableCredentialsProvider.create() ,endpoint, region);

        StartStreamTranscriptionRequest request = StartStreamTranscriptionRequest.builder()
                .languageCode(language)
                .mediaEncoding(encoding)
                .mediaSampleRateHertz(sample_rate)
                .build();
        /**
         * Start real-time speech recognition. The Amazon Transcribe streaming java client uses the Reactive-streams
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
        private static Subscription currentSubscription;

        private AudioStreamPublisher(InputStream inputStream) {
            this.inputStream = inputStream;
        }

        @Override
        public void subscribe(Subscriber<? super AudioStream> s) {
            if (this.currentSubscription == null) {
                this.currentSubscription = new TranscribeStreamingDemoApp.SubscriptionImpl(s, inputStream);
            } else {
                this.currentSubscription.cancel();
                this.currentSubscription = new TranscribeStreamingDemoApp.SubscriptionImpl(s, inputStream);
            }
            s.onSubscribe(currentSubscription);
        }
    }
}
```