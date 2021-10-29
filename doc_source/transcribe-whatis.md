# What is Amazon Transcribe?<a name="transcribe-whatis"></a>

Amazon Transcribe is an automatic speech recognition service that uses machine learning models to convert audio to text\.

Amazon Transcribe’s features allow you to ingest audio input, produce easy\-to\-read transcripts, improve accuracy with language customization, and filter content to ensure customer privacy\. Practical use cases for Amazon Transcribe include transcribing and analyzing customer\-agent calls and creating closed captions for videos\.

With Amazon Transcribe, you can add speech\-to\-text capabilities to any application\.

## Amazon Transcribe features<a name="transcribe-features"></a>

The following list highlights the Amazon Transcribe features that are available with **all supported languages**\. There are several features that are only supported with specific languages; refer to [Supported languages and language\-specific features](supported-languages.md#table-language-matrix) for more information\.
+ **[Channel identification](channel-id.md)**: Create a transcript for each audio channel or single stream of recorded sound in an audio file\. For example, a phone conversation between two people consists of two separate audio channels\. With channel identification, Amazon Transcribe returns two or more transcriptions: a combined transcription of all of the audio channels, and a transcription of each audio channel\.
+ **[Custom vocabularies](custom-vocabulary.md)**: Use a list of specific words you want Amazon Transcribe to recognize in your audio input\. Custom vocabularies are often used for domain\-specific terms or proper nouns that Amazon Transcribe isn't rendering correctly in your transcription output\.

  Use custom vocabularies to:
  + Recognize industry\-specific terms
  + Display acronyms correctly
  + Improve the accuracy of your transcription output

  See also: [Custom language models](custom-language-models.md)
+  **[Language identification](auto-lang-id.md)**: Amazon Transcribe can automatically identify the predominant language in a media file without you having to specify a language code\. You can also select several language codes to help Amazon Transcribe narrow down the predominant language for improved transcription accuracy\.

  Amazon Transcribe also has the ability to transcribe accented speech of individuals who are non\-native speakers of a language\. For example, you can transcribe US English \(en\-US\) audio spoken with a German \(de\-DE\) accent\.
+ **[Speaker diarization](diarization.md)**: Identify individual speakers in an audio clip—a technique known as speaker diarization\. When you activate speaker diarization, Amazon Transcribe includes an attribute that identifies each speaker in the audio clip\.

  Use speaker diarization to:
  + Identify the customer and the support representative in a recorded customer support call
  + Identify characters for closed captions
  + Identify the speaker and questioners in a recorded press conference or lecture
+ **[Subtitles](subtitles.md)**: Create subtitles for your video files\. You can use content redaction \(only in US English\) and vocabulary filters when generating subtitles\.

  Use subtitles to:
  + Create closed captions for your video files
  + Filter out inappropriate content, such as profanity, from your subtitles \(note that filtered or redacted content shows as whitespace, `***`, or `[PII]` in your transcript and subtitle files, but the audio component is not altered\)
+  **[Vocabulary filtering](vocabulary-filtering.md)**: Mask, remove, or tag words you don't want to appear in your transcription\. Vocabulary filtering helps you filter for any word you consider profane, obscene, offensive, or otherwise unsuitable for display in your transcripts\.

  Use vocabulary filtering to:
  + Generate family\-friendly captions of a TV show
  + Remove proprietary terms from transcripts of conference proceedings

**Important**  
Not all Amazon Transcribe features are available in all languages; please review the [Supported languages and language\-specific features](supported-languages.md#table-language-matrix) table before getting started\.

## Pricing<a name="transcribe-pricing"></a>

Amazon Transcribe is a pay\-as\-you\-go service; pricing is based on seconds of transcribed audio, billed on a monthly basis\. For more information on cost, including cost\-breakdown examples for various Regions, see [Amazon Transcribe Pricing](http://aws.amazon.com/transcribe/pricing/)\.