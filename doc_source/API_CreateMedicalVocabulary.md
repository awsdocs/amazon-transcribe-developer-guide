# CreateMedicalVocabulary<a name="API_CreateMedicalVocabulary"></a>

Creates a new custom vocabulary that you can use to change how Amazon Transcribe Medical transcribes your audio file\.

## Request Syntax<a name="API_CreateMedicalVocabulary_RequestSyntax"></a>

```
{
   "[LanguageCode](#transcribe-CreateMedicalVocabulary-request-LanguageCode)": "string",
   "[VocabularyFileUri](#transcribe-CreateMedicalVocabulary-request-VocabularyFileUri)": "string",
   "[VocabularyName](#transcribe-CreateMedicalVocabulary-request-VocabularyName)": "string"
}
```

## Request Parameters<a name="API_CreateMedicalVocabulary_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [LanguageCode](#API_CreateMedicalVocabulary_RequestSyntax) **   <a name="transcribe-CreateMedicalVocabulary-request-LanguageCode"></a>
The language code for the language used for the entries in your custom vocabulary\. The language code of your custom vocabulary must match the language code of your transcription job\. US English \(en\-US\) is the only language code available for Amazon Transcribe Medical\.  
Type: String  
Valid Values:` en-US | es-US | en-AU | fr-CA | en-GB | de-DE | pt-BR | fr-FR | it-IT | ko-KR | es-ES | en-IN | hi-IN | ar-SA | ru-RU | zh-CN | nl-NL | id-ID | ta-IN | fa-IR | en-IE | en-AB | en-WL | pt-PT | te-IN | tr-TR | de-CH | he-IL | ms-MY | ja-JP | ar-AE`   
Required: Yes

 ** [VocabularyFileUri](#API_CreateMedicalVocabulary_RequestSyntax) **   <a name="transcribe-CreateMedicalVocabulary-request-VocabularyFileUri"></a>
The location in Amazon S3 of the text file you use to define your custom vocabulary\. The URI must be in the same AWS Region as the resource that you're calling\. Enter information about your `VocabularyFileUri` in the following format:  
 ` https://s3.<aws-region>.amazonaws.com/<bucket-name>/<keyprefix>/<objectkey> `   
The following is an example URI for a vocabulary file that is stored in Amazon S3:  
 `https://s3.us-east-1.amazonaws.com/AWSDOC-EXAMPLE-BUCKET/vocab.txt`   
For more information about Amazon S3 object names, see [Object Keys](http://docs.aws.amazon.com/AmazonS3/latest/dev/UsingMetadata.html#object-keys) in the *Amazon S3 Developer Guide*\.  
For more information about custom vocabularies, see [Medical Custom Vocabularies](http://docs.aws.amazon.com/transcribe/latest/dg/how-it-works.html#how-vocabulary-med)\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 2000\.  
Pattern: `(s3://|http(s*)://).+`   
Required: Yes

 ** [VocabularyName](#API_CreateMedicalVocabulary_RequestSyntax) **   <a name="transcribe-CreateMedicalVocabulary-request-VocabularyName"></a>
The name of the custom vocabulary\. This case\-sensitive name must be unique within an AWS account\. If you try to create a vocabulary with the same name as a previous vocabulary, you get a `ConflictException` error\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 200\.  
Pattern: `^[0-9a-zA-Z._-]+`   
Required: Yes

## Response Syntax<a name="API_CreateMedicalVocabulary_ResponseSyntax"></a>

```
{
   "[FailureReason](#transcribe-CreateMedicalVocabulary-response-FailureReason)": "string",
   "[LanguageCode](#transcribe-CreateMedicalVocabulary-response-LanguageCode)": "string",
   "[LastModifiedTime](#transcribe-CreateMedicalVocabulary-response-LastModifiedTime)": number,
   "[VocabularyName](#transcribe-CreateMedicalVocabulary-response-VocabularyName)": "string",
   "[VocabularyState](#transcribe-CreateMedicalVocabulary-response-VocabularyState)": "string"
}
```

## Response Elements<a name="API_CreateMedicalVocabulary_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [FailureReason](#API_CreateMedicalVocabulary_ResponseSyntax) **   <a name="transcribe-CreateMedicalVocabulary-response-FailureReason"></a>
If the `VocabularyState` field is `FAILED`, this field contains information about why the job failed\.  
Type: String

 ** [LanguageCode](#API_CreateMedicalVocabulary_ResponseSyntax) **   <a name="transcribe-CreateMedicalVocabulary-response-LanguageCode"></a>
The language code for the entries in your custom vocabulary\. US English \(en\-US\) is the only valid language code for Amazon Transcribe Medical\.  
Type: String  
Valid Values:` en-US | es-US | en-AU | fr-CA | en-GB | de-DE | pt-BR | fr-FR | it-IT | ko-KR | es-ES | en-IN | hi-IN | ar-SA | ru-RU | zh-CN | nl-NL | id-ID | ta-IN | fa-IR | en-IE | en-AB | en-WL | pt-PT | te-IN | tr-TR | de-CH | he-IL | ms-MY | ja-JP | ar-AE` 

 ** [LastModifiedTime](#API_CreateMedicalVocabulary_ResponseSyntax) **   <a name="transcribe-CreateMedicalVocabulary-response-LastModifiedTime"></a>
The date and time that you created the vocabulary\.  
Type: Timestamp

 ** [VocabularyName](#API_CreateMedicalVocabulary_ResponseSyntax) **   <a name="transcribe-CreateMedicalVocabulary-response-VocabularyName"></a>
The name of the vocabulary\. The name must be unique within an AWS account and is case sensitive\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 200\.  
Pattern: `^[0-9a-zA-Z._-]+` 

 ** [VocabularyState](#API_CreateMedicalVocabulary_ResponseSyntax) **   <a name="transcribe-CreateMedicalVocabulary-response-VocabularyState"></a>
The processing state of your custom vocabulary in Amazon Transcribe Medical\. If the state is `READY`, you can use the vocabulary in a `StartMedicalTranscriptionJob` request\.  
Type: String  
Valid Values:` PENDING | READY | FAILED` 

## Errors<a name="API_CreateMedicalVocabulary_Errors"></a>

For information about the errors that are common to all actions, see [Common Errors](CommonErrors.md)\.

 **BadRequestException**   
Your request didn't pass one or more validation tests\. For example, if the transcription you're trying to delete doesn't exist or if it is in a non\-terminal state \(for example, it's "in progress"\)\. See the exception `Message` field for more information\.  
HTTP Status Code: 400

 **ConflictException**   
There is already a resource with that name\.  
HTTP Status Code: 400

 **InternalFailureException**   
There was an internal error\. Check the error message and try your request again\.  
HTTP Status Code: 500

 **LimitExceededException**   
Either you have sent too many requests or your input file is too long\. Wait before you resend your request, or use a smaller file and resend the request\.  
HTTP Status Code: 400

## See Also<a name="API_CreateMedicalVocabulary_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/transcribe-2017-10-26/CreateMedicalVocabulary) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/transcribe-2017-10-26/CreateMedicalVocabulary) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transcribe-2017-10-26/CreateMedicalVocabulary) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transcribe-2017-10-26/CreateMedicalVocabulary) 
+  [AWS SDK for Java](https://docs.aws.amazon.com/goto/SdkForJava/transcribe-2017-10-26/CreateMedicalVocabulary) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/transcribe-2017-10-26/CreateMedicalVocabulary) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/transcribe-2017-10-26/CreateMedicalVocabulary) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/transcribe-2017-10-26/CreateMedicalVocabulary) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transcribe-2017-10-26/CreateMedicalVocabulary) 