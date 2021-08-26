# Identifying the language of your media files<a name="auto-lang-id"></a>

Amazon Transcribe is able to automatically identify the predominant language in a media file without you having to specify a language code\. Automatic language identification can be used for any batch transcription with the API or the [Amazon Transcribe console](https://console.aws.amazon.com/transcribe/)\. For a list of languages, see [Supported languages and language\-specific features](how-it-works.md#table-language-matrix)\.

To identify the language with greater accuracy, you can specify a list of languages you think are present in your collection of media files\. From that list, Amazon Transcribe chooses the language with the greatest confidence score to transcribe your audio\. A score with a larger value indicates that Amazon Transcribe is more confident it identified the language correctly\. For best results, if you are certain of the language spoken in each of the audio files, specify a language code\. For more information, see the [StartTranscriptionJob](API_StartTranscriptionJob.md) API\.

**Note**  
Media files are transcribed in a single language, even if they contain speech in two or more languages\. Amazon Transcribe transcribes the audio according to the predominant language identified in the file\.

Some Amazon Transcribe features require you to specify a language code\. Automatic language identification is not supported with the following features enabled:
+ Custom language models
+ Custom vocabularies
+ Vocabulary filtering
+ Automatic content redaction

To increase the chance of identifying the language successfully, media files should have at least 30 seconds of speech\.

**Topics**
+ [Transcribing with automatic language identification](transcribe-lang-id.md)
+ [Getting notifications using Automatic language identification](lang-id-cloudwatch.md)