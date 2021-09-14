# Redacting or identifying PII in an audio file<a name="pii-redaction-batch"></a>

Use a batch transcription job to transcribe audio files and redact the personally identifiable information \(PII\) within them\. When you activate PII Redaction, Amazon Transcribe redacts the PII that it identified in the transcription results\. For information about PII that Amazon Transcribe can identify, see the list of [](pii-redaction.md#table-redaction-list)\.

**Note**  
PII redaction for batch jobs is only supported in these AWS regions: Asia Pacific \(Hong Kong\), Asia Pacific \(Mumbai\), Asia Pacific \(Seoul\), Asia Pacific \(Singapore\), Asia Pacific \(Sydney\), Asia Pacific \(Tokyo\), AWS GovCloud \(US\-West\), Canada \(Central\), EU \(Frankfurt\), EU \(Ireland\), EU \(London\), EU \(Paris\), Middle East \(Bahrain\), South America \(Sao Paulo\), US East \(N\. Virginia\), US East \(Ohio\), US West \(Oregon\), and US West \(N\. California\)\.

 Amazon Transcribe replaces each identified instance of PII with a `[PII]` tag in the transcript\. You can use this feature to protect privacy and comply with local laws and regulations\. PII redaction gives you the ability to easily review and share transcripts to improve the customer service experience, coach agents, and discover new business opportunities while protecting sensitive personal information\. You can use this feature for source audio in US English \(en\-US\)\.

When redaction is enabled, Amazon Transcribe can generate the following files, depending on which options you select:
+ A redacted text file\. A redacted text file displays `[PII]` in place of the redacted text; see below for example excerpts from a redacted conversation\.
+ An unredacted \(original\) text file\. This file is only generated if you choose to get both the redacted and the original transcripts\.

**Note**  
The original unredacted file is the only place where the complete conversation is stored\. If you delete it, there is no record of the unredacted sensitive data\.

Both redacted and unredacted transcripts are stored in the same output S3 bucket\. Amazon Transcribe stores them in either a bucket you specify or in the default S3 bucket managed by the service\.

A redacted transcript replaces sensitive PII with a `[PII]` tag, as shown in the first truncated JSON output on this page\. Because Amazon Transcribe has redacted this transcript, the `isRedacted` field of this JSON output is `true`\. Each JSON output of a transcription job has a `results` section that contains the transcription results\. Every word, number, punctuation mark, or redaction has a confidence value\.

Transcription jobs using automatic content redaction generate two types of `confidence` values\. The Automatic Speech Recognition \(ASR\) confidence indicates the items that have the `type` of `pronunciation` or `punctuation` is a specific utterance\. In the transcript output below, the word `Good` has a `confidence` of `1.0`\. This confidence value indicates that Amazon Transcribe is 100 percent confident that the word uttered in this transcript is `Good`\. The `confidence` value for a `[PII]` tag is the confidence that the speech it flagged for redaction is truly PII\. In the following transcript output, the `confidence` of `0.9999` indicates that Amazon Transcribe is 99\.99 percent confident that the entity it redacted in the transcript is PII\.

You can start a batch transcription job using either the [ StartTranscriptionJob ](API_StartTranscriptionJob.md) operation or the Amazon Transcribe console\.

## Console<a name="redaction-howto-console"></a>

1. Sign in to the [Amazon Transcribe console](https://console.aws.amazon.com/transcribe/)\.

1. In the navigation pane, choose **Transcription jobs**, then select the **Create job** button \(top right\)\. This will open the **Specify job details** page\.

1. After filling in your desired fields on the **Specify job details** page, click the **Next** button to go to the **Configure job \- *optional*** page\. Here you'll find the **Content removal** panel with the options of **Automatic content redaction** and **Vocabulary filtering**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/content-redact.png)

1. Once you select **Automatic content redaction**, which redacts all PII, you have the option to check the **Include unredacted transcript in job output** box\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/content-redact-select.png)

1. Click the **Create job** button to run your transcription job\.

## AWS CLI<a name="redaction-howto-cli"></a>

This example uses the [start\-transcription\-job](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/transcribe/start-transcription-job.html) command and `content-redaction` parameter\.

```
aws transcribe start-transcription-job \
--transcription-job-name my-job-name \
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
  "TranscriptionJobName": "my-job-name",
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

The following example uses the AWS SDK for Python \(Boto3\) to redact content using the `ContentRedaction` argument for the [start\_transcription\_job](https://boto3.amazonaws.com/v1/documentation/api/latest/reference/services/transcribe.html#TranscribeService.Client.start_transcription_job) method:

```
from __future__ import print_function
import time
import boto3
transcribe = boto3.client('transcribe')
job_name = "my-job-name"
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