# Settings<a name="API_Settings"></a>

Provides optional settings for the `StartTranscriptionJob` operation\.

## Contents<a name="API_Settings_Contents"></a>

 **ChannelIdentification**   <a name="transcribe-Type-Settings-ChannelIdentification"></a>
Instructs Amazon Transcribe to process each audio channel separately and then merge the transcription output of each channel into a single transcription\.   
Amazon Transcribe also produces a transcription of each item detected on an audio channel, including the start time and end time of the item and alternative transcriptions of the item including the confidence that Amazon Transcribe has in the transcription\.  
You can't set both `ShowSpeakerLabels` and `ChannelIdentification` in the same request\. If you set both, your request returns a `BadRequestException`\.  
Type: Boolean  
Required: No

 **MaxSpeakerLabels**   <a name="transcribe-Type-Settings-MaxSpeakerLabels"></a>
The maximum number of speakers to identify in the input audio\. If there are more speakers in the audio than this number, multiple speakers will be identified as a single speaker\. If you specify the `MaxSpeakerLabels` field, you must set the `ShowSpeakerLabels` field to true\.  
Type: Integer  
Valid Range: Minimum value of 2\. Maximum value of 10\.  
Required: No

 **ShowSpeakerLabels**   <a name="transcribe-Type-Settings-ShowSpeakerLabels"></a>
Determines whether the transcription job uses speaker recognition to identify different speakers in the input audio\. Speaker recognition labels individual speakers in the audio file\. If you set the `ShowSpeakerLabels` field to true, you must also set the maximum number of speaker labels `MaxSpeakerLabels` field\.  
You can't set both `ShowSpeakerLabels` and `ChannelIdentification` in the same request\. If you set both, your request returns a `BadRequestException`\.  
Type: Boolean  
Required: No

 **VocabularyName**   <a name="transcribe-Type-Settings-VocabularyName"></a>
The name of a vocabulary to use when processing the transcription job\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 200\.  
Pattern: `^[0-9a-zA-Z._-]+`   
Required: No

## See Also<a name="API_Settings_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transcribe-2017-10-26/Settings) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transcribe-2017-10-26/Settings) 
+  [AWS SDK for Java](https://docs.aws.amazon.com/goto/SdkForJava/transcribe-2017-10-26/Settings) 
+  [AWS SDK for Ruby V2](https://docs.aws.amazon.com/goto/SdkForRubyV2/transcribe-2017-10-26/Settings) 