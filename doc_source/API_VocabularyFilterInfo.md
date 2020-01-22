# VocabularyFilterInfo<a name="API_VocabularyFilterInfo"></a>

Provides information about a vocabulary filter\.

## Contents<a name="API_VocabularyFilterInfo_Contents"></a>

 **LanguageCode**   <a name="transcribe-Type-VocabularyFilterInfo-LanguageCode"></a>
The language code of the words in the vocabulary filter\.  
Type: String  
Valid Values:` en-US | es-US | en-AU | fr-CA | en-GB | de-DE | pt-BR | fr-FR | it-IT | ko-KR | es-ES | en-IN | hi-IN | ar-SA | ru-RU | zh-CN | nl-NL | id-ID | ta-IN | fa-IR | en-IE | en-AB | en-WL | pt-PT | te-IN | tr-TR | de-CH | he-IL | ms-MY | ja-JP | ar-AE`   
Required: No

 **LastModifiedTime**   <a name="transcribe-Type-VocabularyFilterInfo-LastModifiedTime"></a>
The date and time that the vocabulary was last updated\.  
Type: Timestamp  
Required: No

 **VocabularyFilterName**   <a name="transcribe-Type-VocabularyFilterInfo-VocabularyFilterName"></a>
The name of the vocabulary filter\. The name must be unique in the account that holds the filter\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 200\.  
Pattern: `^[0-9a-zA-Z._-]+`   
Required: No

## See Also<a name="API_VocabularyFilterInfo_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transcribe-2017-10-26/VocabularyFilterInfo) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transcribe-2017-10-26/VocabularyFilterInfo) 
+  [AWS SDK for Java](https://docs.aws.amazon.com/goto/SdkForJava/transcribe-2017-10-26/VocabularyFilterInfo) 
+  [AWS SDK for Ruby V2](https://docs.aws.amazon.com/goto/SdkForRubyV2/transcribe-2017-10-26/VocabularyFilterInfo) 