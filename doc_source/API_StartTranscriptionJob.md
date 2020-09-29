# StartTranscriptionJob<a name="API_StartTranscriptionJob"></a>

Starts an asynchronous job to transcribe speech to text\. 

## Request Syntax<a name="API_StartTranscriptionJob_RequestSyntax"></a>

```
{
   "ContentRedaction": { 
      "RedactionOutput": "string",
      "RedactionType": "string"
   },
   "IdentifyLanguage": boolean,
   "JobExecutionSettings": { 
      "AllowDeferredExecution": boolean,
      "DataAccessRoleArn": "string"
   },
   "LanguageCode": "string",
   "LanguageOptions": [ "string" ],
   "Media": { 
      "MediaFileUri": "string"
   },
   "MediaFormat": "string",
   "MediaSampleRateHertz": number,
   "ModelSettings": { 
      "LanguageModelName": "string"
   },
   "OutputBucketName": "string",
   "OutputEncryptionKMSKeyId": "string",
   "OutputKey": "string",
   "Settings": { 
      "ChannelIdentification": boolean,
      "MaxAlternatives": number,
      "MaxSpeakerLabels": number,
      "ShowAlternatives": boolean,
      "ShowSpeakerLabels": boolean,
      "VocabularyFilterMethod": "string",
      "VocabularyFilterName": "string",
      "VocabularyName": "string"
   },
   "TranscriptionJobName": "string"
}
```

## Request Parameters<a name="API_StartTranscriptionJob_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [ContentRedaction](#API_StartTranscriptionJob_RequestSyntax) **   <a name="transcribe-StartTranscriptionJob-request-ContentRedaction"></a>
An object that contains the request parameters for content redaction\.  
Type: [ContentRedaction](API_ContentRedaction.md) object  
Required: No

 ** [IdentifyLanguage](#API_StartTranscriptionJob_RequestSyntax) **   <a name="transcribe-StartTranscriptionJob-request-IdentifyLanguage"></a>
Set this field to `true` to enable automatic language identification\. Automatic language identification is disabled by default\. You receive a `BadRequestException` error if you enter a value for a `LanguageCode`\.  
Type: Boolean  
Required: No

 ** [JobExecutionSettings](#API_StartTranscriptionJob_RequestSyntax) **   <a name="transcribe-StartTranscriptionJob-request-JobExecutionSettings"></a>
Provides information about how a transcription job is executed\. Use this field to indicate that the job can be queued for deferred execution if the concurrency limit is reached and there are no slots available to immediately run the job\.  
Type: [JobExecutionSettings](API_JobExecutionSettings.md) object  
Required: No

 ** [LanguageCode](#API_StartTranscriptionJob_RequestSyntax) **   <a name="transcribe-StartTranscriptionJob-request-LanguageCode"></a>
The language code for the language used in the input media file\.  
Type: String  
Valid Values:` af-ZA | ar-AE | ar-SA | cy-GB | da-DK | de-CH | de-DE | en-AB | en-AU | en-GB | en-IE | en-IN | en-US | en-WL | es-ES | es-US | fa-IR | fr-CA | fr-FR | ga-IE | gd-GB | he-IL | hi-IN | id-ID | it-IT | ja-JP | ko-KR | ms-MY | nl-NL | pt-BR | pt-PT | ru-RU | ta-IN | te-IN | tr-TR | zh-CN`   
Required: No

 ** [LanguageOptions](#API_StartTranscriptionJob_RequestSyntax) **   <a name="transcribe-StartTranscriptionJob-request-LanguageOptions"></a>
An object containing a list of languages that might be present in your collection of audio files\. Automatic language identification chooses a language that best matches the source audio from that list\.  
Type: Array of strings  
Array Members: Minimum number of 2 items\.  
Valid Values:` af-ZA | ar-AE | ar-SA | cy-GB | da-DK | de-CH | de-DE | en-AB | en-AU | en-GB | en-IE | en-IN | en-US | en-WL | es-ES | es-US | fa-IR | fr-CA | fr-FR | ga-IE | gd-GB | he-IL | hi-IN | id-ID | it-IT | ja-JP | ko-KR | ms-MY | nl-NL | pt-BR | pt-PT | ru-RU | ta-IN | te-IN | tr-TR | zh-CN`   
Required: No

 ** [Media](#API_StartTranscriptionJob_RequestSyntax) **   <a name="transcribe-StartTranscriptionJob-request-Media"></a>
An object that describes the input media for a transcription job\.  
Type: [Media](API_Media.md) object  
Required: Yes

 ** [MediaFormat](#API_StartTranscriptionJob_RequestSyntax) **   <a name="transcribe-StartTranscriptionJob-request-MediaFormat"></a>
The format of the input media file\.  
Type: String  
Valid Values:` mp3 | mp4 | wav | flac | ogg | amr | webm`   
Required: No

 ** [MediaSampleRateHertz](#API_StartTranscriptionJob_RequestSyntax) **   <a name="transcribe-StartTranscriptionJob-request-MediaSampleRateHertz"></a>
The sample rate, in Hertz, of the audio track in the input media file\.   
If you do not specify the media sample rate, Amazon Transcribe determines the sample rate\. If you specify the sample rate, it must match the sample rate detected by Amazon Transcribe\. In most cases, you should leave the `MediaSampleRateHertz` field blank and let Amazon Transcribe determine the sample rate\.  
Type: Integer  
Valid Range: Minimum value of 8000\. Maximum value of 48000\.  
Required: No

 ** [ModelSettings](#API_StartTranscriptionJob_RequestSyntax) **   <a name="transcribe-StartTranscriptionJob-request-ModelSettings"></a>
Choose the custom language model you use for your transcription job in this parameter\.  
Type: [ModelSettings](API_ModelSettings.md) object  
Required: No

 ** [OutputBucketName](#API_StartTranscriptionJob_RequestSyntax) **   <a name="transcribe-StartTranscriptionJob-request-OutputBucketName"></a>
The location where the transcription is stored\.  
If you set the `OutputBucketName`, Amazon Transcribe puts the transcript in the specified S3 bucket\. When you call the [GetTranscriptionJob](API_GetTranscriptionJob.md) operation, the operation returns this location in the `TranscriptFileUri` field\. If you enable content redaction, the redacted transcript appears in `RedactedTranscriptFileUri`\. If you enable content redaction and choose to output an unredacted transcript, that transcript's location still appears in the `TranscriptFileUri`\. The S3 bucket must have permissions that allow Amazon Transcribe to put files in the bucket\. For more information, see [Permissions Required for IAM User Roles](https://docs.aws.amazon.com/transcribe/latest/dg/security_iam_id-based-policy-examples.html#auth-role-iam-user)\.  
You can specify an AWS Key Management Service \(KMS\) key to encrypt the output of your transcription using the `OutputEncryptionKMSKeyId` parameter\. If you don't specify a KMS key, Amazon Transcribe uses the default Amazon S3 key for server\-side encryption of transcripts that are placed in your S3 bucket\.  
If you don't set the `OutputBucketName`, Amazon Transcribe generates a pre\-signed URL, a shareable URL that provides secure access to your transcription, and returns it in the `TranscriptFileUri` field\. Use this URL to download the transcription\.  
Type: String  
Length Constraints: Maximum length of 64\.  
Pattern: `[a-z0-9][\.\-a-z0-9]{1,61}[a-z0-9]`   
Required: No

 ** [OutputEncryptionKMSKeyId](#API_StartTranscriptionJob_RequestSyntax) **   <a name="transcribe-StartTranscriptionJob-request-OutputEncryptionKMSKeyId"></a>
The Amazon Resource Name \(ARN\) of the AWS Key Management Service \(KMS\) key used to encrypt the output of the transcription job\. The user calling the `StartTranscriptionJob` operation must have permission to use the specified KMS key\.  
You can use either of the following to identify a KMS key in the current account:  
+ KMS Key ID: "1234abcd\-12ab\-34cd\-56ef\-1234567890ab"
+ KMS Key Alias: "alias/ExampleAlias"
You can use either of the following to identify a KMS key in the current account or another account:  
+ Amazon Resource Name \(ARN\) of a KMS Key: "arn:aws:kms:region:account ID:key/1234abcd\-12ab\-34cd\-56ef\-1234567890ab"
+ ARN of a KMS Key Alias: "arn:aws:kms:region:account ID:alias/ExampleAlias"
If you don't specify an encryption key, the output of the transcription job is encrypted with the default Amazon S3 key \(SSE\-S3\)\.   
If you specify a KMS key to encrypt your output, you must also specify an output location in the `OutputBucketName` parameter\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 2048\.  
Pattern: `^[A-Za-z0-9][A-Za-z0-9:_/+=,@.-]{0,2048}$`   
Required: No

 ** [OutputKey](#API_StartTranscriptionJob_RequestSyntax) **   <a name="transcribe-StartTranscriptionJob-request-OutputKey"></a>
You can specify a location in an Amazon S3 bucket to store the output of your transcription job\.  
If you don't specify an output key, Amazon Transcribe stores the output of your transcription job in the Amazon S3 bucket you specified\. By default, the object key is "your\-transcription\-job\-name\.json"\.  
You can use output keys to specify the Amazon S3 prefix and file name of the transcription output\. For example, specifying the Amazon S3 prefix, "folder1/folder2/", as an output key would lead to the output being stored as "folder1/folder2/your\-transcription\-job\-name\.json"\. If you specify "my\-other\-job\-name\.json" as the output key, the object key is changed to "my\-other\-job\-name\.json"\. You can use an output key to change both the prefix and the file name, for example "folder/my\-other\-job\-name\.json"\.  
If you specify an output key, you must also specify an S3 bucket in the `OutputBucketName` parameter\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 1024\.  
Pattern: `[a-zA-Z0-9-_.!*'()/]{1,1024}$`   
Required: No

 ** [Settings](#API_StartTranscriptionJob_RequestSyntax) **   <a name="transcribe-StartTranscriptionJob-request-Settings"></a>
A `Settings` object that provides optional settings for a transcription job\.  
Type: [Settings](API_Settings.md) object  
Required: No

 ** [TranscriptionJobName](#API_StartTranscriptionJob_RequestSyntax) **   <a name="transcribe-StartTranscriptionJob-request-TranscriptionJobName"></a>
The name of the job\. You can't use the strings "`.`" or "`..`" by themselves as the job name\. The name must also be unique within an AWS account\. If you try to create a transcription job with the same name as a previous transcription job, you get a `ConflictException` error\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 200\.  
Pattern: `^[0-9a-zA-Z._-]+`   
Required: Yes

## Response Syntax<a name="API_StartTranscriptionJob_ResponseSyntax"></a>

```
{
   "TranscriptionJob": { 
      "CompletionTime": number,
      "ContentRedaction": { 
         "RedactionOutput": "string",
         "RedactionType": "string"
      },
      "CreationTime": number,
      "FailureReason": "string",
      "IdentifiedLanguageScore": number,
      "IdentifyLanguage": boolean,
      "JobExecutionSettings": { 
         "AllowDeferredExecution": boolean,
         "DataAccessRoleArn": "string"
      },
      "LanguageCode": "string",
      "LanguageOptions": [ "string" ],
      "Media": { 
         "MediaFileUri": "string"
      },
      "MediaFormat": "string",
      "MediaSampleRateHertz": number,
      "ModelSettings": { 
         "LanguageModelName": "string"
      },
      "Settings": { 
         "ChannelIdentification": boolean,
         "MaxAlternatives": number,
         "MaxSpeakerLabels": number,
         "ShowAlternatives": boolean,
         "ShowSpeakerLabels": boolean,
         "VocabularyFilterMethod": "string",
         "VocabularyFilterName": "string",
         "VocabularyName": "string"
      },
      "StartTime": number,
      "Transcript": { 
         "RedactedTranscriptFileUri": "string",
         "TranscriptFileUri": "string"
      },
      "TranscriptionJobName": "string",
      "TranscriptionJobStatus": "string"
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
Your request didn't pass one or more validation tests\. For example, if the entity that you're trying to delete doesn't exist or if it is in a non\-terminal state \(for example, it's "in progress"\)\. See the exception `Message` field for more information\.  
HTTP Status Code: 400

 **ConflictException**   
There is already a resource with that name\.  
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
+  [AWS SDK for Java](https://docs.aws.amazon.com/goto/SdkForJava/transcribe-2017-10-26/StartTranscriptionJob) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/transcribe-2017-10-26/StartTranscriptionJob) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/transcribe-2017-10-26/StartTranscriptionJob) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/transcribe-2017-10-26/StartTranscriptionJob) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transcribe-2017-10-26/StartTranscriptionJob) 