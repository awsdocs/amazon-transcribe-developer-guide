# Delete a custom Amazon Transcribe vocabulary using an AWS SDK<a name="example_transcribe_DeleteVocabulary_section"></a>

The following code example shows how to delete a custom Amazon Transcribe vocabulary\.

------
#### [ Python ]

**SDK for Python \(Boto3\)**  
  

```
def delete_vocabulary(vocabulary_name, transcribe_client):
    """
    Deletes a custom vocabulary.

    :param vocabulary_name: The name of the vocabulary to delete.
    :param transcribe_client: The Boto3 Transcribe client.
    """
    try:
        transcribe_client.delete_vocabulary(VocabularyName=vocabulary_name)
        logger.info("Deleted vocabulary %s.", vocabulary_name)
    except ClientError:
        logger.exception("Couldn't delete vocabulary %s.", vocabulary_name)
        raise
```
+  Find instructions and more code on [GitHub](https://github.com/awsdocs/aws-doc-sdk-examples/tree/main/python/example_code/transcribe#code-examples)\. 
+  For API details, see [DeleteVocabulary](https://docs.aws.amazon.com/goto/boto3/transcribe-2017-10-26/DeleteVocabulary) in *AWS SDK for Python \(Boto3\) API Reference*\. 

------

For a complete list of AWS SDK developer guides and code examples, including help getting started and information about previous versions, see [Using this service with an AWS SDK](getting-started-sdk.md#sdk-general-information-section)\.