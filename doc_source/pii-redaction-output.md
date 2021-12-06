# Example PII redaction and identification output<a name="pii-redaction-output"></a>

The following examples show redacted output from batch and streaming jobs, and PII identification from a streaming job\.

Transcription jobs using content redaction generate two types of `confidence` values\. The Automatic Speech Recognition \(ASR\) confidence indicates the items that have the `type` of `pronunciation` or `punctuation` is a specific utterance\. In the following transcript output, the word `Good` has a `confidence` of `1.0`\. This confidence value indicates that Amazon Transcribe is 100 percent confident that the word uttered in this transcript is 'Good'\. The `confidence` value for a `[PII]` tag is the confidence that the speech it flagged for redaction is truly PII\. In the following transcript output, the `confidence` of `0.9999` indicates that Amazon Transcribe is 99\.99 percent confident that the entity it redacted in the transcript is PII\.

## Example redacted batch output<a name="pii-redaction-output-batch"></a>

```
{
    "jobName": "job id",
    "accountId": "account id",
    "isRedacted": true,
    "results": {
        "transcripts": [
            {
                "transcript": "Good morning, everybody. My name is [PII], and today I feel like
                sharing a whole lot of personal information with you. Let's start with my Social 
                Security number [PII]. My credit card number is [PII] and my C V V code is [PII].
                I hope that Amazon Transcribe is doing a good job at redacting that personal 
                information away. Let's check."
            }
        ],
        "items": [
            {
                "start_time": "2.86",
                "end_time": "3.35",
                "alternatives": [
                    {
                        "confidence": "1.0",
                        "content": "Good"
                    }
                ],
                "type": "pronunciation"
            },
            Items removed for brevity
            {
                "start_time": "5.56",
                "end_time": "6.25",
                "alternatives": [
                    {
                        "content": "[PII]",
                        "redactions": [
                            {
                                "confidence": "0.9999"
                            }
                        ]
                    }
                ],
                "type": "pronunciation"
            },
            Items removed for brevity
        ],
    },
    "status": "COMPLETED"
}
```

Here's the unredacted transcript for comparison:

```
{
    "jobName": "job id",
    "accountId": "account id",
    "isRedacted": false,
    "results": {
        "transcripts": [
            {
                "transcript": "Good morning, everybody. My name is Mike, and today I feel like
                sharing a whole lot of personal information with you. Let's start with my Social 
                Security number 000000000. My credit card number is 5555555555555555 
                and my C V V code is 000. I hope that Amazon Transcribe is doing a good job 
                at redacting that personal information away. Let's check."
            }
        ],
        "items": [
            {
                "start_time": "2.86",
                "end_time": "3.35",
                "alternatives": [
                    {
                        "confidence": "1.0",
                        "content": "Good"
                    }
                ],
                "type": "pronunciation"
            },
            Items removed for brevity
            {
                "start_time": "5.56",
                "end_time": "6.25",
                "alternatives": [
                    {
                        "confidence": "0.9999",
                        "content": "Mike",
                     {                        
                ],
                "type": "pronunciation"
            },
            Items removed for brevity
        ],
    },
    "status": "COMPLETED"
}
```

## Example redacted streaming output<a name="pii-redaction-output-stream"></a>

```
{
    "TranscriptResultStream": {
        "TranscriptEvent": {
            "Transcript": {
                "Results": [
                    {
                        "Alternatives": [
                            {
                                "Transcript": "my name is [NAME]",
                                "Items": [
                                    {
                                        "Content": "my",
                                        "EndTime": 0.3799375,
                                        "StartTime": 0.0299375,
                                        "Type": "pronunciation"
                                    },
                                    {
                                        "Content": "name",
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
                                        "Content": "[NAME]",
                                        "EndTime": 1.0199375,
                                        "StartTime": 0.7999375,
                                        "Type": "pronunciation"
                                    }
                                ],
                                "Entities": [
                                    {
                                        "Content": "[NAME]",
                                        "Category": "PII",
                                        "Type": "NAME",
                                        "StartTime" : 0.7999375,
                                        "EndTime" : 1.0199375,
                                        "Confidence": 0.9989
                                    }
                                ]
                            }
                        ],
                        "EndTime": 1.02,
                        "IsPartial": false,
                        "ResultId": "2db76dc8-d728-11e8-9f8b-f2801f1b9fd1",
                        "StartTime": 0.0199375
                    }
                ]
            }
        }
    }
}
```

## Example PII identification output<a name="pii-redaction-output-id"></a>

PII identification is an additional feature that you can use with your streaming transcription job\.

```
{
    "TranscriptResultStream": {
        "TranscriptEvent": {
            "Transcript": {
                "Results": [
                    {
                        "Alternatives": [
                            {
                                "Transcript": "my name is janet smithy",
                                "Items": [
                                    {
                                        "Content": "my",
                                        "EndTime": 0.3799375,
                                        "StartTime": 0.0299375,
                                        "Type": "pronunciation"
                                    },
                                    {
                                        "Content": "name",
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
                                        "Content": "janet",
                                        "EndTime": 0.9199375,
                                        "StartTime": 0.7999375,
                                        "Type": "pronunciation"
                                    },
                                    {
                                        "Content": "smithy",
                                        "EndTime": 1.0199375,
                                        "StartTime": 0.9299375,
                                        "Type": "pronunciation"
                                    }
                                ],
                                "Entities": [
                                    {
                                        "Content": "janet smithy",
                                        "Category": "PII",
                                        "Type": "NAME",
                                        "StartTime" : 0.7999375,
                                        "EndTime" : 1.0199375,
                                        "Confidence": 0.9989
                                    }
                                ]
                            }
                        ],
                        "EndTime": 1.02,
                        "IsPartial": false,
                        "ResultId": "2db76dc8-d728-11e8-9f8b-f2801f1b9fd1",
                        "StartTime": 0.0199375
                    }
                ]
            }
        }
    }
}
```