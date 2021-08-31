# UntagResource<a name="API_UntagResource"></a>

Removes specified tags from a specified Amazon Transcribe resource\.

## Request Syntax<a name="API_UntagResource_RequestSyntax"></a>

```
{
   "ResourceArn": "string",
   "TagKeys": [ "string" ]
}
```

## Request Parameters<a name="API_UntagResource_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [ ResourceArn ](#API_UntagResource_RequestSyntax) **   <a name="transcribe-UntagResource-request-ResourceArn"></a>
The Amazon Resource Name \(ARN\) of the Amazon Transcribe resource you want to remove tags from\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 1011\.  
Pattern: `arn:aws(-[^:]+)?:transcribe:[a-zA-Z0-9-]*:[0-9]{12}:[a-zA-Z-]*/[0-9a-zA-Z._-]+`   
Required: Yes

 ** [ TagKeys ](#API_UntagResource_RequestSyntax) **   <a name="transcribe-UntagResource-request-TagKeys"></a>
A list of tag keys you want to remove from a specified Amazon Transcribe resource\.  
Type: Array of strings  
Array Members: Minimum number of 1 item\. Maximum number of 200 items\.  
Length Constraints: Minimum length of 1\. Maximum length of 128\.  
Required: Yes

## Response Elements<a name="API_UntagResource_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response with an empty HTTP body\.

## Errors<a name="API_UntagResource_Errors"></a>

For information about the errors that are common to all actions, see [Common Errors](CommonErrors.md)\.

 ** BadRequestException **   
Your request didn't pass one or more validation tests\. For example, if the entity that you're trying to delete doesn't exist or if it is in a non\-terminal state \(for example, it's "in progress"\)\. See the exception `Message` field for more information\.  
HTTP Status Code: 400

 ** ConflictException **   
There is already a resource with that name\.  
HTTP Status Code: 400

 ** InternalFailureException **   
There was an internal error\. Check the error message and try your request again\.  
HTTP Status Code: 500

 ** LimitExceededException **   
Either you have sent too many requests or your input file is too long\. Wait before you resend your request, or use a smaller file and resend the request\.  
HTTP Status Code: 400

 ** NotFoundException **   
We can't find the requested resource\. Check the name and try your request again\.  
HTTP Status Code: 400

## See Also<a name="API_UntagResource_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [ AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/transcribe-2017-10-26/UntagResource) 
+  [ AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/transcribe-2017-10-26/UntagResource) 
+  [ AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transcribe-2017-10-26/UntagResource) 
+  [ AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transcribe-2017-10-26/UntagResource) 
+  [ AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transcribe-2017-10-26/UntagResource) 
+  [ AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/transcribe-2017-10-26/UntagResource) 
+  [ AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/transcribe-2017-10-26/UntagResource) 
+  [ AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/transcribe-2017-10-26/UntagResource) 
+  [ AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transcribe-2017-10-26/UntagResource) 