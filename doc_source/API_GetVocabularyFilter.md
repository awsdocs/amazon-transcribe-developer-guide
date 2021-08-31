# GetVocabularyFilter<a name="API_GetVocabularyFilter"></a>

Returns information about a vocabulary filter\.

## Request Syntax<a name="API_GetVocabularyFilter_RequestSyntax"></a>

```
{
   "VocabularyFilterName": "string"
}
```

## Request Parameters<a name="API_GetVocabularyFilter_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [ VocabularyFilterName ](#API_GetVocabularyFilter_RequestSyntax) **   <a name="transcribe-GetVocabularyFilter-request-VocabularyFilterName"></a>
The name of the vocabulary filter for which to return information\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 200\.  
Pattern: `^[0-9a-zA-Z._-]+`   
Required: Yes

## Response Syntax<a name="API_GetVocabularyFilter_ResponseSyntax"></a>

```
{
   "DownloadUri": "string",
   "LanguageCode": "string",
   "LastModifiedTime": number,
   "VocabularyFilterName": "string"
}
```

## Response Elements<a name="API_GetVocabularyFilter_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [ DownloadUri ](#API_GetVocabularyFilter_ResponseSyntax) **   <a name="transcribe-GetVocabularyFilter-response-DownloadUri"></a>
The URI of the list of words in the vocabulary filter\. You can use this URI to get the list of words\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 2000\.  
Pattern: `(s3://|http(s*)://).+` 

 ** [ LanguageCode ](#API_GetVocabularyFilter_ResponseSyntax) **   <a name="transcribe-GetVocabularyFilter-response-LanguageCode"></a>
The language code of the words in the vocabulary filter\.  
Type: String  
Valid Values:` af-ZA | ar-AE | ar-SA | cy-GB | da-DK | de-CH | de-DE | en-AB | en-AU | en-GB | en-IE | en-IN | en-US | en-WL | es-ES | es-US | fa-IR | fr-CA | fr-FR | ga-IE | gd-GB | he-IL | hi-IN | id-ID | it-IT | ja-JP | ko-KR | ms-MY | nl-NL | pt-BR | pt-PT | ru-RU | ta-IN | te-IN | tr-TR | zh-CN | zh-TW | th-TH | en-ZA | en-NZ` 

 ** [ LastModifiedTime ](#API_GetVocabularyFilter_ResponseSyntax) **   <a name="transcribe-GetVocabularyFilter-response-LastModifiedTime"></a>
The date and time that the contents of the vocabulary filter were updated\.  
Type: Timestamp

 ** [ VocabularyFilterName ](#API_GetVocabularyFilter_ResponseSyntax) **   <a name="transcribe-GetVocabularyFilter-response-VocabularyFilterName"></a>
The name of the vocabulary filter\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 200\.  
Pattern: `^[0-9a-zA-Z._-]+` 

## Errors<a name="API_GetVocabularyFilter_Errors"></a>

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

 ** NotFoundException **   
We can't find the requested resource\. Check the name and try your request again\.  
HTTP Status Code: 400

## See Also<a name="API_GetVocabularyFilter_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [ AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/transcribe-2017-10-26/GetVocabularyFilter) 
+  [ AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/transcribe-2017-10-26/GetVocabularyFilter) 
+  [ AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transcribe-2017-10-26/GetVocabularyFilter) 
+  [ AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transcribe-2017-10-26/GetVocabularyFilter) 
+  [ AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transcribe-2017-10-26/GetVocabularyFilter) 
+  [ AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/transcribe-2017-10-26/GetVocabularyFilter) 
+  [ AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/transcribe-2017-10-26/GetVocabularyFilter) 
+  [ AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/transcribe-2017-10-26/GetVocabularyFilter) 
+  [ AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transcribe-2017-10-26/GetVocabularyFilter) 