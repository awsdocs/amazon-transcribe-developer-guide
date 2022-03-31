# Transcribing with the AWS CLI<a name="getting-started-cli"></a>

When using the AWS CLI to start a transcription, you can either run all commands at the CLI level or you can run the Amazon Transcribe command you wish to use followed by the AWS Region and the location of a JSON file that contains a request body\. Examples throughout this guide show both methods; however, this section focuses on the former method\.

The AWS CLI does not support streaming transcriptions\.

Before you continue, make sure you've:
+ Uploaded your media file into an S3 bucket\. If you're unsure how to create an S3 bucket or upload your file, refer to [Create your first S3 bucket](https://docs.aws.amazon.com/AmazonS3/latest/userguide/creating-bucket.html) and [Upload an object to your bucket](https://docs.aws.amazon.com/AmazonS3/latest/userguide/uploading-an-object-bucket.html)\.
+ Installed the [AWS CLI](getting-started.md#getting-started-api)\.

You can find all AWS CLI commands for Amazon Transcribe in the [AWS CLI Command Reference](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/transcribe/index.html#cli-aws-transcribe)\.

## Starting a new transcription job<a name="getting-started-cli-start-job"></a>

To start a new transcription, use the `start-transcription-job` command\.

1. In a terminal window, type the following:

   ```
   aws transcribe start-transcription-job \
   ```

   A '`>`' appears on the next line and you can now continue adding required parameters, as described in the next step\.

   You can also omit the '`\`' and append all parameters, separating each with a space\.

1. With the `start-transcription-job` command, you must include `region`, `transcription-job-name`, `media`, and either `language-code` or `identify-language`\.

   ```
   aws transcribe start-transcription-job \
    --region us-west-2 \
    --transcription-job-name my-first-transcription-job \
    --media MediaFileUri=s3://DOC-EXAMPLE-BUCKET/my-media-file.flac \
    --language-code en-US
   ```

   If appending all parameters, this request looks like:

   ```
   aws transcribe start-transcription-job --region us-west-2 --transcription-job-name my-first-transcription-job --media MediaFileUri=s3://DOC-EXAMPLE-BUCKET/my-media-file.flac --language-code en-US
   ```

   If you choose not to specify an output bucket using `output-bucket-name`, Amazon Transcribe places your transcription output in a service\-managed bucket\. Transcripts stored in a service\-managed bucket expire after 90 days\.

   Amazon Transcribe responds with:

   ```
   {
       "TranscriptionJob": {
           "TranscriptionJobName": "my-first-transcription-job",
           "TranscriptionJobStatus": "IN_PROGRESS",
           "LanguageCode": "en-US",
           "Media": {
               "MediaFileUri": "s3://DOC-EXAMPLE-BUCKET/my-media-file.flac"
           },
           "StartTime": "2022-03-07T15:03:44.246000-08:00",
           "CreationTime": "2022-03-07T15:03:44.229000-08:00"
       }
   }
   ```

To see if your transcription job is successful, as indicated by [https://docs.aws.amazon.com/transcribe/latest/APIReference/API_TranscriptionJob.html#transcribe-Type-TranscriptionJob-TranscriptionJobStatus](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_TranscriptionJob.html#transcribe-Type-TranscriptionJob-TranscriptionJobStatus) changing from `IN_PROGRESS` to `COMPLETED`, use the `get-transcription-job` or `list-transcription-job` command, as shown in the following section\.

## Getting the status of a transcription job<a name="getting-started-cli-get-job"></a>

To get information about your transcription job, use the `get-transcription-job` command\.

The only required parameters for this command are the AWS Region where the job is located and the name of the job\.

```
aws transcribe get-transcription-job \
 --region us-west-2 \
 --transcription-job-name my-first-transcription-job
```

Amazon Transcribe responds with:

```
{
    "TranscriptionJob": {
        "TranscriptionJobName": "my-first-transcription-job",
        "TranscriptionJobStatus": "COMPLETED",
        "LanguageCode": "en-US",
        "MediaSampleRateHertz": 48000,
        "MediaFormat": "flac",
        "Media": {
            "MediaFileUri": "s3://DOC-EXAMPLE-BUCKET/my-media-file.flac"
        },
        "Transcript": {
            "TranscriptFileUri": "https://s3.the-URI-where-your-job-is-located"
        },
        "StartTime": "2022-03-07T15:03:44.246000-08:00",
        "CreationTime": "2022-03-07T15:03:44.229000-08:00",
        "CompletionTime": "2022-03-07T15:04:01.158000-08:00",
        "Settings": {
            "ChannelIdentification": false,
            "ShowAlternatives": false
        }
    }
}
```

If you've selected your own S3 bucket for your transcription output, this bucket is listed with `TranscriptFileUri`\. If you've selected a service\-managed bucket, a temporary URI is provided; use this URI to download your transcript\.

**Note**  
Temporary URIs for service\-managed S3 buckets are only valid for 15 minutes\. If you get an `AccesDenied` error when using the URI, run the `get-transcription-job` request again to get a new temporary URI\.

## Listing your transcription jobs<a name="getting-started-cli-list-jobs"></a>

To list all your transcription jobs in a given AWS Region, use the `list-transcription-jobs` command\.

The only required parameter for this command is the AWS Region in which your transcription jobs are located\.

```
aws transcribe list-transcription-jobs \
 --region us-west-2
```

Amazon Transcribe responds with:

```
{
    "NextToken": "A-very-long-string",
    "TranscriptionJobSummaries": [
        {
            "TranscriptionJobName": "my-first-transcription-job",
            "CreationTime": "2022-03-07T15:03:44.229000-08:00",
            "StartTime": "2022-03-07T15:03:44.246000-08:00",
            "CompletionTime": "2022-03-07T15:04:01.158000-08:00",
            "LanguageCode": "en-US",
            "TranscriptionJobStatus": "COMPLETED",
            "OutputLocationType": "SERVICE_BUCKET"
        }        
    ]
}
```

## Deleting your transcription job<a name="getting-started-cli-delete-job"></a>

To delete your transcription job, use the `delete-transcription-job` command\.

The only required parameters for this command are the AWS Region where the job is located and the name of the job\.

```
aws transcribe delete-transcription-job \
 --region us-west-2 \
 --transcription-job-name my-first-transcription-job
```

To confirm your delete request is successful, you can run the `list-transcription-jobs` command; your job should no longer appear in the list\.