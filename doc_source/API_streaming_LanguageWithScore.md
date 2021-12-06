# LanguageWithScore<a name="API_streaming_LanguageWithScore"></a>

The language codes of the identified languages and their associated confidence scores\. The confidence score is a value between zero and one; a larger value indicates a higher confidence in the identified language\.

## Contents<a name="API_streaming_LanguageWithScore_Contents"></a>

 ** LanguageCode **   <a name="transcribe-Type-streaming_LanguageWithScore-LanguageCode"></a>
The language code of the language identified by Amazon Transcribe\.  
Type: String  
Valid Values:` en-US | en-GB | es-US | fr-CA | fr-FR | en-AU | it-IT | de-DE | pt-BR | ja-JP | ko-KR | zh-CN`   
Required: No

 ** Score **   <a name="transcribe-Type-streaming_LanguageWithScore-Score"></a>
The confidence score for the associated language code\. Confidence scores are values between zero and one; larger values indicate a higher confidence in the identified language\.   
Type: Double  
Required: No

## See Also<a name="API_streaming_LanguageWithScore_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [ AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transcribe-streaming-2017-10-26/LanguageWithScore) 
+  [ AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transcribe-streaming-2017-10-26/LanguageWithScore) 
+  [ AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transcribe-streaming-2017-10-26/LanguageWithScore) 
+  [ AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transcribe-streaming-2017-10-26/LanguageWithScore) 