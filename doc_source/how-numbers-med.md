# Transcribing numbers<a name="how-numbers-med"></a>

Amazon Transcribe Medical transcribes digits as numbers instead of words\. For example, the spoken number "one thousand two hundred forty\-two" is transcribed as 1242\.

Numbers are transcribed according to the following rules\.


| Rule | Description | 
| --- | --- | 
| Convert cardinal numbers greater than 10 to numbers\. |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/transcribe/latest/dg/how-numbers-med.html)  | 
| Convert cardinal numbers followed by "million" or "billion" to numbers followed by a word when "million" or "billion" is not followed by a number\. |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/transcribe/latest/dg/how-numbers-med.html)  | 
|  Convert ordinal numbers greater than 10 to numbers\.  |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/transcribe/latest/dg/how-numbers-med.html)  | 
|  Convert fractions to their numeric format\.  |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/transcribe/latest/dg/how-numbers-med.html)  | 
| Convert numbers less than 10 to digits if there are more than one in a row\. |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/transcribe/latest/dg/how-numbers-med.html)  | 
| Decimals are indicated by "dot" or "point\." |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/transcribe/latest/dg/how-numbers-med.html)  | 
|  Convert the word "percent" after a number to a percent sign\.  |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/transcribe/latest/dg/how-numbers-med.html)  | 
|  Convert the words "dollar," "US dollar," "Australian dollar, "AUD," or "USD" after a number to a dollar symbol before the number\.  |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/transcribe/latest/dg/how-numbers-med.html)  | 
|  Convert the words "pounds," or "milligrams" to "lbs" or "mg"\.  |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/transcribe/latest/dg/how-numbers-med.html)  | 
|  Convert the words "rupees," "Indian rupees," or "INR" after a number to rupee sign \(₹\) before the number\.  |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/transcribe/latest/dg/how-numbers-med.html)  | 
|  Convert times to numbers\.  |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/transcribe/latest/dg/how-numbers-med.html)  | 
|  Combine years expressed as two digits into four\. Only valid for the 20th, 21st, and 22nd centuries\.   |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/transcribe/latest/dg/how-numbers-med.html)  | 
| Convert dates to numbers\. |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/transcribe/latest/dg/how-numbers-med.html)  | 
|  Separate spans of numbers by the word "to\."  |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/transcribe/latest/dg/how-numbers-med.html)  | 