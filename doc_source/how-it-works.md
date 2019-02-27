# How Amazon Transcribe Works<a name="how-it-works"></a>

Amazon Transcribe analyzes audio files that contain speech and uses advanced machine learning techniques to transcribe the voice data into text\. You can then use the transcription as you would any text document\.

To transcribe an audio file, Amazon Transcribe uses three operations:
+ [StartTranscriptionJob](API_StartTranscriptionJob.md) – Starts an asynchronous job to transcribe the speech in an audio file to text\.
+ [ListTranscriptionJobs](API_ListTranscriptionJobs.md) – Returns a list of transcription jobs that have been started\. You can specify the status of the jobs that you want the operation to return\. For example, you can get a list of all pending jobs, or a list of completed jobs\.
+ [GetTranscriptionJob](API_GetTranscriptionJob.md) – Returns the result of a transcription job\. The response contains a link to a JSON file containing the results\.

To transcribe streaming audio to text, Amazon Transcribe provides one operation:
+ [StartStreamTranscription](API_streaming_StartStreamTranscription.md) – Starts a bi\-directional HTTP/2 stream where audio is streamed to Amazon Transcribe and the transcription results are streamed to your application\.

You can also use the Amazon Transcribe to create and manage custom vocabularies for your solution\. A custom vocabulary gives Amazon Transcribe more information about how to process speech in an audio clip\.
+ [CreateVocabulary](API_CreateVocabulary.md) – Creates a custom vocabulary that you can use in your transcription jobs\.
+ [DeleteVocabulary](API_DeleteVocabulary.md) – Deletes a custom vocabulary from your account\.
+ [GetVocabulary](API_GetVocabulary.md) – Gets information about a custom vocabulary and a URL that you can use to download the contents of a vocabulary\.
+ [ListVocabularies](API_ListVocabularies.md) – Gets a list of custom vocabularies in your account\.
+ [UpdateVocabulary](API_UpdateVocabulary.md) – Updates an existing vocabulary\.

You can transcribe speech in any of the following languages:
+ Australian English \(en\-AU\)
+ British English \(en\-GB\)
+ US English \(en\-US\)
+ French \(fr\-FR\)
+ Canadian French \(fr\-CA\)
+ Italian \(it\-IT\)
+ Brazilian Portuguese \(pt\-BR\)
+ US Spanish \(es\-US\)

You can use streaming transcription for the following languages:
+ US English \(en\-US\)
+ US Spanish \(es\-US\)

## Speech Input<a name="input"></a>

To transcribe an audio file, you use a transcription job\. You store the file as an object in an Amazon S3 bucket\. The input file must be: 
+ In FLAC, MP3, MP4, or WAV file format
+ Less than 2 hours in length

You must specify the language and format of the input file\. 

For best results: 
+ Use a lossless format, such as FLAC or WAV, with PCM 16\-bit encoding\.
+ Use a sample rate of 8000 Hz for telephone audio\.

## Identifying Speakers<a name="how-diarization"></a>

You can have Amazon Transcribe identify the different speakers in an audio clip, a process known as *diarization* or *speaker identification*\. When you enable speaker identification, Amazon Transcribe labels each fragment with the speaker that it identified\. 

You can specify that Amazon Transcribe identify between 2 and 10 speakers in the audio clip\. You get the best performance when the number of speakers that you ask to identify matches the number of speakers in the input audio\.

To turn on speaker identification, set the `MaxSpeakerLabels` and `ShowSpeakerLabels` field of the `Settings` field when you make a call to the [StartTranscriptionJob](API_StartTranscriptionJob.md) operation\. You must set both fields or else Amazon Transcribe will return an exception\.

## Transcribing Streaming Audio<a name="how-streaming-transcription"></a>

Streaming transcription takes a stream of your audio data and transcribes it in real time\. It uses HTTP/2 streams so that the results of the transcription can be returned to your application while you send more audio to Amazon Transcribe\. You can use streaming transcription when you want to make the results of live audio transcription available immediately, or when you have an audio file that you want to process as it is transcribed\.

You can use streaming transcription with the following languages:
+ US English \(en\-US\)
+ US Spanish \(es\-US\)

## Channel Identification<a name="how-channel-id"></a>

When an audio file has multiple channels that you want to transcribe into separate transcriptions that identify the channel that contains the speech, use *channel identification*\. For example, if you have a customer support representative on one channel and a customer on another, use channel identification to create a transcription that is identified by each channel and a single transcription that combines them\.

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

You specify the custom vocabulary as a list\. Each entry can be a single word or a phrase\. You separate the words of a phrase with a hyphen \(\-\)\. For example, you type **Los Angeles** as **Los\-Angeles**\. 

Enter acronyms or other words whose letters should be pronounced individually as single letters followed by dots, such **A\.B\.C\.** or **C\.N\.N\.**\. To enter the plural form of an acronym, such as "ABCs", separate the "s" from the acronym with a hyphen: "**A\.B\.C\.\-s**"\. You can use either upper\- or lower\-case letters to enter an acronym\. Acronyms are supported only by US English \(en\-US\)\.

For more information about creating a custom vocabulary list, see [Create a Custom Vocabulary](#create-vocabulary)\.

To create a custom vocabulary, use the [CreateVocabulary](API_CreateVocabulary.md) or the [Amazon Transcribe console](https://console.aws.amazon.com/transcribe/)\. After you submit the `CreateVocabulary` request, Amazon Transcribe processes the vocabulary\. To see the processing status of the vocabulary, use the [GetVocabulary](API_GetVocabulary.md) operation\.

To use the custom vocabulary, set the `VocabularyName` field of the `Settings` field when you make a call to the [StartTranscriptionJob](API_StartTranscriptionJob.md) operation\. 

### Create a Custom Vocabulary<a name="create-vocabulary"></a>

A custom vocabulary is a list of words that you want Amazon Transcribe to recognize\. Each entry in the list is a single word or phrase\. Each entry must contain:
+ fewer than 256 characters
+ only characters from the allowed character set

For valid character sets, see [English Character Set](#char-english), [French Character Set](#char-french), [Italian Character Set](#char-italian), [Portuguese Character Set](#char-portuguese), and [Spanish Character Set](#char-spanish)\.

The size limit for a custom vocabulary is 50 KB\.

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
Etienne
A.B.C.
A.B.C.-s
```

#### Creating a Custom Vocabulary with a Comma\-separated Values File \(Console\)<a name="creating-csv"></a>

In a comma\-separated values \(CSV\) file, separate each word or phrase with a comma\. You can put multiple entries on one line, and use line returns to break long lines\. Save the file with the extension "\.csv"\. 

The following is an example input file in CSV format:

```
apple,bear,coffee-dog,
five,earring,good-morning,
hi,Etienne,A.B.C.,A.B.C.-s
```

### English Character Set<a name="char-english"></a>

For English custom vocabularies, you can use the following characters:
+ a \- z
+ A \- Z
+ \- \(hyphen\)

### French Character Set<a name="char-french"></a>

For French custom vocabularies, you can use the following characters:
+ a \- z
+ A \- Z
+ ' \(apostrophe\)
+ \- \(hyphen\)


| Character | Code | Character | Code | 
| --- | --- | --- | --- | 
| À | 00C0 | à | 00E0 | 
| Â | 00C2 | â | 00E2 | 
| Ç | 00C7 | ç | 00E7 | 
| È | 00C8 | è | 00E8 | 
| É | 00C9 | é | 00E9 | 
| Ê | 00CA | ê | 00EA | 
| Ë | 00CB | ë | 00EB | 
| Î | 00CE | î | 00EE | 
| Ï | 00CF | ï | 00EF | 
| Ô | 00D4 | ô | 00F4 | 
| Ö | 00D6 | ö | 00F6 | 
| Ù | 00D9 | ù | 00F9 | 
| Û | 00DB | û | 00FB | 
| Ü | 00DC | ü | 00FC | 

### Italian Character Set<a name="char-italian"></a>

For Italian custom vocabularies, you can use the following characters:
+ a \- z
+ A \- Z
+ ' \(apostrophe\)
+ \- \(hyphen\)

You can also use the following Unicode characters:


| Character | Code | Character | Code | 
| --- | --- | --- | --- | 
| À | 00C0 | à | 00E0 | 
| Ä | 00C4 | ä | 00E4 | 
| Ç | 00C7 | ç | 00E7 | 
| È | 00C8 | è | 00E8 | 
| É | 00C9 | é | 00E9 | 
| Ê | 00CA | ê | 00EA | 
| Ë | 00CB | ë | 00EB | 
| Ì | 00CC | ì | 00EC | 
| Ò | 00D2 | ò | 00F2 | 
| Ù | 00D9 | ù | 00F9 | 
| Ü | 00DC | ü | 00FC | 

### Portuguese Character Set<a name="char-portuguese"></a>

For Portuguese custom vocabularies, you can use the following characters:
+ a \- z
+ A \- Z
+ ' \(apostrophe\)
+ \- \(hyphen\)

You can also use the following Unicode characters:


| Character | Code | Character | Code | 
| --- | --- | --- | --- | 
| À | 00C0 | à | 00E0 | 
| Á | 00C1 | á | 00E1 | 
| Â | 00C2 | â | 00E2 | 
| Ã | 00C3 | ã | 00E3 | 
| Ä | 00C4 | ä | 00E4 | 
| Ç | 00C7 | ç | 00E7 | 
| È | 00C8 | è | 00E8 | 
| É | 00C9 | é | 00E9 | 
| Ê | 00CA | ê | 00EA | 
| Ë | 00CB | ë | 00EB | 
| Í | 00CD | í | 00ED | 
| Ñ | 00D1 | ñ | 00F1 | 
| Ó | 00D3 | ó | 00F3 | 
| Ô | 00D4 | ô | 00F4 | 
| Õ | 00D5 | õ | 00F5 | 
| Ö | 00D6 | ö | 00F6 | 
| Ú | 00DA | ú | 00FA | 
| Ü | 00DC | ü | 00FC | 

### Spanish Character Set<a name="char-spanish"></a>

For Spanish custom vocabularies, you can use the following characters:
+ a \- z
+ A \- Z
+ ' \(apostrophe\)
+ \- \(hyphen\)

You can also use the following Unicode characters:


| Character | Code | Character | Code | 
| --- | --- | --- | --- | 
| Á | 00C1 | á | 00E1 | 
| É | 00C9 | é | 00E9 | 
| Í | 00CD | ë | 00ED | 
| Ó | 00D3 | ó | 0XF3 | 
| Ú | 00DA | ú | 00FA | 
| Ñ | 00D1 | ñ | 0XF1 | 
| ü | 00FC |   |   | 