# Redacting or identifying PII in a real\-time stream<a name="pii-redaction-stream"></a>

When redacting personally identifiable information \(PII\) from a streaming transcription, Amazon Transcribe replaces each identified instance of PII with `[PII]` in your transcript\.

An additional option available for streaming transcriptions is *PII identification*\. When you activate PII Identification, Amazon Transcribe labels the PII in your transcription results under an `Entities` object\. For an output sample, see [Example redacted streaming output](pii-redaction-output.md#pii-redaction-output-stream) and [Example PII identification output](pii-redaction-output.md#pii-redaction-output-id)\.

PII identification and redaction for streaming jobs is performed only upon complete transcription of the audio segments\.


**Types of PII Amazon Transcribe can recognize for streaming transcriptions**  

| PII type | Description | 
| --- | --- | 
| ADDRESS | A physical address, such as *100 Main Street, Anytown, USA* or *Suite \#12, Building 123*\. An address can include a street, building, location, city, state, country, county, zip, precinct, neighborhood, and more\.  | 
| AGE | An individual's age, including the quantity and unit of time\. For example, in the phrase *I am 40 years old*, Amazon Transcribe recognizes '40 years' as an age\. | 
| ALL | Redact or identify all PII types listed in this table\. | 
| AWS\_ACCESS\_KEY | A unique identifier that's associated with an AWS secret access key\. Your access key ID and secret access key allow you to sign programmatic AWS requests cryptographically\. | 
| AWS\_SECRET\_KEY | A unique identifier that's associated with an AWS access key\. Your secret access key and access key ID allow you to sign programmatic AWS requests cryptographically\. | 
| BANK\_ACCOUNT\_NUMBER | A US bank account number\. These are typically between 10 \- 12 digits long, but Amazon Transcribe also recognizes bank account numbers when only the last 4 digits are present\. | 
| BANK\_ROUTING | A US bank account routing number\. These are typically 9 digits long, but Amazon Transcribe also recognizes routing numbers when only the last 4 digits are present\. | 
| CREDIT\_DEBIT\_CVV | A 3\-digit card verification code \(CVV\) that is present on VISA, MasterCard, and Discover credit and debit cards\. In American Express credit or debit cards, it is a 4\-digit numeric code\. | 
| CREDIT\_DEBIT\_EXPIRY | The expiration date for a credit or debit card\. This number is usually 4 digits long and formatted as month/year or MM/YY\. For example, Amazon Transcribe can recognize expiration dates such as *01/21*, *01/2021*, and *Jan 2021*\. | 
| CREDIT\_DEBIT\_NUMBER | The number for a credit or debit card\. These numbers can vary from 13 to 16 digits in length, but Amazon Transcribe also recognizes credit or debit card numbers when only the last 4 digits are present\. | 
| DATE\_TIME | A date, which may include the year, month, day, day of week, or time of day\. For example, Amazon Transcribe recognizes *January 19 2020*, *11 am*, and *Thursday morning* as dates\. Amazon Transcribe also recognizes partial dates, date ranges, date intervals and decades, such as *the 1990s*\. | 
| DRIVER\_ID | A driver's license number\. Driver's license numbers consists of alphanumeric characters\. | 
| EMAIL | An email address, such as *efua\.owusu@email\.com*\. | 
| IP\_ADDRESS | An IPv4 address, such as *198\.51\.100\.0*\. | 
| MAC\_ADDRESS | A media access control \(MAC\) address is a unique identifier assigned to a network interface controller \(NIC\)\. | 
| NAME | An individual's name\. This entity type does not include titles, such as Mr\., Mrs\., Miss, or Dr\. Amazon Transcribe does not apply this entity type to names that are part of organizations or addresses\. For example, Amazon Transcribe recognizes the *John Doe Organization* as an organization, and *Jane Doe Street* as an address\. | 
| PASSPORT\_NUMBER | A US passport number\. Passport numbers range from six to nine alphanumeric characters\. | 
| PASSWORD | An alphanumeric string that is used as a password, such as *Myd0GsB\!RthD@y7*\. | 
| PHONE | A phone number\. This entity type also includes fax and pager numbers\. | 
| PIN | A 4\-digit personal identification number \(PIN\) that allows someone to access their bank account information\. | 
| SSN | A Social Security Number \(SSN\) is a 9\-digit number that is issued to US citizens, permanent residents, and temporary working residents\. Amazon Transcribe also recognizes Social Security Numbers when only the last 4 digits are present\. | 
| URL | A web address, such as *www\.example\.com*\. | 
| USERNAME | A name or pseudonym that identifies a user's account, such as a login name, screen name, nickname, or handle\. | 

You can start a streaming transcription using the AWS Management Console, WebSocket, or HTTP/2\.

## AWS Management Console<a name="redaction-console-stream"></a>

1. Sign into the [AWS Management Console](https://console.aws.amazon.com/transcribe/)\.

1. In the navigation pane, choose **Real\-time transcription**\. Scroll down to **Content removal settings** and expand this field if it is minimized\.  
![\[Amazon Transcribe console screenshot: the 'real-time transcription' page.\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/redaction-stream1.png)

1. Toggle on **PII Identification & redaction**\.  
![\[Amazon Transcribe console screenshot: the expanded 'content removal settings' panel.\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/redaction-stream2.png)

1. Select either **Identification only** or **Identification & redaction**, then select the PII entity types you want to identify or redact in your transcript\.  
![\[Amazon Transcribe console screenshot: list of PII types that can be selected.\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/redaction-stream3.png)

1. You're now ready to transcribe your stream\. Select **Start streaming** and begin speaking\. To end your dictation, select **Stop streaming**\.

## WebSocket stream<a name="redaction-websocket"></a>

This example creates a pre\-signed URL that uses either PII Identification or PII redaction in a WebSocket stream\. Line breaks have been added for readability\. For more information on using WebSocket streams with Amazon Transcribe, see [Setting up a WebSocket stream](streaming-websocket.md)\. For more detail on parameters, see [StartStreamTranscription](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_streaming_StartStreamTranscription.html)\.

```
GET wss://transcribestreaming.us-west-2.amazonaws.com:8443/stream-transcription-websocket?
&X-Amz-Algorithm=AWS4-HMAC-SHA256
&X-Amz-Credential=AKIAIOSFODNN7EXAMPLE%2F20220208%2Fus-west-2%2Ftranscribe%2Faws4_request
&X-Amz-Date=20220208T235959Z
&X-Amz-Expires=250
&X-Amz-Security-Token=security-token
&X-Amz-Signature=string
&X-Amz-SignedHeaders=content-type%3Bhost%3Bx-amz-date
&language-code=en-US
&media-encoding=flac
&sample-rate=16000    
&pii-entity-types=NAME,ADDRESS
&content-redaction-type=PII (or &content-identification-type=PII)
```

You cannot use both `content-identification-type` and `content-redaction-type` in the same request\.

Parameter definitions can be found in the [API Reference](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_Reference.html); parameters common to all AWS API operations are listed in the [Common Parameters](https://docs.aws.amazon.com/transcribe/latest/APIReference/CommonParameters.html) section\.

## HTTP/2 stream<a name="redaction-http2"></a>

This example creates an HTTP/2 request with PII identification or PII redaction enabled\. For more information on using HTTP/2 streaming with Amazon Transcribe, see [Setting up an HTTP/2 stream](streaming-http2.md)\. For more detail on parameters and headers specific to Amazon Transcribe, see [StartStreamTranscription](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_streaming_StartStreamTranscription.html)\.

```
POST /stream-transcription HTTP/2
host: transcribestreaming.us-west-2.amazonaws.com
X-Amz-Target: com.amazonaws.transcribe.Transcribe.StartStreamTranscription
Content-Type: application/vnd.amazon.eventstream
X-Amz-Content-Sha256: string
X-Amz-Date: 20220208T235959Z
Authorization: AWS4-HMAC-SHA256 Credential=access-key/20220208/us-west-2/transcribe/aws4_request, SignedHeaders=content-type;host;x-amz-content-sha256;x-amz-date;x-amz-target;x-amz-security-token, Signature=string
x-amzn-transcribe-language-code: en-US
x-amzn-transcribe-media-encoding: flac
x-amzn-transcribe-sample-rate: 16000      
x-amzn-transcribe-content-identification-type: PII (or x-amzn-transcribe-content-redaction-type: PII)
x-amzn-transcribe-pii-entity-types: NAME,ADDRESS
transfer-encoding: chunked
```

You cannot use both `content-identification-type` and `content-redaction-type` in the same request\.

Parameter definitions can be found in the [API Reference](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_Reference.html); parameters common to all AWS API operations are listed in the [Common Parameters](https://docs.aws.amazon.com/transcribe/latest/APIReference/CommonParameters.html) section\.

**Note**  
PII redaction for streaming is only supported in these AWS Regions: Asia Pacific \(Seoul\), Asia Pacific \(Sydney\), Asia Pacific \(Tokyo\), Canada \(Central\), EU \(Frankfurt\), EU \(Ireland\), EU \(London\), US East \(N\. Virginia\), US East \(Ohio\), and US West \(Oregon\)\.