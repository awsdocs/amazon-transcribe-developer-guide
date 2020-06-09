# UpdateVocabularyFilter<a name="API_UpdateVocabularyFilter"></a>

Updates a vocabulary filter with a new list of filtered words\.

## Request Syntax<a name="API_UpdateVocabularyFilter_RequestSyntax"></a>

```
{
   "[VocabularyFilterFileUri](#transcribe-UpdateVocabularyFilter-request-VocabularyFilterFileUri)": "string",
   "[VocabularyFilterName](#transcribe-UpdateVocabularyFilter-request-VocabularyFilterName)": "string",
   "[Words](#transcribe-UpdateVocabularyFilter-request-Words)": [ "string" ]
}
```

## Request Parameters<a name="API_UpdateVocabularyFilter_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [VocabularyFilterFileUri](#API_UpdateVocabularyFilter_RequestSyntax) **   <a name="transcribe-UpdateVocabularyFilter-request-VocabularyFilterFileUri"></a>
The Amazon S3 location of a text file used as input to create the vocabulary filter\. Only use characters from the character set defined for custom vocabularies\. For a list of character sets, see [Character Sets for Custom Vocabularies](https://docs.aws.amazon.com/transcribe/latest/dg/how-vocabulary.html#charsets)\.  
The specified file must be less than 50 KB of UTF\-8 characters\.  
If you provide the location of a list of words in the `VocabularyFilterFileUri` parameter, you can't use the `Words` parameter\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 2000\.  
Pattern: `(s3://|http(s*)://).+`   
Required: No

 ** [VocabularyFilterName](#API_UpdateVocabularyFilter_RequestSyntax) **   <a name="transcribe-UpdateVocabularyFilter-request-VocabularyFilterName"></a>
The name of the vocabulary filter to update\. If you try to update a vocabulary filter with the same name as another vocabulary filter, you get a `ConflictException` error\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 200\.  
Pattern: `^[0-9a-zA-Z._-]+`   
Required: Yes

 ** [Words](#API_UpdateVocabularyFilter_RequestSyntax) **   <a name="transcribe-UpdateVocabularyFilter-request-Words"></a>
The words to use in the vocabulary filter\. Only use characters from the character set defined for custom vocabularies\. For a list of character sets, see [Character Sets for Custom Vocabularies](https://docs.aws.amazon.com/transcribe/latest/dg/how-vocabulary.html#charsets)\.  
If you provide a list of words in the `Words` parameter, you can't use the `VocabularyFilterFileUri` parameter\.  
Type: Array of strings  
Array Members: Minimum number of 1 item\.  
Length Constraints: Minimum length of 1\. Maximum length of 256\.  
Required: No

## Response Syntax<a name="API_UpdateVocabularyFilter_ResponseSyntax"></a>

```
{
   "[LanguageCode](#transcribe-UpdateVocabularyFilter-response-LanguageCode)": "string",
   "[LastModifiedTime](#transcribe-UpdateVocabularyFilter-response-LastModifiedTime)": number,
   "[VocabularyFilterName](#transcribe-UpdateVocabularyFilter-response-VocabularyFilterName)": "string"
}
```

## Response Elements<a name="API_UpdateVocabularyFilter_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [LanguageCode](#API_UpdateVocabularyFilter_ResponseSyntax) **   <a name="transcribe-UpdateVocabularyFilter-response-LanguageCode"></a>
The language code of the words in the vocabulary filter\.  
Type: String  
Valid Values:` en-US | es-US | en-AU | fr-CA | en-GB | de-DE | pt-BR | fr-FR | it-IT | ko-KR | es-ES | en-IN | hi-IN | ar-SA | ru-RU | zh-CN | nl-NL | id-ID | ta-IN | fa-IR | en-IE | en-AB | en-WL | pt-PT | te-IN | tr-TR | de-CH | he-IL | ms-MY | ja-JP | ar-AE` 

 ** [LastModifiedTime](#API_UpdateVocabularyFilter_ResponseSyntax) **   <a name="transcribe-UpdateVocabularyFilter-response-LastModifiedTime"></a>
The date and time that the vocabulary filter was updated\.  
Type: Timestamp

 ** [VocabularyFilterName](#API_UpdateVocabularyFilter_ResponseSyntax) **   <a name="transcribe-UpdateVocabularyFilter-response-VocabularyFilterName"></a>
The name of the updated vocabulary filter\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 200\.  
Pattern: `^[0-9a-zA-Z._-]+` 

## Errors<a name="API_UpdateVocabularyFilter_Errors"></a>

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

 **NotFoundException**   
We can't find the requested resource\. Check the name and try your request again\.  
HTTP Status Code: 400

## See Also<a name="API_UpdateVocabularyFilter_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/transcribe-2017-10-26/UpdateVocabularyFilter) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/transcribe-2017-10-26/UpdateVocabularyFilter) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transcribe-2017-10-26/UpdateVocabularyFilter) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transcribe-2017-10-26/UpdateVocabularyFilter) 
+  [AWS SDK for Java](https://docs.aws.amazon.com/goto/SdkForJava/transcribe-2017-10-26/UpdateVocabularyFilter) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/transcribe-2017-10-26/UpdateVocabularyFilter) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/transcribe-2017-10-26/UpdateVocabularyFilter) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/transcribe-2017-10-26/UpdateVocabularyFilter) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transcribe-2017-10-26/UpdateVocabularyFilter) 