# Get a custom Amazon Transcribe vocabulary using an AWS SDK<a name="example_transcribe_GetVocabulary_section"></a>

The following code example shows how to get a custom Amazon Transcribe vocabulary\.

------
#### [ Python ]

**SDK for Python \(Boto3\)**  
  

```
def get_vocabulary(vocabulary_name, transcribe_client):
    """
    Gets information about a customer vocabulary.

    :param vocabulary_name: The name of the vocabulary to retrieve.
    :param transcribe_client: The Boto3 Transcribe client.
    :return: Information about the vocabulary.
    """
    try:
        response = transcribe_client.get_vocabulary(VocabularyName=vocabulary_name)
        logger.info("Got vocabulary %s.", response['VocabularyName'])
    except ClientError:
        logger.exception("Couldn't get vocabulary %s.", vocabulary_name)
        raise
    else:
        return response
```
+  Find instructions and more code on [GitHub](https://github.com/awsdocs/aws-doc-sdk-examples/tree/main/python/example_code/transcribe#code-examples)\. 
+  For API details, see [GetVocabulary](https://docs.aws.amazon.com/goto/boto3/transcribe-2017-10-26/GetVocabulary) in *AWS SDK for Python \(Boto3\) API Reference*\. 

------

For a complete list of AWS SDK developer guides and code examples, including help getting started and information about previous versions, see [Using this service with an AWS SDK](getting-started-sdk.md#sdk-general-information-section)\.