# CreateVocabularyFilter<a name="API_CreateVocabularyFilter"></a>

Creates a new vocabulary filter that you can use to filter words, such as profane words, from the output of a transcription job\.

## Request Syntax<a name="API_CreateVocabularyFilter_RequestSyntax"></a>

```
{
   "LanguageCode": "string",
   "Tags": [ 
      { 
         "Key": "string",
         "Value": "string"
      }
   ],
   "VocabularyFilterFileUri": "string",
   "VocabularyFilterName": "string",
   "Words": [ "string" ]
}
```

## Request Parameters<a name="API_CreateVocabularyFilter_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [ LanguageCode ](#API_CreateVocabularyFilter_RequestSyntax) **   <a name="transcribe-CreateVocabularyFilter-request-LanguageCode"></a>
The language code of the words in the vocabulary filter\. All words in the filter must be in the same language\. The vocabulary filter can only be used with transcription jobs in the specified language\.  
Type: String  
Valid Values:` af-ZA | ar-AE | ar-SA | cy-GB | da-DK | de-CH | de-DE | en-AB | en-AU | en-GB | en-IE | en-IN | en-US | en-WL | es-ES | es-US | fa-IR | fr-CA | fr-FR | ga-IE | gd-GB | he-IL | hi-IN | id-ID | it-IT | ja-JP | ko-KR | ms-MY | nl-NL | pt-BR | pt-PT | ru-RU | ta-IN | te-IN | tr-TR | zh-CN | zh-TW | th-TH | en-ZA | en-NZ`   
Required: Yes

 ** [ Tags ](#API_CreateVocabularyFilter_RequestSyntax) **   <a name="transcribe-CreateVocabularyFilter-request-Tags"></a>
Adds one or more tags, each in the form of a key:value pair, to a new Amazon Transcribe vocabulary filter at the time you create this new vocabulary filter\.  
Type: Array of [ Tag ](API_Tag.md) objects  
Array Members: Minimum number of 1 item\. Maximum number of 200 items\.  
Required: No

 ** [ VocabularyFilterFileUri ](#API_CreateVocabularyFilter_RequestSyntax) **   <a name="transcribe-CreateVocabularyFilter-request-VocabularyFilterFileUri"></a>
The Amazon S3 location of a text file used as input to create the vocabulary filter\. Only use characters from the character set defined for custom vocabularies\. For a list of character sets, see [Character Sets for Custom Vocabularies](https://docs.aws.amazon.com/transcribe/latest/dg/how-vocabulary.html#charsets)\.  
The specified file must be less than 50 KB of UTF\-8 characters\.  
If you provide the location of a list of words in the `VocabularyFilterFileUri` parameter, you can't use the `Words` parameter\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 2000\.  
Pattern: `(s3://|http(s*)://).+`   
Required: No

 ** [ VocabularyFilterName ](#API_CreateVocabularyFilter_RequestSyntax) **   <a name="transcribe-CreateVocabularyFilter-request-VocabularyFilterName"></a>
The vocabulary filter name\. The name must be unique within the account that contains it\. If you try to create a vocabulary filter with the same name as another vocabulary filter, you get a `ConflictException` error\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 200\.  
Pattern: `^[0-9a-zA-Z._-]+`   
Required: Yes

 ** [ Words ](#API_CreateVocabularyFilter_RequestSyntax) **   <a name="transcribe-CreateVocabularyFilter-request-Words"></a>
The words to use in the vocabulary filter\. Only use characters from the character set defined for custom vocabularies\. For a list of character sets, see [Character Sets for Custom Vocabularies](https://docs.aws.amazon.com/transcribe/latest/dg/how-vocabulary.html#charsets)\.  
If you provide a list of words in the `Words` parameter, you can't use the `VocabularyFilterFileUri` parameter\.  
Type: Array of strings  
Array Members: Minimum number of 1 item\.  
Length Constraints: Minimum length of 1\. Maximum length of 256\.  
Required: No

## Response Syntax<a name="API_CreateVocabularyFilter_ResponseSyntax"></a>

```
{
   "LanguageCode": "string",
   "LastModifiedTime": number,
   "VocabularyFilterName": "string"
}
```

## Response Elements<a name="API_CreateVocabularyFilter_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [ LanguageCode ](#API_CreateVocabularyFilter_ResponseSyntax) **   <a name="transcribe-CreateVocabularyFilter-response-LanguageCode"></a>
The language code of the words in the collection\.  
Type: String  
Valid Values:` af-ZA | ar-AE | ar-SA | cy-GB | da-DK | de-CH | de-DE | en-AB | en-AU | en-GB | en-IE | en-IN | en-US | en-WL | es-ES | es-US | fa-IR | fr-CA | fr-FR | ga-IE | gd-GB | he-IL | hi-IN | id-ID | it-IT | ja-JP | ko-KR | ms-MY | nl-NL | pt-BR | pt-PT | ru-RU | ta-IN | te-IN | tr-TR | zh-CN | zh-TW | th-TH | en-ZA | en-NZ` 

 ** [ LastModifiedTime ](#API_CreateVocabularyFilter_ResponseSyntax) **   <a name="transcribe-CreateVocabularyFilter-response-LastModifiedTime"></a>
The date and time that the vocabulary filter was modified\.  
Type: Timestamp

 ** [ VocabularyFilterName ](#API_CreateVocabularyFilter_ResponseSyntax) **   <a name="transcribe-CreateVocabularyFilter-response-VocabularyFilterName"></a>
The name of the vocabulary filter\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 200\.  
Pattern: `^[0-9a-zA-Z._-]+` 

## Errors<a name="API_CreateVocabularyFilter_Errors"></a>

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

## See Also<a name="API_CreateVocabularyFilter_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [ AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/transcribe-2017-10-26/CreateVocabularyFilter) 
+  [ AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/transcribe-2017-10-26/CreateVocabularyFilter) 
+  [ AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transcribe-2017-10-26/CreateVocabularyFilter) 
+  [ AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transcribe-2017-10-26/CreateVocabularyFilter) 
+  [ AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transcribe-2017-10-26/CreateVocabularyFilter) 
+  [ AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/transcribe-2017-10-26/CreateVocabularyFilter) 
+  [ AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/transcribe-2017-10-26/CreateVocabularyFilter) 
+  [ AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/transcribe-2017-10-26/CreateVocabularyFilter) 
+  [ AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transcribe-2017-10-26/CreateVocabularyFilter) 