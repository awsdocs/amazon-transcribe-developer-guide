# What is Amazon Transcribe Medical?<a name="what-is-transcribe-med"></a>

Amazon Transcribe Medical is an automatic speech recognition \(ASR\) service that enables you to add medical speech\-to\-text capabilities to an application\. Amazon Transcribe Medical is a Health Insurance Portability and Accountability Act of 1996 \(HIPAA\) compliant service and is available through either real\-time streaming or asynchronous API calls\. To help with security and compliance, Amazon Transcribe Medical operates with a shared responsibility model\. AWS is responsible for protecting the infrastructure that runs Amazon Transcribe Medical and you are responsible for the management of your data\. For more information, see [https://aws.amazon.com/compliance/shared-responsibility-model/](https://aws.amazon.com/compliance/shared-responsibility-model/)

Use Amazon Transcribe Medical to transcribe medical\-related speech found in a variety of use cases\. Example uses include physician\-dictated notes, drug safety monitoring, telemedicine, or physician\-to\-patient conversations\.

Amazon Transcribe Medical is available in US English \(en\-US\)\.

Use [Amazon Comprehend Medical](https://docs.aws.amazon.com/comprehend/latest/dg/comprehend-medical.html) for further analysis of your transcript\.



## Important notice<a name="important-notice-med"></a>

 Amazon Transcribe Medical is not a substitute for professional medical advice, diagnosis, or treatment\. Identify the right confidence threshold for your use case, and use high confidence thresholds in situations that require high accuracy\. For certain use cases, results should be reviewed and verified by appropriately trained human reviewers\. All operations of Amazon Transcribe Medical should only be used in patient care scenarios after review for accuracy and sound medical judgment by trained medical professionals\. 

## Streaming audio transcription<a name="what-streaming-transcription-med"></a>

Amazon Transcribe Medical enables you to transcribe medical speech in real time\. To do this, use a WebSocket protocol to establish a bi\-directional connection to the Amazon Transcribe Medical real\-time application programming interface\. When you send Amazon Transcribe Medical a stream of audio, it returns a stream of JSON objects containing the audio's transcription\.

For more information about processing audio streams, see [Establish a bi\-directional connection using the WebSocket protocol](websocket-med.md)\.

## API batch transcription<a name="what-batch-api"></a>

Amazon Transcribe Medical supports the transcription of individual audio files through asynchronous API batch calls\. For more information about transcribing audio files, see [How Amazon Transcribe Medical works](how-it-works-med.md)

Batch transcription can improve your transcription results\. You can also use channel identification to separate and transcribe channels in audio files that have multiple channels\. Channel identification generates separate transcripts for each channel and merges them into a single output\. To identify speakers in single\-channel audio files, use speaker identification\. To generate additional alternative transcription results for the same source audio, use alternative transcriptions\.

## Supported specialties<a name="Medical-Specific-Vocabulary"></a>

You can transcribe medical speech in the following specialties:
+ Cardiology – available in streaming transcription only
+ Neurology – available in streaming transcription only
+ Oncology – available in streaming transcription only
+ Primary Care – includes the following types of medical practice:
  + Family medicine
  + Internal medicine
  + Obstetrics and Gynecology \(OB\-GYN\)
  + Pediatrics
+ Radiology – available in streaming transcription only
+ Urology – available in streaming transcription only

## Are you a first\-time user of Amazon Transcribe Medical?<a name="first-time-user-med"></a>

If you are a first\-time user, we recommend that you read the following topic to get an introduction to Amazon Transcribe Medical: [How Amazon Transcribe Medical works](how-it-works-med.md)\.