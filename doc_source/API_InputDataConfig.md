# InputDataConfig<a name="API_InputDataConfig"></a>

The object that contains the Amazon S3 object location and access role required to train and tune your custom language model\.

## Contents<a name="API_InputDataConfig_Contents"></a>

 **DataAccessRoleArn**   <a name="transcribe-Type-InputDataConfig-DataAccessRoleArn"></a>
The Amazon Resource Name \(ARN\) that uniquely identifies the permissions you've given Amazon Transcribe to access your Amazon S3 buckets containing your media files or text data\.  
Type: String  
Length Constraints: Minimum length of 20\. Maximum length of 2048\.  
Pattern: `^arn:(aws|aws-cn|aws-us-gov|aws-iso-{0,1}[a-z]{0,1}):iam::[0-9]{0,63}:role/[A-Za-z0-9:_/+=,@.-]{0,1024}$`   
Required: Yes

 **S3Uri**   <a name="transcribe-Type-InputDataConfig-S3Uri"></a>
The Amazon S3 prefix you specify to access the plain text files that you use to train your custom language model\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 2000\.  
Pattern: `(s3://|http(s*)://).+`   
Required: Yes

 **TuningDataS3Uri**   <a name="transcribe-Type-InputDataConfig-TuningDataS3Uri"></a>
The Amazon S3 prefix you specify to access the plain text files that you use to tune your custom language model\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 2000\.  
Pattern: `(s3://|http(s*)://).+`   
Required: No

## See Also<a name="API_InputDataConfig_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [ AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transcribe-2017-10-26/InputDataConfig) 
+  [ AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transcribe-2017-10-26/InputDataConfig) 
+  [ AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transcribe-2017-10-26/InputDataConfig) 
+  [ AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transcribe-2017-10-26/InputDataConfig) 