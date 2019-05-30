# VocabularyInfo<a name="API_VocabularyInfo"></a>

Provides information about a custom vocabulary\. 

## Contents<a name="API_VocabularyInfo_Contents"></a>

 **LanguageCode**   <a name="transcribe-Type-VocabularyInfo-LanguageCode"></a>
The language code of the vocabulary entries\.  
Type: String  
Valid Values:` en-US | es-US | en-AU | fr-CA | en-GB | de-DE | pt-BR | fr-FR | it-IT | ko-KR | es-ES | en-IN | hi-IN | ar-SA`   
Required: No

 **LastModifiedTime**   <a name="transcribe-Type-VocabularyInfo-LastModifiedTime"></a>
The date and time that the vocabulary was last modified\.  
Type: Timestamp  
Required: No

 **VocabularyName**   <a name="transcribe-Type-VocabularyInfo-VocabularyName"></a>
The name of the vocabulary\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 200\.  
Pattern: `^[0-9a-zA-Z._-]+`   
Required: No

 **VocabularyState**   <a name="transcribe-Type-VocabularyInfo-VocabularyState"></a>
The processing state of the vocabulary\. If the state is `READY` you can use the vocabulary in a `StartTranscriptionJob` request\.  
Type: String  
Valid Values:` PENDING | READY | FAILED`   
Required: No

## See Also<a name="API_VocabularyInfo_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transcribe-2017-10-26/VocabularyInfo) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transcribe-2017-10-26/VocabularyInfo) 
+  [AWS SDK for Go \- Pilot](https://docs.aws.amazon.com/goto/SdkForGoPilot/transcribe-2017-10-26/VocabularyInfo) 
+  [AWS SDK for Java](https://docs.aws.amazon.com/goto/SdkForJava/transcribe-2017-10-26/VocabularyInfo) 
+  [AWS SDK for Ruby V2](https://docs.aws.amazon.com/goto/SdkForRubyV2/transcribe-2017-10-26/VocabularyInfo) 