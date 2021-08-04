# Step 3: Creating a custom language model<a name="create-custom-language-model"></a>

To create a custom language model, you must provide your text data using an Amazon S3 prefix and specify a *base model*\. There are two base models:
+ `NarrowBand` \- For audio with a sample rate of less than 16 kHz\. You typically use this type of model for telephone conversations recorded at 8 kHz\.
+ `WideBand` \- For audio with a sample rate of 16 kHz or greater\. This includes audio from media sources\.

You can create a custom language model with the base model and the training data using console, the [CreateLanguageModel](API_CreateLanguageModel.md) operation, the AWS Command Line Interface \(AWS CLI\)\.

## Using prefixes in Amazon Simple Storage Service to retrieve your data<a name="prefix-get-data"></a>

To create a custom language model, you use prefixes in Amazon Simple Storage Service to specify the training and the optional tuning data\. To understand how to use prefixes, you need to be familiar with the following Amazon S3 concepts:
+ Bucket – A container to store your objects\.
+ Object – The entity stored in the S3 bucket\. In this case, it's your training or tuning text files\.
+ Key – The unique identifier for an object within a bucket\. 
+ Prefix – Any portion of the key up to the final delimiter\. You use prefixes to organize your data and specify objects in the S3 bucket\.

You store an object, your text file, in a bucket with a key that uniquely identifies the file\.

For example, the key `s3://DOC-EXAMPLE-BUCKET1/myfiles/2020/may/file.txt` uniquely identifies a text file in an S3 bucket\.

The prefix can be any part of the key that comes before its final delimiter\.

For example, the key `myfiles/2020/may/file.txt` has the following prefixes:
+ s3://*DOC\-EXAMPLE\-BUCKET1*/myfiles/2020/may/
+ s3://*DOC\-EXAMPLE\-BUCKET1*/myfiles/2020/
+ s3://*DOC\-EXAMPLE\-BUCKET1*/myfiles/

You can use any of the preceding prefixes to access `file.txt`\. For more information on prefixes, see [Organizing objects using prefixes](https://docs.aws.amazon.com/AmazonS3/latest/userguide/using-prefixes.html)\. 

When you use the [CreateLanguageModel](API_CreateLanguageModel.md) operation, you specify prefixes for your text data in the following fields: 
+ `S3Uri` for the training data
+ Optional: `TuningDataS3Uri` for the tuning data

Amazon Transcribe uses any object whose key matches one of the prefixes that you specify in a custom language model\. Amazon Transcribe returns an error for any file that matches a prefix and is not a plain text file\.

You create a custom language model by providing prefixes to train a base model in either the console or the API\.

## Creating a custom language model \(console\)<a name="create-console"></a>

**To create a custom language model \(Console\)**

To use the console to create a custom language model with the console, you must have your training data stored in an Amazon S3 bucket\.

1. Sign in to AWS Management Console and open the Amazon Transcribe console at [Amazon Transcribe console](https://console.aws.amazon.com/transcribe/)\.

1. In the navigation pane, choose **Custom language models**\.

1. Choose **Train model**\.

1. For **Name**, enter a name for your custom language model that is unique within your AWS account\.

1. For **Language**, choose the language of your custom language model\.

1. For **Base model**, choose **Narrow band** or **Wide band**, as appropriate for the sample rate of the audio that you want to transcribe\.

1. Under **Training data**, for **Training data location on S3**, specify the S3 prefix that accesses only your training data\.

1. Optional: Under **Tuning data \- *optional***, for **Tuning data location on S3** , specify the S3 prefix for the bucket where your tuning data is stored\.

1. For **Access permissions**, use or create an IAM data access role that provides Amazon Transcribe with the `ListBucket` and `GetObject` permissions\.

1. Choose **Train model**\.

## Creating a custom language model \(API\)<a name="create-api"></a>

 To create a custom language model use the [CreateLanguageModel](API_CreateLanguageModel.md) operation\. 

**To create a custom language model \(API\)**
+ In an [CreateLanguageModel](API_CreateLanguageModel.md) request, specify the following:
  + `BaseModelName` \- The type of base model that you want to use for your custom language model
  + `InputDataConfig` \- Specify the Amazon S3 object location and the IAM data access role for your training data:

    `DataAccessRoleARN` \- The Amazon Resource Name \(ARN\) that identifies the permissions to your Amazon S3 bucket\.

    `S3Uri` \- The prefix of the keys to your training data\.

    \(Optional\) `TuningDataS3URI` \- The prefix of the keys to your tuning data\.
  + `LanguageCode` \- The language code for the language of your training data\.
  + `ModelName` \- The name of your custom language model\.

The following is an example request using the AWS SDK for Python \(Boto3\)\.

```
from __future__ import print_function
import time
import boto3
transcribe = boto3.client('transcribe')
model_name = "example-language-model"
transcribe.create_language_model(
    LanguageCode = 'language-code',
    BaseModelName = 'base-model-name',
    ModelName = model_name,
    InputDataConfig = {'S3Uri': 's3://DOC-EXAMPLE-BUCKET/clm-training/',
        'TuningDataS3Uri': 's3://DOC-EXAMPLE-BUCKET/clm-tuning',
        'DataAccessRoleArn':'arn:aws:iam::AWS-account-number:role/IAM role'
         }
         )
```

## Creating a custom language model \(AWS CLI\)<a name="create-cli"></a>

**To create a custom language model \(AWS CLI\)**
+ Run the following code\.

  ```
  aws transcribe create-language-model \ 
  --language-code language-code \ 
  --base-model-name base-model-name \ 
  --model-name example-model-name \ 
  --input-data-config S3Uri="s3://example-bucket",DataAccessRoleArn="arn:aws:iam::aws-account-number:role/IAM role"
  ```

**Next step**  
[Step 4: Transcribing with a custom language model](clm-transcription.md)