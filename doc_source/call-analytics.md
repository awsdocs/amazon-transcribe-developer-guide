# Analyzing call center audio with Call Analytics<a name="call-analytics"></a>

Use Amazon Transcribe Call Analytics to gain insight into customer\-agent interactions\. Call Analytics is designed specifically for call center audio and automatically provides you with valuable data relating to each call and each participant\. You can also hone in on data at specific points throughout call\. For example, you can compare customer sentiment in a call's first few seconds to the last quarter of the call to see if your agent provided a positive experience\. Other use case examples are listed in the [following section](#call-analytics-use-cases)\.

Call Analytics is available for post\-call and real\-time transcriptions\. If you're transcribing a file located in an Amazon S3 bucket, you're performing a post\-call transcription\. If you're transcribing an audio stream, you're performing a real\-time transcription\. These two transcription methods offer different Call Analytics insights and features\. For more detail on each method, see [Post\-call analytics](call-analytics-batch.md) and [Real\-time Call Analytics](call-analytics-streaming.md)\.

With real\-time Call Analytics transcriptions, you can also include [post\-call analytics](tca-post-call.md) in your request\. Your post\-call analytics transcript is stored in the Amazon S3 bucket that you specify in your request\. Refer to [Post\-call analytics with real\-time transcriptions](tca-post-call.md) for more information\.

**API operations specific to Call Analytics**  
Post\-call: [https://docs.aws.amazon.com/transcribe/latest/APIReference/API_CreateCallAnalyticsCategory.html](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_CreateCallAnalyticsCategory.html), [https://docs.aws.amazon.com/transcribe/latest/APIReference/API_DeleteCallAnalyticsCategory.html](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_DeleteCallAnalyticsCategory.html), [https://docs.aws.amazon.com/transcribe/latest/APIReference/API_DeleteCallAnalyticsJob.html](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_DeleteCallAnalyticsJob.html), [https://docs.aws.amazon.com/transcribe/latest/APIReference/API_GetCallAnalyticsCategory.html](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_GetCallAnalyticsCategory.html), [https://docs.aws.amazon.com/transcribe/latest/APIReference/API_GetCallAnalyticsJob.html](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_GetCallAnalyticsJob.html), [https://docs.aws.amazon.com/transcribe/latest/APIReference/API_ListCallAnalyticsCategories.html](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_ListCallAnalyticsCategories.html), [https://docs.aws.amazon.com/transcribe/latest/APIReference/API_ListCallAnalyticsJobs.html](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_ListCallAnalyticsJobs.html), [https://docs.aws.amazon.com/transcribe/latest/APIReference/API_StartCallAnalyticsJob.html](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_StartCallAnalyticsJob.html), [https://docs.aws.amazon.com/transcribe/latest/APIReference/API_UpdateCallAnalyticsCategory.html](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_UpdateCallAnalyticsCategory.html)  
Real\-time: [https://docs.aws.amazon.com/transcribe/latest/APIReference/API_StartCallAnalyticsStreamTranscription.html](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_StartCallAnalyticsStreamTranscription.html), StartCallAnalyticsStreamTranscriptionWebSocket

## Common use cases<a name="call-analytics-use-cases"></a>

**Post\-call transcriptions:**
+ **Monitor issue frequency over time**: Use [call categorization](call-analytics-batch.md#tca-categorization-batch) to identify recurring keywords within your transcripts\.
+ **Gain insight into your customer service experience**: Use [call characteristics](call-analytics-batch.md#tca-characteristics-batch) \(non\-talk time, talk time, interruptions, voice loudness, talk speed\) and sentiment analysis to determine if customer issues are being appropriately resolved during the call\.
+ **Ensure regulatory compliance or adherence to company policy**: Set [keywords and phrases](call-analytics-batch.md#tca-categorization-batch) for company\-specific greetings or disclaimers to verify that your agents are meeting regulatory requirements\.
+ **Improve handling of customers' personal data**: Use [PII redaction](call-analytics-batch.md#tca-pii-redact-batch) in your transcription output or audio file to help protect customer privacy\.
+ **Improve staff training**: Use criteria \(sentiment, non\-talk time, interruptions, talk speed\) to flag transcripts that can be used as examples of positive or negative customer interactions\.
+ **Measure staff efficacy in creating a positive customer experience**: Use [sentiment analysis](call-analytics-batch.md#tca-sentiment-batch) to measure if your agents are able to turn a negative customer sentiment into a positive one as calls progress\.
+ **Improve data organization**: Label and sort calls based on [custom categories](call-analytics-batch.md#tca-categorization-batch) \(including keywords and phrases, sentiment, talk time, and interruptions\)\.
+ **Summarize the important aspects of a call**: Use automatic [call summarization](call-analytics-batch.md#tca-summarization-batch) to get a succinct summary of all issues, action items, and outcomes identified in a given call\.

**Real\-time transcriptions:**
+ **Mitigate escalations in real time**: Set up [real\-time alerts](tca-start-stream.md#tca-create-alert-stream) for key phrases—such as a customer saying "speak to a manager"—to flag calls as they begin to escalate\. You can create real\-time alerts using real\-time category matches\.
+ **Improve handling of customer data**: Use [PII identification](call-analytics-streaming.md#tca-pii-id-stream) or [PII redaction](call-analytics-streaming.md#tca-pii-redact-stream) in your transcription output to help protect customer privacy\.
+ **Identify custom keywords and phrases**: Use [custom categories](call-analytics-streaming.md#tca-category-events-stream) to flag specific keywords in a call\.
+ **Automatically identify issues**: Use automatic [issue detection](call-analytics-streaming.md#tca-issue-detection-stream) to get a succinct summary of all issues identified in a call\.
+ **Measure staff efficacy in creating a positive customer experience**: Use [sentiment analysis](call-analytics-streaming.md#tca-sentiment-stream) to measure if your agents are able to turn a negative customer sentiment into a positive one as calls progress\.
+ **Set up agent\-assist**: Use the insights of your choice to provide your agents with proactive assistance in resolving customer calls\. See [Live Call Analytics and agent assist for your contact center with Amazon language AI services](http://aws.amazon.com/blogs/machine-learning/live-call-analytics-and-agent-assist-for-your-contact-center-with-amazon-language-ai-services/) for more information\.

To compare the features available with Call Analytics to those for Amazon Transcribe and Amazon Transcribe Medical, refer to the [feature table](feature-matrix.md)\.

To get started, see [Starting a post\-call analytics transcription](tca-start-batch.md) and [Starting a real\-time Call Analytics transcription](tca-start-stream.md)\. Call Analytics output is similar to that of a standard transcription job, but contains additional analytics data\. To view sample output, see [Post\-call analytics output](tca-output-batch.md) and [Real\-time Call Analytics output](tca-output-streaming.md)\.

## Considerations and additional information<a name="tca-considerations"></a>

Before using Call Analytics, note that:
+ Call Analytics only supports two\-channel audio, where an agent is present on one channel and a customer is present on a second channel\.
+ [Job queueing](job-queueing.md) is always enabled for post\-call analytics jobs, so you're limited to 100 concurrent Call Analytics jobs\. If you want to request a quota increase, see [AWS service quotas](https://docs.aws.amazon.com/general/latest/gr/aws_service_limits.html)\.
+ Input files for post\-call analytics jobs cannot be greater than 500 MB and must be less than 4 hours\.
+ If using categories, you must create all desired categories before starting a Call Analytics transcription\. Any new categories cannot be applied to existing transcriptions\. To learn how to create a new category, see [Creating categories for post\-call transcriptions](tca-categories-batch.md) and [Creating categories for real\-time transcriptions](tca-categories-stream.md)\.
+ Some Call Analytics quotas differ from Amazon Transcribe and Amazon Transcribe Medical; refer to the [AWS General Reference](https://docs.aws.amazon.com/general/latest/gr/transcribe.html#transcribe_region) for details\.

**Dive deeper with the AWS Machine Learning Blog**  
To learn more about Call Analytics options, see:  
[Post Call Analytics for your contact center with Amazon language AI services](http://aws.amazon.com/blogs/machine-learning/post-call-analytics-for-your-contact-center-with-amazon-language-ai-services/)
[Live Call Analytics and agent assist for your contact center with Amazon language AI services](http://aws.amazon.com/blogs/machine-learning/live-call-analytics-and-agent-assist-for-your-contact-center-with-amazon-language-ai-services/)

To view sample Call Analytics output and features, see our [GitHub demo](https://github.com/aws-samples/amazon-transcribe-post-call-analytics)\. We also offer a [JSON to Word document](https://github.com/aws-samples/amazon-transcribe-output-word-document) application to convert your transcript into an easy\-to\-read format\.

## Region availability<a name="tca-regions"></a>

Call Analytics is supported in the following AWS Regions:


| Region | Support | 
| --- | --- | 
| ap\-northeast\-1 \(Tokyo\) | post\-call, real\-time | 
| ap\-northeast\-2 \(Seoul\) | post\-call, real\-time | 
| ap\-south\-1 \(Mumbai\) | post\-call | 
| ap\-southeast\-1 \(Singapore\) | post\-call | 
| ap\-southeast\-2 \(Sydney\) | post\-call, real\-time | 
| ca\-central\-1 \(Canada, Central\) | post\-call, real\-time | 
|  eu\-central\-1 \(Frankfurt\) | post\-call, real\-time | 
| eu\-west\-2 \(London\) | post\-call, real\-time | 
| us\-east\-1 \(N\. Virginia\) | post\-call, real\-time | 
| us\-west\-2 \(Oregon\) | post\-call, real\-time | 

 For more information on AWS Regions, see:
+ [AWS service endpoints ](https://docs.aws.amazon.com/general/latest/gr/rande.html)
+ [Amazon Transcribe Endpoints and Quotas](https://docs.aws.amazon.com/general/latest/gr/transcribe.html#transcribe_region)