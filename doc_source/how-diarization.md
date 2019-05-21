# Identifying Speakers<a name="how-diarization"></a>

You can have Amazon Transcribe identify the different speakers in an audio clip, a process known as *diarization* or *speaker identification*\. When you enable speaker identification, Amazon Transcribe labels each fragment with the speaker that it identified\. 

You can specify that Amazon Transcribe identify between 2 and 10 speakers in the audio clip\. You get the best performance when the number of speakers that you ask to identify matches the number of speakers in the input audio\.

To turn on speaker identification, set the `MaxSpeakerLabels` and `ShowSpeakerLabels` field of the `Settings` field when you make a call to the [StartTranscriptionJob](API_StartTranscriptionJob.md) operation\. You must set both fields or else Amazon Transcribe will return an exception\.

When Amazon Transcribe completes a transcription job, it creates a JSON file that contains the results and saves the file in an S3 bucket\. The file is identified by a user\-specific URI\. Use the URI to get the results\.

The following is the JSON file for a short audio file:

```
{
    "jobName": "job ID",
    "accountId": "account ID",
	"results": {
		"transcripts": [{
			"transcript": "Professional answer."
		}],
		"speaker_labels": {
			"speakers": 1,
			"segments": [{
				"start_time": "0.000000",
				"speaker_label": "spk_0",
				"end_time": "1.430",
				"items": [{
					"start_time": "0.100",
					"speaker_label": "spk_0",
					"end_time": "0.690"
				}, {
					"start_time": "0.690",
					"speaker_label": "spk_0",
					"end_time": "1.210"
				}]
			}]
		},
		"items": [{
			"start_time": "0.100",
			"end_time": "0.690",
			"alternatives": [{
				"confidence": "0.8162",
				"content": "Professional"
			}],
			"type": "pronunciation"
		}, {
			"start_time": "0.690",
			"end_time": "1.210",
			"alternatives": [{
				"confidence": "0.9939",
				"content": "answer"
			}],
			"type": "pronunciation"
		}, {
			"alternatives": [{
				"content": "."
			}],
			"type": "punctuation"
		}]
	},
	"status": "COMPLETED"
}
```