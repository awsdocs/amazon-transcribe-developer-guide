# How Amazon Transcribe Works<a name="how-it-works"></a>

Amazon Transcribe analyzes audio files that contain speech and uses advanced machine learning techniques to transcribe the voice data into text\. You can then use the transcription as you would any text document\.

To transcribe an audio file, Amazon Transcribe uses three operations:

+ [StartTranscriptionJob](API_StartTranscriptionJob.md)—Starts an asynchronous job to transcribe the speech in an audio file to text\.

+ [ListTranscriptionJobs](API_ListTranscriptionJobs.md) – Returns a list of transcription jobs that have been started\. You can specify the status of the jobs that you want the operation to return\. For example, you can get a list of all pending jobs, or a list of completed jobs\.

+ [GetTranscriptionJob](API_GetTranscriptionJob.md) – Returns the result of a transcription job\. The response contains a link to a JSON file containing the results\.

You can also use the Amazon Transcribe to create and manage custom vocabularies for your solution\. A custom vocabulary gives Amazon Transcribe more information about how to process speech in an audio clip\.

+ [CreateVocabulary](API_CreateVocabulary.md) – Creates a custom vocabulary that you can use in your transcription jobs\.

+ [DeleteVocabulary](API_DeleteVocabulary.md) – Deletes a custom vocabulary from your account\.

+ [GetVocabulary](API_GetVocabulary.md) – Gets information about a custom vocabulary and a URL that you can use to download the contents of a vocabulary\.

+ [ListVocabularies](API_ListVocabularies.md) – Gets a list of custom vocabularies in your account\.

+ [UpdateVocabulary](API_UpdateVocabulary.md) – Updates an existing vocabulary\.

You can use Amazon Transcribe to convert English and Spanish audio to text\. You can use Amazon Translate to translate the text into another language, and use Amazon Polly to speak the text\.

## Speech Input<a name="input"></a>

To transcribe an audio file, you use a transcription job\. You store the file as an object in an Amazon S3 bucket\. The input file must be: 

+ In FLAC, MP3, MP4, or WAV file format

+ Less than 2 hours in length

You must specify the language and format of the input file\. 

For best results: 

+ Use a lossless format, such as FLAC or WAV, with PCM 16\-bit encoding\.

+ Use a sample rate of 8000 Hz for low\-fidelity audio and 16000 Hz for high\-fidelity audio\.

## Identifying Speakers<a name="how-diarization"></a>

You can have Amazon Transcribe identify the different speakers in an audio clip, a process known as *diarization* or *speaker identification*\. When you enable speaker identification, Amazon Transcribe labels each fragment with the speaker that it identified\. 

You can specify that Amazon Transcribe identify between 2 and 10 speakers in the audio clip\. You get the best performance when the number of speakers that you ask to identify matches the number of speakers in the input audio\.

To turn on speaker identification, set the `MaxSpeakerLabels` and `ShowSpeakerLabels` field of the `Settings` field when you make a call to the [StartTranscriptionJob](API_StartTranscriptionJob.md) operation\. You must set both fields or else Amazon Transcribe will return an exception\.

## Custom Vocabularies<a name="how-vocabulary"></a>

You can give Amazon Transcribe more information about how to process speech in your input file by creating a custom vocabulary\. A *custom vocabulary* is a list of specific words that you want Amazon Transcribe to recognize in your audio input\. These are generally domain\-specific words and phrases, words that Amazon Transcribe isn't recognizing, or non\-English names\.

You specify the custom vocabulary as a list\. Each entry can be a single word or a phrase\. You separate the words of a phrase with a hyphen \(\-\)\. For example, you type **IP address** as **IP\-address**\. For more information about creating a custom vocabulary list, see [Create a Custom Vocabulary](custom-vocabulary-files.md)\.

To create a custom vocabulary, use the [CreateVocabulary](API_CreateVocabulary.md) or the [Amazon Transcribe console](https://console.aws.amazon.com/transcribe/)\. After you submit the `CreateVocabulary` request, Amazon Transcribe processes the vocabulary\. To see the processing status of the vocabulary, use the [GetVocabulary](API_GetVocabulary.md) operation\.

To use the custom vocabulary, set the `VocabularyName` field of the `Settings` field when you make a call to the [StartTranscriptionJob](API_StartTranscriptionJob.md) operation\. 

## Output JSON<a name="output"></a>

When Amazon Transcribe completes a transcription job, it creates a JSON file that contains the results and saves the file in an S3 bucket\. The file is identified by a user\-specific URI\. Use the URI to get the results\.

The following is the JSON file for a short audio file:

```
{
    "jobName": "job ID",
    "accountId": "account ID",
    "results": {
        "transcripts": [
            {
                "transcript": " that's no answer"
            }
        ],
        "items": [
            {
                "start_time": "0.180",
                "end_time": "0.470",
                "alternatives": [
                    {
                        "confidence": 0.84,
                        "content": "that's"
                    }
                ],
                "type": "pronunciation"
            },
            {
                "start_time": "0.0",
                "end_time": "0.1",
                "alternatives": [
                    {
                        "confidence": "1.0000",
                        "content": "no"
                    }
                ],
                "type": "pronunciation"
            },
            {
                "start_time": "0.1",
                "end_time": "0.2",
                "alternatives": [
                    {
                        "confidence": "1.0000",
                        "content": "answer"
                    }
                ],
                "type": "pronunciation"
            }
        ],
        "speaker_labels": {
            "speakers": 2,
            "items": [
                {
                    "start_time": 0,
                    "end_time": 0.1,
                    "speaker": "sp_0"
                },
                {
                    "start_time": 0.1,
                    "end_time": 0.2,
                    "speaker": "sp_1"
                }
            ]
        },
        "status": "COMPLETED"
    }
}
```