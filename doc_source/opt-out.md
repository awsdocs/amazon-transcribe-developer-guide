# Opting out of using your data for service improvement<a name="opt-out"></a>

By default, Amazon Transcribe stores and uses voice inputs that it has processed to develop the service and continuously improve your experience\. You can opt out of having your content used to develop and improve Amazon Transcribe by using an AWS Organizations opt\-out policy\. For information about how to opt out, see [AI services opt\-out policies](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_manage_policies_ai-opt-out.html)\.

Opting out results in:
+ Deletion of all transcripts stored in service\-managed buckets\.
+ Disallowed future use of service\-managed buckets\.

  After opting out, you must specify an output location \(`OutputBucketName` or `OutputLocation`\) for your transcripts when you make a [https://docs.aws.amazon.com/transcribe/latest/APIReference/API_StartTranscriptionJob.html](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_StartTranscriptionJob.html), [https://docs.aws.amazon.com/transcribe/latest/APIReference/API_StartMedicalTranscriptionJob.html](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_StartMedicalTranscriptionJob.html), or [https://docs.aws.amazon.com/transcribe/latest/APIReference/API_StartCallAnalyticsJob.html](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_StartCallAnalyticsJob.html) request\. If you don't specify an output location, you get a `BadRequestException` error\.

If you want to keep any transcripts stored in service\-managed buckets, you must download them prior to opting out\. To see which of your transcripts are in service\-managed buckets, make a [https://docs.aws.amazon.com/transcribe/latest/APIReference/API_ListTranscriptionJobs.html](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_ListTranscriptionJobs.html) request and note the location specified in `OutputLocationType`\.