# ListVocabularyFilters<a name="API_ListVocabularyFilters"></a>

Gets information about vocabulary filters\.

## Request Syntax<a name="API_ListVocabularyFilters_RequestSyntax"></a>

```
{
   "MaxResults": number,
   "NameContains": "string",
   "NextToken": "string"
}
```

## Request Parameters<a name="API_ListVocabularyFilters_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [ MaxResults ](#API_ListVocabularyFilters_RequestSyntax) **   <a name="transcribe-ListVocabularyFilters-request-MaxResults"></a>
The maximum number of filters to return in each page of results\. If there are fewer results than the value you specify, only the actual results are returned\. If you do not specify a value, the default of 5 is used\.  
Type: Integer  
Valid Range: Minimum value of 1\. Maximum value of 100\.  
Required: No

 ** [ NameContains ](#API_ListVocabularyFilters_RequestSyntax) **   <a name="transcribe-ListVocabularyFilters-request-NameContains"></a>
Filters the response so that it only contains vocabulary filters whose name contains the specified string\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 200\.  
Pattern: `^[0-9a-zA-Z._-]+`   
Required: No

 ** [ NextToken ](#API_ListVocabularyFilters_RequestSyntax) **   <a name="transcribe-ListVocabularyFilters-request-NextToken"></a>
If the result of the previous request to `ListVocabularyFilters` was truncated, include the `NextToken` to fetch the next set of collections\.  
Type: String  
Length Constraints: Maximum length of 8192\.  
Pattern: `.+`   
Required: No

## Response Syntax<a name="API_ListVocabularyFilters_ResponseSyntax"></a>

```
{
   "NextToken": "string",
   "VocabularyFilters": [ 
      { 
         "LanguageCode": "string",
         "LastModifiedTime": number,
         "VocabularyFilterName": "string"
      }
   ]
}
```

## Response Elements<a name="API_ListVocabularyFilters_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [ NextToken ](#API_ListVocabularyFilters_ResponseSyntax) **   <a name="transcribe-ListVocabularyFilters-response-NextToken"></a>
The `ListVocabularyFilters` operation returns a page of collections at a time\. The maximum size of the page is set by the `MaxResults` parameter\. If there are more jobs in the list than the page size, Amazon Transcribe returns the `NextPage` token\. Include the token in the next request to the `ListVocabularyFilters` operation to return in the next page of jobs\.  
Type: String  
Length Constraints: Maximum length of 8192\.  
Pattern: `.+` 

 ** [ VocabularyFilters ](#API_ListVocabularyFilters_ResponseSyntax) **   <a name="transcribe-ListVocabularyFilters-response-VocabularyFilters"></a>
The list of vocabulary filters\. It contains at most `MaxResults` number of filters\. If there are more filters, call the `ListVocabularyFilters` operation again with the `NextToken` parameter in the request set to the value of the `NextToken` field in the response\.  
Type: Array of [ VocabularyFilterInfo ](API_VocabularyFilterInfo.md) objects

## Errors<a name="API_ListVocabularyFilters_Errors"></a>

For information about the errors that are common to all actions, see [Common Errors](CommonErrors.md)\.

 ** BadRequestException **   
Your request didn't pass one or more validation tests\. For example, if the entity that you're trying to delete doesn't exist or if it is in a non\-terminal state \(for example, it's "in progress"\)\. See the exception `Message` field for more information\.  
HTTP Status Code: 400

 ** InternalFailureException **   
There was an internal error\. Check the error message and try your request again\.  
HTTP Status Code: 500

 ** LimitExceededException **   
Either you have sent too many requests or your input file is too long\. Wait before you resend your request, or use a smaller file and resend the request\.  
HTTP Status Code: 400

## See Also<a name="API_ListVocabularyFilters_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [ AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/transcribe-2017-10-26/ListVocabularyFilters) 
+  [ AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/transcribe-2017-10-26/ListVocabularyFilters) 
+  [ AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transcribe-2017-10-26/ListVocabularyFilters) 
+  [ AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transcribe-2017-10-26/ListVocabularyFilters) 
+  [ AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transcribe-2017-10-26/ListVocabularyFilters) 
+  [ AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/transcribe-2017-10-26/ListVocabularyFilters) 
+  [ AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/transcribe-2017-10-26/ListVocabularyFilters) 
+  [ AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/transcribe-2017-10-26/ListVocabularyFilters) 
+  [ AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transcribe-2017-10-26/ListVocabularyFilters) 