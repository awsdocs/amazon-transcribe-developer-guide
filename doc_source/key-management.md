# Key management<a name="key-management"></a>

Amazon Transcribe works with AWS Key Management Service \(KMS\) to provide enhanced encryption for your data\. Amazon S3 already enables you to encrypt your input audio when creating a transcription job\. Integration with KMS enables you to encrypt the output of the [StartTranscriptionJob](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_StartTranscriptionJob.html) API\. 

If you don't specify an AWS KMS key, the output of the transcription job is encrypted with the default Amazon S3 key \(SSE\-S3\)\.

For more information on AWS KMS, see the [AWS Key Management Service Developer Guide](https://docs.aws.amazon.com/kms/latest/developerguide/concepts.html)\.

## KMS encryption with the AWS Management Console<a name="kms-console"></a>

To encrypt the output of your transcription job, you can choose between using a KMS key for the account that is making the request, or you can use a KMS key from another account\.

If you don't specify a KMS key, the output of the transcription job is encrypted with the default Amazon S3 key \(SSE\-S3\)\.

**To enable output result encryption**

1. Under **Output data** choose **Encryption**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/output-encryption.png)![\[Image NOT FOUND\]](http://docs.aws.amazon.com/transcribe/latest/dg/)

1. Choose whether the KMS key is from the account you're currently using or from a different account\. If you want to use a key from the current account, choose the key from **KMS key ID**\. If you're using a key from a different account, you need to enter the key ARN\. To use a key from a different account, the caller must have `kms:Encrypt` permissions for the KMS key\.

## KMS encryption with the API<a name="kms-api"></a>

To use output encryption with the API, you set the `OutputEncryptionKMSKeyId` parameter of the [StartTranscriptionJob](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_StartTranscriptionJob.html) API\. You can use a KMS key from the current account, or you can use a key from another account\. The account that you are using to create the job must have `kms:Encrypt` permissions for the KMS key\.

You can use either of the following to identify a KMS key in the current account:
+ KMS Key ID: "1234abcd\-12ab\-34cd\-56ef\-1234567890ab"
+ KMS Key Alias: "alias/ExampleAlias"

You can use either of the following to identify a AWS KMS key in the current account or another account:
+ Amazon Resource Name \(ARN\) of a KMS Key: "arn:aws:kms:region:account\-ID:key/1234abcd\-12ab\-34cd\-56ef\-1234567890ab"
+ ARN of a KMS Key Alias: "arn:aws:kms:region:account\-ID:alias/ExampleAlias"

## KMS encryption context<a name="kms-context"></a>

AWS KMS encryption context is a map of plain text, non\-secret key:value pairs\. This map represents additional authenticated data, known as encryption context pairs, which provide an added layer of security for your data\. Amazon Transcribe requires a symmetric key to encrypt transcription output into a customer\-specified S3 bucket\. To learn more, see [Using symmetric and asymmetric keys](https://docs.aws.amazon.com/kms/latest/developerguide/symmetric-asymmetric.html)\.

When creating your encryption context pairs, **do not** use sensitive information\. Encryption context is not secret—it is visible in plain text within your CloudTrail logs \(so you can use it to identify and categorize your cryptographic operations\)\.

Your encryption context pair can include special characters, such as underscores \(\_\), dashes \(\-\), slashes \(/, \\\) and colons \(:\)\.

**Tip**  
It can be useful to relate the values in your encryption context pair to the data being encrypted\. Although not required, we recommend you use non\-sensitive metadata related to your encrypted content, such as file names, header values, or unencrypted database fields\.

To use output encryption with the API, set the `KMSEncryptionContext` parameter in the [StartTranscriptionJob](https://docs.aws.amazon.com/transcribe/latest/APIReference/API_StartTranscriptionJob.html) operation\. In order to provide encryption context for the output encryption operation, the `OutputEncryptionKMSKeyId` parameter must reference a symmetric KMS key ID\.

You can use [AWS KMS condition keys](https://docs.aws.amazon.com/kms/latest/developerguide/policy-conditions.html#conditions-kms) with IAM policies to control access to a symmetric KMS key based on the encryption context that was used in the request for a [cryptographic operation](https://docs.aws.amazon.com/kms/latest/developerguide/concepts.html#cryptographic-operations)\. For example, the following policy grants the IAM role “ExampleRole” permission to use the KMS *Decrypt* and *Encrypt* operations for this particular KMS key\. This policy works **only** for requests with at least one encryption context pair, in this case "color:indig0Blu3”\.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Principal": {
                "AWS": "arn:aws:iam::111122223333:role/ExampleRole"
            },
            "Action": [
                "kms:Decrypt",
                "kms:DescribeKey",
                "kms:Encrypt",
                "kms:GenerateDataKey*",
                "kms:ReEncrypt*"
            ],
            "Resource": "*",
            "Condition": {
                "StringEquals": {
                    "kms:EncryptionContext:color":"indig0Blu3"
                }
             }
          }
     ]
}
```

Using encryption context is optional, but recommended\. For more information, see [ Encryption context](https://docs.aws.amazon.com/kms/latest/developerguide/concepts.html#encrypt_context)\.