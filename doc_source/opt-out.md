# Opting out of using your data for service improvement<a name="opt-out"></a>

By default, Amazon Transcribe stores and uses voice inputs that it has processed to develop the service and continuously improve your experience\. You can opt out of having your content used to develop and improve Amazon Transcribe by using an AWS Organizations opt\-out policy\. For information about how to opt out, see [AI services opt\-out policies](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_manage_policies_ai-opt-out.html)\.

Opting out has the following effect:
+ Amazon Transcribe deletes all of the transcripts stored in service\-managed buckets that were generated before you opted out\.
+ When you use the [StartTranscriptionJob](API_StartTranscriptionJob.md) API, you must specify where you want to store output with the `OutputBucketName` parameter\. Otherwise, you get a `BadRequestException` error\.
+ If the transcripts were stored in a service\-managed bucket, the [GetTranscriptionJob](API_GetTranscriptionJob.md) API returns `null` as the value of the `TranscriptFileUri` or `RedactedTranscriptFileUri` parameters\.

If you store transcripts in service\-managed buckets, we highly recommend backing them up\. To back up your transcripts, store them in an S3 bucket that you manage before you opt out\. To see which of your transcription jobs uses Amazon Transcribe to store its outputs, see the `OutputLocationType` response parameter of the [ListTranscriptionJobs](API_ListTranscriptionJobs.md) API\.

**To move transcripts to your own S3 buckets**



1.  In the `TranscriptionJobName` parameter of the [GetTranscriptionJob](API_GetTranscriptionJob.md) API, specify the name of the transcription job whose output you want to back up\.

1. Use the link provided in the `TranscriptFileUri` or `RedactedTranscriptFileUri` response parameters to download your transcript\.

1. Sign in to the [Amazon S3 console](https://console.aws.amazon.com/s3/)\.

1. In the **Bucket name** list, choose the name of the bucket that you want to upload your files to\.

1. Choose **Upload**\.

1. In the **Upload** dialog box, choose **Add files**\.

1. Choose one or more files to upload, and then choose **Open**\.

1. Choose **Upload**\.