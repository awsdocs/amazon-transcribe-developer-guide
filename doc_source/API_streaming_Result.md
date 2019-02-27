# Result<a name="API_streaming_Result"></a>

The result of transcribing a portion of the input audio stream\. 

## Contents<a name="API_streaming_Result_Contents"></a>

 **Alternatives**   <a name="transcribe-Type-streaming_Result-Alternatives"></a>
A list of possible transcriptions for the audio\. Each alternative typically contains one `item` that contains the result of the transcription\.  
Type: Array of [Alternative](API_streaming_Alternative.md) objects  
Required: No

 **EndTime**   <a name="transcribe-Type-streaming_Result-EndTime"></a>
The offset in milliseconds from the beginning of the audio stream to the end of the result\.  
Type: Double  
Required: No

 **IsPartial**   <a name="transcribe-Type-streaming_Result-IsPartial"></a>
 `true` to indicate that Amazon Transcribe has additional transcription data to send, `false` to indicate that this is the last transcription result for the audio stream\.  
Type: Boolean  
Required: No

 **ResultId**   <a name="transcribe-Type-streaming_Result-ResultId"></a>
A unique identifier for the result\.   
Type: String  
Required: No

 **StartTime**   <a name="transcribe-Type-streaming_Result-StartTime"></a>
The offset in milliseconds from the beginning of the audio stream to the beginning of the result\.  
Type: Double  
Required: No

## See Also<a name="API_streaming_Result_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transcribe-streaming-2017-10-26/Result) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transcribe-streaming-2017-10-26/Result) 
+  [AWS SDK for Java](https://docs.aws.amazon.com/goto/SdkForJava/transcribe-streaming-2017-10-26/Result) 
+  [AWS SDK for Ruby V2](https://docs.aws.amazon.com/goto/SdkForRubyV2/transcribe-streaming-2017-10-26/Result) 