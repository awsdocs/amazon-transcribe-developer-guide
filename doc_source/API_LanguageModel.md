# LanguageModel<a name="API_LanguageModel"></a>

The structure used to describe a custom language model\.

## Contents<a name="API_LanguageModel_Contents"></a>

 ** BaseModelName **   <a name="transcribe-Type-LanguageModel-BaseModelName"></a>
The Amazon Transcribe standard language model, or base model used to create the custom language model\.  
Type: String  
Valid Values:` NarrowBand | WideBand`   
Required: No

 ** CreateTime **   <a name="transcribe-Type-LanguageModel-CreateTime"></a>
The time the custom language model was created\.  
Type: Timestamp  
Required: No

 ** FailureReason **   <a name="transcribe-Type-LanguageModel-FailureReason"></a>
The reason why the custom language model couldn't be created\.  
Type: String  
Required: No

 ** InputDataConfig **   <a name="transcribe-Type-LanguageModel-InputDataConfig"></a>
The data access role and Amazon S3 prefixes for the input files used to train the custom language model\.  
Type: [ InputDataConfig ](API_InputDataConfig.md) object  
Required: No

 ** LanguageCode **   <a name="transcribe-Type-LanguageModel-LanguageCode"></a>
The language code you used to create your custom language model\.  
Type: String  
Valid Values:` en-US | hi-IN | es-US | en-GB | en-AU`   
Required: No

 ** LastModifiedTime **   <a name="transcribe-Type-LanguageModel-LastModifiedTime"></a>
The most recent time the custom language model was modified\.  
Type: Timestamp  
Required: No

 ** ModelName **   <a name="transcribe-Type-LanguageModel-ModelName"></a>
The name of the custom language model\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 200\.  
Pattern: `^[0-9a-zA-Z._-]+`   
Required: No

 ** ModelStatus **   <a name="transcribe-Type-LanguageModel-ModelStatus"></a>
The creation status of a custom language model\. When the status is `COMPLETED` the model is ready for use\.  
Type: String  
Valid Values:` IN_PROGRESS | FAILED | COMPLETED`   
Required: No

 ** UpgradeAvailability **   <a name="transcribe-Type-LanguageModel-UpgradeAvailability"></a>
Whether the base model used for the custom language model is up to date\. If this field is `true` then you are running the most up\-to\-date version of the base model in your custom language model\.  
Type: Boolean  
Required: No

## See Also<a name="API_LanguageModel_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [ AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transcribe-2017-10-26/LanguageModel) 
+  [ AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transcribe-2017-10-26/LanguageModel) 
+  [ AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transcribe-2017-10-26/LanguageModel) 
+  [ AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transcribe-2017-10-26/LanguageModel) 