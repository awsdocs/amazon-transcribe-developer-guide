# Channel identification<a name="channel-id"></a>

If you have an audio file or stream that has multiple channels, you can use *channel identification* to transcribe the speech from each of those channels\. Amazon Transcribe identifies the speech from each channel and transcribes that speech in separate transcriptions\. It combines those transcriptions into a single transcription output\.

 You can enable channel identification for both batch processing and real\-time streaming\. The following list describes how to enable it for each method\.
+ Batch transcription \- [Amazon Transcribe console](https://console.aws.amazon.com/transcribe/) and [ StartTranscriptionJob ](API_StartTranscriptionJob.md) API
+ Streaming transcription \- WebSocket streaming and [ StartStreamTranscription ](API_streaming_StartStreamTranscription.md) API

## Transcribing multi\-channel audio files<a name="channel-id-batch"></a>

To transcribe multi\-channel audio in a batch transcription job, use the [Amazon Transcribe console](https://console.aws.amazon.com/transcribe/) or the [ StartTranscriptionJob ](API_StartTranscriptionJob.md) API\.

### Console<a name="channel-id-batch-console"></a>

To use the console to enable channel identification in your batch transcription job, you enable audio identification and then channel identification\. Channel identification is a subset of audio identification in the console\.

**To transcribe a multi\-channel audio file \(console\)**

1. Sign in to the [Amazon Transcribe console](https://console.aws.amazon.com/transcribe/)\.

1. In the navigation pane, under Amazon Transcribe, choose **Transcription jobs**\.

1. Choose **Create job**\.

1. On the **Specify job details** page, provide information about your transcription job\.

1. Choose **Next**\.

1. Enable **Audio identification**\.

1. For **Audio identification type**, choose **Channel identification**\.

1. Choose **Create**\.

### API<a name="channel-id-batch-api"></a>

**To transcribe a multi\-channel audio file \(API\)**
+ For the [ StartTranscriptionJob ](API_StartTranscriptionJob.md) API, specify the following\.

  1. For `TranscriptionJobName`, specify a name unique to your AWS account\.

  1. For `LanguageCode`, specify the language code that corresponds to the language spoken in your media file\. For available languages and corresponding language codes, see [What is Amazon Transcribe?](transcribe-whatis.md)\. 

  1. For the `MediaFileUri` parameter of the `Media` object, specify the name of the media file you want to transcribe\.

  1. For the `Settings` object, set `ChannelIdentification` to `true`\.

The following is an example request using the AWS SDK for Python \(Boto3\)\.

```
  from __future__ import print_function
  import time
  import boto3
  transcribe = boto3.client('transcribe')
  job_name = "your-transcription-job-name"
  job_uri = "the-Amazon-S3-object-URL-of-your-media-file"
  transcribe.start_transcription_job(
      TranscriptionJobName=job_name,
      Media= {'MediaFileUri': job_uri},
      MediaFormat= 'mp4',
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

**To transcribe a multi\-channel audio file using a batch transcription job \(AWS CLI\)**
+ Run the following code\.

  ```
                      
  aws transcribe start-transcription-job \
  --cli-input-json file://example-start-command.json
  ```

  The following is the code of `example-start-command.json`\.

  ```
    {
      "TranscriptionJobName": "your-transcription-job-name",
      "LanguageCode": "en-US",
      "Media": {
          "MediaFileUri": "s3://DOC-EXAMPLE-BUCKET/your-audio-file.mp4"
      },
      "Settings":{
    "ChannelIdentification":true
    }
  ```

  ```
    {
      "TranscriptionJobName": "your-transcription-job-name",
      "LanguageCode": "en-US",
      "Media": {
          "MediaFileUri": "s3://DOC-EXAMPLE-BUCKET/your-audio-file"
      },
      "Settings":{
    "ChannelIdentification":true
    }
  ```

  The following is the response\.

  ```
  {
      "TranscriptionJob": {
          "TranscriptionJobName": "your-transcription-job",
          "TranscriptionJobStatus": "IN_PROGRESS",
          "LanguageCode": "en-US",
          "Media": {
              "MediaFileUri": "s3://DOC-EXAMPLE-BUCKET/your-audio-file"
          },
          "StartTime": "2020-09-12T23:20:28.239000+00:00",
          "CreationTime": "2020-09-12T23:20:28.203000+00:00",
          "Settings": {
              "ChannelIdentification": true
          }
      }
  }
  ```

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

Amazon Transcribe transcribes the audio from each channel separately and combines the transcribed text from each channel into a single transcription output\.

For each channel in the transcription output, Amazon Transcribe returns a list of *items*\. An item is a transcribed word, pause, or punctuation mark\. Each item has a start time and an end time\. If a person on one channel speaks over a person on a separate channel, the start times and end times of the items for each channel overlap while the individuals are speaking over each other\.

By default, you can transcribe audio files with two channels\. You can request a quota increase if you need to transcribe files that have more than two channels\. For information about requesting a quota increase, see [AWS service quotas](https://docs.aws.amazon.com/general/latest/gr/aws_service_limits.html)\.

## Transcribing multi\-channel audio streams<a name="channel-id-stream"></a>

You can transcribe audio from separate channels in either HTTP/2 or WebSocket streams using the [ StartStreamTranscription ](API_streaming_StartStreamTranscription.md) API\.

By default, you can transcribe streams with two channels\. You can request a quota increase if you need to transcribe streams that have more than two channels\. For information about requesting a quota increase, see [AWS service quotas](https://docs.aws.amazon.com/general/latest/gr/aws_service_limits.html)\.

### Transcribing multi\-channel audio in an HTTP/2 stream<a name="channel-id-http2"></a>

To transcribe multi\-channel audio in an HTTP/2 stream, use the [ StartStreamTranscription ](API_streaming_StartStreamTranscription.md) API and specify the following:
+ `LanguageCode` \- The language code of the audio\.
+ `MediaEncoding` \- The encoding of the audio\.
+ `EnableChannelIdentification` \- `true`
+ `NumberOfChannels` \- The number of channels in your streaming audio\.

The following is the syntax for the parameters of an HTTP/2 request\.

```
    POST /stream-transcription HTTP/2
    x-amzn-transcribe-language-code: LanguageCode
    x-amzn-transcribe-sample-rate: MediaSampleRateHertz
    x-amzn-transcribe-media-encoding: MediaEncoding
    x-amzn-transcribe-session-id: SessionId
    x-amzn-transcribe-vocabulary-filter-name: VocabularyFilterName
    x-amzn-transcribe-vocabulary-filter-method: VocabularyFilterMethod
    x-amzn-transcribe-enable-channel-identification: EnableChannelIdentification
    x-amzn-transcribe-number-of-channels: NumberOfChannels
    Content-type: application/json
    
    {
       "AudioStream": { 
          "AudioEvent": { 
             "AudioChunk": blob
          }
       }
    }
```

### Transcribing multi\-channel audio in a WebSocket stream<a name="channel-id-websocket"></a>

To identify speakers in WebSocket streams, use the following format to create a pre\-signed URL and start a WebSocket request\. Specify `enable-channel-id` as `true` and the number of channels in your stream in `number-of-channels`\. A pre\-signed URL contains the information needed to set up bi\-directional communication between your application and Amazon Transcribe\.

```
GET wss://transcribestreaming.region.amazonaws.com:8443/stream-transcription-websocket
?language-code=languageCode
    &X-Amz-Algorithm=AWS4-HMAC-SHA256
    &X-Amz-Credential=Signature Version 4 credential scope
    &X-Amz-Date=date
    &X-Amz-Expires=time in seconds until expiration
    &X-Amz-Security-Token=security-token
    &X-Amz-Signature=Signature Version 4 signature
    &X-Amz-SignedHeaders=host
    &media-encoding=mediaEncoding
    &sample-rate=mediaSampleRateHertz
    &session-id=sessionId
    &enable-channel-identification=true
    &number-of-channels=number of channels in your audio stream
```

For more information about WebSocket requests, see [Creating a pre\-signed URL](websocket.md#websocket-url)\.

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