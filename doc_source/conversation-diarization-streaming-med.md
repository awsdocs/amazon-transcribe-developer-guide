# Enabling speaker partitioning in real\-time streams<a name="conversation-diarization-streaming-med"></a>

To partition speakers and label their speech in a real\-time stream, use the AWS Management Console or a streaming request\. Speaker partitioning works best for between two and five speakers in a stream\. Although Amazon Transcribe Medical can partition more than five speakers in a stream, the accuracy of the partitions decrease if you exceed that number\.

To start an HTTP/2 request, use the [https://docs.aws.amazon.com/transcribe/latest/APIReference/API_streaming_StartMedicalStreamTranscription.html](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_streaming_StartMedicalStreamTranscription.html) API\. To start a WebSocket request, use a pre\-signed URI\. The URI contains the information required to set up bi\-directional communication between your application and Amazon Transcribe Medical\.

## Enabling speaker partitioning in audio that is spoken into your microphone \(AWS Management Console\)<a name="conversation-diarization-console"></a>

You can use the AWS Management Console to start a real\-time stream of a clinician\-patient conversation, or a dictation that is spoken into your microphone in real\-time\.

1. Sign in to the [AWS Management Console](https://console.aws.amazon.com/transcribe/)\.

1. In the navigation pane, for Amazon Transcribe Medical choose **Real\-time transcription**\.

1. For **Audio input type**, choose the type of medical speech that you want to transcribe\.

1. For **Additional settings**, choose **Speaker partitioning**\.

1. Choose **Start streaming** to start transcribing your real\-time audio\.

1. Speak into the microphone\.

## Enabling speaker partitioning in an HTTP/2 stream<a name="conversation-diarization-med-http2"></a>

To enable speaker partitioning in an HTTP/2 stream of a medical conversation, use the [https://docs.aws.amazon.com/transcribe/latest/APIReference/API_streaming_StartMedicalStreamTranscription.html](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_streaming_StartMedicalStreamTranscription.html) API and specify the following: 
+ For `LanguageCode`, specify the language code that corresponds to the language in the stream\. The valid value is `en-US`\.
+ For `MediaSampleHertz`, specify the sample rate of the audio\.
+ For `Specialty`, specify the medical specialty of the provider\.
+ `ShowSpeakerLabel` – `true`

For more information on setting up an HTTP/2 stream to transcribe a medical conversation, see [Setting up an HTTP/2 stream](streaming-http2.md)\.

## Enabling speaker partitioning in a WebSocket request<a name="conversation-diarization-med-websocket"></a>

To partition speakers in WebSocket streams with the API, use the following format to create a pre\-signed URI to start a WebSocket request and set `show-speaker-label` to `true`\. 

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
&specialty=medicalSpecialty
&type=CONVERSATION
&vocabulary-name=vocabularyName
&show-speaker-label=boolean
```

## <a name="conversation-diarization-med-streaming-output"></a>

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

Amazon Transcribe Medical breaks your incoming audio stream based on natural speech segments, such as a change in speaker or a pause in the audio\. The transcription is returned progressively to your application, with each response containing more transcribed speech until the entire segment is transcribed\. The preceding code is a truncated example of a fully\-transcribed speech segment\. Speaker labels only appear for entirely transcribed segments\. 

The following list shows the organization of the objects and parameters in a streaming transcription output\.

**`Transcript`**  
Each speech segment has its own `Transcript` object\.

**`Results`**  
Each `Transcript` object has its own `Results` object\. This object contains the `isPartial` field\. When its value is `false`, the results returned are for an entire speech segment\.

**`Alternatives`**  
Each `Results` object has an `Alternatives` object\.

**`Items`**  
Each `Alternatives` object has its own `Items` object that contains information about each word and punctuation mark in the transcription output\. When you enable speaker partitioning, each word has a `Speaker` label for fully\-transcribed speech segments\. Amazon Transcribe Medical uses this label to assign a unique integer to each speaker in the stream\. The `Type` parameter having a value of `speaker-change` indicates that one person has stopped speaking and that another person is about to begin\.

**`Transcript`**  
Each Items object contains a transcribed speech segment as the value of the `Transcript` field\.

For more information about WebSocket requests, see [Setting up a WebSocket stream](streaming-websocket.md)\.