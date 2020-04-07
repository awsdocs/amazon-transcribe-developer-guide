# Identifying Speakers<a name="how-diarization-med"></a>

You can have Amazon Transcribe Medical identify the different speakers in an audio file, a process known as *diarization* or *speaker identification*\. When you enable speaker identification, Amazon Transcribe Medical labels each fragment with the speaker that it identified\. 

You can specify that Amazon Transcribe Medical identify between 2 and 10 speakers in the audio clip\. For best results, match the number of speakers that you ask to identify to the number of speakers in the input audio\.

To turn on speaker identification, set the `MaxSpeakerLabels` and `ShowSpeakerLabels` field of the `Settings` field when you call the [StartMedicalTranscriptionJob](API_StartMedicalTranscriptionJob.md) operation\. You must set both fields or else Amazon Transcribe Medical returns an exception\.

When Amazon Transcribe Medical completes a transcription job, it creates a JSON file that contains the results\. The file is saved in the S3 bucket you've previously specified\. The file is identified by a URI specific to your file and bucket\. Use the URI to access the results\.

The following is the JSON file for a short audio file\.

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