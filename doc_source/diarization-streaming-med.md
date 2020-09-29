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

Amazon Transcribe Medical breaks your incoming audio stream based on natural speech segments, such as a change in speaker or a pause in the audio\. The transcription is returned progressively to your application, with each response containing more transcribed speech until the entire segment is transcribed\. The above code is a truncated example of a fully\-transcribed speech segment\. Speaker labels only appear for entirely transcribed segments\. 

The following list shows the organization of the objects and parameters in a streaming transcription output\.

**`Transcript`**  
Each speech segment has its own `Transcript` object\.

**`Results`**  
Each `Transcript` object has its own `Results` object\. This object contains the `isPartial` field\. When its value is `false`, the results returned are for an entire speech segment\.

**`Alternatives`**  
Each `Results` object has an `Alternatives` object\.

**`Items`**  
Each `Alternatives` object has its own `Items` object that contains information about each word and punctuation mark in the transcription output\. When you enable speaker identification, each word has a `Speaker` label for fully\-transcribed speech segments\. Amazon Transcribe Medical uses this label to assign a unique integer to each speaker it identifies in the stream\. The `Type` parameter having a value of `speaker-change` indicates that one person has stopped speaking and that another person is about to begin\.

**`Transcript`**  
Each Items object contains a transcribed speech segment as the value of the `Transcript` field\.

For more information about WebSocket requests, see [Creating a Pre\-Signed URL](websocket-med.md#websocket-url-med)\.