# Transcribing multi\-channel audio<a name="channel-id"></a>

If your audio has multiple channels, you can use *channel identification* to transcribe the speech from each channel separately\. The output from each channel is provided in one file, with the content from the first channel listed above the content from the second channel\.

For each channel in the transcription output, Amazon Transcribe returns a list of *items*\. An item is a transcribed word, pause, or punctuation mark\. Each item has a start time and an end time\. If a person on one channel speaks over a person on a separate channel, the start times and end times of the items for each channel overlap while the individuals are speaking over each other\.

## Using channel identification in a batch transcription<a name="channel-id-batch"></a>

To identify channels in a batch transcription, you can use the **AWS Management Console**, **AWS CLI**, or **AWS SDKs**; see the following for examples:

### AWS Management Console<a name="channel-id-console-batch"></a>

1. Sign in to the [AWS Management Console](https://console.aws.amazon.com/transcribe/)\.

1. In the navigation pane, choose **Transcription jobs**, then select **Create job** \(top right\)\. This opens the **Specify job details** page\.  
![\[Amazon Transcribe console 'Specify job details' page. In the 'Job settings' panel, you can specify a name for your transcription job, select a Model type, and specify your language settings.\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/console-batch-job-details-1.png)![\[Amazon Transcribe console 'Specify job details' page. In the 'Job settings' panel, you can specify a name for your transcription job, select a Model type, and specify your language settings.\]](http://docs.aws.amazon.com/transcribe/latest/dg/)

1. Fill in any fields you want to include on the **Specify job details** page, then select **Next**\. This takes you to the **Configure job \- *optional*** page\.

   In the **Audio settings** panel, select **Channel identification** \(under the 'Audio identification type heading'\)\.  
![\[Amazon Transcribe console 'Configure job' page. In the 'Audio settings' panel, you can enable Channel identification.\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/channel-id-batch.png)

1. Select **Create job** to run your transcription job\. 

### AWS CLI<a name="channel-id-cli"></a>

This example uses the [start\-transcription\-job](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/transcribe/start-transcription-job.html)\. For more information, see [https://docs.aws.amazon.com/transcribe/latest/APIReference/API_StartTranscriptionJob.html](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_StartTranscriptionJob.html)\.

```
aws transcribe start-transcription-job \
--region us-west-2 \
--transcription-job-name my-first-transcription-job \
--media MediaFileUri=s3://DOC-EXAMPLE-BUCKET/my-input-files/my-media-file.flac \
--output-bucket-name DOC-EXAMPLE-BUCKET \
--output-key my-output-files/ \
--language-code en-US \
--settings ChannelIdentification=true
```

Here's another example using the [start\-transcription\-job](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/transcribe/start-transcription-job.html) command, and a request body that enables channel identification with that job\.

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
    "Settings": {
        "ChannelIdentification": true
    }
}
```

### AWS SDK for Python \(Boto3\)<a name="channel-id-python-batch"></a>

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
    Settings = {
        'ChannelIdentification':True
    }
)

while True:
    status = transcribe.get_transcription_job(TranscriptionJobName = job_name)
    if status['TranscriptionJob']['TranscriptionJobStatus'] in ['COMPLETED', 'FAILED']:
        break
    print("Not ready yet...")
    time.sleep(5)
print(status)
```

## Using channel identification in a streaming transcription<a name="channel-id-stream"></a>

To identify channels in a streaming transcription, you can use **HTTP/2** or **WebSockets**; see the following for examples:

### HTTP/2 stream<a name="channel-id-http2"></a>

This example creates an HTTP/2 request that separates channels in your transcription output\. For more information on using HTTP/2 streaming with Amazon Transcribe, see [Setting up an HTTP/2 stream](streaming-http2.md)\. For more detail on parameters and headers specific to Amazon Transcribe, see [StartStreamTranscription](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_streaming_StartStreamTranscription.html)\.

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
x-amzn-channel-identification: TRUE
transfer-encoding: chunked
```

Parameter definitions can be found in the [API Reference](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_Reference.html); parameters common to all AWS API operations are listed in the [Common Parameters](https://docs.aws.amazon.com/transcribe/latest/APIReference/CommonParameters.html) section\.

### WebSocket stream<a name="channel-id-websocket"></a>

This example creates a pre\-signed URL that separates channels in your transcription output\. Line breaks have been added for readability\. For more information on using WebSocket streams with Amazon Transcribe, see [Setting up a WebSocket stream](streaming-websocket.md)\. For more detail on parameters, see [https://docs.aws.amazon.com/transcribe/latest/APIReference/API_streaming_StartStreamTranscription.html](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_streaming_StartStreamTranscription.html)\.

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
&channel-identification=TRUE
```

Parameter definitions can be found in the [API Reference](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_Reference.html); parameters common to all AWS API operations are listed in the [Common Parameters](https://docs.aws.amazon.com/transcribe/latest/APIReference/CommonParameters.html) section\.