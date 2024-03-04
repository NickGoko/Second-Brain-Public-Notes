---
tags:
  - cloud/aws
---
**AWS Key Management Store (KMS)** is <mark style="background: #D2B3FFA6;">a managed service that enables you to easily encrypt your data.</mark>

_AWS KMS_ <mark style="background: #ABF7F7A6;">provides a highly available key storage, management, and auditing solution for you to encrypt data within your own applications and control the encryption of stored data across AWS services.</mark>

AWS KMS allows you to centrally manage and securely store your keys. These are known as AWS KMS keys (formerly known as customer master keys (CMKs).

![](https://i.imgur.com/s7Pv4xL.png)  
![](https://i.imgur.com/sr7CLsm.png)  
![](https://i.imgur.com/4dfhIeI.png)  
![](https://i.imgur.com/s7OpIRw.png)  
 ![](https://i.imgur.com/zXazY99.png)

![](https://i.imgur.com/wXGl2PQ.png)  
![](https://i.imgur.com/nJq3s6v.png)

## AWS KMS Keys

A KMS key consists of:
- Alias.
- Creation date.
- Description.
- Key state.
- Key material (either customer provided or AWS provided).

**KMS keys** are the primary resources in AWS KMS.

The KMS key includes metadata, such as the key ID, creation date, description, and key state.

The KMS key also contains the key material used to encrypt and decrypt data.

<mark style="background: #FFF3A3A6;">AWS KMS supports symmetric and asymmetric KMS keys.</mark>

![[Pasted image 20240229210853.png]]  
KMS keys are created in AWS KMS. Symmetric KMS keys and the private keys of asymmetric KMS keys never leave AWS KMS unencrypted.

By default, AWS KMS creates the key material for a KMS key.

A KMS key can encrypt data up to 4KB in size.

A KMS key can generate, encrypt, and decrypt Data Encryption Keys (DEKs).

- A KMS key can never be exported from KMS (CloudHSM allows this).

![](https://i.imgur.com/6HSSPiJ.png)

**AWS Managed KMS keys**:
- KMS keys managed by AWS are used by AWS services that interact with KMS to encrypt data.
- They can only be used by the service that created them within a particular region.
- They are created on the first time you implement encryption using that service.

**Customer managed KMS keys**:
- These provide the ability to implement greater flexibility.
- You can perform rotation, governing access, and key policy configuration.
- You are able to enable and disable the key when it is no longer required.

![AWS KMS CMKs](https://digitalcloud.training/wp-content/uploads/2022/01/aws-kms-cmks.jpeg)

## Customer Managed KMS Keys

Customer managed KMS keys are KMS keys in your AWS account that you create, own, and manage.

You have full control over these KMS keys, including establishing and maintaining their key policies, IAM policies, and grants, enabling and disabling them, rotating their cryptographic material, adding tags, creating aliases that refer to the KMS key, and scheduling the KMS keys for deletion.

Customer managed KMS keys incur a monthly fee and a fee for use in excess of the free tier.

## AWS Managed KMS Keys

AWS managed KMS keys are KMS keys in your account that are created, managed, and used on your behalf by an AWS service that is integrated with AWS KMS.

You cannot manage these KMS keys, rotate them, or change their key policies.

You also cannot use AWS managed KMS keys in cryptographic operations directly; the service that creates them uses them on your behalf.

You do not pay a monthly fee for AWS managed KMS keys. They can be subject to fees for use in excess of the free tier, but some AWS services cover these costs for you.

## AWS Owned KMS Keys

AWS owned KMS keys are a collection of KMS keys that an AWS service owns and manages for use in multiple AWS accounts.

Although AWS owned KMS keys are not in your AWS account, an AWS service can use its AWS owned KMS keys to protect the resources in your account.

You do not need to create or manage the AWS owned KMS keys.

However, you cannot view, use, track, or audit them.

You are not charged a monthly fee or usage fee for AWS owned KMS keys and they do not count against the AWS KMS quotas for your account.

## Data Encryption Keys

Data keys are encryption keys that you can use to encrypt data, including large amounts of data and other data encryption keys.

You can use AWS KMS keys to generate, encrypt, and decrypt data keys.

AWS KMS does not store, manage, or track your data keys, or perform cryptographic operations with data keys.

You must use and manage data keys outside of AWS KMS.

The GenerateDataKey API can be used to create a data encryption key using a KMS key:

![Amazon KMS data encryption keys](https://digitalcloud.training/wp-content/uploads/2022/01/amazon-kms-data-encryption-keys.jpeg)

## KMS Details

You set usage policies on the keys that determine which users can use them to encrypt and decrypt data and under which conditions.

Key material options:

- KMS generated.
- Import your own.

You can generate KMS keys in KMS, in an AWS CloudHSM cluster, or import them from your own key management infrastructure.

These master keys are protected by hardware security modules (HSMs) and are only ever used within those modules.

You can submit data directly to KMS to be encrypted or decrypted using these master keys.

KMS now has the option for symmetric and asymmetric keys.

KMS is for encryption at rest only (not in transit, use SSL).

KMS is tightly integrated into many AWS services like Lambda, S3, EBS, EFS, DynamoDB, SQS etc.

Data keys are not retained or managed by KMS.

AWS services encrypt your data and store an encrypted copy of the data key along with the data it protects.

When a service needs to decrypt your data they request KMS to decrypt the data key using your master key.

If the user requesting data from the AWS service is authorized to decrypt under your master key policy, the service will receive the decrypted data key from KMS with which it can decrypt your data and return it in plaintext.

All requests to use your master keys are logged in AWS CloudTrail so you can understand who used which key under which context and when they used it.

You can control who manages and accesses keys via IAM users and roles.

You can audit the use of keys via CloudTrail.

KMS differs from Secrets Manager as its purpose-built for encryption key management.

KMS is validated by many compliance schemes (e.g. PCI DSS Level 1, FIPS 140-2 Level 2).

**Exam tip:** Encryption keys are regional.

## Key Management with KMS
![](https://i.imgur.com/ZSb9t0f.png)  
![](https://i.imgur.com/YPIyjjR.png)

You can perform the following key management functions in AWS KMS:

- Create keys with a unique alias and description.
- Import your own key material.
- Define which IAM users and roles can manage keys.
- Define which IAM users and roles can use keys to encrypt and decrypt data.
- Choose to have AWS KMS automatically rotate your keys on an annual basis.
- Temporarily disable keys so they cannot be used by anyone.
- Re-enable disabled keys.
- Delete keys that you no longer use.
- Audit use of keys by inspecting logs in AWS CloudTrail.
- Create custom key stores*.
- Connect and disconnect custom key stores*.
- Delete custom key stores*.

- The use of custom key stores requires CloudHSM resources to be available in your account.

## Data Encryption Scenarios

Typically, data is encrypted in one of the following three scenarios:

1. You can use KMS APIs directly to encrypt and decrypt data using your master keys stored in KMS.
2. You can choose to have AWS services encrypt your data using your master keys stored in KMS. In this case data is encrypted using data keys that are protected by your master keys in KMS.
3. You can use the AWS Encryption SDK that is integrated with AWS KMS to perform encryption within your own applications, whether they operate in AWS or not.

## Custom Key Store

The AWS KMS custom key store feature combines the controls provided by AWS CloudHSM with the integration and ease of use of AWS KMS.

You can configure your own CloudHSM cluster and authorize KMS to use it as a dedicated key store for your keys rather than the default KMS key store.

When you create keys in KMS you can chose to generate the key material in your CloudHSM cluster. Master keys that are generated in your custom key store never leave the HSMs in the CloudHSM cluster in plaintext and all KMS operations that use those keys are only performed in your HSMs.

In all other respects master keys stored in your custom key store are consistent with other KMS keys.

## Key Deletion

You can schedule a customer master key and associated metadata that you created in AWS KMS for deletion, with a configurable waiting period from 7 to 30 days.

This waiting period allows you to verify the impact of deleting a key on your applications and users that depend on it.

The default waiting period is 30 days.

You can cancel key deletion during the waiting period.

## AWS KMS API’s

The following APIs are useful to know for the exam:

Encrypt (aws kms encrypt):

- Encrypts plaintext into ciphertext by using a customer master key (KMS key).
- You can encrypt small amounts of arbitrary data, such as  a  personal identifier or database password, or other sensitive information.
- You can use the Encrypt operation to move encrypted data from one AWS region to another.

Decrypt (aws kms decrypt):

- Decrypts ciphertext that was encrypted by an AWS KMS key using any of the following operations:
    - Encrypt
    - GenerateDataKey
    - GenerateDataKeyPair
    - GenerateDataKeyWithoutPlaintext
    - GenerateDataKeyPairWithoutPlaintext

Re-encrypt (aws kms re-encrypt):

- Decrypts ciphertext and then re-encrypts it entirely within AWS KMS.
- You can use this operation to change the customer master  key  (KMS key)  under which  data  is  encrypted,  such  as when you manually rotate a KMS key or change the KMS key that protects a ciphertext.
- You can also use it to re-encrypt  ciphertext  under the same KMS key, such as to change the encryption context of a ciphertext.

Enable-key-rotation:

- Enables  automatic  rotation of the key material for the specified symmetric customer master key (KMS key).
- You cannot perform this operation  on a KMS key in a different AWS account.

GenerateDataKey (aws kms generate-data-key):

- Enables  automatic  rotation of the key material for the specified symmetric customer master key (KMS key).
- You cannot perform this operation  on a KMS key in a different AWS account.

GenerateDataKeyWithoutPlaintext (generate-data-key-without-plaintext):

- Generates  a  unique  symmetric data key.
- This operation returns a data key that is encrypted under a customer master key (KMS key) that you  specify.
- To request an asymmetric data key pair, use the  GenerateDataKeyPair or  GenerateDataKeyPairWithoutPlaintext operations.

## KMS Envelope Encryption

AWS KMS is integrated with AWS services and client-side toolkits that use a method known as envelope encryption to encrypt your data.

Under this method, KMS generates data keys which are used to encrypt data and are themselves encrypted using your master keys in KMS:

- A KMS key is used to encrypt the data key (envelope key).
- The envelope key is used to decrypt the data.

## Limits

You can create up to 1000 KMS keys per account per region.

As both enabled and disabled KMS keys count towards the limit, AWS recommend deleting disabled keys that you no longer use.

AWS managed master keys created on your behalf for use within supported AWS services do not count against this limit.

There is no limit to the number of data keys that can be derived using a master key and used in your application or by AWS services to encrypt data on your behalf.

---
![](https://i.imgur.com/hvG5FEI.png)  
![](https://i.imgur.com/ZAxEp7O.png)

# FAQ

## General

### Q: What is AWS KMS?

AWS KMS is a managed service that helps you more easily create and control the keys used for cryptographic operations. The service provides a highly available key generation, storage, management, and auditing solution for you to encrypt or digitally sign data within your own applications or control the encryption of data across AWS services.  

### Q: Why Should I Use AWS KMS?

If you are responsible for securing your data across AWS services, you should use it to centrally manage the encryption keys that control access to your data. If you are a developer who needs to encrypt data in your applications, you should use the [AWS Encryption SDK](https://docs.aws.amazon.com/encryption-sdk/latest/developer-guide/introduction.html) with AWS KMS to more easily generate, use and protect symmetric encryption keys in your code. If you are a developer who needs to digitally sign or verify data using asymmetric keys, you should use the service to create and manage the private keys you’ll need. If you’re looking for a scalable key management infrastructure to support your developers and their growing number of applications, you should use it to reduce your licensing costs and operational burden. If you’re responsible for proving data security for regulatory or compliance purposes, you should use it because it facilitates proving your data is consistently protected. It’s also in scope for a broad set of industry and regional compliance regimes.  

### Q: How Do I Get Started with AWS KMS?

The easiest way to get started with AWS KMS is to choose to encrypt your data with an AWS service that uses AWS owned root keys that are automatically created by each service. If you want full control over the management of your keys, including the ability to share access to keys across accounts or services, you can create your own AWS KMS customer managed keys in AWS KMS. You can also use the KMS keys that you create directly within your own applications. AWS KMS can be accessed from the [KMS console](https://console.aws.amazon.com/kms/home) that is grouped under Security, Identity and Compliance on the [AWS Services home page](https://console.aws.amazon.com/console/home) of the AWS KMS Console. AWS KMS APIs can also be accessed directly through the AWS KMS Command Line Interface (CLI) or AWS SDK for programmatic access. AWS KMS APIs can also be used indirectly to encrypt data within your own applications by using the [AWS Encryption SDK](https://docs.aws.amazon.com/encryption-sdk/latest/developer-guide/introduction.html). Visit the [Getting Started](https://aws.amazon.com/kms/getting-started/) page to learn more.

### Q: In what AWS Regions is AWS KMS Available?

### Q: What Key Management Features Are Available in AWS KMS?

You can perform the following key management functions:

- Create symmetric, asymmetric, and HMAC keys where the key material is only ever used within the service
- Create symmetric keys where the key material is generated and used within a custom key store under your control and backed by either AWS CloudHSM or your own external key manager outside of AWS.
- Import your own symmetric, asymmetric, and HMAC key material for use within supported AWS services and your own application
- Define which AWS Identity and Access Management (IAM) users and roles can manage keys
- Define which IAM users and roles can use keys to encrypt and decrypt data
- Choose to have keys that were generated by the service to be automatically rotated on an annual basis
- Temporarily disable keys so they cannot be used by anyone
- Re-enable disabled keys
- Schedule the deletion of keys that you no longer use
- Audit use of keys by inspecting logs in AWS CloudTrail

### Q: How Does AWS KMS Work?

You can start using the service by requesting the creation of an AWS KMS key. You control the lifecycle of any customer managed KMS key and who can use or manage it. Once you have created a KMS key, you can submit data directly to the service AWS KMS to be encrypted, decrypted, signed, verified, or to generate or verify an HMAC using this KMS key. You set usage policies on these keys that determine which users can perform which actions under which conditions.

AWS services and client-side toolkits that integrate with AWS KMS use a method known as envelope encryption to protect your data. Under this method, AWS KMS generates data keys that are used to encrypt data locally in the AWS service or your application. The data keys are themselves encrypted under an AWS KMS key you define. Data keys are not retained or managed by AWS KMS. AWS services encrypt your data and store an encrypted copy of the data key along with the encrypted data. When a service needs to decrypt your data, it requests AWS KMS to decrypt the data key using your KMS key. If the user requesting data from the AWS service is authorized to decrypt under your KMS key, the AWS service will receive the decrypted data key from AWS KMS. The AWS service then decrypts your data and returns it in plaintext. All requests to use your KMS keys are logged in CloudTrail so you can understand who used which key under what context and when they used it.

### Q: Where is My Data Encrypted if I Use AWS KMS?

There are typically three scenarios for how data is encrypted using AWS KMS. First, you can use AWS KMS APIs directly to encrypt and decrypt data using your KMS keys stored in the service. Second, you can choose to have AWS services encrypt your data using your KMS keys stored in the service. In this case data is encrypted using data keys that are protected by your KMS keys. Third, you can use the AWS Encryption SDK that is integrated with AWS KMS to perform encryption within your own applications, whether they operate in AWS or not.

### Q: Which AWS Cloud Services Are Integrated with AWS KMS?

AWS KMS is seamlessly integrated with most other AWS services to make encrypting data in those services easier. In some cases, data is encrypted by default using keys that are stored in AWS KMS but owned and managed by the AWS service in question. In many cases the AWS KMS keys are owned and managed by you within your account. Some services give you the choice of managing the keys yourself or allowing the service to manage the keys on your behalf. See the [list of AWS services](https://aws.amazon.com/kms/features/#AWS_Service_Integration) currently integrated with AWS KMS. See the [AWS KMS Developer’s Guide](https://docs.aws.amazon.com/kms/latest/developerguide/service-integration.html) for more information on how integrated services use AWS KMS.

### Q: Why Use Envelope Encryption? Why not just Send Data to AWS KMS to Encrypt Directly?

While AWS KMS does support sending data up to 4 KB to be encrypted directly, envelope encryption can offer significant performance benefits. When you encrypt data directly with AWS KMS it must be transferred over the network. Envelope encryption reduces the network load since only the request and delivery of the much smaller data key go over the network. The data key is used locally in your application or encrypting AWS service, avoiding the need to send the entire block of data to AWS KMS and suffer network latency.

### Q: What’s the Difference between a KMS Key I Create and KMS Keys Created Automatically for Me by other AWS Services?

You have the option of selecting a specific KMS key to use when you want an AWS service to encrypt data on your behalf. These are known as customer managed KMS keys and you have full control over them. You define the access control and usage policy for each key and you can grant permissions to other accounts and services to use them. In addition to customer managed keys, AWS KMS also provides two types of keys managed by AWS: (1) AWS managed KMS keys are keys created in your account but managed by AWS, and (2) AWS owned keys are keys fully owned and operated from AWS accounts. You can track AWS managed keys in your account and all usage is logged in CloudTrail, but you have no direct control over the keys themselves. AWS owned keys are the most automated and provide encryption of your data within AWS but do not provide policy controls or CloudTrail logs on their key activity.

### Q: Why Should I Create My Own AWS KMS Keys?

Creating your own KMS key gives you more control than you have with AWS managed KMS keys. When you create a symmetric customer managed KMS key, you can choose to use key material generated by AWS KMS, generated within an AWS CloudHSM cluster or external key manager (through the custom key store), or import your own key material. You can define an alias and description for the key and opt-in to have the key automatically rotated once per year if it was generated by AWS KMS. You also define all the permissions on the key to control who can use or manage the key. With asymmetric customer managed KMS keys, there are a couple of caveats to management: the key material can only be generated within AWS KMS HSMs and there is no option for automatic key rotation.

### Q: Can I Rotate My Keys?

Yes. You can choose to have AWS KMS automatically rotate KMS keys every year, provided that those keys were generated within AWS KMS HSMs. Automatic key rotation is not supported for imported keys, asymmetric keys, or keys generated in a CloudHSM cluster using the AWS KMS custom key store feature. If you choose to import keys to AWS KMS or asymmetric keys or use a custom key store, you can manually rotate them by creating a new KMS key and mapping an existing key alias from the old KMS key to the new KMS key.

### Q: Do I Have to Re-encrypt My Data after Keys in AWS KMS Are Rotated?

If you choose to have AWS KMS automatically rotate keys, you don’t have to re-encrypt your data. AWS KMS automatically keeps previous versions of keys to use for decryption of data encrypted under an old version of a key. All new encryption requests against a key in AWS KMS are encrypted under the newest version of the key.If you manually rotate your imported or custom key store keys, you may have to re-encrypt your data depending on whether you decide to keep old versions of keys available.

If you manually rotate your imported or custom key store keys, you may have to re-encrypt your data depending on whether you decide to keep old versions of keys available.

### Q: Can I Delete a Key from AWS KMS?

Yes. You can schedule an AWS KMS key and associated metadata that you created in AWS KMS for deletion, with a configurable waiting period from 7 to 30 days. This waiting period helps you verify the impact of deleting a key on your applications and users that depend on it. The default waiting period is 30 days. You can cancel key deletion during the waiting period. The key cannot be used if it is scheduled for deletion until you cancel the deletion during the waiting period. The key gets deleted at the end of the configurable waiting period if you don’t cancel the deletion. Once a key is deleted, you can no longer use it. All data protected under a deleted root key is inaccessible.

For customer AWS KMS keys with imported key material, you can delete the key material without deleting the AWS KMS key id or metadata in two ways. First, you can delete your imported key material on demand without a waiting period. Second, at the time of importing the key material into the AWS KMS key, you can define an expiration time for how long AWS can use your imported key material before it is deleted. You can re-import your key material into the AWS KMS key if you need to use it again.

### Q: Can I Use AWS KMS to Help Manage Encryption of Data outside of AWS Cloud Services?

Yes. AWS KMS is supported in AWS SDKs, AWS Encryption SDK, the Amazon DynamoDB Client-side Encryption, and the Amazon Simple Storage Service (S3) Encryption Client to facilitate encryption of data within your own applications wherever they run. Visit the [AWS Crypto Tools](https://docs.aws.amazon.com/aws-crypto-tools/) and [Developing on AWS](https://aws.amazon.com/developers/getting-started/) website for more information.

### Q: Is there a Limit to the Number of Keys I Can Create in AWS KMS?

You can create up to 100,000 KMS keys per account per Region. As both enabled and disabled KMS keys count towards the limit, we recommend deleting disabled keys that you no longer use. AWS managed KMS keys created on your behalf for use within supported AWS services do not count against this limit. There is no limit to the number of data keys that can be derived using a KMS key and used in your application or by AWS services to encrypt data on your behalf. You may request a limit increase for KMS keys by visiting the [AWS Support Center.](https://aws.amazon.com/premiumsupport/)

### Q: Can Any KMS Keys Be Exported out of the Service in Plain Text?

No. All KMS keys or the private portion of an asymmetric KMS key cannot be exported in plain text from the HSMs. Only the public portion of an asymmetric KMS key can be exported from the console or by calling the GetPublicKey API.

### Q: Can Data Keys and Data Key Pairs Be Exported out of the HSMs in Plain Text?

Yes. The symmetric data keys can be exported using either the GenerateDataKey API or the GenerateDataKeyWithoutPlaintext API. Also, the private and public portion of asymmetric data key pairs can be exported out of AWS KMS using either the GenerateDataKeyPair API or the GenerateDataKeypairWithoutPlaintext API.

### Q: How Are Data Keys and Data Key Pairs Protected for Storage outside the Service?

The symmetric data key or the private portion of the asymmetric data key is encrypted under the symmetric KMS key you define when you request AWS KMS to generate the data key.

The primary reason to use the [AWS Private CA](https://docs.aws.amazon.com/privateca/latest/userguide/PcaWelcome.html) service is to provide a public key infrastructure (PKI) for the purpose of identifying entities and securing network connections. PKI provides processes and mechanisms, primarily using X.509 certificates, to put structure around public key cryptographic operations. Certificates provide an association between an identity and a public key. The certification process in which a certificate authority issues a certificate allows the trusted certificate authority to assert the identity of another entity by signing a certificate. PKI provides identity, distributed trust, key lifecycle management, and certificate status vended through revocation. These functions add important processes and infrastructure to the underlying asymmetric cryptographic keys and algorithms provided by AWS KMS.

AWS Private CA helps you issue certificates to identify web and application servers, service meshes, VPN users, internal API endpoints, and AWS IoT Core devices. Certificates help you establish the identity of these resources and create encrypted TLS/SSL communications channels. If you are considering using asymmetric keys for TLS termination on web or application servers, Elastic Load Balancers, API Gateway endpoints, Amazon Elastic Compute Cloud (EC2) instances or containers, you should consider using AWS Private CA for issuing certificates and providing a PKI infrastructure.

In contrast, AWS KMS helps you generate, manage, and use asymmetric keys for digital signing and encryption operations that don’t require certificates. While certificates can enable verification of sender and recipient identity among untrusted parties, the kind of raw asymmetric operations offered by AWS KMS are typically useful when you have other mechanisms to prove identity or don’t need to prove it to get the security benefit you desire.

### Q: Can I Use My applications’ Cryptographic API Providers such as OpenSSL, JCE, Bouncy Castle, or CNG with AWS KMS?

There is no native integration offered by AWS KMS for any other cryptographic API providers. You must use AWS KMS APIs directly or through the AWS SDK to integrate signing and encryption capabilities into your applications.

### Q: Does AWS KMS Offer a Service Level Agreement (SLA)?

Yes. The [AWS KMS SLA](https://aws.amazon.com/kms/sla/) provides for a service credit if your monthly uptime percentage is below our service commitment in any billing cycle.

## Security

### Q: Who Can Use and Manage My Keys in AWS KMS?

AWS KMS enforces usage and management policies that you define. You can choose to allow IAM users and roles from your account or other accounts to use and manage your keys.

### Q: How Does AWS Secure the KMS Keys that I Create?

AWS KMS is designed so that no one, including AWS employees, can retrieve your plaintext KMS keys from the service. AWS KMS uses hardware security modules (HSMs) that have been validated under FIPS 140-2, or are in the process of being validated, to protect the confidentiality and integrity of your keys. Your plaintext KMS keys never leave the HSMs, are never written to disk, and are only ever used in the volatile memory of the HSMs for the time needed to perform your requested cryptographic operation. Updates to software on the service hosts and to the AWS KMS HSM firmware is controlled by multi-party access control that is audited and reviewed by an independent group within Amazon and a NIST-certified lab in compliance with FIPS 140-2.

More details about these security controls can be found in the [AWS KMS cryptographic details tech paper](https://docs.aws.amazon.com/kms/latest/cryptographic-details/intro.html). You can also review the [FIPS 140-2 certificate for AWS KMS HSMs](https://csrc.nist.gov/projects/cryptographic-module-validation-program/certificate/4523) along with the associated [Security Policy](https://csrc.nist.gov/CSRC/media/projects/cryptographic-module-validation-program/documents/security-policies/140sp4523.pdf) to get more details about how AWS KMS HSMs meets the security requirements of FIPS 140-2. Also, you can download a copy of the System and Organization Controls (SOC) report from [AWS Artifact](https://aws.amazon.com/artifact/) to learn more about security controls used by the service to protect your KMS keys.

### Q: How Do I Migrate My Existing AWS KMS Keys to Use FIPS 140-2 Security Level 3 Validated HSMs?

You do not need to do anything. All AWS KMS keys, regardless of their creation date or origin are automatically protected using HSMs that have been validated under FIPS 140-2 Security Level 3.

### Q: Which AWS Regions Have FIPS 140-2 Security Level 3 Validated HSMs?

FIPS 140-2 Security Level 3 validated HSMs are deployed in all AWS Regions where AWS KMS is offered.  
_NOTE: By regulation, AWS KMS in China Regions cannot use NIST FIPS HSMs and uses China's Office of the State Commercial Cryptographic Administration (OSCCA) certified HSMs instead._

### Q: What is the Difference between the FIPS 140-2 Validated Endpoints and the FIPS 140-2 Validated HSMs in AWS KMS?

AWS KMS is a two-tier service. The API endpoints receive client requests over an HTTPS connection using only TLS ciphersuites that support perfect forward secrecy. These API endpoints authenticate and authorize the request before passing the request for a cryptographic operation to the AWS KMS HSMs or your AWS CloudHSM cluster if you’re using the KMS custom key store feature.

### Q: How Do I Make API Requests to AWS KMS Using the FIPS 140-2 Validated Endpoints?

You configure your applications to connect to the unique regional [FIPS 140-2 validated HTTPS](https://docs.aws.amazon.com/general/latest/gr/rande.html#kms_region) endpoints. AWS KMS FIPS 140-2 validated HTTPS endpoints are powered by the [OpenSSL FIPS Object Module](https://csrc.nist.gov/CSRC/media/projects/cryptographic-module-validation-program/documents/security-policies/140sp4282.pdf). You can review the security policy of the OpenSSL module here. FIPS 140-2 validated API endpoints are available in all commercial Regions where AWS KMS is available.

### Q: Can I Use AWS KMS to Help Me Comply with the Encryption and Key Management Requirements in the Payment Card Industry Data Security Standard (PCI DSS 3.2.1)?

Yes. AWS KMS has been validated as having the functionality and security controls to help you meet the encryption and key management requirements (primarily referenced in sections 3.5 and 3.6) of the PCI DSS 3.2.1.

For more details on PCI DSS compliant services in AWS, you can read the [PCI DSS FAQs](https://aws.amazon.com/compliance/pci-dss-level-1-faqs/).

### Q: How Does AWS KMS Secure the Data Keys I Export and Use in My Application?

You can request that AWS KMS generate data keys and return them for use in your own application. The data keys are encrypted under a root key you define in AWS KMS so that you can safely store the encrypted data key along with your encrypted data. Your encrypted data key (and therefore your source data) can be decrypted by only users with permissions to use the original root key to decrypt your encrypted data key.

### Q: Can I Export an AWS KMS Key and Use it in My Own Applications?

No. AWS KMS keys are created and used only within the service to help verify their security, implement your policies to be consistently enforced, and provide a centralized log of their use.

### Q: What Geographic Region Are My Keys Stored In?

A single-Region KMS key generated by AWS KMS is stored and used only in the Region in which it was created. With AWS KMS multi-Region keys you can choose to replicate a multi-Region primary key into multiple Regions within the same AWS partition.

### Q: How Can I Tell Who Used or Changed the Configuration of My Keys in AWS KMS?

[Logs in AWS CloudTrail](https://docs.aws.amazon.com/kms/latest/developerguide/logging-using-cloudtrail.html) will show all AWS KMS API requests, including both management requests (such as create, rotate, disable, policy edits) and cryptographic requests (such as encrypt/decrypt). Turn on CloudTrail in your account to view these logs.

### Q: How Does AWS KMS Compare to CloudHSM?

[CloudHSM](https://docs.aws.amazon.com/cloudhsm/latest/userguide/introduction.html) provides you with a validated single-tenant HSM cluster in your Amazon Virtual Private Cloud (VPC) to store and use your keys. You have exclusive control over how your keys are used through an authentication mechanism independent from AWS. You interact with keys in your CloudHSM cluster similar to the way you interact with your applications running in Amazon EC2. You can use CloudHSM to support a variety of use cases, such as Digital Rights Management (DRM), Public Key Infrastructure (PKI), document signing, and cryptographic functions using PKCS#11, Java JCE, or Microsoft CNG interfaces.  

AWS KMS helps you to create and control the encryption keys used by your applications and supported AWS services in multiple Regions around the world from a single console. The service uses a FIPS HSM that has been validated under FIPS 140-2, or are in the process of being validated, to protect the security of your keys. Centralized management of all your keys in AWS KMS helps you enforce who can use your keys under which conditions, when they get rotated, and who can manage them. AWS KMS integration with CloudTrail gives you the ability to audit the use of your keys to support your regulatory and compliance activities. You interact with AWS KMS from your applications using the AWS SDK if you want to call the service APIs directly, through [other AWS services that are integrated with AWS KMS](https://aws.amazon.com/kms/features/#AWS_Service_Integration) or by using the [AWS Encryption SDK](https://docs.aws.amazon.com/encryption-sdk/latest/developer-guide/introduction.html) if you want to perform client-side encryption.  

## Billing

### Q: How Will I Be Charged and Billed for My Use of AWS KMS?

With AWS KMS, you pay only for what you use; there is no minimum fee. There are no set-up fees or commitments to begin using the service. At the end of the month, your credit card will automatically be charged for that month’s usage.

You are charged for all KMS keys you create and for API requests made to the service each month above a free tier.  

For current pricing information, please visit the [AWS KMS pricing page.](https://aws.amazon.com/kms/pricing/)  

### Q: Is there a Free Tier?

Yes. With the [AWS Free Tier](https://aws.amazon.com/free/) you can get started with AWS KMS for free\* in all Regions. AWS managed AWS KMS keys that are created on your behalf by AWS services are free to store in your account. There is a free tier for usage that provides a free number of requests to the service each month. For current information on pricing, including the Free Tier, please visit the [AWS KMS pricing page](https://aws.amazon.com/kms/pricing/).  

\*API requests involving asymmetric KMS keys and API requests to the GenerateDataKeyPair and GenerateDataKeyPairWithoutPlaintext APIs are excluded from the Free Tier.

### Q: Do Your Prices Include Taxes?

Except as otherwise noted, our prices are exclusive of applicable taxes and duties, including VAT and applicable sales tax. For customers with a Japanese billing address, use of AWS services is subject to Japanese Consumption Tax. You can learn more [here](https://aws.amazon.com/c-tax-faqs/).  

## Import

### Q: Can I Bring My Own Keys to AWS KMS?

Yes. You can import a copy of your key from your own key management infrastructure to AWS KMS and use it with any integrated AWS service or from within your own applications.

### Q: When Would I Use an Imported Key?

You can use an imported key to get greater control over the creation, lifecycle management, and durability of your key in AWS KMS. Imported keys are designed to help you meet your compliance requirements which may include the ability to generate or maintain a secure copy of the key in your infrastructure, and the ability to immediately delete the imported copy of the key from AWS infrastructure.

### Q: What Type of Keys Can I Import?

You can import symmetric keys, asymmetric keys (RSA and elliptic curve), and HMAC keys.

### Q: How is the Key that I Import into AWS KMS Protected in Transit?

During the import process, your key must be wrapped by an AWS KMS-provided public key using the supported wrapping algorithm. This verifies that your encrypted key can be decrypted by only AWS KMS.

### Q: What’s the Difference between a Key I Import and a Key I Generate in AWS KMS?

There are two main differences:  

1. You are responsible for maintaining a copy of your imported keys in your key management infrastructure so that you can re-import them at any time. AWS, however, verifies the availability, security, and durability of keys generated by AWS KMS on your behalf until you schedule the keys for deletion.
2. You may set an expiration period for an imported key. AWS KMS will automatically delete the key material after the expiration period. You can also delete imported key material on demand. In both cases the key material itself is deleted but the KMS key reference in AWS KMS and associated metadata are retained so that the key material can be re-imported in the future. Keys generated by AWS KMS do not have an expiration time and cannot be deleted immediately; there is a mandatory 7 to 30 day wait period. All customer managed KMS keys, regardless of whether the key material was imported, can be manually disabled or scheduled for deletion. In this case the KMS key itself is deleted, not just the underlying key material.

### Q: What Should I Do if My Imported Key Material Has Expired or I Accidentally Deleted It?

You can re-import your copy of the key material with a valid expiration period to AWS KMS under the original AWS KMS key so it can be used.

### Q: Can I Be Alerted that I Need to Re-import the Key?

Yes. Once you import your key to an AWS KMS key, you will receive a CloudWatch Metric every few minutes that counts down the time to expiration of the imported key. You will also receive a CloudWatch Event once the imported key under your AWS KMS key expires. You can build logic that acts on these metrics or events and automatically re-imports the key with a new expiration period to avoid an availability risk.

## Key Types and Algorithms

### Q: What Symmetric Encryption Key Types and Algorithms Are Supported?

AWS KMS supports 256-bit keys when creating a KMS key for encryption and decryption. Generated data keys returned to the caller can be 256-bit, 128-bit, or an arbitrary value up to 1024-bytes. When AWS KMS uses a 256-bit KMS key on your behalf to encrypt or decrypt, the AES algorithm in Galois Counter Mode (AES-GCM) is used.

### Q: What Kind of Asymmetric Encryption Key Types and Algorithms Are Supported?

AWS KMS supports the following asymmetric key types: RSA 2048, RSA 3072, RSA 4096, ECC NIST P-256, ECC NIST P-384, ECC NIST-521, and ECC SECG P-256k1. AWS KMS supports the RSAES\_OAEP\_SHA\_1 and RSAES\_OAEP\_SHA\_256 encryption algorithms with RSA 2048, RSA 3072, and RSA 4096 key types. Encryption algorithms cannot be used with the elliptic curve key types (ECC NIST P-256, ECC NIST P-384, ECC NIST-521, and ECC SECG P-256k1).

### Q: What Kinds of Asymmetric Signing Algorithms Are Supported?

When using RSA key types, AWS KMS supports the RSASSA\_PSS\_SHA\_256, RSASSA\_PSS\_SHA\_384, RSASSA\_PSS\_SHA\_512, RSASSA\_PKCS1\_V1\_5\_SHA\_256, RSASSA\_PKCS1\_V1\_5\_SHA\_384, and RSASSA\_PKCS1\_V1\_5\_SHA\_512 signing algorithms. When using elliptic curve key types, AWS KMS supports the ECDSA\_SHA\_256, ECDSA\_SHA\_384, and ECDSA\_SHA\_512 signing algorithms.

### Q: How Do I Use the Public Portion of an Asymmetric KMS Key?

The public portion of the asymmetric key material is generated in AWS KMS and can be used for digital signature verification by calling the “Verify” API, or for public key encryption by calling the “Encrypt” API. The public key can also be used outside of AWS KMS for verification or encryption. You can call the GetPublicKey API to retrieve the public portion of the asymmetric KMS key.

### Q: What is the Size Limit for Data Sent to AWS KMS for Asymmetric Operations?

The size limit is 4 KB. If you want to digitally sign data larger than 4 KB, you have the option to create a message digest of the data and send it to AWS KMS. The digital signature is created over the digest of the data and returned. You specify whether you are sending the full message or a message digest as a parameter in the Sign API request. Any data submitted to the Encrypt, Decrypt, or Re-Encrypt APIs that require use of asymmetric operations must also be less than 4 KB.

### Q: How Can I Distinguish between Asymmetric or Symmetric KMS Keys I Have Created?

In the console, each key will have a new field called Key Type. It will have the value Asymmetric Key or Symmetric Key to indicate the type of key. The DescribeKey API will return a KeyUsage field that will specify if the key can be used to sign, generate HMACs, or encrypt.

### Q: Is Automatic Rotation of Asymmetric or HMAC KMS Keys Supported?

No. Automatic key rotation is not supported for asymmetric or HMAC KMS keys. In general, rotation of asymmetric or HMAC keys can be highly disruptive to your existing workload because you need to retire and replace all instances of keys in which you shared with other parties in the past. If necessary, you can manually rotate them by creating a new KMS key and mapping an existing key alias from the old KMS key to the new KMS key.

### Q: Can a Single Asymmetric KMS Key Be Used for both Encryption and Signing?

No. When creating a KMS key, you must specify whether the key can be used for decrypt or sign operations. An RSA key type can be used for signing or encryption operations, but not both. Elliptic curve key types can be used for only signing operations.

Yes. The request per second rate limits are different for different key types and algorithms. Refer to the [AWS KMS limits](https://docs.aws.amazon.com/kms/latest/developerguide/limits.html) page for details.

### Q: Do Asymmetric Keys Work with AWS KMS Custom Key Stores?

No. You cannot use the custom key store functionality with asymmetric keys.

### Q: Can I Use Asymmetric KMS Keys for Digital Signing Applications that Require Digital Certificates?

Not directly. AWS KMS doesn’t store or associate digital certificates with asymmetric KMS keys it creates. You could choose to have a certificate authority such as AWS Private Certificate Authority issue a certificate for the public portion of your asymmetric KMS key. This will allow the entities that are consuming your public key to verify that the public key indeed belongs to you.

## CloudHSM Backed Key Store

### Q: How Can I Connect AWS KMS to CloudHSM?

The AWS KMS custom key store feature combines the controls provided by [CloudHSM](https://aws.amazon.com/cloudhsm/) with the integration and ease of use of AWS KMS. You can configure your own CloudHSM cluster and authorize AWS KMS to use it as a dedicated key store for your keys rather than the default AWS KMS key store. When you create keys in AWS KMS you can chose to generate the key material in your CloudHSM cluster. KMS keys that are generated in your custom key store never leave the HSMs in the CloudHSM cluster in plaintext and all AWS KMS operations that use those keys are performed in only your HSMs. In all other respects KMS keys stored in your custom key store are consistent with other AWS KMS keys.

Additional guidance for deciding if using a custom key store it is right for you can be found in this [blog](https://aws.amazon.com/blogs/security/are-kms-custom-key-stores-right-for-you/).

### Q: Why Would I Need to Use a CloudHSM?

Since you control your CloudHSM cluster, you have the option to manage the lifecycle of your KMS keys independently of AWS KMS. There are three reasons why you might find a custom key store useful. First, you might have keys that are explicitly required to be protected in a single tenant HSM or in an HSM over which you have direct control. Second, you might need the ability to immediately remove key material from AWS KMS and to prove you have done so by independent means. Third, you might have a requirement to be able to audit all use of your keys independently of AWS KMS or CloudTrail.

### Q: How Does CloudHSM Change the way KMS Keys Are Managed?

There are two differences when managing keys in a custom key store backed by CloudHSM compared to the default AWS KMS key store. You cannot import key material into your custom key store and you cannot have AWS KMS automatically rotate keys. In all other respects, including the type of keys that can be generated, the way that keys use aliases and how policies are defined, keys that are stored in a custom key store are managed in the same way as any other AWS KMS customer managed KMS key.

### Q: Can I Use a CloudHSM to Store an AWS Managed KMS Key?

No, only customer managed KMS keys can be stored and managed in an AWS KMS custom key store backed by CloudHSM. AWS managed KMS keys that are created on your behalf by other AWS services to encrypt your data are always generated and stored in the AWS KMS default key store.

### Q: Does Integration with CloudHSM Affect how Encryption APIs Function in KMS?

No, API requests to AWS KMS to use a KMS key to encrypt and decrypt data are handled in the same way. Authentication and authorization processes operate independently of where the key is stored. All activity using a key in a custom key store backed by CloudHSM is also logged to CloudTrail in the same way. However, the actual cryptographic operations happen exclusively in either the custom key store or the default AWS KMS key store.

### Q: How Can I Audit the Use of Keys in a Custom Key Store?

In addition to the activity that is logged to CloudTrail by AWS KMS, the use of a custom key store provides three further auditing mechanisms. First, CloudHSM also logs all API activity to CloudTrail, such as creating clusters and adding or removing HSMs. Second, each cluster also captures its own local logs to record user and key management activity. Third, each CloudHSM instance copies the local user and key management activity logs to AWS CloudWatch.

### Q: What Impact Does Using CloudHSM Have on Availability of Keys?

The use of an AWS KMS custom key store helps you be responsible for verifying that your keys are available for use by AWS KMS. Errors in configuration of CloudHSM and accidental deletion of key material within a CloudHSM cluster could impact availability. The number of HSMs you use and your choice of Availability Zones (AZs) can also affect the resilience of your cluster. As in any key management system, it is important to understand how the availability of keys can impact the recovery of your encrypted data.

### Q: What Are the Performance Limitations Associated with CloudHSM?

The rate at which keys stored in an AWS KMS custom key store backed by CloudHSM can be used through AWS KMS API calls are lower than for keys stored in the default AWS KMS key store. See the AWS KMS Developer Guide for the current [performance limits.](https://docs.aws.amazon.com/kms/latest/developerguide/limits.html)

### Q: What Are the Costs Associated with Using a Custom Key Store Backed by CloudHSM?

[AWS KMS prices](https://aws.amazon.com/kms/pricing/) are unaffected by the use of a custom key store. However, each custom key store does require that your AWS CloudHSM cluster contains at least two HSMs. These HSMs are charged at the standard [AWS CloudHSM prices](https://aws.amazon.com/cloudhsm/pricing/). There are no additional charges for using a custom key store.

### Q: What Additional Skills and Resources Are Required to Configure CloudHSM?

AWS KMS users that want to use a custom key store will need to set up an [AWS CloudHSM cluster](https://docs.aws.amazon.com/cloudhsm/latest/userguide/create-cluster.html), [add HSMs](https://docs.aws.amazon.com/cloudhsm/latest/userguide/add-remove-hsm.html), [manage HSMs users](https://docs.aws.amazon.com/cloudhsm/latest/userguide/manage-hsm-users.html) and potentially [restore HSMs from backup](https://docs.aws.amazon.com/cloudhsm/latest/userguide/create-cluster-from-backup.html). These are security sensitive tasks and you can verify that you have the appropriate resources and organizational controls in place.

### Q: Can I Import Keys into a Custom Key Store?

No, the ability to import your own key material into an AWS KMS custom key store is not supported. Keys that are stored in a custom key store can only be generated in the HSMs that form your CloudHSM cluster.

### Q: Can I Migrate Keys between the Default AWS KMS Keys Store and a Custom Key Store?

No, the ability to migrate keys between the different types of AWS KMS key store is not currently supported. All keys must be created in the key store in which they will be used, except in situations where you import you own key material into the default AWS KMS key store.

### Q: Can I Rotate Keys Stored in a Custom Key Store?

The ability to automatically rotate key material in an AWS KMS custom key store is not supported. Key rotation must be performed manually by creating new keys and re-mapping AWS KMS key aliases used by your application code to use the new keys for future encryption operations.

### Q: Can I Use My CloudHSM Cluster for other Applications?

Yes, AWS KMS does not require exclusive access to your CloudHSM cluster. If you already have a cluster you can use it as a custom key store and continue to use it for your other applications. However, if your cluster is supporting high, non-AWS KMS, workloads you may experience reduced throughput for operations using KMS keys in your custom key store. Similarly, a high AWS KMS request rate to your custom key store could impact your other applications.

### Q: How Can I Learn More about AWS CloudHSM?

## External Key Store

### Q: What is an External Key Store (XKS)?

An external key store is a custom key store backed by an external key management infrastructure that you own and manage outside of AWS. All encryption or decryption operations that use a KMS key in an external key store are performed in your key manager with cryptographic keys and operations that are under your control and are physically inaccessible to AWS.

### Q: Why Would I Use an External Key Store?

XKS can help you comply with rules or regulations that require encryption keys to be stored and used outside of AWS under your control.

### Q: How Does AWS KMS Connect to My External Key Manager?

Requests to AWS KMS from integrated AWS services on your behalf or from your own applications are forwarded to a component in your network called an XKS Proxy. The XKS Proxy is an open source API specification that helps you and your key management vendor build a service that accepts these requests and forwards them to your key management infrastructure to use its keys for encryption and decryption.

### Q: Which External Vendors Support the XKS Proxy Specification?

Thales, Entrust, Atos, Fortanix, DuoKey, Securonix, Utimaco, Salesforce, T-Systems, and HashiCorp have solutions that integrate with the XKS Proxy specification. For information about availability, pricing, and how to use solutions from these vendors, see their respective documentation. We encourage you and your key management infrastructure partner to leverage the open source XKS Proxy specification to build a solution that meets your needs. The API specification for XKS Proxy is published [here](https://github.com/aws/aws-kms-xksproxy-api-spec/).

### Q: Which AWS KMS Features Support External Keys?

External keys support the following symmetric encryption operations: Encrypt, ReEncrypt, Decrypt, and GenerateDataKey.

### Q: How Does XKS Work with AWS Services that Integrate with AWS KMS for Data Encryption?

You can use XKS keys to encrypt data in any AWS service that integrates with AWS KMS using customer managed keys. See the list of supported services here. AWS services call the AWS KMS GenerateDataKey API to request a unique plaintext data key to encrypt your data. The plaintext data key is returned to the service along with an encrypted copy of the data key to be stored alongside your encrypted data. To produce the encrypted copy of the data key, the plaintext data key is first encrypted by a key stored in AWS KMS unique to your AWS account. This encrypted data key is then forwarded to your XKS Proxy implementation connected to your external key manager to be encrypted a second time under the key you define in your external key manager. The resulting double-encrypted data key is returned in the response to the GenerateDataKey API request.

### Q: What is Double Encryption and how Does it Work?

The network connection between AWS KMS, your XKS Proxy implementation, and your external key manager should be protected with a point-to-point encryption protocol like TLS. However, in order to protect your data leaving AWS KMS until it reaches your external key manager, AWS KMS ﬁrst encrypts it with an internally managed KMS key in your account speciﬁc to each KMS key defined in your external key store. The resulting ciphertext is forwarded to your external key manager, which encrypts it using the key in your external key manager. Double encryption provides the security control that no ciphertext can ever be decrypted without using the key material in your external key manager. It also provides the security control that the ciphertext leaving the AWS network is encrypted using the FIPS 140 certiﬁed AWS KMS HSMs. Because your external key manager must be used to decrypt data, if you revoke access to AWS KMS, your underlying encrypted data becomes is inaccessible.

### Q: Can I Use XKS Keys in My Own Applications that Implement Client-side Encryption?

Yes. XKS keys can also be used from within your own applications when using a client-side symmetric encryption solution that uses AWS KMS as its key provider. AWS open source client-side encryption solutions like the AWS Encryption SDK, S3 Encryption Client and DynamoDB Encryption Client support XKS keys.

### Q: I’ve Already Been Using AWS KMS with Standard KMS Keys, Imported KMS Keys, or Keys Stored in My CloudHSM Cluster. Can I Migrate These KMS Keys to XKS or Re-encrypt Existing Encrypted under XKS Keys?

All XKS keys must be created as new keys in KMS. You cannot migrate existing KMS keys into XKS keys hosted in your external key manager.

You can re-encrypt existing data under newly generated XKS keys, assuming the AWS service or your own application supports the action. Many AWS services will help you copy an encrypted resource and designate a new KMS key to use to encrypt the copy. You can configure the XKS key in the COPY command provided by the AWS service. You can re-encrypt client-side encrypted data in your own applications by calling the KMS ReEncrypt API and configuring the XKS key.

### Q: How is XKS Priced in KMS?

Like all customer managed keys, XKS keys are priced at $1 per month per key until they are deleted. Requests under XKS keys are charged at the same rate as any other AWS KMS symmetric key. Learn more about pricing on the AWS KMS pricing page.

### Q: Is Automatic Key Rotation Possible with XKS Keys?

Yes. Automatic key rotation is supported by the XKS specification, and it is a capability provided by most vendors that support XKS. Automatic rotation for XKS keys occurs entirely in the external key manager and works in a similar way to the automatic key rotation for AWS KMS keys created and managed within KMS. When you use a rotated KMS XKS key to encrypt data, your external key manager uses the current key material. When you use the rotated XKS key to decrypt ciphertext, your external key manager uses the version of the key material that was used to encrypt it. As long as previous XKS keys used to create earlier ciphertexts are still enabled in external key manager, you will be able to successfully make Decrypt API request under those versions of you XKS keys.

### Q: If I Disable, Block, or Delete Keys in the External Key Store, where Will My Data Still Be Accessible in the Cloud?

For services that do not cache keys, the next API call using this XKS KMS key will fail. Some services implement data key caching or other key derivation schemes for performance, latency, or KMS cost management. Caching of these keys can vary from 5 mins to 24 hrs. Any protected resource that is currently in use (such as RDS database or EC2 instance) will respond differently after you deny access to the key. See the relevant AWS service documentation for details.

### Q: How Do I Authenticate XKS Proxy Requests from AWS KMS to My External Key Manager?

To authenticate to your external key store proxy, AWS KMS signs all requests to the proxy using AWS SigV4 credentials that you configure on your proxy and provide to KMS. AWS KMS authenticates your external key store proxy using server-side TLS certificates. Optionally, your proxy can enable mutual TLS for additional assurance that it only accepts requests from AWS KMS.

### Q: What Types of Authorization Policies Can I Build for XKS Keys?

All of the usual AWS KMS authorization mechanisms — IAM policies, AWS KMS key policies, grants — that you use with other KMS keys, work the same way for KMS keys in external key stores.

In addition, your and/or your external key manager partners have the ability to implement a secondary layer of authorization controls based on request metadata included with each request sent from AWS KMS to the XKS Proxy. This metadata includes the calling AWS user/role, the KMS key ARN, and the specific KMS API that was requested. This allows you to apply fine-grained authorization policy on the use of a key in your external key manager beyond simply trusting any request from AWS KMS. The choice of policy enforcement using these request attributes are left to your individual XKS Proxy implementations.

### Q: How Does Logging and Auditing Work with XKS?

The unique ID generated for every request coming to AWS KMS involving XKS keys is also forwarded to the XKS proxy. You can use the log data (if available) from your XKS proxy or external key manager to reconcile requests made to AWS KMS with the ones made to your external key manager. This feature allows you to verify that all requests to use keys in your external key manager originated from a call you initiated to AWS KMS either directly or through an integrated AWS service.

### Q: What Risks Do I Accept if I Choose XKS instead of Using Standard KMS Keys Generated and Stored in AWS KMS?

**Availability risk:** You are responsible for the availability of the XKS Proxy and external key material. This system must have high availability to verify that whenever you need an XKS key to decrypt an encrypted resource or encrypt new data, AWS KMS can successfully connect to the XKS proxy, which itself can connect to your external key manager to complete the necessary cryptographic operation using the key. For example, suppose you encrypted an EBS volume using an XKS key and now you want to launch an EC2 instance and attach that encrypted volume. The EC2 service will pass the unique encrypted data key for that volume to AWS KMS to decrypt it so it can be provisioned in volatile memory of the Nitro card in order to decrypt and encrypt read/write operations to the volume. If your XKS Proxy or external key manager isn’t available to decrypt the volume key, your EC2 instance will fail to launch. In these types of failures, AWS KMS returns a KMSInvalidStateException stating that the XKS Proxy is not available. It is now up to you to determine why your XKS Proxy and key manager is unavailable based on the error messages provided by KMS.

**Durability risk:** Because keys are under your control in systems outside of AWS, you are solely responsible for the durability of all external keys you create. If the external key for a XKS key is permanently lost or deleted, all ciphertext encrypted under the XKS key is unrecoverable.

**Performance risk:** You are responsible for verifying that your XKS Proxy and external key store infrastructure is designed with sufficient performance characteristics to meet your needs. Since every request using XKS keys requires a connection to your external key store, your XKS proxy can become a bottleneck if the request rate from AWS KMS exceeds the request rate your XKS Proxy or external key manager can support. Also, if the elapsed time of a single request (including one retry) from AWS KMS to your XKS Proxy takes more than 500ms\*, AWS KMS will return a 400 error to its calling client, effectively communicating that your XKS key is unavailable and the calling client should not retry. This behavior is designed to minimize the risk of upstream AWS services or your own applications having to react to sporadic excessive latency caused by connectivity issues to your infrastructure.

\*AWS KMS will attempt a single retry for any request that takes 250ms. If the retry request also takes more than 250ms, a 400 error will be returned to the calling client.

### Q: What Are the Service Level Availability (SLA) Impacts of Using the External Key Store?

Because AWS cannot control the end-to-end availability of the connection between AWS KMS and your external key store infrastructure, we specifically exclude the use of XKS in [our public KMS availability SLA](https://aws.amazon.com/kms/sla/). Also, XKS keys are excluded in the availability SLA for any AWS service in which an XKS key is configured by you to encrypt data within the service.
