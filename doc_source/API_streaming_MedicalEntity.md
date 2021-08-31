# MedicalEntity<a name="API_streaming_MedicalEntity"></a>

The medical entity identified as personal health information\.

## Contents<a name="API_streaming_MedicalEntity_Contents"></a>

 ** Category **   <a name="transcribe-Type-streaming_MedicalEntity-Category"></a>
The type of personal health information of the medical entity\.  
Type: String  
Required: No

 ** Confidence **   <a name="transcribe-Type-streaming_MedicalEntity-Confidence"></a>
A value between zero and one that Amazon Transcribe Medical assigned to the personal health information that it identified in the source audio\. Larger values indicate that Amazon Transcribe Medical has higher confidence in the personal health information that it identified\.  
Type: Double  
Required: No

 ** Content **   <a name="transcribe-Type-streaming_MedicalEntity-Content"></a>
The word or words in the transcription output that have been identified as a medical entity\.  
Type: String  
Required: No

 ** EndTime **   <a name="transcribe-Type-streaming_MedicalEntity-EndTime"></a>
The end time of the speech that was identified as a medical entity\.  
Type: Double  
Required: No

 ** StartTime **   <a name="transcribe-Type-streaming_MedicalEntity-StartTime"></a>
The start time of the speech that was identified as a medical entity\.  
Type: Double  
Required: No

## See Also<a name="API_streaming_MedicalEntity_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [ AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transcribe-streaming-2017-10-26/MedicalEntity) 
+  [ AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transcribe-streaming-2017-10-26/MedicalEntity) 
+  [ AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transcribe-streaming-2017-10-26/MedicalEntity) 
+  [ AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transcribe-streaming-2017-10-26/MedicalEntity) 