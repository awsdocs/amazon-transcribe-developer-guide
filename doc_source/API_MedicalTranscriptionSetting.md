# MedicalTranscriptionSetting<a name="API_MedicalTranscriptionSetting"></a>

Optional settings for the [StartMedicalTranscriptionJob](API_StartMedicalTranscriptionJob.md) operation\.

## Contents<a name="API_MedicalTranscriptionSetting_Contents"></a>

 **ChannelIdentification**   <a name="transcribe-Type-MedicalTranscriptionSetting-ChannelIdentification"></a>
Instructs Amazon Transcribe Medical to process each audio channel separately and then merge the transcription output of each channel into a single transcription\.  
Amazon Transcribe Medical also produces a transcription of each item detected on an audio channel, including the start time and end time of the item and alternative transcriptions of item\. The alternative transcriptions also come with confidence scores provided by Amazon Transcribe Medical\.  
You can't set both `ShowSpeakerLabels` and `ChannelIdentification` in the same request\. If you set both, your request returns a `BadRequestException`   
Type: Boolean  
Required: No

 **MaxAlternatives**   <a name="transcribe-Type-MedicalTranscriptionSetting-MaxAlternatives"></a>
The maximum number of alternatives that you tell the service to return\. If you specify the `MaxAlternatives` field, you must set the `ShowAlternatives` field to true\.  
Type: Integer  
Valid Range: Minimum value of 2\. Maximum value of 10\.  
Required: No

 **MaxSpeakerLabels**   <a name="transcribe-Type-MedicalTranscriptionSetting-MaxSpeakerLabels"></a>
The maximum number of speakers to identify in the input audio\. If there are more speakers in the audio than this number, multiple speakers are identified as a single speaker\. If you specify the `MaxSpeakerLabels` field, you must set the `ShowSpeakerLabels` field to true\.  
Type: Integer  
Valid Range: Minimum value of 2\. Maximum value of 10\.  
Required: No

 **ShowAlternatives**   <a name="transcribe-Type-MedicalTranscriptionSetting-ShowAlternatives"></a>
Determines whether alternative transcripts are generated along with the transcript that has the highest confidence\. If you set `ShowAlternatives` field to true, you must also set the maximum number of alternatives to return in the `MaxAlternatives` field\.  
Type: Boolean  
Required: No

 **ShowSpeakerLabels**   <a name="transcribe-Type-MedicalTranscriptionSetting-ShowSpeakerLabels"></a>
Determines whether the transcription job uses speaker recognition to identify different speakers in the input audio\. Speaker recongition labels individual speakers in the audio file\. If you set the `ShowSpeakerLabels` field to true, you must also set the maximum number of speaker labels in the `MaxSpeakerLabels` field\.  
You can't set both `ShowSpeakerLabels` and `ChannelIdentification` in the same request\. If you set both, your request returns a `BadRequestException`\.  
Type: Boolean  
Required: No

## See Also<a name="API_MedicalTranscriptionSetting_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transcribe-2017-10-26/MedicalTranscriptionSetting) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transcribe-2017-10-26/MedicalTranscriptionSetting) 
+  [AWS SDK for Java](https://docs.aws.amazon.com/goto/SdkForJava/transcribe-2017-10-26/MedicalTranscriptionSetting) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transcribe-2017-10-26/MedicalTranscriptionSetting) 