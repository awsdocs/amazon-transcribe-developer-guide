# Channel Identification<a name="how-channel-id-med"></a>

When an audio file has multiple channels that you want to transcribe into separate transcriptions, use *channel identification*\. For example, if you have a drug safety monitoring agent on one channel and a patient on another, use channel identification to create a transcription that is identified by each channel and a single transcription that combines them\.

Amazon Transcribe Medical splits your audio file into multiple channels and transcribes the channels separately\. After transcribing all channels, Amazon Transcribe Medical also merges the transcriptions to create a single transcription\. It returns all of the transcriptions in a single result file\.

Channel identification uses *utterances* to distinguish the speech of different speakers when they are talking over each other\. An *utterance* is a unit of speech on an audio channel that is typically separated from other utterances by silence\. If an utterance on one channel overlaps one on another channel, Amazon Transcribe Medical orders them in the transcription by their start times\. Utterances that overlap in the input audio don't overlap in the transcription output\.

Enable channel identification in the Amazon Transcribe Medical console or with the API\. In the console, choose **Channel identification** when you create the transcription job\. When you use the API, set the `ChannelIdentification` flag when you call the [StartMedicalTranscriptionJob](API_StartMedicalTranscriptionJob.md) operation\. 

The following is the abbreviated output for a conversation on two channels\.

```
{
  "jobName": "job id",
  "accountId": "account id",
  "results": {
    "transcripts": [
      {
        "transcript": "When you try ... It seems to ..."
      }
    ],
    "channel_labels": {
      "channels": [
        {
          "channel_label": "ch_0",
          "items": [
            {
              "start_time": "12.282",
              "end_time": "12.592",
              "alternatives": [
                {
                  "confidence": "1.0000",
                  "content": "When"
                }
              ],
              "type": "pronunciation"
            },
            {
              "start_time": "12.592",
              "end_time": "12.692",
              "alternatives": [
                {
                  "confidence": "0.8787",
                  "content": "you"
                }
              ],
              "type": "pronunciation"
            },
            {
              "start_time": "12.702",
              "end_time": "13.252",
              "alternatives": [
                {
                  "confidence": "0.8318",
                  "content": "try"
                }
              ],
              "type": "pronunciation"
            },
            Transcription abbreviated
         ]
      },
      {
          "channel_label": "ch_1",
          "items": [
            {
              "start_time": "12.379",
              "end_time": "12.589",
              "alternatives": [
                {
                  "confidence": "0.5645",
                  "content": "It"
                }
              ],
              "type": "pronunciation"
            },
            {
              "start_time": "12.599",
              "end_time": "12.659",
              "alternatives": [
                {
                  "confidence": "0.2907",
                  "content": "seems"
                }
              ],
              "type": "pronunciation"
            },
            {
              "start_time": "12.669",
              "end_time": "13.029",
              "alternatives": [
                {
                  "confidence": "0.2497",
                  "content": "to"
                }
              ],
              "type": "pronunciation"
            },
            Transcription abbreviated
        ]
    }
}
```