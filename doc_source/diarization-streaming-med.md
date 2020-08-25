# Identifying Speakers in Real\-time Streams<a name="diarization-streaming-med"></a>

To identify speakers in a real\-time stream, use the Amazon Transcribe Medical console or the WebSocket streaming request\. Speaker identification works best for identifying between two and five speakers in a stream\. Although Amazon Transcribe Medical can identify more than five speakers in a stream, the accuracy of speaker identification decreases if you exceed that number\. To start a WebSocket request, you use a pre\-signed URL\. The URL contains the information required to set up bi\-directional communication between your application and Amazon Transcribe Medical\. 

## <a name="diarization-med-websocket"></a>

**To identify speakers in audio that is spoken into your microphone \(console\)**

You can use the Amazon Transcribe Medical console to start a real\-time stream of a clinician\-patient conversation, or a dictation that is spoken into your microphone in real\-time\.

1. Sign into the AWS Management Console and open the Amazon Transcribe Medical console at [Amazon Transcribe Medical console](https://console.aws.amazon.com/transcribe/)\.

1. In the navigation pane, for Amazon Transcribe Medical choose **Real\-time transcription**\.

1. For **Audio input type**, choose the type of medical speech that you want to transcribe\.

1. For **Additional settings**, choose **Speaker identification**\.

1. Choose **Start streaming** to start transcribing your real\-time audio\.

1. Speak into the microphone\.

To identify speakers in WebSocket streams with the API, use the following format to create a pre\-signed URL to start a WebSocket request and set `show-speaker-label` to `true`\. 

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

For more information about WebSocket requests, see [Creating a Pre\-Signed URL](websocket-med.md#websocket-url-med)\.