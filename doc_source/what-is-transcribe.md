# What Is Amazon Transcribe?<a name="what-is-transcribe"></a>

Amazon Transcribe uses advanced machine learning technologies to recognize speech in audio files and transcribe them into text\. You can use Amazon Transcribe to convert audio to text and to create applications that incorporate the content of audio files\. For example, you can transcribe the audio track from a video recording to create closed captioning for the video\.

You can use Amazon Transcribe to transcribe the following languages to text:
+ Gulf Arabic \(ar\-AE\)
+ Modern Standard Arabic \(ar\-SA\)
+ Chinese Mandarin \- Mainland \(zh\-CN\)
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
+ Tamil \(ta\-IN\)
+ Telugu \(te\-IN\)
+ Turkish \(tr\-TR\)

You can transcribe streaming audio in the following languages:
+ Australian English \(en\-AU\)
+ British English \(en\-GB\)
+ US English \(en\-US\)
+ French \(fr\-FR\)
+ Canadian French \(fr\-CA\)
+ US Spanish \(es\-US\)

You can use Amazon Transcribe with other AWS services to create applications\. For example, you can: 
+ Use Amazon Transcribe to convert voice to text, send the text to Amazon Translate to translate it into another language, and send the translated text to Amazon Polly to speak the translated text\.
+ Use Amazon Transcribe to transcribe recordings of customer service calls for analysis\. After transcribing a recording, send the transcription to Amazon Comprehend to identify keywords, topics, or sentiments\.
+ Use Amazon Transcribe to transcribe live broadcasts such as television to provide real\-time subtitles\.

To use Amazon Transcribe you store your audio file in an Amazon S3 bucket\. The output from the transcription job is also stored in an S3 bucket\. Content delivered to Amazon S3 buckets might contain customer content\. For more information about removing sensitive data, see [How Do I Empty an S3 Bucket?](https://docs.aws.amazon.com/AmazonS3/latest/user-guide/empty-bucket.html) or [How Do I Delete an S3 Bucket?](https://docs.aws.amazon.com/AmazonS3/latest/user-guide/delete-bucket.html)\.

## Recognizing Voices<a name="what-speaker-recognition"></a>

Amazon Transcribe can identify the individual speakers in an audio clip, a technique known as *diarization* or *speaker identification*\. When you activate speaker identification, Amazon Transcribe includes an attribute that identifies each speaker in the audio clip\. You can use speaker identification to:
+ identify the customer and the support representative in a recorded customer support call
+ identify characters for closed captions
+ identify the speaker and questioners in a recorded press conference or lecture

You can specify the number of voices that you want Amazon Transcribe to recognize in an audio clip\.

## Transcribing Separate Audio Channels<a name="what-channel-id"></a>

To create a transcript for each channel, or single stream of recorded sound, in an audio file, use *channel identification*\. With channel identification, Amazon Transcribe returns two or more transcriptions: a combined transcription of all of the audio channels and a transcription of each audio channel\.

Use channel identification when your audio is on multiple channels\. For example, use channel identification:
+ When your recording has a customer service representative on one channel and a customer on another
+ When you transcribe a podcast where the host is recorded on one channel and the guest on another

For more information about channel identification, see [Channel Identification](how-channel-id.md)\.

## Transcribing Streaming Audio<a name="what-streaming-transcription"></a>

You can use Amazon Transcribe to transcribe streaming audio in real\-time\. You send Amazon Transcribe a stream of audio and Amazon Transcribe returns a stream of JSON objects containing the transcription of the audio\.

For more information about processing audio streams, see [Streaming Transcription](streaming.md)\.

## Custom Vocabulary<a name="what-custom-vocabulary"></a>

Create a custom vocabulary to help Amazon Transcribe recognize words that are specific to your use case and improve its accuracy in converting speech to text\. For example, you might create a custom vocabulary that includes industry\-specific words and phrases\. 

Use a custom vocabulary to help Amazon Transcribe recognize:
+ words that are not being recognized
+ unfamiliar words that are specific to your domain

For more information about creating a custom vocabulary, see [Custom Vocabularies](how-vocabulary.md)\.

## Are You a First\-time User of Amazon Transcribe ?<a name="first-time-user"></a>

If you are a first\-time user, we recommend that you read the following sections in order:

1. [How Amazon Transcribe Works](how-it-works.md)—Introduces Amazon Transcribe\.

1. [Getting Started with Amazon Transcribe](getting-started.md)—Explains how to set up your AWS account and use Amazon Transcribe\.

1.  [API Reference](API_Reference.md)—Contains reference documentation for Amazon Transcribe operations\.