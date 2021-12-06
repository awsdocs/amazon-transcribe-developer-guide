# Redacting PII in your batch job<a name="pii-redaction-batch"></a>

When redacting personally identifiable information \(PII\) from a transcript during a batch transcription job, Amazon Transcribe replaces each identified instance of PII with `[PII]` in your transcript\. For an output sample, see [Example redacted batch output](pii-redaction-output.md#pii-redaction-output-batch)\.

Both redacted and unredacted transcripts are stored in the same output S3 bucket\. Amazon Transcribe stores them in either a bucket you specify or in the default S3 bucket managed by the service\.

You can start a batch transcription job using the Amazon Transcribe console, AWS CLI, or AWS SDK\.

## Console<a name="redaction-howto-console-batch"></a>

1. Sign in to the [Amazon Transcribe console](https://console.aws.amazon.com/transcribe/)\.

1. In the navigation pane, choose **Transcription jobs**, then select the **Create job** button \(top right\)\. This will open the **Specify job details** page\.

1. After filling in your desired fields on the **Specify job details** page, click the **Next** button to go to the **Configure job \- *optional*** page\. Here you'll find the **Content removal** panel with the options of **Automatic content redaction** and **Vocabulary filtering**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/content-redact.png)

1. Once you select **Automatic content redaction**, which redacts all PII, you have the option to check the **Include unredacted transcript in job output** box\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/content-redact-select.png)

1. Click the **Create job** button to run your transcription job\.

## AWS CLI<a name="redaction-howto-cli"></a>

This example uses the [start\-transcription\-job](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/transcribe/start-transcription-job.html) command and `content-redaction` parameter\. For more information, see [ StartTranscriptionJob ](API_StartTranscriptionJob.md) and [ ContentRedaction ](API_ContentRedaction.md)\.

```
aws transcribe start-transcription-job \
--transcription-job-name your-job-name \
--media MediaFileUri=s3://your-S3-bucket/S3-prefix/your-filename.file-extension \
--language-code en-US \
--content-redaction  RedactionType=PII,RedactionOutput=redacted
```

Here's another example using the [start\-transcription\-job](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/transcribe/start-transcription-job.html) method, and the request body redacts PII for that job\.

```
aws transcribe start-transcription-job \
--cli-input-json file://example-start-command.json
```

The file *example\-start\-command\.json* contains the following request body\.

```
{
  "TranscriptionJobName": "your-job-name",
  "LanguageCode": "en-US",
  "Media": {
      "MediaFileUri":  "s3://your-S3-bucket/S3-prefix/your-filename.file-extension"
  },
  "ContentRedaction": {
      "RedactionOutput":"redacted",
      "RedactionType":"PII"
  }
}
```

## AWS SDK for Python \(Boto3\)<a name="redaction-howto-sdk"></a>

This example uses the AWS SDK for Python \(Boto3\) to redact content using the `ContentRedaction` argument for the [start\_transcription\_job](https://boto3.amazonaws.com/v1/documentation/api/latest/reference/services/transcribe.html#TranscribeService.Client.start_transcription_job) method\. For more information, see [ StartTranscriptionJob ](API_StartTranscriptionJob.md) and [ ContentRedaction ](API_ContentRedaction.md)\.

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
    LanguageCode='en-US', 
    ContentRedaction = { 'RedactionOutput':'redacted',
      'RedactionType':'PII'
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