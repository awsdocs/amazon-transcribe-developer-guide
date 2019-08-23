# StartTranscriptionJob<a name="API_StartTranscriptionJob"></a>

Starts an asynchronous job to transcribe speech to text\. 

## Request Syntax<a name="API_StartTranscriptionJob_RequestSyntax"></a>

```
{
   "[LanguageCode](#transcribe-StartTranscriptionJob-request-LanguageCode)": "string",
   "[Media](#transcribe-StartTranscriptionJob-request-Media)": { 
      "[MediaFileUri](API_Media.md#transcribe-Type-Media-MediaFileUri)": "string"
   },
   "[MediaFormat](#transcribe-StartTranscriptionJob-request-MediaFormat)": "string",
   "[MediaSampleRateHertz](#transcribe-StartTranscriptionJob-request-MediaSampleRateHertz)": number,
   "[OutputBucketName](#transcribe-StartTranscriptionJob-request-OutputBucketName)": "string",
   "[Settings](#transcribe-StartTranscriptionJob-request-Settings)": { 
      "[ChannelIdentification](API_Settings.md#transcribe-Type-Settings-ChannelIdentification)": boolean,
      "[MaxSpeakerLabels](API_Settings.md#transcribe-Type-Settings-MaxSpeakerLabels)": number,
      "[ShowSpeakerLabels](API_Settings.md#transcribe-Type-Settings-ShowSpeakerLabels)": boolean,
      "[VocabularyName](API_Settings.md#transcribe-Type-Settings-VocabularyName)": "string"
   },
   "[TranscriptionJobName](#transcribe-StartTranscriptionJob-request-TranscriptionJobName)": "string"
}
```

## Request Parameters<a name="API_StartTranscriptionJob_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [LanguageCode](#API_StartTranscriptionJob_RequestSyntax) **   <a name="transcribe-StartTranscriptionJob-request-LanguageCode"></a>
The language code for the language used in the input media file\.  
Type: String  
Valid Values:` en-US | es-US | en-AU | fr-CA | en-GB | de-DE | pt-BR | fr-FR | it-IT | ko-KR | es-ES | en-IN | hi-IN | ar-SA | ru-RU | zh-CN`   
Required: Yes

 ** [Media](#API_StartTranscriptionJob_RequestSyntax) **   <a name="transcribe-StartTranscriptionJob-request-Media"></a>
An object that describes the input media for a transcription job\.  
Type: [Media](API_Media.md) object  
Required: Yes

 ** [MediaFormat](#API_StartTranscriptionJob_RequestSyntax) **   <a name="transcribe-StartTranscriptionJob-request-MediaFormat"></a>
The format of the input media file\.  
Type: String  
Valid Values:` mp3 | mp4 | wav | flac`   
Required: No

 ** [MediaSampleRateHertz](#API_StartTranscriptionJob_RequestSyntax) **   <a name="transcribe-StartTranscriptionJob-request-MediaSampleRateHertz"></a>
The sample rate, in Hertz, of the audio track in the input media file\.   
If you do not specify the media sample rate, Amazon Transcribe determines the sample rate\. If you specify the sample rate, it must match the sample rate detected by Amazon Transcribe\. In most cases, you should leave the `MediaSampleRateHertz` field blank and let Amazon Transcribe determine the sample rate\.  
Type: Integer  
Valid Range: Minimum value of 8000\. Maximum value of 48000\.  
Required: No

 ** [OutputBucketName](#API_StartTranscriptionJob_RequestSyntax) **   <a name="transcribe-StartTranscriptionJob-request-OutputBucketName"></a>
The location where the transcription is stored\.  
If you set the `OutputBucketName`, Amazon Transcribe puts the transcription in the specified S3 bucket\. When you call the [GetTranscriptionJob](API_GetTranscriptionJob.md) operation, the operation returns this location in the `TranscriptFileUri` field\. The S3 bucket must have permissions that allow Amazon Transcribe to put files in the bucket\. For more information, see [Permissions Required for IAM User Roles](https://docs.aws.amazon.com/transcribe/latest/dg/security_iam_id-based-policy-examples.html#auth-role-iam-user)\.  
Amazon Transcribe uses the default Amazon S3 key for server\-side encryption of transcripts that are placed in your S3 bucket\. You can't specify your own encryption key\.  
If you don't set the `OutputBucketName`, Amazon Transcribe generates a pre\-signed URL, a shareable URL that provides secure access to your transcription, and returns it in the `TranscriptFileUri` field\. Use this URL to download the transcription\.  
Type: String  
Pattern: `[a-z0-9][\.\-a-z0-9]{1,61}[a-z0-9]`   
Required: No

 ** [Settings](#API_StartTranscriptionJob_RequestSyntax) **   <a name="transcribe-StartTranscriptionJob-request-Settings"></a>
A `Settings` object that provides optional settings for a transcription job\.  
Type: [Settings](API_Settings.md) object  
Required: No

 ** [TranscriptionJobName](#API_StartTranscriptionJob_RequestSyntax) **   <a name="transcribe-StartTranscriptionJob-request-TranscriptionJobName"></a>
The name of the job\. Note that you can't use the strings "\." or "\.\." by themselves as the job name\. The name must also be unique within an AWS account\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 200\.  
Pattern: `^[0-9a-zA-Z._-]+`   
Required: Yes

## Response Syntax<a name="API_StartTranscriptionJob_ResponseSyntax"></a>

```
{
   "[TranscriptionJob](#transcribe-StartTranscriptionJob-response-TranscriptionJob)": { 
      "[CompletionTime](API_TranscriptionJob.md#transcribe-Type-TranscriptionJob-CompletionTime)": number,
      "[CreationTime](API_TranscriptionJob.md#transcribe-Type-TranscriptionJob-CreationTime)": number,
      "[FailureReason](API_TranscriptionJob.md#transcribe-Type-TranscriptionJob-FailureReason)": "string",
      "[LanguageCode](API_TranscriptionJob.md#transcribe-Type-TranscriptionJob-LanguageCode)": "string",
      "[Media](API_TranscriptionJob.md#transcribe-Type-TranscriptionJob-Media)": { 
         "[MediaFileUri](API_Media.md#transcribe-Type-Media-MediaFileUri)": "string"
      },
      "[MediaFormat](API_TranscriptionJob.md#transcribe-Type-TranscriptionJob-MediaFormat)": "string",
      "[MediaSampleRateHertz](API_TranscriptionJob.md#transcribe-Type-TranscriptionJob-MediaSampleRateHertz)": number,
      "[Settings](API_TranscriptionJob.md#transcribe-Type-TranscriptionJob-Settings)": { 
         "[ChannelIdentification](API_Settings.md#transcribe-Type-Settings-ChannelIdentification)": boolean,
         "[MaxSpeakerLabels](API_Settings.md#transcribe-Type-Settings-MaxSpeakerLabels)": number,
         "[ShowSpeakerLabels](API_Settings.md#transcribe-Type-Settings-ShowSpeakerLabels)": boolean,
         "[VocabularyName](API_Settings.md#transcribe-Type-Settings-VocabularyName)": "string"
      },
      "[Transcript](API_TranscriptionJob.md#transcribe-Type-TranscriptionJob-Transcript)": { 
         "[TranscriptFileUri](API_Transcript.md#transcribe-Type-Transcript-TranscriptFileUri)": "string"
      },
      "[TranscriptionJobName](API_TranscriptionJob.md#transcribe-Type-TranscriptionJob-TranscriptionJobName)": "string",
      "[TranscriptionJobStatus](API_TranscriptionJob.md#transcribe-Type-TranscriptionJob-TranscriptionJobStatus)": "string"
   }
}
```

## Response Elements<a name="API_StartTranscriptionJob_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [TranscriptionJob](#API_StartTranscriptionJob_ResponseSyntax) **   <a name="transcribe-StartTranscriptionJob-response-TranscriptionJob"></a>
An object containing details of the asynchronous transcription job\.  
Type: [TranscriptionJob](API_TranscriptionJob.md) object

## Errors<a name="API_StartTranscriptionJob_Errors"></a>

For information about the errors that are common to all actions, see [Common Errors](CommonErrors.md)\.

 **BadRequestException**   
Your request didn't pass one or more validation tests\. For example, if the transcription you're trying to delete doesn't exist or if it is in a non\-terminal state \(for example, it's "in progress"\)\. See the exception `Message` field for more information\.  
HTTP Status Code: 400

 **ConflictException**   
When you are using the `StartTranscriptionJob` operation, the `JobName` field is a duplicate of a previously entered job name\. Resend your request with a different name\.  
When you are using the `UpdateVocabulary` operation, there are two jobs running at the same time\. Resend the second request later\.  
HTTP Status Code: 400

 **InternalFailureException**   
There was an internal error\. Check the error message and try your request again\.  
HTTP Status Code: 500

 **LimitExceededException**   
Either you have sent too many requests or your input file is too long\. Wait before you resend your request, or use a smaller file and resend the request\.  
HTTP Status Code: 400

## See Also<a name="API_StartTranscriptionJob_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/transcribe-2017-10-26/StartTranscriptionJob) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/transcribe-2017-10-26/StartTranscriptionJob) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transcribe-2017-10-26/StartTranscriptionJob) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transcribe-2017-10-26/StartTranscriptionJob) 
+  [AWS SDK for Go \- Pilot](https://docs.aws.amazon.com/goto/SdkForGoPilot/transcribe-2017-10-26/StartTranscriptionJob) 
+  [AWS SDK for Java](https://docs.aws.amazon.com/goto/SdkForJava/transcribe-2017-10-26/StartTranscriptionJob) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/transcribe-2017-10-26/StartTranscriptionJob) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/transcribe-2017-10-26/StartTranscriptionJob) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/transcribe-2017-10-26/StartTranscriptionJob) 
+  [AWS SDK for Ruby V2](https://docs.aws.amazon.com/goto/SdkForRubyV2/transcribe-2017-10-26/StartTranscriptionJob) 