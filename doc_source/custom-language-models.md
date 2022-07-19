# Custom language models<a name="custom-language-models"></a>

Custom language models are designed to improve transcription accuracy for domain\-specific speech\. This includes any content outside of what you would hear in normal, everyday conversations\. For example, if you're transcribing the proceedings from a scientific conference, a standard transcription is unlikely to recognize many of the scientific terms used by presenters\. In this case, you can train a custom language model to recognize the specialized terms used in your discipline\.

Unlike custom vocabularies, which increase recognition of a word by providing hints \(such as pronunciations\), custom language models learn the context associated with a given word\. This includes how and when a word is used, and the relationship a word has to other words\. For example, if you train your model using climate science research papers, your model may learn that 'ice floe' is a more likely word pair than 'ice flow'\.

To view the supported languages for custom language models, refer to [Supported languages and language\-specific features](supported-languages.md)\.

**API operations specific to custom language models**  
 [CreateLanguageModel](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_CreateLanguageModel.html), [DeleteLanguageModel](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_DeleteLanguageModel.html), [DescribeLanguageModel](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_DescribeLanguageModel.html), [ListLanguageModels](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_ListLanguageModels.html) 

## Data sources<a name="custom-language-models-data-sources"></a>

You can use any type of text data you want to train your model\. However, the closer your text content is to your audio content, the more accurate your model\. Therefore, it's important to choose text data that use the same terms in the same context as your audio\.

The best data for training a model are accurate transcripts\. This is considered in\-domain data\. In\-domain text data have the exact same terms, usage, and context as the audio you want to transcribe\.

If you don't have accurate transcripts, use journal articles, technical reports, whitepapers, conference proceedings, instruction manuals, news articles, website content, and any other text that contains the desired terms used in a similar context to that of your audio\. This is considered domain\-related data\.

Creating a robust custom language model may require a significant amount of text data, which must contain the terms spoken in your audio\. You can supply Amazon Transcribe with up to 2 GB of text data to train your model—this is referred to as **training data**\. Optionally, when you have no \(or few\) in\-domain transcripts, you can provide Amazon Transcribe with up to 200 MB of text data to tune your model—this is referred to as **tuning data**\.

## Training versus tuning data<a name="custom-language-models-training-tuning"></a>

The purpose of training data is to teach Amazon Transcribe to recognize new terms and learn the context in which these terms are used\. In order to create a robust model, Amazon Transcribe may require a large volume of relevant text data\. Providing as much training data as possible, up to the 2 GB limit, is strongly recommended\.

The purpose of tuning data is to help refine and optimize the contextual relationships learned from your training data\. Tuning data are not required to create a custom language model\.

It's up to you to decide how best to select training and, optionally, tuning data\. Each case is unique and depends on the type and amount of data you have\. Tuning data are recommended when you lack in\-domain training data\.

If you choose to include both data types, do **not** overlap your training and tuning data; training and tuning data should be unique\. Overlapping data can bias and skew your custom language model, impacting its accuracy\.

As general guidance, we recommend using accurate, in\-domain text as training data whenever possible\. Here are some general scenarios, listed in order of preference:
+ If you have more than 10,000 words of accurate, in\-domain transcript text, use it as training data\. In this case, there is no need to include tuning data\. This is the ideal scenario for training a custom language model\.
+ If you have accurate, in\-domain transcript text that contains less than 10,000 words and are not getting the desired results, consider augmenting your training data with domain\-related written texts, such as technical reports\. In this case, reserve a small portion \(10\-25%\) of your in\-domain transcript data to use as tuning data\.
+ If you have no in\-domain transcript text, upload all your domain\-related text as training data\. In this case, transcript\-style text is preferable to written text\. This is the least effective scenario for training a custom language model\.

When you're ready to create your model, see [Creating a custom language model](custom-language-models-create.md)\.