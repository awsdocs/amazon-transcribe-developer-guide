# GetMedicalVocabulary<a name="API_GetMedicalVocabulary"></a>

Retrieves information about a medical vocabulary\.

## Request Syntax<a name="API_GetMedicalVocabulary_RequestSyntax"></a>

```
{
   "VocabularyName": "string"
}
```

## Request Parameters<a name="API_GetMedicalVocabulary_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [VocabularyName](#API_GetMedicalVocabulary_RequestSyntax) **   <a name="transcribe-GetMedicalVocabulary-request-VocabularyName"></a>
The name of the vocabulary that you want information about\. The value is case sensitive\.   
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 200\.  
Pattern: `^[0-9a-zA-Z._-]+`   
Required: Yes

## Response Syntax<a name="API_GetMedicalVocabulary_ResponseSyntax"></a>

```
{
   "DownloadUri": "string",
   "FailureReason": "string",
   "LanguageCode": "string",
   "LastModifiedTime": number,
   "VocabularyName": "string",
   "VocabularyState": "string"
}
```

## Response Elements<a name="API_GetMedicalVocabulary_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [DownloadUri](#API_GetMedicalVocabulary_ResponseSyntax) **   <a name="transcribe-GetMedicalVocabulary-response-DownloadUri"></a>
The location in Amazon S3 where the vocabulary is stored\. Use this URI to get the contents of the vocabulary\. You can download your vocabulary from the URI for a limited time\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 2000\.  
Pattern: `(s3://|http(s*)://).+` 

 ** [FailureReason](#API_GetMedicalVocabulary_ResponseSyntax) **   <a name="transcribe-GetMedicalVocabulary-response-FailureReason"></a>
If the `VocabularyState` is `FAILED`, this field contains information about why the job failed\.  
Type: String

 ** [LanguageCode](#API_GetMedicalVocabulary_ResponseSyntax) **   <a name="transcribe-GetMedicalVocabulary-response-LanguageCode"></a>
The valid language code for your vocabulary entries\.  
Type: String  
Valid Values:` af-ZA | ar-AE | ar-SA | cy-GB | da-DK | de-CH | de-DE | en-AB | en-AU | en-GB | en-IE | en-IN | en-US | en-WL | es-ES | es-US | fa-IR | fr-CA | fr-FR | ga-IE | gd-GB | he-IL | hi-IN | id-ID | it-IT | ja-JP | ko-KR | ms-MY | nl-NL | pt-BR | pt-PT | ru-RU | ta-IN | te-IN | tr-TR | zh-CN` 

 ** [LastModifiedTime](#API_GetMedicalVocabulary_ResponseSyntax) **   <a name="transcribe-GetMedicalVocabulary-response-LastModifiedTime"></a>
The date and time that the vocabulary was last modified with a text file different from the one that was previously used\.  
Type: Timestamp

 ** [VocabularyName](#API_GetMedicalVocabulary_ResponseSyntax) **   <a name="transcribe-GetMedicalVocabulary-response-VocabularyName"></a>
The name of the vocabulary returned by Amazon Transcribe Medical\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 200\.  
Pattern: `^[0-9a-zA-Z._-]+` 

 ** [VocabularyState](#API_GetMedicalVocabulary_ResponseSyntax) **   <a name="transcribe-GetMedicalVocabulary-response-VocabularyState"></a>
The processing state of the vocabulary\. If the `VocabularyState` is `READY` then you can use it in the `StartMedicalTranscriptionJob` operation\.   
Type: String  
Valid Values:` PENDING | READY | FAILED` 

## Errors<a name="API_GetMedicalVocabulary_Errors"></a>

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

 **NotFoundException**   
We can't find the requested resource\. Check the name and try your request again\.  
HTTP Status Code: 400

## See Also<a name="API_GetMedicalVocabulary_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/transcribe-2017-10-26/GetMedicalVocabulary) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/transcribe-2017-10-26/GetMedicalVocabulary) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transcribe-2017-10-26/GetMedicalVocabulary) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transcribe-2017-10-26/GetMedicalVocabulary) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transcribe-2017-10-26/GetMedicalVocabulary) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/transcribe-2017-10-26/GetMedicalVocabulary) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/transcribe-2017-10-26/GetMedicalVocabulary) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/transcribe-2017-10-26/GetMedicalVocabulary) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transcribe-2017-10-26/GetMedicalVocabulary) 