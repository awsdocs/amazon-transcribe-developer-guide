# Redacting or identifying personally identifiable information<a name="pii-redaction"></a>

Redaction is used to mask or remove sensitive content, in the form of personally identifiable information \(PII\), from your transcripts\. Amazon Transcribe can redact information with batch jobs and streaming transcriptions\. Additionally, if you're performing a streaming transcription, you also have the option to flag PII without redacting it; see [Example PII identification output](pii-redaction-output.md#pii-redaction-output-id) for an example\.


**Types of PII Amazon Transcribe can recognize**  

| PII type | Description | 
| --- | --- | 
| Bank Account Number | A number that uniquely identifies a bank account\. | 
| Bank Routing Number | A number that identifies the location of a bank account\. | 
| Credit Card Number or Debit Card Number | A value that uniquely defines a payment card issued by a bank\. | 
| Credit Card or Debit Card CVV Code |  A 3\-digit or 4\-digit security code on each credit card\. | 
| Credit Card or Debit Card Expiration Date | The month and year a card expires\. | 
|  Debit or credit card PIN  |  A security code issued by a bank or credit union\. This number is used for bank accounts and payment cards\.  | 
| Email address | The unique identifier of an email box where messages are delivered\. | 
| U\.S\. mailing address | The United States mailing address of an individual\. | 
| Name | The first and last name of a person\. | 
| U\.S\. phone number | A 10\-digit phone number within the United States\.  | 
| Social Security Number | A 9\-digit number \(or the last 4 digits of that number\)\. Issued to U\.S\. citizens, permanent residents, and temporary residents with employment\. | 
| All PII | Redact or identify all PII types listed in this table\. | 

When redaction is enabled, you have the option to generate only a redacted transcript or both a redacted transcript and an unredacted transcript\. If you choose to generate only a redacted transcript, note that your media file is the only place where the complete conversation is stored\. If you delete it, there is no record of the unredacted PII\. Because of this, it may be prudent to generate an unredacted transcript in addition to a redacted one\.

To learn more about PII redaction with an audio file, refer to: [Redacting PII in your batch job](pii-redaction-batch.md)\.

To learn more about PII redaction or identification with a media stream, refer to: [Redacting or identifying PII in a real\-time stream](pii-redaction-stream.md)\.

**Important**  
The redaction feature is designed to identify and remove sensitive data\. However, due to the predictive nature of machine learning, Amazon Transcribe may not identify and remove all instances of sensitive data in your transcript\. We strongly recommend that you review any redacted output to ensure it meets your needs\.  
The redaction feature does not meet the requirements for de\-identification under medical privacy laws, such as the U\.S\. Health Insurance Portability and Accountability Act of 1996 \(HIPAA\)\.

Redaction is supported with U\.S\. English \(en\-US\) only\.