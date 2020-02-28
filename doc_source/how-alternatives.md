# Alternative Transcriptions<a name="how-alternatives"></a>

When Amazon Transcribe transcribes an audio file, it returns the transcription with the highest confidence level\. You can specify that Amazon Transcribe return additional transcriptions with lower confidence levels\. Use alternative transcriptions to see different interpretations of the transcribed audio\. For example, in an application that enables a person to review the transcription, you can present the alternative transcriptions for the person to choose from\. Alternative transcriptions are only available for the [StartTranscriptionJob](API_StartTranscriptionJob.md) operation\.

You can configure Amazon Transcribe to return alternative transcription using the console or by using the Amazon Transcribe API\. To get alternative transcriptions using the API, set the `ShowAlternatives` field to `true` and set the `MaxAlternatives` field to the number of alternatives to return when you call the [StartTranscriptionJob](API_StartTranscriptionJob.md) operation\. You can specify that Amazon Transcribe return up to 10 alternative transcriptions\. 

You can combine alternative transcriptions with speaker identification and channel identification\. Alternative transcriptions are available in all supported languages\.

Alternatives are presented at the segment level of the transcription\. Segments are defined by natural pauses in speech, such as a change in speaker or pause in the audio\. For example, the spoken phrase "It is raining today in Seattle, but not in Portland" is separated into two segments: "It is raining today in Seattle" and "but not in Portland\."

Amazon Transcribe returns an overall transcription of your audio file in the response\. When you have configured Amazon Transcribe to return alternatives, the overall transcription is built from the segment alternatives with the highest confidence level\. Alternative transcriptions are returned in the `segments` structure in the output JSON\. If Amazon Transcribe doesn't find alternatives, it returns fewer than the number of alternatives specified in the `MaxAlternatives` field\.

The following is the JSON output from Amazon Transcribe\. It is the transcription output for this input: **Uh, you can just call this number if I don't pick up, just leave a voicemail and I'll get back to you\. Okay\. And that's the number\. The 1166 number, you mean?** 

The following is the JSON output with `ShowAlternatives` set to `false`\.

```
{
    "results": {
        "transcripts": [
            "Uh, you can just call this number if I don't pick up and leave a voicemail and I'll get back to you. Okay. And that's the number. The 1166 number, you mean"
        ],
        "items": [
            {
                "start_time": 12.35,
                "end_time": 12.57,
                "alternatives": [
                    {
                        "confidence": 0.9989,
                        "content": "Uh"
                    }
                ],
                "type": "pronunciation"
            },
            Items removed for brevity.
        ]
    }
}
```

The following is the JSON output for the same input with `ShowAlternatives` set to `true` and `MaxAlternatives` set to `2`\. 

```
{
    "results": {
        "transcripts": [
            "Uh, you can just call this number if I don't pick up and leave a voicemail and I'll get back to you. Okay. And that's the number. The 1166 number, you mean"
        ],
        "items": [
            {
                "start_time": 12.35,
                "end_time": 12.57,
                "alternatives": [
                    {
                        "confidence": 0.9989,
                        "content": "Uh"
                    }
                ],
                "type": "pronunciation"
            },
            Items removed for brevity..
        ],
        "segments": [
            {
                "start_time": 11.84,
                "end_time": 19.665,
                "alternatives": [
                    {
                        "transcript": "Uh, you can just call this number if I don't pick up and leave a voicemail and I'll get back to you.",
                        "items": [
                            {
                                "start_time": 12.35,
                                "end_time": 12.57,
                                "confidence": 0.9989,
                                "content": "Uh",
                                "type": "pronunciation"
                            },
                            Items removed for brevity.
                            {
                                "start_time": 16.42,
                                "end_time": 16.52,
                                "confidence": 0.7572,
                                "content": "and",
                                "type": "pronunciation"
                            },
                            Items removed for brevity.
                        ]
                    },
                    {
                        "transcript": "Uh, you can just call this number if I don't pick up, just leave a voicemail and I'll get back to you.",
                        "items": [
                            {
                                "start_time": 12.35,
                                "end_time": 12.57,
                                "confidence": 0.9989,
                                "content": "Uh",
                                "type": "pronunciation"
                            },
                            Items removed for brevity..
                            {
                                "start_time": 16.42,
                                "end_time": 16.52,
                                "content": ",",
                                "type": "punctuation"
                            },
                            {
                                "start_time": 16.42,
                                "end_time": 16.52,
                                "confidence": 0.8934,
                                "content": "just",
                                "type": "punctuation"
                            },
                            Items removed for brevity..
                        ]
                    },
                    Alternatives removed for brevity.
                ]
            },
            Segments removed for brevity..
        ]
    }
}
```