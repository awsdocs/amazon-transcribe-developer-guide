# ContentRedaction<a name="API_ContentRedaction"></a>

Settings for content redaction within a transcription job\.

## Contents<a name="API_ContentRedaction_Contents"></a>

 **RedactionOutput**   <a name="transcribe-Type-ContentRedaction-RedactionOutput"></a>
The output transcript file stored in either the default S3 bucket or in a bucket you specify\.  
When you choose `redacted` Amazon Transcribe outputs only the redacted transcript\.  
When you choose `redacted_and_unredacted` Amazon Transcribe outputs both the redacted and unredacted transcripts\.  
Type: String  
Valid Values:` redacted | redacted_and_unredacted`   
Required: Yes

 **RedactionType**   <a name="transcribe-Type-ContentRedaction-RedactionType"></a>
Request parameter that defines the entities to be redacted\. The only accepted value is `PII`\.  
Type: String  
Valid Values:` PII`   
Required: Yes

## See Also<a name="API_ContentRedaction_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [ AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transcribe-2017-10-26/ContentRedaction) 
+  [ AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transcribe-2017-10-26/ContentRedaction) 
+  [ AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transcribe-2017-10-26/ContentRedaction) 
+  [ AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transcribe-2017-10-26/ContentRedaction) 