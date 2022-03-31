# Job queuing<a name="job-queuing"></a>

When you send transcription jobs to Amazon Transcribe, there is a limit to the total number of jobs that can run at one time\. By default, there are 250 slots for jobs\. When the limit is reached, you must wait until one or more jobs have finished and freed up a slot before you can send your next job\.

To queue jobs so that they run as soon as a slot becomes available, you can use *job queuing*\. Job queuing creates a queue on your behalf that contains your jobs\. When a slot is available, Amazon Transcribe takes the next job from the queue and immediately starts processing it\. To allow resources for new jobs to be submitted and processed, Amazon Transcribe uses at most 90 percent of your slots to process jobs in the queue\.

You can turn on job queuing with the AWS Management Console, or you can set the `AllowDeferredExecution` field of the `JobExecutionSettings` parameter to `true` when you call the [StartTranscriptionJob](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_StartTranscriptionJob.html) API\. 

When you submit a job with job queuing turned on, one of the following things happens\.
+ If slots are available, the job is processed immediately\.
+ If no slots are available, the job is sent into a queue\. When slots become available, jobs are removed from the queue in FIFO order \(first in, first out\)\.

You can see the progress of a queued job using the console or by using the [GetTranscriptionJob](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_GetTranscriptionJob.html) API\. When a job is queued, the `Status` field of the `TranscriptionJob` object returned by the [StartTranscriptionJob](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_StartTranscriptionJob.html) API is set to `QUEUED`\. The status changes to `IN_PROGRESS` when Amazon Transcribe starts processing the audio, and then changes to either `COMPLETED` or `FAILED` when processing is finished\. You can use the `TranscriptionJobName` field with the [GetTranscriptionJob](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_GetTranscriptionJob.html) API to monitor the status of a job\. 

You can submit up to 10,000 jobs to the queue\. If you exceed 10,000 jobs, you get a `LimitExceededConcurrentJobException` exception\.

## IAM policies for job queuing<a name="job-queuing-policy"></a>

To use job queuing, you must provide Amazon Transcribe with a data access role that permits access to the audio you want transcribed\. You can choose the data access role using the AWS Management Console, or you use the `DataAccessRoleArn` field of the `JobExecutionSettings` parameter of the [StartTranscriptionJob](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_StartTranscriptionJob.html) API to specify the role to use\.

The role policies that you use depend on where you are storing your input files, where you are storing your output files, and whether you are encrypting the output with an AWS KMS key\. The IAM policies in this section are required for the role\. The policies enable Amazon Transcribe to work on your behalf, allow access to the input and output locations for your jobs, and enable Amazon Transcribe to use a KMS key to encrypt your transcriptions\.

### Trust policy<a name="job-queuing-trust-policy"></a>

The data access role that you use for transcription must have a trust policy that enables Amazon Transcribe to assume the role\. Use the following trust policy\.

```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "",
      "Effect": "Allow",
      "Principal": {
        "Service": [
          "transcribe.amazonaws.com",
        ]
      },
      "Action": "sts:AssumeRole"
    }
  ]
}
```

### Input bucket policy<a name="job-queuing-input-bucket"></a>

The following IAM policy gives the data access role permission to read files from your input bucket\.

```
{
    "Version": "2012-10-17",
    "Statement": {
        "Effect": "Allow",
        "Action": [
            "s3:GetObject",
            "s3:ListBucket"
        ],
        "Resource": [
            "arn:aws:s3:::input-bucket-name",
            "arn:aws:s3:::input-bucket-name/*"
        ]
    }
}
```

### Output bucket policy<a name="job-queuing-output-bucket"></a>

The following IAM policy gives the data access role permission to write files to your output bucket\.

```
{
    "Version": "2012-10-17",
    "Statement": {
        "Effect": "Allow",
        "Action": [
            "s3:PutObject"
        ],
        "Resource": [
            "arn:aws:s3:::output-bucket-name/*"
        ]
    }
}
```

### AWS KMS key policy for input buckets<a name="job-queuing-input-kms"></a>

If you have encrypted your input files, the data access role needs permission to use the AWS KMS key to decrypt the files\. The following policy provides that permission\.

```
{
    "Version": "2012-10-17",
    "Statement": {
        "Effect": "Allow",
        "Action": [
            "kms:Decrypt"
        ],
        "Resource": [
            "arn:aws:kms:us-west-2:111122223333:key/input-bucket-key-id" 
        ]
    }
}
```

### AWS KMS key policy for output buckets<a name="job-queuing-output-kms"></a>

To encrypt your output transcriptions, the data access role needs permission to use the AWS KMS key\. The following policy provides that permission\.

```
{
    "Version": "2012-10-17",
    "Statement": {
        "Effect": "Allow",
        "Action": [
            "kms:GenerateDataKey*"
        ],
        "Resource": [
            "arn:aws:kms:us-west-2:111122223333:key/output-bucket-key-id" 
        ]
    }
}
```