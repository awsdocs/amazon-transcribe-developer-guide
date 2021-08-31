# MedicalTranscriptResultStream<a name="API_streaming_MedicalTranscriptResultStream"></a>

Represents the transcription result stream from Amazon Transcribe Medical to your application\.

## Contents<a name="API_streaming_MedicalTranscriptResultStream_Contents"></a>

 ** BadRequestException **   <a name="transcribe-Type-streaming_MedicalTranscriptResultStream-BadRequestException"></a>
One or more arguments to the `StartStreamTranscription` or `StartMedicalStreamTranscription` operation was invalid\. For example, `MediaEncoding` was not set to a valid encoding, or `LanguageCode` was not set to a valid code\. Check the parameters and try your request again\.  
Type: Exception  
Required: No

 ** ConflictException **   <a name="transcribe-Type-streaming_MedicalTranscriptResultStream-ConflictException"></a>
A new stream started with the same session ID\. The current stream has been terminated\.  
Type: Exception  
Required: No

 ** InternalFailureException **   <a name="transcribe-Type-streaming_MedicalTranscriptResultStream-InternalFailureException"></a>
A problem occurred while processing the audio\. Amazon Transcribe or Amazon Transcribe Medical terminated processing\. Try your request again\.  
Type: Exception  
Required: No

 ** LimitExceededException **   <a name="transcribe-Type-streaming_MedicalTranscriptResultStream-LimitExceededException"></a>
You have exceeded the maximum number of concurrent transcription streams, are starting transcription streams too quickly, or the maximum audio length of 4 hours\. Wait until a stream has finished processing, or break your audio stream into smaller chunks and try your request again\.  
Type: Exception  
Required: No

 ** ServiceUnavailableException **   <a name="transcribe-Type-streaming_MedicalTranscriptResultStream-ServiceUnavailableException"></a>
Service is currently unavailable\. Try your request later\.  
Type: Exception  
Required: No

 ** TranscriptEvent **   <a name="transcribe-Type-streaming_MedicalTranscriptResultStream-TranscriptEvent"></a>
A portion of the transcription of the audio stream\. Events are sent periodically from Amazon Transcribe Medical to your application\. The event can be a partial transcription of a section of the audio stream, or it can be the entire transcription of that portion of the audio stream\.  
Type: [ MedicalTranscriptEvent ](API_streaming_MedicalTranscriptEvent.md) object  
Required: No

## See Also<a name="API_streaming_MedicalTranscriptResultStream_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [ AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transcribe-streaming-2017-10-26/MedicalTranscriptResultStream) 
+  [ AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transcribe-streaming-2017-10-26/MedicalTranscriptResultStream) 
+  [ AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transcribe-streaming-2017-10-26/MedicalTranscriptResultStream) 
+  [ AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transcribe-streaming-2017-10-26/MedicalTranscriptResultStream) 