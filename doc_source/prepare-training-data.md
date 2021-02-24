# Step 1: Preparing the data<a name="prepare-training-data"></a>

Create a custom language model by providing training data in plain text format and by choosing a base model\. You can also provide additional tuning data, also in plain text format, for optimization\.

To prepare your text data:

1. Properly format it and save it in one or more text files\. Make sure that each text file:
   + Is in US English \(en\-US\)\.
   + Is in plain text \(it's not a file such as a Microsoft Word document, comma\-separated value file, or PDF\)\.
   + Has a single sentence per line\.
   + Is encoded in UTF\-8\.
   + Doesn't contain any formatting characters, such as HTML tags\.
   + Is less than 2 GB in size if you intend to use the file as training data\. You can provide a maximum of 2 GB of training data\.
   + Is less than 200 MB in size if you intend to use the file as tuning data\. You can provide a maximum of 200 MB of optional tuning data\.

1. Upload those files to Amazon Simple Storage Service \(Amazon S3\)\. If you intend to tune the model, store your tuning data in a separate S3 bucket from the one you use for your training data\.

 Use your own data processing pipelines to prepare your plain text files\. If you're extracting text from HTML, remove the HTML tags and unescape the entities\. 

The following example shows how to format sentences in a text file:

```
Ribosomes help translate RNA into protein.
RISC is essential in RNA interference.
Interferon type 1 signaling proteins help prevent viruses from replicating their RNA or DNA.
...
```

It doesn't matter how many text files you use to upload your training or tuning data\. For model training, you get the same improvements in transcription accuracy if you use one file with 100,000 words or 10 files with 10,000 words\. Prepare your text data in a way that is most convenient for you\.

**Next step**  
[Step 2: Providing Amazon Transcribe with data permissions](training-data-permissions.md)