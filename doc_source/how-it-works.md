# How Amazon Transcribe works<a name="how-it-works"></a>

Amazon Transcribe analyzes audio files that contain speech and uses advanced machine learning techniques to transcribe the voice data into text\. You can then use the transcription as you would any text document\.

To transcribe an audio file, Amazon Transcribe uses three operations:
+ [StartTranscriptionJob](API_StartTranscriptionJob.md) – Starts a batch job to transcribe the speech in an audio file to text\.
+ [ListTranscriptionJobs](API_ListTranscriptionJobs.md) – Returns a list of transcription jobs that have been started\. You can specify the status of the jobs that you want the operation to return\. For example, you can get a list of all pending jobs, or a list of completed jobs\.
+ [GetTranscriptionJob](API_GetTranscriptionJob.md) – Returns the result of a transcription job\. The response contains a link to a JSON file containing the results\.

To transcribe streaming audio to text, Amazon Transcribe provides one operation:
+ [StartStreamTranscription](API_streaming_StartStreamTranscription.md) – Starts a bi\-directional HTTP/2 stream where audio is streamed to Amazon Transcribe and the transcription results are streamed to your application\.

You can also start a WebSocket protocol stream to send audio the Amazon Transcribe\. For more information, see [Using Amazon Transcribe streaming with WebSockets](websocket.md)\.

You can use Amazon Transcribe to create and manage custom vocabularies for your solution\. A custom vocabulary gives Amazon Transcribe more information about how to process speech in an audio clip\.
+ [CreateVocabulary](API_CreateVocabulary.md) – Creates a custom vocabulary that you can use in your transcription jobs\.
+ [DeleteVocabulary](API_DeleteVocabulary.md) – Deletes a custom vocabulary from your account\.
+ [GetVocabulary](API_GetVocabulary.md) – Gets information about a custom vocabulary and a URL that you can use to download the contents of a vocabulary\.
+ [ListVocabularies](API_ListVocabularies.md) – Gets a list of custom vocabularies in your account\.
+ [UpdateVocabulary](API_UpdateVocabulary.md) – Updates an existing vocabulary\.

You can transcribe speech in any of the following languages:
+ Gulf Arabic \(ar\-AE\)
+ Modern Standard Arabic \(ar\-SA\)
+ Mandarin Chinese \- Mainland \(zh\-CN\)
+ Dutch \(nl\-NL\)
+ Australian English \(en\-AU\)
+ British English \(en\-GB\)
+ Indian English \(en\-IN\)
+ Irish English \(en\-IE\)
+ Scottish English \(en\-AB\)
+ US English \(en\-US\)
+ Welsh English \(en\-WL\)
+ French \(fr\-FR\)
+ Canadian French \(fr\-CA\)
+ Farsi \(fa\-IR\)
+ German \(de\-DE\)
+ Swiss German \(de\-CH\)
+ Hebrew \(he\-IL\)
+ Indian Hindi \(hi\-IN\)
+ Indonesian \(id\-ID\)
+ Italian \(it\-IT\)
+ Japanese \(ja\-JP\)
+ Korean \(ko\-KR\)
+ Malay \(ms\-MY\)
+ Portuguese \(pt\-PT\)
+ Brazilian Portuguese \(pt\-BR\)
+ Russian \(ru\-RU\)
+ Spanish \(es\-ES\)
+ US Spanish \(es\-US\)
+ Tamil \(ta\-IN\)
+ Telugu \(te\-IN\)
+ Turkish \(tr\-TR\)

For information on the languages available for streaming audio transcription, see [What is Amazon Transcribe?](transcribe-whatis.md)\.

Amazon Transcribe has the capability to transcribe accented speech of individuals who are non\-native speakers of a language\. For example, Amazon Transcribe enables you to transcribe US English \(en\-US\) audio spoken with a German \(de\-DE\) accent\.

**Topics**
+ [Speech input](input.md)
+ [Transcribing numbers and punctuation](how-numbers.md)
+ [Alternative transcriptions](how-alternatives.md)
+ [Transcribing streaming audio](how-streaming-transcription.md)
+ [Custom vocabularies](how-vocabulary.md)
+ [Automatic content redaction](content-redaction.md)
+ [Job queuing](job-queuing.md)