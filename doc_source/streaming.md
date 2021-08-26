# Streaming transcription<a name="streaming"></a>

Use Amazon Transcribe streaming transcription to send an audio stream and receive a stream of text in real time\. You can use this text stream to add real\-time speech\-to\-text capability to your applications\.

Streaming transcription takes a stream of your audio data and transcribes it in real time\. Streaming uses HTTP/2 or WebSocket streams so that the results of the transcription are returned to your application while you send more audio to Amazon Transcribe\. Use streaming transcription when you want to make the results of live audio transcription available immediately, or when you have an audio file that you want to process as it is transcribed\.

For a streaming transcription using:
+ HTTP/2 – Use the [StartStreamTranscription](API_streaming_StartStreamTranscription.md) API to start a stream\. When you use this API, the client handles retrying the connection when there are transient problems on the network\.
+ WebSocket – Create your own client\.
+ [Amazon Transcribe console](https://console.aws.amazon.com/transcribe/) – Speak directly into a computer microphone\. You can use the console as a preview to see how your transcription results are returned to your application when using the API\.

**Note**  
Streaming transcription is not supported in all languages\. See [Supported languages and language\-specific features](how-it-works.md#table-language-matrix) for details\.

You can use Amazon Transcribe streaming transcription for a variety of purposes\. For example:
+ Streaming transcriptions can generate real\-time subtitles for live broadcast media\.
+ Lawyers can make real\-time annotations on top of streaming transcriptions during  depositions\.
+ Video game chat can be transcribed in real time so that hosts can moderate content or run real\-time analysis\.
+ Streaming transcriptions can provide assistance to the hearing impaired\.

Streaming transcription takes a stream of your audio data and transcribes it in real time\. The transcription is returned to your application in a stream of transcription events\. 

Amazon Transcribe breaks up the incoming audio stream based on natural speech segments, such as a change in speaker or a pause in the audio\. The transcription is returned progressively to your application, with each response containing more transcribed speech until the entire segment is transcribed\. 

In the following example, each line is a partial result transcription output of an audio segment that is being streamed\.

```
The
The ad. 
The and
The Amazon. 
The Amazon is 
The Amazon is the
The Amazon is the law.
The Amazon is the lar.
The Amazon is the large
The Amazon is the largest
The Amazon is the largest ray
The Amazon is the largest rain
The Amazon is the largest rain for
The Amazon is the largest rainforest. 
The Amazon is the largest rainforest on the planet
```

Each [Result](https://docs.aws.amazon.com/transcribe/latest/dg/API_streaming_Result.html) object in the response contains a field called `IsPartial`\. The value indicates whether the response is a partial response that contains the transcription results so far, or whether it is a complete transcription of the audio segment\. 

Each [Result](https://docs.aws.amazon.com/transcribe/latest/dg/API_streaming_Result.html) object also contains the start and end time of the transcribed audio segment from the stream\. You can use these values to, for example, synchronize the transcription with the video\. 

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
                              "Content": "The",
                              "EndTime": 0.3799375,
                              "StartTime": 0.0299375,
                              "Type": "pronunciation",
                              "VocabularyFilterMatch": false
                           },
                           { 
                              "Content": "Amazon",
                              "EndTime": 0.5899375,
                              "StartTime": 0.3899375,
                              "Type": "pronunciation",
                              "VocabularyFilterMatch": false
                           },
                           { 
                              "Content": "is",
                              "EndTime": 0.7899375,
                              "StartTime": 0.5999375,
                              "Type": "pronunciation",
                              "VocabularyFilterMatch": false
                           },
                           { 
                              "Content": "the",
                              "EndTime": 0.9199375,
                              "StartTime": 0.7999375,
                              "Type": "pronunciation",
                              "VocabularyFilterMatch": false
                           },
                           { 
                              "Content": "largest",
                              "EndTime": 1.0199375,
                              "StartTime": 0.9299375,
                              "Type": "pronunciation",
                              "VocabularyFilterMatch": false
                           }
                        ],
                        "Transcript": "The Amazon is the largest"
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

The following example shows the transcription results for a fully transcribed speech segment\.

```
{
    "Transcript": {
        "Results": [
            {
                "Alternatives": [
                    {
                        "Items": [
                            {
                                "Confidence": 1,
                                "Content": "The",
                                "EndTime": 2.58,
                                "StartTime": 2.33,
                                "Type": "pronunciation",
                                "VocabularyFilterMatch": false
                            },
                            {
                                "Confidence": 1,
                                "Content": "Amazon",
                                "EndTime": 3.12,
                                "StartTime": 2.59,
                                "Type": "pronunciation",
                                "VocabularyFilterMatch": false
                            },
                            {
                                "Confidence": 1,
                                "Content": "is",
                                "EndTime": 3.25,
                                "StartTime": 3.13,
                                "Type": "pronunciation",
                                "VocabularyFilterMatch": false
                            },
                            {
                                "Confidence": 1,
                                "Content": "the",
                                "EndTime": 3.39,
                                "StartTime": 3.26,
                                "Type": "pronunciation",
                                "VocabularyFilterMatch": false
                            },
                            {
                                "Confidence": 1,
                                "Content": "largest",
                                "EndTime": 3.93,
                                "StartTime": 3.4,
                                "Type": "pronunciation",
                                "VocabularyFilterMatch": false
                            },
                            {
                                "Confidence": 0.99,
                                "Content": "rainforest",
                                "EndTime": 4.8,
                                "StartTime": 3.95,
                                "Type": "pronunciation",
                                "VocabularyFilterMatch": false
                            },
                            {
                                "Confidence": 1,
                                "Content": "on",
                                "EndTime": 5.01,
                                "StartTime": 4.82,
                                "Type": "pronunciation",
                                "VocabularyFilterMatch": false
                            },
                            {
                                "Confidence": 1,
                                "Content": "the",
                                "EndTime": 5.11,
                                "StartTime": 5.02,
                                "Type": "pronunciation",
                                "VocabularyFilterMatch": false
                            },
                            {
                                "Confidence": 1,
                                "Content": "planet",
                                "EndTime": 5.64,
                                "StartTime": 5.12,
                                "Type": "pronunciation",
                                "VocabularyFilterMatch": false
                            },
                            {
                                "Confidence": 0.89,
                                "Content": "covering",
                                "EndTime": 6.24,
                                "StartTime": 5.72,
                                "Type": "pronunciation",
                                "VocabularyFilterMatch": false
                            },
                            {
                                "Confidence": 1,
                                "Content": "over",
                                "EndTime": 6.46,
                                "StartTime": 6.25,
                                "Type": "pronunciation",
                                "VocabularyFilterMatch": false
                            },
                            {
                                "Confidence": 1,
                                "Content": "seven",
                                "EndTime": 6.82,
                                "StartTime": 6.47,
                                "Type": "pronunciation",
                                "VocabularyFilterMatch": false
                            },
                            {
                                "Confidence": 1,
                                "Content": "million",
                                "EndTime": 7.15,
                                "StartTime": 6.83,
                                "Type": "pronunciation",
                                "VocabularyFilterMatch": false
                            },
                            {
                                "Confidence": 1,
                                "Content": "kilometers",
                                "EndTime": 7.92,
                                "StartTime": 7.16,
                                "Type": "pronunciation",
                                "VocabularyFilterMatch": false
                            },
                            {
                                "Content": ".",
                                "EndTime": 7.92,
                                "StartTime": 7.92,
                                "Type": "punctuation",
                                "VocabularyFilterMatch": false
                            }
                        ],
                        "Transcript": "The Amazon is the largest rainforest on the planet covering over seven million kilometers."
                    }
                ],
                "EndTime": 7.92,
                "IsPartial": false,
                "ResultId": "a37114fa-5288-438d-afdf-833cfd1ea55c",
                "StartTime": 2.33
            }
        ]
    }
}
```

Each word, phrase, or punctuation mark in the transcription output is an *item*\. Each word or phrase has a *confidence* score\. The confidence score is a value between `0` and `1` that indicates how confident Amazon Transcribe is that it correctly transcribed the item\. A confidence score with a larger value indicates that Amazon Transcribe is more confident that it transcribed the item correctly\.

**Topics**
+ [Event stream encoding](event-stream.md)
+ [Using Amazon Transcribe streaming with WebSockets](websocket.md)
+ [Using Amazon Transcribe streaming With HTTP/2](how-streaming.md)
+ [Partial result stabilization](result-stabilization.md)