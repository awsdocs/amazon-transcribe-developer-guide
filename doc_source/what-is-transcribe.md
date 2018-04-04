# What Is Amazon Transcribe?<a name="what-is-transcribe"></a>

Amazon Transcribe uses advanced machine learning technologies to recognize speech in audio files and transcribe them into text\. You can use Amazon Transcribe to convert English and Spanish audio to text and to create applications that incorporate the content of audio files\. For example, you can transcribe the audio track from a video recording to create closed captioning for the video\.

You can use Amazon Transcribe with other AWS services to create applications\. For example, you can: 

+ Use Amazon Transcribe to convert voice to text, send the text to Amazon Translate to translate it into another language, and send the translated text to Amazon Polly to speak the translated text\.

+ Use Amazon Transcribe to transcribe recordings of customer service calls for analysis\. After transcribing a recording, send the transcription to Amazon Comprehend to identify keywords, topics, or sentiments\.

## Recognizing Voices<a name="what-speaker-recognition"></a>

Amazon Transcribe can identify the individual speakers in an audio clip, a technique known as *diarization* or *speaker identification*\. When you activate speaker identification, Amazon Transcribe includes an attribute that identifies each speaker in the audio clip\. You can use speaker identification to:

+ identify the customer and the support representative in a recorded customer support call

+ identify characters for closed captions

+ identify the speaker and questioners in a recorded press conference or lecture

You can specify the number of voices that you want Amazon Transcribe to recognize in an audio clip

## Custom Vocabulary<a name="what-custom-vocabulary"></a>

Create a custom vocabulary to help Amazon Transcribe recognize words that are specific to your use case and improve its accuracy in converting speech to text\. For example, you might create a custom vocabulary that includes industry\-specific words and phrases\. 

Use a custom vocabulary to help Amazon Transcribe recognize:

+ words that are not being recognized

+ unfamiliar words that are specific to your domain

For more information about creating a custom vocabulary, see [Custom Vocabularies](how-it-works.md#how-vocabulary)\.

## Are You a First\-time User of Amazon Transcribe ?<a name="first-time-user"></a>

If you are a first\-time user, we recommend that you read the following sections in order:

1. [How Amazon Transcribe Works](how-it-works.md)—Introduces Amazon Transcribe\.

1. [Getting Started with Amazon Transcribe](getting-started.md)—Explains how to set up your AWS account and use Amazon Transcribe\.

1.  [API Reference](API_Reference.md)—Contains reference documentation for Amazon Transcribe operations\.