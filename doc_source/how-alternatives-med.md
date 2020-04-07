# Alternative Transcriptions<a name="how-alternatives-med"></a>

When you use Amazon Transcribe Medical you have the option to return transcriptions with different confidence levels\. By default, you get the transcription with the highest confidence level\. However, you can specify that Amazon Transcribe Medical return additional transcriptions with lower confidence levels\. Use alternative transcriptions to see different interpretations of the transcribed audio\. For example, in an application that enables a person to review the transcription, you can present the alternative transcriptions for the person to choose from\. Alternative transcriptions are only available for the [StartMedicalTranscriptionJob](API_StartMedicalTranscriptionJob.md) operation\.

You can configure Amazon Transcribe to return alternative transcriptions by using the console or by direct API call\. To get alternative transcriptions call the [StartMedicalTranscriptionJob](API_StartMedicalTranscriptionJob.md) operation\., Set the `ShowAlternatives` field to `true` and set the `MaxAlternatives` field to the number of alternatives to return\. You can specify that Amazon Transcribe return up to 10 alternative transcriptions\. 

Alternatives are presented at the segment level of the transcription\. Segments are defined by natural pauses in speech, such as a change in speaker or pause in the audio\. For example, the sentence "Her blood pressure has been elevated, so we have started her on 50 mg metoprolol succinate twice daily" is separated into two segments\. "Her blood pressure has been elevated" and "so we have started her on 50 mg metoprolol succinate twice daily"

Amazon Transcribe returns an overall transcription of your audio file in the response\. When you configure Amazon Transcribe to return alternatives, the overall transcription is built from the segment alternatives with the highest confidence level\. Alternative transcriptions are returned in the `segments` structure in the output JSON\. If Amazon Transcribe doesn't find alternatives, it returns fewer than the number of alternatives specified in the `MaxAlternatives` field\.

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