# Entity<a name="API_streaming_Entity"></a>

The entity identified as personally identifiable information \(PII\)\.

## Contents<a name="API_streaming_Entity_Contents"></a>

 **Category**   <a name="transcribe-Type-streaming_Entity-Category"></a>
The category of of information identified in this entity; for example, PII\.  
Type: String  
Required: No

 **Confidence**   <a name="transcribe-Type-streaming_Entity-Confidence"></a>
A value between zero and one that Amazon Transcribe assigns to PII identified in the source audio\. Larger values indicate a higher confidence in PII identification\.  
Type: Double  
Required: No

 **Content**   <a name="transcribe-Type-streaming_Entity-Content"></a>
The words in the transcription output that have been identified as a PII entity\.  
Type: String  
Required: No

 **EndTime**   <a name="transcribe-Type-streaming_Entity-EndTime"></a>
The end time of speech that was identified as PII\.  
Type: Double  
Required: No

 **StartTime**   <a name="transcribe-Type-streaming_Entity-StartTime"></a>
The start time of speech that was identified as PII\.  
Type: Double  
Required: No

 **Type**   <a name="transcribe-Type-streaming_Entity-Type"></a>
The type of PII identified in this entity; for example, name or credit card number\.  
Type: String  
Required: No

## See Also<a name="API_streaming_Entity_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [ AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transcribe-streaming-2017-10-26/Entity) 
+  [ AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transcribe-streaming-2017-10-26/Entity) 
+  [ AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transcribe-streaming-2017-10-26/Entity) 
+  [ AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transcribe-streaming-2017-10-26/Entity) 