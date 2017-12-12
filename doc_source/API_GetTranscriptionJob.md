# GetTranscriptionJob<a name="API_GetTranscriptionJob"></a>

Returns information about a transcription job\. To see the status of the job, check the `Status` field\. If the status is `COMPLETE`, the job is finished and you can find the results at the location specified in the `TranscriptionFileUri` field\.

## Request Syntax<a name="API_GetTranscriptionJob_RequestSyntax"></a>

```
{
   "TranscriptionJobName": "string"
}
```

## Request Parameters<a name="API_GetTranscriptionJob_RequestParameters"></a>

For information about the parameters that are common to all actions, see Common Parameters\.

The request accepts the following data in JSON format\.

 ** TranscriptionJobName **   
The name of the job\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 200\.  
Pattern: `^[a-zA-Z0-9](-*[a-zA-Z0-9])*`   
Required: Yes

## Response Syntax<a name="API_GetTranscriptionJob_ResponseSyntax"></a>

```
{
   "TranscriptionJob": { 
      "CompletionTime": number,
      "CreationTime": number,
      "FailureReason": "string",
      "LanguageCode": "string",
      "Media": { 
         "MediaFileUri": "string"
      },
      "MediaFormat": "string",
      "MediaSampleRateHertz": number,
      "Transcript": { 
         "TranscriptFileUri": "string"
      },
      "TranscriptionJobName": "string",
      "TranscriptionJobStatus": "string"
   }
}
```

## Response Elements<a name="API_GetTranscriptionJob_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** TranscriptionJob **   
An object that contains the results of the transcription job\.  
Type: [TranscriptionJob](API_TranscriptionJob.md) object

## Errors<a name="API_GetTranscriptionJob_Errors"></a>

For information about the errors that are common to all actions, see [Common Errors](CommonErrors.md)\.

 **BadRequestException**   
There is a problem with one of the input fields\. Check the S3 bucket name, make sure that the job name is not a duplicate, and confirm that you are using the correct file format\. Then resend your request\.  
HTTP Status Code: 400

 **InternalFailureException**   
There was an internal error\. Check the error message and try your request again\.  
HTTP Status Code: 400

 **LimitExceededException**   
Either you have sent too many requests or your input file is longer than 2 hours\. Wait before you resend your request, or use a smaller file and resend the request\.  
HTTP Status Code: 400

 **NotFoundException**   
We can't find the requested job\. Check the job name and try your request again\.  
HTTP Status Code: 400

## See Also<a name="API_GetTranscriptionJob_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:

+  [AWS Command Line Interface](http://docs.aws.amazon.com/goto/aws-cli/transcribe-2017-10-26/GetTranscriptionJob) 

+  [AWS SDK for \.NET](http://docs.aws.amazon.com/goto/DotNetSDKV3/transcribe-2017-10-26/GetTranscriptionJob) 

+  [AWS SDK for C\+\+](http://docs.aws.amazon.com/goto/SdkForCpp/transcribe-2017-10-26/GetTranscriptionJob) 

+  [AWS SDK for Go](http://docs.aws.amazon.com/goto/SdkForGoV1/transcribe-2017-10-26/GetTranscriptionJob) 

+  [AWS SDK for Java](http://docs.aws.amazon.com/goto/SdkForJava/transcribe-2017-10-26/GetTranscriptionJob) 

+  [AWS SDK for JavaScript](http://docs.aws.amazon.com/goto/AWSJavaScriptSDK/transcribe-2017-10-26/GetTranscriptionJob) 

+  [AWS SDK for PHP V3](http://docs.aws.amazon.com/goto/SdkForPHPV3/transcribe-2017-10-26/GetTranscriptionJob) 

+  [AWS SDK for Python](http://docs.aws.amazon.com/goto/boto3/transcribe-2017-10-26/GetTranscriptionJob) 

+  [AWS SDK for Ruby V2](http://docs.aws.amazon.com/goto/SdkForRubyV2/transcribe-2017-10-26/GetTranscriptionJob) 