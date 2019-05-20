# UpdateVocabulary<a name="API_UpdateVocabulary"></a>

Updates an existing vocabulary with new values\. The `UpdateVocabulary` operation overwrites all of the existing information with the values that you provide in the request\. 

## Request Syntax<a name="API_UpdateVocabulary_RequestSyntax"></a>

```
{
   "[LanguageCode](#transcribe-UpdateVocabulary-request-LanguageCode)": "string",
   "[Phrases](#transcribe-UpdateVocabulary-request-Phrases)": [ "string" ],
   "[VocabularyFileUri](#transcribe-UpdateVocabulary-request-VocabularyFileUri)": "string",
   "[VocabularyName](#transcribe-UpdateVocabulary-request-VocabularyName)": "string"
}
```

## Request Parameters<a name="API_UpdateVocabulary_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [LanguageCode](#API_UpdateVocabulary_RequestSyntax) **   <a name="transcribe-UpdateVocabulary-request-LanguageCode"></a>
The language code of the vocabulary entries\.  
Type: String  
Valid Values:` en-US | es-US | en-AU | fr-CA | en-GB | de-DE | pt-BR | fr-FR | it-IT | ko-KR | es-ES | en-IN | hi-IN`   
Required: Yes

 ** [Phrases](#API_UpdateVocabulary_RequestSyntax) **   <a name="transcribe-UpdateVocabulary-request-Phrases"></a>
An array of strings containing the vocabulary entries\.  
Type: Array of strings  
Length Constraints: Minimum length of 0\. Maximum length of 256\.  
Required: No

 ** [VocabularyFileUri](#API_UpdateVocabulary_RequestSyntax) **   <a name="transcribe-UpdateVocabulary-request-VocabularyFileUri"></a>
The S3 location of the text file that contains the definition of the custom vocabulary\. The URI must be in the same region as the API endpoint that you are calling\. The general form is   
 ` https://s3-<aws-region>.amazonaws.com/<bucket-name>/<keyprefix>/<objectkey> `   
For example:  
 `https://s3-us-east-1.amazonaws.com/examplebucket/vocab.txt`   
For more information about S3 object names, see [Object Keys](http://docs.aws.amazon.com/AmazonS3/latest/dev/UsingMetadata.html#object-keys) in the *Amazon S3 Developer Guide*\.  
For more information about custom vocabularies, see [Custom Vocabularies](http://docs.aws.amazon.com/transcribe/latest/dg/how-it-works.html#how-vocabulary)\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 2000\.  
Required: No

 ** [VocabularyName](#API_UpdateVocabulary_RequestSyntax) **   <a name="transcribe-UpdateVocabulary-request-VocabularyName"></a>
The name of the vocabulary to update\. The name is case\-sensitive\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 200\.  
Pattern: `^[0-9a-zA-Z._-]+`   
Required: Yes

## Response Syntax<a name="API_UpdateVocabulary_ResponseSyntax"></a>

```
{
   "[LanguageCode](#transcribe-UpdateVocabulary-response-LanguageCode)": "string",
   "[LastModifiedTime](#transcribe-UpdateVocabulary-response-LastModifiedTime)": number,
   "[VocabularyName](#transcribe-UpdateVocabulary-response-VocabularyName)": "string",
   "[VocabularyState](#transcribe-UpdateVocabulary-response-VocabularyState)": "string"
}
```

## Response Elements<a name="API_UpdateVocabulary_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [LanguageCode](#API_UpdateVocabulary_ResponseSyntax) **   <a name="transcribe-UpdateVocabulary-response-LanguageCode"></a>
The language code of the vocabulary entries\.  
Type: String  
Valid Values:` en-US | es-US | en-AU | fr-CA | en-GB | de-DE | pt-BR | fr-FR | it-IT | ko-KR | es-ES | en-IN | hi-IN` 

 ** [LastModifiedTime](#API_UpdateVocabulary_ResponseSyntax) **   <a name="transcribe-UpdateVocabulary-response-LastModifiedTime"></a>
The date and time that the vocabulary was updated\.  
Type: Timestamp

 ** [VocabularyName](#API_UpdateVocabulary_ResponseSyntax) **   <a name="transcribe-UpdateVocabulary-response-VocabularyName"></a>
The name of the vocabulary that was updated\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 200\.  
Pattern: `^[0-9a-zA-Z._-]+` 

 ** [VocabularyState](#API_UpdateVocabulary_ResponseSyntax) **   <a name="transcribe-UpdateVocabulary-response-VocabularyState"></a>
The processing state of the vocabulary\. When the `VocabularyState` field contains `READY` the vocabulary is ready to be used in a `StartTranscriptionJob` request\.  
Type: String  
Valid Values:` PENDING | READY | FAILED` 

## Errors<a name="API_UpdateVocabulary_Errors"></a>

For information about the errors that are common to all actions, see [Common Errors](CommonErrors.md)\.

 **BadRequestException**   
Your request didn't pass one or more validation tests\. For example, if the transcription you're trying to delete doesn't exist or if it is in a non\-terminal state \(for example, it's "in progress"\)\. See the exception `Message` field for more information\.  
HTTP Status Code: 400

 **ConflictException**   
When you are using the `StartTranscriptionJob` operation, the `JobName` field is a duplicate of a previously entered job name\. Resend your request with a different name\.  
When you are using the `UpdateVocabulary` operation, there are two jobs running at the same time\. Resend the second request later\.  
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

## See Also<a name="API_UpdateVocabulary_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/transcribe-2017-10-26/UpdateVocabulary) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/transcribe-2017-10-26/UpdateVocabulary) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transcribe-2017-10-26/UpdateVocabulary) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transcribe-2017-10-26/UpdateVocabulary) 
+  [AWS SDK for Go \- Pilot](https://docs.aws.amazon.com/goto/SdkForGoPilot/transcribe-2017-10-26/UpdateVocabulary) 
+  [AWS SDK for Java](https://docs.aws.amazon.com/goto/SdkForJava/transcribe-2017-10-26/UpdateVocabulary) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/transcribe-2017-10-26/UpdateVocabulary) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/transcribe-2017-10-26/UpdateVocabulary) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/transcribe-2017-10-26/UpdateVocabulary) 
+  [AWS SDK for Ruby V2](https://docs.aws.amazon.com/goto/SdkForRubyV2/transcribe-2017-10-26/UpdateVocabulary) 