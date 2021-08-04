# GetMedicalTranscriptionJob<a name="API_GetMedicalTranscriptionJob"></a>

Returns information about a transcription job from Amazon Transcribe Medical\. To see the status of the job, check the `TranscriptionJobStatus` field\. If the status is `COMPLETED`, the job is finished\. You find the results of the completed job in the `TranscriptFileUri` field\.

## Request Syntax<a name="API_GetMedicalTranscriptionJob_RequestSyntax"></a>

```
{
   "MedicalTranscriptionJobName": "string"
}
```

## Request Parameters<a name="API_GetMedicalTranscriptionJob_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [MedicalTranscriptionJobName](#API_GetMedicalTranscriptionJob_RequestSyntax) **   <a name="transcribe-GetMedicalTranscriptionJob-request-MedicalTranscriptionJobName"></a>
The name of the medical transcription job\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 200\.  
Pattern: `^[0-9a-zA-Z._-]+`   
Required: Yes

## Response Syntax<a name="API_GetMedicalTranscriptionJob_ResponseSyntax"></a>

```
{
   "MedicalTranscriptionJob": { 
      "CompletionTime": number,
      "ContentIdentificationType": "string",
      "CreationTime": number,
      "FailureReason": "string",
      "LanguageCode": "string",
      "Media": { 
         "MediaFileUri": "string",
         "RedactedMediaFileUri": "string"
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

## Response Elements<a name="API_GetMedicalTranscriptionJob_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [MedicalTranscriptionJob](#API_GetMedicalTranscriptionJob_ResponseSyntax) **   <a name="transcribe-GetMedicalTranscriptionJob-response-MedicalTranscriptionJob"></a>
An object that contains the results of the medical transcription job\.  
Type: [MedicalTranscriptionJob](API_MedicalTranscriptionJob.md) object

## Errors<a name="API_GetMedicalTranscriptionJob_Errors"></a>

For information about the errors that are common to all actions, see [Common Errors](CommonErrors.md)\.

 **BadRequestException**   
Your request didn't pass one or more validation tests\. For example, if the entity that you're trying to delete doesn't exist or if it is in a non\-terminal state \(for example, it's "in progress"\)\. See the exception `Message` field for more information\.  
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

## See Also<a name="API_GetMedicalTranscriptionJob_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/transcribe-2017-10-26/GetMedicalTranscriptionJob) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/transcribe-2017-10-26/GetMedicalTranscriptionJob) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transcribe-2017-10-26/GetMedicalTranscriptionJob) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transcribe-2017-10-26/GetMedicalTranscriptionJob) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transcribe-2017-10-26/GetMedicalTranscriptionJob) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/transcribe-2017-10-26/GetMedicalTranscriptionJob) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/transcribe-2017-10-26/GetMedicalTranscriptionJob) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/transcribe-2017-10-26/GetMedicalTranscriptionJob) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transcribe-2017-10-26/GetMedicalTranscriptionJob) 