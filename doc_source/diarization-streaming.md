# Identifying Speakers in Real\-time Streams<a name="diarization-streaming"></a>

You can identify different speakers in either HTTP/2 or Websocket streams\. Speaker identification works best for identifying between two and five speakers\. Although Amazon Transcribe can identify more than five speakers in a stream, the accuracy of speaker identification decreases if you exceed that number\. To start an HTTP/2 stream, you specify the `ShowSpeakerLabel` request parameter of the [StartStreamTranscription](API_streaming_StartStreamTranscription.md) operation\. To start a Websocket request, you use a pre\-signed URL, a URL that contains the information needed to start your stream\. To use the console to transcribe speech spoken into your microphone, use the following procedure\.

**To identify speakers in audio that is spoken into your microphone \(console\)**

You can use the Amazon Transcribe console to start a real\-time stream and transcribe any speech picked up by your microphone\.

1. Sign into the AWS Management Console and open the Amazon Transcribe console at [Amazon Transcribe console](https://console.aws.amazon.com/transcribe/)\.

1. In the navigation pane, choose **Real\-time transcription**\.

1. In **Language**, choose the language of your real\-time stream\.

1. Under **Additional settings**, enable **Speaker identification**\.

1. Choose **Start streaming**\.

1. Speak into the microphone\.

## HTTP/2 Streaming<a name="diarization-http2"></a>

The following is the syntax for the parameters of an HTTP/2 request\.

```
    POST /stream-transcription HTTP/2
    x-amzn-transcribe-language-code: LanguageCode
    x-amzn-transcribe-sample-rate: MediaSampleRateHertz
    x-amzn-transcribe-media-encoding: MediaEncoding
    x-amzn-transcribe-session-id: SessionId
    x-amzn-transcribe-vocabulary-filter-name: VocabularyFilterName
    x-amzn-transcribe-vocabulary-filter-method: VocabularyFilterMethod
    x-amzn-transcribe-show-speaker-label: ShowSpeakerLabel
    Content-type: application/json
    
    {
       "AudioStream": { 
          "AudioEvent": { 
             "AudioChunk": blob
          }
       }
    }
```

To identify speakers in an HTTP/2 stream, use the [StartStreamTranscription](API_streaming_StartStreamTranscription.md) and specify the following:
+ For `LanguageCode`, specify the language code that corresponds to the language spoken in your audio file\.
+ For `MediaSampleHertz`, specify the sample rate of the audio\.
+ `ShowSpeakerLabel` – `true`\.

## Websocket Streaming<a name="diarization-websocket"></a>

To identify speakers in Websocket streams, use the following format to create a pre\-signed URL to start a Websocket request and specify `show-speaker-label` as `true`\. A pre\-signed URL contains the information to set up bi\-directional communication between your application and Amazon Transcribe\.

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
    &show-speaker-label=true
```

For more information on completing Websocket requests, see [Creating a Pre\-Signed URL](websocket.md#websocket-url)\.