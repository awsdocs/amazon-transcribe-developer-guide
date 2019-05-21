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
+ Indian English \(en\-IN\)
+ US English \(en\-US\)
+ French \(fr\-FR\)
+ Canadian French \(fr\-CA\)
+ German \(de\-DE\)
+ Indian Hindi \(hi\-IN\)
+ Italian \(it\-IT\)
+ Korean \(ko\-KR\)
+ Brazilian Portuguese \(pt\-BR\)
+ Spanish \(es\-ES\)
+ US Spanish \(es\-US\)

You can use streaming transcription for the following languages:
+ British English \(en\-GB\)
+ US English \(en\-US\)
+ French \(fr\-FR\)
+ Canadian French \(fr\-CA\)
+ US Spanish \(es\-US\)

**Topics**
+ [Speech Input](input.md)
+ [Identifying Speakers](how-diarization.md)
+ [Transcribing Streaming Audio](how-streaming-transcription.md)
+ [Channel Identification](how-channel-id.md)
+ [Custom Vocabularies](how-vocabulary.md)