# Step 2: Providing Amazon Transcribe with Data Permissions<a name="training-data-permissions"></a>

To create a custom language model, you need to give Amazon Transcribe access to your text data\. To do this, give Amazon Transcribe the `GetObject` and `ListBucket` permissions to your Amazon Simple Storage Service \(Amazon S3\) bucket\.

**To provide data permissions**

1. Sign in to AWS Management Console and open the IAM console at [IAM console](https://console.aws.amazon.com/iam/)\.

1. In the navigation pane, for **Access management**, choose **Roles** and choose one of the following options\.
   + Choose the name of the IAM role to use to create your custom language model and run transcription jobs\.
   + To create a new IAM role, choose **Create role**\.

     1. Under **Common use cases**, choose **EC2**\. You can select any use case, but EC2 is one of the most straightforward ones\.

     1. Choose **Next: Tags**\.

     1. Choose **Next: Review**\.

     1. Specify a name for the role under **Role name**\. Remove the text under **Role description**\.

     1. Choose **Create role**\.

     1. Choose the role you've created\.

1. Choose **Trust relationships**\.

1. Choose **Edit trust relationship**\.

1. If you're using an existing role, modify your trust policy with the following code\. If you've created a new role using this procedure, replace the trust policy text with the following code\. 

   ```
   {
       "Version": "2012-10-17",
       "Statement": [
           {
               "Effect": "Allow",
               "Principal": {
                   "Service": "transcribe.amazonaws.com"
               },
               "Action": "sts:AssumeRole"
           }
       ]
   }
   ```

1. In the navigation pane, choose **Policies**\.

1. 
   + From the policy list, choose **AmazonTranscribeFullAccess**\.

     1. From **Policy actions**, choose **Attach policy**

     1. Choose the IAM role that you want to attach the policy to\.
   + Choose **Create policy**\.

     1. Choose **JSON**\.

     1. Enter the following code, which adds `GetObject` and `ListBucket` permissions:

        ```
        {
            "Version": "2012-10-17",
            "Statement": [
                {
                    "Action": [
                        "s3:GetObject"
                    ],
                    "Resource": [
                        "arn:aws:s3:::your-input-bucket/*"
                    ],
                    "Effect": "Allow"
                },
                {
                    "Action": [
                        "s3:ListBucket"
                    ],
                    "Resource": [
                        "arn:aws:s3:::your-input-bucket"
                    ],
                    "Effect": "Allow"
                }
            ]
        }
        ```

     1. Choose **Review policy**\.

     1. Specify a name for the policy\.

     1. Choose **Create policy**\.

     1. Attach the policy to the IAM role\.

Amazon Transcribe now has the necessary permissions to access the data for your custom language model\.

**Next Step**  
[Step 3: Creating a Custom Language Model](create-custom-language-model.md)