# Sample call analytics output<a name="analyze-output"></a>

Below is an example of redacted JSON output from a call analytics job between a customer and an agent\. Note that in addition to redacted content \(shown as \[PII\]\), there are loudness scores and sentiment values \(negative, positive, or neutral\) associated with each segment of the dialogue\.

```
{
    "JobStatus": "COMPLETED",
    "LanguageCode": "en-US",
    "Transcript": [
        {
            "LoudnessScores": [
                87.87,
                85.25,
                83.46,
                81.37,
                80.37,
                75.91
            ],
            "Content": "Hey Mr [PII]? Um I think I lost my debit card or it was stolen. I don't know.",
            "IssuesDetected": [
                {
                    "CharacterOffsets": {
                        "Begin": 27,
                        "End": 63
                    }
                }
            ],
            "Redaction": {
                "RedactedTimestamps": [
                    [
                        {
                            "BeginOffsetMillis": 6950,
                            "EndOffsetMillis": 7470
                        }
                    ]
                ]
            }, 
            
           Items removed for brevity
                
            ],
            "Id": "cccccccc-cccc-cccc-cccc-ccccccccccccc",
            "BeginOffsetMillis": 6040,
            "EndOffsetMillis": 11650,
            "Sentiment": "NEUTRAL",
            "ParticipantRole": "CUSTOMER"
        },
        {
            "LoudnessScores": [
                86.09,
                83.63,
                86.11,
                85.33,
                74.4,
                19.55,
                64.23,
                81.19,
                89.7
            ],
            "Content": "Uh I am very sorry to hear that. Um May I ask who I'm speaking with [PII].",
            "Redaction": {
                "RedactedTimestamps": [
                    [
                        {
                            "BeginOffsetMillis": 19500,
                            "EndOffsetMillis": 20230
                        }
                    ]
                ]
            },   
                    ],
                    "BeginOffsetMillis": 19500,
                    "EndOffsetMillis": 20230
                },
               
           Items removed for brevity
                
            ],
            "Id": "bbbbbbbb-bbbb-bbbb-bbbb-bbbbbbbbbbbbb",
            "BeginOffsetMillis": 12040,
            "EndOffsetMillis": 20230,
            "Sentiment": "NEGATIVE",
            "ParticipantRole": "AGENT"
        },
        {
            "LoudnessScores": [
                78.49,
                84.47,
                81.35
            ],
            "Content": "Yeah, this is [PII].",
            "Redaction": {
                "RedactedTimestamps": [
                    [
                        {
                            "BeginOffsetMillis": 17420,
                            "EndOffsetMillis": 18460
                        }
                    ]
                ]
            },
            
           Items removed for brevity
            
            ],
            "Id": "aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaaa",
            "BeginOffsetMillis": 16840,
            "EndOffsetMillis": 18460,
            "Sentiment": "NEUTRAL",
            "ParticipantRole": "CUSTOMER"
        }
    ],
    "AccountId": "123456789012",
    "Categories": {
        "MatchedDetails": {
            "matchedCategoryA": {
                "PointsOfInterest": [{
                    "BeginOffsetMillis": 440,
                    "EndOffsetMillis": 4960
                }]
            }
        },
        "MatchedCategories": ["matchedCategoryA"]
    },
    "Channel": "VOICE",
    "JobName": "call-analytics-job-name",
    "Participants": [{
        "ParticipantRole": "AGENT"
    }, {
        "ParticipantRole": "CUSTOMER"
    }],
    "ConversationCharacteristics": {
        "NonTalkTime": {
            "Instances": [{
                "BeginOffsetMillis": 216450,
                "DurationMillis": 7690,
                "EndOffsetMillis": 224140
            }],
            "TotalTimeMillis": 7690
        },
        "Interruptions": {
            "TotalCount": 4,
            "TotalTimeMillis": 12129,
            "InterruptionsByInterrupter": {
                "AGENT": [{
                    "BeginOffsetMillis": 30940,
                    "DurationMillis": 2800,
                    "EndOffsetMillis": 33740
                }, {
                    "BeginOffsetMillis": 133440,
                    "DurationMillis": 4510,
                    "EndOffsetMillis": 137950
                }, {
                    "BeginOffsetMillis": 163240,
                    "DurationMillis": 2710,
                    "EndOffsetMillis": 165950
                }, {
                    "BeginOffsetMillis": 169840,
                    "DurationMillis": 2110,
                    "EndOffsetMillis": 171950
                }]
            }
        },
        "TotalConversationDurationMillis": 279060,
        "Sentiment": {
            "OverallSentiment": {
                "AGENT": 2.7,
                "CUSTOMER": 0.2
            },
            "SentimentByPeriod": {
                "QUARTER": {
                    "AGENT": [{
                        "Score": 2.1,
                        "BeginOffsetMillis": 0,
                        "EndOffsetMillis": 69765
                    }, {
                        "Score": -0.7,
                        "BeginOffsetMillis": 69765,
                        "EndOffsetMillis": 139530
                    }, {
                        "Score": 5.0,
                        "BeginOffsetMillis": 139530,
                        "EndOffsetMillis": 209295
                    }, {
                        "Score": 3.0,
                        "BeginOffsetMillis": 209295,
                        "EndOffsetMillis": 279060
                    }],
                    "CUSTOMER": [{
                        "Score": -2.0,
                        "BeginOffsetMillis": 0,
                        "EndOffsetMillis": 69660
                    }, {
                        "Score": 0.0,
                        "BeginOffsetMillis": 69660,
                        "EndOffsetMillis": 139320
                    }, {
                        "Score": 0.0,
                        "BeginOffsetMillis": 139320,
                        "EndOffsetMillis": 208980
                    }, {
                        "Score": 2.1,
                        "BeginOffsetMillis": 208980,
                        "EndOffsetMillis": 278640
                    }]
                }
            }
        },
        "TalkSpeed": {
            "DetailsByParticipant": {
                "AGENT": {
                    "AverageWordsPerMinute": 195
                },
                "CUSTOMER": {
                    "AverageWordsPerMinute": 116
                }
            }
        },
        "TalkTime": {
            "DetailsByParticipant": {
                "AGENT": {
                    "TotalTimeMillis": 158120
                },
                "CUSTOMER": {
                    "TotalTimeMillis": 108009
                }
            },
            "TotalTimeMillis": 266129
        }
    },
    "ContentMetadata": {
        "Output": "Redacted",
        "RedactionTypes": ["PII"]
    }
}
```