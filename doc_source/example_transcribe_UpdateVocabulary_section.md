# Update a custom Amazon Transcribe vocabulary using an AWS SDK<a name="example_transcribe_UpdateVocabulary_section"></a>

The following code example shows how to update a custom Amazon Transcribe vocabulary\.

**Note**  
The source code for these examples is in the [AWS Code Examples GitHub repository](https://github.com/awsdocs/aws-doc-sdk-examples)\. Have feedback on a code example? [Create an Issue](https://github.com/awsdocs/aws-doc-sdk-examples/issues/new/choose) in the code examples repo\. 

------
#### [ Python ]

**SDK for Python \(Boto3\)**  
 To learn how to set up and run this example, see [GitHub](https://github.com/awsdocs/aws-doc-sdk-examples/tree/main/python/example_code/transcribe#code-examples)\. 
  

```
def update_vocabulary(
        vocabulary_name, language_code, transcribe_client, phrases=None,
        table_uri=None):
    """
    Updates an existing custom vocabulary. The entire vocabulary is replaced with
    the contents of the update.

    :param vocabulary_name: The name of the vocabulary to update.
    :param language_code: The language code of the vocabulary.
    :param transcribe_client: The Boto3 Transcribe client.
    :param phrases: A list of comma-separated phrases to include in the vocabulary.
    :param table_uri: A table of phrases and pronunciation hints to include in the
                      vocabulary.
    """
    try:
        vocab_args = {'VocabularyName': vocabulary_name, 'LanguageCode': language_code}
        if phrases is not None:
            vocab_args['Phrases'] = phrases
        elif table_uri is not None:
            vocab_args['VocabularyFileUri'] = table_uri
        response = transcribe_client.update_vocabulary(**vocab_args)
        logger.info(
            "Updated custom vocabulary %s.", response['VocabularyName'])
    except ClientError:
        logger.exception("Couldn't update custom vocabulary %s.", vocabulary_name)
        raise
```
+  For API details, see [UpdateVocabulary](https://docs.aws.amazon.com/goto/boto3/transcribe-2017-10-26/UpdateVocabulary) in *AWS SDK for Python \(Boto3\) API Reference*\. 

------

For a complete list of AWS SDK developer guides and code examples, see [Using this service with an AWS SDK](getting-started-sdk.md#sdk-general-information-section)\. This topic also includes information about getting started and details about previous SDK versions\.