# AWS Command Line Interface<a name="getting-started-cli"></a>

In the following exercise, you use the AWS Command Line Interface \(AWS CLI\) to transcribe speech into text\. To complete this exercise, you need to: 
+ Have a text editor\.
+ Be familiar with the AWS CLI\. For more information, see [Step 2: Set up the AWS Command Line Interface \(AWS CLI\)](setup-awscli.md)\.
+ Have a speech file in WAV or MP4 format that is stored in an S3 bucket that has the proper permissions\. For more information about the permissions needed for Amazon Transcribe, see [Permissions required for IAM user roles](security_iam_id-based-policy-examples.md#auth-role-iam-user)\.

To transcribe text, you have to provide the input parameters in a JSON file\.

**To transcribe text**

1. Copy your input speech to an S3 bucket\. The location must be in the same Region as the endpoint that you are calling\.

1. Create a JSON file named `example-start-command.json` that contains the input parameters for the [ StartTranscriptionJob ](API_StartTranscriptionJob.md) API\. Enter a unique name for your transcription job under "TranscriptionJobName"\.

   ```
   {
       "TranscriptionJobName": "job-name", 
       "LanguageCode": "en-US", 
       "MediaFormat": "wav", 
       "Media": {
           "MediaFileUri": "s3://DOC-EXAMPLE-BUCKET/your-audio-file"
       }
   }
   ```

1. In the AWS CLI, run the following command\. The example is formatted for Unix, Linux, and macOS\. For Windows, replace the backslash \(\\\) Unix continuation character at the end of each line with a caret \(^\)\.

   ```
   aws transcribe start-transcription-job \
        --region region \
        --cli-input-json file://filepath/example-start-command.json
   ```

   Amazon Transcribe responds with the following:

   ```
   {
       "TranscriptionJob": {
           "TranscriptionJobName": "job-name",
           "LanguageCode": "en-US",
           "TranscriptionJobStatus": "IN_PROGRESS",
           "Media": {
               "MediaFileUri": "s3://DOC-EXAMPLE-BUCKET/your-audio-file"
           },
           "CreationTime": timestamp,
           "MediaFormat": "wav"
       }
   }
   ```

**To list transcription jobs**
+ Run the following command:

  ```
  aws transcribe list-transcription-jobs \
       --region region \
       --status IN_PROGRESS
  ```

  Amazon Transcribe responds with the following:

  ```
  {
      "Status": "IN_PROGRESS",
      "TranscriptionJobSummaries": [
          {
              "TranscriptionJobName": "job-name",
              "LanguageCode": "en-US",
              "CreationTime": timestamp,
              "TranscriptionJobStatus": "IN_PROGRESS"
          }
      ]
  }
  ```

**To get the results of a transcription job**

1. When the job has the status `COMPLETED`, get the results of the job\. Type the following command:

   ```
   aws transcribe get-transcription-job \
      --region region \
      --transcription-job-name "job-name"
   ```

   Amazon Transcribe responds with the following:

   ```
   {
       "TranscriptionJob": {
           "TranscriptionJobName": "job-name",
           "LanguageCode": "en-US",
           "TranscriptionJobStatus": "COMPLETED",
           "Media": {
               "MediaFileUri": "input URI"
           },
           "CreationTime": timestamp,
           "CompletionTime": timestamp,
           "Transcript": {
               "TranscriptFileUri": "output URI"
           }
       }
   }
   ```

1. Use the output URI to get the transcribed text from the audio file\. The following is the output from transcribing a short audio clip:

   ```
       {
         "jobName":"job ID",
         "accountId":"account ID",
         "results": {
            "transcripts":[
               {
                  "transcript":" that's no answer"  
               }
            ],
            "items":[
               {
                  "start_time":"0.180",
                  "end_time":"0.470",
                  "alternatives":[
                     {
                        "confidence":0.84,
                        "content":"that's"
                     }
                  ],
                  "type": "pronunciation"
               },
               {
                  "start_time":"0.470",
                  "end_time":"0.710",
                  "alternatives":[
                     {
                        "confidence":0.99,
                        "content":"no"
                     }
                  ],
                  "type": "pronunciation"
               },
               {
                  "start_time":"0.710",
                  "end_time":"1.080",
                  "alternatives":[
                     {
                        "confidence":0.874,
                        "content":"answer"
                     }
                  ],
                  "type": "pronunciation"
               }
            ]
         },
         "status":"COMPLETED"
      }
   ```