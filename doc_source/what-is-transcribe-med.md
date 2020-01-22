# What Is Amazon Transcribe Medical?<a name="what-is-transcribe-med"></a>

Amazon Transcribe Medical is an automatic speech recognition \(ASR\) service that you can use to add medical speech\-to\-text capabilities to an application\. Amazon Transcribe Medical is available as a real\-time application programming interface \(API\) that you call to connect using the WebSocket protocol, which helps secure the bi\-directional connection\. When you pass an audio stream to Amazon Transcribe Medical, the service returns a stream of JSON objects containing the results of the transcription\. 

You can use Amazon Transcribe Medical to transcribe medical\-related speech found in a variety of use cases\. For example, physician\-dictated notes, drug safety monitoring, telemedicine, or even physician\-patient conversations\.

You can use [Amazon Comprehend Medical](https://docs.aws.amazon.com/comprehend/latest/dg/comprehend-medical.html) for further analysis of your transcript\.

## Important Notice<a name="important-notice-med"></a>

 Amazon Transcribe Medical is not a substitute for professional medical advice, diagnosis, or treatment\. Identify the right confidence threshold for your use case, and use high confidence thresholds in situations that require high accuracy\. For certain use cases, results should be reviewed and verified by appropriately trained human reviewers\. All operations of Amazon Transcribe Medical should only be used in patient care scenarios after review for accuracy and sound medical judgement by trained medical professionals\. 

## Transcribing Streaming Audio<a name="what-streaming-transcription-med"></a>

You can use Amazon Transcribe Medical to transcribe medical speech in real time\. When you send Amazon Transcribe Medical a stream of audio, it returns a stream of JSON objects containing the transcription of the audio\.

For more information about processing audio streams, see [Establish a Bi\-Directional Connection Using the WebSocket Protocol](websocket-med.md)\.

## Supported Specialties<a name="Medical-Specific-Vocabulary"></a>

 Amazon Transcribe Medical currently supports transcription for primary care\. The following specialties are included:
+ Family Medicine
+ Internal Medicine
+ Obstetrics and Gynecology \(OB\-GYN\)
+ Pediatrics

## Are You a First\-time User of Amazon Transcribe Medical?<a name="first-time-user-med"></a>

If you are a first\-time user, we recommend that you read the following topic to get an introduction to Amazon Transcribe Medical: [How Amazon Transcribe Medical Works](how-it-works-med.md)\.