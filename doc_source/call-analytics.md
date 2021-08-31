# Call analytics<a name="call-analytics"></a>

Call analytics helps you gain insight into the content and sentiment of your recordings, which you can use to create a better customer experience and improve product development\. Using call analytics, you can:
+ **Identify the sentiment of each participant**: Sentiment analysis tells you how the customer and agent were feeling during the call \(positive, neutral, or negative\)\.
+ **Perform automated call categorization**: Set flags for key words and phrases, sentiment, non\-talk time, or interruptions\.
+ **Perform call issue detection**: Identify the reason for the call \(for example, did the customer call about the wrong item being delivered or was their item damaged in transit?\)\.
+ **Redact sensitive data**: Replace personally identifiable information \(PII\) in both the text transcript and the audio file\. A redacted transcript will replace PII with `[PII]`; a redacted audio file will replace PII with silence\. To learn more about redaction with Amazon Transcribe, see [Content redaction](content-redaction.md)\.
+ **Extract conversation characteristics**: Identify the amount of non\-talk time, number of interruptions, talk speed, or sentiment trends\.

For a list of languages that support call analytics, refer to [Supported languages and language\-specific features](how-it-works.md#table-language-matrix)\.

**Note**  
If **content redaction** is enabled, you can only use call analytics in U\.S\. English \(en\-US\)\.  
Input files for call analytics cannot be greater than 500 MB and must be less than 4 hours\.

Using the call analytics **categories** feature, you can create categories with one to 20 rules\. Amazon Transcribe then uses the rules you've defined within a category to identify phrases or conversational characteristics within your transcript that match your rules\. For example, you can create a category with the following rules:
+ *Rule 1*: The agent didn't say the welcoming phrase “How are you today?” during the first two minutes of the call\.
+ *Rule 2*: There's silence \(a period when neither the customer nor agent spoke\) that lasted longer than one minute\. 

If you run a call analytics job and the characteristics of that job match the rules you've specified in a category, Amazon Transcribe automatically flags your job with that category\.

You can create as many categories as you'd like to cover a range of different situations\. Using a variety of categories can help you determine how your rules and/or categories may correlate\. For example, you might hypothesize that an agent not using a greeting is correlated with negative customer sentiment\. To test this hypothesis, you can create two separate categories: category 1 has a rule for an agent not using a specific greeting; category 2 has a rule that the customer sentiment during the call was negative for the last five minutes\. When you run your analytics jobs, you can then see how these categories correlate, if at all\.

**Note**  
A call analytics job only uses the categories you've previously created\. Any new categories cannot be applied to previous call analytics jobs\.

For call analytics quotas, refer to [Guidelines and quotas](limits-guidelines.md)\.

To use call analytics in your transcription job, use [ StartCallAnalyticsJob ](API_StartCallAnalyticsJob.md) or **call analytics job** in th econsole\. Call analytics output is similar to that of a standard transcription job, but contains additional data based on the analytics categories you create\. To learn how to set up a call analytics job, see [Setting up call analytics transcription jobs](start-call-analytics.md)\. For example output, see [Sample call analytics output](analyze-output.md)\.

**Tip**  
To view sample call analytics output and features, check out our [GitHub demo](https://github.com/aws-samples/amazon-transcribe-output-word-document)\.