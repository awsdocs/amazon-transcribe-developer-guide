# Custom vocabularies<a name="custom-vocabulary"></a>

Use custom vocabularies to improve transcription accuracy for one or more specific words\. These are generally domain\-specific words and phrases, words that Amazon Transcribe isn't recognizing, and proper nouns\. We recommend creating separate, small vocabularies tailored to specific audio recordings instead of creating a single, large vocabulary for use with all of your recordings\.

**Important**  
You are responsible for the integrity of your own data when you use Amazon Transcribe\. Do not enter confidential information, personal information \(PII\), or protected health information \(PHI\) into a custom vocabulary\.

Considerations when creating a custom vocabulary:
+ You can have up to 100 vocabularies in your account\.
+ The size limit for each custom vocabulary is 50 Kb\.
+ Each entry must contain fewer than 256 characters, including hyphens\.
+ You can only use characters that are supported for your language\. Refer to your language's [character set](charsets.md) for details\.
+ Each vocabulary file can be in either table or list format; table format is strongly recommended\.
+ Your vocabulary files must be stored in an S3 bucket if using a table format\. If using a list, you can upload a text file using the AWS Management Console or include your list of words within an API call\.

**Tip**  
You can test your vocabulary using the AWS Management Console\. Once your vocabulary is ready to use, log into the AWS Management Console, select **Real\-time transcription**, scroll to **Customizations**, toggle on **Custom vocabulary**, and select your vocabulary from the drop\-down list\. Then select **start streaming**\. Speak some of the words in your vocabulary into your microphone to see if they render correctly\.

**Should I use a table or a list for my custom vocabulary?**

Table format is strongly preferred\.

Tables give you more options for—and more control over—the input and output of words within your custom vocabulary\. With tables, you must specify multiple categories \(Phrase, IPA, SoundsLike, and DisplayAs\), allowing you to fine\-tune your output\. If you have domain\-specific or non\-standard words, use the table format and add a pronunciation hint in the 'SoundsLike' column\.

Lists don't have additional options, so you can only type in entries as you want them to appear in your transcript, replacing any spaces with hyphens\. Vocabulary lists are not supported with the [https://docs.aws.amazon.com/transcribe/latest/APIReference/API_CreateMedicalVocabulary.html](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_CreateMedicalVocabulary.html) operation\.

The AWS Management Console, AWS CLI, and AWS SDKs all use custom vocabulary tables in the same way; lists are used differently for each method and thus may require additional formatting for successful use between each method\.

For more information, see [Creating a custom vocabulary using a table](custom-vocabulary-create-table.md) and [Creating a custom vocabulary using a list](custom-vocabulary-create-list.md)\.

For a video walkthrough of creating and using custom vocabularies, see:

[![AWS Videos](http://img.youtube.com/vi/https://www.youtube.com/embed/oBgSJ7bsP2U/0.jpg)](http://www.youtube.com/watch?v=https://www.youtube.com/embed/oBgSJ7bsP2U)

For a real\-life example of how Formula 1 is using custom vocabularies to create live captions for their races, see [Live transcriptions of F1 races using Amazon Transcribe](http://aws.amazon.com/blogs/machine-learning/live-transcriptions-of-f1-races-using-amazon-transcribe/)\.

**API operations specific to custom vocabularies**  
 [CreateVocabulary](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_CreateVocabulary.html), [DeleteVocabulary](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_DeleteVocabulary.html), [GetVocabulary](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_GetVocabulary.html), [ListVocabularies](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_ListVocabularies.html), [UpdateVocabulary](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_UpdateVocabulary.html) 