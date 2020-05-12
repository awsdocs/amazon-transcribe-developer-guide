# UpdateMedicalVocabulary<a name="API_UpdateMedicalVocabulary"></a>

Updates an existing vocabulary with new values in a different text file\. The `UpdateMedicalVocabulary` operation overwrites all of the existing information with the values that you provide in the request\.

## Request Syntax<a name="API_UpdateMedicalVocabulary_RequestSyntax"></a>

```
{
   "[LanguageCode](#transcribe-UpdateMedicalVocabulary-request-LanguageCode)": "string",
   "[VocabularyFileUri](#transcribe-UpdateMedicalVocabulary-request-VocabularyFileUri)": "string",
   "[VocabularyName](#transcribe-UpdateMedicalVocabulary-request-VocabularyName)": "string"
}
```

## Request Parameters<a name="API_UpdateMedicalVocabulary_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [LanguageCode](#API_UpdateMedicalVocabulary_RequestSyntax) **   <a name="transcribe-UpdateMedicalVocabulary-request-LanguageCode"></a>
The language code of the entries in the updated vocabulary\. US English \(en\-US\) is the only valid language code in Amazon Transcribe Medical\.  
Type: String  
Valid Values:` en-US | es-US | en-AU | fr-CA | en-GB | de-DE | pt-BR | fr-FR | it-IT | ko-KR | es-ES | en-IN | hi-IN | ar-SA | ru-RU | zh-CN | nl-NL | id-ID | ta-IN | fa-IR | en-IE | en-AB | en-WL | pt-PT | te-IN | tr-TR | de-CH | he-IL | ms-MY | ja-JP | ar-AE`   
Required: Yes

 ** [VocabularyFileUri](#API_UpdateMedicalVocabulary_RequestSyntax) **   <a name="transcribe-UpdateMedicalVocabulary-request-VocabularyFileUri"></a>
The Amazon S3 location of the text file containing the definition of the custom vocabulary\. The URI must be in the same AWS region as the API endpoint you are calling\. You can see the fields you need to enter for you Amazon S3 location in the example URI here:  
 ` https://s3.<aws-region>.amazonaws.com/<bucket-name>/<keyprefix>/<objectkey> `   
For example:  
 `https://s3.us-east-1.amazonaws.com/AWSDOC-EXAMPLE-BUCKET/vocab.txt`   
For more information about S3 object names, see [Object Keys](http://docs.aws.amazon.com/AmazonS3/latest/dev/UsingMetadata.html#object-keys) in the *Amazon S3 Developer Guide*\.  
For more information about custom vocabularies in Amazon Transcribe Medical, see [Medical Custom Vocabularies](http://docs.aws.amazon.com/transcribe/latest/dg/how-it-works.html#how-vocabulary)\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 2000\.  
Pattern: `(s3://|http(s*)://).+`   
Required: No

 ** [VocabularyName](#API_UpdateMedicalVocabulary_RequestSyntax) **   <a name="transcribe-UpdateMedicalVocabulary-request-VocabularyName"></a>
The name of the vocabulary to update\. The name is case\-sensitive\. If you try to update a vocabulary with the same name as a previous vocabulary you will receive a `ConflictException` error\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 200\.  
Pattern: `^[0-9a-zA-Z._-]+`   
Required: Yes

## Response Syntax<a name="API_UpdateMedicalVocabulary_ResponseSyntax"></a>

```
{
   "[LanguageCode](#transcribe-UpdateMedicalVocabulary-response-LanguageCode)": "string",
   "[LastModifiedTime](#transcribe-UpdateMedicalVocabulary-response-LastModifiedTime)": number,
   "[VocabularyName](#transcribe-UpdateMedicalVocabulary-response-VocabularyName)": "string",
   "[VocabularyState](#transcribe-UpdateMedicalVocabulary-response-VocabularyState)": "string"
}
```

## Response Elements<a name="API_UpdateMedicalVocabulary_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [LanguageCode](#API_UpdateMedicalVocabulary_ResponseSyntax) **   <a name="transcribe-UpdateMedicalVocabulary-response-LanguageCode"></a>
The language code for the text file used to update the custom vocabulary\. US English \(en\-US\) is the only language supported in Amazon Transcribe Medical\.  
Type: String  
Valid Values:` en-US | es-US | en-AU | fr-CA | en-GB | de-DE | pt-BR | fr-FR | it-IT | ko-KR | es-ES | en-IN | hi-IN | ar-SA | ru-RU | zh-CN | nl-NL | id-ID | ta-IN | fa-IR | en-IE | en-AB | en-WL | pt-PT | te-IN | tr-TR | de-CH | he-IL | ms-MY | ja-JP | ar-AE` 

 ** [LastModifiedTime](#API_UpdateMedicalVocabulary_ResponseSyntax) **   <a name="transcribe-UpdateMedicalVocabulary-response-LastModifiedTime"></a>
The date and time the vocabulary was updated\.  
Type: Timestamp

 ** [VocabularyName](#API_UpdateMedicalVocabulary_ResponseSyntax) **   <a name="transcribe-UpdateMedicalVocabulary-response-VocabularyName"></a>
The name of the updated vocabulary\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 200\.  
Pattern: `^[0-9a-zA-Z._-]+` 

 ** [VocabularyState](#API_UpdateMedicalVocabulary_ResponseSyntax) **   <a name="transcribe-UpdateMedicalVocabulary-response-VocabularyState"></a>
The processing state of the update to the vocabulary\. When the `VocabularyState` field is `READY` the vocabulary is ready to be used in a `StartMedicalTranscriptionJob` request\.  
Type: String  
Valid Values:` PENDING | READY | FAILED` 

## Errors<a name="API_UpdateMedicalVocabulary_Errors"></a>

For information about the errors that are common to all actions, see [Common Errors](CommonErrors.md)\.

 **BadRequestException**   
Your request didn't pass one or more validation tests\. For example, if the transcription you're trying to delete doesn't exist or if it is in a non\-terminal state \(for example, it's "in progress"\)\. See the exception `Message` field for more information\.  
HTTP Status Code: 400

 **ConflictException**   
The resource name already exists\.  
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

## See Also<a name="API_UpdateMedicalVocabulary_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/transcribe-2017-10-26/UpdateMedicalVocabulary) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/transcribe-2017-10-26/UpdateMedicalVocabulary) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transcribe-2017-10-26/UpdateMedicalVocabulary) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transcribe-2017-10-26/UpdateMedicalVocabulary) 
+  [AWS SDK for Java](https://docs.aws.amazon.com/goto/SdkForJava/transcribe-2017-10-26/UpdateMedicalVocabulary) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/transcribe-2017-10-26/UpdateMedicalVocabulary) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/transcribe-2017-10-26/UpdateMedicalVocabulary) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/transcribe-2017-10-26/UpdateMedicalVocabulary) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transcribe-2017-10-26/UpdateMedicalVocabulary) 