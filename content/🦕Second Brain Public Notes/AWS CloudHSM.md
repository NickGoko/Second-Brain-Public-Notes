---
tags:
  - cloud/aws
---
## I. What is AWS CloudHSM?

[AWS CloudHSM](https://aws.amazon.com/cloudhsm/) <mark style="background: #ADCCFFA6;">is a cloud-based hardware security module that provides secure cryptographic key storage and operations within a tamper-resistant hardware device.</mark> This service helps you meet corporate, contractual, and regulatory compliance requirements for data security by using FIPS 140-2 Level 3 validated HSMs.

## II. AWS CloudHSM Features and Advantages

### A. Secure Key Storage

AWS CloudHSM allows you to generate, store, and manage cryptographic keys securely.

### B. FIPS 140-2 Level 3 Compliance

The service meets [high compliance standards](https://en.wikipedia.org/wiki/FIPS_140-2), ensuring your data’s security.

### C. Scalability

AWS CloudHSM is fully scalable, allowing you to increase capacity as needed.

### D. Flexibility

It supports multiple APIs, including [PKCS#11](https://www.ibm.com/docs/en/linux-on-systems?topic=introduction-what-is-pkcs-11), [Java Cryptography Extensions (JCE)](https://www.oracle.com/java/technologies/javase-jce-all-downloads.html), and [Microsoft CryptoNG (CNG)](https://learn.microsoft.com/en-us/windows/win32/seccng/cng-portal) libraries.

### E. Control and Independence

Users have exclusive, single-tenant access to each HSM in their cluster.

## III. AWS CloudHSM Monitoring

AWS CloudHSM integrates with [AWS CloudTrail](https://aws.amazon.com/cloudtrail/) and [Amazon CloudWatch](https://aws.amazon.com/cloudwatch/). CloudTrail records API calls for your account, while CloudWatch allows you to collect and track metrics, collect and monitor log files, set alarms, and automatically react to changes in your AWS resources.

## IV. AWS CloudHSM Pricing

![AWS CloudHSM Pricing Table](https://digitalcloud.training/wp-content/uploads/2023/05/AWS-CloudHSM-Pricing-Table-1024x219.png)

Please note, the actual costs can vary based on different regions and specific usage patterns. Always refer to the official [AWS Pricing page](https://aws.amazon.com/pricing/?nc2=h_ql_pr_ln&aws-products-pricing.sort-by=item.additionalFields.productNameLowercase&aws-products-pricing.sort-order=asc&awsf.Free%20Tier%20Type=*all&awsf.tech-category=*all) for the most accurate and up-to-date information.

## V. AWS CloudHSM Use Cases

### A. Protect Private Keys for an Issuing CA

AWS CloudHSM can securely generate and store the private key of a root or intermediate CA, reducing the risk of unauthorized access.

### B. Offload SSL Processing for Web Servers

The service can offload SSL/TLS processing from web servers, improving website performance.

### C. Encrypt Data at Rest

AWS CloudHSM enables the encryption of data at rest, providing an additional layer of protection for sensitive data.

## VI. AWS CloudHSM FAQs

### A. What is the Difference between AWS KMS and AWS CloudHSM?

![AWS KMS and AWS CloudHSM Comparison Table](https://digitalcloud.training/wp-content/uploads/2023/05/AWS-KMS-and-AWS-CloudHSM-Comparison-Table-1024x403.png)

### B. When Should I Use AWS CloudHSM instead of AWS KMS?

AWS CloudHSM is recommended when you need to control and manage your own encryption keys in single-tenant hardware, or when you have compliance requirements that cannot be met by AWS KMS.

### C. What Level of compliance is CloudHSM?

AWS CloudHSM is compliant with FIPS 140-2 Level 3, one of the highest levels of compliance for data security. This signifies that it meets stringent requirements for physical tamper-resistance, role-based access control, and ability to zeroize all plaintext cryptographic keys and critical security parameters within the module. This level of certification provides assurance that CloudHSM is designed to prevent unauthorized physical and logical access to cryptographic keys, making it suitable for handling sensitive data.

## VII. Conclusion

AWS CloudHSM offers a robust platform that enables organizations to generate, store, and manage encryption keys securely in the cloud. The service’s flexibility comes from its support for various APIs and its scalability from the ability to increase capacity on-demand. With its high compliance standards, including FIPS 140-2 Level 3, it ensures stringent security for cryptographic operations. As such, businesses seeking a solution for securely managing cryptographic keys, while maintaining control and meeting compliance requirements, will find AWS CloudHSM to be a highly suitable service.

# FAQ
**Q: What is AWS CloudHSM?**

The AWS CloudHSM service helps you meet corporate, contractual, and regulatory compliance requirements for data security by using dedicated Hardware Security Module (HSM) instances within the AWS cloud. AWS and AWS Marketplace partners offer a variety of solutions for protecting sensitive data within the AWS platform, but for some applications and data subject to contractual or regulatory mandates for managing cryptographic keys, additional protection may be necessary. CloudHSM complements existing data protection solutions and allows you to protect your encryption keys within HSMs that are designed and validated to government standards for secure key management. CloudHSM allows you to securely generate, store, and manage cryptographic keys used for data encryption in a way that keys are accessible only by you.

**Q: What is a Hardware Security Module (HSM)?**

A Hardware Security Module (HSM) provides secure key storage and cryptographic operations within a tamper-resistant hardware device. HSMs are designed to securely store cryptographic key material and use the key material without exposing it outside the cryptographic boundary of the hardware.

**Q: What can I do with CloudHSM?**

You can use the CloudHSM service to support a variety of use cases and applications, such as database encryption, Digital Rights Management (DRM), Public Key Infrastructure (PKI), authentication and authorization, document signing, and transaction processing.

**Q: How does CloudHSM work?**

When you use the AWS CloudHSM service you create a CloudHSM Cluster. Clusters can contain multiple HSMs, spread across multiple Availability Zones in a region. HSMs in a cluster are automatically synchronized and load-balanced. You receive dedicated, single-tenant access to each HSM in your cluster. Each HSM appears as a network resource in your Amazon Virtual Private Cloud (VPC). Adding and removing HSMs from your Cluster is a single call to the AWS CloudHSM API (or on the command line using the AWS CLI). After creating and initializing a CloudHSM Cluster, you can configure a client on your EC2 instance that allows your applications to use the cluster over a secure, authenticated network connection.

The service automatically monitors the health of your HSMs, but no AWS personnel have access to your keys or data. Your applications use standard cryptographic APIs, in conjunction with HSM client software installed on the application instance, to send cryptographic requests to the HSM. The client software maintains a secure channel to all of the HSMs in your cluster and sends requests on this channel, and the HSM performs the operations and returns the results over the secure channel. The client then returns the result to the application through the cryptographic API.

**Q: I don’t currently have a VPC. Can I still use AWS CloudHSM?**

No. To protect and isolate your AWS CloudHSM from other Amazon customers, CloudHSM must be provisioned inside an Amazon VPC. Creating a VPC is easy. Please see the [VPC Getting Started Guide](http://docs.aws.amazon.com/AmazonVPC/latest/GettingStartedGuide/ExerciseOverview.html) for more information.

**Q: Does my application need to reside in the same VPC as the CloudHSM Cluster?**

No, but the server or instance on which your application and the HSM client are running must have network (IP) reachability to all HSMs in the cluster. You can establish network connectivity from your application to the HSM in many ways, including operating your application in the same VPC, with VPC peering, with a VPN connection, or with Direct Connect. Please see the [VPC Peering Guide](http://docs.aws.amazon.com/AmazonVPC/latest/UserGuide/vpc-peering.html) and [VPC User Guide](http://docs.aws.amazon.com/AmazonVPC/latest/UserGuide) for more details.

**Q: Does CloudHSM work with on-premises HSMs?**

Yes. While CloudHSM does not interoperate directly with on-premises HSMs, you can securely transfer exportable keys between CloudHSM and most commercial HSMs using one of several supported RSA key wrap methods.   

**Q: How can my application use CloudHSM?**

We have integrated and tested CloudHSM with a number of third-party software solutions such as Oracle Database 11g and 12c and Web servers including Apache and Nginx for SSL offload. Please see the [CloudHSM User Guide](https://docs.aws.amazon.com/cloudhsm/latest/userguide/) for more information.

If you are developing your own custom application, your application can use the standard APIs supported by CloudHSM, including PKCS#11 and Java JCA/JCE (Java Cryptography Architecture/Java Cryptography Extensions), or Microsoft CAPI/CNG. Please refer to the [CloudHSM User Guide](https://docs.aws.amazon.com/cloudhsm/latest/userguide/) for code samples and help with getting started.

If you are moving an existing workload from CloudHSM Classic or on-premises HSMs to CloudHSM, our [CloudHSM migration guide](https://s3.amazonaws.com/cloudhsmv2-software/CloudHsmClient/Docs/CloudHSMUpgradeGuide-latest.pdf) provides information on how to plan and execute your migration.  

**Q: Can I use CloudHSM to store keys or encrypt data used by other AWS services?**

Yes. You can do all encryption in your CloudHSM-integrated application. In this case, AWS services such as Amazon S3 or Amazon Elastic Block Store (EBS) would only see your data encrypted.

**Q: Can other AWS services use CloudHSM to store and manage keys?**

AWS services integrate with AWS Key Management Service, which in turn is integrated with AWS CloudHSM through the KMS custom key store feature. If you want to use the server-side encryption offered by many AWS services (such as EBS, S3, or Amazon RDS), you can do so by configuring a custom key store in AWS KMS.  

**Q: Can CloudHSM be used to perform personal identification number (PIN) block translation or other cryptographic operations used with debit payment transactions**?

Currently, CloudHSM provides general-purpose HSMs. Over time we may provide payment functions. If this is of interest to you, please [let us know](https://pages.awscloud.com/cloudHSM-contact-us.html).

**Q: How do I get started with CloudHSM?**

You can provision a CloudHSM Cluster in the CloudHSM Console, or with a few API calls through the AWS SDK or API. To learn more, please see the [CloudHSM User Guide](https://docs.aws.amazon.com/cloudhsm/latest/userguide/) for information about getting started, the [CloudHSM Documentation](https://aws.amazon.com/documentation/cloudhsm/) for information about the CloudHSM API, or the Tools for Amazon Web Services page for more information about the SDK.

**Q: How do I terminate CloudHSM service?**

You can use the CloudHSM console, API, or SDK to delete your HSMs and stop using the service. Please refer to the [CloudHSM User Guide](https://docs.aws.amazon.com/cloudhsm/latest/userguide/) for further instructions.