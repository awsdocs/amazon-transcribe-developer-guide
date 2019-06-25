# Getting Started \(AWS SDK for Python \(Boto\)\)<a name="getting-started-python"></a>

In this exercise you create script that uses the SDK for Python to transcribe speech into text\. To complete this exercise, you need to: 
+ Install the AWS CLI\. For more information, see [Step 2: Set up the AWS Command Line Interface \(AWS CLI\)](setup-asc-awscli.md)\. This installs the AWS SDK for Python \(Boto\)\.
+ Have a speech file in \.WAV or \.MP4 format that is stored in an S3 bucket that has the proper permissions\. For more information about the permissions needed for Amazon Transcribe, see [Permissions Required for IAM User Roles](security_iam_id-based-policy-examples.md#auth-role-iam-user)\. The location must be in the same region as the endpoint that you are calling\. This example assumes that the file is in an Amazon S3 bucket named `test-transcribe` and that the file name is `answer2.wav`\.

```
from __future__ import print_function
import time
import boto3
transcribe = boto3.client('transcribe')
job_name = "job name"
job_uri = "https://S3 endpoint/test-transcribe/answer2.wav"
transcribe.start_transcription_job(
    TranscriptionJobName=job_name,
    Media={'MediaFileUri': job_uri},
    MediaFormat='wav',
    LanguageCode='en-US'
)
while True:
    status = transcribe.get_transcription_job(TranscriptionJobName=job_name)
    if status['TranscriptionJob']['TranscriptionJobStatus'] in ['COMPLETED', 'FAILED']:
        break
    print("Not ready yet...")
    time.sleep(5)
print(status)
```

When the transcription job is complete, the result links to an Amazon S3 presigned URL that contains the transcription in JSON format:

```
   {
      "jobName":"job ID",
      "accountId":"account ID",
      "results": {
         "transcripts":[
            {
               "transcript":" that's no answer",
               "confidence":1.0
            }
         ],
         "items":[
            {
               "start_time":"0.180",
               "end_time":"0.470",
               "alternatives":[
                  {
                     "confidence":0.84,
                     "word":"that's"
                  }
               ]
            },
            {
               "start_time":"0.470",
               "end_time":"0.710",
               "alternatives":[
                  {
                     "confidence":0.99,
                     "word":"no"
                  }
               ]
            },
            {
               "start_time":"0.710",
               "end_time":"1.080",
               "alternatives":[
                  {
                     "confidence":0.87,
                     "word":"answer"
                  }
               ]
            }
         ]
      },
      "status":"COMPLETED"
   }
```