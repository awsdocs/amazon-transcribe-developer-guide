# How Amazon Transcribe works<a name="how-it-works"></a>

Amazon Transcribe analyzes audio files that contain speech and uses advanced machine learning techniques to transcribe the voice data into text\. You can then use the transcription as you would any text document\.

Each language has its own *language code* that you can use to specify the language of your audio or video file\.

You can transcribe an uploaded file or live\-stream audio\. Procesing an uploaded file is referred to as a **batch transcription job**, while using live audio is referred to as a **streaming transcription**\. For information on supported file containers and formats for both batch and streaming options, see [Speech input](input.md)\.

To transcribe an audio file, Amazon Transcribe uses three APIs:
+ [ StartTranscriptionJob ](API_StartTranscriptionJob.md) – Starts a batch job to transcribe the speech in an audio file to text\.
+ [ ListTranscriptionJobs ](API_ListTranscriptionJobs.md) – Returns a list of transcription jobs that have been started\. You can specify the status of the jobs that you want the API to return\. For example, you can get a list of all pending jobs, or a list of completed jobs\.
+ [ GetTranscriptionJob ](API_GetTranscriptionJob.md) – Returns the result of a transcription job\. The response contains a link to a JSON file containing the results\.

To transcribe streaming audio to text, Amazon Transcribe uses one API:
+ [ StartStreamTranscription ](API_streaming_StartStreamTranscription.md) – Starts a bi\-directional HTTP/2 stream where audio is streamed to Amazon Transcribe and the transcription results are streamed to your application\.

You can also start a WebSocket protocol stream to send audio the Amazon Transcribe\. For more information, see [Using Amazon Transcribe streaming with WebSockets](websocket.md)\.

You can use Amazon Transcribe to create and manage custom vocabularies for your solution\. A custom vocabulary gives Amazon Transcribe more information about how to process speech in an audio clip\.
+ [ CreateVocabulary ](API_CreateVocabulary.md) – Creates a custom vocabulary that you can use in your transcription jobs\.
+ [ DeleteVocabulary ](API_DeleteVocabulary.md) – Deletes a custom vocabulary from your account\.
+ [ GetVocabulary ](API_GetVocabulary.md) – Gets information about a custom vocabulary and a URL that you can use to download the contents of a vocabulary\.
+ [ ListVocabularies ](API_ListVocabularies.md) – Gets a list of custom vocabularies in your account\.
+ [ UpdateVocabulary ](API_UpdateVocabulary.md) – Updates an existing vocabulary\.


**Supported languages and language\-specific features**  

| Language | Language Code | [Speech input](input.md) | [Transcribing digits](how-numbers.md) | [Acronyms](how-vocabulary.md#create-vocabulary-acronym) | [Custom language models](custom-language-models.md) | [Content redaction](content-redaction.md) | [Call analytics](call-analytics.md) | 
| --- | --- | --- | --- | --- | --- | --- | --- | 
| [Afrikaans](charsets.md#char-afrikaans) | af\-ZA | batch only | no | yes | no | no | no | 
| [Arabic](charsets.md#char-arabic), Gulf | ar\-AE | batch only | no | no | no | no | yes | 
| [Arabic](charsets.md#char-arabic), Modern Standard | ar\-SA | batch only | no | no | no | no | no | 
| [Chinese, Simplified](charsets.md#char-chinese-man-cn) | zh\-CN | batch, streaming | no | no | no | no | yes | 
| [Chinese, Traditional](charsets.md#char-chinese-man-tw) | zh\-TW | batch only | no | no | no | no | no | 
| [Danish](charsets.md#char-danish) | da\-DK | batch only | no | yes | no | no | no | 
| [Dutch](charsets.md#char-dutch) | nl\-NL | batch only | no | yes | no | no | no | 
| [English](charsets.md#char-english), Australian | en\-AU | batch, streaming | yes | yes | yes | no | yes | 
| [English](charsets.md#char-english), British | en\-GB | batch, streaming | yes | yes | yes | no | yes | 
| [English](charsets.md#char-english), Indian | en\-IN | batch only | yes | yes | no | no | yes | 
| [English](charsets.md#char-english), Irish | en\-IE | batch only | yes | yes | no | no | yes | 
| [English](charsets.md#char-english), New Zealand | en\-NZ | batch only | yes | yes | no | no | no | 
| [English](charsets.md#char-english), Scottish | en\-AB | batch only | yes | yes | no | no | yes | 
| [English](charsets.md#char-english), South African | en\-ZA | batch only | yes | yes | no | no | no | 
| [English](charsets.md#char-english), US | en\-US | batch, streaming | yes | yes | yes | yes \(batch\) | yes | 
| [English](charsets.md#char-english), Welsh | en\-WL | batch only | yes | yes | no | no | yes | 
| [French](charsets.md#char-french) | fr\-FR | batch, streaming | no | yes | no | no | yes | 
| [French](charsets.md#char-french), Canadian | fr\-CA | batch, streaming | no | yes | no | no | yes | 
| [Farsi](charsets.md#char-farsi) | fa\-IR | batch only | no | no | no | no | no | 
| [German](charsets.md#char-german) | de\-DE | batch, streaming | yes | yes | no | no | yes | 
| [German](charsets.md#char-german), Swiss | de\-CH | batch only | yes | yes | no | no | yes | 
| [Hebrew](charsets.md#char-hebrew) | he\-IL | batch only | no | no | no | no | no | 
| [Hindi](charsets.md#char-hindi), Indian | hi\-IN | batch only | no | yes | yes | no | yes | 
| [Indonesian](charsets.md#char-indonesian) | id\-ID | batch only | no | yes | no | no | no | 
| [Italian](charsets.md#char-italian) | it\-IT | batch, streaming | no | yes | no | no | yes | 
| [Japanese](charsets.md#char-japanese) | ja\-JP | batch, streaming | no | no | no | no | yes | 
| [Korean](charsets.md#char-korean) | ko\-KR | batch, streaming | no | no | no | no | yes | 
| [Malay](charsets.md#char-malay) | ms\-MY | batch only | no | yes | no | no | no | 
| [Portuguese](charsets.md#char-portuguese) | pt\-PT | batch only | no | yes | no | no | yes | 
| [Portuguese](charsets.md#char-portuguese), Brazilian | pt\-BR | batch, streaming | no | yes | no | no | yes | 
| [Russian](charsets.md#char-russian) | ru\-RU | batch only | no | no | no | no | no | 
| [Spanish](charsets.md#char-spanish) | es\-ES | batch only | no | yes | no | no | yes | 
| [Spanish](charsets.md#char-spanish), US | es\-US | batch, streaming | no | yes | yes | no | yes | 
| [Tamil](charsets.md#char-tamil) | ta\-IN | batch only | no | no | no | no | no | 
| [Telugu](charsets.md#char-telugu) | te\-IN | batch only | no | no | no | no | no | 
| [Thai](charsets.md#char-thai) | th\-TH | batch only | no | yes | no | no | no | 
| [Turkish](charsets.md#char-turkish) | tr\-TR | batch only | no | yes | no | no | no | 