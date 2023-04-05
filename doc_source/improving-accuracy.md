# Improving transcription accuracy with custom vocabularies and custom language models<a name="improving-accuracy"></a>

If your media contains domain\-specific or non\-standard terms, such as brand names, acronyms, technical words, and jargon, Amazon Transcribe might not correctly capture these terms in your transcription output\.

To correct transcription inaccuracies and customize your output for your specific use case, you can create [Custom vocabularies](custom-vocabulary.md) and [Custom language models](custom-language-models.md)\.
+ [Custom vocabularies](custom-vocabulary.md) are designed to tune and boost both the recognition and the formatting of specific words in all contexts\. This involves supplying Amazon Transcribe with words and, optionally, pronunciation and display forms\.

  If Amazon Transcribe is not correctly rendering specific terms in your transcripts, you can create a custom vocabulary file that tells Amazon Transcribe how you want these terms displayed\. This word\-specific approach is most appropriate for correcting terms like brand names and acronyms\.
+ [Custom language models](custom-language-models.md) are designed to capture the context associated with terms\. This involves supplying Amazon Transcribe with a large volume of domain\-specific text data\.

  If Amazon Transcribe is not correctly rendering technical terms or is using the incorrect homophone in your transcripts, you can create a custom language model that teaches Amazon Transcribe your domain\-specific language\. For example, a custom language model can learn when to use 'floe' \(ice floe\) versus 'flow' \(linear flow\)\.

  This context\-aware approach is most appropriate for transcribing large volumes of domain\-specific speech\. Custom language models can produce significant accuracy improvements over custom vocabularies alone\. When using batch transcriptions, you can include both a custom language model and a custom vocabulary in your request\.

**Tip**  
To achieve the highest transcription accuracy, use custom vocabularies in conjunction with your custom language models\.

For a video walkthrough of creating and using custom vocabularies, see:

[![AWS Videos](http://img.youtube.com/vi/https://www.youtube.com/embed/oBgSJ7bsP2U/0.jpg)](http://www.youtube.com/watch?v=https://www.youtube.com/embed/oBgSJ7bsP2U)

For a video walkthrough of creating and using custom language models, see:

[![AWS Videos](http://img.youtube.com/vi/https://www.youtube.com/embed/iTkJoIqRrPU/0.jpg)](http://www.youtube.com/watch?v=https://www.youtube.com/embed/iTkJoIqRrPU)

**Dive deeper with the AWS Machine Learning Blog**  
Custom vocabularies:  
[Live transcriptions of F1 races using Amazon Transcribe](http://aws.amazon.com/blogs/machine-learning/live-transcriptions-of-f1-races-using-amazon-transcribe/)
Custom language models:  
[Building custom language models to supercharge speech\-to\-text performance Amazon Transcribe](http://aws.amazon.com/blogs/machine-learning/building-custom-language-models-to-supercharge-speech-to-text-performance-for-amazon-transcribe/)
[Boost transcription accuracy of class lectures with custom language models for Amazon Transcribe](http://aws.amazon.com/blogs/machine-learning/transcribe-class-lectures-accurately-using-amazon-transcribe-with-custom-language-models/)