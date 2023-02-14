# Partitioning speakers \(diarization\)<a name="diarization"></a>

You can partition the text from different speakers using *speaker diarization*\. When you enable speaker diarization, Amazon Transcribe labels each speaker utterance in your transcript so you can distinguish between each speaker\.

## Partitioning speakers in a batch transcription<a name="diarization-batch"></a>

To partition speakers in a batch transcription, see the following examples:

### AWS Management Console<a name="diarization-console-batch"></a>

1. Sign in to the [AWS Management Console](https://console.aws.amazon.com/transcribe/)\.

1. In the navigation pane, choose **Transcription jobs**, then select **Create job** \(top right\)\. This opens the **Specify job details** page\.  
![\[Amazon Transcribe console 'Specify job details' page. In the 'Job settings' panel, you can specify a name for your transcription job, select a Model type, and specify your language settings.\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/console-batch-job-details-1.png)![\[Amazon Transcribe console 'Specify job details' page. In the 'Job settings' panel, you can specify a name for your transcription job, select a Model type, and specify your language settings.\]](http://docs.aws.amazon.com/transcribe/latest/dg/)

1. Fill in any fields you want to include on the **Specify job details** page, then select **Next**\. This takes you to the **Configure job \- *optional*** page\.

   In the **Audio settings** panel, select **Speaker partitioning** \(under the 'Audio identification type heading'\)\. You can optionally specify the number of speakers you want to partition, up to a maximum of 10\.  
![\[Amazon Transcribe console 'Configure job' page. In the 'Audio settings' panel, you can enable 'Speaker partitioning'.\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/diarization-batch.png)

1. Select **Create job** to run your transcription job\. 

### AWS CLI<a name="diarization-cli"></a>

This example uses the [start\-transcription\-job](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/transcribe/start-transcription-job.html)\. For more information, see [https://docs.aws.amazon.com/transcribe/latest/APIReference/API_StartTranscriptionJob.html](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_StartTranscriptionJob.html)\.

```
aws transcribe start-transcription-job \
--region us-west-2 \
--transcription-job-name my-first-transcription-job \
--media MediaFileUri=s3://DOC-EXAMPLE-BUCKET/my-input-files/my-media-file.flac \
--output-bucket-name DOC-EXAMPLE-BUCKET \
--output-key my-output-files/ \
--language-code en-US \
--show-speaker-labels TRUE \    
--max-speaker-labels 3
```

Here's another example using the [start\-transcription\-job](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/transcribe/start-transcription-job.html) command, and a request body that enables speaker partitioning with that job\.

```
aws transcribe start-transcription-job \
--region us-west-2 \
--cli-input-json file://my-first-transcription-job.json
```

The file *my\-first\-transcription\-job\.json* contains the following request body\.

```
{
  "TranscriptionJobName": "my-first-transcription-job",
  "Media": {
        "MediaFileUri": "s3://DOC-EXAMPLE-BUCKET/my-input-files/my-media-file.flac"
  },
  "OutputBucketName": "DOC-EXAMPLE-BUCKET",
  "OutputKey": "my-output-files/", 
  "LanguageCode": "en-US",
  "ShowSpeakerLabels": 'TRUE',    
  "MaxSpeakerLabels": 3
 }
```

### AWS SDK for Python \(Boto3\)<a name="diarization-python-batch"></a>

This example uses the AWS SDK for Python \(Boto3\) to identify channels using the [start\_transcription\_job](https://boto3.amazonaws.com/v1/documentation/api/latest/reference/services/transcribe.html#TranscribeService.Client.start_transcription_job) method\. For more information, see [StartTranscriptionJob](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_StartTranscriptionJob.html)\.

```
from __future__ import print_function
import time
import boto3
transcribe = boto3.client('transcribe', 'us-west-2')
job_name = "my-first-transcription-job"
job_uri = "s3://DOC-EXAMPLE-BUCKET/my-input-files/my-media-file.flac"
transcribe.start_transcription_job(
    TranscriptionJobName = job_name,
    Media = {
        'MediaFileUri': job_uri
    },
    OutputBucketName = 'DOC-EXAMPLE-BUCKET',
    OutputKey = 'my-output-files/', 
    LanguageCode = 'en-US', 
    ShowSpeakerLabels: 'TRUE',    
    MaxSpeakerLabels: 3
)

while True:
    status = transcribe.get_transcription_job(TranscriptionJobName = job_name)
    if status['TranscriptionJob']['TranscriptionJobStatus'] in ['COMPLETED', 'FAILED']:
        break
    print("Not ready yet...")
    time.sleep(5)
print(status)
```

## Partitioning speakers in a streaming transcription<a name="diarization-stream"></a>

To partition speakers in a streaming transcription, see the following examples:

### Streaming transcriptions<a name="diarization-console-stream"></a>

1. Sign in to the [AWS Management Console](https://console.aws.amazon.com/transcribe/)\.

1. In the navigation pane, choose **Real\-time transcription**\. Scroll down to **Audio settings** and expand this field if it is minimized\.  
![\[Amazon Transcribe console screenshot: the 'audio settings' tab on the 'real-time transcription' page.\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/diarization-streaming1.png)

1. Toggle on **Speaker partitioning**\.  
![\[Amazon Transcribe console screenshot: the expanded 'audio settings' tab with speaker partitioning enabled.\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/diarization-streaming2.png)

1. You're now ready to transcribe your stream\. Select **Start streaming** and begin speaking\. To end your dictation, select **Stop streaming**\.

### HTTP/2 stream<a name="diarization-http2"></a>

This example creates an HTTP/2 request that partitions speakers in your transcription output\. For more information on using HTTP/2 streaming with Amazon Transcribe, see [Setting up an HTTP/2 stream](streaming-http2.md)\. For more detail on parameters and headers specific to Amazon Transcribe, see [StartStreamTranscription](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_streaming_StartStreamTranscription.html)\.

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
x-amzn-transcribe-show-speaker-label: true
transfer-encoding: chunked
```

Parameter definitions can be found in the [API Reference](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_Reference.html); parameters common to all AWS API operations are listed in the [Common Parameters](https://docs.aws.amazon.com/transcribe/latest/APIReference/CommonParameters.html) section\.

### WebSocket stream<a name="diarization-websocket"></a>

This example creates a pre\-signed URL that separates speakers in your transcription output\. Line breaks have been added for readability\. For more information on using WebSocket streams with Amazon Transcribe, see [Setting up a WebSocket stream](streaming-websocket.md)\. For more detail on parameters, see [https://docs.aws.amazon.com/transcribe/latest/APIReference/API_streaming_StartStreamTranscription.html](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_streaming_StartStreamTranscription.html)\.

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
&specialty=PRIMARYCARE
&type=DICTATION
&media-encoding=flac
&sample-rate=16000        
&show-speaker-label=true
```

Parameter definitions can be found in the [API Reference](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_Reference.html); parameters common to all AWS API operations are listed in the [Common Parameters](https://docs.aws.amazon.com/transcribe/latest/APIReference/CommonParameters.html) section\.