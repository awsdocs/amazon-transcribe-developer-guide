# Improving transcription accuracy with medical custom vocabularies<a name="vocabulary-med"></a>

To improve transcription accuracy in Amazon Transcribe Medical, create and use one or more medical custom vocabularies\. A *custom vocabulary* is a collection of words or phrases that are domain\-specific\. This collection helps improve the performance of Amazon Transcribe Medical in transcribing those words or phrases\.

You are responsible for the integrity of your own data when you use Amazon Transcribe Medical\. Do not enter confidential information, personal information \(PII\), or protected health information \(PHI\), into a custom vocabulary\.

For best results, create separate small custom vocabularies that each help transcribe a specific audio recording\. You receive greater improvements in transcription accuracy than if you created one large custom vocabulary to use with all of your recordings\.

By default, you can have up to 100 custom vocabularies in your AWS account\. A custom vocabulary can't exceed 50 KB in size\. For information on requesting an increase to the number of custom vocabularies that you can have in your AWS account, see [AWS service quotas](https://docs.aws.amazon.com/general/latest/gr/aws_service_limits.html)\.

Custom vocabularies are available in US English \(en\-US\)\.

**Topics**
+ [Creating a text file for your medical custom vocabulary](create-med-vocab-text.md)
+ [Using a text file to create a medical custom vocabulary](create-med-custom-vocabulary.md)
+ [Transcribing an audio file using a medical custom vocabulary](start-med-custom-vocab-job.md)
+ [Transcribing a real\-time stream using a medical custom vocabulary](start-med-vocab-stream.md)
+ [Character sets for Amazon Transcribe Medical](charsets-med.md)