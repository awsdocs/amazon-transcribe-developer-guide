# Issue detection<a name="call-analytics-issue-detection"></a>

Using call analytics, Amazon Transcribe attempts to identify the reason behind customer calls\. The issue detection feature works across all industries and business sectors, searching for common customer service\-related phrases and terms, such as "I need help \.\.\.", "\.\.\. tell me your issue \.\.\.", "wrong", "lost", "damaged", and "stolen", to hone in on customer issues\.

Issue detection works out\-of\-the\-box, and thus doesn't support customization, such as model training or custom categories\.

Here's what issue detection looks like in your transcription output:

```
"Content": "Hey Mr [PII]? Um I think I lost my debit card or it was stolen. I don't know.",
            "IssuesDetected": [
                {
                    "CharacterOffsets": {
                        "Begin": 27,
                        "End": 63
                    }
                }
            ],
```

In this output, the issue is identified in the text between characters 27 and 63 in the preceeding text: "*lost my debit card or it was stolen*"\.