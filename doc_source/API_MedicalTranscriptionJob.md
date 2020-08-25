# MedicalTranscriptionJob<a name="API_MedicalTranscriptionJob"></a>

The data structure that contains the information for a medical transcription job\.

## Contents<a name="API_MedicalTranscriptionJob_Contents"></a>

 **CompletionTime**   <a name="transcribe-Type-MedicalTranscriptionJob-CompletionTime"></a>
A timestamp that shows when the job was completed\.  
Type: Timestamp  
Required: No

 **CreationTime**   <a name="transcribe-Type-MedicalTranscriptionJob-CreationTime"></a>
A timestamp that shows when the job was created\.  
Type: Timestamp  
Required: No

 **FailureReason**   <a name="transcribe-Type-MedicalTranscriptionJob-FailureReason"></a>
If the `TranscriptionJobStatus` field is `FAILED`, this field contains information about why the job failed\.  
The `FailureReason` field contains one of the following values:  
+  `Unsupported media format`\- The media format specified in the `MediaFormat` field of the request isn't valid\. See the description of the `MediaFormat` field for a list of valid values\.
+  `The media format provided does not match the detected media format`\- The media format of the audio file doesn't match the format specified in the `MediaFormat` field in the request\. Check the media format of your media file and make sure the two values match\.
+  `Invalid sample rate for audio file`\- The sample rate specified in the `MediaSampleRateHertz` of the request isn't valid\. The sample rate must be between 8000 and 48000 Hertz\.
+  `The sample rate provided does not match the detected sample rate`\- The sample rate in the audio file doesn't match the sample rate specified in the `MediaSampleRateHertz` field in the request\. Check the sample rate of your media file and make sure that the two values match\.
+  `Invalid file size: file size too large`\- The size of your audio file is larger than what Amazon Transcribe Medical can process\. For more information, see [Guidelines and Quotas](https://docs.aws.amazon.com/transcribe/latest/dg/limits-guidelines.html#limits) in the *Amazon Transcribe Medical Guide* 
+  `Invalid number of channels: number of channels too large`\- Your audio contains more channels than Amazon Transcribe Medical is configured to process\. To request additional channels, see [Amazon Transcribe Medical Endpoints and Quotas](https://docs.aws.amazon.com/general/latest/gr/transcribe-medical.html) in the *Amazon Web Services General Reference* 
Type: String  
Required: No

 **LanguageCode**   <a name="transcribe-Type-MedicalTranscriptionJob-LanguageCode"></a>
The language code for the language spoken in the source audio file\. US English \(en\-US\) is the only supported language for medical transcriptions\. Any other value you enter for language code results in a `BadRequestException` error\.  
Type: String  
Valid Values:` af-ZA | ar-AE | ar-SA | cy-GB | da-DK | de-CH | de-DE | en-AB | en-AU | en-GB | en-IE | en-IN | en-US | en-WL | es-ES | es-US | fa-IR | fr-CA | fr-FR | ga-IE | gd-GB | he-IL | hi-IN | id-ID | it-IT | ja-JP | ko-KR | ms-MY | nl-NL | pt-BR | pt-PT | ru-RU | ta-IN | te-IN | tr-TR | zh-CN`   
Required: No

 **Media**   <a name="transcribe-Type-MedicalTranscriptionJob-Media"></a>
Describes the input media file in a transcription request\.  
Type: [Media](API_Media.md) object  
Required: No

 **MediaFormat**   <a name="transcribe-Type-MedicalTranscriptionJob-MediaFormat"></a>
The format of the input media file\.  
Type: String  
Valid Values:` mp3 | mp4 | wav | flac`   
Required: No

 **MediaSampleRateHertz**   <a name="transcribe-Type-MedicalTranscriptionJob-MediaSampleRateHertz"></a>
The sample rate, in Hertz, of the source audio containing medical information\.  
If you don't specify the sample rate, Amazon Transcribe Medical determines it for you\. If you choose to specify the sample rate, it must match the rate detected by Amazon Transcribe Medical\. In most cases, you should leave the `MediaSampleHertz` blank and let Amazon Transcribe Medical determine the sample rate\.  
Type: Integer  
Valid Range: Minimum value of 8000\. Maximum value of 48000\.  
Required: No

 **MedicalTranscriptionJobName**   <a name="transcribe-Type-MedicalTranscriptionJob-MedicalTranscriptionJobName"></a>
The name for a given medical transcription job\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 200\.  
Pattern: `^[0-9a-zA-Z._-]+`   
Required: No

 **Settings**   <a name="transcribe-Type-MedicalTranscriptionJob-Settings"></a>
Object that contains [MedicalTranscriptionSetting](API_MedicalTranscriptionSetting.md) object\.  
Type: [MedicalTranscriptionSetting](API_MedicalTranscriptionSetting.md) object  
Required: No

 **Specialty**   <a name="transcribe-Type-MedicalTranscriptionJob-Specialty"></a>
The medical specialty of any clinicians providing a dictation or having a conversation\. `PRIMARYCARE` is the only available setting for this object\. This specialty enables you to generate transcriptions for the following medical fields:  
+ Family Medicine
Type: String  
Valid Values:` PRIMARYCARE`   
Required: No

 **StartTime**   <a name="transcribe-Type-MedicalTranscriptionJob-StartTime"></a>
A timestamp that shows when the job started processing\.  
Type: Timestamp  
Required: No

 **Transcript**   <a name="transcribe-Type-MedicalTranscriptionJob-Transcript"></a>
An object that contains the `MedicalTranscript`\. The `MedicalTranscript` contains the `TranscriptFileUri`\.  
Type: [MedicalTranscript](API_MedicalTranscript.md) object  
Required: No

 **TranscriptionJobStatus**   <a name="transcribe-Type-MedicalTranscriptionJob-TranscriptionJobStatus"></a>
The completion status of a medical transcription job\.  
Type: String  
Valid Values:` QUEUED | IN_PROGRESS | FAILED | COMPLETED`   
Required: No

 **Type**   <a name="transcribe-Type-MedicalTranscriptionJob-Type"></a>
The type of speech in the transcription job\. `CONVERSATION` is generally used for patient\-physician dialogues\. `DICTATION` is the setting for physicians speaking their notes after seeing a patient\. For more information, see [How Amazon Transcribe Medical Works](how-it-works-med.md)   
Type: String  
Valid Values:` CONVERSATION | DICTATION`   
Required: No

## See Also<a name="API_MedicalTranscriptionJob_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transcribe-2017-10-26/MedicalTranscriptionJob) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transcribe-2017-10-26/MedicalTranscriptionJob) 
+  [AWS SDK for Java](https://docs.aws.amazon.com/goto/SdkForJava/transcribe-2017-10-26/MedicalTranscriptionJob) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transcribe-2017-10-26/MedicalTranscriptionJob) 