# Monitoring Amazon Transcribe API Calls with AWS CloudTrail<a name="monitoring-transcribe-cloud-trail"></a>

To create a log of Amazon Transcribe API calls, use AWS CloudTrail\. CloudTrail captures and stores log entries in an Amazon S3 bucket\. CloudTrail logs calls made from the Amazon Transcribe console or API\. You can use the logs to track requests made to Amazon Transcribe, the source IP address from which requests were made, who made the requests, when they were made, and so on\.

All Amazon Transcribe operations are logged by CloudTrail and are documented in the Amazon Transcribe [API Reference](API_Reference.md)\.

Every log entry contains information about who generated the request\. Use the user identity in log entries to determine whether the request was made:
+ With root or IAM user credentials
+ With temporary security credentials for an IAM role or federated user
+ By another AWS service

For more information, see the [CloudTrail userIdentity Element](http://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-event-reference-user-identity.html)\.

To log calls, you need to enable and configure CloudTrail You can configure: 
+ The bucket where log files are created\.
+ The frequency that new log files are created\.
+ The maximum size of a log file\.

You can store your log files in the bucket for as long as you want\. To archive or delete log files automatically, you can define Amazon S3 lifecycle rules \. By default, your log files are encrypted with Amazon S3 server\-side encryption \(SSE\)\.

To be notified when CloudTrail delivers log files, configure CloudTrail to publish Amazon SNS notifications\. For more information, see [Configuring Amazon SNS Notifications for CloudTrail](http://docs.aws.amazon.com/awscloudtrail/latest/userguide/getting_notifications_top_level.html) in the [AWS CloudTrail User Guide](http://docs.aws.amazon.com/awscloudtrail/latest/userguide/)\.

To learn more about CloudTrail, including how to configure and enable it, see the [AWS CloudTrail User Guide](http://docs.aws.amazon.com/awscloudtrail/latest/userguide/)\.

## <a name="aws-transcribe-info-in-cloudtrail"></a>

You can also aggregate Amazon Transcribe log files from multiple AWS Regions and multiple AWS accounts into a single S3 bucket\. For more information, see [Receiving CloudTrail Log Files from Multiple Regions](http://docs.aws.amazon.com/awscloudtrail/latest/userguide/receive-cloudtrail-log-files-from-multiple-regions.html) and [Receiving CloudTrail Log Files from Multiple Accounts](http://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-receive-logs-from-multiple-accounts.html)\. 

### Example: Amazon Transcribe Log File Entries<a name="cloud-trail-log-entry"></a>

CloudTrail log files can contain one or more log entries in the bucket that you specified when you created the trail\. A log entry represents a single request from any source and includes information about the requested action, the date and time of the action, request parameters, and so on\. Log entries are not an ordered stack trace of the public API calls\. They don't appear in any specific order\.

The following log entry shows the result of calls to the `ListTranscriptionJobs` and `GetTranscriptionJob` operations:

```
{
    "Records": [
        {
            "eventVersion": "1.05",
            "userIdentity": {
                "type": "AssumedRole | FederatedUser | IAMUser | Root | SAMLUser | WebIdentityUser",
                "principalId": "principal ID",
                "arn": "ARN",
                "accountId": "account ID",
                "accessKeyId": "access key",
                "userName": "user name"
            },
            "eventTime": "timestamp",
            "eventSource": "transcribe.amazonaws.com",
            "eventName": "StartTranscriptionJob",
            "awsRegion": "region",
            "sourceIPAddress": "source IP address",
            "userAgent": "user agent",
            "requestParameters": {
                "mediaFormat": "flac | mp3 | mp4 | wav",
                "languageCode": "en-US | es-US",
                "transcriptionJobName": "unique job name",
                "media": {
                    "mediaFileUri": ""
                }
            },
            "responseElements": {
                "transcriptionJob": {
                    "transcriptionJobStatus": "IN_PROGRESS",
                    "mediaFormat": "flac | mp3 | mp4 | wav",
                    "creationTime": "timestamp",
                    "transcriptionJobName": "unique job name",
                    "languageCode": "en-US | es-US",
                    "media": {
                        "mediaFileUri": ""
                    }
                }
            },
            "requestID": "request ID",
            "eventID": "event ID",
            "eventType": "AwsApiCall",
            "recipientAccountId": "account id"
        },
        {
            "eventVersion": "1.05",
            "userIdentity": {
                "type": "AssumedRole | FederatedUser | IAMUser | Root | SAMLUser | WebIdentityUser",
                "principalId": "principal ID",
                "arn": "ARN",
                "accountId": "account ID",
                "accessKeyId": "access key",
                "userName": "user name"
            },
            "eventTime": "timestamp",
            "eventSource": "transcribe.amazonaws.com",
            "eventName": "GetTranscriptionJob",
            "awsRegion": "region",
            "sourceIPAddress": "source IP address",
            "userAgent": "user agent",
            "requestParameters": {
                "transcriptionJobName": "unique job name"
            },
            "responseElements": {
                "transcriptionJob": {
                    "settings": {
                        
                    },
                    "transcriptionJobStatus": "COMPLETED | FAILED | IN_PROGRESS",
                    "mediaFormat": "flac | mp3 | mp4 | wav",
                    "creationTime": "timestamp",
                    "transcriptionJobName": "unique job name",
                    "languageCode": "en-US | es-US",
                    "media": {
                        "mediaFileUri": ""
                    },
                    "transcript": {
                        "transcriptFileUri": ""
                    }
                }
            },
            "requestID": "request ID",
            "eventID": "event ID",
            "eventType": "AwsApiCall",
            "recipientAccountId": "account id"
        }        
    ]
}
```