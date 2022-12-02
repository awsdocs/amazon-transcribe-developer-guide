# Transcribe audio and get job data with Amazon Transcribe using an AWS SDK<a name="example_transcribe_Scenario_GettingStartedTranscriptionJobs_section"></a>

The following code example shows how to:
+ Start a transcription job with Amazon Transcribe\.
+ Wait for the job to complete\.
+ Get the URI where the transcript is stored\.

**Note**  
The source code for these examples is in the [AWS Code Examples GitHub repository](https://github.com/awsdocs/aws-doc-sdk-examples)\. Have feedback on a code example? [Create an Issue](https://github.com/awsdocs/aws-doc-sdk-examples/issues/new/choose) in the code examples repo\. 

For more information, see [Getting started with Amazon Transcribe](https://docs.aws.amazon.com/transcribe/latest/dg/getting-started.html)\.

------
#### [ Python ]

**SDK for Python \(Boto3\)**  
 There's more on GitHub\. Find the complete example and learn how to set up and run in the [AWS Code Examples Repository](https://github.com/awsdocs/aws-doc-sdk-examples/tree/main/python/example_code/transcribe#code-examples)\. 
  

```
import time
import boto3


def transcribe_file(job_name, file_uri, transcribe_client):
    transcribe_client.start_transcription_job(
        TranscriptionJobName=job_name,
        Media={'MediaFileUri': file_uri},
        MediaFormat='wav',
        LanguageCode='en-US'
    )

    max_tries = 60
    while max_tries > 0:
        max_tries -= 1
        job = transcribe_client.get_transcription_job(TranscriptionJobName=job_name)
        job_status = job['TranscriptionJob']['TranscriptionJobStatus']
        if job_status in ['COMPLETED', 'FAILED']:
            print(f"Job {job_name} is {job_status}.")
            if job_status == 'COMPLETED':
                print(
                    f"Download the transcript from\n"
                    f"\t{job['TranscriptionJob']['Transcript']['TranscriptFileUri']}.")
            break
        else:
            print(f"Waiting for {job_name}. Current status is {job_status}.")
        time.sleep(10)


def main():
    transcribe_client = boto3.client('transcribe')
    file_uri = 's3://test-transcribe/answer2.wav'
    transcribe_file('Example-job', file_uri, transcribe_client)


if __name__ == '__main__':
    main()
```
+ For API details, see the following topics in *AWS SDK for Python \(Boto3\) API Reference*\.
  + [GetTranscriptionJob](https://docs.aws.amazon.com/goto/boto3/transcribe-2017-10-26/GetTranscriptionJob)
  + [StartTranscriptionJob](https://docs.aws.amazon.com/goto/boto3/transcribe-2017-10-26/StartTranscriptionJob)

------

For a complete list of AWS SDK developer guides and code examples, see [Using this service with an AWS SDK](getting-started-sdk.md#sdk-general-information-section)\. This topic also includes information about getting started and details about previous SDK versions\.