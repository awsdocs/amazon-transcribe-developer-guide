# VocabularyInfo<a name="API_VocabularyInfo"></a>

Provides information about a custom vocabulary\. 

## Contents<a name="API_VocabularyInfo_Contents"></a>

 ** LanguageCode **   <a name="transcribe-Type-VocabularyInfo-LanguageCode"></a>
The language code of the vocabulary entries\.  
Type: String  
Valid Values:` af-ZA | ar-AE | ar-SA | cy-GB | da-DK | de-CH | de-DE | en-AB | en-AU | en-GB | en-IE | en-IN | en-US | en-WL | es-ES | es-US | fa-IR | fr-CA | fr-FR | ga-IE | gd-GB | he-IL | hi-IN | id-ID | it-IT | ja-JP | ko-KR | ms-MY | nl-NL | pt-BR | pt-PT | ru-RU | ta-IN | te-IN | tr-TR | zh-CN | zh-TW | th-TH | en-ZA | en-NZ`   
Required: No

 ** LastModifiedTime **   <a name="transcribe-Type-VocabularyInfo-LastModifiedTime"></a>
The date and time that the vocabulary was last modified\.  
Type: Timestamp  
Required: No

 ** VocabularyName **   <a name="transcribe-Type-VocabularyInfo-VocabularyName"></a>
The name of the vocabulary\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 200\.  
Pattern: `^[0-9a-zA-Z._-]+`   
Required: No

 ** VocabularyState **   <a name="transcribe-Type-VocabularyInfo-VocabularyState"></a>
The processing state of the vocabulary\. If the state is `READY` you can use the vocabulary in a `StartTranscriptionJob` request\.  
Type: String  
Valid Values:` PENDING | READY | FAILED`   
Required: No

## See Also<a name="API_VocabularyInfo_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [ AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transcribe-2017-10-26/VocabularyInfo) 
+  [ AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transcribe-2017-10-26/VocabularyInfo) 
+  [ AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transcribe-2017-10-26/VocabularyInfo) 
+  [ AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transcribe-2017-10-26/VocabularyInfo) 