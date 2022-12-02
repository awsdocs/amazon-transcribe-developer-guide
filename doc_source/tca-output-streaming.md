# Real\-time Call Analytics output<a name="tca-output-streaming"></a>

Real\-time Call Analytics transcripts are displayed in a turn\-by\-turn format by segment\. They include category events, issue detection, sentiment, and PII identification and redaction\. Category events allow you to set real\-time alerts; see [Creating real\-time alerts for category matches](tca-start-stream.md#tca-create-alert-stream) for more information\.

To increase accuracy and further customize your transcripts to your use case, such as including industry\-specific terms, add [custom vocabularies](custom-vocabulary.md) or [custom language models](custom-language-models.md) to your Call Analytics request\. To mask, remove, or tag words you don't want in your transcription results, such as profanity, add [vocabulary filtering](vocabulary-filtering.md)\.

The following sections show examples of JSON output for real\-time Call Analytics transcriptions\.

## Category events<a name="tca-output-category-event-stream"></a>

Here's what a category match looks like in your transcription output\. This example shows that the audio from the 19010 millisecond timestamp to the 22690 millisecond timestamp is a match to the 'network\-complaint' category\. In this case, the custom 'network\-complaint' category required that the customer said "*network issues*" \(exact word match\)\.

```
"CategoryEvent": { 
    "MatchedCategories": [ 
        "network-complaint" 
    ],
    "MatchedDetails": { 
        "network issues" : { 
            "TimestampRanges": [    
                { 
                    "BeginOffsetMillis": 9299375,
                    "EndOffsetMillis": 7899375
                }
            ]
        }
    }
},
```

## Issue detection<a name="tca-output-issue-detection-stream"></a>

Here's what an issue detection match looks like in your transcription output\. This example shows that the text from character 26 to character 62 describes an issue\.

```
"UtteranceEvent": {
    ...
    "Transcript": "Wang Xiulan I'm tired of the network issues my phone is having.",
    ...
    "IssuesDetected": [
        {
            "CharacterOffsets": {
                "BeginOffsetChar": 26,
                "EndOffsetChar": 62
            }
        }
    ]
},
```

## Sentiment<a name="tca-output-sentiment-stream"></a>

Here's what sentiment analysis looks like in your transcription output\.

```
"UtteranceEvent": {    
    ...
    "Sentiment": "NEGATIVE",
    "Items": [{
        ...
```

## PII identification<a name="tca-output-pii-id-stream"></a>

Here's what PII identification looks like in your transcription output\.

```
"Entities": [
    {
        "Content": "Wang Xiulan",
        "Category": "PII",
        "Type": "NAME",
        "BeginOffsetMillis": 7999375,
        "EndOffsetMillis": 199375,
        "Confidence": 0.9989
    }
],
```

## PII redaction<a name="tca-output-pii-redact-stream"></a>

Here's what PII redaction looks like in your transcription output\.

```
"Content": "[NAME]. Hi, [NAME]. I'm [NAME] Happy to be helping you today.",
"Redaction": {
    "RedactedTimestamps": [
        {
            "BeginOffsetMillis": 32670,
            "EndOffsetMillis": 33343
        }, 
        {
            "BeginOffsetMillis": 33518,
            "EndOffsetMillis": 33858
        }, 
        {
            "BeginOffsetMillis": 34068,
            "EndOffsetMillis": 34488
        }
    ]
},
```

## Compiled real\-time Call Analytics output<a name="tca-output-streaming-compiled"></a>

For brevity, some content is replaced with ellipses in the following transcription output\.

```
{
    "CallAnalyticsTranscriptResultStream": {
        "BadRequestException": {},
        "ConflictException": {},
        "InternalFailureException": {},
        "LimitExceededException": {},
        "ServiceUnavailableException": {},
        "UtteranceEvent": {
            "UtteranceId": "58c27f92-7277-11ec-90d6-0242ac120003",
            "ParticipantRole": "CUSTOMER",
            "IsPartial": false,
            "Transcript": "Wang Xiulan I'm tired of the network issues my phone is having.",
            "BeginOffsetMillis": 19010,
            "EndOffsetMillis": 22690,
            "Sentiment": "NEGATIVE",
            "Items": [{
                    "Content": "Wang",
                    "BeginOffsetMillis": 379937,
                    "EndOffsetMillis": 299375,
                    "Type": "pronunciation",
                    "Confidence": 0.9961,
                    "VocabularyFilterMatch": false
                },
                {
                    "Content": "Xiulan",
                    "EndOffsetMillis": 5899375,
                    "BeginOffsetMillis": 3899375,
                    "Type": "pronunciation",
                    "Confidence": 0.9961,
                    "VocabularyFilterMatch": false
                },
                ...
                {
                    "Content": "network",
                    "EndOffsetMillis": 199375,
                    "BeginOffsetMillis": 9299375,
                    "Type": "pronunciation",
                    "Confidence": 0.9961,
                    "VocabularyFilterMatch": false
                },
                {
                    "Content": "issues",
                    "EndOffsetMillis": 7899375,
                    "BeginOffsetMillis": 5999375,
                    "Type": "pronunciation",
                    "Confidence": 0.9961,
                    "VocabularyFilterMatch": false
                },
                {
                    "Content": "my",
                    "EndOffsetMillis": 9199375,
                    "BeginOffsetMillis": 7999375,
                    "Type": "pronunciation",
                    "Confidence": 0.9961,
                    "VocabularyFilterMatch": false
                },
                {
                    "Content": "phone",
                    "EndOffsetMillis": 199375,
                    "BeginOffsetMillis": 9299375,
                    "Type": "pronunciation",
                    "Confidence": 0.9961,
                    "VocabularyFilterMatch": false
                },
                ...
            ],
            "Entities": [{
                "Content": "Wang Xiulan",
                "Category": "PII",
                "Type": "NAME",
                "BeginOffsetMillis": 7999375,
                "EndOffsetMillis": 199375,
                "Confidence": 0.9989
            }],
            "IssuesDetected": [{
                "CharacterOffsets": {
                    "BeginOffsetChar": 26,
                    "EndOffsetChar": 62
                }
            }]
        },
        "CategoryEvent": { 
            "MatchedCategories": [ 
                "network-complaint" 
            ],
            "MatchedDetails": { 
                "network issues" : { 
                    "TimestampRanges": [    
                        { 
                            "BeginOffsetMillis": 9299375,
                            "EndOffsetMillis": 7899375
                        }
                    ]
                }
            }
        }
    }
}
```