# Post\-call analytics with real\-time transcriptions<a name="tca-post-call"></a>

Post\-call analytics is an optional feature available with real\-time Call Analytics transcriptions\. In addition to the standard [real\-time analytics insights](call-analytics-streaming.md#call-analytics-insights-streaming), post\-call analytics provides you with the following:
+ **Action items**: Lists any action items identified in the call
+ **Interruptions**: Measures if and when one participant cuts off the other participant midsentence
+ **Issues**: Provides the issues identified in the call
+ **Loudness**: Measures the volume at which each participant is speaking
+ **Non\-talk time**: Measures periods of time that do not contain speech
+ **Outcomes**: Provides the outcome, or resolution, identified in the call
+ **Talk speed**: Measures the speed at which both participants are speaking
+ **Talk time**: Measures the amount of time \(in milliseconds\) each participant spoke during the call

When enabled, post\-call analytics from an audio stream produces a transcript similar to a [post\-call analytics from an audio file](call-analytics-batch.md) and stores it in the Amazon S3 bucket specified in `OutputLocation`\. Additionally, post\-call analytics records your audio stream and saves it as an audio file \(`WAV` format\) in the same Amazon S3 bucket\. If you enable redaction, a redacted transcript and a redacted audio file are also stored in the specified Amazon S3 bucket\. Enabling post\-call analytics with your audio stream produces between two and four files, as described here:
+ If redaction is **not** enabled, your output files are:

  1. An unredacted transcript

  1. An unredacted audio file
+ If redaction is enabled **without** the unredacted option \(`redacted`\), your output files are:

  1. A redacted transcript

  1. A redacted audio file
+ If redaction is enabled **with** the unredacted option \(`redacted_and_unredacted`\), your output files are:

  1. A redacted transcript

  1. A redacted audio file

  1. An unredacted transcript

  1. An unredacted audio file

Note that if you enable post\-call analytics \([https://docs.aws.amazon.com/transcribe/latest/APIReference/API_streaming_PostCallAnalyticsSettings.html](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_streaming_PostCallAnalyticsSettings.html)\) with your request, and you're using `FLAC` or `OPUS-OGG` media, you **do not** get `loudnessScore` in your transcript and no audio recordings of your stream are created\.

For more information on the insights available with post\-call analytics for audio streams, refer to the [post\-call analytics insights](call-analytics-batch.md#call-analytics-insights-batch) section\.

**Tip**  
If you enable post\-call analytics with your real\-time Call Analytics request, all of your `POST_CALL` and `REAL-TIME` categories are applied to your post\-call analytics transcription\.

## Enabling post\-call analytics<a name="tca-post-call-enable"></a>

To enable post\-call analytics, you must include the [https://docs.aws.amazon.com/transcribe/latest/APIReference/API_streaming_PostCallAnalyticsSettings.html](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_streaming_PostCallAnalyticsSettings.html) parameter in your real\-time Call Analytics request\. The following parameters must be included when `PostCallAnalyticsSettings` is enabled:
+ `OutputLocation`: The Amazon S3 bucket where you want your post\-call transcript stored\.
+ `DataAccessRoleArn`: The Amazon Resource Name \(ARN\) of the Amazon S3 role that has permissions to access the specified Amazon S3 bucket\. Note that you must also use the [Trust policy for real\-time analytics](security_iam_id-based-policy-examples.md#trust-policy)\.

If you want a redacted version of your transcript, you can include `ContentRedactionOutput` or `ContentRedactionType` in your request\. For more information on these parameters, see [https://docs.aws.amazon.com/transcribe/latest/APIReference/API_streaming_StartCallAnalyticsStreamTranscription.html](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_streaming_StartCallAnalyticsStreamTranscription.html) in the API Reference\.

To start a real\-time Call Analytics transcription with post\-call analytics enabled, you can use the **AWS Management Console** \(demo only\), **HTTP/2**, or **WebSockets**\. For examples, see [Starting a real\-time Call Analytics transcription](tca-start-stream.md)\.

**Important**  
Currently, the AWS Management Console only offers a demo for real\-time Call Analytics with pre\-loaded audio examples\. If you want to use your own audio, you must use the API \(HTTP/2, WebSockets, or an SDK\)\.

## Example post\-call analytics output<a name="tca-output-post-call"></a>

Post\-call transcripts are displayed in a turn\-by\-turn format by segment\. They include call characteristics, sentiment, call summarization, issue detection, and \(optionally\) PII redaction\. If any of your post\-call categories are a match to the audio content, these are also present in your output\.

To increase accuracy and further customize your transcripts to your use case, such as including industry\-specific terms, add [custom vocabularies](custom-vocabulary.md) or [custom language models](custom-language-models.md) to your Call Analytics request\. To mask, remove, or tag words you don't want in your transcription results, such as profanity, add [vocabulary filtering](vocabulary-filtering.md)\.

Here is a compiled post\-call analytics output example:

```
{
    "JobStatus": "COMPLETED",
    "LanguageCode": "en-US",
    "AccountId": "1234567890",
    "Channel": "VOICE",
    "Participants": [{
        "ParticipantRole": "AGENT"
    }, 
    {
        "ParticipantRole": "CUSTOMER"
    }],
    "SessionId": "12a3b45c-de6f-78g9-0123-45h6ab78c901",
    "ContentMetadata": {
        "Output": "Raw"
    }
    "Transcript": [{
        "LoudnessScores": [
            78.63,
            78.37,
            77.98,
            74.18
        ],
        "Content": "[PII], my name is [PII], how can I help?",

            ...

        "Content": "Well, I would like to cancel my recipe subscription.",
            "IssuesDetected": [{
                "CharacterOffsets": {
                    "Begin": 7,
                    "End": 51
                }
            }],

            ...

        "Content": "That's very sad to hear. Can I offer you a 50% discount to have you stay with us?",
        "Id": "649afe93-1e59-4ae9-a3ba-a0a613868f5d",
        "BeginOffsetMillis": 12180,
        "EndOffsetMillis": 16960,
        "Sentiment": "NEGATIVE",
        "ParticipantRole": "AGENT"
    },
    {
        "LoudnessScores": [
            80.22,
            79.48,
            82.81
        ],
        "Content": "That is a very generous offer. And I accept.",
        "Id": "f9266cba-34df-4ca8-9cea-4f62a52a7981",
        "BeginOffsetMillis": 17140,
        "EndOffsetMillis": 19860,
        "Sentiment": "POSITIVE",
        "ParticipantRole": "CUSTOMER"
    },
            ...

        "Content": "Wonderful. I made all changes to your account and now this discount is applied, please check.",
        "OutcomesDetected": [{
        "CharacterOffsets": {
            "Begin": 12,
            "End": 78
        }
        }],

            ...

        "Content": "I will send an email with all the details to you today, and I will call you back next week to follow up. Have a wonderful evening.",
        "Id": "78cd0923-cafd-44a5-a66e-09515796572f",
        "BeginOffsetMillis": 31800,
        "EndOffsetMillis": 39450,
        "Sentiment": "POSITIVE",
        "ParticipantRole": "AGENT"
    },
    {
        "LoudnessScores": [
            78.54,
            68.76,
            67.76
        ],
        "Content": "Thank you very much, sir. Goodbye.",
        "Id": "5c5e6be0-8349-4767-8447-986f995af7c3",
        "BeginOffsetMillis": 40040,
        "EndOffsetMillis": 42460,
        "Sentiment": "POSITIVE",
        "ParticipantRole": "CUSTOMER"
    }
    ],

    ...

    "Categories": {
        "MatchedDetails": {
            "positive-resolution": {
                "PointsOfInterest": [{
                    "BeginOffsetMillis": 40040,
                    "EndOffsetMillis": 42460
                }]
            }
        },
        "MatchedCategories": [
            "positive-resolution"
        ]
    },

    ...

    "ConversationCharacteristics": {
        "NonTalkTime": {
            "Instances": [],
            "TotalTimeMillis": 0
        },
        "Interruptions": {
            "TotalCount": 2,
            "TotalTimeMillis": 10700,
            "InterruptionsByInterrupter": {
                "AGENT": [{
                    "BeginOffsetMillis": 26040,
                    "DurationMillis": 5510,
                    "EndOffsetMillis": 31550
                }],
                "CUSTOMER": [{
                    "BeginOffsetMillis": 770,
                    "DurationMillis": 5190,
                    "EndOffsetMillis": 5960
                }]
            }
        },
        "TotalConversationDurationMillis": 42460,
        "Sentiment": {
            "OverallSentiment": {
                "AGENT": 2.5,
                "CUSTOMER": 2.1
            },
            "SentimentByPeriod": {
                "QUARTER": {
                    "AGENT": [{
                        "Score": 0.0,
                        "BeginOffsetMillis": 0,
                        "EndOffsetMillis": 9862
                    },
                    {
                        "Score": -5.0,
                        "BeginOffsetMillis": 9862,
                        "EndOffsetMillis": 19725
                    },
                    {
                        "Score": 5.0,
                        "BeginOffsetMillis": 19725,
                        "EndOffsetMillis": 29587
                    },
                    {
                       "Score": 5.0,
                        "BeginOffsetMillis": 29587,
                        "EndOffsetMillis": 39450
                    }
                    ],
                    "CUSTOMER": [{
                        "Score": -2.5,
                        "BeginOffsetMillis": 0,
                        "EndOffsetMillis": 10615
                    },
                    {
                        "Score": 5.0,
                        "BeginOffsetMillis": 10615,
                        "EndOffsetMillis": 21230
                    },
                    {
                        "Score": 2.5,
                        "BeginOffsetMillis": 21230,
                        "EndOffsetMillis": 31845
                    },
                    {
                        "Score": 5.0,
                        "BeginOffsetMillis": 31845,
                        "EndOffsetMillis": 42460
                    }
                    ]
                }
            }
        },
        "TalkSpeed": {
            "DetailsByParticipant": {
                "AGENT": {
                    "AverageWordsPerMinute": 150
                },
                "CUSTOMER": {
                    "AverageWordsPerMinute": 167
                }
            }
        },
        "TalkTime": {
            "DetailsByParticipant": {
                "AGENT": {
                    "TotalTimeMillis": 32750
                },
                "CUSTOMER": {
                    "TotalTimeMillis": 18010
                }
            },
            "TotalTimeMillis": 50760
        }
    },
```