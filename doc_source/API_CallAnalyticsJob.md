# CallAnalyticsJob<a name="API_CallAnalyticsJob"></a>

Describes an asynchronous analytics job that was created with the `StartAnalyticsJob` operation\.

## Contents<a name="API_CallAnalyticsJob_Contents"></a>

 ** CallAnalyticsJobName **   <a name="transcribe-Type-CallAnalyticsJob-CallAnalyticsJobName"></a>
The name of the call analytics job\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 200\.  
Pattern: `^[0-9a-zA-Z._-]+`   
Required: No

 ** CallAnalyticsJobStatus **   <a name="transcribe-Type-CallAnalyticsJob-CallAnalyticsJobStatus"></a>
The status of the analytics job\.  
Type: String  
Valid Values:` QUEUED | IN_PROGRESS | FAILED | COMPLETED`   
Required: No

 ** ChannelDefinitions **   <a name="transcribe-Type-CallAnalyticsJob-ChannelDefinitions"></a>
Shows numeric values to indicate the channel assigned to the agent's audio and the channel assigned to the customer's audio\.   
Type: Array of [ ChannelDefinition ](API_ChannelDefinition.md) objects  
Array Members: Fixed number of 2 items\.  
Required: No

 ** CompletionTime **   <a name="transcribe-Type-CallAnalyticsJob-CompletionTime"></a>
A timestamp that shows when the analytics job was completed\.  
Type: Timestamp  
Required: No

 ** CreationTime **   <a name="transcribe-Type-CallAnalyticsJob-CreationTime"></a>
A timestamp that shows when the analytics job was created\.  
Type: Timestamp  
Required: No

 ** DataAccessRoleArn **   <a name="transcribe-Type-CallAnalyticsJob-DataAccessRoleArn"></a>
The Amazon Resource Number \(ARN\) that you use to get access to the analytics job\.  
Type: String  
Length Constraints: Minimum length of 20\. Maximum length of 2048\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso-{0,1}[a-z]{0,1}):iam::[0-9]{0,63}:role/[A-Za-z0-9:_/+=,@.-]{0,1024}$`   
Required: No

 ** FailureReason **   <a name="transcribe-Type-CallAnalyticsJob-FailureReason"></a>
If the `AnalyticsJobStatus` is `FAILED`, this field contains information about why the job failed\.  
The `FailureReason` field can contain one of the following values:  
+  `Unsupported media format`: The media format specified in the `MediaFormat` field of the request isn't valid\. See the description of the `MediaFormat` field for a list of valid values\.
+  `The media format provided does not match the detected media format`: The media format of the audio file doesn't match the format specified in the `MediaFormat` field in the request\. Check the media format of your media file and make sure the two values match\.
+  `Invalid sample rate for audio file`: The sample rate specified in the `MediaSampleRateHertz` of the request isn't valid\. The sample rate must be between 8,000 and 48,000 Hertz\.
+  `The sample rate provided does not match the detected sample rate`: The sample rate in the audio file doesn't match the sample rate specified in the `MediaSampleRateHertz` field in the request\. Check the sample rate of your media file and make sure that the two values match\.
+  `Invalid file size: file size too large`: The size of your audio file is larger than what Amazon Transcribe Medical can process\. For more information, see *Guidelines and Quotas* in the Amazon Transcribe Medical Guide\.
+  `Invalid number of channels: number of channels too large`: Your audio contains more channels than Amazon Transcribe Medical is configured to process\. To request additional channels, see Amazon Transcribe Medical Endpoints and Quotas in the [Amazon Web Services General Reference](https://docs.aws.amazon.com/general/latest/gr/Welcome.html)\.
Type: String  
Required: No

 ** IdentifiedLanguageScore **   <a name="transcribe-Type-CallAnalyticsJob-IdentifiedLanguageScore"></a>
A value between zero and one that Amazon Transcribe assigned to the language that it identified in the source audio\. This value appears only when you don't provide a single language code\. Larger values indicate that Amazon Transcribe has higher confidence in the language that it identified  
Type: Float  
Required: No

 ** LanguageCode **   <a name="transcribe-Type-CallAnalyticsJob-LanguageCode"></a>
If you know the language spoken between the customer and the agent, specify a language code for this field\.  
If you don't know the language, you can leave this field blank, and Amazon Transcribe will use machine learning to automatically identify the language\. To improve the accuracy of language identification, you can provide an array containing the possible language codes for the language spoken in your audio\. Refer to [Supported languages and language\-specific features](https://docs.aws.amazon.com/transcribe/latest/dg/how-it-works.html) for additional information\.  
Type: String  
Valid Values:` af-ZA | ar-AE | ar-SA | cy-GB | da-DK | de-CH | de-DE | en-AB | en-AU | en-GB | en-IE | en-IN | en-US | en-WL | es-ES | es-US | fa-IR | fr-CA | fr-FR | ga-IE | gd-GB | he-IL | hi-IN | id-ID | it-IT | ja-JP | ko-KR | ms-MY | nl-NL | pt-BR | pt-PT | ru-RU | ta-IN | te-IN | tr-TR | zh-CN | zh-TW | th-TH | en-ZA | en-NZ`   
Required: No

 ** Media **   <a name="transcribe-Type-CallAnalyticsJob-Media"></a>
Describes the input media file in a transcription request\.  
Type: [ Media ](API_Media.md) object  
Required: No

 ** MediaFormat **   <a name="transcribe-Type-CallAnalyticsJob-MediaFormat"></a>
The format of the input audio file\. Note: for call analytics jobs, only the following media formats are supported: MP3, MP4, WAV, FLAC, OGG, and WebM\.   
Type: String  
Valid Values:` mp3 | mp4 | wav | flac | ogg | amr | webm`   
Required: No

 ** MediaSampleRateHertz **   <a name="transcribe-Type-CallAnalyticsJob-MediaSampleRateHertz"></a>
The sample rate, in Hertz, of the audio\.  
Type: Integer  
Valid Range: Minimum value of 8000\. Maximum value of 48000\.  
Required: No

 ** Settings **   <a name="transcribe-Type-CallAnalyticsJob-Settings"></a>
Provides information about the settings used to run a transcription job\.  
Type: [ CallAnalyticsJobSettings ](API_CallAnalyticsJobSettings.md) object  
Required: No

 ** StartTime **   <a name="transcribe-Type-CallAnalyticsJob-StartTime"></a>
A timestamp that shows when the analytics job started processing\.  
Type: Timestamp  
Required: No

 ** Transcript **   <a name="transcribe-Type-CallAnalyticsJob-Transcript"></a>
Identifies the location of a transcription\.  
Type: [ Transcript ](API_Transcript.md) object  
Required: No

## See Also<a name="API_CallAnalyticsJob_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [ AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transcribe-2017-10-26/CallAnalyticsJob) 
+  [ AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transcribe-2017-10-26/CallAnalyticsJob) 
+  [ AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transcribe-2017-10-26/CallAnalyticsJob) 
+  [ AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transcribe-2017-10-26/CallAnalyticsJob) 