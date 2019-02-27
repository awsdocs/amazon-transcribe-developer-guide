# Using Amazon Transcribe Streaming<a name="how-streaming"></a>

Streaming transcription takes a stream of your audio data and transcribes it in real time\. The transcription is returned to your application in a stream of transcription events\. 

To start transcribing streaming audio, use the [StartStreamTranscription](https://docs.aws.amazon.com/transcribe/latest/dg/API_streaming_StartStreamTranscription.html) operation\. You can transcribe up to four hours of streaming audio\. 

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

The following example is a partial transcription response from the [StartStreamTranscription](https://docs.aws.amazon.com/transcribe/latest/dg/API_streaming_StartStreamTranscription.html) operation\. 

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