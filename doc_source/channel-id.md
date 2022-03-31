# Transcribing multi\-channel audio<a name="channel-id"></a>

If your audio has multiple channels, you can use *channel identification* to transcribe the speech from each of those channels\. Amazon Transcribe identifies the speech from each channel and transcribes that speech in separate transcriptions\. It combines those transcriptions into a single transcription output\.

 You can enable channel identification for both batch processing and real\-time streaming\. The following list describes how to enable it for each method\.
+ Batch transcription \- [AWS Management Console](https://console.aws.amazon.com/transcribe/) and [StartTranscriptionJob](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_StartTranscriptionJob.html) API
+ Streaming transcription \- WebSocket streaming and [StartStreamTranscription](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_streaming_StartStreamTranscription.html) API

## Transcribing multi\-channel audio<a name="channel-id-batch"></a>

To transcribe multi\-channel audio in a batch transcription job, use the [AWS Management Console](https://console.aws.amazon.com/transcribe/) or the [StartTranscriptionJob](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_StartTranscriptionJob.html) API\.

### AWS Management Console<a name="channel-id-batch-console"></a>

To use the AWS Management Console to enable channel identification in your batch transcription job, you enable audio identification and then channel identification\. Channel identification is a subset of audio identification in the AWS Management Console\.

1. Sign in to the [AWS Management Console](https://console.aws.amazon.com/transcribe/)\.

1. In the navigation pane, under Amazon Transcribe, choose **Transcription jobs**\.

1. Choose **Create job**\.

1. On the **Specify job details** page, provide information about your transcription job\.

1. Choose **Next**\.

1. Enable **Audio identification**\.

1. For **Audio identification type**, choose **Channel identification**\.

1. Choose **Create**\.

### API<a name="channel-id-batch-api"></a>

**To transcribe multi\-channel audio \(API\)**
+ For the [StartTranscriptionJob](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_StartTranscriptionJob.html) API, specify the following\.

  1. For `TranscriptionJobName`, specify a name unique to your AWS account\.

  1. For `LanguageCode`, specify the language code that corresponds to the language spoken in your media file\. For available languages and corresponding language codes, see [What is Amazon Transcribe?](what-is.md)\. 

  1. For the `MediaFileUri` parameter of the `Media` object, specify the name of the media file you want to transcribe\.

  1. For the `Settings` object, set `ChannelIdentification` to `true`\.

The following is an example request using the AWS SDK for Python \(Boto3\)\.

```
  from __future__ import print_function
  import time
  import boto3
  transcribe = boto3.client('transcribe')
  job_name = "my-first-transcription-job"
  job_uri = "s3://DOC-EXAMPLE-BUCKET/my-media-file.flac"
  transcribe.start_transcription_job(
      TranscriptionJobName=job_name,
      Media= {'MediaFileUri': job_uri},
      MediaFormat= 'flac',
      LanguageCode= 'en-US',
      Settings = {
          'ChannelIdentification': True,
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

### AWS CLI<a name="channel-id-cli"></a>

**To transcribe multi\-channel audio using a batch transcription job \(AWS CLI\)**
+ Run the following code\.

  ```
                      
  aws transcribe start-transcription-job \
  --cli-input-json file://filepath/my-first-channel-id-job.json
  ```

  The following is the code of `my-first-channel-id-job.json`\.

  ```
    {
      "TranscriptionJobName": "my-first-transcription-job",
      "LanguageCode": "en-US",
      "Media": {
          "MediaFileUri": "s3://DOC-EXAMPLE-BUCKET/my-media-file.flac"
      },
      "Settings":{
    "ChannelIdentification":true
    }
  ```

  The following is the response\.

  ```
  {
      "TranscriptionJob": {
          "TranscriptionJobName": "my-first-transcription-job",
          "TranscriptionJobStatus": "IN_PROGRESS",
          "LanguageCode": "en-US",
          "Media": {
              "MediaFileUri": "s3:/DOC-EXAMPLE-BUCKET/my-media-file.flac"
          },
          "StartTime": "2020-09-12T23:20:28.239000+00:00",
          "CreationTime": "2020-09-12T23:20:28.203000+00:00",
          "Settings": {
              "ChannelIdentification": true
          }
      }
  }
  ```

The following code shows the transcription output for audio that has a conversation on two channels\.

```
{
  "jobName": "job id",
  "accountId": "account id",
  "results": {
    "transcripts": [
      {
        "transcript": "When you try ... It seems to ..."
      }
    ],
    "channel_labels": {
      "channels": [
        {
          "channel_label": "ch_0",
          "items": [
            {
              "start_time": "12.282",
              "end_time": "12.592",
              "alternatives": [
                {
                  "confidence": "1.0000",
                  "content": "When"
                }
              ],
              "type": "pronunciation"
            },
            {
              "start_time": "12.592",
              "end_time": "12.692",
              "alternatives": [
                {
                  "confidence": "0.8787",
                  "content": "you"
                }
              ],
              "type": "pronunciation"
            },
            {
              "start_time": "12.702",
              "end_time": "13.252",
              "alternatives": [
                {
                  "confidence": "0.8318",
                  "content": "try"
                }
              ],
              "type": "pronunciation"
            },
            ...
         ]
      },
      {
          "channel_label": "ch_1",
          "items": [
            {
              "start_time": "12.379",
              "end_time": "12.589",
              "alternatives": [
                {
                  "confidence": "0.5645",
                  "content": "It"
                }
              ],
              "type": "pronunciation"
            },
            {
              "start_time": "12.599",
              "end_time": "12.659",
              "alternatives": [
                {
                  "confidence": "0.2907",
                  "content": "seems"
                }
              ],
              "type": "pronunciation"
            },
            {
              "start_time": "12.669",
              "end_time": "13.029",
              "alternatives": [
                {
                  "confidence": "0.2497",
                  "content": "to"
                }
              ],
              "type": "pronunciation"
            },
            ...
        ]
    }
}
```

Amazon Transcribe transcribes the audio from each channel separately and combines the transcribed text from each channel into a single transcription output\.

For each channel in the transcription output, Amazon Transcribe returns a list of *items*\. An item is a transcribed word, pause, or punctuation mark\. Each item has a start time and an end time\. If a person on one channel speaks over a person on a separate channel, the start times and end times of the items for each channel overlap while the individuals are speaking over each other\.

## Transcribing multi\-channel audio streams<a name="channel-id-stream"></a>

You can transcribe audio from separate channels in either HTTP/2 or WebSocket streams using the [StartStreamTranscription](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_streaming_StartStreamTranscription.html) API\.

### Transcribing multi\-channel audio in an HTTP/2 stream<a name="channel-id-http2"></a>

To transcribe multi\-channel audio in an HTTP/2 stream, use the [StartStreamTranscription](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_streaming_StartStreamTranscription.html) API and specify the following:
+ `LanguageCode` \- The language code of the audio\.
+ `MediaEncoding` \- The encoding of the audio\.
+ `EnableChannelIdentification` \- `true`
+ `NumberOfChannels` \- The number of channels in your streaming audio\.

The following is the syntax for the parameters of an HTTP/2 request\.

```
POST /stream-transcription HTTP/2
host: transcribestreaming.us-west-2.amazonaws.com
authorization: Generated value
x-amz-target: com.amazonaws.transcribe.Transcribe.StartStreamTranscription
x-amz-content-sha256: STREAMING-AWS4-HMAC-SHA256-EVENTS
x-amz-date: 20220208T235959Z
x-amzn-transcribe-session-id: my-first-http2-channel-id-stream
x-amzn-transcribe-language-code: en-US
x-amzn-transcribe-media-encoding: flac
x-amzn-transcribe-sample-rate: 16000
x-amzn-transcribe-enable-channel-identification: true
x-amzn-transcribe-number-of-channels: 2
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
+ **x\-amzn\-transcribe\-language\-code**: The encoding used for your input audio\. Refer to [StartStreamTranscription](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_streaming_StartStreamTranscription.html) or [Supported languages and language\-specific features](supported-languages.md#table-language-matrix) for a list of valid values\.
+ **x\-amzn\-transcribe\-media\-encoding**: The encoding used for your input audio\. Valid values are `pcm`, `ogg-opus`, and `flac`\.
+ **x\-amzn\-transcribe\-sample\-rate**: The sample rate of the input audio \(in Hertz\)\. Amazon Transcribe supports a range from 8,000 Hz to 48,000 Hz\. Low\-quality audio, such as telephone audio, is typically around 8,000 Hz\. High\-quality audio typically ranges from 16,000 Hz to 48,000 Hz\. Note that the sample rate you specify **must** match that of your audio\.
+ **x\-amzn\-transcribe\-enable\-channel\-identification**: To enable channel identification, this field must be `true`\.
+ **x\-amzn\-transcribe\-number\-of\-channels**: Must be `2` when `x-amzn-transcribe-enable-channel-identification` is set to `true`\.
+ **content\-type**: Don't alter this field; use the content shown in the preceding example\.

### Transcribing multi\-channel audio in a WebSocket stream<a name="channel-id-websocket"></a>

To identify speakers in WebSocket streams, use the following format to create a pre\-signed URI and start a WebSocket request\. Specify `enable-channel-id` as `true` and the number of channels in your stream in `number-of-channels`\. A pre\-signed URI contains the information needed to set up bi\-directional communication between your application and Amazon Transcribe\.

```
GET wss://transcribestreaming.us-west-2.amazonaws.com:8443/stream-transcription-websocket
?language-code=languageCode
&X-Amz-Algorithm=AWS4-HMAC-SHA256
&X-Amz-Credential=AKIAIOSFODNN7EXAMPLE%2F20220208%2Fus-west-2%2Ftranscribe%2Faws4_request
&X-Amz-Date=20220208T235959Z
&X-Amz-Expires=250
&X-Amz-Security-Token=security-token
&X-Amz-Signature=Signature Version 4 signature
&X-Amz-SignedHeaders=host
&media-encoding=flac
&sample-rate=16000
&session-id=sessionId
&enable-channel-identification=true
&number-of-channels=number of channels in your audio stream
```

### Multi\-channel streaming output<a name="streaming-output"></a>

The output of a streaming transcription is the same for HTTP/2 and WebSocket requests\. The following is an example output\.

```
{
    "resultId": "XXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXX",
    "startTime": 0.11,
    "endTime": 0.66,
    "isPartial": false,
    "alternatives": [
        {
            "transcript": "Left.",
            "items": [
                {
                    "startTime": 0.11,
                    "endTime": 0.45,
                    "type": "pronunciation",
                    "content": "Left",
                    "vocabularyFilterMatch": false
                },
                {
                    "startTime": 0.45,
                    "endTime": 0.45,
                    "type": "punctuation",
                    "content": ".",
                    "vocabularyFilterMatch": false
                }
            ]
        }
    ],
    "channelId": "ch_0"
}
```

For each speech segment, there is a `channelId` flag that indicates which channel the speech belongs to\.