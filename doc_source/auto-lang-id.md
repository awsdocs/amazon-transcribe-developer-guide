# Identifying the Language of Your Media Files<a name="auto-lang-id"></a>

When you generate transcriptions, Amazon Transcribe can automatically identify the predominant language in a media file with *automatic language identification*\. This enables you to transcribe your files without specifying a language code for each individual file\.

Use automatic language identification to:
+ Transcribe customer service recordings in countries where multiple languages are spoken\.
+ Transcribe a media library that has files in different languages\.
+ Label media content with the language automatically identified by Amazon Transcribe\.
+ Identify incorrectly labeled audio and video content for media content operations\. For example, you can identify videos and podcasts labeled with the incorrect language\. 

Media files are transcribed in a single language, even if they contain speech in two or more languages\. Amazon Transcribe transcribes the audio according to the primary language found in the file\. Amazon Transcribe can automatically identify any language that can be used for batch transcription with the API or the Amazon Transcribe console\. For a list of languages, see [What Is Amazon Transcribe?](what-is-transcribe.md)\.

To identify the language with greater accuracy, you can specify a list of languages that you think are present in your collection of media files\. From that list, Amazon Transcribe chooses the language with the greatest confidence score to transcribe your audio\. A score with a larger value indicates that Amazon Transcribe is more confident that it identified the language correctly\. For best results, if you are certain of the language spoken in each of the audio files, specify a language code\. For more information, see the [StartTranscriptionJob](API_StartTranscriptionJob.md) operation\.

Some Amazon Transcribe features require you to specify a language code\. If you try to automatically identify the language of your audio with the following features enabled, you receive an error: 
+ Custom language models
+ Custom vocabularies
+ Vocabulary filtering
+ Automatic content redaction

To increase the chance of identifying the language successfully, media files should have at least 30 seconds of speech\.

**Topics**
+ [Transcribing with Automatic Language Identification](transcribe-lang-id.md)
+ [Getting Notifications Using Automatic Language Identification](lang-id-cloudwatch.md)