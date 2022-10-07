# Enabling speaker partitioning<a name="conversation-diarization-med"></a>

To enable speaker partitioning in Amazon Transcribe Medical, use *speaker diarization*\. This enables you to see what the patient said and what the clinician said in the transcription output\.

When you enable speaker diarization, Amazon Transcribe Medical labels each speaker *utterance* with a unique identifier for each speaker\. An *utterance* is a unit of speech that is typically separated from other utterances by silence\. In batch transcription, an utterance from the clinician could receive a label of `spk_0` and an utterance the patient could receive a label of `spk_1`\.

If an utterance from one speaker overlaps with an utterance from another speaker, Amazon Transcribe Medical orders them in the transcription by their start times\. Utterances that overlap in the input audio don't overlap in the transcription output\.

You can enable speaker diariziation when you transcribe an audio file using batch transcription job, or in a real\-time stream\.

**Topics**
+ [Enabling speaker partitioning in batch transcriptions](conversation-diarization-batch-med.md)
+ [Enabling speaker partitioning in real\-time streams](conversation-diarization-streaming-med.md)