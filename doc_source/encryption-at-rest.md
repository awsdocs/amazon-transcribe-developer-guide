# Encryption at Rest<a name="encryption-at-rest"></a>

Amazon Transcribe uses the default Amazon S3 key \(SSE\-S3\) for server\-side encryption of transcripts placed in your S3 bucket\.

When you use the [StartTranscriptionJob](API_StartTranscriptionJob.md) operation, you can specify your own AWS Key Management Service key to encrypt the output from a transcription job\.

Amazon Transcribe uses an Amazon EBS volume encrypted with the default key\.