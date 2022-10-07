# Partitioning speakers \(diarization\)<a name="diarization"></a>

To partition the text from different speakers in Amazon Transcribe, use *speaker diarization*\. When you enable speaker diarization, Amazon Transcribe labels each speaker utterance\. You enable speaker diarization by using the batch transcription or real\-time streaming APIs, or the AWS Management Console\.

## Partitioning speakers in audio<a name="diarization-batch"></a>

You can enable speaker diarization in a batch transcription job using either the [StartTranscriptionJob](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_StartTranscriptionJob.html) API or the [AWS Management Console](https://console.aws.amazon.com/transcribe/)\.

### AWS Management Console<a name="diarization-console-batch"></a>

To use the AWS Management Console to enable speaker diarization in your transcription job, you enable audio identification and then speaker diarization\.

1. Sign in to the [AWS Management Console](https://console.aws.amazon.com/transcribe/)\.

1. In the navigation pane, under Amazon Transcribe, choose **Transcription jobs**\.

1. Choose **Create job**\.

1. On the **Specify job details** page, provide information about your transcription job\.

1. Choose **Next**\.

1. Enable **Audio identification**\.

1. For **Audio identification type**, choose **Speaker partitioning**\.

1. For **Maximum number of speakers**, specify the maximum number of speakers you think are speaking in your audio\.

1. Choose **Create**\.

### AWS CLI<a name="diarization-batch-cli"></a>
+ Run the following code\.

  ```
                      
  aws transcribe start-transcription-job \
  --cli-input-json file://filepath/example-start-command.json
  ```

  The following code shows the contents of `example-start-command.json`\.

  ```
  {
      "TranscriptionJobName": "my-first-transcription-job",
      "LanguageCode": "en-US",
      "Media": {
          "MediaFileUri": "s3://DOC-EXAMPLE-BUCKET/my-input-files/my-media-file.flac"
      },
      "OutputBucketName": "DOC-EXAMPLE-BUCKET",
      "OutputKey": "my-output-files/", 
      "Settings":{
          "MaxSpeakerLabels": 2,
          "ShowSpeakerLabels":true
      }
  }
  ```

## Partitioning speakers in real\-time streams<a name="diarization-streaming"></a>

You can partition different speakers in either HTTP/2 or WebSocket streams\. Speaker diarization works best for partitioning between two and five speakers\. Although Amazon Transcribe can separate text for more than five speakers in a stream, the accuracy of speaker diarization decreases if you exceed that number\. To start an HTTP/2 stream, you specify the `ShowSpeakerLabel` request parameter of the [StartStreamTranscription](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_streaming_StartStreamTranscription.html) API\. To start a WebSocket request, you use a pre\-signed URI, which is a URI that contains the information needed to start your stream\. To use the AWS Management Console to transcribe speech spoken into your microphone, use the following procedure\.

You can partition speakers in real\-time streams that are in US English \(en\-US\)\.

You can use the [AWS Management Console](https://console.aws.amazon.com/transcribe/) to start a real\-time stream and transcribe any speech picked up by your microphone\.

1. Sign in to the [AWS Management Console](https://console.aws.amazon.com/transcribe/)\.

1. In the navigation pane, choose **Real\-time transcription**\.

1. In **Language**, choose the language of your real\-time stream\.

1. Under **Additional settings**, enable **Speaker partitioning**\.

1. Choose **Start streaming**\.

1. Speak into the microphone\.

### HTTP/2 streaming<a name="diarization-http2"></a>

The following is the syntax for the parameters of an HTTP/2 request\.

```
POST /stream-transcription HTTP/2
host: transcribestreaming.us-west-2.amazonaws.com
authorization: Generated value
x-amz-target: com.amazonaws.transcribe.Transcribe.StartStreamTranscription
x-amz-content-sha256: STREAMING-AWS4-HMAC-SHA256-EVENTS
x-amz-date: 20220208T235959Z
x-amzn-transcribe-session-id: my-first-http2-diarization-stream
x-amzn-transcribe-language-code: en-US
x-amzn-transcribe-media-encoding: flac
x-amzn-transcribe-sample-rate: 16000
x-amzn-transcribe-show-speaker-label: true
content-type: application/vnd.amazon.eventstream
transfer-encoding: chunked
```

Parameter descriptions:
+ **host**: Update the AWS Region \('us\-west\-2' in the preceding example\) with the AWS Region you are calling\. For a list of valid AWS Regions, see [AWS Regions and Endpoints](https://docs.aws.amazon.com/general/latest/gr/rande.html#transcribe_region)\.
+ **authorization**: This is a generated field\. To learn more about creating a signature, see [Signing AWS requests with Signature Version 4](https://docs.aws.amazon.com/general/latest/gr/sigv4_signing.html)\.
+ **x\-amz\-target**: Don't alter this field; use the content shown in the preceding example\.
+ **x\-amz\-content\-sha256**: This is a generated field\. To learn more about calculating a signature, see [Signing AWS requests with Signature Version 4](https://docs.aws.amazon.com/general/latest/gr/sigv4_signing.html)\.
+ **x\-amz\-date**: The date and time the signature is created\. The format is YYYYMMDDTHHMMSSZ, where YYYY=year, MM=month, DD=day, HH=hour, MM=minute, SS=seconds, and 'T' and 'Z' are fixed characters\. For more information, refer to [Handling Dates in Signature Version 4](https://docs.aws.amazon.com/general/latest/gr/sigv4-date-handling.html)\.
+ **x\-amzn\-transcribe\-session\-id**: The name for your streaming session\.
+ **x\-amzn\-transcribe\-language\-code**: The encoding used for your input audio\. Refer to [StartStreamTranscription](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_streaming_StartStreamTranscription.html) or [Supported languages and language\-specific features](supported-languages.md) for a list of valid values\.
+ **x\-amzn\-transcribe\-media\-encoding**: The encoding used for your input audio\. Valid values are `pcm`, `ogg-opus`, and `flac`\.
+ **x\-amzn\-transcribe\-sample\-rate**: The sample rate of the input audio \(in Hertz\)\. Amazon Transcribe supports a range from 8,000 Hz to 48,000 Hz\. Low\-quality audio, such as telephone audio, is typically around 8,000 Hz\. High\-quality audio typically ranges from 16,000 Hz to 48,000 Hz\. Note that the sample rate you specify **must** match that of your audio\.
+ **x\-amzn\-transcribe\-show\-speaker\-label**: To enable diarization, this value must be `true`\.
+ **content\-type**: Don't alter this field; use the content shown in the preceding example\.

### WebSocket streaming<a name="diarization-websocket"></a>

To partition speakers in WebSocket streams, use the following format to create a pre\-signed URI to start a WebSocket request and specify `show-speaker-label` as `true`\. A pre\-signed URI contains the information to set up bi\-directional communication between your application and Amazon Transcribe\.

```
GET wss://transcribestreaming.us-west-2.amazonaws.com:8443/stream-transcription-websocket
?
&X-Amz-Algorithm=AWS4-HMAC-SHA256
&X-Amz-Credential=AKIAIOSFODNN7EXAMPLE%2F20220208%2Fus-west-2%2Ftranscribe%2Faws4_request
&X-Amz-Date=20220208T235959Z
&X-Amz-Expires=250
&X-Amz-Security-Token=security-token
&X-Amz-Signature=Signature Version 4 signature
&X-Amz-SignedHeaders=host
&language-code=en-US
&media-encoding=flac
&sample-rate=16000
&show-speaker-label=true
```

Parameter definitions can be found in the [API Reference](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_Reference.html); parameters common to all AWS API operations are listed in the [Common Parameters](https://docs.aws.amazon.com/transcribe/latest/APIReference/CommonParameters.html) section\.