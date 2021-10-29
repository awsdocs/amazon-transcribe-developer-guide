# Creating video subtitles<a name="subtitles"></a>

Amazon Transcribe supports WebVTT \(\*\.vtt\) and SubRip \(\*\.srt\) output for use as video subtitles\. You can select one or both file types when setting up your batch video transcription job\. When using the subtitle feature, your selected subtitle file\(s\) and a regular transcript file \(containing additional information\) are produced\. Subtitle and transcription files are output to the same destination\.

Subtitles are displayed at the same time text is spoken, and remain visible until there is a natural pause or the speaker finishes talking\.

Features supported with subtitles:
+ Content redaction: Any redacted content is reflected as `PII` in both your subtitle and regular transcript files\. The audio is not altered\.
+ Vocabulary filters: Subtitle files are generated from the transcription file, so any words you filter in your standard transcription output are also filtered in your subtitles\. Filtered content is displayed as whitespace or `***` in your transcript and subtitle files\. The audio is not altered\.
+ If there are multiple speakers in a given subtitle segment, dashes are used to distinguish each speaker\. This applies to both WebVTT and SubRip formats; for example:
  + \-\- Text spoken by Person 1
  + \-\- Text spoken by Person 2

## Adding subtitles to your Amazon Transcribe video files<a name="subtitles-how-to"></a>

You can add subtitles using the **console**, **SDK**, or **AWS CLI**; see below for instructions:

### Console<a name="subtitles-howto-console"></a>

1. Sign in to the [Amazon Transcribe console](https://console.aws.amazon.com/transcribe/)\.

1. In the navigation pane, choose **Transcription jobs**, then select the **Create job** button \(top right\)\. This will open the **Specify job details** page\. Subtitle options are located in the **Output data** panel\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/subtitles.png)

1. Fill in any other fields you wish to include on the **Specify job details** page, then click the **Next** button\. This takes you to the **Configure job \- *optional* page\.**

1. Click the **Create job** button to run your transcription job\. 

### AWS CLI<a name="subtitles-howto-cli"></a>

This example uses the [start\-transcription\-job](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/transcribe/start-transcription-job.html) command and `Subtitles` parameter\.

```
aws transcribe start-transcription-job \
--transcription-job-name job-name \
--media MediaFileUri=s3://your-S3-bucket/S3-prefix/your-filename.file-extension \
--language-code en-US \
--subtitles Formats=vtt
```

Here's another example using the [start\-transcription\-job](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/transcribe/start-transcription-job.html) command, and a request body that adds subtitles to that job\.

```
aws transcribe start-transcription-job \
--cli-input-json file://example-start-command.json
```

The file *example\-start\-command\.json* contains the following request body\.

```
{
  "TranscriptionJobName": "job-name",
  "LanguageCode": "en-US",
  "Media": {
        "MediaFileUri": "s3://your-S3-bucket/S3-prefix/your-filename.file-extension"
    },
  "Subtitles": {"Formats": ["vtt"]}
}
```

### AWS SDK for Python \(Boto3\)<a name="subtitles-howto-sdk"></a>

The following example uses the AWS SDK for Python \(Boto3\) to add subtitles using the `Subtitles` argument for the [start\_transcription\_job](https://boto3.amazonaws.com/v1/documentation/api/latest/reference/services/transcribe.html#TranscribeService.Client.start_transcription_job) method:

```
from __future__ import print_function
import time
import boto3
transcribe = boto3.client('transcribe')
job_name = "job-name"
job_uri = "s3://your-S3-bucket/S3-prefix/your-filename.file-extension"
transcribe.start_transcription_job(
    TranscriptionJobName=job_name,
    Media={'MediaFileUri': job_uri},
    MediaFormat='wav',
    LanguageCode='en-US', 
    Subtitles={'Formats': ['vtt']}
)
while True:
    status = transcribe.get_transcription_job(TranscriptionJobName=job_name)
    if status['TranscriptionJob']['TranscriptionJobStatus'] in ['COMPLETED', 'FAILED']:
        break
    print("Not ready yet...")
    time.sleep(5)
print(status)
```