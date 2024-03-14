---
tags:
  - cloud/aws
---
![[Amazon Kinesis#Kinesis Data Streams]]

# FAQ
**Q: Can I encrypt the data I put into a Kinesis data stream?**

Yes, and there are two options for doing so. You can use server-side encryption, which is a fully managed feature that automatically encrypts and decrypts data as you put and get it from a data stream. You can also write encrypted data to a data stream by encrypting and decrypting on the client side.  

**Q: Why should I use server-side encryption instead of client-side encryption?**

You might choose server-side encryption over client-side encryption for any of the following reason:

- It is hard to enforce client-side encryption.
- They want a second layer of security on top of client-side encryption.
- It is hard to implement client-side key management schemes.

**Q: What is server-side encryption?**

Server-side encryption for Kinesis Data Streams automatically encrypts data using a user specified AWS KMS key before it is written to the data stream storage layer, and decrypts the data after it is retrieved from storage. Encryption makes writes impossible and the payload and the partition key unreadable unless the user writing or reading from the data stream has the permission to use the key selected for encryption on the data stream. As a result, server-side encryption can make it easier to meet internal security and compliance requirements governing your data.

With server-side encryption your client-side applications (producers and consumers) do not need to be aware of encryption, they do not need to manage KMS keys or cryptographic operations, and your data is encrypted when it is at rest and in motion within the Kinesis Data Streams service. All KMS keys used by the server-side encryption feature are provided by the AWS KMS. AWS KMS makes it easy to use an AWS-managed KMS key for Kinesis (a “one-click” encryption method), your own AWS KMS customer-managed key, or a KMS key that you imported for encryption.  

**Q: Is there a server-side encryption getting started guide?**

Yes, there is a getting started guide in the user [documentation](https://docs.aws.amazon.com/streams/latest/dev/server-side-encryption.html).

**Q: Does server-side encryption interfere with how my applications interact with Kinesis Data Streams?**

Possibly. It depends on the key you use for encryption and the permissions governing access to the key.

- If you use the AWS-managed KMS key for Kinesis (key alias = aws/kinesis) your applications will not be impacted by enabling or disabling encryption with this key.
- If you use a different KMS key, like a custom AWS KMS key or one you imported into the AWS KMS service, and if your producers and consumers of a data stream do not have permission to use the KMS key used for encryption, then your PUT and GET requests will fail. Before you can use server-side encryption you must configure AWS KMS key policies to allow encryption and decryption of messages. For examples and more information about AWS KMS permissions, see AWS KMS API Permissions: Actions and Resources Reference in the AWS Key Management Service Developer Guide or the permissions guidelines in the Kinesis Data Streams [server-side encryption user documentation](https://docs.aws.amazon.com/streams/latest/dev/server-side-encryption.html).

**Q: Is there an additional cost associated with the use of server-side encryption?**

Yes, however if you are using the AWS-managed KMS key for Kinesis and are not exceeding the AWS Free Tier KMS API usage costs, your use of server-side encryption is free. The following describes the costs by resource:

**Keys:**

The AWS-managed KMS key for Kinesis (alias = “aws/kinesis”) is free.  
Customer managed KMS keys are subject to KMS key costs. [Learn more](https://aws.amazon.com/kms/pricing/).

**KMS API Usage:**

API usage costs apply for every KMS key, including custom ones. Kinesis Data Streams calls KMS approximately every five minutes when it’s rotating the data key. In a 30-day month, the total cost of KMS API calls initiated by a Kinesis data stream should be less than a few dollars. Note that this cost scales with the number of user credentials you use on your data producers and consumers because each user credential requires a unique API call to AWS KMS. When you use IAM role for authentication, each assume role-call will result in unique user credentials, and you might want to cache user credentials returned by the assume-role-call to save KMS costs.  

**Q: Which AWS regions offer server-side encryption for Kinesis Data Streams?**

Kinesis Data Streams server-side encryption is available in the AWS GovCloud Region and all public Regions except the China (Beijing) Region.

**Q: How do I start, update, or remove server-side encryption from a data stream?**

All of these operations can be completed using the AWS Management Console or the AWS SDK. To learn more, see the [Kinesis Data Streams server-side encryption getting started guide](https://docs.aws.amazon.com/streams/latest/dev/server-side-encryption.html).

**Q: What encryption algorithm is used for server-side encryption?**

Kinesis Data Streams uses an [AES-GCM 256 algorithm](https://docs.aws.amazon.com/kms/latest/developerguide/crypto-intro.html) for encryption.

**Q: If I encrypt a data stream that already has data written to it, either in plain text or ciphertext, will all of the data in the data stream be encrypted or decrypted if I update encryption?**

No. Only new data written into the data stream will be encrypted (or left decrypted) by the new application of encryption.

**Q: What does server-side encryption for Kinesis Data Streams encrypt?**

Server-side encryption encrypts the payload of the message along with the partition key, which is specified by the data stream producer applications.

**Q: Is server-side encryption a shard specific feature or a stream specific feature?**

Server-side encryption is a stream specific feature.

**Q: Can I change the KMS key that is used to encrypt a specific data stream?**

Yes, using the AWS Management Console or the AWS SDK, you can choose a new KMS key to apply to a specific data stream.

**Q: Is Kinesis Data Streams available in the AWS Free Tier?**

No. Kinesis Data Streams is not currently available in the AWS Free Tier. AWS  
Free Tier is a program that offers free trial for a group of AWS services. For more  
details about AWS Free Tier, see [AWS Free Tier](https://aws.amazon.com/free/).