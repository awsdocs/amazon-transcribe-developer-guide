# Batch transcriptions<a name="getting-started-console-batch"></a>

First make sure that you've uploaded the media file you want to transcribe into an S3 bucket\. If you're unsure how to do this, refer to the Amazon S3 User Guide: [Upload an object to your bucket](https://docs.aws.amazon.com/AmazonS3/latest/userguide/uploading-an-object-bucket.html)\.

1. From the [AWS Management Console](https://console.aws.amazon.com/transcribe), select **Transcription jobs** in the left navigation pane\. This takes you to a list of your transcription jobs\.  
![\[The Amazon Transcribe create job page.\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/console-batch-1.png)![\[The Amazon Transcribe create job page.\]](http://docs.aws.amazon.com/transcribe/latest/dg/)

   Click the **Create job** button\.

1. Complete the fields on the **Specify job details** page\.  
![\[The Amazon Transcribe specify job details page.\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/console-batch-job-details-1.png)![\[The Amazon Transcribe specify job details page.\]](http://docs.aws.amazon.com/transcribe/latest/dg/)

   The input location *must* be an object within an S3 bucket\. For output location, you can choose a secure AWS service\-managed bucket or you can specify your own S3 bucket\.

   If you choose a service\-managed bucket, you can view a transcript preview in the AWS Management Console and you can download your transcript from the job details page \(see below\)\.

   If you choose your own S3 bucket, you cannot see a preview in the AWS Management Console and must go to the S3 bucket to download your transcript\.  
![\[The Amazon Transcribe specify job details page: specify your input and output buckets.\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/console-batch-job-details-2.png)![\[The Amazon Transcribe specify job details page: specify your input and output buckets.\]](http://docs.aws.amazon.com/transcribe/latest/dg/)

   Click **Next**\.

1. Select any desired options on the **Configure job** page\. If you want to use [Custom vocabularies](custom-vocabulary.md) or [Custom language models](custom-language-models.md) with your transcription, you must create these before starting your transcription job\.  
![\[The Amazon Transcribe specify job details page.\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/console-batch-configure-job.png)![\[The Amazon Transcribe specify job details page.\]](http://docs.aws.amazon.com/transcribe/latest/dg/)

   Click **Create job**\.

1. You're now the **Transcription jobs** page\. Here you can see the status of the transcription job\. Once complete, click on the name of your transcription\.  
![\[The Amazon Transcribe specify job details page.\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/console-batch-transcription-jobs.png)![\[The Amazon Transcribe specify job details page.\]](http://docs.aws.amazon.com/transcribe/latest/dg/)

1. You're now viewing the **Job details** page for your transcription\. Here you can view all of the options you specified when setting up your transcription job\.

   To view your transcript, select the linked filepath in the right column under **Output data location**\. This takes you to the S3 output folder you specified\. Click on the name you of your output file, which now has a \.json extension\.  
![\[The Amazon Transcribe job summary page.\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/console-batch-complete.png)![\[The Amazon Transcribe job summary page.\]](http://docs.aws.amazon.com/transcribe/latest/dg/)

1. How you download your transcript depends on whether you chose a service\-managed S3 bucket or your own S3 bucket\.

   1. If you chose a service\-managed bucket, you can see a **Transcription preview** pane on your transcription job's information page, along with a **Download** button\.  
![\[Your transcription information page.\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/console-batch-output-service-s3.png)![\[Your transcription information page.\]](http://docs.aws.amazon.com/transcribe/latest/dg/)

      Click on the **Download** button and choose **Download transcript**\.

   1. If you chose your own S3 bucket, you don't see any text in the **Transcription preview** pane on your transcription job's information page\. Instead, you see a blue information box with a link to the S3 bucket you chose\.  
![\[Your transcription information page.\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/console-batch-output-own-s3.png)![\[Your transcription information page.\]](http://docs.aws.amazon.com/transcribe/latest/dg/)

      To access your transcript, go to the specified S3 bucket using either the link under **Output data location** in the **Job details** pane or the **S3 Bucket** link within the blue information box in the **Transcription preview** pane\.