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

In the console you turn speaker identification on by enabling **Speaker identification**\. and then specifying the number of speakers to identify\. If you don't set the number of speakers to identify, Amazon Transcribe will identify 2\.

To turn on speaker identification using the API, set the `MaxSpeakerLabels` and `ShowSpeakerLabels` field of the `Settings` field when you make a call to the [StartTranscriptionJob](API_StartTranscriptionJob.md) operation\. You must set both fields or else Amazon Transcribe will return an exception\.

When Amazon Transcribe completes a transcription job, it creates a JSON file that contains the results and saves the file in an S3 bucket\. The file is identified by a user\-specific URI\. Use the URI to get the results\.

The following is the JSON file for a short audio file transcribed with speaker identification enabled:

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

## Channel Identification<a name="how-channel-id"></a>

When an audio file has multiple channels that you want to transcribe into separate transcriptions that identify the channel that contains the speech, use *channel identification* \. For example, if you have a customer support representative on one channel and a customer on another, use channel identification to create a transcription that is identified by each channel and a single transcription that combines them\.

Amazon Transcribe splits your audio file into multiple channels and transcribes the channels separately\. After transcribing all channels, Amazon Transcribe also merges the transcriptions to create a single transcription\. It returns all of the transcriptions in a single result file\.

Speakers' utterances are ordered by their start time\. An *utterance* is a unit of speech on the audio channel that is typically separated from other utterances by silence\. If an utterance on one channel overlaps one on another channel, Amazon Transcribe orders them in the transcription by their start times\. Utterances that overlap in the input audio don't overlap in the transcription output\.

You can enable channel identification in the Amazon Transcribe console or with the API\. In the console, choose **Channel identification** when you create the transcription job\. When you use the API, set the `ChannelIdentification` flag when you call the [StartTranscriptionJob](API_StartTranscriptionJob.md) operation\. 

The following is the abbreviated output for a conversation on two channels:

```
{
  "jobName": "job id",
  "accountId": "account id",
  "results": {
    "transcripts": [
      {
        "transcript": "When you try ... It seems to ..."
      }
    ],
    "channel_labels": {
      "channels": [
        {
          "channel_label": "ch_0",
          "items": [
            {
              "start_time": "12.282",
              "end_time": "12.592",
              "alternatives": [
                {
                  "confidence": "1.0000",
                  "content": "When"
                }
              ],
              "type": "pronunciation"
            },
            {
              "start_time": "12.592",
              "end_time": "12.692",
              "alternatives": [
                {
                  "confidence": "0.8787",
                  "content": "you"
                }
              ],
              "type": "pronunciation"
            },
            {
              "start_time": "12.702",
              "end_time": "13.252",
              "alternatives": [
                {
                  "confidence": "0.8318",
                  "content": "try"
                }
              ],
              "type": "pronunciation"
            },
            Transcription abbreviated
         ]
      },
      {
          "channel_label": "ch_1",
          "items": [
            {
              "start_time": "12.379",
              "end_time": "12.589",
              "alternatives": [
                {
                  "confidence": "0.5645",
                  "content": "It"
                }
              ],
              "type": "pronunciation"
            },
            {
              "start_time": "12.599",
              "end_time": "12.659",
              "alternatives": [
                {
                  "confidence": "0.2907",
                  "content": "seems"
                }
              ],
              "type": "pronunciation"
            },
            {
              "start_time": "12.669",
              "end_time": "13.029",
              "alternatives": [
                {
                  "confidence": "0.2497",
                  "content": "to"
                }
              ],
              "type": "pronunciation"
            },
            Transcription abbreviated
        ]
    }
}
```

## Custom Vocabularies<a name="how-vocabulary"></a>

You can give Amazon Transcribe more information about how to process speech in your input file by creating a custom vocabulary\. A *custom vocabulary* is a list of specific words that you want Amazon Transcribe to recognize in your audio input\. These are generally domain\-specific words and phrases, words that Amazon Transcribe isn't recognizing, or non\-English names\.

You specify the custom vocabulary as a list\. Each entry can be a single word or a phrase\. You separate the words of a phrase with a hyphen \(\-\)\. For example, you type **IP address** as **IP\-address**\. For more information about creating a custom vocabulary list, see [Create a Custom Vocabulary](#create-vocabulary)\.

To create a custom vocabulary, use the [CreateVocabulary](API_CreateVocabulary.md) operation or the [Amazon Transcribe console](https://console.aws.amazon.com/transcribe/)\. After you submit the `CreateVocabulary` request, Amazon Transcribe processes the vocabulary\. To see the processing status of the vocabulary, use the [GetVocabulary](API_GetVocabulary.md) operation\.

To use the custom vocabulary, set the `VocabularyName` field of the `Settings` field when you make a call to the [StartTranscriptionJob](API_StartTranscriptionJob.md) operation\. 

### Create a Custom Vocabulary<a name="create-vocabulary"></a>

A custom vocabulary is a list of words that you want Amazon Transcribe to recognize\. Each entry in the list is a single word or phrase\. Each entry must contain:
+ fewer than 256 characters
+ only characters from the allowed character set

For valid character sets, see [English Character Set](#char-english) and [Spanish Character Set](#char-spanish)\.

The size limit for a custom vocabulary is 50 KB\.

When typing a multi\-word term or phrase into the custom vocabulary, separate the words with a hyphen \(\-\) instead of a space\. For example, type the term **IP address** as **IP\-address**\. 

Create a custom vocabulary by using the [CreateVocabulary](API_CreateVocabulary.md) operation or the [Amazon Transcribe console](https://console.aws.amazon.com/transcribe)\. If you use the Amazon Transcribe console to create a custom vocabulary, you can provide the entries in either a text file or a comma\-separated values file \(CSV\)\. 

#### Creating a Custom Vocabulary with a Text File \(Console\)<a name="creating-text"></a>

When you use a text file, place each word or phrase on a separate line\. Save the file with the extension \.txt\. The following is an example input file in text format:

```
apple
bear
coffee-dog
five
earring
good-morning
hi
IPhone
Etienne
```

#### Creating a Custom Vocabulary with a Comma\-separated Values File \(Console\)<a name="creating-csv"></a>

In a comma\-separated values \(CSV\) file, separate each word or phrase with a comma\. You can put multiple entries on one line, and use line returns to break long lines\. Save the file with the extension "\.csv"\. 

The following is an example input file in CSV format:

```
apple,bear,coffee-dog,
five,earring,good-morning,
hi,IPhone,Etienne
```

### English Character Set<a name="char-english"></a>

For English custom vocabularies, you can use the following characters:
+ a \- z
+ A \- Z
+ \- \(hyphen\)

### Spanish Character Set<a name="char-spanish"></a>

For Spanish custom vocabularies, you can use the following characters:
+ a \- z
+ A \- Z
+ \- \(hyphen\)

You can also use the following Unicode characters:


| Code | Character | Code | Character | 
| --- | --- | --- | --- | 
| 00C1 | Á | 00E1 | á | 
| 00C9 | É | 00E9 | é | 
| 00CD | Í | 00ED | í | 
| 00D3 | Ó | 0XF3 | ó | 
| 00DA | Ú | 00FA | ú | 
| 00D1 | Ñ | 0XF1 | ñ | 
| 00FC | ü |   |   | 