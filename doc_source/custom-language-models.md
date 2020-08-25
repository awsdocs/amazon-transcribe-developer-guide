# Improving Domain\-Specific Transcription Accuracy with Custom Language Models<a name="custom-language-models"></a>

Use *custom language models* to train and develop language models that are domain\-specific\. For example, you can use custom language models to improve transcription performance for domains such as legal, hospitality, finance, and insurance\. Although the general model provided by Amazon Transcribe works well in most instances, custom language models might produce even more accurate results\.

To train a custom language model, you must upload text data from your specific use case to Amazon Simple Storage Service \(Amazon S3\), provide Amazon Transcribe with permission to access that data, and choose a *base model*\. A base model is a general speech recognition model, which you customize with your text data\.

Custom language models use your text data to improve transcription accuracy for your use case\. Your text data can include domain\-specific text or audio transcripts\. Domain\-specific text data includes website content, instruction manuals, and technical documentation\. Audio transcript data consists of ground\-truth audio transcripts\. Ground\-truth audio transcripts have been processed with very high accuracy and are the ideal representation of the source audio\.

You must provide text data that represents the audio that you want to transcribe\. The domain\-specific data that you provide must be related to your use case, and the audio transcript data that you provide should be similar to the audio that you want to transcribe\. Any potential improvement in transcription accuracy depends on how closely your text data represents your audio and how much text data you provide\. The quality of your text data is much more important than its quantity in creating custom language models that generate accurate transcriptions\.

You upload your text data to Amazon Simple Storage Service \(Amazon S3\) and then give Amazon Transcribe access to the S3 buckets that contain that data\. After uploading your data to Amazon S3, you choose a *base model*\. A base model is a general speech recognition model that you customize with your text data\.

There are two ways that you can upload your text data to create a custom language model:

1. Upload your text as *training data*\. You use training data to train your custom language model for your specific use case\.

1. Upload your domain\-specific text as training data and your audio transcripts as *tuning data*\. You use tuning data to optimize your custom language model and increase its transcription accuracy\.

Use the following table to determine how to upload your data\.


| If you have | Upload this | 
| --- | --- | 
| A large amount of domain\-specific text and a much smaller amount of audio transcript text data | Domain\-specific text as training data\. Upload your transcription text as tuning data\. | 
| A minimum of 10,000 words of audio transcript text | Audio transcript text as training data\. | 
| At least 100,000 words of audio transcript text and a large amount of additional domain\-specific text | Audio transcript text as training data\. Typically, this method leads to the greatest possible increase in transcription accuracy\. Follow the first method described in this table if this method doesn't produce the desired increase in transcription accuracy\. | 

You can provide up to 2 GB of training data and 200 MB of tuning data\. 

If you have enough text that represents the audio you want to transcribe, training custom language models can produce significant improvements in accuracy over using [Custom Vocabularies](how-vocabulary.md) \. Custom vocabularies improve the ability of Amazon Transcribe to recognize terms without using the context in which they're spoken\. Custom language models not only recognize individual terms, but additionally use each term's context to transcribe your audio\. 

Custom language models can also add words to their recognition vocabularies automatically, eliminating the need for you to manually input new words\. You can't use custom language models with custom vocabularies\.

Custom language models are available only in US English \(en\-US\)\.

You can't use AWS Key Management Service \(AWS KMS\) to encrypt your training data,  but you can use AWS KMS condition keys to encrypt your transcription output\. For information about condition keys, see [Key Management](key-management.md)\.

To use custom language models in your transcription jobs, you do the following:
+ Prepare and upload plain text data
+ Provide Amazon Transcribe with permissions to access your data
+ Create a custom language model
+ Use a custom language model in a transcription job
+ View and update your custom language models to take advantage of speech recognition improvements in Amazon Transcribe

**Topics**
+ [Step 1: Preparing the Data](prepare-training-data.md)
+ [Step 2: Providing Amazon Transcribe with Data Permissions](training-data-permissions.md)
+ [Step 3: Creating a Custom Language Model](create-custom-language-model.md)
+ [Step 4: Transcribing with a Custom Language Model](clm-transcription.md)
+ [Step 5: Viewing and Updating Your Custom Language Models](view-update-lang.md)