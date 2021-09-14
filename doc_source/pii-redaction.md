# Redacting or identifying personally identifiable information<a name="pii-redaction"></a>

Use *content redaction* to omit sensitive personally identifiable information \(PII\) from your transcription results\. Use *content identification* to flag PII in your transcript without redacting it\.

**Important**  
The redaction feature is designed to identify and remove sensitive data\. However, due to the predictive nature of machine learning, Amazon Transcribe may not identify and remove all instances of sensitive data in your transcript\. We strongly recommend that you review any redacted output to ensure it meets your needs\.  
The redaction feature does not meet the requirements for de\-identification under medical privacy laws, such as the U\.S\. Health Insurance Portability and Accountability Act of 1996 \(HIPAA\)\.

PII redaction can be performed on batch transcription jobs and streaming transcriptions, whereas PII identification can only be performed on streaming transcriptions\. With batch transcription jobs, you can choose to have both a redacted and an unredacted transcript\.

Amazon Transcribe can identify the following types of PII:


| PII entity | Definition | 
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

**Topics**
+ [Redacting or identifying PII in an audio file](pii-redaction-batch.md)
+ [Redacting or identifying PII in a real\-time stream](pii-redaction-stream.md)
+ [Example PII redaction and identification output](redaction-output.md)