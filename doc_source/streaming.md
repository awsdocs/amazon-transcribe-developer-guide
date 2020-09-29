# Streaming Transcription<a name="streaming"></a>

Amazon Transcribe streaming transcription enables you to send an audio stream and receive a stream of text in real time\. The API makes it easy for developers to add real\-time speech\-to\-text capability to their applications\.

The following table shows which languages are available for streaming transcription and how you can access them\.


| Language | Sample Rate | Available In | 
| --- | --- | --- | 
| US English \(en\-US\) | 16 kHz, 8 kHz | [Amazon Transcribe console](https://console.aws.amazon.com/transcribe/), [StartStreamTranscription](API_streaming_StartStreamTranscription.md) operation, and WebSocket request | 
| US Spanish \(es\-US\) | 16 kHz, 8 kHz | [Amazon Transcribe console](https://console.aws.amazon.com/transcribe/), [StartStreamTranscription](API_streaming_StartStreamTranscription.md) operation, and WebSocket request | 
| Australian English \(en\-AU\) | 8 kHz | [StartStreamTranscription](API_streaming_StartStreamTranscription.md) operation and WebSocket request | 
| British English \(en\-GB\) | 8 kHz | [StartStreamTranscription](API_streaming_StartStreamTranscription.md) operation and WebSocket request | 
| French \(fr\-FR\) | 8 kHz | [StartStreamTranscription](API_streaming_StartStreamTranscription.md) operation and WebSocket request | 
| Canadian French \(fr\-CA\) | 8 kHz | [StartStreamTranscription](API_streaming_StartStreamTranscription.md) operation and WebSocket request | 

Amazon Transcribe streaming transcription can be used for a variety of purposes\. For example:
+ Streaming transcriptions can generate real\-time subtitles for live broadcast media\.
+ Lawyers can make real\-time annotations on top of streaming transcriptions during courtroom depositions\.
+ Video game chat can be transcribed in real time so that hosts can moderate content or run real\-time analysis\.
+ Streaming transcriptions can provide assistance to the hearing impaired\.

If you are using HTTP/2, we provide an HTTP/2 streaming client that handles retrying the connection when there are transient problems on the network\. You can use this client as a starting point for your own applications\. To use Amazon Transcribe streaming with the WebSocket protocol, you can create your own client\.

Streaming transcription takes a stream of your audio data and transcribes it in real time\. The transcription is returned to your application in a stream of transcription events\. 

Amazon Transcribe breaks your incoming audio stream based on natural speech segments, such as a change in speaker or a pause in the audio\. The transcription is returned progressively to your application, with each response containing more transcribed speech until the entire segment is transcribed\. 

In the following example, each line is a partial result transcription output of an audio segment being streamed: 

```
the amazon is the largest 
the amazon is the largest 
the amazon is the largest 
the amazon is the largest rainforest 
the amazon is the largest rainforest 
the amazon is the largest rainforest
the amazon is the largest rainforest on the 
the amazon is the largest rainforest on the 
the amazon is the largest rainforest on the planet 
the amazon is the largest rainforest on the planet 
the amazon is the largest rainforest on the planet 
the amazon is the largest rainforest on the planet 
the amazon is the largest rainforest on the planet covering over 
the amazon is the largest rainforest on the planet covering over 
the amazon is the largest rainforest on the planet covering over two million
```

Each [Result](https://docs.aws.amazon.com/transcribe/latest/dg/API_streaming_Result.html) object in the response contains a field called `IsPartial` that indicates whether the response is a partial response containing the transcription results so far or if it is a complete transcription of the audio segment\. 

Each [Result](https://docs.aws.amazon.com/transcribe/latest/dg/API_streaming_Result.html) object also contains the start time and end time of the term from the audio stream so that you can, for example, synchronize the transcription with the video\. 

The following example is a partial transcription response\. 

```
{
   "TranscriptResultStream": { 
      "TranscriptEvent": { 
         "Transcript": { 
            "Results": [ 
               { 
                  "Alternatives": [ 
                     { 
                        "Items": [ 
                           { 
                              "Content": "the",
                              "EndTime": 0.3799375,
                              "StartTime": 0.0299375,
                              "Type": "pronunciation"
                           },
                           { 
                              "Content": "amazon",
                              "EndTime": 0.5899375,
                              "StartTime": 0.3899375,
                              "Type": "pronunciation"
                           },
                           { 
                              "Content": "is",
                              "EndTime": 0.7899375,
                              "StartTime": 0.5999375,
                              "Type": "pronunciation"
                           },
                           { 
                              "Content": "the",
                              "EndTime": 0.9199375,
                              "StartTime": 0.7999375,
                              "Type": "pronunciation"
                           },
                           { 
                              "Content": "largest",
                              "EndTime": 1.0199375,
                              "StartTime": 0.9299375,
                              "Type": "pronunciation"
                           }
                        ],
                        "Transcript": "the amazon is the largest"
                     }
                  ],
                  "EndTime": 1.02,
                  "IsPartial": true,
                  "ResultId": "2db76dc8-d728-11e8-9f8b-f2801f1b9fd1",
                  "StartTime": 0.0199375
               }
            ]
         }
      }
   }
}
```

**Topics**
+ [Event Stream Encoding](event-stream.md)
+ [Using Amazon Transcribe Streaming with WebSockets](websocket.md)
+ [Using Amazon Transcribe Streaming With HTTP/2](how-streaming.md)