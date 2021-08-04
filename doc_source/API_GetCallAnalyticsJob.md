# GetCallAnalyticsJob<a name="API_GetCallAnalyticsJob"></a>

Returns information about a call analytics job\. To see the status of the job, check the `CallAnalyticsJobStatus` field\. If the status is `COMPLETED`, the job is finished and you can find the results at the location specified in the `TranscriptFileUri` field\. If you enable personally identifiable information \(PII\) redaction, the redacted transcript appears in the `RedactedTranscriptFileUri` field\.

## Request Syntax<a name="API_GetCallAnalyticsJob_RequestSyntax"></a>

```
{
   "CallAnalyticsJobName": "string"
}
```

## Request Parameters<a name="API_GetCallAnalyticsJob_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [CallAnalyticsJobName](#API_GetCallAnalyticsJob_RequestSyntax) **   <a name="transcribe-GetCallAnalyticsJob-request-CallAnalyticsJobName"></a>
The name of the analytics job you want information about\. This value is case sensitive\.   
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 200\.  
Pattern: `^[0-9a-zA-Z._-]+`   
Required: Yes

## Response Syntax<a name="API_GetCallAnalyticsJob_ResponseSyntax"></a>

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

## Response Elements<a name="API_GetCallAnalyticsJob_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [CallAnalyticsJob](#API_GetCallAnalyticsJob_ResponseSyntax) **   <a name="transcribe-GetCallAnalyticsJob-response-CallAnalyticsJob"></a>
An object that contains the results of your call analytics job\.  
Type: [CallAnalyticsJob](API_CallAnalyticsJob.md) object

## Errors<a name="API_GetCallAnalyticsJob_Errors"></a>

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

## See Also<a name="API_GetCallAnalyticsJob_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/transcribe-2017-10-26/GetCallAnalyticsJob) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/transcribe-2017-10-26/GetCallAnalyticsJob) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transcribe-2017-10-26/GetCallAnalyticsJob) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transcribe-2017-10-26/GetCallAnalyticsJob) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transcribe-2017-10-26/GetCallAnalyticsJob) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/transcribe-2017-10-26/GetCallAnalyticsJob) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/transcribe-2017-10-26/GetCallAnalyticsJob) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/transcribe-2017-10-26/GetCallAnalyticsJob) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transcribe-2017-10-26/GetCallAnalyticsJob) 