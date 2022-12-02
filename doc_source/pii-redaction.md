# Redacting or identifying personally identifiable information<a name="pii-redaction"></a>

Redaction is used to mask or remove sensitive content, in the form of personally identifiable information \(PII\), from your transcripts\. The types of PII Amazon Transcribe can redact varies between batch and streaming transcriptions\. To view the PII list for each transcription method, refer to [Redacting PII in your batch job](pii-redaction-batch.md) and [Redacting or identifying PII in a real\-time stream](pii-redaction-stream.md)\. With streaming transcriptions, you also have the option to flag PII without redacting it; refer to [Example PII identification output](pii-redaction-output.md#pii-redaction-output-id) for an output example\.

When redaction is enabled, you have the option to generate only a redacted transcript or both a redacted transcript and an unredacted transcript\. If you choose to generate only a redacted transcript, note that your media is the only place where the complete conversation is stored\. If you delete your original media, there is no record of the unredacted PII\. Because of this, it may be prudent to generate an unredacted transcript in addition to a redacted one\.

To learn more about PII redaction with batch transcriptions, refer to: [Redacting PII in your batch job](pii-redaction-batch.md)\.

To learn more about PII redaction or identification with streaming transcriptions, refer to: [Redacting or identifying PII in a real\-time stream](pii-redaction-stream.md)\.

**Important**  
The redaction feature is designed to identify and remove sensitive data\. However, due to the predictive nature of machine learning, Amazon Transcribe may not identify and remove all instances of sensitive data in your transcript\. We strongly recommend that you review any redacted output to ensure it meets your needs\.  
The redaction feature does not meet the requirements for de\-identification under medical privacy laws, such as the U\.S\. Health Insurance Portability and Accountability Act of 1996 \(HIPAA\)\.

For a video walkthrough of redacting and identifying PII, see:

[![AWS Videos](http://img.youtube.com/vi/https://www.youtube.com/embed/4H8dQoeLkyM/0.jpg)](http://www.youtube.com/watch?v=https://www.youtube.com/embed/4H8dQoeLkyM)