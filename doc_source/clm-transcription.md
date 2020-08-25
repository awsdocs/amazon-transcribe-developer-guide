# Step 4: Transcribing with a Custom Language Model<a name="clm-transcription"></a>

You can use a custom language model in transcription jobs with the Amazon Transcribe console, the [StartTranscriptionJob](API_StartTranscriptionJob.md) operation, or the AWS CLI\.

## Transcribing with a Custom Language Model \(Console\)<a name="start-console"></a>

**To start a transcription job \(console\)**

1. Sign in to AWS Management Console and open the Amazon Transcribe console at [Amazon Transcribe console](https://console.aws.amazon.com/transcribe/)\.

1. In the navigation pane, choose **Transcription jobs**\.

1. For **Name**, enter a transcription job name that is unique within your AWS account\.

1. For **Model selection**, choose your custom language model\.

1. For **Input file location on S3**, enter the URI of the media file\. If you can't remember the URI, choose **Browse S3** and choose it\.

1. Choose **Next**\.

1. Enable any of the available features for your transcription job that you want to use\.

1. Choose **Create**\.

## Transcribing with a Custom Language Model \(API\)<a name="start-api"></a>

**To start a transcription job \(API\)**

1. Specify values for the required parameters:
   + `TranscriptionJobName` \- The name of the transcription job\.
   + `LanguageCode` \- The language code of the transcription job\. US English \(en\-US\) is the only valid language code\.
   + `MediaFileUri` parameter of the `Media` object \- The Amazon S3 location of the media file that you want to transcribe\.
   + `LanguageModelName` parameter of the `ModelSettings` object \- The name of the custom language model\.

1. Specify values for optional parameters\. The following code shows both required and optional parameters:

   ```
       {
       "JobExecutionSettings": {
       "AllowDeferredExecution": boolean,
       "DataAccessRoleArn": "string"
       },
       "LanguageCode": "string",
       "Media": {
       "MediaFileUri": "string"
       },
       "MediaFormat": "string",
       "MediaSampleRateHertz": number,
       "ModelSettings": {
       "LanguageModelName": "string"
       },
       "OutputBucketName": "string",
       "OutputEncryptionKMSKeyId": "string",
       "Settings": {
       "ChannelIdentification": boolean,
       "MaxAlternatives": number,
       "MaxSpeakerLabels": number,
       "ProfanityCollectionName": "string",
       "ProfanityFilterMethod": "string",
       "ShowAlternatives": boolean,
       "ShowSpeakerLabels": boolean,
       "VocabularyName": "string"
       },
       "TranscriptionJobName": "string"
       }
   ```

## Transcribing with a Custom Language Model \(AWS CLI\)<a name="start-custom-cli"></a>

**To transcribe with a custom language model \(AWS CLI\)**
+ Run the following code\.

  ```
  aws transcribe start-transcription-job \ 
   --transcription-job-name "example-job-name" \ 
   --language-code "en-US" \ 
   --media MediaFileUri="s3://example-bucket/example-audio.wav" \ 
   --model-settings LanguageModelName="ExampleLanguageModel"
  ```

**Next step**  
[Step 5: Viewing and Updating Your Custom Language Models](view-update-lang.md)