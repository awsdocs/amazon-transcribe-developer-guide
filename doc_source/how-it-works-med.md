# Medical specialties and terms<a name="how-it-works-med"></a>

When creating a medical transcription job, you specify the language, the medical specialty, and the audio type of the source file\. You input US English \(en\-US\) as the language and `PRIMARYCARE` as the medical specialty\. Entering primary care as the value enables you to generate transcriptions from source audio in the following medical specialties:
+ Family Medicine
+ Internal Medicine
+ Obstetrics and Gynecology \(OB\-GYN\)
+ Pediatrics

You have the choice between dictation and conversation for your audio type\. Choose dictation for audio files where the physician is giving a report about a patient visit or procedure\. Choose conversation for audio files that involve a conversation between a physician and a patient or a conversation between physicians\.

To store the output of your transcription job, select an Amazon S3 bucket that you've already created\. For more information on Amazon S3 buckets see [Getting Started with Amazon Simple Storage Service](https://docs.aws.amazon.com/AmazonS3/latest/gsg/GetStartedWithS3.html)\.

The following are the minimum number of request parameters to enter in the sample JSON\.

```
{
   "MedicalTranscriptionJobName": "my-first-transcription-job",
   "LanguageCode": "en-US",
   "Media": {
       "MediaFileUri": "s3://path to your audio file"
   },
   "OutputBucketName": “your output bucket name",
   "Specialty": "PRIMARYCARE",
   "Type": "CONVERSATION"
}
```

Amazon Transcribe Medical enables you to generate alternative transcriptions\. For more information, see [Generating alternative transcriptions](alternative-med-transcriptions.md)\.

You can also enable speaker partitioning or identify channels in your audio\. For more information, see [Enabling speaker partitioning](conversation-diarization-med.md) and [Transcribing multi\-channel audio](conversation-channel-id-med.md)\.