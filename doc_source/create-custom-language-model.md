# Step 3: Creating a custom language model<a name="create-custom-language-model"></a>

To create a custom language model, you must specify a base model and provide text data using an Amazon S3 prefix\.

There are two base model options:
+ `NarrowBand` \- Use this option for audio with a sample rate of less than 16,000 Hz\. This model type is typically used for telephone conversations recorded at 8,000 Hz\.
+ `WideBand` \- Use this option for audio with a sample rate greater than or equal to 16,000 Hz\.

You use prefixes in Amazon Simple Storage Service to specify training data and, optionally, tuning data\. Here are some Amazon S3 concepts to be aware of before proceeding:
+ Object – The entity stored in your S3 bucket\. In this case, the object is your training or tuning text file\.
+ Bucket – A container where you store your objects\.
+ Key – The unique identifier for an object within a bucket; for example, a file path including the file name and extension\.
+ Prefix – Any portion of the key preceeding the filename\. You use prefixes to organize your data and specify objects in your S3 bucket\.

So, a key might look like this: s3://your\-S3\-bucket/clm/creation\-date/clm\-files/your\-filename\.txt\. The prefixes for this key could be any of: s3://your\-S3\-bucket/clm/, s3://your\-S3\-bucket/clm/creation\-date/, or s3://your\-S3\-bucket/clm/creation\-date/clm\-files/\. For more information on prefixes, see [Organizing objects using prefixes](https://docs.aws.amazon.com/AmazonS3/latest/userguide/using-prefixes.html)\.

You specify prefixes for your text data in the following fields:
+ `S3Uri` for your training data
+ `TuningDataS3Uri` for your tuning data—this field is optional

Amazon Transcribe uses any object whose key matches one of the prefixes you specify in your CLM request\. Amazon Transcribe returns an error for any file that matches a prefix and is not a plain text file\.

The following examples show how to create a CLM\.

## Console<a name="clm-create-howto-console"></a>

1. Sign in to the [Amazon Transcribe console](https://console.aws.amazon.com/transcribe/)\.

1. In the navigation pane, choose **Custom language model**\. This opens the **Custom language models** page where you can view existing language models or train a new model\.

1. To train a new model, select the **Train model** button\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/clm-create-console.png)

   This takes you to the **Train model** page where you can add specifications for your model, such as name, base model, training data, and IAM permissions\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/clm-train-console.png)

1. Once you have all fields completed, click the **Train model** button at the bottom of the page\.

## AWS SDK for Python \(Boto3\)<a name="clm-create-howto-sdk"></a>

The following example uses the AWS SDK for Python \(Boto3\) to create a CLM using the [create\_language\_model](https://boto3.amazonaws.com/v1/documentation/api/latest/reference/services/transcribe.html#TranscribeService.Client.create_language_model) method:

```
from __future__ import print_function
import time
import boto3
transcribe = boto3.client('transcribe')
model_name = 'my-model-name',
transcribe.create_language_model(
    LanguageCode='en-US', 
    BaseModelName = 'NarrowBand',
    ModelName = model_name,
    InputDataConfig = {
        'S3Uri': 's3://your-S3-bucket/clm-training-data',
        'TuningDataS3Uri': 's3://your-S3-bucket/clm-tuning-data',
        'DataAccessRoleArn':'arn:aws:iam::AWS-account-number:role/IAM-role'
         }
)
while True:
    status = transcribe.get_transcription_job(TranscriptionJobName=job_name)
    if status['TranscriptionJob']['TranscriptionJobStatus'] in ['COMPLETED', 'FAILED']:
        break
    print("Not ready yet...")
    time.sleep(5)
print(status)
```

## AWS CLI<a name="clm-create-howto-cli"></a>

This example uses the [create\-language\-model](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/transcribe/create-language-model.html) command\.

```
aws transcribe create-language-model \ 
--language-code en-US \ 
--base-model-name NarrowBand \ 
--model-name my-language-model-name \ 
--input-data-config S3Uri=s3://your-S3-bucket,TuningDataS3Uri=s3://your-S3-bucket/S3-prefix/your-filename.file-extension,DataAccessRoleArn=arn:aws:iam::aws-account-number:role/IAM role
```

Here's another example using the [create\-language\-model](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/transcribe/start-transcription-job.html) command, and a request body that creates your CLM\.

```
aws transcribe create-language-model \
--cli-input-json file://example-start-command.json
```

The file *example\-start\-command\.json* contains the following request body\.

```
{
  "LanguageCode": "en-US",
  "BaseModelName": "my-base-model-name",
  "ModelName": "my-language-model-name",
  "InputDataConfig": {
         "S3Uri": "s3://your-S3-bucket",
         "TuningDataS3Uri"="s3://your-S3-bucket/S3-prefix/your-filename.file-extension",
         "DataAccessRoleArn": "arn:aws:iam::aws-account-number:role/IAM role"
    }
}
```

**Next step**  
[Step 4: Transcribing with a custom language model](clm-transcription.md)