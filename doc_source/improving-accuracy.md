# Improving transcription accuracy<a name="improving-accuracy"></a>

If you want to improve the accuracy of your transcriptions, you can use custom vocabularies, custom language models, or both\.

[Custom vocabularies](custom-vocabulary.md) involve the input of specific words\. For example, if Amazon Transcribe is not correctly rendering terms that are specific to your use case, you can create a vocabulary file with the correct terms for Amazon Transcribe to use in the transcription\.

Custom vocabularies do not use context, and instead focus on individual words that you input manually\.

[Custom language models](custom-language-models.md) are more generalized and require the input of large amounts of training and, optionally, tuning data\. Although custom language models often require more work upfront, they can be more widely applied once created\.

Custom language models also recognize individual terms, but, unlike custom vocabularies, they take into account the context associated with each term when transcribing your audio\. This context\-specific approach can produce significant accuracy improvements over custom vocabularies alone\.

**Tip**  
To achieve the highest transcription accuracy with batch transcriptions, use custom vocabularies in conjunction with your custom language models\. Note that streaming custom language models do not support custom vocabularies\.