# GetVocabulary<a name="API_GetVocabulary"></a>

Gets information about a vocabulary\.

## Request Syntax<a name="API_GetVocabulary_RequestSyntax"></a>

```
{
   "[VocabularyName](#transcribe-GetVocabulary-request-VocabularyName)": "string"
}
```

## Request Parameters<a name="API_GetVocabulary_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [VocabularyName](#API_GetVocabulary_RequestSyntax) **   <a name="transcribe-GetVocabulary-request-VocabularyName"></a>
The name of the vocabulary to return information about\. The name is case\-sensitive\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 200\.  
Pattern: `^[0-9a-zA-Z._-]+`   
Required: Yes

## Response Syntax<a name="API_GetVocabulary_ResponseSyntax"></a>

```
{
   "[DownloadUri](#transcribe-GetVocabulary-response-DownloadUri)": "string",
   "[FailureReason](#transcribe-GetVocabulary-response-FailureReason)": "string",
   "[LanguageCode](#transcribe-GetVocabulary-response-LanguageCode)": "string",
   "[LastModifiedTime](#transcribe-GetVocabulary-response-LastModifiedTime)": number,
   "[VocabularyName](#transcribe-GetVocabulary-response-VocabularyName)": "string",
   "[VocabularyState](#transcribe-GetVocabulary-response-VocabularyState)": "string"
}
```

## Response Elements<a name="API_GetVocabulary_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [DownloadUri](#API_GetVocabulary_ResponseSyntax) **   <a name="transcribe-GetVocabulary-response-DownloadUri"></a>
The S3 location where the vocabulary is stored\. Use this URI to get the contents of the vocabulary\. The URI is available for a limited time\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 2000\.

 ** [FailureReason](#API_GetVocabulary_ResponseSyntax) **   <a name="transcribe-GetVocabulary-response-FailureReason"></a>
If the `VocabularyState` field is `FAILED`, this field contains information about why the job failed\.  
Type: String

 ** [LanguageCode](#API_GetVocabulary_ResponseSyntax) **   <a name="transcribe-GetVocabulary-response-LanguageCode"></a>
The language code of the vocabulary entries\.  
Type: String  
Valid Values:` en-US | es-US | en-AU | fr-CA | en-GB` 

 ** [LastModifiedTime](#API_GetVocabulary_ResponseSyntax) **   <a name="transcribe-GetVocabulary-response-LastModifiedTime"></a>
The date and time that the vocabulary was last modified\.  
Type: Timestamp

 ** [VocabularyName](#API_GetVocabulary_ResponseSyntax) **   <a name="transcribe-GetVocabulary-response-VocabularyName"></a>
The name of the vocabulary to return\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 200\.  
Pattern: `^[0-9a-zA-Z._-]+` 

 ** [VocabularyState](#API_GetVocabulary_ResponseSyntax) **   <a name="transcribe-GetVocabulary-response-VocabularyState"></a>
The processing state of the vocabulary\.  
Type: String  
Valid Values:` PENDING | READY | FAILED` 

## Errors<a name="API_GetVocabulary_Errors"></a>

For information about the errors that are common to all actions, see [Common Errors](CommonErrors.md)\.

 **BadRequestException**   
Your request didn't pass one or more validation tests\. For example, a name already exists when creating a resource or a name may not exist when getting a transcription job or custom vocabulary\. See the exception `Message` field for more information\.  
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

## See Also<a name="API_GetVocabulary_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/transcribe-2017-10-26/GetVocabulary) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/transcribe-2017-10-26/GetVocabulary) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transcribe-2017-10-26/GetVocabulary) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transcribe-2017-10-26/GetVocabulary) 
+  [AWS SDK for Java](https://docs.aws.amazon.com/goto/SdkForJava/transcribe-2017-10-26/GetVocabulary) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/transcribe-2017-10-26/GetVocabulary) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/transcribe-2017-10-26/GetVocabulary) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/transcribe-2017-10-26/GetVocabulary) 
+  [AWS SDK for Ruby V2](https://docs.aws.amazon.com/goto/SdkForRubyV2/transcribe-2017-10-26/GetVocabulary) 