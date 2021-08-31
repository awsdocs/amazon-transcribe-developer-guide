# CallAnalyticsJobSettings<a name="API_CallAnalyticsJobSettings"></a>

Provides optional settings for the `CallAnalyticsJob` operation\. 

## Contents<a name="API_CallAnalyticsJobSettings_Contents"></a>

 ** ContentRedaction **   <a name="transcribe-Type-CallAnalyticsJobSettings-ContentRedaction"></a>
Settings for content redaction within a transcription job\.  
Type: [ ContentRedaction ](API_ContentRedaction.md) object  
Required: No

 ** LanguageModelName **   <a name="transcribe-Type-CallAnalyticsJobSettings-LanguageModelName"></a>
The structure used to describe a custom language model\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 200\.  
Pattern: `^[0-9a-zA-Z._-]+`   
Required: No

 ** LanguageOptions **   <a name="transcribe-Type-CallAnalyticsJobSettings-LanguageOptions"></a>
When you run a call analytics job, you can specify the language spoken in the audio, or you can have Amazon Transcribe identify the language for you\.  
To specify a language, specify an array with one language code\. If you don't know the language, you can leave this field blank and Amazon Transcribe will use machine learning to identify the language for you\. To improve the ability of Amazon Transcribe to correctly identify the language, you can provide an array of the languages that can be present in the audio\. Refer to [Supported languages and language\-specific features](https://docs.aws.amazon.com/transcribe/latest/dg/how-it-works.html) for additional information\.  
Type: Array of strings  
Array Members: Minimum number of 1 item\.  
Valid Values:` af-ZA | ar-AE | ar-SA | cy-GB | da-DK | de-CH | de-DE | en-AB | en-AU | en-GB | en-IE | en-IN | en-US | en-WL | es-ES | es-US | fa-IR | fr-CA | fr-FR | ga-IE | gd-GB | he-IL | hi-IN | id-ID | it-IT | ja-JP | ko-KR | ms-MY | nl-NL | pt-BR | pt-PT | ru-RU | ta-IN | te-IN | tr-TR | zh-CN | zh-TW | th-TH | en-ZA | en-NZ`   
Required: No

 ** VocabularyFilterMethod **   <a name="transcribe-Type-CallAnalyticsJobSettings-VocabularyFilterMethod"></a>
Set to mask to remove filtered text from the transcript and replace it with three asterisks \("\*\*\*"\) as placeholder text\. Set to `remove` to remove filtered text from the transcript without using placeholder text\. Set to `tag` to mark the word in the transcription output that matches the vocabulary filter\. When you set the filter method to `tag`, the words matching your vocabulary filter are not masked or removed\.  
Type: String  
Valid Values:` remove | mask | tag`   
Required: No

 ** VocabularyFilterName **   <a name="transcribe-Type-CallAnalyticsJobSettings-VocabularyFilterName"></a>
The name of the vocabulary filter to use when running a call analytics job\. The filter that you specify must have the same language code as the analytics job\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 200\.  
Pattern: `^[0-9a-zA-Z._-]+`   
Required: No

 ** VocabularyName **   <a name="transcribe-Type-CallAnalyticsJobSettings-VocabularyName"></a>
The name of a vocabulary to use when processing the call analytics job\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 200\.  
Pattern: `^[0-9a-zA-Z._-]+`   
Required: No

## See Also<a name="API_CallAnalyticsJobSettings_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [ AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transcribe-2017-10-26/CallAnalyticsJobSettings) 
+  [ AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transcribe-2017-10-26/CallAnalyticsJobSettings) 
+  [ AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transcribe-2017-10-26/CallAnalyticsJobSettings) 
+  [ AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transcribe-2017-10-26/CallAnalyticsJobSettings) 