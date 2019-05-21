# Amazon Transcribe Developer Guide

-----
*****Copyright &copy; 2019 Amazon Web Services, Inc. and/or its affiliates. All rights reserved.*****

-----
Amazon's trademarks and trade dress may not be used in 
     connection with any product or service that is not Amazon's, 
     in any manner that is likely to cause confusion among customers, 
     or in any manner that disparages or discredits Amazon. All other 
     trademarks not owned by Amazon are the property of their respective
     owners, who may or may not be affiliated with, connected to, or 
     sponsored by Amazon.

-----
## Contents
+ [What Is Amazon Transcribe?](what-is-transcribe.md)
+ [How Amazon Transcribe Works](how-it-works.md)
   + [Speech Input](input.md)
   + [Identifying Speakers](how-diarization.md)
   + [Transcribing Streaming Audio](how-streaming-transcription.md)
   + [Channel Identification](how-channel-id.md)
   + [Custom Vocabularies](how-vocabulary.md)
+ [Getting Started with Amazon Transcribe](getting-started.md)
   + [Step 1: Set up an AWS Account and Create an Administrator User](setting-up-asc.md)
   + [Step 2: Set up the AWS Command Line Interface (AWS CLI)](setup-asc-awscli.md)
   + [Step 3: Getting Started Using the Console](getting-started-asc-console.md)
   + [Step 4: Getting Started Using the API](getting-started-asc-api.md)
      + [Getting Started (AWS Command Line Interface)](getting-started-cli.md)
      + [Getting Started (AWS SDK for Python (Boto))](getting-started-python.md)
   + [Step 5: Getting Started With Streaming Audio](getting-started-streaming.md)
+ [Streaming Transcription](streaming.md)
   + [Using Amazon Transcribe Streaming](how-streaming.md)
   + [Streaming Retry Client](streaming-client.md)
   + [Using the Retry Client](retry-client-example.md)
   + [Amazon Transcribe Streaming Format](streaming-format.md)
+ [Monitoring Amazon Transcribe](monitoring-transcribe.md)
   + [Monitoring Amazon Transcribe API Calls with AWS CloudTrail](monitoring-transcribe-cloud-trail.md)
   + [Using Amazon CloudWatch Events with Amazon Transcribe](cloud-watch-events.md)
+ [Authentication and Access Control for Amazon Transcribe](auth-and-access-control.md)
   + [Overview of Managing Access Permissions to Amazon Transcribe Resources](access-control-overview.md)
   + [Using Identity-based Policies (IAM Policies) for Amazon Transcribe](access-control-managing-permissions.md)
   + [Amazon Transcribe API Permissions: Actions, Resources, and Conditions Reference](asc-api-permissions-ref.md)
+ [Guidelines and Limits](limits-guidelines.md)
+ [Document History for Amazon Transcribe](doc-history.md)
+ [API Reference](API_Reference.md)
   + [Actions](API_Operations.md)
      + [Amazon Transcribe Service](API_Operations_Amazon_Transcribe_Service.md)
         + [CreateVocabulary](API_CreateVocabulary.md)
         + [DeleteTranscriptionJob](API_DeleteTranscriptionJob.md)
         + [DeleteVocabulary](API_DeleteVocabulary.md)
         + [GetTranscriptionJob](API_GetTranscriptionJob.md)
         + [GetVocabulary](API_GetVocabulary.md)
         + [ListTranscriptionJobs](API_ListTranscriptionJobs.md)
         + [ListVocabularies](API_ListVocabularies.md)
         + [StartTranscriptionJob](API_StartTranscriptionJob.md)
         + [UpdateVocabulary](API_UpdateVocabulary.md)
      + [Amazon Transcribe Streaming Service](API_Operations_Amazon_Transcribe_Streaming_Service.md)
         + [StartStreamTranscription](API_streaming_StartStreamTranscription.md)
   + [Data Types](API_Types.md)
      + [Amazon Transcribe Service](API_Types_Amazon_Transcribe_Service.md)
         + [Media](API_Media.md)
         + [Settings](API_Settings.md)
         + [Transcript](API_Transcript.md)
         + [TranscriptionJob](API_TranscriptionJob.md)
         + [TranscriptionJobSummary](API_TranscriptionJobSummary.md)
         + [VocabularyInfo](API_VocabularyInfo.md)
      + [Amazon Transcribe Streaming Service](API_Types_Amazon_Transcribe_Streaming_Service.md)
         + [Alternative](API_streaming_Alternative.md)
         + [AudioEvent](API_streaming_AudioEvent.md)
         + [AudioStream](API_streaming_AudioStream.md)
         + [Item](API_streaming_Item.md)
         + [Result](API_streaming_Result.md)
         + [Transcript](API_streaming_Transcript.md)
         + [TranscriptEvent](API_streaming_TranscriptEvent.md)
         + [TranscriptResultStream](API_streaming_TranscriptResultStream.md)
   + [Common Errors](CommonErrors.md)
   + [Common Parameters](CommonParameters.md)
+ [AWS Glossary](glossary.md)