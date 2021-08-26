# Step 4: Transcribing with a custom language model<a name="clm-transcription"></a>

You can use a custom language model in transcription jobs with the [Amazon Transcribe console](https://console.aws.amazon.com/transcribe/) or the [StartTranscriptionJob](API_StartTranscriptionJob.md) API\.

## Transcribing with a custom language model \(console\)<a name="start-console"></a>



**To start a transcription job \(console\)**

1. Sign in to the [Amazon Transcribe console](https://console.aws.amazon.com/transcribe/)\.

1. In the navigation pane, choose **Transcription jobs**\.

1. For **Name**, enter a transcription job name that is unique within your AWS account\.

1. For **Language**, choose the language of your media file\.

1. For **Custom model selection**, choose your custom language model\.

1. For **Input file location on S3**, enter the URI of the media file\. If you can't remember the URI, choose **Browse S3** and choose it\.

1. Choose **Next**\.

1. Enable any of the available features you want to use for your transcription job\.

1. Choose **Create**\.

## Transcribing with a custom language model \(API\)<a name="start-api"></a>

**To start a transcription job \(API\)**

**To transcribe an audio or video file with a custom language model \(API\)**
+ For the [StartTranscriptionJob](API_StartTranscriptionJob.md) API, specify the following\.

  1. For `TranscriptionJobName`, specify a name that is unique to your AWS account\.

  1. For `LanguageCode`, specify the language code that corresponds to the language spoken in your audio or video file\.

  1. For the `MediaFileUri` parameter of the `Media` object, specify Amazon S3 location of the file you want to transcribe\.

  1. For the `LanguageModelName` parameter of the `ModelSettings` object, specify the name of the custom language model\.

The following is an example request using the AWS SDK for Python \(Boto3\)\.

```
import time
import boto3
transcribe = boto3.client('transcribe')
job_name = 'transcription-job-name'
job_uri = 's3://path-to-your-media-file/media-file.file-extension'

transcribe.start_transcription_job(
        TranscriptionJobName = job_name,
        Media = {'MediaFileUri': job_uri},
        MediaFormat = 'media-format',
        LanguageCode = 'language-code',
    ModelSettings = {
        'LanguageModelName': 'language-model-name'
        }
    )
while True:
    status = transcribe.get_transcription_job(TranscriptionJobName=job_name)
    if status['TranscriptionJob']['TranscriptionJobStatus'] in ['COMPLETED', 'FAILED']:
        break
    print('Not ready yet...')
    time.sleep(5)
print(status)
```

## Transcribing with a custom language model \(AWS CLI\)<a name="start-custom-cli"></a>

**To transcribe with a custom language model \(AWS CLI\)**
+ Run the following code\.

  ```
  aws transcribe start-transcription-job \ 
   --transcription-job-name "example-job-name" \ 
   --language-code "language-code" \ 
   --media MediaFileUri="s3://example-bucket/example-audio.wav" \ 
   --model-settings LanguageModelName="ExampleLanguageModel"
  ```

**Next step**  
[Step 5: Viewing and updating your custom language models](view-update-lang.md)