# ListMedicalVocabularies<a name="API_ListMedicalVocabularies"></a>

Returns a list of vocabularies that match the specified criteria\. If you don't enter a value in any of the request parameters, returns the entire list of vocabularies\.

## Request Syntax<a name="API_ListMedicalVocabularies_RequestSyntax"></a>

```
{
   "[MaxResults](#transcribe-ListMedicalVocabularies-request-MaxResults)": number,
   "[NameContains](#transcribe-ListMedicalVocabularies-request-NameContains)": "string",
   "[NextToken](#transcribe-ListMedicalVocabularies-request-NextToken)": "string",
   "[StateEquals](#transcribe-ListMedicalVocabularies-request-StateEquals)": "string"
}
```

## Request Parameters<a name="API_ListMedicalVocabularies_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [MaxResults](#API_ListMedicalVocabularies_RequestSyntax) **   <a name="transcribe-ListMedicalVocabularies-request-MaxResults"></a>
The maximum number of vocabularies to return in the response\.  
Type: Integer  
Valid Range: Minimum value of 1\. Maximum value of 100\.  
Required: No

 ** [NameContains](#API_ListMedicalVocabularies_RequestSyntax) **   <a name="transcribe-ListMedicalVocabularies-request-NameContains"></a>
Returns vocabularies whose names contain the specified string\. The search is not case sensitive\. `ListMedicalVocabularies` returns both "`vocabularyname`" and "`VocabularyName`"\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 200\.  
Pattern: `^[0-9a-zA-Z._-]+`   
Required: No

 ** [NextToken](#API_ListMedicalVocabularies_RequestSyntax) **   <a name="transcribe-ListMedicalVocabularies-request-NextToken"></a>
If the result of your previous request to `ListMedicalVocabularies` was truncated, include the `NextToken` to fetch the next set of vocabularies\.  
Type: String  
Length Constraints: Maximum length of 8192\.  
Pattern: `.+`   
Required: No

 ** [StateEquals](#API_ListMedicalVocabularies_RequestSyntax) **   <a name="transcribe-ListMedicalVocabularies-request-StateEquals"></a>
When specified, returns only vocabularies with the `VocabularyState` equal to the specified vocabulary state\. Use this field to see which vocabularies are ready for your medical transcription jobs\.  
Type: String  
Valid Values:` PENDING | READY | FAILED`   
Required: No

## Response Syntax<a name="API_ListMedicalVocabularies_ResponseSyntax"></a>

```
{
   "[NextToken](#transcribe-ListMedicalVocabularies-response-NextToken)": "string",
   "[Status](#transcribe-ListMedicalVocabularies-response-Status)": "string",
   "[Vocabularies](#transcribe-ListMedicalVocabularies-response-Vocabularies)": [ 
      { 
         "[LanguageCode](API_VocabularyInfo.md#transcribe-Type-VocabularyInfo-LanguageCode)": "string",
         "[LastModifiedTime](API_VocabularyInfo.md#transcribe-Type-VocabularyInfo-LastModifiedTime)": number,
         "[VocabularyName](API_VocabularyInfo.md#transcribe-Type-VocabularyInfo-VocabularyName)": "string",
         "[VocabularyState](API_VocabularyInfo.md#transcribe-Type-VocabularyInfo-VocabularyState)": "string"
      }
   ]
}
```

## Response Elements<a name="API_ListMedicalVocabularies_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [NextToken](#API_ListMedicalVocabularies_ResponseSyntax) **   <a name="transcribe-ListMedicalVocabularies-response-NextToken"></a>
The `ListMedicalVocabularies` operation returns a page of vocabularies at a time\. You set the maximum number of vocabularies to return on a page with the `MaxResults` parameter\. If there are more jobs in the list will fit on a page, Amazon Transcribe Medical returns the `NextPage` token\. To return the next page of vocabularies, include the token in the next request to the `ListMedicalVocabularies` operation \.  
Type: String  
Length Constraints: Maximum length of 8192\.  
Pattern: `.+` 

 ** [Status](#API_ListMedicalVocabularies_ResponseSyntax) **   <a name="transcribe-ListMedicalVocabularies-response-Status"></a>
The requested vocabulary state\.  
Type: String  
Valid Values:` PENDING | READY | FAILED` 

 ** [Vocabularies](#API_ListMedicalVocabularies_ResponseSyntax) **   <a name="transcribe-ListMedicalVocabularies-response-Vocabularies"></a>
A list of objects that describe the vocabularies that match your search criteria\.  
Type: Array of [VocabularyInfo](API_VocabularyInfo.md) objects

## Errors<a name="API_ListMedicalVocabularies_Errors"></a>

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

## See Also<a name="API_ListMedicalVocabularies_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/transcribe-2017-10-26/ListMedicalVocabularies) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/transcribe-2017-10-26/ListMedicalVocabularies) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transcribe-2017-10-26/ListMedicalVocabularies) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transcribe-2017-10-26/ListMedicalVocabularies) 
+  [AWS SDK for Java](https://docs.aws.amazon.com/goto/SdkForJava/transcribe-2017-10-26/ListMedicalVocabularies) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/transcribe-2017-10-26/ListMedicalVocabularies) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/transcribe-2017-10-26/ListMedicalVocabularies) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/transcribe-2017-10-26/ListMedicalVocabularies) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transcribe-2017-10-26/ListMedicalVocabularies) 