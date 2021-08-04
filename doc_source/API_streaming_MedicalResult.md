# MedicalResult<a name="API_streaming_MedicalResult"></a>

The results of transcribing a portion of the input audio stream\.

## Contents<a name="API_streaming_MedicalResult_Contents"></a>

 **Alternatives**   <a name="transcribe-Type-streaming_MedicalResult-Alternatives"></a>
A list of possible transcriptions of the audio\. Each alternative typically contains one `Item` that contains the result of the transcription\.  
Type: Array of [MedicalAlternative](API_streaming_MedicalAlternative.md) objects  
Required: No

 **ChannelId**   <a name="transcribe-Type-streaming_MedicalResult-ChannelId"></a>
When channel identification is enabled, Amazon Transcribe Medical transcribes the speech from each audio channel separately\.  
You can use `ChannelId` to retrieve the transcription results for a single channel in your audio stream\.  
Type: String  
Required: No

 **EndTime**   <a name="transcribe-Type-streaming_MedicalResult-EndTime"></a>
The time, in seconds, from the beginning of the audio stream to the end of the result\.  
Type: Double  
Required: No

 **IsPartial**   <a name="transcribe-Type-streaming_MedicalResult-IsPartial"></a>
Amazon Transcribe Medical divides the incoming audio stream into segments at natural points in the audio\. Transcription results are returned based on these segments\.  
The `IsPartial` field is `true` to indicate that Amazon Transcribe Medical has additional transcription data to send\. The `IsPartial` field is `false` to indicate that this is the last transcription result for the segment\.  
Type: Boolean  
Required: No

 **ResultId**   <a name="transcribe-Type-streaming_MedicalResult-ResultId"></a>
A unique identifier for the result\.  
Type: String  
Required: No

 **StartTime**   <a name="transcribe-Type-streaming_MedicalResult-StartTime"></a>
The time, in seconds, from the beginning of the audio stream to the beginning of the result\.  
Type: Double  
Required: No

## See Also<a name="API_streaming_MedicalResult_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transcribe-streaming-2017-10-26/MedicalResult) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transcribe-streaming-2017-10-26/MedicalResult) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transcribe-streaming-2017-10-26/MedicalResult) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transcribe-streaming-2017-10-26/MedicalResult) 