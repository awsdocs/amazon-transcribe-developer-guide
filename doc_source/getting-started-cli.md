# Getting Started \(AWS Command Line Interface\)<a name="getting-started-cli"></a>

In the following exercise, you use the AWS Command Line Interface \(AWS CLI\) to transcribe speech into text\. To complete this exercise, you need to: 

+ Have a text editor\.

+ Be familiar with the AWS CLI\. For more information, see [Step 2: Set up the AWS Command Line Interface \(AWS CLI\)](setup-asc-awscli.md)\.

+ Have a speech file in \.WAV or \.MP4 format that is stored in an S3 bucket that has the proper permissions\. For more information about required permissions, see [Permissions Required for Audio Transcription](access-control-managing-permissions.md#auth-role-permissions)\.

To transcribe text, you have to provide the input parameters in a JSON file\. 

**To transcribe text**

1. Copy your input speech to an S3 bucket\. The location must be in the same region as the endpoint that you are calling\. This example assumes that the file is in an S3 bucket named `test-transcribe` and that the file name is `answer2.wav`\.

1. Create a JSON file named `test-start-command.json` that contains the input parameters for the [StartTranscriptionJob](API_StartTranscriptionJob.md) operation\.

   ```
   {
       "TranscriptionJobName": "request ID", 
       "LanguageCode": "en-US", 
       "MediaFormat": "wav", 
       "Media": {
           "MediaFileUri": "https://S3 endpoint/test-transcribe/answer2.wav"
       }
   }
   ```

1. In the AWS CLI, run the following command\. The example is formatted for Unix, Linux, and macOS\. For Windows, replace the backslash \(\\\) Unix continuation character at the end of each line with a caret \(^\)\.

   ```
   aws transcribe start-transcription-job \
        --endpoint-url endpoint \
        --region region \
        --cli-input-json file://test-start-command.json
   ```

   Amazon Transcribe responds with the following:

   ```
   {
       "TranscriptionJob": {
           "TranscriptionJobName": "request ID",
           "LanguageCode": "en-US",
           "TranscriptionJobStatus": "IN_PROGRESS",
           "Media": {
               "MediaFileUri": "https://S3 endpoint/test-transcribe/answer2.wav"
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
       --endpoint-url endpoint \
       --region region \
       --status IN_PROGRESS
  ```

  Amazon Transcribe responds with the following:

  ```
  {
      "Status": "IN_PROGRESS",
      "TranscriptionJobSummaries": [
          {
              "TranscriptionJobName": "request ID",
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
   aws transcribe get-transcription-job-results \
      --endpoint-url endpoint \
      --region endpoint \
      --request-id "DocTest-01"
   ```

   Amazon Transcribe responds with the following:

   ```
   {
       "TranscriptionJob": {
           "TranscriptionJobName": "request ID",
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