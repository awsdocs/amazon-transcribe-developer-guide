# What is Amazon Transcribe?<a name="what-is"></a>

Amazon Transcribe is an automatic speech recognition service that uses machine learning models to convert audio to text\. You can use Amazon Transcribe as a standalone transcription service or to add speech\-to\-text capabilities to any application\.

With Amazon Transcribe, you can improve accuracy for your specific use case with language customization, filter content to ensure customer privacy or audience\-appropriate language, analyze content in multi\-channel audio, partition the speech of individual speakers, and more\.

You can transcribe media in real time \(streaming\) or you can transcribe media files located in an Amazon S3 bucket \(batch\)\. To see which languages are supported for each type of transcription, refer to the [Supported languages and language\-specific features](supported-languages.md) table\.

**Topics**
+ [Amazon Transcribe and HIPAA eligibility](#transcribe-hippa)
+ [Pricing](#transcribe-pricing)
+ [Endpoints and quotas](#endpoints-quotas)

For a short video tour of Amazon Transcribe, see:

[![AWS Videos](http://img.youtube.com/vi/https://www.youtube.com/embed/zD8NMw4T1TI/0.jpg)](http://www.youtube.com/watch?v=https://www.youtube.com/embed/zD8NMw4T1TI)

To learn more, see [How Amazon Transcribe works](how-it-works.md) and [Getting started with Amazon Transcribe](getting-started.md)\.

**Tip**  
Information on the **Amazon Transcribe API** is located in the [API Reference](https://docs.aws.amazon.com/transcribe/latest/APIReference/Welcome.html)\.

## Amazon Transcribe and HIPAA eligibility<a name="transcribe-hippa"></a>

Amazon Transcribe is covered under AWS’s HIPAA eligibility and BAA which requires BAA customers to encrypt all PHI at rest and in transit when in use\. Automatic PHI identification is available at no additional charge and in all regions where Amazon Transcribe operates\. For more information, refer to [ HIPAA eligibility and BAA](http://aws.amazon.com/compliance/hipaa-compliance/)\.

## Pricing<a name="transcribe-pricing"></a>

Amazon Transcribe is a pay\-as\-you\-go service; pricing is based on seconds of transcribed audio, billed on a monthly basis\.

Usage is billed in one\-second increments, with a minimum per request charge of 15 seconds\. Note that additional charges apply for features such as PII content redaction and custom language models\.

For cost information for each AWS Region, refer to [Amazon Transcribe Pricing](http://aws.amazon.com/transcribe/pricing/)\.

## Endpoints and quotas<a name="endpoints-quotas"></a>

For a list of AWS Regions and endpoints available for Amazon Transcribe, refer to the [Service endpoints](https://docs.aws.amazon.com/general/latest/gr/transcribe.html#transcribe_region) in the *AWS General Reference*\.

For a list of quotas that pertain to your transcriptions, refer to the [Service quotas](https://docs.aws.amazon.com/general/latest/gr/transcribe.html#limits-amazon-transcribe) in the *AWS General Reference*\. Some quotas can be changed upon request\. If the **Adjustable** column contains '**Yes**', you can request an increase\. To do so, select the provided link\.