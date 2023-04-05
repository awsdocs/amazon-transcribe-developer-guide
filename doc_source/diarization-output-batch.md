# Example diarization output \(batch\)<a name="diarization-output-batch"></a>

Here's an output example for a batch transcription with diarization enabled\.

```
{
    "jobName": "my-first-transcription-job",
    "accountId": "111122223333",
    "results": {
        "transcripts": [
            {
                "transcript": "I've been on hold for an hour. Sorry about that."
            }
        ],
        "speaker_labels": {
            "channel_label": "ch_0",
            "speakers": 2,
            "segments": [
                {
                    "start_time": "4.87",
                    "speaker_label": "spk_0",
                    "end_time": "6.88",
                    "items": [                                                 
                        {
                            "start_time": "4.87",
                            "speaker_label": "spk_0",
                            "end_time": "5.02"
                        },
                        {
                            "start_time": "5.02",
                            "speaker_label": "spk_0",
                            "end_time": "5.17"
                        },
                        {
                            "start_time": "5.17",
                            "speaker_label": "spk_0",
                            "end_time": "5.29"
                        },
                        {
                            "start_time": "5.29",
                            "speaker_label": "spk_0",
                            "end_time": "5.64"
                        },
                        {
                            "start_time": "5.64",
                            "speaker_label": "spk_0",
                            "end_time": "5.84"
                        },                     
                        {
                            "start_time": "6.11",
                            "speaker_label": "spk_0",
                            "end_time": "6.26"
                        },
                        {
                            "start_time": "6.26",
                            "speaker_label": "spk_0",
                            "end_time": "6.88"
                        }
                    ]
                },
                {
                    "start_time": "8.49",
                    "speaker_label": "spk_1",
                    "end_time": "9.24",
                    "items": [
                        {
                            "start_time": "8.49",
                            "speaker_label": "spk_1",
                            "end_time": "8.88"
                        },
                        {
                            "start_time": "8.88",
                            "speaker_label": "spk_1",
                            "end_time": "9.05"
                        },
                        {
                            "start_time": "9.05",
                            "speaker_label": "spk_1",
                            "end_time": "9.24"
                        }                                           
                    ]
                }
            ]
        },
        "items": [            
            {
                "start_time": "4.87",
                "speaker_label": "spk_0",
                "end_time": "5.02",
                "alternatives": [
                    {
                        "confidence": "1.0",
                        "content": "I've"
                    }
                ],
                "type": "pronunciation"
            },
            {
                "start_time": "5.02",
                "speaker_label": "spk_0",
                "end_time": "5.17",
                "alternatives": [
                    {
                        "confidence": "1.0",
                        "content": "been"
                    }
                ],
                "type": "pronunciation"
            },
            {
                "start_time": "5.17",
                "speaker_label": "spk_0",
                "end_time": "5.29",
                "alternatives": [
                    {
                        "confidence": "1.0",
                        "content": "on"
                    }
                ],
                "type": "pronunciation"
            },
            {
                "start_time": "5.29",
                "speaker_label": "spk_0",
                "end_time": "5.64",
                "alternatives": [
                    {
                        "confidence": "1.0",
                        "content": "hold"
                    }
                ],
                "type": "pronunciation"
            },
            {
                "start_time": "5.64",
                "speaker_label": "spk_0",
                "end_time": "5.84",
                "alternatives": [
                    {
                        "confidence": "1.0",
                        "content": "for"
                    }
                ],
                "type": "pronunciation"
            },      
            {
                "start_time": "6.11",
                "speaker_label": "spk_0",
                "end_time": "6.26",
                "alternatives": [
                    {
                        "confidence": "1.0",
                        "content": "an"
                    }
                ],
                "type": "pronunciation"
            },
            {
                "start_time": "6.26",
                "speaker_label": "spk_0",
                "end_time": "6.88",
                "alternatives": [
                    {
                        "confidence": "1.0",
                        "content": "hour"
                    }
                ],
                "type": "pronunciation"
            },
            {
                "speaker_label": "spk_0",
                "alternatives": [
                    {
                        "confidence": "0.0",
                        "content": "."
                    }
                ],
                "type": "punctuation"
            },
            {
                "start_time": "8.49",
                "speaker_label": "spk_1",
                "end_time": "8.88",
                "alternatives": [
                    {
                        "confidence": "1.0",
                        "content": "Sorry"
                    }
                ],
                "type": "pronunciation"
            },
            {
                "start_time": "8.88",
                "speaker_label": "spk_1",
                "end_time": "9.05",
                "alternatives": [
                    {
                        "confidence": "0.902",
                        "content": "about"
                    }
                ],
                "type": "pronunciation"
            },
            {
                "start_time": "9.05",
                "speaker_label": "spk_1",
                "end_time": "9.24",
                "alternatives": [
                    {
                        "confidence": "1.0",
                        "content": "that"
                    }
                ],
                "type": "pronunciation"
            },
            {
                "speaker_label": "spk_1",
                "alternatives": [
                    {
                        "confidence": "0.0",
                        "content": "."
                    }
                ],
                "type": "punctuation"
            }           
          ]
    },
    "status": "COMPLETED"
}
```