# DescribeLanguageModel<a name="API_DescribeLanguageModel"></a>

Gets information about a single custom language model\. Use this information to see details about the language model in your AWS account\. You can also see whether the base language model used to create your custom language model has been updated\. If Amazon Transcribe has updated the base model, you can create a new custom language model using the updated base model\. If the language model wasn't created, you can use this operation to understand why Amazon Transcribe couldn't create it\. 

## Request Syntax<a name="API_DescribeLanguageModel_RequestSyntax"></a>

```
{
   "ModelName": "string"
}
```

## Request Parameters<a name="API_DescribeLanguageModel_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [ModelName](#API_DescribeLanguageModel_RequestSyntax) **   <a name="transcribe-DescribeLanguageModel-request-ModelName"></a>
The name of the custom language model you submit to get more information\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 200\.  
Pattern: `^[0-9a-zA-Z._-]+`   
Required: Yes

## Response Syntax<a name="API_DescribeLanguageModel_ResponseSyntax"></a>

```
{
   "LanguageModel": { 
      "BaseModelName": "string",
      "CreateTime": number,
      "FailureReason": "string",
      "InputDataConfig": { 
         "DataAccessRoleArn": "string",
         "S3Uri": "string",
         "TuningDataS3Uri": "string"
      },
      "LanguageCode": "string",
      "LastModifiedTime": number,
      "ModelName": "string",
      "ModelStatus": "string",
      "UpgradeAvailability": boolean
   }
}
```

## Response Elements<a name="API_DescribeLanguageModel_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [LanguageModel](#API_DescribeLanguageModel_ResponseSyntax) **   <a name="transcribe-DescribeLanguageModel-response-LanguageModel"></a>
The name of the custom language model you requested more information about\.  
Type: [LanguageModel](API_LanguageModel.md) object

## Errors<a name="API_DescribeLanguageModel_Errors"></a>

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

## See Also<a name="API_DescribeLanguageModel_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/transcribe-2017-10-26/DescribeLanguageModel) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/transcribe-2017-10-26/DescribeLanguageModel) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transcribe-2017-10-26/DescribeLanguageModel) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transcribe-2017-10-26/DescribeLanguageModel) 
+  [AWS SDK for Java](https://docs.aws.amazon.com/goto/SdkForJava/transcribe-2017-10-26/DescribeLanguageModel) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/transcribe-2017-10-26/DescribeLanguageModel) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/transcribe-2017-10-26/DescribeLanguageModel) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/transcribe-2017-10-26/DescribeLanguageModel) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transcribe-2017-10-26/DescribeLanguageModel) 