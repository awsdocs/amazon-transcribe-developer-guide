# Amazon Transcribe Medical<a name="transcribe-medical"></a>

Amazon Transcribe Medical is an automatic speech recognition \(ASR\) service designed for medical professionals who wish to transcribe medical\-related speech, such as physician\-dictated notes, drug safety monitoring, telemedicine appointments, or physician\-patient conversations\. Amazon Transcribe Medical is available through either real\-time streaming \(via microphone\) or transcription of an uploaded file \(batch\)\.

**Important**  
Amazon Transcribe Medical is not a substitute for professional medical advice, diagnosis, or treatment\. Identify the right confidence threshold for your use case, and use high confidence thresholds in situations that require high accuracy\. For certain use cases, results should be reviewed and verified by appropriately trained human reviewers\. Amazon Transcribe Medical transcriptions should only be used in patient care scenarios after review for accuracy and sound medical judgment by trained medical professionals\.

Amazon Transcribe Medical operates under a shared responsibility model, whereby AWS is responsible for protecting the infrastructure that runs Amazon Transcribe Medical and you are responsible for managing your data\. For more information, see [Shared Responsibility Model](http://aws.amazon.com/compliance/shared-responsibility-model/)\.

Amazon Transcribe Medical is available in US English \(en\-US\)\.

For analysis of your transcripts, you can use other AWS services, such as [Amazon Comprehend Medical](https://docs.aws.amazon.com/comprehend/latest/dg/comprehend-medical.html)\.


**Supported specialties**  

| Specialty | Sub\-specialty | Audio input | 
| --- | --- | --- | 
| Cardiology | none | streaming only | 
| Neurology | none | streaming only | 
| Oncology | none | streaming only | 
| Primary Care | Family Medicine | batch, streaming | 
| Primary Care | Internal Medicine | batch, streaming | 
| Primary Care | Obstetrics and Gynecology \(OB\-GYN\) | batch, streaming | 
| Primary Care | Pediatrics | batch, streaming | 
| Radiology | none | streaming only | 
| Urology | none | streaming only | 