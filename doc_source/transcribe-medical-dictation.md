# Transcribing a medical dictation<a name="transcribe-medical-dictation"></a>

You can use Amazon Transcribe Medical to transcribe clinician\-dictated medical notes using either a batch transcription job or a real\-time stream\. Batch transcription jobs enable you to transcribe audio files\. You specify the medical specialty of the clinician in your transcription job or stream to ensure that Amazon Transcribe Medical produces transcription results with the highest possible accuracy\.

You can transcribe a medical dictation in the following specialties:
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

You can improve transcription accuracy by using custom vocabularies\. For information on how medical custom vocabularies work, see [Improving transcription accuracy with medical custom vocabularies](vocabulary-med.md)\.

By default, Amazon Transcribe Medical returns the transcription with the highest confidence level\. If you'd like to configure it to return alternative transcriptions, see [Generating alternative transcriptions](alternative-med-transcriptions.md)\.

For information about how numbers and medical measurements appear in the transcription output, see [Transcribing numbers](how-numbers-med.md) and [Transcribing medical terms and measurements](how-measurements-med.md)\.

**Topics**
+ [Transcribing an audio file of a medical dictation](batch-medical-dictation.md)
+ [Transcribing a medical dictation in a real\-time stream](streaming-medical-dictation.md)