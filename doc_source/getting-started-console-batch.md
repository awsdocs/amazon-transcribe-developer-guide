# Batch transcriptions<a name="getting-started-console-batch"></a>

First make sure that you've uploaded the media file you want to transcribe into an Amazon S3 bucket\. If you're unsure how to do this, refer to the Amazon S3 User Guide: [Upload an object to your bucket](https://docs.aws.amazon.com/AmazonS3/latest/userguide/uploading-an-object-bucket.html)\.

1. From the [AWS Management Console](https://console.aws.amazon.com/transcribe), select **Transcription jobs** in the left navigation pane\. This takes you to a list of your transcription jobs\.  
![\[Amazon Transcribe console screenshot: the 'transcription jobs' page.\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/console-batch-1.png)![\[Amazon Transcribe console screenshot: the 'transcription jobs' page.\]](http://docs.aws.amazon.com/transcribe/latest/dg/)

   Select **Create job**\.

1. Complete the fields on the **Specify job details** page\.  
![\[Amazon Transcribe console screenshot: the 'specify job details' page.\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/console-batch-job-details-1.png)![\[Amazon Transcribe console screenshot: the 'specify job details' page.\]](http://docs.aws.amazon.com/transcribe/latest/dg/)

   The input location *must* be an object within an Amazon S3 bucket\. For output location, you can choose a secure Amazon S3 service\-managed bucket or you can specify your own Amazon S3 bucket\.

   If you choose a service\-managed bucket, you can view a transcript preview in the AWS Management Console and you can download your transcript from the job details page \(see below\)\.

   If you choose your own Amazon S3 bucket, you cannot see a preview in the AWS Management Console and must go to the Amazon S3 bucket to download your transcript\.  
![\[Amazon Transcribe console screenshot: the input and output data panes for a batch transcription.\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/console-batch-job-details-2.png)![\[Amazon Transcribe console screenshot: the input and output data panes for a batch transcription.\]](http://docs.aws.amazon.com/transcribe/latest/dg/)

   Select **Next**\.

1. Select any desired options on the **Configure job** page\. If you want to use [Custom vocabularies](custom-vocabulary.md) or [Custom language models](custom-language-models.md) with your transcription, you must create these before starting your transcription job\.  
![\[Amazon Transcribe console screenshot: the 'configure job' page.\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/console-batch-configure-job.png)![\[Amazon Transcribe console screenshot: the 'configure job' page.\]](http://docs.aws.amazon.com/transcribe/latest/dg/)

   Select **Create job**\.

1. You're now on the **Transcription jobs** page\. Here you can see the status of the transcription job\. Once complete, click on the name of your transcription\.  
![\[Amazon Transcribe console screenshot: the transcription jobs summary page.\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/console-batch-transcription-jobs.png)![\[Amazon Transcribe console screenshot: the transcription jobs summary page.\]](http://docs.aws.amazon.com/transcribe/latest/dg/)

1. You're now viewing the **Job details** page for your transcription\. Here you can view all of the options you specified when setting up your transcription job\.

   To view your transcript, select the linked filepath in the right column under **Output data location**\. This takes you to the Amazon S3 output folder you specified\. Click on the name you of your output file, which now has a \.json extension\.  
![\[Amazon Transcribe console screenshot: summary page for completed transcription.\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/console-batch-complete.png)![\[Amazon Transcribe console screenshot: summary page for completed transcription.\]](http://docs.aws.amazon.com/transcribe/latest/dg/)

1. How you download your transcript depends on whether you chose a service\-managed Amazon S3 bucket or your own Amazon S3 bucket\.

   1. If you chose a service\-managed bucket, you can see a **Transcription preview** pane on your transcription job's information page, along with a **Download** button\.  
![\[Amazon Transcribe console screenshot: summary page for transcription in a service-managed bucket.\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/console-batch-output-service-s3.png)![\[Amazon Transcribe console screenshot: summary page for transcription in a service-managed bucket.\]](http://docs.aws.amazon.com/transcribe/latest/dg/)

      Select **Download** and choose **Download transcript**\.

   1. If you chose your own Amazon S3 bucket, you don't see any text in the **Transcription preview** pane on your transcription job's information page\. Instead, you see a blue information box with a link to the Amazon S3 bucket you chose\.  
![\[Amazon Transcribe console screenshot: summary page for transcription in a self-managed bucket.\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/console-batch-output-own-s3.png)![\[Amazon Transcribe console screenshot: summary page for transcription in a self-managed bucket.\]](http://docs.aws.amazon.com/transcribe/latest/dg/)

      To access your transcript, go to the specified Amazon S3 bucket using either the link under **Output data location** in the **Job details** pane or the **S3 Bucket** link within the blue information box in the **Transcription preview** pane\.