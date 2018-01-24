# How Amazon Transcribe Works<a name="how-it-works"></a>


|  | 
| --- |
| This is prerelease documentation for a service in preview release\. It is subject to change\. | 

Amazon Transcribe analyzes audio files containing speech and then uses advanced machine learning techniques to transcribe the voice data into text\. You can then use the transcription as you would any text document\.

Amazon Transcribe has three operations:

+ [StartTranscriptionJob](API_StartTranscriptionJob.md) – Starts an asynchronous job to transcribe the speech in an audio file to text\.

+ [ListTranscriptionJobs](API_ListTranscriptionJobs.md) – Returns a list of speech recognition jobs that have been started\. You can specify the status of the jobs that you want the operation to return\. For example, you can get a list of all pending jobs, or a list of completed jobs\.

+ [GetTranscriptionJob](API_GetTranscriptionJob.md) – Returns the result of a speech recognition job\. The response contains a link to a JSON file containing the results\.

## Speech Input<a name="input"></a>

Input to an Amazon Transcribe transcription job comes from an object stored in an Amazon S3 bucket\. The input file must be: 

+ In FLAC, MP3, MP4, or WAV file format

+ Less than 2 hours in length

You must specify the language and format of the input file\. 

For best results, 

+ Use a lossless format, such as FLAC or WAV with PCM 16\-bit encoding\.

+ The sample rate should be 8000 Hz for low\-fidelity audio and 16000 Hz for high\-fidelity audio\.

You must give Amazon Transcribe permission to access the Amazon S3 bucket that contains your input file\. For more information about the required permissions, see [Permissions Required for Audio Transcription](access-control-managing-permissions.md#auth-role-permissions)\.

## Output JSON<a name="output"></a>

When Amazon Transcribe completes a transcription job, it creates a JSON file containing the results and puts the file in an S3 bucket\. The file is identified by a user\-specific URI\. You use the URI to get the results\.

The following is the JSON file for a short audio file:

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