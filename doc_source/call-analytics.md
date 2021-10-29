# Call analytics<a name="call-analytics"></a>

The call analytics feature is designed to help you gain insight into customer\-agent interactions\. The key components of this feature are:
+ [Turn\-by\-turn transcription](call-analytics-turn-by-turn.md)
+ [Sentiment analysis](call-analytics-sentiment.md)
+ [Call categorization](call-analytics-categorization.md)
+ [Issue detection](call-analytics-issue-detection.md)
+ [Sensitive data redaction](call-analytics-pii-redaction.md)
+ [Call characteristics](call-analytics-characteristics.md)

**Tip**  
To view sample call analytics output and features, check out our [GitHub demo](https://github.com/aws-samples/amazon-transcribe-output-word-document)\.

Considerations when using call analytics:
+ Job queuing is always enabled\.
+ Input files for call analytics cannot be greater than 500 MB and must be less than 4 hours\.
+ A call analytics job only uses the categories you've previously created\. Any new categories cannot be applied to previous call analytics jobs\.

For a list of languages that support call analytics, refer to [Supported languages and language\-specific features](supported-languages.md#table-language-matrix)\. Note that if you're using redaction, only U\.S\. English \(en\-US\) is supported\.

For call analytics quotas, refer to [Guidelines and quotas](limits-guidelines.md)\.

Call analytics output is similar to that of a standard transcription job, but contains additional data based on the analytics categories you create\. To learn how to set up a call analytics job, see [Start a call analytics transcription job](call-analytics-start.md)\. For example output, see [Sample call analytics output](call-analytics-output.md)\.

**API operations specific to call analytics**  
 [CreateCallAnalyticsCategory](https://docs.aws.amazon.com/transcribe/latest/dg/API_CreateCallAnalyticsCategory.html), [DeleteCallAnalyticsCategory](https://docs.aws.amazon.com/transcribe/latest/dg/API_DeleteCallAnalyticsCategory.html), [DeleteCallAnalyticsJob](https://docs.aws.amazon.com/transcribe/latest/dg/API_DeleteCallAnalyticsJob.html), [GetCallAnalyticsCategory](https://docs.aws.amazon.com/transcribe/latest/dg/API_GetCallAnalyticsCategory.html), [GetCallAnalyticsJob](https://docs.aws.amazon.com/transcribe/latest/dg/API_GetCallAnalyticsJob.html), [ListCallAnalyticsCategories](https://docs.aws.amazon.com/transcribe/latest/dg/API_ListCallAnalyticsCategories.html), [ListCallAnalyticsjobs](https://docs.aws.amazon.com/transcribe/latest/dg/API_ListCallAnalyticsjobs.html), [StartCallAnalyticsJob](https://docs.aws.amazon.com/transcribe/latest/dg/API_StartCallAnalyticsJob.html), [UpdateCallAnalyticsCategory](https://docs.aws.amazon.com/transcribe/latest/dg/API_UpdateCallAnalyticsCategory.html) 