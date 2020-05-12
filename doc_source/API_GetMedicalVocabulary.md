# GetMedicalVocabulary<a name="API_GetMedicalVocabulary"></a>

Retrieve information about a medical vocabulary\.

## Request Syntax<a name="API_GetMedicalVocabulary_RequestSyntax"></a>

```
{
   "[VocabularyName](#transcribe-GetMedicalVocabulary-request-VocabularyName)": "string"
}
```

## Request Parameters<a name="API_GetMedicalVocabulary_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [VocabularyName](#API_GetMedicalVocabulary_RequestSyntax) **   <a name="transcribe-GetMedicalVocabulary-request-VocabularyName"></a>
The name of the vocabulary you are trying to get information about\. The value you enter for this request is case\-sensitive\.   
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 200\.  
Pattern: `^[0-9a-zA-Z._-]+`   
Required: Yes

## Response Syntax<a name="API_GetMedicalVocabulary_ResponseSyntax"></a>

```
{
   "[DownloadUri](#transcribe-GetMedicalVocabulary-response-DownloadUri)": "string",
   "[FailureReason](#transcribe-GetMedicalVocabulary-response-FailureReason)": "string",
   "[LanguageCode](#transcribe-GetMedicalVocabulary-response-LanguageCode)": "string",
   "[LastModifiedTime](#transcribe-GetMedicalVocabulary-response-LastModifiedTime)": number,
   "[VocabularyName](#transcribe-GetMedicalVocabulary-response-VocabularyName)": "string",
   "[VocabularyState](#transcribe-GetMedicalVocabulary-response-VocabularyState)": "string"
}
```

## Response Elements<a name="API_GetMedicalVocabulary_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [DownloadUri](#API_GetMedicalVocabulary_ResponseSyntax) **   <a name="transcribe-GetMedicalVocabulary-response-DownloadUri"></a>
The Amazon S3 location where the vocabulary is stored\. Use this URI to get the contents of the vocabulary\. You can download your vocabulary from the URI for a limited time\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 2000\.  
Pattern: `(s3://|http(s*)://).+` 

 ** [FailureReason](#API_GetMedicalVocabulary_ResponseSyntax) **   <a name="transcribe-GetMedicalVocabulary-response-FailureReason"></a>
If the `VocabularyState` is `FAILED`, this field contains information about why the job failed\.  
Type: String

 ** [LanguageCode](#API_GetMedicalVocabulary_ResponseSyntax) **   <a name="transcribe-GetMedicalVocabulary-response-LanguageCode"></a>
The valid language code returned for your vocabulary entries\.  
Type: String  
Valid Values:` en-US | es-US | en-AU | fr-CA | en-GB | de-DE | pt-BR | fr-FR | it-IT | ko-KR | es-ES | en-IN | hi-IN | ar-SA | ru-RU | zh-CN | nl-NL | id-ID | ta-IN | fa-IR | en-IE | en-AB | en-WL | pt-PT | te-IN | tr-TR | de-CH | he-IL | ms-MY | ja-JP | ar-AE` 

 ** [LastModifiedTime](#API_GetMedicalVocabulary_ResponseSyntax) **   <a name="transcribe-GetMedicalVocabulary-response-LastModifiedTime"></a>
The date and time the vocabulary was last modified with a text file different from what was previously used\.  
Type: Timestamp

 ** [VocabularyName](#API_GetMedicalVocabulary_ResponseSyntax) **   <a name="transcribe-GetMedicalVocabulary-response-VocabularyName"></a>
The valid name that Amazon Transcribe Medical returns\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 200\.  
Pattern: `^[0-9a-zA-Z._-]+` 

 ** [VocabularyState](#API_GetMedicalVocabulary_ResponseSyntax) **   <a name="transcribe-GetMedicalVocabulary-response-VocabularyState"></a>
The processing state of the vocabulary\.  
Type: String  
Valid Values:` PENDING | READY | FAILED` 

## Errors<a name="API_GetMedicalVocabulary_Errors"></a>

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

## See Also<a name="API_GetMedicalVocabulary_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/transcribe-2017-10-26/GetMedicalVocabulary) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/transcribe-2017-10-26/GetMedicalVocabulary) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transcribe-2017-10-26/GetMedicalVocabulary) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transcribe-2017-10-26/GetMedicalVocabulary) 
+  [AWS SDK for Java](https://docs.aws.amazon.com/goto/SdkForJava/transcribe-2017-10-26/GetMedicalVocabulary) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/transcribe-2017-10-26/GetMedicalVocabulary) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/transcribe-2017-10-26/GetMedicalVocabulary) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/transcribe-2017-10-26/GetMedicalVocabulary) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transcribe-2017-10-26/GetMedicalVocabulary) 