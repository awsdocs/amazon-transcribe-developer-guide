# Post\-call analytics output<a name="tca-output-batch"></a>

Post\-call analytics transcripts are displayed in a turn\-by\-turn format by segment\. They include call categorization, call characteristics \(loudness scores, interruptions, non\-talk time, talk speed\), call summarization \(issues, outcomes, and action items\), redaction, and sentiment\. Additionally, a summary of conversation characteristics is provided at the end of the transcript\.

To increase accuracy and further customize your transcripts to your use case, such as including industry\-specific terms, add [custom vocabularies](custom-vocabulary.md) or [custom language models](custom-language-models.md) to your Call Analytics request\. To mask, remove, or tag words that you don't want in your transcription results, such as profanity, add [vocabulary filtering](vocabulary-filtering.md)\.

The following sections show examples of JSON output at an insight level\. For compiled output, see [Compiled post\-call analytics output](#tca-output-batch-compiled)\.

## Call categorization<a name="tca-output-categorization-batch"></a>

Here's what a category match looks like in your transcription output\. This example shows that the audio from the 40040 millisecond timestamp to the 42460 millisecond timestamp is a match to the 'positive\-resolution' category\. In this case, the custom 'positive\-resolution' category required a positive sentiment in last few seconds of speech\.

```
"Categories": {
    "MatchedDetails": {
        "positive-resolution": {
            "PointsOfInterest": [
                {
                    "BeginOffsetMillis":  40040,
                    "EndOffsetMillis":  42460
                }
            ]
        }
    },
    "MatchedCategories": [
        " positive-resolution"
    ]
},
```

## Call characteristics<a name="tca-output-characteristics-batch"></a>

Here's what call characteristics look like in your transcription output\. Note that loudness scores are provided for each conversation turn, while all other characteristics are provided at the end of the transcript\.

```
"LoudnessScores": [
    87.54,
    88.74,
    90.16,
    86.36,
    85.56,
    85.52,
    81.79,
    87.74,
    89.82
],
  
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
            "AGENT": [
                {
                    "BeginOffsetMillis": 26040,
                    "DurationMillis": 5510,
                    "EndOffsetMillis": 31550
                }
            ],
            "CUSTOMER": [
                {
                    "BeginOffsetMillis": 770,
                    "DurationMillis": 5190,
                    "EndOffsetMillis": 5960
                }
            ]
        }
    },
    "TotalConversationDurationMillis": 42460,
  
    ...
    
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

## Call summarization<a name="tca-output-summarization-batch"></a>

Here's what call summarization looks like in your transcription output:
+ In the following example, **issues** are identified as starting at character 7 and ending at character 51, which refers to this section of the text: "*I would like to cancel my recipe subscription*"\.

  ```
  "Content": "Well, I would like to cancel my recipe subscription.",
      
  "IssuesDetected": [
      {
          "CharacterOffsets": {
              "Begin": 7,
              "End": 51
          }
      }
  ],
  ```
+ In the following example, **outcomes** are identified as starting at character 12 and ending at character 78, which refers to this section of the text: "*I made all changes to your account and now this discount is applied*"\.

  ```
  "Content": "Wonderful. I made all changes to your account and now this discount is applied, please check.",
  
  "OutcomesDetected": [
      {
          "CharacterOffsets": {
              "Begin": 12,
              "End": 78
          }
      }
  ],
  ```
+ In the following example, **action items** are identified as starting at character 0 and ending at character 103, which refers to this section of the text: "*I will send an email with all the details to you today, and I will call you back next week to follow up*"\.

  ```
  "Content": "I will send an email with all the details to you today, and I will call you back next week to follow up. Have a wonderful evening.",
      
  "ActionItemsDetected": [
      {
          "CharacterOffsets": {
              "Begin": 0,
              "End": 103
          }
      }
  ],
  ```

## Sentiment analysis<a name="tca-output-sentiment-batch"></a>

Here's what sentiment analysis looks like in your transcription output\.
+ Qualitative turn\-by\-turn sentiment values:

  ```
  "Content": "That's very sad to hear. Can I offer you a 50% discount to have you stay with us?",
      
  ...
      
  "BeginOffsetMillis": 12180,
  "EndOffsetMillis": 16960,
  "Sentiment": "NEGATIVE",
  "ParticipantRole": "AGENT"
              
  ...
              
  "Content": "That is a very generous offer. And I accept.",
  
  ...
  
  "BeginOffsetMillis": 17140,
  "EndOffsetMillis": 19860,
  "Sentiment": "POSITIVE",
  "ParticipantRole": "CUSTOMER"
  ```
+ Quantitative sentiment values for the entire call:

  ```
  "Sentiment": {
      "OverallSentiment": {
          "AGENT": 2.5,
          "CUSTOMER": 2.1
      },
  ```
+ Quantitative sentiment values per participant and per call quarter:

  ```
  "SentimentByPeriod": {
      "QUARTER": {
          "AGENT": [
              {
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
          "CUSTOMER": [
              {
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
  ```

## PII redaction<a name="tca-output-pii-redact-batch"></a>

Here's what PII redaction looks like in your transcription output\.

```
"Content": "[PII], my name is [PII], how can I help?",
```

## Compiled post\-call analytics output<a name="tca-output-batch-compiled"></a>

For brevity, some content is replaced with ellipses in the following transcription output\.

```
{
    "JobStatus": "COMPLETED",
    "LanguageCode": "en-US",
    "Transcript": [
        {
            "LoudnessScores": [
                78.63,
                78.37,
                77.98,
                74.18
            ],
            "Content": "[PII], my name is [PII], how can I help?",
            
            ...
     
             "Content": "Well, I would like to cancel my recipe subscription.",
             "IssuesDetected": [
                 {
                     "CharacterOffsets": {
                         "Begin": 7,
                         "End": 51
                     }
                 }
             ],
            
            ...
     
            "Content": "That's very sad to hear. Can I offer you a 50% discount to have you stay with us?",
            "Items": [
            ...
             ],
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
            "Items": [
            ...
            ],
            "Id": "f9266cba-34df-4ca8-9cea-4f62a52a7981",
            "BeginOffsetMillis": 17140,
            "EndOffsetMillis": 19860,
            "Sentiment": "POSITIVE",
            "ParticipantRole": "CUSTOMER"
        },
        {
     
     ...
     
            "Content": "Wonderful. I made all changes to your account and now this discount is applied, please check.",
            "OutcomesDetected": [
                {
                    "CharacterOffsets": {
                        "Begin": 12,
                        "End": 78
                    }
                }
            ],
            
            ...
            
            "Content": "I will send an email with all the details to you today, and I will call you back next week to follow up. Have a wonderful evening.",
            "Items": [
            ...   
            ],
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
           "Items": [
           ...     
           ],
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
                "PointsOfInterest": [
                    {
                        "BeginOffsetMillis": 40040,
                        "EndOffsetMillis": 42460
                    }
                ]
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
                "AGENT": [
                    {
                        "BeginOffsetMillis": 26040,
                        "DurationMillis": 5510,
                        "EndOffsetMillis": 31550
                    }
                ],
                "CUSTOMER": [
                    {
                        "BeginOffsetMillis": 770,
                        "DurationMillis": 5190,
                        "EndOffsetMillis": 5960
                    }
                ]
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
                    "AGENT": [
                        {
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
                    "CUSTOMER": [
                        {
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