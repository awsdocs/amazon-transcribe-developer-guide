# Sensitive data redaction<a name="call-analytics-pii-redaction"></a>

Sensitive data redaction replaces personally identifiable information \(PII\) in the text transcript and the audio file\. A redacted transcript replaces the original text with `[PII]`; a redacted audio file replaces spoken personal information with silence\. This parameter is useful for protecting customer information\.

**Note**  
Redaction is supported with US English \(en\-US\) only\.

PII redaction works out\-of\-the\-box, and thus doesn't support customization\. To view the list of PII that is redacted using this feature, or to learn more about redaction with Amazon Transcribe, see [Redacting or identifying personally identifiable information](pii-redaction.md)\.

Here's what sensitive data redaction looks like in your transcription output:

```
"Content": "Hey Mr [PII]? Um I think I lost my debit card or it was stolen. I don't know."
```

When you're ready to set up a call analytics job, see [Start a call analytics transcription job](call-analytics-start.md)\.