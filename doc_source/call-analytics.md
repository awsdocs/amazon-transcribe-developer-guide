# Analyzing call center audio with Call Analytics<a name="call-analytics"></a>

Use Amazon Transcribe Call Analytics to gain insight into customer\-agent interactions\. Call Analytics provides you with:
+ [Call characteristics](call-analytics-insights.md#call-analytics-insights-characteristics), including talk time, non\-talk time, speaker loudness, interruptions, and talk speed
+ [Call summarization](call-analytics-insights.md#call-analytics-insights-summarization), which detects issues, action items, and outcomes
+ [Custom categories](call-analytics-insights.md#call-analytics-insights-categorization) and rules that you can use to hone in on specific keywords and criteria
+ [Redaction](call-analytics-insights.md#call-analytics-insights-redaction) of your text transcript and your audio file
+ [Speaker sentiment](call-analytics-insights.md#call-analytics-insights-sentiment) for each caller at various points in a call 

Call Analytics can also help increase staff productivity by reducing the need for manual note\-taking after each call\. It also reduces the time required by supervisors to read transcripts or listen to audio recordings\.

## Call Analytics use cases<a name="call-analytics-use-cases"></a>
+ **Monitor issue frequency over time**: Use [call categorization](call-analytics-insights.md#call-analytics-insights-categorization) to identify recurring keywords within your transcripts\.
+ **Gain insight into your customer service experience**: Use [call characteristics](call-analytics-insights.md#call-analytics-insights-characteristics) \(non\-talk time, talk time, interruptions, voice loudness, talk speed\) and sentiment analysis to determine if customers' issues are being appropriately resolved during their call\.
+ **Ensure regulatory compliance or adherence to company policy**: Set [keywords and phrases](call-analytics-insights.md#call-analytics-insights-categorization) for company\-specific greetings or disclaimers to verify your agents are meeting regulatory requirements\.
+ **Improve handling of customer data**: Use transcript and audio [redaction](call-analytics-insights.md#call-analytics-insights-redaction) to protect customer privacy\.
+ **Improve staff training**: Use criteria \(sentiment, non\-talk time, interruptions, talk speed\) to flag transcripts that can be used as examples of positive or negative customer interactions\.
+ **Measure staff efficacy in creating a positive customer experience**: Use [sentiment analysis](call-analytics-insights.md#call-analytics-insights-sentiment) to measure if your agents are able to turn a negative customer sentiment into a positive one as calls progress\.
+ **Improve data organization**: Label and sort calls based on [custom categories](call-analytics-insights.md#call-analytics-insights-categorization) \(including keywords and phrases, sentiment, talk time, and interruptions\)\.
+ Quickly **summarize the important aspects of a call** without needing to review the entire transcript: Use automatic [call summarization](call-analytics-insights.md#call-analytics-insights-summarization) to get a succinct summary of all issues, action items, and outcomes identified in a given call\.

To compare the features available with Call Analytics to those for Amazon Transcribe and Amazon Transcribe Medical, refer to the [Amazon Transcribe features](feature-matrix.md) table\.

To get started, see [Starting a Call Analytics job](call-analytics-start.md)\. Call Analytics output is similar to that of a standard transcription job, but contains additional analytics data\. To view Call Analytics output, see [Example output](call-analytics-output.md)\.

**API operations specific to Call Analytics**  
[CreateCallAnalyticsCategory](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_CreateCallAnalyticsCategory.html), [DeleteCallAnalyticsCategory](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_DeleteCallAnalyticsCategory.html), [DeleteCallAnalyticsJob](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_DeleteCallAnalyticsJob.html), [GetCallAnalyticsCategory](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_GetCallAnalyticsCategory.html), [GetCallAnalyticsJob](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_GetCallAnalyticsJob.html), [ListCallAnalyticsCategories](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_ListCallAnalyticsCategories.html), [ListCallAnalyticsJobs](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_ListCallAnalyticsJobs.html), [StartCallAnalyticsJob](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_StartCallAnalyticsJob.html), [UpdateCallAnalyticsCategory](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_UpdateCallAnalyticsCategory.html)

## Considerations and additional information<a name="call-analytics-considerations"></a>

Before using Call Analytics, note that:
+ Call Analytics only supports stereo\-channel audio; mono\-channel audio cannot be used with this feature\.
+ [Job queueing](job-queueing.md) is always enabled, meaning that you are limited to 100 concurrent Call Analytics jobs\. If you need to request a quota increase, see [AWS service quotas](https://docs.aws.amazon.com/general/latest/gr/aws_service_limits.html)\.
+ Input files for Call Analytics cannot be greater than 500 MB and must be less than 4 hours\.
+ If using categories, you must create all desired categories before starting a Call Analytics job\. Any new categories cannot be applied to existing Call Analytics jobs\. To learn how to create a new category, see [Creating categories](call-analytics-create-categories.md)\.
+ If you're using redaction, only US English \(en\-US\) is supported\. Refer to [Supported languages and language\-specific features](supported-languages.md) for a complete list of languages supported with Call Analytics\.
+ Call summarization is only supported for the following English language dialects: Australian \(en\-AU\), British \(en\-GB\), Indian \(en\-IN\), Irish \(en\-IE\), Scottish \(en\-AB\), US \(en\-US\), and Welsh \(en\-WL\)\.
+ Some Call Analytics quotas differ from Amazon Transcribe and Amazon Transcribe Medical; refer to [Guidelines and quotas](limits-guidelines.md) for specifics\.

**Tip**  
To learn more about post\-Call Analytics options, see [Post Call Analytics for your contact center with Amazon language AI services](http://aws.amazon.com/blogs/machine-learning/post-call-analytics-for-your-contact-center-with-amazon-language-ai-services/)\.  
To view sample Call Analytics output and features, check out our [GitHub demo](https://github.com/aws-samples/amazon-transcribe-post-call-analytics)\. We also have a [JSON to Word document GitHub example](https://github.com/aws-samples/amazon-transcribe-output-word-document) for Call Analytics\.