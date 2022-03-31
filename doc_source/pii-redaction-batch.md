# Redacting PII in your batch job<a name="pii-redaction-batch"></a>

When redacting personally identifiable information \(PII\) from a transcript during a batch transcription job, Amazon Transcribe replaces each identified instance of PII with `[PII]` in the main text body of your transcript\. You can also view the type of PII that was redacted in the word\-for\-word portion of the transcription output\. For an output sample, see [Example redacted batch output](pii-redaction-output.md#pii-redaction-output-batch)\.

Both redacted and unredacted transcripts are stored in the same output S3 bucket\. Amazon Transcribe stores them in either a bucket you specify or in the default S3 bucket managed by the service\.

You can start a batch transcription job using the AWS Management Console, AWS CLI, or AWS SDK\.

## AWS Management Console<a name="redaction-howto-console-batch"></a>

1. Sign in to the [AWS Management Console](https://console.aws.amazon.com/transcribe/)\.

1. In the navigation pane, choose **Transcription jobs**, then select the **Create job** button \(top right\)\. This will open the **Specify job details** page\.

1. After filling in your desired fields on the **Specify job details** page, click the **Next** button to go to the **Configure job \- *optional*** page\. Here you'll find the **Content removal** panel with the **PII redaction** toggle\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/content-redact.png)

1. Once you select **PII redaction**, you have the option to select all PII types you want to redact\. You can also choose to have an unredacted transcript if you select **Include unredacted transcript in job output** box\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/content-redact-select.png)

1. Click the **Create job** button to run your transcription job\.

## AWS CLI<a name="redaction-howto-cli"></a>

This example uses the [start\-transcription\-job](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/transcribe/start-transcription-job.html) command and `content-redaction` parameter\. For more information, see [StartTranscriptionJob](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_StartTranscriptionJob.html) and [ContentRedaction](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_ContentRedaction.html)\.

```
aws transcribe start-transcription-job \
--region us-west-2 \
--transcription-job-name my-first-transcription-job \
--media MediaFileUri=s3://DOC-EXAMPLE-BUCKET/my-media-file.flac \
--output-bucket-name DOC-EXAMPLE-BUCKET \
--language-code en-US \
--content-redaction  RedactionType=PII,RedactionOutput=redacted,PiiEntityTypes=NAME,ADDRESS,BANK_ACCOUNT_NUMBER
```

Here's another example using the [start\-transcription\-job](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/transcribe/start-transcription-job.html) method, and the request body redacts PII for that job\.

```
aws transcribe start-transcription-job \
--cli-input-json file://filepath/my-first-redaction-job.json
```

The file *my\-first\-redaction\-job\.json* contains the following request body\.

```
{
  "TranscriptionJobName": "my-first-transcription-job",
  "Media": {
      "MediaFileUri":  "s3://DOC-EXAMPLE-BUCKET/my-media-file.flac"
  },
  "OutputBucketName": "DOC-EXAMPLE-BUCKET",
  "LanguageCode": "en-US",
  "ContentRedaction": {
      "RedactionOutput":"redacted",
      "RedactionType":"PII"
      "PiiEntityTypes": [
           "NAME",
           "ADDRESS",
           "BANK_ACCOUNT_NUMBER"	
      ]
  }
}
```

## AWS SDK for Python \(Boto3\)<a name="redaction-howto-python-batch"></a>

This example uses the AWS SDK for Python \(Boto3\) to redact content using the `ContentRedaction` argument for the [start\_transcription\_job](https://boto3.amazonaws.com/v1/documentation/api/latest/reference/services/transcribe.html#TranscribeService.Client.start_transcription_job) method\. For more information, see [StartTranscriptionJob](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_StartTranscriptionJob.html) and [ContentRedaction](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_ContentRedaction.html)\.

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
    ContentRedaction={ 
        'RedactionOutput':'redacted',
        'RedactionType':'PII', 
        'PiiEntityTypes': [
            'NAME','ADDRESS','BANK_ACCOUNT_NUMBER'
        ]
)

while True:
    status = transcribe.get_transcription_job(TranscriptionJobName=job_name)
    if status['TranscriptionJob']['TranscriptionJobStatus'] in ['COMPLETED', 'FAILED']:
        break
    print("Not ready yet...")
    time.sleep(5)
print(status)
```

**Note**  
PII redaction for batch jobs is only supported in these AWS Regions: Asia Pacific \(Hong Kong\), Asia Pacific \(Mumbai\), Asia Pacific \(Seoul\), Asia Pacific \(Singapore\), Asia Pacific \(Sydney\), Asia Pacific \(Tokyo\), AWS GovCloud \(US\-West\), Canada \(Central\), EU \(Frankfurt\), EU \(Ireland\), EU \(London\), EU \(Paris\), Middle East \(Bahrain\), South America \(Sao Paulo\), US East \(N\. Virginia\), US East \(Ohio\), US West \(Oregon\), and US West \(N\. California\)\.