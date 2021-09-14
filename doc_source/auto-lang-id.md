# Identifying the dominant language in your media files<a name="auto-lang-id"></a>

Amazon Transcribe is able to automatically identify the predominant language in a media file without you having to specify a language code\. Automatic language identification can be used for any batch transcription job, and all supported languages can be identified\. Streaming transcriptions are not supported\. For a complete list of languages available with Amazon Transcribe, see [Supported languages and language\-specific features](how-it-works.md#table-language-matrix)\.

To identify the language with greater accuracy, you can specify a list of languages you think are present in your collection of media files\. From that list, Amazon Transcribe chooses the language with the greatest confidence score to transcribe your audio\. A score with a larger value indicates that Amazon Transcribe is more confident it identified the language correctly\. For best results, if you are certain of the language spoken in each of the audio files, specify a language code\.

**Note**  
Media files are transcribed in a single language, even if they contain speech in two or more languages\. Amazon Transcribe transcribes the audio according to the predominant language identified in the file\.

Because some Amazon Transcribe features require you to specify a language code, automatic language identification is not supported with all features\. You cannot use automatic language identification if the following features are enabled:
+ Custom language models
+ Custom vocabularies
+ Vocabulary filtering
+ Content redaction

To increase the chance of identifying the language successfully, media files should have at least 30 seconds of speech\.

You can use automatic language identification in a batch transcription job using the **Amazon Transcribe Console**, **AWS CLI**, or **AWS SDK**; see below for instructions:

## Console<a name="autolang-howto-console"></a>

1. Sign in to the [Amazon Transcribe console](https://console.aws.amazon.com/transcribe/)\.

1. In the navigation pane, choose **Transcription jobs**, then select the **Create job** button \(top right\)\. This opens the **Specify job details** page\.

1. In the **Job settings** panel, find the **Language settings**, section and select **Automatic language identification**\. You also have the option to select multiple languages \(from the *Select languages* drop\-down box\) if you have an idea of which language your file contains\. This option can improve accuracy, but is not required\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/auto-lang-id.png)

1. Fill in any other fields you wish to include on the **Specify job details** page, then click the **Next** button\. This takes you to the **Configure job \- *optional* page\.**  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/auto-lang-id-configure.png)

1. Click the **Create job** button to run your transcription job\. 

## AWS SDK for Python \(Boto3\)<a name="autolang-howto-sdk"></a>

The following example uses the AWS SDK for Python \(Boto3\) to add a tag by using the `IdentifyLanguage` argument for the [start\_transcription\_job](https://boto3.amazonaws.com/v1/documentation/api/latest/reference/services/transcribe.html#TranscribeService.Client.start_transcription_job) method:

```
from __future__ import print_function
import time
import boto3
transcribe = boto3.client('transcribe')
job_name = "your-job-name"
job_uri = "s3://your-S3-bucket/S3-prefix/your-filename.file-extension"
transcribe.start_transcription_job(
    TranscriptionJobName=job_name,
    Media={'MediaFileUri': job_uri},
    MediaFormat='wav',
    IdentifyLanguage='True' 
)
while True:
    status = transcribe.get_transcription_job(TranscriptionJobName=job_name)
    if status['TranscriptionJob']['TranscriptionJobStatus'] in ['COMPLETED', 'FAILED']:
        break
    print("Not ready yet...")
    time.sleep(5)
print(status)
```

## AWS CLI<a name="autolang-howto-cli"></a>

This example uses the [start\-transcription\-job](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/transcribe/start-transcription-job.html) command and `IdentifyLanguage` parameter\.

```
aws transcribe start-transcription-job \
--transcription-job-name your-job-name \
--media  MediaFileUri=s3://your-S3-bucket/S3-prefix/your-filename.file-extension \
--identify-language
```

Here's another example using the [start\-transcription\-job](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/transcribe/start-transcription-job.html) command, and a request body that identifies the language\.

```
aws transcribe start-transcription-job \
--cli-input-json file://filepath/example-start-command.json
```

The file *example\-start\-command\.json* contains the following request body\.

```
{
  "TranscriptionJobName": "your-job-name",  
  "Media": {
        "MediaFileUri": "s3://your-S3-bucket/S3-prefix/your-filename.file-extension"
    },
  "IdentifyLanguage": "true"
}
```

## Getting notifications using Automatic language identification<a name="lang-id-cloudwatch"></a>

Amazon Transcribe can notify you if it successfully identifies the language of your media file before the transcription job finishes\. To receive a notification, enable a rule for an Amazon CloudWatch event\. CloudWatch is a service you can use to monitor your AWS resources and applications in real time\. For more information see [What Is Amazon CloudWatch](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/WhatIsCloudWatch.html)\.

For more information about the CloudWatch events that show whether the language has been identified successfully in your audio, see [Language identification events](cloud-watch-events.md#lang-id-event)\. For general information about CloudWatch events in Amazon Transcribe, see [Using Amazon EventBridge with Amazon Transcribe](cloud-watch-events.md)\. 