# ListLanguageModels<a name="API_ListLanguageModels"></a>

Provides more information about the custom language models you've created\. You can use the information in this list to find a specific custom language model\. You can then use the [DescribeLanguageModel](API_DescribeLanguageModel.md) operation to get more information about it\.

## Request Syntax<a name="API_ListLanguageModels_RequestSyntax"></a>

```
{
   "MaxResults": number,
   "NameContains": "string",
   "NextToken": "string",
   "StatusEquals": "string"
}
```

## Request Parameters<a name="API_ListLanguageModels_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [MaxResults](#API_ListLanguageModels_RequestSyntax) **   <a name="transcribe-ListLanguageModels-request-MaxResults"></a>
 The maximum number of language models to return in each page of results\. If there are fewer results than the value you specify, only the actual results are returned\. If you do not specify a value, the default of 5 is used\.  
Type: Integer  
Valid Range: Minimum value of 1\. Maximum value of 100\.  
Required: No

 ** [NameContains](#API_ListLanguageModels_RequestSyntax) **   <a name="transcribe-ListLanguageModels-request-NameContains"></a>
When specified, the custom language model names returned contain the substring you've specified\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 200\.  
Pattern: `^[0-9a-zA-Z._-]+`   
Required: No

 ** [NextToken](#API_ListLanguageModels_RequestSyntax) **   <a name="transcribe-ListLanguageModels-request-NextToken"></a>
When included, fetches the next set of jobs if the result of the previous request was truncated\.  
Type: String  
Length Constraints: Maximum length of 8192\.  
Pattern: `.+`   
Required: No

 ** [StatusEquals](#API_ListLanguageModels_RequestSyntax) **   <a name="transcribe-ListLanguageModels-request-StatusEquals"></a>
When specified, returns only custom language models with the specified status\. Language models are ordered by creation date, with the newest models first\. If you don't specify a status, Amazon Transcribe returns all custom language models ordered by date\.  
Type: String  
Valid Values:` IN_PROGRESS | FAILED | COMPLETED`   
Required: No

## Response Syntax<a name="API_ListLanguageModels_ResponseSyntax"></a>

```
{
   "Models": [ 
      { 
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
   ],
   "NextToken": "string"
}
```

## Response Elements<a name="API_ListLanguageModels_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [Models](#API_ListLanguageModels_ResponseSyntax) **   <a name="transcribe-ListLanguageModels-response-Models"></a>
A list of objects containing information about custom language models\.  
Type: Array of [LanguageModel](API_LanguageModel.md) objects

 ** [NextToken](#API_ListLanguageModels_ResponseSyntax) **   <a name="transcribe-ListLanguageModels-response-NextToken"></a>
The [ListLanguageModels](#API_ListLanguageModels) operation returns a page of jobs at a time\. The maximum size of the list is set by the MaxResults parameter\. If there are more language models in the list than the page size, Amazon Transcribe returns the `NextPage` token\. Include the token in the next request to the [ListLanguageModels](#API_ListLanguageModels) operation to return the next page of language models\.  
Type: String  
Length Constraints: Maximum length of 8192\.  
Pattern: `.+` 

## Errors<a name="API_ListLanguageModels_Errors"></a>

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

## See Also<a name="API_ListLanguageModels_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [ AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/transcribe-2017-10-26/ListLanguageModels) 
+  [ AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/transcribe-2017-10-26/ListLanguageModels) 
+  [ AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transcribe-2017-10-26/ListLanguageModels) 
+  [ AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transcribe-2017-10-26/ListLanguageModels) 
+  [ AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transcribe-2017-10-26/ListLanguageModels) 
+  [ AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/transcribe-2017-10-26/ListLanguageModels) 
+  [ AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/transcribe-2017-10-26/ListLanguageModels) 
+  [ AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/transcribe-2017-10-26/ListLanguageModels) 
+  [ AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transcribe-2017-10-26/ListLanguageModels) 