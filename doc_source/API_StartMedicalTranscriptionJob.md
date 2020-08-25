# StartMedicalTranscriptionJob<a name="API_StartMedicalTranscriptionJob"></a>

Starts a batch job to transcribe medical speech to text\.

## Request Syntax<a name="API_StartMedicalTranscriptionJob_RequestSyntax"></a>

```
{
   "LanguageCode": "string",
   "Media": { 
      "MediaFileUri": "string"
   },
   "MediaFormat": "string",
   "MediaSampleRateHertz": number,
   "MedicalTranscriptionJobName": "string",
   "OutputBucketName": "string",
   "OutputEncryptionKMSKeyId": "string",
   "Settings": { 
      "ChannelIdentification": boolean,
      "MaxAlternatives": number,
      "MaxSpeakerLabels": number,
      "ShowAlternatives": boolean,
      "ShowSpeakerLabels": boolean,
      "VocabularyName": "string"
   },
   "Specialty": "string",
   "Type": "string"
}
```

## Request Parameters<a name="API_StartMedicalTranscriptionJob_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [LanguageCode](#API_StartMedicalTranscriptionJob_RequestSyntax) **   <a name="transcribe-StartMedicalTranscriptionJob-request-LanguageCode"></a>
The language code for the language spoken in the input media file\. US English \(en\-US\) is the valid value for medical transcription jobs\. Any other value you enter for language code results in a `BadRequestException` error\.  
Type: String  
Valid Values:` af-ZA | ar-AE | ar-SA | cy-GB | da-DK | de-CH | de-DE | en-AB | en-AU | en-GB | en-IE | en-IN | en-US | en-WL | es-ES | es-US | fa-IR | fr-CA | fr-FR | ga-IE | gd-GB | he-IL | hi-IN | id-ID | it-IT | ja-JP | ko-KR | ms-MY | nl-NL | pt-BR | pt-PT | ru-RU | ta-IN | te-IN | tr-TR | zh-CN`   
Required: Yes

 ** [Media](#API_StartMedicalTranscriptionJob_RequestSyntax) **   <a name="transcribe-StartMedicalTranscriptionJob-request-Media"></a>
Describes the input media file in a transcription request\.  
Type: [Media](API_Media.md) object  
Required: Yes

 ** [MediaFormat](#API_StartMedicalTranscriptionJob_RequestSyntax) **   <a name="transcribe-StartMedicalTranscriptionJob-request-MediaFormat"></a>
The audio format of the input media file\.  
Type: String  
Valid Values:` mp3 | mp4 | wav | flac`   
Required: No

 ** [MediaSampleRateHertz](#API_StartMedicalTranscriptionJob_RequestSyntax) **   <a name="transcribe-StartMedicalTranscriptionJob-request-MediaSampleRateHertz"></a>
The sample rate, in Hertz, of the audio track in the input media file\.  
If you do not specify the media sample rate, Amazon Transcribe Medical determines the sample rate\. If you specify the sample rate, it must match the rate detected by Amazon Transcribe Medical\. In most cases, you should leave the `MediaSampleRateHertz` field blank and let Amazon Transcribe Medical determine the sample rate\.  
Type: Integer  
Valid Range: Minimum value of 8000\. Maximum value of 48000\.  
Required: No

 ** [MedicalTranscriptionJobName](#API_StartMedicalTranscriptionJob_RequestSyntax) **   <a name="transcribe-StartMedicalTranscriptionJob-request-MedicalTranscriptionJobName"></a>
The name of the medical transcription job\. You can't use the strings "`.`" or "`..`" by themselves as the job name\. The name must also be unique within an AWS account\. If you try to create a medical transcription job with the same name as a previous medical transcription job, you get a `ConflictException` error\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 200\.  
Pattern: `^[0-9a-zA-Z._-]+`   
Required: Yes

 ** [OutputBucketName](#API_StartMedicalTranscriptionJob_RequestSyntax) **   <a name="transcribe-StartMedicalTranscriptionJob-request-OutputBucketName"></a>
The Amazon S3 location where the transcription is stored\.  
You must set `OutputBucketName` for Amazon Transcribe Medical to store the transcription results\. Your transcript appears in the S3 location you specify\. When you call the [GetMedicalTranscriptionJob](API_GetMedicalTranscriptionJob.md), the operation returns this location in the `TranscriptFileUri` field\. The S3 bucket must have permissions that allow Amazon Transcribe Medical to put files in the bucket\. For more information, see [Permissions Required for IAM User Roles](https://docs.aws.amazon.com/transcribe/latest/dg/security_iam_id-based-policy-examples.html#auth-role-iam-user)\.  
You can specify an AWS Key Management Service \(KMS\) key to encrypt the output of your transcription using the `OutputEncryptionKMSKeyId` parameter\. If you don't specify a KMS key, Amazon Transcribe Medical uses the default Amazon S3 key for server\-side encryption of transcripts that are placed in your S3 bucket\.  
Type: String  
Length Constraints: Maximum length of 64\.  
Pattern: `[a-z0-9][\.\-a-z0-9]{1,61}[a-z0-9]`   
Required: Yes

 ** [OutputEncryptionKMSKeyId](#API_StartMedicalTranscriptionJob_RequestSyntax) **   <a name="transcribe-StartMedicalTranscriptionJob-request-OutputEncryptionKMSKeyId"></a>
The Amazon Resource Name \(ARN\) of the AWS Key Management Service \(KMS\) key used to encrypt the output of the transcription job\. The user calling the [StartMedicalTranscriptionJob](#API_StartMedicalTranscriptionJob) operation must have permission to use the specified KMS key\.  
You use either of the following to identify a KMS key in the current account:  
+ KMS Key ID: "1234abcd\-12ab\-34cd\-56ef\-1234567890ab"
+ KMS Key Alias: "alias/ExampleAlias"
You can use either of the following to identify a KMS key in the current account or another account:  
+ Amazon Resource Name \(ARN\) of a KMS key in the current account or another account: "arn:aws:kms:region:account ID:key/1234abcd\-12ab\-34cd\-56ef\-1234567890ab"
+ ARN of a KMS Key Alias: "arn:aws:kms:region:account ID:alias/ExampleAlias"
If you don't specify an encryption key, the output of the medical transcription job is encrypted with the default Amazon S3 key \(SSE\-S3\)\.  
If you specify a KMS key to encrypt your output, you must also specify an output location in the `OutputBucketName` parameter\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 2048\.  
Pattern: `^[A-Za-z0-9][A-Za-z0-9:_/+=,@.-]{0,2048}$`   
Required: No

 ** [Settings](#API_StartMedicalTranscriptionJob_RequestSyntax) **   <a name="transcribe-StartMedicalTranscriptionJob-request-Settings"></a>
Optional settings for the medical transcription job\.  
Type: [MedicalTranscriptionSetting](API_MedicalTranscriptionSetting.md) object  
Required: No

 ** [Specialty](#API_StartMedicalTranscriptionJob_RequestSyntax) **   <a name="transcribe-StartMedicalTranscriptionJob-request-Specialty"></a>
The medical specialty of any clinician speaking in the input media\.  
Type: String  
Valid Values:` PRIMARYCARE`   
Required: Yes

 ** [Type](#API_StartMedicalTranscriptionJob_RequestSyntax) **   <a name="transcribe-StartMedicalTranscriptionJob-request-Type"></a>
The type of speech in the input audio\. `CONVERSATION` refers to conversations between two or more speakers, e\.g\., a conversations between doctors and patients\. `DICTATION` refers to single\-speaker dictated speech, e\.g\., for clinical notes\.  
Type: String  
Valid Values:` CONVERSATION | DICTATION`   
Required: Yes

## Response Syntax<a name="API_StartMedicalTranscriptionJob_ResponseSyntax"></a>

```
{
   "MedicalTranscriptionJob": { 
      "CompletionTime": number,
      "CreationTime": number,
      "FailureReason": "string",
      "LanguageCode": "string",
      "Media": { 
         "MediaFileUri": "string"
      },
      "MediaFormat": "string",
      "MediaSampleRateHertz": number,
      "MedicalTranscriptionJobName": "string",
      "Settings": { 
         "ChannelIdentification": boolean,
         "MaxAlternatives": number,
         "MaxSpeakerLabels": number,
         "ShowAlternatives": boolean,
         "ShowSpeakerLabels": boolean,
         "VocabularyName": "string"
      },
      "Specialty": "string",
      "StartTime": number,
      "Transcript": { 
         "TranscriptFileUri": "string"
      },
      "TranscriptionJobStatus": "string",
      "Type": "string"
   }
}
```

## Response Elements<a name="API_StartMedicalTranscriptionJob_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [MedicalTranscriptionJob](#API_StartMedicalTranscriptionJob_ResponseSyntax) **   <a name="transcribe-StartMedicalTranscriptionJob-response-MedicalTranscriptionJob"></a>
A batch job submitted to transcribe medical speech to text\.  
Type: [MedicalTranscriptionJob](API_MedicalTranscriptionJob.md) object

## Errors<a name="API_StartMedicalTranscriptionJob_Errors"></a>

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

## See Also<a name="API_StartMedicalTranscriptionJob_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/transcribe-2017-10-26/StartMedicalTranscriptionJob) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/transcribe-2017-10-26/StartMedicalTranscriptionJob) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transcribe-2017-10-26/StartMedicalTranscriptionJob) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transcribe-2017-10-26/StartMedicalTranscriptionJob) 
+  [AWS SDK for Java](https://docs.aws.amazon.com/goto/SdkForJava/transcribe-2017-10-26/StartMedicalTranscriptionJob) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/transcribe-2017-10-26/StartMedicalTranscriptionJob) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/transcribe-2017-10-26/StartMedicalTranscriptionJob) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/transcribe-2017-10-26/StartMedicalTranscriptionJob) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transcribe-2017-10-26/StartMedicalTranscriptionJob) 