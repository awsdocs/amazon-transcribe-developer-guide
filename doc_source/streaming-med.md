# Streaming transcription<a name="streaming-med"></a>

Amazon Transcribe Medical streaming transcription enables you to send an audio stream and receive a stream of text in real time\. The API makes it easy for developers to add real\-time speech\-to\-text capability to their applications\.

The following table shows which languages are available for streaming transcription and how you can access them\.


| Language | Sample rate | Available in | 
| --- | --- | --- | 
| US English \(en\-US\) | 16 kHz, 8 kHz | [AWS Management Console](https://console.aws.amazon.com/transcribe/), [https://docs.aws.amazon.com/transcribe/latest/APIReference/API_streaming_StartMedicalStreamTranscription.html](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_streaming_StartMedicalStreamTranscription.html) API, and WebSocket request | 

If you are using HTTP/2, we provide an HTTP/2 streaming client that handles retrying the connection when there are transient problems on the network\. You can use this client as a starting point for your own applications\. To use Amazon Transcribe Medical streaming with the WebSocket protocol, you can create your own client\.

Streaming transcription takes a stream of your audio data and transcribes it in real time\. The transcription is returned to your application in a stream of transcription events\.

Amazon Transcribe Medical breaks your incoming audio stream based on natural speech segments, such as a change in speaker or a pause in the audio\. The transcription is returned progressively to your application, with each response containing more transcribed speech until the entire segment is transcribed\.

In the following example, each line is a partial result transcription output of an audio segment being streamed\. 

```
The
The PE.
The pain.
The patient.
The patient was
The patient was in
The patient was entered.
The patient was entered, and, uh
The patient was I/O.
The patient was I/0 of
The patient was I/0 of some
The patient was I/0 sign.
The patient was I/0 of Sinus.
The patient was I/0 of Sinus rhyth.
The patient was I/0 of Sinus rhythm.
The patient was I/0 of Sinus rhythm with
```

Each [https://docs.aws.amazon.com/transcribe/latest/APIReference/API_streaming_MedicalResult.html](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_streaming_MedicalResult.html) object in the response contains a field called `IsPartial` that indicates whether the response is a partial response containing the transcription results so far or if it is a complete transcription of the audio segment\. 

Each [https://docs.aws.amazon.com/transcribe/latest/APIReference/API_streaming_MedicalResult.html](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_streaming_MedicalResult.html) object also contains the start time and end time of the term from the audio stream so that you can, for example, synchronize the transcription with the video\. 

The following example is a partial transcription response\. 

```
{
    "Transcript": {
        "Results": [
            {
                "Alternatives": [
                    {
                        "Items": [
                            {
                                "Content": "The",
                                "EndTime": 1.07,
                                "StartTime": 1.04,
                                "Type": "pronunciation",
                                "VocabularyFilterMatch": false
                            },
                            {
                                "Content": "patient",
                                "EndTime": 1.5,
                                "StartTime": 1.08,
                                "Type": "pronunciation",
                                "VocabularyFilterMatch": false
                            },
                            {
                                "Content": "was",
                                "EndTime": 1.61,
                                "StartTime": 1.51,
                                "Type": "pronunciation",
                                "VocabularyFilterMatch": false
                            },
                            {
                                "Content": "I/O",
                                "EndTime": 2.25,
                                "StartTime": 2.06,
                                "Type": "pronunciation",
                                "VocabularyFilterMatch": false
                            },
                            {
                                "Content": "of",
                                "EndTime": 2.34,
                                "StartTime": 2.26,
                                "Type": "pronunciation",
                                "VocabularyFilterMatch": false
                            },
                            {
                                "Content": "Sinus",
                                "EndTime": 2.71,
                                "StartTime": 2.35,
                                "Type": "pronunciation",
                                "VocabularyFilterMatch": false
                            },
                            {
                                "Content": "rhythm",
                                "EndTime": 3.07,
                                "StartTime": 2.72,
                                "Type": "pronunciation",
                                "VocabularyFilterMatch": false
                            },
                            {
                                "Content": "with",
                                "EndTime": 3.68,
                                "StartTime": 3.49,
                                "Type": "pronunciation",
                                "VocabularyFilterMatch": false
                            }
                        ],
                        "Transcript": "The patient was I/O of Sinus rhythm with"
                    }
                ],
                "EndTime": 3.75,
                "IsPartial": true,
                "ResultId": "93b1df2b-8702-4c91-892a-ace3b65a6477",
                "StartTime": 1.04
            }
        ]
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
                                "Confidence": 0.99,
                                "Content": "The",
                                "EndTime": 1.12,
                                "StartTime": 1.04,
                                "Type": "pronunciation",
                                "VocabularyFilterMatch": false
                            },
                            {
                                "Confidence": 0.99,
                                "Content": "patient",
                                "EndTime": 1.53,
                                "StartTime": 1.13,
                                "Type": "pronunciation",
                                "VocabularyFilterMatch": false
                            },
                            {
                                "Confidence": 1,
                                "Content": "was",
                                "EndTime": 1.73,
                                "StartTime": 1.54,
                                "Type": "pronunciation",
                                "VocabularyFilterMatch": false
                            },
                            {
                                "Confidence": 1,
                                "Content": "I/O",
                                "EndTime": 2.3,
                                "StartTime": 2.12,
                                "Type": "pronunciation",
                                "VocabularyFilterMatch": false
                            },
                            {
                                "Confidence": 1,
                                "Content": "of",
                                "EndTime": 2.39,
                                "StartTime": 2.31,
                                "Type": "pronunciation",
                                "VocabularyFilterMatch": false
                            },
                            {
                                "Confidence": 1,
                                "Content": "Sinus",
                                "EndTime": 2.82,
                                "StartTime": 2.4,
                                "Type": "pronunciation",
                                "VocabularyFilterMatch": false
                            },
                            {
                                "Confidence": 0.99,
                                "Content": "rhythm",
                                "EndTime": 3.32,
                                "StartTime": 2.83,
                                "Type": "pronunciation",
                                "VocabularyFilterMatch": false
                            },
                            {
                                "Confidence": 0.99,
                                "Content": "with",
                                "EndTime": 3.72,
                                "StartTime": 3.49,
                                "Type": "pronunciation",
                                "VocabularyFilterMatch": false
                            },
                            {
                                "Confidence": 0.99,
                                "Content": "a",
                                "EndTime": 3.78,
                                "StartTime": 3.73,
                                "Type": "pronunciation",
                                "VocabularyFilterMatch": false
                            },
                            {
                                "Confidence": 1,
                                "Content": "heart",
                                "EndTime": 4.02,
                                "StartTime": 3.79,
                                "Type": "pronunciation",
                                "VocabularyFilterMatch": false
                            },
                            {
                                "Confidence": 1,
                                "Content": "rate",
                                "EndTime": 4.19,
                                "StartTime": 4.03,
                                "Type": "pronunciation",
                                "VocabularyFilterMatch": false
                            },
                            {
                                "Confidence": 0.99,
                                "Content": "of",
                                "EndTime": 4.26,
                                "StartTime": 4.2,
                                "Type": "pronunciation",
                                "VocabularyFilterMatch": false
                            },
                            {
                                "Confidence": 1,
                                "Content": "75",
                                "EndTime": 4.81,
                                "StartTime": 4.27,
                                "Type": "pronunciation",
                                "VocabularyFilterMatch": false
                            },
                            {
                                "Confidence": 0.97,
                                "Content": "bpm",
                                "EndTime": 5.47,
                                "StartTime": 4.82,
                                "Type": "pronunciation",
                                "VocabularyFilterMatch": false
                            },
                            {
                                "Content": ".",
                                "EndTime": 5.47,
                                "StartTime": 5.47,
                                "Type": "punctuation",
                                "VocabularyFilterMatch": false
                            }
                        ],
                        "Transcript": "The patient was I/O of Sinus rhythm with a heart rate of 75 bpm."
                    }
                ],
                "EndTime": 5.53,
                "IsPartial": false,
                "ResultId": "93b1df2b-8702-4c91-892a-ace3b65a6477",
                "StartTime": 1.04
            }
        ]
    }
}
```

````

Each word, phrase or punctuation mark in the transcription output is an *item*\. Each word or phrase has a *confidence* score\. The confidence score is a value between `0` and `1` that indicates how confident Amazon Transcribe Medical is that it correctly transcribed the item\. A confidence score with a larger value indicates that Amazon Transcribe Medical is more confident that it transcribed the item correctly\.

The preceding example shows "I/O" in the transcription output, which is an abbreviation for "in and out"\. For more information on how Amazon Transcribe Medical uses abbreviations in the transcription output, see [Transcribing medical terms and measurements](how-measurements-med.md)\.

**Topics**
+ [Event stream encoding](event-stream-med.md)
+ [Using Amazon Transcribe Medical streaming with HTTP/2](how-streaming-med.md)
+ [Establish a bi\-directional connection using the WebSocket protocol](websocket-med.md)