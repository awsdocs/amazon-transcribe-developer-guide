# MedicalTranscriptionJobSummary<a name="API_MedicalTranscriptionJobSummary"></a>

Provides summary information about a transcription job\.

## Contents<a name="API_MedicalTranscriptionJobSummary_Contents"></a>

 **CompletionTime**   <a name="transcribe-Type-MedicalTranscriptionJobSummary-CompletionTime"></a>
A timestamp that shows when the job was completed\.  
Type: Timestamp  
Required: No

 **CreationTime**   <a name="transcribe-Type-MedicalTranscriptionJobSummary-CreationTime"></a>
A timestamp that shows when the medical transcription job was created\.  
Type: Timestamp  
Required: No

 **FailureReason**   <a name="transcribe-Type-MedicalTranscriptionJobSummary-FailureReason"></a>
If the `TranscriptionJobStatus` field is `FAILED`, a description of the error\.  
Type: String  
Required: No

 **LanguageCode**   <a name="transcribe-Type-MedicalTranscriptionJobSummary-LanguageCode"></a>
The language of the transcript in the source audio file\.  
Type: String  
Valid Values:` af-ZA | ar-AE | ar-SA | cy-GB | da-DK | de-CH | de-DE | en-AB | en-AU | en-GB | en-IE | en-IN | en-US | en-WL | es-ES | es-US | fa-IR | fr-CA | fr-FR | ga-IE | gd-GB | he-IL | hi-IN | id-ID | it-IT | ja-JP | ko-KR | ms-MY | nl-NL | pt-BR | pt-PT | ru-RU | ta-IN | te-IN | tr-TR | zh-CN`   
Required: No

 **MedicalTranscriptionJobName**   <a name="transcribe-Type-MedicalTranscriptionJobSummary-MedicalTranscriptionJobName"></a>
The name of a medical transcription job\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 200\.  
Pattern: `^[0-9a-zA-Z._-]+`   
Required: No

 **OutputLocationType**   <a name="transcribe-Type-MedicalTranscriptionJobSummary-OutputLocationType"></a>
Indicates the location of the transcription job's output\.  
The `CUSTOMER_BUCKET` is the S3 location provided in the `OutputBucketName` field when the   
Type: String  
Valid Values:` CUSTOMER_BUCKET | SERVICE_BUCKET`   
Required: No

 **Specialty**   <a name="transcribe-Type-MedicalTranscriptionJobSummary-Specialty"></a>
The medical specialty of the transcription job\. `Primary care` is the only valid value\.  
Type: String  
Valid Values:` PRIMARYCARE`   
Required: No

 **StartTime**   <a name="transcribe-Type-MedicalTranscriptionJobSummary-StartTime"></a>
A timestamp that shows when the job began processing\.  
Type: Timestamp  
Required: No

 **TranscriptionJobStatus**   <a name="transcribe-Type-MedicalTranscriptionJobSummary-TranscriptionJobStatus"></a>
The status of the medical transcription job\.  
Type: String  
Valid Values:` QUEUED | IN_PROGRESS | FAILED | COMPLETED`   
Required: No

 **Type**   <a name="transcribe-Type-MedicalTranscriptionJobSummary-Type"></a>
The speech of the clinician in the input audio\.  
Type: String  
Valid Values:` CONVERSATION | DICTATION`   
Required: No

## See Also<a name="API_MedicalTranscriptionJobSummary_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transcribe-2017-10-26/MedicalTranscriptionJobSummary) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transcribe-2017-10-26/MedicalTranscriptionJobSummary) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transcribe-2017-10-26/MedicalTranscriptionJobSummary) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transcribe-2017-10-26/MedicalTranscriptionJobSummary) 