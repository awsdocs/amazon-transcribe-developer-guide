# CreateLanguageModel<a name="API_CreateLanguageModel"></a>

Creates a new custom language model\. Use Amazon S3 prefixes to provide the location of your input files\. The time it takes to create your model depends on the size of your training data\.

## Request Syntax<a name="API_CreateLanguageModel_RequestSyntax"></a>

```
{
   "BaseModelName": "string",
   "InputDataConfig": { 
      "DataAccessRoleArn": "string",
      "S3Uri": "string",
      "TuningDataS3Uri": "string"
   },
   "LanguageCode": "string",
   "ModelName": "string"
}
```

## Request Parameters<a name="API_CreateLanguageModel_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [BaseModelName](#API_CreateLanguageModel_RequestSyntax) **   <a name="transcribe-CreateLanguageModel-request-BaseModelName"></a>
The Amazon Transcribe standard language model, or base model used to create your custom language model\.  
If you want to use your custom language model to transcribe audio with a sample rate of 16 kHz or greater, choose `Wideband`\.  
If you want to use your custom language model to transcribe audio with a sample rate that is less than 16 kHz, choose `Narrowband`\.  
Type: String  
Valid Values:` NarrowBand | WideBand`   
Required: Yes

 ** [InputDataConfig](#API_CreateLanguageModel_RequestSyntax) **   <a name="transcribe-CreateLanguageModel-request-InputDataConfig"></a>
Contains the data access role and the Amazon S3 prefixes to read the required input files to create a custom language model\.  
Type: [InputDataConfig](API_InputDataConfig.md) object  
Required: Yes

 ** [LanguageCode](#API_CreateLanguageModel_RequestSyntax) **   <a name="transcribe-CreateLanguageModel-request-LanguageCode"></a>
The language of the input text you're using to train your custom language model\.  
Type: String  
Valid Values:` en-US | hi-IN | es-US | en-GB | en-AU`   
Required: Yes

 ** [ModelName](#API_CreateLanguageModel_RequestSyntax) **   <a name="transcribe-CreateLanguageModel-request-ModelName"></a>
The name you choose for your custom language model when you create it\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 200\.  
Pattern: `^[0-9a-zA-Z._-]+`   
Required: Yes

## Response Syntax<a name="API_CreateLanguageModel_ResponseSyntax"></a>

```
{
   "BaseModelName": "string",
   "InputDataConfig": { 
      "DataAccessRoleArn": "string",
      "S3Uri": "string",
      "TuningDataS3Uri": "string"
   },
   "LanguageCode": "string",
   "ModelName": "string",
   "ModelStatus": "string"
}
```

## Response Elements<a name="API_CreateLanguageModel_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [BaseModelName](#API_CreateLanguageModel_ResponseSyntax) **   <a name="transcribe-CreateLanguageModel-response-BaseModelName"></a>
The Amazon Transcribe standard language model, or base model you've used to create a custom language model\.  
Type: String  
Valid Values:` NarrowBand | WideBand` 

 ** [InputDataConfig](#API_CreateLanguageModel_ResponseSyntax) **   <a name="transcribe-CreateLanguageModel-response-InputDataConfig"></a>
The data access role and Amazon S3 prefixes you've chosen to create your custom language model\.  
Type: [InputDataConfig](API_InputDataConfig.md) object

 ** [LanguageCode](#API_CreateLanguageModel_ResponseSyntax) **   <a name="transcribe-CreateLanguageModel-response-LanguageCode"></a>
The language code of the text you've used to create a custom language model\.  
Type: String  
Valid Values:` en-US | hi-IN | es-US | en-GB | en-AU` 

 ** [ModelName](#API_CreateLanguageModel_ResponseSyntax) **   <a name="transcribe-CreateLanguageModel-response-ModelName"></a>
The name you've chosen for your custom language model\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 200\.  
Pattern: `^[0-9a-zA-Z._-]+` 

 ** [ModelStatus](#API_CreateLanguageModel_ResponseSyntax) **   <a name="transcribe-CreateLanguageModel-response-ModelStatus"></a>
The status of the custom language model\. When the status is `COMPLETED` the model is ready to use\.  
Type: String  
Valid Values:` IN_PROGRESS | FAILED | COMPLETED` 

## Errors<a name="API_CreateLanguageModel_Errors"></a>

For information about the errors that are common to all actions, see [Common Errors](CommonErrors.md)\.

 **BadRequestException**   
Your request didn't pass one or more validation tests\. For example, if the entity that you're trying to delete doesn't exist or if it is in a non\-terminal state \(for example, it's "in progress"\)\. See the exception `Message` field for more information\.  
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

## See Also<a name="API_CreateLanguageModel_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/transcribe-2017-10-26/CreateLanguageModel) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/transcribe-2017-10-26/CreateLanguageModel) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transcribe-2017-10-26/CreateLanguageModel) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transcribe-2017-10-26/CreateLanguageModel) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transcribe-2017-10-26/CreateLanguageModel) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/transcribe-2017-10-26/CreateLanguageModel) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/transcribe-2017-10-26/CreateLanguageModel) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/transcribe-2017-10-26/CreateLanguageModel) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transcribe-2017-10-26/CreateLanguageModel) 