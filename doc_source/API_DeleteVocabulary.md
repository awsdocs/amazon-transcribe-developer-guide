# DeleteVocabulary<a name="API_DeleteVocabulary"></a>

Deletes a vocabulary from Amazon Transcribe\. 

## Request Syntax<a name="API_DeleteVocabulary_RequestSyntax"></a>

```
{
   "[VocabularyName](#transcribe-DeleteVocabulary-request-VocabularyName)": "string"
}
```

## Request Parameters<a name="API_DeleteVocabulary_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [VocabularyName](#API_DeleteVocabulary_RequestSyntax) **   <a name="transcribe-DeleteVocabulary-request-VocabularyName"></a>
The name of the vocabulary to delete\.   
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 200\.  
Pattern: `^[0-9a-zA-Z._-]+`   
Required: Yes

## Response Elements<a name="API_DeleteVocabulary_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response with an empty HTTP body\.

## Errors<a name="API_DeleteVocabulary_Errors"></a>

For information about the errors that are common to all actions, see [Common Errors](CommonErrors.md)\.

 **InternalFailureException**   
There was an internal error\. Check the error message and try your request again\.  
HTTP Status Code: 500

 **LimitExceededException**   
Either you have sent too many requests or your input file is too long\. Wait before you resend your request, or use a smaller file and resend the request\.  
HTTP Status Code: 400

 **NotFoundException**   
We can't find the requested resource\. Check the name and try your request again\.  
HTTP Status Code: 400

## See Also<a name="API_DeleteVocabulary_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:

+  [AWS Command Line Interface](http://docs.aws.amazon.com/goto/aws-cli/transcribe-2017-10-26/DeleteVocabulary) 

+  [AWS SDK for \.NET](http://docs.aws.amazon.com/goto/DotNetSDKV3/transcribe-2017-10-26/DeleteVocabulary) 

+  [AWS SDK for C\+\+](http://docs.aws.amazon.com/goto/SdkForCpp/transcribe-2017-10-26/DeleteVocabulary) 

+  [AWS SDK for Go](http://docs.aws.amazon.com/goto/SdkForGoV1/transcribe-2017-10-26/DeleteVocabulary) 

+  [AWS SDK for Java](http://docs.aws.amazon.com/goto/SdkForJava/transcribe-2017-10-26/DeleteVocabulary) 

+  [AWS SDK for JavaScript](http://docs.aws.amazon.com/goto/AWSJavaScriptSDK/transcribe-2017-10-26/DeleteVocabulary) 

+  [AWS SDK for PHP V3](http://docs.aws.amazon.com/goto/SdkForPHPV3/transcribe-2017-10-26/DeleteVocabulary) 

+  [AWS SDK for Python](http://docs.aws.amazon.com/goto/boto3/transcribe-2017-10-26/DeleteVocabulary) 

+  [AWS SDK for Ruby V2](http://docs.aws.amazon.com/goto/SdkForRubyV2/transcribe-2017-10-26/DeleteVocabulary) 