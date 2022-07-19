# Monitoring Amazon Transcribe with Amazon CloudWatch<a name="monitoring-cloudwatch"></a>

You can monitor Amazon Transcribe using CloudWatch, which collects raw data and processes it into readable, near real\-time metrics\. These statistics are kept for 15 months, so that you can access historical information and gain a better perspective on how your web application or service is performing\. You can also set alarms that watch for certain thresholds, and send notifications or take actions when those thresholds are met\. For more information, see the [CloudWatch User Guide](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/WhatIsCloudWatch.html)\.

## Using Amazon CloudWatch metrics and dimensions with Amazon Transcribe<a name="monitoring-cwmetrics"></a>

Amazon Transcribe supports CloudWatch metrics and dimensions, which are data that can help you monitor performance; supported metrics categories include traffic, errors, data transfer, and latency associated with your transcription jobs\. Supported metrics are located through CloudWatch in the **AWS/Transcribe** namespace\.

**Note**  
CloudWatch monitoring metrics are free of charge and don't count against CloudWatch service quotas\.

For more information on CloudWatch metrics, see [Using Amazon CloudWatch metrics](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/working_with_metrics.html)\.


**CloudWatch metrics for Amazon Transcribe**  

| Metric | Service Type | Description | 
| --- | --- | --- | 
| TotalRequestCount | batch |  Shows the number of transactions\. Represents all successful and unsuccessful requests made to Transcribe\. **Unit**: count **Relevant Statistics**: sum, average **Valid Dimensions**: `Domain`, `ServiceType`, `Operation`, `LanguageCode`  | 
| SuccessfulRequestCount | batch |  Shows the number of successful requests\. The response code range for a successful request is 200 to 299\. **Unit**: count **Relevant Statistics**: sum, average **Valid Dimensions**: `Domain`, `ServiceType`, `Operation`  | 
| SyncServerErrorCount | batch |  Shows the number of servers errors\. The response code range for a server error is 500 to 599\. **Unit**: count **Relevant Statistics**: sum, average **Valid Dimensions**: `Domain`, `ServiceType`, `Operation`  | 
| SyncUserErrorCount | batch |  Shows the number of user errors, such as invalid parameters, invalid file, invalid permissions, and throttling error\. The response code range for a user error is 400 to 499\.  **Unit**: count **Relevant Statistics**: sum, average **Valid Dimensions**: `Domain`, `ServiceType`, `Operation`  | 
| ThrottledCount | batch |  Shows the number of requests that return a **LimitExceededException** resulting from an exceeded transaction rate quota\. Amazon Transcribe limits the number of requests a customer can make per second\. If the quota limit set for your AWS account is frequently exceeded, you can request a quota increase\. To request an increase, see [AWS service quotas](https://docs.aws.amazon.com/general/latest/gr/aws_service_limits.html)\. **Unit**: count **Relevant Statistics**: sum, average **Valid Dimensions**: `Domain`, `ServiceType`, `Operation`  | 
| LimitExceededCount | batch |  Shows the number of requests that return a **LimitExceededException** resulting from an exceeded non\-rate quota\. Amazon Transcribe limits the number of concurrent jobs, total number of transcriptions, maximum audio file size, etc\. If the limit set for your AWS account is frequently exceeded, you can request a quota increase\. To request an increase, see [AWS service quotas](https://docs.aws.amazon.com/general/latest/gr/aws_service_limits.html)\. **Unit**: count **Relevant Statistics**: sum, average **Valid Dimensions**: `Domain`, `ServiceType`, `Operation`  | 
| AsyncUserErrorCount | batch |  The number of asynchronous \(backend\) user errors, such as: given audio format does not match that detected, invalid sample rate, customer Amazon S3 access error\. **Unit**: count **Relevant Statistics**: sum, average **Valid Dimensions**: `Domain`, `ServiceType`, `Operation` **Operations**: `StartCallAnalyticsJob`, `StartMedicalTranscriptionJob`, `StartTranscriptionJob`, `CreateMedicalVocabulary`, `CreateVocabulary`, `UpdateMedicalVocabulary`, `UpdateVocabulary`  | 
| AsyncServerErrorCount | batch |  The number of asynchronous \(backend\) server errors or, more specifically, automatic speech recognition \(ASR\) processing errors\.  **Unit**: count **Relevant Statistics**: sum, average **Valid Dimensions**: `Domain`, `ServiceType`, `Operation` **Operations**: `StartCallAnalyticsJob`, `StartMedicalTranscriptionJob`, `StartTranscriptionJob`, `CreateMedicalVocabulary`, `CreateVocabulary`, `UpdateMedicalVocabulary`, `UpdateVocabulary`  | 
| AudioDurationTime | batch |  The length, in seconds, of an audio or video file\. **Unit**: seconds **Relevant Statistics**: average, minimum, maximum **Valid Dimensions**: `Domain`, `ServiceType`, `LanguageCode`  | 


**CloudWatch dimensions for Amazon Transcribe**  

| Dimension | Description | 
| --- | --- | 
| Domain |  Only shows metrics with the specified Transcribe type\. **Valid Options**: Transcribe, Transcribe Medical, Transcribe Call Analytics  | 
| ServiceType |  Only shows metrics with the specified service type\. **Valid Options**: batch  | 
| Operation |  Only shows metrics with the specified operation\. **Valid Options**: any Amazon Transcribe API  | 
| LanguageCode |  Only shows metrics with the specified language\. **Valid Options**: any valid language code, in the form `en-US`  | 