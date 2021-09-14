# What is Amazon Transcribe?<a name="transcribe-whatis"></a>

Amazon Transcribe uses machine learning to recognize speech in audio and video files and transcribe that speech into text\. Practical use cases for Amazon Transcribe include transcriptions of customer\-agent calls and closed captions for videos\.

## Amazon Transcribe features<a name="transcribe-features"></a>

The following list highlights the Amazon Transcribe features that are available with **all supported languages**\. There are several features that are only supported with specific languages; refer to [Supported languages and language\-specific features](how-it-works.md#table-language-matrix) for more information\.
+ **[Custom vocabularies](how-vocabulary.md)**: Use a list of specific words you want Amazon Transcribe to recognize in your audio input\. Custom vocabularies are often used for domain\-specific terms or proper nouns that Amazon Transcribe isn't rendering correctly in your transcription output\.

  Use custom vocabularies to:
  + Recognize industry\-specific terms
  + Display acronyms correctly
  + Improve the accuracy of your transcription output

  See also: [Custom language models](custom-language-models.md)
+  **[Language identification](auto-lang-id.md)**: Amazon Transcribe can automatically identify the predominant language in a media file without you having to specify a language code\. You can also select several language codes to help Amazon Transcribe narrow down the predominant language and improve its accuracy\. Automatic language identification can be used for any **batch transcription** with the API or the [ Amazon Transcribe console](https://console.aws.amazon.com/transcribe/)\. 

  Amazon Transcribe also has the ability to transcribe accented speech of individuals who are non\-native speakers of a language\. For example, you can transcribe US English \(en\-US\) audio spoken with a German \(de\-DE\) accent\.
+  **[Vocabulary filtering](vocabulary-filtering.md)**: Mask, remove, or tag words you don't want to appear in your transcription\. Vocabulary filtering helps you filter for any word you consider profane, obscene, offensive, or otherwise unsuitable for display in your transcripts\.

  Use vocabulary filtering to:
  + Generate family\-friendly captions of a TV show
  + Remove proprietary terms from transcripts of conference proceedings
+ **[Speaker diarization](diarization.md)**: Identify individual speakers in an audio clip—a technique known as speaker diarization\. When you activate speaker diarization, Amazon Transcribe includes an attribute that identifies each speaker in the audio clip\.

  Use speaker diarization to:
  + Identify the customer and the support representative in a recorded customer support call
  + Identify characters for closed captions
  + Identify the speaker and questioners in a recorded press conference or lecture
+ **[Channel identification](channel-id.md)**: Create a transcript for each audio channel or single stream of recorded sound in an audio file\. For example, a phone conversation between two people consists of two separate audio channels\. With channel identification, Amazon Transcribe returns two or more transcriptions: a combined transcription of all of the audio channels, and a transcription of each audio channel\.

**Important**  
Not all Amazon Transcribe features are available in all languages; please review the [Supported languages and language\-specific features](how-it-works.md#table-language-matrix) table before getting started\.

## Cross\-service applications<a name="transcribe-cross-service"></a>

You can use Amazon Transcribe with other AWS services to create applications\. For example, you can: 
+ Translate your audio into another language\. Use Amazon Transcribe to convert voice to text, Amazon Translate to translate your text into another language, and Amazon Polly to generate audio from the translated text\.
+ Use Amazon Transcribe to transcribe recordings of customer service calls for analysis\. After transcribing a recording, send the transcription to Amazon Comprehend to identify keywords, topics, or sentiments\.
+ Use Amazon Transcribe to transcribe live broadcasts, such as television, to provide real\-time subtitles\. Amazon Transcribe might require additional customization—such as using a custom language model or manual transcript correction—for broadcast\-grade applications\.