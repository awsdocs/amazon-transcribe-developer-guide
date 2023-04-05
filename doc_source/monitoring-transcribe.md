# Monitoring Amazon Transcribe<a name="monitoring-transcribe"></a>

Monitoring is an important part of maintaining the reliability, availability, and performance of Amazon Transcribe and your other AWS solutions\. AWS provides the following monitoring tools to watch Amazon Transcribe, report when something is wrong, and take automatic actions when appropriate:
+ **Amazon CloudWatch** monitors your AWS resources and the applications that you run on AWS in real time\. You can collect and track metrics, create customized dashboards, and set alarms that notify you or take actions when a specified metric reaches a threshold that you specify\. For example, you can have CloudWatch track CPU usage or other metrics on your Amazon EC2 instances and automatically launch new instances when needed\.
+ **Amazon CloudWatch Logs** can monitor, store, and access your log files from Amazon EC2 instances, CloudTrail, and other sources\. CloudWatch Logs can monitor information in the log files and notify you when certain thresholds are met\. You can also archive your log data in highly durable storage\.
+ **AWS CloudTrail** captures API calls and related events made by or on behalf of your AWS account and delivers the log files to an Amazon S3 bucket that you specify\. You can identify which users and accounts called AWS, the source IP address from which the calls were made, and when the calls occurred\.

For more information, see the *[Amazon CloudWatch User Guide](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/WhatIsCloudWatch.html)*\.

**Amazon EventBridge** is a serverless service that uses events to connect application components together, making it easier for you to build scalable event\-driven applications\. EventBridge delivers a stream of real\-time data from your own applications, Software as a Service \(SaaS\) applications, and AWS services and routes that data to targets such as Lambda\. You can monitor events that happen in services, and build event\-driven architectures\. For more information, see the *[Amazon EventBridge User Guide](https://docs.aws.amazon.com/eventbridge/latest/userguide/eb-what-is.html)*\.

**Topics**
+ [Monitoring Amazon Transcribe with Amazon CloudWatch](monitoring-cloudwatch.md)
+ [Monitoring Amazon Transcribe with AWS CloudTrail](monitoring-transcribe-cloud-trail.md)
+ [Using Amazon EventBridge with Amazon Transcribe](monitoring-events.md)