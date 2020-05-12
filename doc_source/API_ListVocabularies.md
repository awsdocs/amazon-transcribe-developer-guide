# ListVocabularies<a name="API_ListVocabularies"></a>

Returns a list of vocabularies that match the specified criteria\. If no criteria are specified, returns the entire list of vocabularies\.

## Request Syntax<a name="API_ListVocabularies_RequestSyntax"></a>

```
{
   "[MaxResults](#transcribe-ListVocabularies-request-MaxResults)": number,
   "[NameContains](#transcribe-ListVocabularies-request-NameContains)": "string",
   "[NextToken](#transcribe-ListVocabularies-request-NextToken)": "string",
   "[StateEquals](#transcribe-ListVocabularies-request-StateEquals)": "string"
}
```

## Request Parameters<a name="API_ListVocabularies_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [MaxResults](#API_ListVocabularies_RequestSyntax) **   <a name="transcribe-ListVocabularies-request-MaxResults"></a>
The maximum number of vocabularies to return in the response\. If there are fewer results in the list, this response contains only the actual results\.  
Type: Integer  
Valid Range: Minimum value of 1\. Maximum value of 100\.  
Required: No

 ** [NameContains](#API_ListVocabularies_RequestSyntax) **   <a name="transcribe-ListVocabularies-request-NameContains"></a>
When specified, the vocabularies returned in the list are limited to vocabularies whose name contains the specified string\. The search is case\-insensitive, `ListVocabularies` returns both "vocabularyname" and "VocabularyName" in the response list\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 200\.  
Pattern: `^[0-9a-zA-Z._-]+`   
Required: No

 ** [NextToken](#API_ListVocabularies_RequestSyntax) **   <a name="transcribe-ListVocabularies-request-NextToken"></a>
If the result of the previous request to `ListVocabularies` was truncated, include the `NextToken` to fetch the next set of jobs\.  
Type: String  
Length Constraints: Maximum length of 8192\.  
Pattern: `.+`   
Required: No

 ** [StateEquals](#API_ListVocabularies_RequestSyntax) **   <a name="transcribe-ListVocabularies-request-StateEquals"></a>
When specified, only returns vocabularies with the `VocabularyState` field equal to the specified state\.  
Type: String  
Valid Values:` PENDING | READY | FAILED`   
Required: No

## Response Syntax<a name="API_ListVocabularies_ResponseSyntax"></a>

```
{
   "[NextToken](#transcribe-ListVocabularies-response-NextToken)": "string",
   "[Status](#transcribe-ListVocabularies-response-Status)": "string",
   "[Vocabularies](#transcribe-ListVocabularies-response-Vocabularies)": [ 
      { 
         "[LanguageCode](API_VocabularyInfo.md#transcribe-Type-VocabularyInfo-LanguageCode)": "string",
         "[LastModifiedTime](API_VocabularyInfo.md#transcribe-Type-VocabularyInfo-LastModifiedTime)": number,
         "[VocabularyName](API_VocabularyInfo.md#transcribe-Type-VocabularyInfo-VocabularyName)": "string",
         "[VocabularyState](API_VocabularyInfo.md#transcribe-Type-VocabularyInfo-VocabularyState)": "string"
      }
   ]
}
```

## Response Elements<a name="API_ListVocabularies_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [NextToken](#API_ListVocabularies_ResponseSyntax) **   <a name="transcribe-ListVocabularies-response-NextToken"></a>
The `ListVocabularies` operation returns a page of vocabularies at a time\. The maximum size of the page is set by the `MaxResults` parameter\. If there are more jobs in the list than the page size, Amazon Transcribe returns the `NextPage` token\. Include the token in the next request to the `ListVocabularies` operation to return in the next page of jobs\.  
Type: String  
Length Constraints: Maximum length of 8192\.  
Pattern: `.+` 

 ** [Status](#API_ListVocabularies_ResponseSyntax) **   <a name="transcribe-ListVocabularies-response-Status"></a>
The requested vocabulary state\.  
Type: String  
Valid Values:` PENDING | READY | FAILED` 

 ** [Vocabularies](#API_ListVocabularies_ResponseSyntax) **   <a name="transcribe-ListVocabularies-response-Vocabularies"></a>
A list of objects that describe the vocabularies that match the search criteria in the request\.  
Type: Array of [VocabularyInfo](API_VocabularyInfo.md) objects

## Errors<a name="API_ListVocabularies_Errors"></a>

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

## See Also<a name="API_ListVocabularies_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/transcribe-2017-10-26/ListVocabularies) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/transcribe-2017-10-26/ListVocabularies) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transcribe-2017-10-26/ListVocabularies) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transcribe-2017-10-26/ListVocabularies) 
+  [AWS SDK for Java](https://docs.aws.amazon.com/goto/SdkForJava/transcribe-2017-10-26/ListVocabularies) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/transcribe-2017-10-26/ListVocabularies) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/transcribe-2017-10-26/ListVocabularies) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/transcribe-2017-10-26/ListVocabularies) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transcribe-2017-10-26/ListVocabularies) 