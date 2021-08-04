# StartCallAnalyticsJob<a name="API_StartCallAnalyticsJob"></a>

Starts an asynchronous analytics job that not only transcribes the audio recording of a caller and agent, but also returns additional insights\. These insights include how quickly or loudly the caller or agent was speaking\. To retrieve additional insights with your analytics jobs, create categories\. A category is a way to classify analytics jobs based on attributes, such as a customer's sentiment or a particular phrase being used during the call\. For more information, see the [CreateCallAnalyticsCategory](API_CreateCallAnalyticsCategory.md) operation\. 

## Request Syntax<a name="API_StartCallAnalyticsJob_RequestSyntax"></a>

```
{
   "CallAnalyticsJobName": "string",
   "ChannelDefinitions": [ 
      { 
         "ChannelId": number,
         "ParticipantRole": "string"
      }
   ],
   "DataAccessRoleArn": "string",
   "Media": { 
      "MediaFileUri": "string",
      "RedactedMediaFileUri": "string"
   },
   "OutputEncryptionKMSKeyId": "string",
   "OutputLocation": "string",
   "Settings": { 
      "ContentRedaction": { 
         "RedactionOutput": "string",
         "RedactionType": "string"
      },
      "LanguageModelName": "string",
      "LanguageOptions": [ "string" ],
      "VocabularyFilterMethod": "string",
      "VocabularyFilterName": "string",
      "VocabularyName": "string"
   }
}
```

## Request Parameters<a name="API_StartCallAnalyticsJob_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [CallAnalyticsJobName](#API_StartCallAnalyticsJob_RequestSyntax) **   <a name="transcribe-StartCallAnalyticsJob-request-CallAnalyticsJobName"></a>
The name of the call analytics job\. You can't use the string "\." or "\.\." by themselves as the job name\. The name must also be unique within an AWS account\. If you try to create a call analytics job with the same name as a previous call analytics job, you get a `ConflictException` error\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 200\.  
Pattern: `^[0-9a-zA-Z._-]+`   
Required: Yes

 ** [ChannelDefinitions](#API_StartCallAnalyticsJob_RequestSyntax) **   <a name="transcribe-StartCallAnalyticsJob-request-ChannelDefinitions"></a>
When you start a call analytics job, you must pass an array that maps the agent and the customer to specific audio channels\. The values you can assign to a channel are 0 and 1\. The agent and the customer must each have their own channel\. You can't assign more than one channel to an agent or customer\.   
Type: Array of [ChannelDefinition](API_ChannelDefinition.md) objects  
Array Members: Fixed number of 2 items\.  
Required: No

 ** [DataAccessRoleArn](#API_StartCallAnalyticsJob_RequestSyntax) **   <a name="transcribe-StartCallAnalyticsJob-request-DataAccessRoleArn"></a>
The Amazon Resource Name \(ARN\) of a role that has access to the S3 bucket that contains your input files\. Amazon Transcribe assumes this role to read queued audio files\. If you have specified an output S3 bucket for your transcription results, this role should have access to the output bucket as well\.  
Type: String  
Length Constraints: Minimum length of 20\. Maximum length of 2048\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso-{0,1}[a-z]{0,1}):iam::[0-9]{0,63}:role/[A-Za-z0-9:_/+=,@.-]{0,1024}$`   
Required: Yes

 ** [Media](#API_StartCallAnalyticsJob_RequestSyntax) **   <a name="transcribe-StartCallAnalyticsJob-request-Media"></a>
Describes the input media file in a transcription request\.  
Type: [Media](API_Media.md) object  
Required: Yes

 ** [OutputEncryptionKMSKeyId](#API_StartCallAnalyticsJob_RequestSyntax) **   <a name="transcribe-StartCallAnalyticsJob-request-OutputEncryptionKMSKeyId"></a>
The Amazon Resource Name \(ARN\) of the AWS Key Management Service key used to encrypt the output of the call analytics job\. The user calling the [StartCallAnalyticsJob](#API_StartCallAnalyticsJob) operation must have permission to use the specified KMS key\.  
You use either of the following to identify an AWS KMS key in the current account:  
+ KMS Key ID: "1234abcd\-12ab\-34cd\-56ef\-1234567890ab"
+ KMS Key Alias: "alias/ExampleAlias"
 You can use either of the following to identify a KMS key in the current account or another account:  
+ Amazon Resource Name \(ARN\) of a KMS key in the current account or another account: "arn:aws:kms:region:account ID:key/1234abcd\-12ab\-34cd\-56ef1234567890ab"
+ ARN of a KMS Key Alias: "arn:aws:kms:region:account ID:alias/ExampleAlias"
If you don't specify an encryption key, the output of the call analytics job is encrypted with the default Amazon S3 key \(SSE\-S3\)\.  
If you specify a KMS key to encrypt your output, you must also specify an output location in the `OutputLocation` parameter\.   
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 2048\.  
Pattern: `^[A-Za-z0-9][A-Za-z0-9:_/+=,@.-]{0,2048}$`   
Required: No

 ** [OutputLocation](#API_StartCallAnalyticsJob_RequestSyntax) **   <a name="transcribe-StartCallAnalyticsJob-request-OutputLocation"></a>
The Amazon S3 location where the output of the call analytics job is stored\. You can provide the following location types to store the output of call analytics job:  
+ s3://DOC\-EXAMPLE\-BUCKET1

   If you specify a bucket, Amazon Transcribe saves the output of the analytics job as a JSON file at the root level of the bucket\.
+ s3://DOC\-EXAMPLE\-BUCKET1/folder/

  f you specify a path, Amazon Transcribe saves the output of the analytics job as s3://DOC\-EXAMPLE\-BUCKET1/folder/your\-transcription\-job\-name\.json

  If you specify a folder, you must provide a trailing slash\.
+ s3://DOC\-EXAMPLE\-BUCKET1/folder/filename\.json

   If you provide a path that has the filename specified, Amazon Transcribe saves the output of the analytics job as s3://DOC\-EXAMPLEBUCKET1/folder/filename\.json
You can specify an AWS Key Management Service key to encrypt the output of our analytics job using the `OutputEncryptionKMSKeyId` parameter\. If you don't specify a KMS key, Amazon Transcribe uses the default Amazon S3 key for server\-side encryption of the analytics job output that is placed in your S3 bucket\.   
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 2000\.  
Pattern: `(s3://|http(s*)://).+`   
Required: No

 ** [Settings](#API_StartCallAnalyticsJob_RequestSyntax) **   <a name="transcribe-StartCallAnalyticsJob-request-Settings"></a>
A `Settings` object that provides optional settings for a call analytics job\.   
Type: [CallAnalyticsJobSettings](API_CallAnalyticsJobSettings.md) object  
Required: No

## Response Syntax<a name="API_StartCallAnalyticsJob_ResponseSyntax"></a>

```
{
   "CallAnalyticsJob": { 
      "CallAnalyticsJobName": "string",
      "CallAnalyticsJobStatus": "string",
      "ChannelDefinitions": [ 
         { 
            "ChannelId": number,
            "ParticipantRole": "string"
         }
      ],
      "CompletionTime": number,
      "CreationTime": number,
      "DataAccessRoleArn": "string",
      "FailureReason": "string",
      "IdentifiedLanguageScore": number,
      "LanguageCode": "string",
      "Media": { 
         "MediaFileUri": "string",
         "RedactedMediaFileUri": "string"
      },
      "MediaFormat": "string",
      "MediaSampleRateHertz": number,
      "Settings": { 
         "ContentRedaction": { 
            "RedactionOutput": "string",
            "RedactionType": "string"
         },
         "LanguageModelName": "string",
         "LanguageOptions": [ "string" ],
         "VocabularyFilterMethod": "string",
         "VocabularyFilterName": "string",
         "VocabularyName": "string"
      },
      "StartTime": number,
      "Transcript": { 
         "RedactedTranscriptFileUri": "string",
         "TranscriptFileUri": "string"
      }
   }
}
```

## Response Elements<a name="API_StartCallAnalyticsJob_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [CallAnalyticsJob](#API_StartCallAnalyticsJob_ResponseSyntax) **   <a name="transcribe-StartCallAnalyticsJob-response-CallAnalyticsJob"></a>
An object containing the details of the asynchronous call analytics job\.  
Type: [CallAnalyticsJob](API_CallAnalyticsJob.md) object

## Errors<a name="API_StartCallAnalyticsJob_Errors"></a>

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

## See Also<a name="API_StartCallAnalyticsJob_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/transcribe-2017-10-26/StartCallAnalyticsJob) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/transcribe-2017-10-26/StartCallAnalyticsJob) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transcribe-2017-10-26/StartCallAnalyticsJob) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transcribe-2017-10-26/StartCallAnalyticsJob) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transcribe-2017-10-26/StartCallAnalyticsJob) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/transcribe-2017-10-26/StartCallAnalyticsJob) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/transcribe-2017-10-26/StartCallAnalyticsJob) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/transcribe-2017-10-26/StartCallAnalyticsJob) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transcribe-2017-10-26/StartCallAnalyticsJob) 