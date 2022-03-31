# Transcribing multi\-channel audio<a name="conversation-channel-id-med"></a>

If you have an audio file or stream that has multiple channels, you can use *channel identification* to transcribe the speech from each of those channels\. Amazon Transcribe Medical transcribes the speech from each channel separately\. It combines the separate transcriptions of each channel into a single transcription output\.

Use channel identification to identify the separate channels in your audio and transcribe the speech from each of those channels\. Enable this in situations such as a caller and agent scenario\. Use this to distinguish a caller from an agent in recordings or streams from contact centers that perform drug safety monitoring\.

You can enable channel identification for both batch processing and real\-time streaming\. The following list describes how to enable it for each method\.
+ Batch transcription – AWS Management Console and [StartMedicalTranscriptionJob](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_StartMedicalTranscriptionJob.html) API
+ Streaming transcription – WebSocket streaming and [StartMedicalStreamTranscription](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_streaming_StartMedicalStreamTranscription.html) API

## Transcribing multi\-channel audio files<a name="conversation-channel-id-med-batch"></a>

When you transcribe an audio file, Amazon Transcribe Medical returns a list of *items* for each channel\. An item is a transcribed word or punctuation mark\. Each word has a start time and an end time\. If a person on one channel speaks over a person on a separate channel, the start times and end times of the items for each channel overlap while the individuals are speaking over each other\.

By default, you can transcribe audio files with two channels\. You can request a quota increase if you need to transcribe files that have more than two channels\. For information about requesting a quota increase, see [AWS service quotas](https://docs.aws.amazon.com/general/latest/gr/aws_service_limits.html)\.

To transcribe multi\-channel audio in a batch transcription job, use the AWS Management Console or the [StartMedicalTranscriptionJob](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_StartMedicalTranscriptionJob.html) API\.

### AWS Management Console<a name="channel-id-batch-med-console"></a>

To use the AWS Management Console to enable channel identification in your batch transcription job, you enable audio identification and then channel identification\. Channel identification is a subset of audio identification in the AWS Management Console\.

1. Sign in to the [AWS Management Console](https://console.aws.amazon.com/transcribe/)\.

1. In the navigation pane, under Amazon Transcribe Medical, choose **Transcription jobs**\.

1. Choose **Create job**\.

1. On the **Specify job details** page, provide information about your transcription job\.

1. Choose **Next**\.

1. Enable **Audio identification**\.

1. For **Audio identification type**, choose **Channel identification**\.

1. Choose **Create**\.

### API<a name="channel-id-batch-med-api"></a>

**To transcribe a multi\-channel audio file \(API\)**
+ For the [StartMedicalTranscriptionJob](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_StartMedicalTranscriptionJob.html) API, specify the following\.

  1. For `TranscriptionJobName`, specify a name unique to your AWS account\.

  1. For `LanguageCode`, specify the language code that corresponds to the language spoken in the audio file\. The valid value is `en-US`\.

  1. For the `MediaFileUri` parameter of the `Media` object, specify the name of the media file that you want to transcribe\.

  1. For the `Settings` object, set `ChannelIdentification` to `true`\.

The following is an example request using the AWS SDK for Python \(Boto3\)\.

```
from __future__ import print_function
import time
import boto3
transcribe = boto3.client('transcribe')
job_name = "my-first-transcription-job"
job_uri = "s3://DOC-EXAMPLE-BUCKET/my-audio-file.flac"
transcribe.start_medical_transcription_job(
      MedicalTranscriptionJobName=job_name,
      Media = {'MediaFileUri': job_uri},
      MediaFormat = 'flac',
      LanguageCode = 'en-US',
      OutputBucketName = 's3://DOC-EXAMPLE-BUCKET',
      Specialty = 'PRIMARYCARE',
      Type = 'CONVERSATION',
Settings = {
          'ChannelIdentification': True
          }
  )
while True:
    status = transcribe.get_transcription_job(MedicalTranscriptionJobName=job_name)
    if status['MedicalTranscriptionJob']['TranscriptionJobStatus'] in ['COMPLETED', 'FAILED']:
        break
    print("Not ready yet...")
    time.sleep(5)
print(status)
```

### AWS CLI<a name="channel-id-med-cli"></a>

**To transcribe a multi\-channel audio file using a batch transcription job \(AWS CLI\)**
+ Run the following code\.

  ```
                      
  aws transcribe start-medical-transcription-job \
  –-cli-input-json file://example-start-command.json
  ```

  The following is the code of `example-start-command.json`\.

  ```
  {
      "MedicalTranscriptionJobName": "my-first-med-transcription-job",
      "LanguageCode": "language-code",
      "Specialty": "PRIMARYCARE",
      "Type": "CONVERSATION",
      "OutputBucketName":"s3://DOC-EXAMPLE-BUCKET",
          "Media": {
            "MediaFileUri": "s3://DOC-EXAMPLE-BUCKET/my-audio-file.flac"
          },
          "Settings":{
            "ChannelIdentification": true
          }
  }
  ```

  The following is the response\.

  ```
  {
      "MedicalTranscriptionJob": {
          "MedicalTranscriptionJobName": "my-first-transcription-job",
          "TranscriptionJobStatus": "IN_PROGRESS",
          "LanguageCode": "language-code",
          "Media": {
              "MediaFileUri": "s3://DOC-EXAMPLE-BUCKET/my-audio-file.flac"
          },
          "StartTime": "2020-09-20T23:46:44.081000+00:00",
          "CreationTime": "2020-09-20T23:46:44.053000+00:00",
          "Settings": {
              "ChannelIdentification": true
          },
          "Specialty": "PRIMARYCARE",
          "Type": "CONVERSATION"
      }
  }
  ```

### <a name="med-channel-id-output"></a>

The following code shows the transcription output for an audio file that has a conversation on two channels\.

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

## Transcribing multi\-channel audio streams<a name="conversation-channel-id-med-stream"></a>

You can transcribe audio from separate channels in either HTTP/2 or WebSocket streams using the [StartMedicalStreamTranscription](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_streaming_StartMedicalStreamTranscription.html) API\.

By default, you can transcribe streams with two channels\. You can request a quota increase if you need to transcribe streams that have more than two channels\. For information about requesting a quota increase, see [AWS service quotas](https://docs.aws.amazon.com/general/latest/gr/aws_service_limits.html)\.

### Transcribing multi\-channel audio in an HTTP/2 stream<a name="conversation-channel-id-http2"></a>

To transcribe multi\-channel audio in an HTTP/2 stream, use the [StartMedicalStreamTranscription](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_streaming_StartMedicalStreamTranscription.html) API and specify the following:
+ `LanguageCode` – The language code of the audio\. The valid value is `en-US`\.
+ `MediaEncoding` – The encoding of the audio\. Valid values are `ogg-opus`, `flac`, and `pcm`\.
+ `EnableChannelIdentification` – `true`
+ `NumberOfChannels` – the number of channels in your streaming audio\.

For more information on setting up an HTTP/2 stream to transcribe a medical conversation, see [Streaming request](how-streaming-med.md#streaming-med-request)\.

### Transcribing multi\-channel audio in a WebSocket stream<a name="channel-id-med-websocket"></a>

To identify speakers in WebSocket streams, use the following format to create a pre\-signed URI and start a WebSocket request\. Specify `enable-channel-identification` as `true` and the number of channels in your stream in `number-of-channels`\. A pre\-signed URI contains the information needed to set up bi\-directional communication between your application and Amazon Transcribe Medical\.

```
GET wss://transcribestreaming.us-west-2.amazonaws.com:8443/medical-stream-transcription-websocket
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

Parameter definitions can be found in the [API Reference](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_Reference.html); parameters common to all AWS API operations are listed in the [Common Parameters](https://docs.aws.amazon.com/transcribe/latest/APIReference/CommonParameters.html) section\.

For more information about WebSocket requests, see [Creating a pre\-signed URI](websocket-med.md#websocket-url-med)\.

### Multi\-channel streaming output<a name="streaming-med-output"></a>

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