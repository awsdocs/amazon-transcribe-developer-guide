# Security best practices for Amazon Transcribe<a name="security-best-practices"></a>

The following best practices are general guidelines and don’t represent a complete security solution\. Because these best practices might not be appropriate or sufficient for your environment, use them as helpful considerations rather than prescriptions\.
+ **Use data encryption, such as AWS KMS encryption context**

  AWS KMS encryption context is a map of plain text, non\-secret key:value pairs\. This map represents additional authenticated data, known as encryption context pairs, which provide an added layer of security for your data\.

  For more information, refer to [AWS KMS encryption context](data-encryption.md#kms-context)\.
+ **Use temporary credentials whenever possible**

  Where possible, use temporary credentials instead of long\-term credentials, such as access keys\. For scenarios in which you need IAM users with programmatic access and long\-term credentials, we recommend that you rotate access keys\. Regularly rotating long\-term credentials helps you familiarize yourself with the process\. This is useful in case you are ever in a situation where you must rotate credentials, such as when an employee leaves your company\. We recommend that you use *IAM access last used information* to rotate and remove access keys safely\.

  For more information, see [Rotating access keys](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html#Using_RotateAccessKey) and [Security best practices in IAM](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html)\.
+ **Use IAM roles for applications and AWS services that require Amazon Transcribe access**

  Use an IAM role to manage temporary credentials for applications or services that need to access Amazon Transcribe\. When you use a role, you don't have to distribute long\-term credentials, such as passwords or access keys, to an Amazon EC2 instance or AWS service\. IAM roles can supply temporary permissions that applications can use when they make requests to AWS resources\.

  For more information, refer to [IAM roles](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles.html) and [Common scenarios for roles: Users, applications, and services](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_common-scenarios.html)\.
+ **Use tag\-based access control**

  You can use tags to control access within your AWS accounts\. In Amazon Transcribe\. tags can be added to: transcription jobs, custom vocabularies, custom vocabulary filters, and custom language models\.

  For more information, refer to [Tag\-based access control](tagging.md#tagging-access-control)\.
+ **Use AWS monitoring tools**

  Monitoring is an important part of maintaining the reliability, security, availability, and performance of Amazon Transcribe and your AWS solutions\. You can monitor Amazon Transcribe using CloudTrail\.

  For more information, refer to [Monitoring Amazon Transcribe with AWS CloudTrail](monitoring-transcribe-cloud-trail.md)\.
+ **Enable AWS Config**

  AWS Config can assess, audit, and evaluate the configurations of your AWS resources\. Using AWS Config, you can review changes in configurations and relationships between AWS resources\. You can also investigate detailed resource configuration histories and determine your overall compliance against the configurations specified in your internal guidelines\. This can help you simplify compliance auditing, security analysis, change management, and operational troubleshooting\.

  For more information, refer to [What Is AWS Config?](https://docs.aws.amazon.com/config/latest/developerguide/WhatIsConfig.html)