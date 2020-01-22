# GetTranscriptionJob<a name="API_GetTranscriptionJob"></a>

Returns information about a transcription job\. To see the status of the job, check the `TranscriptionJobStatus` field\. If the status is `COMPLETED`, the job is finished and you can find the results at the location specified in the `TranscriptionFileUri` field\.

## Request Syntax<a name="API_GetTranscriptionJob_RequestSyntax"></a>

```
{
   "[TranscriptionJobName](#transcribe-GetTranscriptionJob-request-TranscriptionJobName)": "string"
}
```

## Request Parameters<a name="API_GetTranscriptionJob_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [TranscriptionJobName](#API_GetTranscriptionJob_RequestSyntax) **   <a name="transcribe-GetTranscriptionJob-request-TranscriptionJobName"></a>
The name of the job\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 200\.  
Pattern: `^[0-9a-zA-Z._-]+`   
Required: Yes

## Response Syntax<a name="API_GetTranscriptionJob_ResponseSyntax"></a>

```
{
   "[TranscriptionJob](#transcribe-GetTranscriptionJob-response-TranscriptionJob)": { 
      "[CompletionTime](API_TranscriptionJob.md#transcribe-Type-TranscriptionJob-CompletionTime)": number,
      "[CreationTime](API_TranscriptionJob.md#transcribe-Type-TranscriptionJob-CreationTime)": number,
      "[FailureReason](API_TranscriptionJob.md#transcribe-Type-TranscriptionJob-FailureReason)": "string",
      "[JobExecutionSettings](API_TranscriptionJob.md#transcribe-Type-TranscriptionJob-JobExecutionSettings)": { 
         "[AllowDeferredExecution](API_JobExecutionSettings.md#transcribe-Type-JobExecutionSettings-AllowDeferredExecution)": boolean,
         "[DataAccessRoleArn](API_JobExecutionSettings.md#transcribe-Type-JobExecutionSettings-DataAccessRoleArn)": "string"
      },
      "[LanguageCode](API_TranscriptionJob.md#transcribe-Type-TranscriptionJob-LanguageCode)": "string",
      "[Media](API_TranscriptionJob.md#transcribe-Type-TranscriptionJob-Media)": { 
         "[MediaFileUri](API_Media.md#transcribe-Type-Media-MediaFileUri)": "string"
      },
      "[MediaFormat](API_TranscriptionJob.md#transcribe-Type-TranscriptionJob-MediaFormat)": "string",
      "[MediaSampleRateHertz](API_TranscriptionJob.md#transcribe-Type-TranscriptionJob-MediaSampleRateHertz)": number,
      "[Settings](API_TranscriptionJob.md#transcribe-Type-TranscriptionJob-Settings)": { 
         "[ChannelIdentification](API_Settings.md#transcribe-Type-Settings-ChannelIdentification)": boolean,
         "[MaxAlternatives](API_Settings.md#transcribe-Type-Settings-MaxAlternatives)": number,
         "[MaxSpeakerLabels](API_Settings.md#transcribe-Type-Settings-MaxSpeakerLabels)": number,
         "[ShowAlternatives](API_Settings.md#transcribe-Type-Settings-ShowAlternatives)": boolean,
         "[ShowSpeakerLabels](API_Settings.md#transcribe-Type-Settings-ShowSpeakerLabels)": boolean,
         "[VocabularyFilterMethod](API_Settings.md#transcribe-Type-Settings-VocabularyFilterMethod)": "string",
         "[VocabularyFilterName](API_Settings.md#transcribe-Type-Settings-VocabularyFilterName)": "string",
         "[VocabularyName](API_Settings.md#transcribe-Type-Settings-VocabularyName)": "string"
      },
      "[StartTime](API_TranscriptionJob.md#transcribe-Type-TranscriptionJob-StartTime)": number,
      "[Transcript](API_TranscriptionJob.md#transcribe-Type-TranscriptionJob-Transcript)": { 
         "[TranscriptFileUri](API_Transcript.md#transcribe-Type-Transcript-TranscriptFileUri)": "string"
      },
      "[TranscriptionJobName](API_TranscriptionJob.md#transcribe-Type-TranscriptionJob-TranscriptionJobName)": "string",
      "[TranscriptionJobStatus](API_TranscriptionJob.md#transcribe-Type-TranscriptionJob-TranscriptionJobStatus)": "string"
   }
}
```

## Response Elements<a name="API_GetTranscriptionJob_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [TranscriptionJob](#API_GetTranscriptionJob_ResponseSyntax) **   <a name="transcribe-GetTranscriptionJob-response-TranscriptionJob"></a>
An object that contains the results of the transcription job\.  
Type: [TranscriptionJob](API_TranscriptionJob.md) object

## Errors<a name="API_GetTranscriptionJob_Errors"></a>

For information about the errors that are common to all actions, see [Common Errors](CommonErrors.md)\.

 **BadRequestException**   
Your request didn't pass one or more validation tests\. For example, if the transcription you're trying to delete doesn't exist or if it is in a non\-terminal state \(for example, it's "in progress"\)\. See the exception `Message` field for more information\.  
HTTP Status Code: 400

 **InternalFailureException**   
There was an internal error\. Check the error message and try your request again\.  
HTTP Status Code: 500

 **LimitExceededException**   
Either you have sent too many requests or your input file is too long\. Wait before you resend your request, or use a smaller file and resend the request\.  
HTTP Status Code: 400

 **NotFoundException**   
We can't find the requested resource\. Check the name and try your request again\.  
HTTP Status Code: 400

## See Also<a name="API_GetTranscriptionJob_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/transcribe-2017-10-26/GetTranscriptionJob) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/transcribe-2017-10-26/GetTranscriptionJob) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transcribe-2017-10-26/GetTranscriptionJob) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transcribe-2017-10-26/GetTranscriptionJob) 
+  [AWS SDK for Java](https://docs.aws.amazon.com/goto/SdkForJava/transcribe-2017-10-26/GetTranscriptionJob) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/transcribe-2017-10-26/GetTranscriptionJob) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/transcribe-2017-10-26/GetTranscriptionJob) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/transcribe-2017-10-26/GetTranscriptionJob) 
+  [AWS SDK for Ruby V2](https://docs.aws.amazon.com/goto/SdkForRubyV2/transcribe-2017-10-26/GetTranscriptionJob) 