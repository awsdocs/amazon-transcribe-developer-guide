# What is Amazon Transcribe?<a name="transcribe-whatis"></a>

Amazon Transcribe uses advanced machine learning technologies to recognize speech in your audio or video and transcribe that speech into text\. You can use Amazon Transcribe to convert audio to text and to create applications that incorporate the content of audio files\. For example, you can transcribe the audio track from a video recording to create closed captioning for the video\.

You can also provide Amazon Transcribe with video files and transcribe the audio directly from those files\. For example, you can provide Amazon Transcribe with an MP4 video file, and it will transcribe the audio directly from that file\. For information on available file containers and formats, see [Speech input](input.md)\.

The following list shows the languages available for batch transcription\. Each language has its own *language code*, which is shown in the parentheses next to the language\. You use the language code to specify the language of your audio or video file\.
+ Gulf Arabic \(ar\-AE\)
+ Modern Standard Arabic \(ar\-SA\)
+ Mandarin Chinese – Mainland \(zh\-CN\)
+ Dutch \(nl\-NL\)
+ Australian English \(en\-AU\)
+ British English \(en\-GB\)
+ Indian English \(en\-IN\)
+ Irish English \(en\-IE\)
+ Scottish English \(en\-AB\)
+ US English \(en\-US\)
+ Welsh English \(en\-WL\)
+ Spanish \(es\-ES\)
+ US Spanish \(es\-US\)
+ French \(fr\-FR\)
+ Canadian French \(fr\-CA\)
+ Farsi Persian \(fa\-IR\)
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
+ Tamil \(ta\-IN\)
+ Telugu \(te\-IN\)
+ Turkish \(tr\-TR\)

You can transcribe streaming audio in the following languages\. To specify a language in your real\-time stream, you use a *language code*\. The language codes are shown in parentheses next to the languages\.
+ Mandarin Chinese – Mainland \(zh\-CN\)
+ Australian English \(en\-AU\)
+ British English \(en\-GB\)
+ US English \(en\-US\)
+ French \(fr\-FR\)
+ Canadian French \(fr\-CA\)
+ German \(de\-DE\)
+ Italian \(it\-IT\)
+ Japanese \(ja\-JP\)
+ Korean \(ko\-KR\)
+ Brazilian Portuguese \(pt\-BR\)
+ US Spanish \(es\-US\)

You can use Amazon Transcribe with other AWS services to create applications\. For example, you can: 
+ Use Amazon Transcribe to convert voice to text, send the text to Amazon Translate to translate it into another language, and send the translated text to Amazon Polly to speak the translated text\.
+ Use Amazon Transcribe to transcribe recordings of customer service calls for analysis\. After transcribing a recording, send the transcription to Amazon Comprehend to identify keywords, topics, or sentiments\.
+ Use Amazon Transcribe to transcribe live broadcasts such as television to provide real\-time subtitles\. Amazon Transcribe might require additional customization or human supervision for broadcast\-grade applications\.

To use Amazon Transcribe you store your audio file in an Amazon S3 bucket\. The output from the transcription job is also stored in an S3 bucket\. Content delivered to Amazon S3 buckets might contain customer content\. For more information about removing sensitive data, see [How Do I Empty an S3 Bucket?](https://docs.aws.amazon.com/AmazonS3/latest/user-guide/empty-bucket.html) or [How Do I Delete an S3 Bucket?](https://docs.aws.amazon.com/AmazonS3/latest/user-guide/delete-bucket.html)\.

## Recognizing voices<a name="what-speaker-recognition"></a>

Amazon Transcribe can identify individual speakers in an audio clip, a technique known as *speaker diarization*\. When you activate speaker diarization, Amazon Transcribe includes an attribute that identifies each speaker in the audio clip\. You can use speaker diarization to:
+ identify the customer and the support representative in a recorded customer support call
+ identify characters for closed captions
+ identify the speaker and questioners in a recorded press conference or lecture

You can specify the number of voices that you want Amazon Transcribe to recognize in an audio clip\.

## Transcribing separate audio channels<a name="what-channel-id"></a>

To create a transcript for each channel, or single stream of recorded sound, in an audio file, use *channel identification*\. With channel identification, Amazon Transcribe returns two or more transcriptions: a combined transcription of all of the audio channels and a transcription of each audio channel\.

Use channel identification when your audio is on multiple channels\. For example, use channel identification:
+ When your recording has a customer service representative on one channel and a customer on another
+ When you transcribe a podcast where the host is recorded on one channel and the guest on another

For more information about channel identification, see [Transcribing multi\-channel audio](channel-id.md)\.

## Transcribing streaming audio<a name="what-streaming-transcription"></a>

You can use Amazon Transcribe to transcribe streaming audio in real\-time\. You send Amazon Transcribe a stream of audio and Amazon Transcribe returns a stream of JSON objects containing the transcription of the audio\.

For more information about processing audio streams, see [Streaming transcription](streaming.md)\.

## Custom vocabulary<a name="what-custom-vocabulary"></a>

Create a custom vocabulary to help Amazon Transcribe recognize words that are specific to your use case and improve its accuracy in converting speech to text\. For example, you might create a custom vocabulary that includes industry\-specific words and phrases\. 

Use a custom vocabulary to help Amazon Transcribe recognize:
+ words that are not being recognized
+ unfamiliar words that are specific to your domain

For more information about creating a custom vocabulary, see [Custom vocabularies](how-vocabulary.md)\.

## Are you a first\-time user of Amazon Transcribe?<a name="first-time-user"></a>

If you are a first\-time user, we recommend that you read the following sections in order:

1. [How Amazon Transcribe works](how-it-works.md)—Introduces Amazon Transcribe\.

1. [Getting started with Amazon Transcribe](getting-started.md)—Explains how to set up your AWS account and use Amazon Transcribe\.

1.  [API Reference](API_Reference.md)—Contains reference documentation for Amazon Transcribe operations\.