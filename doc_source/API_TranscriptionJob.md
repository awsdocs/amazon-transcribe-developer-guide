# TranscriptionJob<a name="API_TranscriptionJob"></a>

Describes an asynchronous transcription job that was created with the `StartTranscriptionJob` operation\.

## Contents<a name="API_TranscriptionJob_Contents"></a>

 **CompletionTime**   <a name="transcribe-Type-TranscriptionJob-CompletionTime"></a>
Timestamp of the date and time that the job completed\.  
Type: Timestamp  
Required: No

 **CreationTime**   <a name="transcribe-Type-TranscriptionJob-CreationTime"></a>
Timestamp of the date and time that the job was created\.  
Type: Timestamp  
Required: No

 **FailureReason**   <a name="transcribe-Type-TranscriptionJob-FailureReason"></a>
If the `TranscriptionJobStatus` field is `FAILED`, this field contains information about why the job failed\.  
Type: String  
Required: No

 **LanguageCode**   <a name="transcribe-Type-TranscriptionJob-LanguageCode"></a>
The language code for the input speech\.  
Type: String  
Valid Values:` en-US | es-US`   
Required: No

 **Media**   <a name="transcribe-Type-TranscriptionJob-Media"></a>
An object that describes the input media for a transcription job\.  
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
Optional settings for the transcription job\.  
Type: [Settings](API_Settings.md) object  
Required: No

 **Transcript**   <a name="transcribe-Type-TranscriptionJob-Transcript"></a>
An object that describes the output of the transcription job\.  
Type: [Transcript](API_Transcript.md) object  
Required: No

 **TranscriptionJobName**   <a name="transcribe-Type-TranscriptionJob-TranscriptionJobName"></a>
A name to identify the transcription job\.  
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

+  [AWS SDK for C\+\+](http://docs.aws.amazon.com/goto/SdkForCpp/transcribe-2017-10-26/TranscriptionJob) 

+  [AWS SDK for Go](http://docs.aws.amazon.com/goto/SdkForGoV1/transcribe-2017-10-26/TranscriptionJob) 

+  [AWS SDK for Java](http://docs.aws.amazon.com/goto/SdkForJava/transcribe-2017-10-26/TranscriptionJob) 

+  [AWS SDK for Ruby V2](http://docs.aws.amazon.com/goto/SdkForRubyV2/transcribe-2017-10-26/TranscriptionJob) 