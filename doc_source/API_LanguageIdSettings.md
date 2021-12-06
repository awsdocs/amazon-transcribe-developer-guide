# LanguageIdSettings<a name="API_LanguageIdSettings"></a>

Language\-specific settings that can be specified when language identification is enabled\.

## Contents<a name="API_LanguageIdSettings_Contents"></a>

 ** LanguageModelName **   <a name="transcribe-Type-LanguageIdSettings-LanguageModelName"></a>
The name of the language model you want to use when transcribing your audio\. The model you specify must have the same language codes as the transcription job; if the languages don't match, the language model isn't be applied\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 200\.  
Pattern: `^[0-9a-zA-Z._-]+`   
Required: No

 ** VocabularyFilterName **   <a name="transcribe-Type-LanguageIdSettings-VocabularyFilterName"></a>
The name of the vocabulary filter you want to use when transcribing your audio\. The filter you specify must have the same language codes as the transcription job; if the languages don't match, the vocabulary filter isn't be applied\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 200\.  
Pattern: `^[0-9a-zA-Z._-]+`   
Required: No

 ** VocabularyName **   <a name="transcribe-Type-LanguageIdSettings-VocabularyName"></a>
The name of the vocabulary you want to use when processing your transcription job\. The vocabulary you specify must have the same language codes as the transcription job; if the languages don't match, the vocabulary isn't applied\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 200\.  
Pattern: `^[0-9a-zA-Z._-]+`   
Required: No

## See Also<a name="API_LanguageIdSettings_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [ AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transcribe-2017-10-26/LanguageIdSettings) 
+  [ AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transcribe-2017-10-26/LanguageIdSettings) 
+  [ AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transcribe-2017-10-26/LanguageIdSettings) 
+  [ AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transcribe-2017-10-26/LanguageIdSettings) 