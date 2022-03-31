# What is Amazon Transcribe?<a name="what-is"></a>

Amazon Transcribe is an automatic speech recognition service that uses machine learning models to convert audio to text\.

With Amazon Transcribe, you can ingest audio input, produce easy\-to\-read transcripts, improve accuracy with language customization, and filter content to ensure customer privacy\. Practical use cases for Amazon Transcribe include transcribing and analyzing customer\-agent calls and creating closed captions for videos\.

With Amazon Transcribe, you can add speech\-to\-text capabilities to any application\.

For a short video tour of Amazon Transcribe, see:

[![AWS Videos](http://img.youtube.com/vi/https://www.youtube.com/embed/zD8NMw4T1TI/0.jpg)](http://www.youtube.com/watch?v=https://www.youtube.com/embed/zD8NMw4T1TI)

## Amazon Transcribe use cases<a name="transcribe-use-cases"></a>

Amazon Transcribe is a robust speech\-to\-text service that offers a diverse array of features, many of which can be combined between Amazon Transcribe and other AWS services\.
+ Gain insight into agent\-customer calls using [Call Analytics](call-analytics.md)\. This feature automatically analyzes 11 different criteria without any customization on your part\. For each speaker, you get sentiment data, talk time, non\-talk time, loudness, interruptions, and talk speed\. Call summarization, call categorization, and turn\-by\-turn output are provided for the whole call\.

  We've also launched two new analytics options for call center audio: [post\-call analytics](http://aws.amazon.com/blogs/machine-learning/post-call-analytics-for-your-contact-center-with-amazon-language-ai-services/) \(designed for audio files located in an S3 bucket\) and [live\-call analytics](http://aws.amazon.com/blogs/machine-learning/live-call-analytics-for-your-contact-center-with-amazon-language-ai-services/) \(designed for live audio streams\)\.
+ Get a summary of customer\-agent interactions with [call summarization](call-analytics-insights.md#call-analytics-insights-summarization)\. Get an at\-a\-glance summary of issues, action items, and outcomes for every call\.
+ Teach Amazon Transcribe industry\-specific terms, unique spelling, acronyms, and any words that are not being rendered correctly in your transcription results using [custom vocabularies](custom-vocabulary.md)\. Providing Amazon Transcribe with custom vocabularies can improve the accuracy of your transcription output\. See also: [Custom language models](custom-language-models.md)\.
+ Create [subtitles](subtitles.md) for your video files\. You can also use [content redaction](pii-redaction.md) \(only in US English\) and [vocabulary filtering](vocabulary-filtering.md) when generating subtitles to ensure your content is audience\-appropriate\. Note that filtered or redacted content shows as white space, `***`, or `[PII]` in your transcript and subtitle files, but **the audio itself is not altered**\.
+ Redact personally identifiable information \(PII\), such as social security numbers, from your transcripts using standard [content redaction](pii-redaction.md) or Call Analytics [sensitive data redaction](call-analytics-insights.md#call-analytics-insights-redaction)\. Call Analytics can also **redact your audio** by replacing spoken PII with silence\.
+ Identify individual speakers in an audio clip using [speaker diarization](diarization.md)\. When you activate speaker diarization, Amazon Transcribe attaches a unique attribute to each speaker in your transcription output\.
+ Remove proprietary terms from your transcript using [vocabulary filtering](vocabulary-filtering.md)\. For example, you can mask the name of a new product in a pre\-launch stakeholder meeting\. Vocabulary filtering can also be used to mask profane, offensive, or audience\-inappropriate terms\.
+ Using multi\-channel audio, you can have Amazon Transcribe produce a separate transcript for each channel, or have all channels transcribed in one output file\. See [Transcribing multi\-channel audio](channel-id.md)\.
+ If your audio is not in a language you speak, let Amazon Transcribe identify the language for you using [language identification](lang-id.md)\. You can then use [Amazon Translate](https://docs.aws.amazon.com/translate/latest/dg/what-is.html) to translate your transcript, and have [Amazon Polly](https://docs.aws.amazon.com/polly/latest/dg/what-is.html) read your transcript back to you\.
+ Improve streaming transcription accuracy with [partial result stabilization](streaming.md#streaming-partial-result-stabilization), which can also be used to [adjust the latency of your transcript](http://aws.amazon.com/blogs/machine-learning/amazon-transcribe-now-supports-partial-results-stabilization-for-streaming-audio/)\.

### Use cases in action<a name="transcribe-use-cases-in-action"></a>

Here are some diverse examples of how individuals and organizations are using Amazon Transcribe\.
+ [Live transcriptions of F1 races using Amazon Transcribe](http://aws.amazon.com/blogs/machine-learning/live-transcriptions-of-f1-races-using-amazon-transcribe/)
+ [Generate high\-quality meeting notes using Amazon Transcribe and Amazon Comprehend](http://aws.amazon.com/blogs/machine-learning/generate-high-quality-meeting-notes-using-amazon-transcribe-and-amazon-comprehend/)
+ [Boost transcription accuracy of class lectures with custom language models for Amazon Transcribe](http://aws.amazon.com/blogs/machine-learning/transcribe-class-lectures-accurately-using-amazon-transcribe-with-custom-language-models/)
+ [Make your audio and video files searchable using Amazon Transcribe and Amazon Kendra](http://aws.amazon.com/blogs/machine-learning/make-your-audio-and-video-files-searchable-using-amazon-transcribe-and-amazon-kendra/)
+ [Perform medical transcription analysis in real\-time with AWS AI services and Twilio Media Streams](http://aws.amazon.com/blogs/machine-learning/perform-medical-transcription-analysis-in-real-time-with-amazon-transcribe-medical-and-amazon-comprehend-medical-with-twilio-media-streams/)

## Pricing<a name="transcribe-pricing"></a>

Amazon Transcribe is a pay\-as\-you\-go service; pricing is based on seconds of transcribed audio, billed on a monthly basis\. For more information on cost, including cost\-breakdown examples for various AWS Regions, see [Amazon Transcribe Pricing](http://aws.amazon.com/transcribe/pricing/)\.