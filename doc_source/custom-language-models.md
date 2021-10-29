# Improving transcription accuracy with custom language models<a name="custom-language-models"></a>

Custom language models use your text data \(training data\) to improve transcription accuracy for your specific use case\. For example, you can provide Amazon Transcribe with industry\-specific terms or acronyms that it might not otherwise recognize\.

In order to produce accurate transcriptions, your text data must be representative of the audio you want to transcribe\. Domain\-specific text data can include website content, instruction manuals, technical documentation, and audio transcripts\. The text data you provide must be related to your use case and, if using transcripts, these must be accurate\. Using innaccurate data to train language models results in inaccurate models, which in turn affects the accuracy of any transcription results that use those models\.

The quality of your training data is much more important than the quantity of data when creating a custom language model\. You can provide up to 2 GB of training data and 200 MB of tuning data\.

There are two ways to upload your text data to create a custom language model:

1. Upload your text as *training data*, which is used to train your custom language model for your specific use case\.

1. Upload your text as *tuning data*, which is used to optimize your custom language model and increase its transcription accuracy\.

If you're unsure on whether to use your data for training or tuning, this table may help you decide:


| If you have | Upload this | 
| --- | --- | 
| A large amount of domain\-specific text and a much smaller amount of audio transcript text data | Domain\-specific text as training data\. Upload your transcription text as tuning data\. | 
| A minimum of 10,000 words of audio transcript text | Audio transcript text as training data\. | 
| At least 100,000 words of audio transcript text and a large amount of additional domain\-specific text | Audio transcript text as training data\. Typically, this method leads to the greatest increase in transcription accuracy\. If this method doesn't produce the desired increase in transcription accuracy, follow the first method described in this table\. | 
| Domain\-specific text only | Domain\-specific text as training data\. This is the least robust option for training your model\. | 

Custom language models are not available with all Amazon Transcribe\-supported languages; refer to [Supported languages and language\-specific features](supported-languages.md#table-language-matrix) for more information\.

**API operations specific to custom language models**  
 [CreateLanguageModel](https://docs.aws.amazon.com/transcribe/latest/dg/API_CreateLanguageModel.html), [DeleteLanguageModel](https://docs.aws.amazon.com/transcribe/latest/dg/API_DeleteLanguageModel.html), [DescribeLanguageModel](https://docs.aws.amazon.com/transcribe/latest/dg/API_DescribeLanguageModel.html), [ListLanguageModels](https://docs.aws.amazon.com/transcribe/latest/dg/API_ListLanguageModels.html) 

## Custom language models versus custom vocabularies<a name="custom-language-models-vs-vocabularies"></a>

Custom language models are more robust than [Custom vocabularies](custom-vocabulary.md)\. As such, they require more training data than custom vocabularies; they also give you the option to provide tuning data, which is not available for custom vocabularies\. Because of the additional training involved, custom language models can produce significant accuracy improvements over [Custom vocabularies](custom-vocabulary.md)\.

Not only do custom language models recognize individual terms, but they use each term's context to transcribe your audio\. Custom vocabularies do not use context, and instead focus on individual words, independent of context\.

Custom vocabularies require you to manually input new words\. Custom language models can add words to their recognition vocabularies automatically, adding robustness without any extra work from you\.

To acheive the highest transcription accuracy, use custom vocabularies in conjunction with your custom language model\.

**Note**  
Streaming custom language models do not support custom vocabularies\.