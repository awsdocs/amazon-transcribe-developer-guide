# TranscriptionJob<a name="API_TranscriptionJob"></a>

Describes an asynchronous transcription job that was created with the `StartTranscriptionJob` operation\. 

## Contents<a name="API_TranscriptionJob_Contents"></a>

 **CompletionTime**   <a name="transcribe-Type-TranscriptionJob-CompletionTime"></a>
A timestamp that shows when the job was completed\.  
Type: Timestamp  
Required: No

 **CreationTime**   <a name="transcribe-Type-TranscriptionJob-CreationTime"></a>
A timestamp that shows when the job was created\.  
Type: Timestamp  
Required: No

 **FailureReason**   <a name="transcribe-Type-TranscriptionJob-FailureReason"></a>
If the `TranscriptionJobStatus` field is `FAILED`, this field contains information about why the job failed\.  
The `FailureReason` field can contain one of the following values:  
+  `Unsupported media format` \- The media format specified in the `MediaFormat` field of the request isn't valid\. See the description of the `MediaFormat` field for a list of valid values\.
+  `The media format provided does not match the detected media format` \- The media format of the audio file doesn't match the format specified in the `MediaFormat` field in the request\. Check the media format of your media file and make sure that the two values match\.
+  `Invalid sample rate for audio file` \- The sample rate specified in the `MediaSampleRateHertz` of the request isn't valid\. The sample rate must be between 8000 and 48000 Hertz\.
+  `The sample rate provided does not match the detected sample rate` \- The sample rate in the audio file doesn't match the sample rate specified in the `MediaSampleRateHertz` field in the request\. Check the sample rate of your media file and make sure that the two values match\.
+  `Invalid file size: file size too large` \- The size of your audio file is larger than Amazon Transcribe can process\. For more information, see [Limits](https://docs.aws.amazon.com/transcribe/latest/dg/limits-guidelines.html#limits) in the *Amazon Transcribe Developer Guide*\.
+  `Invalid number of channels: number of channels too large` \- Your audio contains more channels than Amazon Transcribe is configured to process\. To request additional channels, see [Amazon Transcribe Limits](https://docs.aws.amazon.com/general/latest/gr/aws_service_limits.html#limits-amazon-transcribe) in the *Amazon Web Services General Reference*\.
Type: String  
Required: No

 **LanguageCode**   <a name="transcribe-Type-TranscriptionJob-LanguageCode"></a>
The language code for the input speech\.  
Type: String  
Valid Values:` en-US | es-US | en-AU | fr-CA | en-GB | de-DE | pt-BR | fr-FR | it-IT | ko-KR | es-ES | en-IN | hi-IN`   
Required: No

 **Media**   <a name="transcribe-Type-TranscriptionJob-Media"></a>
An object that describes the input media for the transcription job\.  
Type: [Media](API_Media.md) object  
Required: No

 **MediaFormat**   <a name="transcribe-Type-TranscriptionJob-MediaFormat"></a>
The format of the input media file\.  
Type: String  
Valid Values:` mp3 | mp4 | wav | flac`   
Required: No

 **MediaSampleRateHertz**   <a name="transcribe-Type-TranscriptionJob-MediaSampleRateHertz"></a>
The sample rate, in Hertz, of the audio track in the input media file\.   
Type: Integer  
Valid Range: Minimum value of 8000\. Maximum value of 48000\.  
Required: No

 **Settings**   <a name="transcribe-Type-TranscriptionJob-Settings"></a>
Optional settings for the transcription job\. Use these settings to turn on speaker recognition, to set the maximum number of speakers that should be identified and to specify a custom vocabulary to use when processing the transcription job\.  
Type: [Settings](API_Settings.md) object  
Required: No

 **Transcript**   <a name="transcribe-Type-TranscriptionJob-Transcript"></a>
An object that describes the output of the transcription job\.  
Type: [Transcript](API_Transcript.md) object  
Required: No

 **TranscriptionJobName**   <a name="transcribe-Type-TranscriptionJob-TranscriptionJobName"></a>
The name of the transcription job\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 200\.  
Pattern: `^[0-9a-zA-Z._-]+`   
Required: No

 **TranscriptionJobStatus**   <a name="transcribe-Type-TranscriptionJob-TranscriptionJobStatus"></a>
The status of the transcription job\.  
Type: String  
Valid Values:` IN_PROGRESS | FAILED | COMPLETED`   
Required: No

## See Also<a name="API_TranscriptionJob_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transcribe-2017-10-26/TranscriptionJob) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transcribe-2017-10-26/TranscriptionJob) 
+  [AWS SDK for Go \- Pilot](https://docs.aws.amazon.com/goto/SdkForGoPilot/transcribe-2017-10-26/TranscriptionJob) 
+  [AWS SDK for Java](https://docs.aws.amazon.com/goto/SdkForJava/transcribe-2017-10-26/TranscriptionJob) 
+  [AWS SDK for Ruby V2](https://docs.aws.amazon.com/goto/SdkForRubyV2/transcribe-2017-10-26/TranscriptionJob) 