# CallAnalyticsJobSummary<a name="API_CallAnalyticsJobSummary"></a>

Provides summary information about a call analytics job\.

## Contents<a name="API_CallAnalyticsJobSummary_Contents"></a>

 **CallAnalyticsJobName**   <a name="transcribe-Type-CallAnalyticsJobSummary-CallAnalyticsJobName"></a>
The name of the call analytics job\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 200\.  
Pattern: `^[0-9a-zA-Z._-]+`   
Required: No

 **CallAnalyticsJobStatus**   <a name="transcribe-Type-CallAnalyticsJobSummary-CallAnalyticsJobStatus"></a>
The status of the call analytics job\.  
Type: String  
Valid Values:` QUEUED | IN_PROGRESS | FAILED | COMPLETED`   
Required: No

 **CompletionTime**   <a name="transcribe-Type-CallAnalyticsJobSummary-CompletionTime"></a>
A timestamp that shows when the job was completed\.  
Type: Timestamp  
Required: No

 **CreationTime**   <a name="transcribe-Type-CallAnalyticsJobSummary-CreationTime"></a>
A timestamp that shows when the call analytics job was created\.  
Type: Timestamp  
Required: No

 **FailureReason**   <a name="transcribe-Type-CallAnalyticsJobSummary-FailureReason"></a>
If the `CallAnalyticsJobStatus` is `FAILED`, a description of the error\.  
Type: String  
Required: No

 **LanguageCode**   <a name="transcribe-Type-CallAnalyticsJobSummary-LanguageCode"></a>
The language of the transcript in the source audio file\.  
Type: String  
Valid Values:` af-ZA | ar-AE | ar-SA | cy-GB | da-DK | de-CH | de-DE | en-AB | en-AU | en-GB | en-IE | en-IN | en-US | en-WL | es-ES | es-US | fa-IR | fr-CA | fr-FR | ga-IE | gd-GB | he-IL | hi-IN | id-ID | it-IT | ja-JP | ko-KR | ms-MY | nl-NL | pt-BR | pt-PT | ru-RU | ta-IN | te-IN | tr-TR | zh-CN | zh-TW | th-TH | en-ZA | en-NZ`   
Required: No

 **StartTime**   <a name="transcribe-Type-CallAnalyticsJobSummary-StartTime"></a>
A timestamp that shows when the job began processing\.  
Type: Timestamp  
Required: No

## See Also<a name="API_CallAnalyticsJobSummary_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [ AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transcribe-2017-10-26/CallAnalyticsJobSummary) 
+  [ AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transcribe-2017-10-26/CallAnalyticsJobSummary) 
+  [ AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transcribe-2017-10-26/CallAnalyticsJobSummary) 
+  [ AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transcribe-2017-10-26/CallAnalyticsJobSummary) 