# Creating a custom language model<a name="custom-language-models-create"></a>

The steps involved in creating and using a custom language model are:
+ [Step 1: Preparing your data](#prepare-training-data)
+ [ Step 2: Providing Amazon Transcribe with data permissions ](#training-data-permissions)
+ [Step 3: Creating a custom language model](#create-custom-language-model)
+ [Step 4: Transcribing with a custom language model](#clm-transcription)
+ [Step 5: Viewing and updating your custom language models](#view-update-lang)

## Step 1: Preparing your data<a name="prepare-training-data"></a>

Create a custom language model by providing training data in plain text format and by choosing a base model\. You can also provide additional tuning data, also in plain text format, for optimization\.

To prepare your text data:

1. Properly format it and save it in one or more text files\. Make sure each text file:
   + Is in the same language as the model you want to create\. For example, if you want to create a custom language model that transcribes audio in US English \(en\-US\), your text data must also be in US English \(en\-US\)\.
   + Is in plain text \(it's not a file such as a Microsoft Word document, comma\-separated value file, or PDF\)\.
   + Is encoded in UTF\-8\.
   + Doesn't contain any formatting characters, such as HTML tags\.
   + Is less than 2 GB in size if you intend to use the file as training data\. Amazon Transcribe only accepts a maximum of 2 GB of training data\.
   + Is less than 200 MB in size if you intend to use the file as tuning data\. You can provide a maximum of 200 MB of optional tuning data\.
**Note**  
Although not a requirement, it is best practice to have only one sentence per line within your text file\.

1. Upload those files to Amazon Simple Storage Service \(Amazon S3\)\. If you intend to tune the model, store your tuning data in a separate S3 bucket from the one you use for your training data\.

Use your own data processing pipelines to prepare your plain text files\. If you're extracting text from HTML, remove the HTML tags and unescape the entities\. 

The following example shows how to format sentences in a text file:

```
Ribosomes help translate RNA into protein.
RISC is essential in RNA interference.
Interferon type 1 signaling proteins help prevent viruses from replicating their RNA or DNA.
...
```

It doesn't matter how many text files you use to upload your training or tuning data\. For model training, you get the same improvements in transcription accuracy if you use one file with 100,000 words or 10 files with 10,000 words\. Prepare your text data in a way that's most convenient for you\.

**Next step**  
[ Step 2: Providing Amazon Transcribe with data permissions ](#training-data-permissions)

## Step 2: Providing Amazon Transcribe with data permissions<a name="training-data-permissions"></a>

To create a custom language model, you need to give Amazon Transcribe access to your text data\. To do this, give Amazon Transcribe the `GetObject` and `ListBucket` permissions to your Amazon Simple Storage Service \(Amazon S3\) bucket\.

**To provide data permissions**

1. Sign in to the [AWS Management Console](https://console.aws.amazon.com/iam/)\.

1. In the navigation pane, for **Access management**, choose **Roles** and choose one of the following options\.
   + Choose the name of the IAM role to use to create your custom language model and run transcription jobs\.
   + To create a new IAM role, choose **Create role**\.

     1. Under **Common use cases**, choose **EC2**\. You can select any use case, but EC2 is one of the most straightforward ones\.

     1. Choose **Next: Tags**\.

     1. Choose **Next: Review**\.

     1. Specify a name for the role under **Role name**\. Remove the text under **Role description**\.

     1. Choose **Create role**\.

     1. Choose the role you've created\.

1. Choose **Trust relationships**\.

1. Choose **Edit trust relationship**\.

1. If you're using an existing role, modify your trust policy with the following code\. If you've created a new role using this procedure, replace the trust policy text with the following code\. 

   ```
   {
       "Version": "2012-10-17",
       "Statement": [
           {
               "Effect": "Allow",
               "Principal": {
                   "Service": "transcribe.amazonaws.com"
               },
               "Action": "sts:AssumeRole"
           }
       ]
   }
   ```

1. In the navigation pane, choose **Policies**\.

1. 
   + From the policy list, choose **AmazonTranscribeFullAccess**\.

     1. From **Policy actions**, choose **Attach policy**

     1. Choose the IAM role you want to attach the policy to\.
   + Choose **Create policy**\.

     1. Choose **JSON**\.

     1. Enter the following code, which adds `GetObject` and `ListBucket` permissions:

        ```
        {
            "Version": "2012-10-17",
            "Statement": [
                {
                    "Action": [
                        "s3:GetObject"
                    ],
                    "Resource": [
                        "arn:aws:s3:::DOC-EXAMPLE-BUCKET/*"
                    ],
                    "Effect": "Allow"
                },
                {
                    "Action": [
                        "s3:ListBucket"
                    ],
                    "Resource": [
                        "arn:aws:s3:::DOC-EXAMPLE-BUCKET"
                    ],
                    "Effect": "Allow"
                }
            ]
        }
        ```

     1. Choose **Review policy**\.

     1. Specify a name for the policy\.

     1. Choose **Create policy**\.

     1. Attach the policy to the IAM role\.

Amazon Transcribe now has the necessary permissions to access the data for your custom language model\.

**Next step**  
[Step 3: Creating a custom language model](#create-custom-language-model)

## Step 3: Creating a custom language model<a name="create-custom-language-model"></a>

To create a custom language model, you must specify a base model and provide text data using an Amazon S3 prefix\.

There are two base model options:
+ `NarrowBand` \- Use this option for audio with a sample rate of less than 16,000 Hz\. This model type is typically used for telephone conversations recorded at 8,000 Hz\.
+ `WideBand` \- Use this option for audio with a sample rate greater than or equal to 16,000 Hz\.

You use prefixes in Amazon Simple Storage Service to specify training data and, optionally, tuning data\. Here are some Amazon S3 concepts to be aware of before proceeding:
+ Object – The entity stored in your S3 bucket\. In this case, the object is your training or tuning text file\.
+ Bucket – A container where you store your objects\.
+ Key – The unique identifier for an object within a bucket; for example, a file path including the file name and extension\.
+ Prefix – Any portion of the key preceding the file name\. You use prefixes to organize your data and specify objects in your S3 bucket\.

So, a key might look like this: s3://DOC\-EXAMPLE\-BUCKET/clm/creation\-date/clm\-files/my\-clm\-file\.txt\. The prefixes for this key could be any of: s3://DOC\-EXAMPLE\-BUCKET/clm/, s3://DOC\-EXAMPLE\-BUCKET/clm/creation\-date/, or s3://DOC\-EXAMPLE\-BUCKET/clm/creation\-date/clm\-files/\. For more information on prefixes, see [Organizing objects using prefixes](https://docs.aws.amazon.com/AmazonS3/latest/userguide/using-prefixes.html)\.

You specify prefixes for your text data in the following fields:
+ `S3Uri` for your training data
+ `TuningDataS3Uri` for your tuning data—this field is optional

**Note**  
S3 paths for `S3Uri` and `TuningDataS3Uri` must be the location of the folder in which your text files are located\. For example, *S3Uri=s3://*DOC\-EXAMPLE\-BUCKET*/*clm\-training\-data*/* and *TuningDataS3Uri=s3://*DOC\-EXAMPLE\-BUCKET*/*clm\-tuning\-data*/*\.

Amazon Transcribe uses any object whose key matches one of the prefixes you specify in your CLM request\. Amazon Transcribe returns an error for any file that matches a prefix and is not a plain text file\.

The following examples show how to create a CLM\.

### AWS Management Console<a name="clm-create-howto-console"></a>

1. Sign in to the [AWS Management Console](https://console.aws.amazon.com/transcribe/)\.

1. In the navigation pane, choose **Custom language model**\. This opens the **Custom language models** page where you can view existing language models or train a new model\.

1. To train a new model, select the **Train model** button\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/clm-create-console.png)

   This takes you to the **Train model** page where you can add specifications for your model, such as name, base model, training data, and IAM permissions\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/clm-train-console.png)

1. Once you have all fields completed, click the **Train model** button at the bottom of the page\.

### AWS CLI<a name="clm-create-howto-cli"></a>

This example uses the [create\-language\-model](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/transcribe/create-language-model.html) command\. For more information, see [CreateLanguageModel](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_CreateLanguageModel.html) and [LanguageModel](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_LanguageModel.html)\.

```
aws transcribe create-language-model \ 
--base-model-name NarrowBand \ 
--model-name your-language-model-name \ 
--input-data-config S3Uri=s3://DOC-EXAMPLE-BUCKET,TuningDataS3Uri=s3://DOC-EXAMPLE-BUCKET/S3-prefix/your-filename.txt,DataAccessRoleArn=arn:aws:iam::aws-account-number:role/IAM role \
--language-code en-US
```

Here's another example using the [create\-language\-model](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/transcribe/start-transcription-job.html) command, and a request body that creates your CLM\.

```
aws transcribe create-language-model \
--cli-input-json file://filepath/my-first-language-model.json
```

The file *my\-first\-language\-model\.json* contains the following request body\.

```
{
  "BaseModelName": "your-base-model-name",
  "ModelName": "your-language-model-name",
  "InputDataConfig": {
         "S3Uri": "s3://DOC-EXAMPLE-BUCKET",
         "TuningDataS3Uri"="s3://DOC-EXAMPLE-BUCKET/S3-prefix/your-filename.txt",
         "DataAccessRoleArn": "arn:aws:iam::aws-account-number:role/IAM role"
    },
  "LanguageCode": "en-US"  
}
```

### AWS SDK for Python \(Boto3\)<a name="clm-create-howto-python-batch"></a>

This example uses the AWS SDK for Python \(Boto3\) to create a CLM using the [create\_language\_model](https://boto3.amazonaws.com/v1/documentation/api/latest/reference/services/transcribe.html#TranscribeService.Client.create_language_model) method\. For more information, see [CreateLanguageModel](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_CreateLanguageModel.html) and [LanguageModel](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_LanguageModel.html)\.

For additional examples using the AWS SDKs, including feature\-specific, scenario, and cross\-service examples, refer to the [Code examples for Amazon Transcribe](service_code_examples.md) chapter\.

```
from __future__ import print_function
import time
import boto3
transcribe = boto3.client('transcribe', 'us-west-2')
model_name = 'my-first-language-model',
transcribe.create_language_model(
    LanguageCode='en-US', 
    BaseModelName = 'NarrowBand',
    ModelName = model_name,
    InputDataConfig = {
        'S3Uri':'s3://DOC-EXAMPLE-BUCKET/my-clm-training-data/',
        'TuningDataS3Uri':'s3://DOC-EXAMPLE-BUCKET/my-clm-tuning-data/',
        'DataAccessRoleArn':'arn:aws:iam::111122223333:role/ExampleRole'
         }
)
while True:
    status = transcribe.get_language_model(ModelName=model_name)
    if status['LanguageModel']['ModelStatus'] in ['COMPLETED', 'FAILED']:
        break
    print("Not ready yet...")
    time.sleep(5)
print(status)
```

**Next step**  
[Step 4: Transcribing with a custom language model](#clm-transcription)

## Step 4: Transcribing with a custom language model<a name="clm-transcription"></a>

You can use a CLM to transcribe your audio using either batch transcription jobs or real\-time streams\.

### Using a custom language model with a batch transcription job<a name="clm-batch-transcription"></a>

You can transcribe with a CLM for batch transcription jobs using the **AWS Management Console**, **AWS CLI**, or **AWS SDK**; see the following instructions\.

#### AWS Management Console<a name="clm-use-howto-console"></a>

1. Sign in to the [AWS Management Console](https://console.aws.amazon.com/transcribe/)\.

1. In the navigation pane, choose **Transcription jobs**, then select the **Create job** button \(top right\)\. This opens the **Specify job details** page\.

1. In the **Job settings** panel under **Model type**, select the **Custom language model** box\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/clm-console.png)

   You must also select an input language from the drop\-down menu\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/clm-console-language.png)

1. Under **Custom model selection**, either select an existing custom language model from the drop\-down menu or click on 'create a new one'\.

   Add the S3 location of your input file in the **Input data** panel\.

1. Click the **Next** button for additional configuration options\. Click the **Create job** button to run your transcription job\.

#### AWS CLI<a name="clm-use-howto-cli"></a>

This example uses the [start\-transcription\-job](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/transcribe/start-transcription-job.html) command and `LanguageModelName` parameter\. For more information, see [StartTranscriptionJob](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_StartTranscriptionJob.html) and [ModelSettings](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_ModelSettings.html)\.

```
aws transcribe start-transcription-job \
--region us-west-2 \
--transcription-job-name my-first-transcription-job \
--media MediaFileUri=s3://DOC-EXAMPLE-BUCKET/my-media-file.flac \
--output-bucket-name DOC-EXAMPLE-BUCKET \
--language-code en-US \
--model-settings LanguageModelName=my-first-language-model
```

Here's another example using the [start\-transcription\-job](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/transcribe/start-transcription-job.html) command, and a request body that uses your CLM with that job\.

```
aws transcribe start-transcription-job \
--region us-west-2 \
--cli-input-json file://filepath/my-first-language-model-job.json
```

The file *my\-first\-language\-model\-job\.json* contains the following request body\.

```
{
  "TranscriptionJobName": "my-first-transcription-job",
  "Media": {
        "MediaFileUri": "s3://DOC-EXAMPLE-BUCKET/my-media-file.flac"
    },
  "OutputBucketName": "DOC-EXAMPLE-BUCKET",
  "LanguageCode": "en-US",
  "ModelSettings": {
        "LanguageModelName": "my-first-language-model"
    }
}
```

#### AWS SDK for Python \(Boto3\)<a name="clm-use-howto-python-batch"></a>

This example uses the AWS SDK for Python \(Boto3\) to transcribe a file with the `LanguageModelName` argument for the [start\_transcription\_job](https://boto3.amazonaws.com/v1/documentation/api/latest/reference/services/transcribe.html#TranscribeService.Client.start_transcription_job) method\. For more information, see [StartTranscriptionJob](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_StartTranscriptionJob.html) and [ModelSettings](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_ModelSettings.html)\.

For additional examples using the AWS SDKs, including feature\-specific, scenario, and cross\-service examples, refer to the [Code examples for Amazon Transcribe](service_code_examples.md) chapter\.

```
from __future__ import print_function
import time
import boto3
transcribe = boto3.client('transcribe', 'us-west-2')
job_name = "my-first-transcription-job"
job_uri = "s3://DOC-EXAMPLE-BUCKET/my-media-file.flac"
transcribe.start_transcription_job(
    TranscriptionJobName=job_name,
    Media={
        'MediaFileUri': job_uri
    },
    MediaFormat='flac',
    LanguageCode='en-US', 
    ModelSettings={
        'LanguageModelName': 'my-first-language-model'
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

### Using a custom language model with a real\-time stream<a name="clm-streaming-transcription"></a>

You can use a CLM to transcribe a real\-time stream with either a WebSocket request or the [StartStreamTranscription](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_streaming_StartStreamTranscription.html) operation\.

**Note**  
Only CLMs created after streaming support are available for use with streaming transcriptions\. If your CLM was created prior to streaming support, you must re\-create it to use it with a real\-time stream\. To view supported languages for streaming CLMs, see [Supported languages and language\-specific features](supported-languages.md#table-language-matrix)\.

#### WebSocket<a name="clm-use-howto-websocket"></a>

This example creates a pre\-signed URL that uses a custom language model in a WebSocket stream\. Line breaks have been added for readability\. For more information on using WebSocket streams with Amazon Transcribe, see [Setting up a WebSocket stream](streaming-websocket.md)\. For more detail on parameters, see [StartStreamTranscription](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_streaming_StartStreamTranscription.html)\.

```
GET wss://transcribestreaming.us-west-2.amazonaws.com:8443/stream-transcription-websocket?
&X-Amz-Algorithm=AWS4-HMAC-SHA256
&X-Amz-Credential=AKIAIOSFODNN7EXAMPLE%2F20220208%2Fus-west-2%2Ftranscribe%2Faws4_request
&X-Amz-Date=20220208T235959Z
&X-Amz-Expires=250
&X-Amz-Security-Token=security-token
&X-Amz-Signature=string
&X-Amz-SignedHeaders=content-type%3Bhost%3Bx-amz-date
&language-code=en-US
&media-encoding=flac
&sample-rate=16000    
&language-model-name=my-first-language-model
```

Parameter definitions can be found in the [API Reference](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_Reference.html); parameters common to all AWS API operations are listed in the [Common Parameters](https://docs.aws.amazon.com/transcribe/latest/APIReference/CommonParameters.html) section\.

#### HTTP/2<a name="clm-use-howto-http2"></a>

This example creates an HTTP/2 request with a custom language model\. For more information on using HTTP/2 streaming with Amazon Transcribe, see [Setting up an HTTP/2 stream](streaming-http2.md)\. For more detail on parameters and headers specific to Amazon Transcribe, see [StartStreamTranscription](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_streaming_StartStreamTranscription.html)\.

```
POST /stream-transcription HTTP/2
host: transcribestreaming.us-west-2.amazonaws.com
X-Amz-Target: com.amazonaws.transcribe.Transcribe.StartStreamTranscription
Content-Type: application/vnd.amazon.eventstream
X-Amz-Content-Sha256: string
X-Amz-Date: 20220208T235959Z
Authorization: AWS4-HMAC-SHA256 Credential=access-key/20220208/us-west-2/transcribe/aws4_request, SignedHeaders=content-type;host;x-amz-content-sha256;x-amz-date;x-amz-target;x-amz-security-token, Signature=string
x-amzn-transcribe-language-code: en-US
x-amzn-transcribe-media-encoding: flac
x-amzn-transcribe-sample-rate: 16000
x-amzn-language-model-name: my-first-language-model    
transfer-encoding: chunked
```

Parameter definitions can be found in the [API Reference](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_Reference.html); parameters common to all AWS API operations are listed in the [Common Parameters](https://docs.aws.amazon.com/transcribe/latest/APIReference/CommonParameters.html) section\.

**Next step**  
[Step 5: Viewing and updating your custom language models](#view-update-lang)

## Step 5: Viewing and updating your custom language models<a name="view-update-lang"></a>

The speech recognition capabilities of Amazon Transcribe are constantly improving\. Specifically, Amazon Transcribe continually updates the base models used in custom language models\.

To see if you're running the latest base model in your custom language model:

1. Use the [DescribeLanguageModel](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_DescribeLanguageModel.html) API and check the `UpgradeAvailability` field\.

1. If `UpgradeAvailability` is `true`, you're not running the latest version of the base model in your custom language model\.

To use the latest base model in a custom language model, you must create a new custom language model\. That custom language model will have the updated base model\.