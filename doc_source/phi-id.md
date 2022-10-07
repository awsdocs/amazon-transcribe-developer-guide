# Identifying personal health information \(PHI\) in a transcription<a name="phi-id"></a>

Use *Personal Health Information Identification* to label personal health information \(PHI\) in your transcription results\. By reviewing labels, you can find PHI that could be used to identify a patient\.

You can identify PHI using either a real\-time stream or batch transcription job\. 

You can use your own post\-processing to redact the PHI identified in the transcription output\.

Use Personal Health Information Identification to identify the following types of PHI:
+ Personal PHI:
  + Names – Full name or last name and initial
  + Gender
  + Age
  + Phone numbers
  + Dates \(not including the year\) that directly relate to the patient
  + Email addresses
+ Geographic PHI:
  + Physical address
  + Zip code
  + Name of medical center or practice
+ Account PHI:
  + Fax numbers
  + Social security numbers \(SSNs\)
  + Health insurance beneficiary numbers
  + Account numbers
  + Certificate or license numbers
+ Vehicle PHI:
  + Vehicle identification number \(VIN\)
  + License plate number
+ Other PHI:
  + Web Uniform Resource Location \(URL\)
  + Internet Protocol \(IP\) address numbers

Amazon Transcribe Medical is a Health Insurance Portability and Accountability Act of 1996 \(HIPAA\) eligible service\. For more information, see [Amazon Transcribe Medical](transcribe-medical.md)\. For information about identifying PHI in an audio file, see [Identifying PHI in an audio file](phi-id-batch.md)\. For information about identifying PHI in a stream, see [Identifying PHI in a real\-time stream](phi-id-stream.md)\.

**Topics**
+ [Identifying PHI in an audio file](phi-id-batch.md)
+ [Identifying PHI in a real\-time stream](phi-id-stream.md)