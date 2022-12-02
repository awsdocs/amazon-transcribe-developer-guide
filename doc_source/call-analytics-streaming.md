# Real\-time Call Analytics<a name="call-analytics-streaming"></a>

Real\-time Call Analytics provides real\-time insights that can be used for addressing issues and mitigating escalations as they happen\.

The following insights are available with real\-time Call Analytics:
+ [Category events](#tca-category-events-stream) that use rules to flag specific keywords and phrases; category events can be used to create [real\-time alerts](tca-start-stream.md#tca-create-alert-stream)
+ [Issue detection](#tca-issue-detection-stream) identifies the issues spoken within each audio segment
+ [PII \(sensitive data\) identification](#tca-pii-id-stream) in your text transcript
+ [PII \(sensitive data\) redaction](#tca-pii-redact-stream) of your text transcript
+ [Sentiment analysis](#tca-sentiment-stream) for each speech segment

In addition to real\-time Call Analytics, Amazon Transcribe can also perform [post\-call analytics](tca-post-call.md) on your media stream\. You can include post\-call analytics in your real\-time Call Analytics request using the [https://docs.aws.amazon.com/transcribe/latest/APIReference/API_streaming_PostCallAnalyticsSettings.html](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_streaming_PostCallAnalyticsSettings.html) parameter\.

## Real\-time insights<a name="call-analytics-insights-streaming"></a>

This section details the insights available for real\-time Call Analytics transcriptions\.

### Category events<a name="tca-category-events-stream"></a>

Using category events, you can match your transcription based on an exact keyword or phrase\. For example, if you set a filter for the phrase "I want to speak to the manager", Amazon Transcribe filters for that *exact* phrase\.

Here's an [output example](tca-output-streaming.md#tca-output-category-event-stream)\.

For more information on creating real\-time Call Analytics categories, see [Creating categories for real\-time transcriptions](tca-categories-stream.md)\.

**Tip**  
Category events allow you to set real\-time alerts; see [Creating real\-time alerts for category matches](tca-start-stream.md#tca-create-alert-stream) for more information\.

### Issue detection<a name="tca-issue-detection-stream"></a>

Issue detection provides succinct summaries of detected issues within each audio segment\. Using the issue detection feature, you can:
+ Reduce the need for manual note\-taking during and after calls
+ Improve agent efficiency, allowing them to respond faster to customers

**Note**  
Issue detection is supported with these English language dialects: Australian \(`en-AU`\), British \(`en-GB`\), and US \(`en-US`\)\.

The issue detection feature works across all industries and business sectors, and is context\-based\. It works out\-of\-the\-box and thus doesn't support customization, such as model training or custom categories\.

Issue detection with real\-time Call Analytics is performed on each complete audio segment\.

Here's an [output example](tca-output-streaming.md#tca-output-issue-detection-stream)\.

### PII \(sensitive data\) identification<a name="tca-pii-id-stream"></a>

Sensitive data identification labels personally identifiable information \(PII\) in the text transcript\. This parameter is useful for protecting customer information\.

**Note**  
Real\-time PII identification is supported with these English language dialects: Australian \(`en-AU`\), British \(`en-GB`\), and US \(`en-US`\)\.

PII identification with real\-time Call Analytics is performed on each complete audio segment\.

To view the list of PII that is identified using this feature, or to learn more about PII identification with Amazon Transcribe, see [Redacting or identifying personally identifiable information](pii-redaction.md)\.

Here is an [output example](tca-output-streaming.md#tca-output-pii-id-stream)\.

### PII \(sensitive data\) redaction<a name="tca-pii-redact-stream"></a>

Sensitive data redaction replaces personally identifiable information \(PII\) in your text transcript with the type of PII \(for example, `[NAME]`\)\. This parameter is useful for protecting customer information\.

**Note**  
Real\-time PII redaction is supported with these English language dialects: Australian \(`en-AU`\), British \(`en-GB`\), and US \(`en-US`\)\.

PII redaction with real\-time Call Analytics is performed on each complete audio segment\.

To view the list of PII that is redacted using this feature, or to learn more about redaction with Amazon Transcribe, see [Redacting or identifying personally identifiable information](pii-redaction.md)\.

Here is an [output example](tca-output-streaming.md#tca-output-pii-redact-stream)\.

### Sentiment analysis<a name="tca-sentiment-stream"></a>

Sentiment analysis estimates how the customer and agent are feeling throughout the call\. This metric is provided for every speech segment and is represented as a qualitative value \(`positive`, `neutral`, `mixed`, or `negative`\)\.

Using this parameter, you can qualitatively evaluate the overall sentiment for each call participant and the sentiment for each participant during each speech segment\. This metric can help identify if your agent is able to delight an upset customer by the time the call ends\.

Sentiment analysis with real\-time Call Analytics is performed on each complete audio segment\.

Sentiment analysis works out\-of\-the\-box and thus doesn't support customization, such as model training or custom categories\.

Here's an [output example](tca-output-streaming.md#tca-output-sentiment-stream)\.