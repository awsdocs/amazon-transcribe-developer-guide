# TranscriptResultStream<a name="API_streaming_TranscriptResultStream"></a>

Represents the transcription result stream from Amazon Transcribe to your application\.

## Contents<a name="API_streaming_TranscriptResultStream_Contents"></a>

 **BadRequestException**   <a name="transcribe-Type-streaming_TranscriptResultStream-BadRequestException"></a>
A client error occurred when the stream was created\. Check the parameters of the request and try your request again\.  
Type: Exception  
Required: No

 **ConflictException**   <a name="transcribe-Type-streaming_TranscriptResultStream-ConflictException"></a>
A new stream started with the same session ID\. The current stream has been terminated\.  
Type: Exception  
Required: No

 **InternalFailureException**   <a name="transcribe-Type-streaming_TranscriptResultStream-InternalFailureException"></a>
A problem occurred while processing the audio\. Amazon Transcribe terminated processing\.  
Type: Exception  
Required: No

 **LimitExceededException**   <a name="transcribe-Type-streaming_TranscriptResultStream-LimitExceededException"></a>
Your client has exceeded one of the Amazon Transcribe limits, typically the limit on audio length\. Break your audio stream into smaller chunks and try your request again\.  
Type: Exception  
Required: No

 **TranscriptEvent**   <a name="transcribe-Type-streaming_TranscriptResultStream-TranscriptEvent"></a>
A portion of the transcription of the audio stream\. Events are sent periodically from Amazon Transcribe to your application\. The event can be a partial transcription of a section of the audio stream, or it can be the entire transcription of that portion of the audio stream\.   
Type: [TranscriptEvent](API_streaming_TranscriptEvent.md) object  
Required: No

## See Also<a name="API_streaming_TranscriptResultStream_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transcribe-streaming-2017-10-26/TranscriptResultStream) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transcribe-streaming-2017-10-26/TranscriptResultStream) 
+  [AWS SDK for Java](https://docs.aws.amazon.com/goto/SdkForJava/transcribe-streaming-2017-10-26/TranscriptResultStream) 
+  [AWS SDK for Ruby V2](https://docs.aws.amazon.com/goto/SdkForRubyV2/transcribe-streaming-2017-10-26/TranscriptResultStream) 