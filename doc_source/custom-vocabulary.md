# Custom vocabularies<a name="custom-vocabulary"></a>

Use custom vocabularies to improve transcription accuracy for one or more specific words\. These are generally domain\-specific terms, such as brand names and acronyms, proper nouns, and words that Amazon Transcribe isn't rendering correctly\.

Custom vocabularies can be used with all supported languages\. Note that only the characters listed in your language's [character set](charsets.md) can be used in a custom vocabulary\.

**Important**  
You are responsible for the integrity of your own data when you use Amazon Transcribe\. Do not enter confidential information, personal information \(PII\), or protected health information \(PHI\) into a custom vocabulary\.

Considerations when creating a custom vocabulary:
+ You can have up to 100 vocabulary files per AWS account
+ The size limit for each custom vocabulary file is 50 Kb
+ Each entry cannot exceed 256 characters
+ Vocabularies can be in table or list format \(table format is strongly recommended\)
+ How you create your custom vocabulary varies depending on the format you used; refer to [Using a custom vocabulary](custom-vocabulary-using.md) for examples
  + Table format: First upload your custom vocabulary file into an Amazon S3 bucket, then include the Amazon S3 URI of your vocabulary file in your request
  + List format: If using the AWS Management Console, you must save your custom vocabulary file locally, then include the path to your custom vocabulary file in your request; if using the command line \(AWS CLI or AWS SDK\), you must include your list as comma\-separated words within your request

**Tip**  
You can test your custom vocabulary using the AWS Management Console\. Once your custom vocabulary is ready to use, log in to the AWS Management Console, select **Real\-time transcription**, scroll to **Customizations**, toggle on **Custom vocabulary**, and select your custom vocabulary from the dropdown list\. Then select **start streaming**\. Speak some of the words in your custom vocabulary into your microphone to see if they render correctly\.

## Custom vocabulary tables versus lists<a name="custom-vocabulary-tables-lists"></a>

Tables are strongly preferred\.

Tables give you more options for—and more control over—the input and output of words within your custom vocabulary\. With tables, you must specify multiple categories \(Phrase, IPA, SoundsLike, and DisplayAs\), allowing you to fine\-tune your output\.

Lists don't have additional options, so you can only type in entries as you want them to appear in your transcript, replacing all spaces with hyphens\. Custom vocabulary lists are not supported with the [https://docs.aws.amazon.com/transcribe/latest/APIReference/API_CreateMedicalVocabulary.html](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_CreateMedicalVocabulary.html) operation\.

The AWS Management Console, AWS CLI, and AWS SDKs all use custom vocabulary tables in the same way; lists are used differently for each method and thus may require additional formatting for successful use between methods\.

For more information, see [Creating a custom vocabulary using a table](custom-vocabulary-create-table.md) and [Creating a custom vocabulary using a list](custom-vocabulary-create-list.md)\.

To dive a little deeper and learn how to use Amazon Augmented AI with custom vocabularies, see:

[![AWS Videos](http://img.youtube.com/vi/https://www.youtube.com/embed/65eVesNiJzY/0.jpg)](http://www.youtube.com/watch?v=https://www.youtube.com/embed/65eVesNiJzY)

**API operations specific to custom vocabularies**  
 [https://docs.aws.amazon.com/transcribe/latest/APIReference/API_CreateVocabulary.html](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_CreateVocabulary.html), [https://docs.aws.amazon.com/transcribe/latest/APIReference/API_DeleteVocabulary.html](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_DeleteVocabulary.html), [https://docs.aws.amazon.com/transcribe/latest/APIReference/API_GetVocabulary.html](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_GetVocabulary.html), [https://docs.aws.amazon.com/transcribe/latest/APIReference/API_ListVocabularies.html](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_ListVocabularies.html), [https://docs.aws.amazon.com/transcribe/latest/APIReference/API_UpdateVocabulary.html](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_UpdateVocabulary.html) 