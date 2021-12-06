# Step 4: Transcribing with a custom language model<a name="clm-transcription"></a>

You can use a CLM to transcribe your audio files using either batch transcription jobs or real\-time streams\.

## Using a custom language model with a batch transcription job<a name="clm-batch-transcription"></a>

You can transcribe with a CLM for batch transcription jobs using the **Amazon Transcribe Console**, **AWS CLI**, or **AWS SDK**; see the following instructions\.

### Console<a name="clm-use-howto-console"></a>

1. Sign in to the [Amazon Transcribe console](https://console.aws.amazon.com/transcribe/)\.

1. In the navigation pane, choose **Transcription jobs**, then select the **Create job** button \(top right\)\. This opens the **Specify job details** page\.

1. In the **Job settings** panel under **Model type**, select the **Custom language model** box\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/clm-console.png)

   You must also select an input language from the drop\-down menu\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/clm-console-language.png)

1. Under **Custom model selection**, either select an existing custom language model from the drop\-down menu or click on 'create a new one'\.

   Add the S3 location of your input file in the **Input data** panel\.

1. Click the **Next** button for additional configuration options\. Click the **Create job** button to run your transcription job\.

### AWS CLI<a name="clm-use-howto-cli"></a>

This example uses the [start\-transcription\-job](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/transcribe/start-transcription-job.html) command and `LanguageModelName` parameter\. For more information, see [ StartTranscriptionJob ](API_StartTranscriptionJob.md) and [ ModelSettings ](API_ModelSettings.md)\.

```
aws transcribe start-transcription-job \
--transcription-job-name job-name
--media MediaFileUri="s3://your-S3-bucket/S3-prefix/your-filename.file-extension" \
--model-settings LanguageModelName=your-language-model-name
```

Here's another example using the [start\-transcription\-job](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/transcribe/start-transcription-job.html) command, and a request body that uses your CLM with that job\.

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
  "ModelSettings": {
        "LanguageModelName": "your-language-model-name"
    }
}
```

### AWS SDK for Python \(Boto3\)<a name="clm-use-howto-sdk"></a>

This example uses the AWS SDK for Python \(Boto3\) to transcribe a file with the `LanguageModelName` argument for the [start\_transcription\_job](https://boto3.amazonaws.com/v1/documentation/api/latest/reference/services/transcribe.html#TranscribeService.Client.start_transcription_job) method\. For more information, see [ StartTranscriptionJob ](API_StartTranscriptionJob.md) and [ ModelSettings ](API_ModelSettings.md)\.

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
    ModelSettings = {
        'LanguageModelName': 'your-language-model-name'
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

## Using a custom language model with a real\-time stream<a name="clm-streaming-transcription"></a>

You can use a CLM to transcribe a real\-time stream with either a WebSocket request or the [ StartStreamTranscription ](API_streaming_StartStreamTranscription.md) operation\.

**Note**  
Only CLMs created after streaming support are available for use with streaming transcriptions\. If your CLM was created prior to streaming support, you must re\-create it to use it with a real\-time stream\.

### WebSocket<a name="clm-use-howto-websocket"></a>

This example creates a pre\-signed URL that uses a custom language model in a WebSocket stream\. For more information on using WebSocket streams with Amazon Transcribe, see [Using Amazon Transcribe streaming with WebSockets](websocket.md)\. For more detail on parameters, see [ StartStreamTranscription ](API_streaming_StartStreamTranscription.md)\.

```
GET wss://transcribestreaming.region.amazonaws.com:8443/stream-transcription-websocket?language-code=en-US
&X-Amz-Algorithm=AWS4-HMAC-SHA256
&X-Amz-Credential=Signature Version 4 credential scope
&X-Amz-Date=date
&X-Amz-Expires=200
&X-Amz-Security-Token=security-token
&X-Amz-Signature=Signature Version 4 signature 
&X-Amz-SignedHeaders=host
&media-encoding=flac
&sample-rate=16000
&session-id=sessionId   &language-model-name=your-language-model-name
```

URL parameters:
+ **region**: The AWS Region where you are calling Amazon Transcribe\. For a list of valid Regions, see [AWS Regions and Endpoints](https://docs.aws.amazon.com/general/latest/gr/rande.html#transcribe_region)\.
+ **language\-code**: The language code for the input audio\. Refer to [Supported languages and language\-specific features](supported-languages.md#table-language-matrix) for supported languages\.
+ **media\-encoding**: The encoding used for the input audio\. Valid values are `pcm`, `ogg-opus`, and `flac`\.
+ **sample\-rate**: The sample rate of the input audio \(in Hertz\)\. We recommend using 8,000 Hz for low\-quality audio and 16,000 Hz \(or higher\) for high\-quality audio\. The sample rate you specify must match that in the audio file\.
+ **session\-id**: Optional\. An identifier for the transcription session\. If you don't provide a session ID, Amazon Transcribe generates one for you and returns it in the response\.
+ **language\-model\-name**: The name of your custom language model\.

Signature Version 4 parameters:
+ **X\-Amz\-Algorithm**: The algorithm to use in the signing process; this must be `AWS4-HMAC-SHA256`\.
+ **X\-Amz\-Credential**: A string, separated by slashes \("/"\), formed by concatenating your access key ID and your credential scope components\. Credential scope includes the date \(YYYYMMDD\), AWS Region, service name, and a special termination string \(aws4\_request\)\.
+ **X\-Amz\-Date**: The date and time your signature is created in the form YYYYMMDD'T'HHMMSS'Z'\.
+ **X\-Amz\-Expires**: The length of time \(in seconds\) until the credentials expire\. The maximum value is 300 seconds\.
+ **X\-Amz\-Security\-Token**: Optional\. A Signature Version 4 token for temporary credentials\. If you specify this parameter, include it in the canonical request\. For more information, see [Requesting temporary security credentials](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_temp_request.html)\.
+ **X\-Amz\-Signature**: The Signature Version 4 signature you generated for your request\.
+ **X\-Amz\-SignedHeaders**: The headers that are signed when creating the signature for your request; this must be `host`\.

For additional details on Signature Version 4 elements, refer to the [AWS General Reference](https://docs.aws.amazon.com/general/latest/gr/sigv4_elements.html)\.

### HTTP/2<a name="clm-use-howto-http2"></a>

This example creates an HTTP/2 request with a custom language model\. For more information on using HTTP/2 streaming with Amazon Transcribe, see [Using Amazon Transcribe streaming With HTTP/2](how-streaming.md)\. For more detail on parameters and headers specific to Amazon Transcribe, see [ StartStreamTranscription ](API_streaming_StartStreamTranscription.md)\.

```
POST /stream-transcription HTTP/2.0
host: transcribestreaming.region.amazonaws.com
authorization: Generated value
content-type: application/vnd.amazon.eventstream
x-amz-target: com.amazonaws.transcribe.Transcribe.StartStreamTranscription
x-amz-content-sha256: STREAMING-AWS4-HMAC-SHA256-EVENTS
x-amz-date: Date
x-amzn-transcribe-language-code: en-US
x-amzn-transcribe-media-encoding: flac
x-amzn-transcribe-sample-rate: 16000
transfer-encoding: chunked            
x-amzn-language-model-name: your-language-model-name
```

Use the following values in your request:
+ **region**: The AWS Region where you are calling Amazon Transcribe\. For a list of valid Regions, see [ AWS Regions and Endpoints](https://docs.aws.amazon.com/general/latest/gr/rande.html#transcribe_region)\.
+ **authorization**: The Signature Version 4 signature for the request\. To learn more about creating a signature, see [ Signing AWS requests with Signature Version 4](https://docs.aws.amazon.com/general/latest/gr/sigv4_signing.html)\.
+ **x\-amz\-date**: The date and time for your request\. Refer to [Handling dates in Signature Version 4](https://docs.aws.amazon.com/general/latest/gr/sigv4-date-handling.html) for instructions\.
+ **x\-amzn\-transcribe\-media\-encoding**: The encoding used for your input audio\. Valid values are `pcm`, `ogg-opus`, and `flac`\.
+ **x\-amzn\-transcribe\-sample\-rate**: The sample rate of the input audio \(in Hertz\)\. We recommend using 8,000 Hz for low\-quality audio and 16,000 Hz \(or higher\) for high\-quality audio\. The sample rate you specify must match that in the audio file\.
+ **x\-amzn\-language\-model\-name**: The name of your custom language model\.

**Next step**  
[Step 5: Viewing and updating your custom language models](view-update-lang.md)