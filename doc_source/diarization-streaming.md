# Identifying speakers in real\-time streams<a name="diarization-streaming"></a>

You can identify different speakers in either HTTP/2 or Websocket streams\. Speaker diarization works best for identifying between two and five speakers\. Although Amazon Transcribe can identify more than five speakers in a stream, the accuracy of speaker diarization decreases if you exceed that number\. To start an HTTP/2 stream, you specify the `ShowSpeakerLabel` request parameter of the [StartStreamTranscription](API_streaming_StartStreamTranscription.md) operation\. To start a Websocket request, you use a pre\-signed URL, a URL that contains the information needed to start your stream\. To use the console to transcribe speech spoken into your microphone, use the following procedure\.

You can identify speakers in real\-time streams that are in US English \(en\-US\)\.

**To identify speakers in audio that is spoken into your microphone \(console\)**

You can use the Amazon Transcribe console to start a real\-time stream and transcribe any speech picked up by your microphone\.

1. Sign into the AWS Management Console and open the Amazon Transcribe console at [Amazon Transcribe console](https://console.aws.amazon.com/transcribe/)\.

1. In the navigation pane, choose **Real\-time transcription**\.

1. In **Language**, choose the language of your real\-time stream\.

1. Under **Additional settings**, enable **Speaker identification**\.

1. Choose **Start streaming**\.

1. Speak into the microphone\.

## HTTP/2 streaming<a name="diarization-http2"></a>

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

To identify speakers in an HTTP/2 stream, use the [StartStreamTranscription](API_streaming_StartStreamTranscription.md) operation and specify the following:
+ `LanguageCode` – the language code that corresponds to the language spoken in the stream\.
+ `MediaSampleHertz` – the sample rate of the audio\.
+ `ShowSpeakerLabel` – `true`\.

## WebSocket streaming<a name="diarization-websocket"></a>

To identify speakers in WebSocket streams, use the following format to create a pre\-signed URL to start a WebSocket request and specify `show-speaker-label` as `true`\. A pre\-signed URL contains the information to set up bi\-directional communication between your application and Amazon Transcribe\.

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

For more information on completing WebSocket requests, see [Creating a pre\-signed URL](websocket.md#websocket-url)\.

## Streaming transcription output<a name="diarization-output"></a>

The following code shows the truncated example response of a streaming request\.

```
{
  "Transcript": {
    "Results": [
      {
        "Alternatives": [
          {
            "Items": [
              {
                "Confidence": 0.97,
                "Content": "From",
                "EndTime": 18.98,
                "Speaker": "0",
                "StartTime": 18.74,
                "Type": "pronunciation",
                "VocabularyFilterMatch": false
              },
              {
                "Confidence": 1,
                "Content": "the",
                "EndTime": 19.31,
                "Speaker": "0",
                "StartTime": 19,
                "Type": "pronunciation",
                "VocabularyFilterMatch": false
              },
              {
                "Confidence": 1,
                "Content": "last",
                "EndTime": 19.86,
                "Speaker": "0",
                "StartTime": 19.32,
                "Type": "pronunciation",
                "VocabularyFilterMatch": false
              },
             ...
              {
                "Confidence": 1,
                "Content": "chronic",
                "EndTime": 22.55,
                "Speaker": "0",
                "StartTime": 21.97,
                "Type": "pronunciation",
                "VocabularyFilterMatch": false
              },
              ...
                "Confidence": 1,
                "Content": "fatigue",
                "EndTime": 24.42,
                "Speaker": "0",
                "StartTime": 23.95,
                "Type": "pronunciation",
                "VocabularyFilterMatch": false
              },
              {
                "EndTime": 25.22,
                "StartTime": 25.22,
                "Type": "speaker-change",
                "VocabularyFilterMatch": false
              },
              {
                "Confidence": 0.99,
                "Content": "True",
                "EndTime": 25.63,
                "Speaker": "1",
                "StartTime": 25.22,
                "Type": "pronunciation",
                "VocabularyFilterMatch": false
              },
              {
                "Content": ".",
                "EndTime": 25.63,
                "StartTime": 25.63,
                "Type": "punctuation",
                "VocabularyFilterMatch": false
              }
            ],
            "Transcript": "From the last note she still has mild sleep deprivation and chronic fatigue True."
          }
        ],
        "EndTime": 25.63,
        "IsPartial": false,
        "ResultId": "XXXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXX",
        "StartTime": 18.74
      }
    ]
  }
}
```

Amazon Transcribe breaks your incoming audio stream based on natural speech segments, such as a change in speaker or a pause in the audio\. The transcription is returned progressively to your application, with each response containing more transcribed speech until the entire segment is transcribed\. The above code is a truncated example of a fully\-transcribed speech segment\. Speaker labels only appear for entirely transcribed segments\. 

The following list shows the organization of the objects and parameters in a streaming transcription output\.

**`Transcript`**  
Each speech segment has its own `Transcript` object\.

**`Results`**  
Each `Transcript` object has its own `Results` object\. This object contains the `isPartial` field\. When its value is `false`, the results returned are for an entire speech segment\.

**`Alternatives`**  
Each `Results` object has an `Alternatives` object\.

**`Items`**  
Each `Alternatives` object has its own `Items` object that contains information about each word and punctuation mark in the transcription output\. When you enable speaker identification, each word has a `Speaker` label for fully\-transcribed speech segments\. Amazon Transcribe uses this label to assign a unique integer to each speaker it identifies in the stream\. The `Type` parameter having a value of `speaker-change` indicates that one person has stopped speaking and that another person is about to begin\.

**`Transcript`**  
Each `Items` object contains a transcribed speech segment as the value of the `Transcript` field\.