---
tags:
  - cloud/aws
---

![[AWS Solutions Architect Skillbuilder#AWS Snowball]]

![[AWS Solutions Architect Skillbuilder#AWS Snowball Overview]]


![[AWS Solutions Architect Skillbuilder#AWS Snowball Edge Features]]

![[AWS Solutions Architect Skillbuilder#AWS Snowball Edge Use Cases]]


# FAQ
## General

**Q: What is AWS Snowball?**

AWS Snowball is a service that provides secure, rugged devices, so you can bring AWS computing and storage capabilities to your edge environments, and transfer data into and out of AWS. Those rugged devices are commonly referred to as AWS Snowball or AWS Snowball Edge devices. Previously, AWS Snowball referred specifically to an early hardware version of these devices, however that model has been replaced by updated hardware. Now the AWS Snowball service operates with Snowball Edge devices, which include on-board computing capabilities as well as storage.  

**Q: What is AWS Snowball Edge?**

AWS Snowball Edge is an edge computing and data transfer device provided by the AWS Snowball service. It has on-board storage and compute power that provides select AWS services for use in edge locations. Snowball Edge comes in two options, Storage Optimized and Compute Optimized, to support local data processing and collection in disconnected environments such as ships, windmills, and remote factories. Learn more about its [features here](https://aws.amazon.com/snowball/features/).

**Q: What happened with the original 50 TB and 80 TB AWS Snowball devices?**

The original Snowball devices were transitioned out of service and Snowball Edge Storage Optimized are now the primary devices used for data transfer.

**Q: Can I still order the original Snowball 50 TB and 80 TB devices?**

No. For data transfer needs now, please select the Snowball Edge Storage Optimized 80TB or 210TB devices.  

**Q: How does Snowball Edge work?**

You start by requesting one or more Snowball Edge Compute Optimized or Snowball Edge Storage Optimized devices in the AWS Management Console based on how much data you need to transfer and the compute needed for local processing. The buckets, data, Amazon EC2 AMIs, and Lambda functions you select are automatically configured, encrypted, and preinstalled on your devices before they are shipped to you. Once a device arrives, you connect it to your local network and set the IP address either manually or automatically with DHCP. Then use the Snowball Edge client software, job manifest, and unlock code to verify the integrity of the Snowball Edge device or cluster, and unlock it for use. The manifest and unlock code are uniquely generated and crypto-logically bound to your account and the Snowball Edge shipped to you, and cannot be used with any other devices. Data copied to Snowball Edge is automatically encrypted and stored in the buckets you specify.

All logistics and shipping is done by Amazon, so when copying is complete and the device is ready to be returned, the E Ink shipping label will automatically update the return address, ensuring that the Snowball Edge device is delivered to the correct AWS facility. Once the device ships, you can receive tracking status via messages sent by Amazon Simple Notification Service (Amazon SNS), generated texts and emails, or directly from the console.

All of the management for your Snowball Edge resources can be performed in the AWS management console and these operations require system engineers.

**Q: What is the difference between Snowball Edge and Snowball?**

AWS Snowball now refers to the service overall, and Snowball Edge are the current types of devices that the service uses – sometimes referred to generically as AWS Snowball devices. Originally, early Snowball hardware designs were for data transport only. Snowball Edge has the additional capability to run computing locally, even when there is no network connection available.

**Q: What is the difference between the Snowball Edge Storage Optimized and Snowball Edge Compute Optimized options?**

Snowball Edge Storage Optimized is the optimal choice if you need to securely and quickly transfer dozens of terabytes to petabytes of data to AWS. It is also a good fit for running general purpose analysis such as IoT data aggregation and transformation. It provides up to 80TB, or 210TB of storage and 10Gb, 40Gb, or 100Gb network connectivity to address large scale data transfer and pre-processing use cases. We recommend using Snowball Edge Compute Optimized for use cases that require access to powerful compute and high-speed storage for data processing before transferring it into AWS. It features 104 vCPUs, 28 TB of NVMe SSD, and up to 100 Gb networking to run applications such as high-resolution video processing, advanced IoT data analytics, and real-time optimization of machine learning models in environments with limited connectivity. For more details, see the [documentation](https://docs.aws.amazon.com/snowball/latest/developer-guide/device-differences.html).

**Q: Who should use Snowball Edge?**

Consider Snowball Edge if you need to run computing in rugged, austere, mobile, or disconnected (or intermittently connected) environments. Also consider it for large-scale data transfers and migrations when bandwidth is not available for use of a high-speed online transfer service, such as AWS DataSync.  
  
Snowball Edge Storage Optimized is the optimal data transfer choice if you need to securely and quickly transfer terabytes to petabytes of data to AWS. You can use Snowball Edge Storage Optimized if you have a large backlog of data to transfer or if you frequently collect data that needs to be transferred to AWS and your storage is in an area where high-bandwidth internet connections are not available or cost-prohibitive.  
  
You can also use Snowball Edge to run edge computing workloads, such as performing local analysis of data on a Snowball Edge cluster and writing it to the Amazon S3 compatible endpoint. You can streamline it into existing workflows leveraging built-in capabilities such as the NFS file interface and migrate files to the device while maintaining file metadata.

Snowball Edge can operate in remote locations or harsh operating environments, such as factory floors, oil and gas rigs, mining sites, hospitals, and on moving vehicles. Snowball Edge is pre-configured and does not have to be connected to the internet, so processing and data collection can take place within isolated operating environments. Snowball Edge allows you to run the same software at the edge and access select AWS capabilities as you would with full connectivity to AWS.

**Q. Can I use Snowball Edge to migrate data from one AWS Region to another AWS Region?**

No. Snowball Edge is intended to serve as a data transport solution for moving high volumes of data into and out of a designated AWS Region. For use cases that require data transfer between AWS Regions, we recommend using S3 Cross-Region Replication as an alternative.

**Q: How much data can I transfer using Snowball Edge?**

You can transfer virtually any amount of data with Snowball Edge, from a few terabytes to many petabytes. You can transfer up to approximately 80 TB with a single Snowball Edge Storage Optimized device and can transfer even larger data sets with multiple devices, either in parallel, or sequentially.

**Q: How long does it take to transfer my data?**

Data transfer speed is affected by a number of factors including local network speed, file size, and the speed at which data can be read from your local servers. The end-to-end time to transfer up to 80 TB of data into AWS with Snowball Edge is approximately one week, including the usual shipping and handling time in AWS data centers.

**Q: How long can I have a Snowball Edge for a specific job?**

For security purposes, jobs using an AWS Snowball Edge device must be completed within 360 days of being prepared. If you need to keep one or more devices for longer than 360 days, contact AWS Support. Otherwise, after 360 days, the device becomes locked, can no longer be accessed, and must be returned. If the AWS Snowball Edge device becomes locked during an import job, we can still transfer the existing data on the device into Amazon S3.

**Q: What are the specifications of the Snowball Edge devices?**

Please see the [AWS Snowball Features page](https://aws.amazon.com/snowball-edge/features/) for feature details and the [Snowball Edge documentation page](https://docs.aws.amazon.com/snowball/latest/developer-guide/getting-started.html) for a complete list of hardware specs, including network connections, thermal and power requirements, decibel output, and dimensions.

**Q: What network interfaces does Snowball Edge support?**

Snowball Edge Storage Optimized for data transfer devices have two 10G RJ45 ports, one 10/25G SFP28 port, and one 40G/100G QSFP28 port.  
  
Snowball Edge Storage Optimized for edge compute devices have one 10G RJ45 port, one 10/25G SFP28 port, and one 40G QSFP+ port.  

The Snowball Edge Compute Optimized devices (including the GPU option) have two 10G RJ45 ports, one 10/25G SFP28 port, and one 40G/100G QSFP28 port.  

**Q: What is the Snowball Edge default shipping option? Can I choose expedited shipping?**

As a default, Snowball Edge uses two-day shipping by UPS. You can choose expedited shipping if your jobs are time-sensitive.  

## Edge Computing Capabilities

**Q: Does Snowball Edge support EC2 instances?**

Yes. The Snowball Edge Storage Optimized option supports SBE1 instance.  
  
The Snowball Edge Compute Optimized option features more powerful and larger instances, sbe-c for compute-intensive applications.  
  
The Snowball Edge Compute Optimized device with an optional GPU, can use sbe-g instances to accelerate your application’s performance.  
  
The support for EC2-compatible instances on Snowball Edge devices enables you to build and test on EC2, then operate your AMI on a Snowball Edge to address workloads that sit in remote or disconnected locations.

**Q: How can I use the GPU with AWS Snowball Edge’s SBE instances?**

The GPU option on AWS Snowball Edge Compute Optimized comes with SBE-G instances that can take advantage of the onboard GPU for accelerating the application performance. After receiving the device, select the option to use the SBE-G instance in order to use the on-board GPU with your application.

**Q: When should I use the EC2 compatible instances on AWS Snowball Edge?**

You should use the EC2 compatible instances when you have an application running on the edge that is managed and deployed as a virtual machine (an Amazon Machine Image, or AMI).

**Q: Can multiple Snowball Edge devices be used for highly available storage?**  

Yes, multiple Snowball Edge Compute Optimized devices can be clustered into a larger durable storage pool with a single Amazon S3 compatible endpoint. For example, if you have 16 Compute Optimized devices, they can be configured to be a single cluster that exposes S3 compatible endpoints with 500 TB of storage. Alternatively, they can be used individually without clustering, each hosting a separate S3 compatible endpoint with 31 TB of usable storage. A durable cluster cannot be created with Amazon S3 compatible storage using Snowball Edge Compute Optimized devices.  

**Q: When would I consider creating a storage cluster?**

With a Snowball Edge storage cluster, you increase local storage durability and scalability. Storage clustering creates durable, scalable, S3 compatible local storage. AWS Snowball Edge storage clusters allow you to scale your local storage capacity up or down depending on your requirements by adding or removing appliances, eliminating the need to buy expensive hardware.  

**Q: How do I get started with local computing on Snowball Edge?**

You can enable EKS-A for modern distributed container based applications, and Amazon EC2 AMIs or Lambda functions during AWS Snowball Edge job creation using either the AWS Console, AWS Snowball SDK, or AWS CLI.  

**Q: Can I use existing Amazon EC2 APIs to start, stop, and manage instances on the device?**

Yes. AWS Snowball Edge provides an Amazon EC2-compatible endpoint that can be used to start, stop, and manage your instances on AWS Snowball Edge. This endpoint is compatible with the AWS CLI and AWS SDK.

**Q: What Amazon EC2 features does AWS Snowball Edge support?**

The Amazon EC2 endpoint running on AWS Snowball Edge, provides a set of EC2 features that customers would find most useful for edge computing scenarios. This includes APIs to run, terminate, and describe your installed AMIs and running instances. Snowball Edge also supports block storage for EC2 images, which is managed using a set of the Amazon EBS API commands.

**Q: Can I use an existing Amazon EBS volume with AWS Snowball Edge?**

No. At this time, you cannot use an existing EBS volume with AWS Snowball Edge, however, Snowball Edge does offer block storage volumes, which are managed with an EBS-compatible API.

**Q: What steps do I need to take to run Amazon EC2 instances on AWS Snowball Edge?**

To run instances, provide the AMI IDs during job creation and the images come pre-installed when the device is shipped to you.

**Q: Can I convert my images from other hypervisors to AMIs and vice versa?**

Yes. You can import or export your KVM/VMware images to AMIs using the EC2 VM Import/Export service. Refer to the [VM Import/Export documentation](https://aws.amazon.com/ec2/vm-import/) for more details.

This is necessary in order to run licensed software, including operating systems other than those which the AWS Snowball service provides.

**Q: What operating systems can I run using this feature?**

Amazon EC2 on Snowball Edge provides default support for a variety of free-to-use operating systems (OS) like Ubuntu and CentOS. They will appear as AMI’s that can be loaded onto Snowball Edge without any modification. To run other OSes that require licenses on Snowball Edge EC2 instances, you must provide your own license, and then export the AMI using [Amazon EC2 VM Import/Export (VMIE)](https://docs.aws.amazon.com/vm-import/latest/userguide/what-is-vmimport.html).

**Q: What kind of workloads can I run on sbe-c instances?**

sbe-c instances feature up to 104 vCPUs, ephemeral instance storage for root volumes, and 418GB of memory for running a wide variety of compute-intensive applications, such as advanced machine learning, full motion video analysis, LAMP stacks, and EC2-hosted containers, in environments with little or no internet connectivity. SBE-C instances can also use Snowball Edge NVMe SSD and HDD block storage for persistent volumes.  

**Q: How do I ensure that my AMIs are compatible to run on EC2-compatible instances on AWS Snowball Edge?**

AMIs that run on the C5 instance type in AWS are compatible with SBE1 instances available on AWS Snowball Edge Storage Optimized in the vast majority of cases. We recommend that you first test your applications in the C5 instance type to ensure they can be run on the Snowball Edge Storage Optimized device.

AMIs that run on the M5a instance type in AWS are compatible with SBE-C instances available on AWS Snowball Edge Compute Optimized in the vast majority of cases. For SBE-C instances running on the AWS Snowball Edge Compute Optimized device, we recommend you test your applications on the M5a instance type.

For SBE-G instance types for the Snowball Edge Compute Optimized with the GPU option, we recommend you first test your applications against the EC2 P3 instance types.

**Q: Can I install more than one instance on a device?**

Yes. You can run multiple instances on a device as long as the total resources used across all instances are within the [limits for your Snowball Edge device](https://docs.aws.amazon.com/snowball/latest/developer-guide/ec2-edge-limits.html).

**Q: How do I use sbe-c and sbe-g instances on an AWS Snowball Edge cluster?**

All the EC2 compatible instances can run on each node of an AWS Snowball Edge cluster. When you provision an AWS Snowball Edge cluster using the AWS Console, you can provide details for instances to run on each node of the cluster, for example, the AMI you want to run and the instance type and size you want to use. Nodes can use the same or different AMIs across each node in a cluster.  
  
**Q: How do I launch an instance manually?**

Each AMI has an AMI ID associated with it. You can use run-instance command to start the instance by providing this ID. Running this command returns an instance-id value that can be used to manage this instance.

**Q: How do I manage the instances on AWS Snowball Edge?**

You can check the status of all the images that are installed on the device using the describe-images command. To see the active instances of instances running on the device, you can use the describe-instance-status command.

**Q: How do I terminate an existing instance?**

You can terminate a running instance using the terminate-instance command.

**Q: How are my AMIs protected while in transit?**

Snowball Edge encrypts all data, including AMIs, with 256-bit encryption. You manage your encryption keys by using the [AWS Key Management Service](https://aws.amazon.com/kms/) (KMS). Your keys are never stored on the device and you need both the keys and an unlock code to use the device on-premises. In addition to using a tamper-evident enclosure, Snowball Edge uses industry-standard Trusted Platform Modules (TPM) designed to detect any unauthorized modifications to the hardware, firmware, or software. AWS visually and cryptographically inspects every device for any signs of tampering.

**Q: Can I add AMIs to my Snowball Edge device after it has been deployed?**  
  
Yes. You can import virtual machine (VM) images as AMIs to your Snow device while it is onsite. For more information about importing VM images into Snow devices, see the [Snowball Edge documentation](https://docs.aws.amazon.com/snowball/latest/developer-guide/whatisedge.html).

**Q: How is software licensing handled with compute instances on AWS Snowball Edge?**

You are responsible for licensing any software that you run on your instance. Specifically, for Windows operating systems, you can bring your existing license to the running instances on the device, by installing the licensed OS in your AMI in EC2, and then using [VM Import/Export](https://docs.aws.amazon.com/vm-import/latest/userguide/what-is-vmimport.html) to load the AMI to your Snowball Edge device.

**Q: How do I get started with the latest AWS IoT Greengrass on Snow devices?** 

AWS IoT Greengrass is an IoT edge runtime (open source starting with version 2.0) and a cloud service that helps you build, deploy and manage IoT applications on your devices. AWS Snow devices running AWS IoT Greengrass can operate as an IoT hub, data aggregation point, application monitor, or a lightweight analytics engine. 

To get started with AWS IoT Greengrass on an AWS Snow device follow the steps listed below:

1. When you are ready to place your job order on the AWS Snow Family console, you can opt-in to install the AWS IoT Greengrass AMI, which uses Amazon Linux 2 (AL2) AMI for the AWS Snow Family on the Snow device of your choice.
2. Once you receive the device, you can use AWS OpsHub for Snow Family to unlock the device with the credentials provided after the job is created.         
3. After the device is powered on and unlocked, you can launch the AL2 AMI for AWS Snow Family on the applicable Snow device and remotely log in to it using your existing SSH keys or by creating new SSH keys.
4. Now you are ready to install the latest version AWS IoT Greengrass on the Snow device following the instructions [here](https://docs.aws.amazon.com/greengrass/v2/developerguide/getting-started.html).         
    
5. Once the installation is complete, you will be able to manage the AWS Snow Family device and deploy IoT workloads from the AWS IoT console. 

**Q: Does Snowball Edge support Kubernetes?  
  
**

Snowball Edge supports EKS Anywhere, which allows you to easily create and operate Kubernetes clusters on Snowball Edge devices.  

**Q: Which devices are supported for Amazon EKS Anywhere on Snow?  
  
**

EKS Anywhere on Snow is supported on AWS Snowball Edge Compute Optimized devices.  

## Block Storage for Amazon EC2 on Snowball Edge

**Q: What is block storage on AWS Snowball Edge?**

You can run block storage on both Snowball Edge Compute Optimized and Snowball Edge Storage Optimized devices. You attach block storage volumes to EC2 instances using a subset of Amazon EBS capabilities that enable you to configure and manage volumes for EC2 instances on Snowball Edge devices.

**Q: Why should I use AWS Snowball Edge block storage?** 

Snowball Edge block storage enables you to have multiple persistent block storage volumes – in addition to your root volume – for your Amazon EC2 based applications on the device. This can provide higher performance and more storage capacity for EC2 applications on Snowball Edge than you can achieve with only a root volume. You can now attach multiple volumes to your EC2 instances. Volumes that are attached to EC2 instances on Snowball Edge persist independently from the life of the instance, enabling you to deploy multiple applications on Snowball Edge, and to start and stop the applications as needed.

**Q: What are the types of block storage volumes I can use, and how much capacity can each volume type use?**

Snowball Edge block storage provides performance-optimized SSD volumes (sbp1), and capacity-optimized HDD volumes (sbg1), to meet IOPS and throughput requirements for a wide-variety of data processing and data collection applications. Block storage volumes have a maximum size of 10 TB per volume, and you can attach up to 10 volumes to any EC2 instance on Snowball Edge.

On Snowball Edge Compute Optimized, you can use up to 7 TB of NVMe SSD for sbp1 volumes, which are good for latency-sensitive applications, such as machine learning. On Snowball Edge Storage Optimized, you can use up to 1 TB of SATA SSD for sbp1 volumes, which are good for pre-processing data.

On both the Snowball Edge Storage Optimized and Compute Optimized devices, you can use capacity-optimized volumes, sbg1, to store data on HDDs. This volume type is appropriate for data collection and less IOPS-intensive applications. It has a maximum volume size of 10 TB, and you can attach multiple volumes to any instance. You can use up to 86 TB of HDD storage for sbg1 on Snowball Edge Storage Optimized. You can use up to 40 TB of HDD storage for sbg1 on Snowball Edge Compute Optimized.

**Q: How do I get started with block storage on Snowball Edge?**

By default, all Snowball Edge devices are now shipped with the block storage feature. Once you unlock the device you can use AWS CLI or SDK to create volumes and attach them to an Amazon EC2 instance. You can attach multiple volumes to each EC2 instance, however, a single volume can only be attached to a single instance at any time.

**Q: How is Snowball Edge block storage different from Amazon EBS?**

Snowball Edge block storage has different performance, availability, and durability characteristics than Amazon EBS volumes. Also, it provides only a subset of Amazon EBS capabilities. For example, snapshot functionality is not currently supported on Snowball Edge block storage. Please see [Snowball Edge’s technical documentation](https://docs.aws.amazon.com/snowball/) for a complete list of supported APIs.

**Q: Which Amazon EBS APIs does SBE block storage support?**

To interact with block storage on SBE, you can use create, delete, attach, detach, and describe volumes EBS APIs. Please see [Snowball Edge’s technical documentation](https://docs.aws.amazon.com/snowball/) for a complete list of supported APIs.

**Q: Which Amazon Machine Images can I use on Snowball Edge to utilize block storage?**

Any Amazon Machine Image (AMI) running on Snowball Edge can access up to 10 block storage volumes at once. Generic AMIs provided by AWS and custom AMIs can access any block storage volume. There are no special requirements to make the block storage volumes work. However, certain operating systems perform better with specific drivers. Please see [Snowball Edge’s technical documentation](https://docs.aws.amazon.com/snowball/) for details.

**Q: Can the volumes on one device be accessible to Amazon EC2 instances running on another device?**

Volumes created on a single Snowball Edge are only accessible to the EC2 instances running on that device.

**Q: How can we monitor storage capacity used by various volumes?**

You can use [describe-device](https://docs.aws.amazon.com/snowball/latest/developer-guide/using-client-commands.html#client-status) command from the Snowball client to monitor how much block storage is been used on the device. When you create a volume, all of the storage capacity requested is allocated to it based on the available capacity.

**Q: Can I transfer data stored on block storage to Amazon EBS volumes in the cloud?**

Not directly, no. Data on block storage volumes on Snowball Edge is deleted when the device returns to AWS. If you wish to preserve data in block storage volumes, you must copy data into the Amazon S3 adapter in the case of data migration jobs or Amazon S3 compatible storage in the case of edge compute devices. The data from the Amazon S3 adapter will be copied into your S3 bucket when the device returns to AWS as part of import job. For edge compute, you can use AWS DataSync to transfer data online back and forth between your S3 buckets in regions and S3 buckets on devices when there’s connectivity to AWS region.

**Q: Can I operate object and block storage on the same device?**

Yes, you can use the Amazon S3 compatible storage on Snow and block storage on the same Snowball Edge Compute Optimized device in a single device deployment. The object storage and block storage used for sbg1 volumes share the same data disk capacity and is pre-provisioned at the time of placing an order. The underlying storage features work together so that an increase in I/O demand for block or object storage does not impede the availability and performance of the other.  Note, this is not supported in the case of cluster deployments where all storage on data disks is utilized for Amazon S3 capacity.  

**Q: Do I need to configure volumes or any storage resources when ordering my Snowball Edge from the AWS Console?**

No, you add volumes to your Amazon EC2 instances after you have received the device.

**Q: Do I need to allocate storage resources on the device between block and object storage?**

No. You can dynamically add or remove volumes and objects based on your application needs.

**Q: Are the volumes encrypted by default?**

Snowball Edge is designed with security in mind for the most sensitive data. All data written into block volumes is encrypted by keys provided by you through AWS Key Management Service (KMS). All volumes are encrypted using the same keys selected during Snowball Edge job creation. The keys are not permanently stored on the device and are erased after loss of power.

**Q: What are best practices to achieve optimum performance with Snowball Edge block storage?**

Additional volumes attached using the block storage offer up to 10 times higher performance compared to the root volumes. We recommended you use relatively smaller root volumes, and create additional block storage volumes for storing data for your Amazon EC2 applications. Please see [Snowball Edge’s technical documentation](https://docs.aws.amazon.com/snowball/latest/developer-guide/BestPractices.html) for performance best practices, and recommended drivers.  

## Regional Availability

**Q: In what Regions are Snowball Edge available?**

Check the [Regional Service Availability](https://aws.amazon.com/about-aws/global-infrastructure/regional-product-services/) pages for the latest information. 

**Q: Can a Snowball Edge be shipped to an alternate AWS Region?**

No. Snowball Edge devices are designed to be requested and used within the same AWS Region where your S3 bucket is located. The device may not be requested from one Region and returned to another. Snowball Edge devices used for imports or exports from an AWS Region in the EU may be used with any of the other EU countries. Check the [Regional Service Availability](https://aws.amazon.com/about-aws/global-infrastructure/regional-product-services/) pages for the latest information.  

## Security

**Q: Does Snowball Edge encrypt my data?**

Snowball Edge encrypts all data with 256-bit encryption. You manage your encryption keys by using the AWS Key Management Service (AWS KMS). Your keys are never stored on the device and all memory is erased when it is disconnected and returned to AWS.

**Q: How does Snowball Edge physically secure my data?**

In addition to using a tamper-resistant enclosure, Snowball Edge uses industry-standard Trusted Platform Modules (TPM) designed to detect any unauthorized modifications to the hardware, firmware, or software. AWS visually and cryptographically inspects every device for any signs of tampering and to verify that no changes were detected by the TPM.

**Q: How does Snowball Edge help digitally secure my data?**

Snowball Edge is designed with security in mind for the most sensitive data. All data is encrypted by keys provided by you through AWS Key Management Service (KMS). The keys are not permanently stored on the device and are erased after loss of power. Applications and Lambda functions run in a physically isolated environment and do not have access to storage. Lastly, after your data has been transferred to AWS, your data is erased from the device using standards defined by National Institute of Standards and Technology. Snowball Edge devices are hardened against attack and all configuration files are encrypted and signed with keys that are never present on the device.

**Q: Is there a way to easily track my data transfer jobs?**

Snowball Edge uses an innovative, E Ink shipping label designed to ensure the device is automatically sent to the correct AWS facility. When you have completed your data transfer job, you can track it by using Amazon SNS generated text messages or emails, and the console.

**Q: Can I get a history of Snowball API calls made on my account for security analysis and operational troubleshooting purposes?**

Yes. To receive a history of Snowball API calls made on your account, you simply turn on CloudTrail in the AWS Management Console; The following API calls in Snowball are not recorded and delivered: DescribeAddress (in response), CreateAddress (in request), DescribeAddresses (in response).  

## Import Data with Snowball Edge

**Q: How do I transfer my data to the Snowball Edge?**

After you have connected and activated the Snowball Edge, you can transfer data from local sources to the device through the S3-compatible endpoint or the NFS file interface, both available on the device. You can also use the Snowball client to copy data. To learn more, please refer to the [Snowball Edge documentation](https://docs.aws.amazon.com/snowball/index.html).  
  
**Q: When can I delete the data on my disk(s) after I’ve copied the data onto Snowball Edge and shipped the Snowball Edge back to AWS?**

Wait to confirm that the Snowball Edge has been received by AWS and your data has successfully been transferred into appropriate S3 buckets prior to you deleting any data on your disk(s). While AWS verifies the integrity of files copied to Snowball Edge during the S3 transfer, it is your responsibility to verify the integrity of data before deleting it from your disk(s). AWS is not liable for any lost or corrupted data during copy or transit.  

**Q: What do I do when the data has been transferred to the Snowball Edge?**

When the data transfer job is complete, the E Ink display on the Snowball Edge automatically updates the return shipping label to indicate the correct AWS facility to ship to. Just drop off the Snowball Edge at the nearest UPS and you're all set. You can track the status of your transfer job through Amazon SNS generated text messages or emails, or directly in the AWS Management Console.  

**Q. Is it possible to stop data ingestion from an AWS Snowball device once returned to AWS?** 

Yes. You can stop the data ingestion to an Amazon Simple Storage Service (Amazon S3) bucket by cancelling the job in the AWS Snow Management Console or by contacting AWS support.   
  

**Q. Is it possible to stop data from being deleted on a returned AWS Snowball device after the data import is completed**?

No. AWS uses an automated workflow process to securely delete the data ingest and clean the returned device with a complete erasure of the Snowball device according to NIST 800-88 standards. Additionally, it is not possible to return the same device back to you after the data import is complete.  

## Export Data with Snowball Edge

**Q: What does it cost to export my data?**

In addition to the Export job fees detailed on our [pricing page](https://aws.amazon.com/snowball/pricing/), you will also be charged all fees incurred to retrieve your data from Amazon S3.

**Q: How quickly can I access my exported data?**

We typically start exporting your data within 24 hours of receiving your request, and exporting data can take as long as a week. Once the job is complete and the device is ready, we ship it to you using the shipping options you selected when you created the job.  

**Q. Do I get a checksum or any kind of receipt on what was loaded into Amazon S3?**  

Yes. AWS saves an import log report to your bucket. This report contains per file information including the date and time of the upload, the Amazon S3 key, MD5 checksum, and number of bytes. For more details, see the [documentation](https://docs.aws.amazon.com/snowball/latest/developer-guide/validation.html "AWS Documentation").

**Q. I created an export job of my Amazon S3 bucket and it contains keys which are in an Amazon S3 Glacier storage class. Will the keys be exported ?**

The Snowball export job from Amazon S3 workflow does not have access to the objects stored in the Amazon S3 Glacier or Amazon S3 Glacier Deep Archive storage classes. You must first restore these objects from the Glacier or Glacier Deep archive for a minimum of 10 days or until the Snow export job completes to ensure that these restored objects are successfully copied to the Snowball device.  

## Large Data Migration Manager

**Q: Why should I use Large Data Migration Manager?**

Large Data Migration Manager helps you plan, and monitor your large data migration from 500TB minimum to petabytes of data. First, Large Data Migration Manager enables you to create a plan for your migration projects that use multiple AWS Snow Family devices to complete your petabyte scale data migration or data movement from the rugged, mobile edge. Creating a plan helps you and your partners onboard to Snow and align on project goals such as data size to be migrated and project duration. Once a plan is in place, Large Data Migration Manager provides a central location in AWS Snow Family management console for you to stay updated with the progress of all your Snow jobs (number of outstanding jobs, current data ingested etc.), and view estimated schedules for placing the next job orders. Finally, you can control the project plan as you monitor the migration and can extend or end the migration when you deem appropriate.  

Prior to the Large Data Migration Manager launch, you had to track all of this information yourself and spend time coordinating with your partners and AWS for tracking data ingestion progress and placing job orders. Large Data Migration Manager saves you time and effort by keeping track of all project details and allows you to focus on your overall goal of data migration. 

**Q: How do I get started with using Large Data Migration Manager?**

You start by creating a data migration or data movement project plan in the AWS Management Console. To create a plan, you are prompted for your import job type specifics that includes plan name, service access roles and notification preference. Once a plan is created, you need to create a site where the Snow devices will be shipped. Site information details include name and shipping address for each site, data size amount, number of concurrent Snow jobs, Snow job type, Snow device, fill rate (as per the last monitored data), project start and end dates. After you create your site, you can review your automatically created Snow job ordering schedule, which helps you know when to order your Snow jobs. You can either clone from prior existing jobs or add a job that was already created to the site.  

**Q: How do I update my project plan using Large Data Migration Manager?**

You can update your project plan in one of two ways: (1) you modify your plan information by updating data size amount, number of concurrent Snow jobs, or (2) Snow’s Data Migration Manager calculates the average Snow job duration (from order creation to completion) and average fill rate on a per site basis to automatically adjust your plan. Data Migration Manager then uses these plan updates to adjust your ordering schedule to inform you of your project status and if additional Snow jobs are required. 

**Q: How do I monitor the Snow jobs using Large Data Migration Manager?**

You monitor your Snow jobs using the Data Migration Manager dashboard or viewing your project plan summary. Using the Data Migration Manager dashboard, you can quickly monitor project status and identify issues at a glance. With this new capability, you can track your overall migration or data movement transfer progress, time remaining, Snow job status, site status, average Snow job fill rate, average Snow job duration, and upcoming order schedule across your plan and site. 

**Q: Do I have to pay money to use Large Data Migration Manager?**

No. Large Data Migration Manager is available to customers using AWS Snow Family. 

**Q: In what regions is Large Data Migration Manager available?**

Large Data Migration Manager is available in all commercial regions where Snowball Edge devices are available.  

## AWS OpsHub

**Q: What is AWS OpsHub for Snow Family?**

AWS OpsHub is an application that you can download from the [Snowball resources page.](https://aws.amazon.com/snowball/resources/) It offers a graphical user interface for managing the AWS Snow Family devices. AWS OpsHub makes it easy to setup and manage AWS Snowball devices enabling you to rapidly deploy edge computing workloads and simplify data migration to the cloud. With just a few clicks in AWS OpsHub, you can unlock and configure devices, drag-and-drop data to devices, launch and manage EC2 instances on devices, or monitor device metrics. AWS OpsHub is available globally at no extra charge.

**Q: How does AWS OpsHub for Snow Family work?**

AWS OpsHub is an application that you can download and install on any Windows or Mac client machine, such as a laptop. Once you have installed AWS OpsHub and have your AWS Snow Family device on site, open AWS OpsHub and unlock the device. You will then be presented with a dashboard showing your device and its system metrics. You can then begin deploying your edge applications or migrating your data to the device with just a few clicks.

**Q: Can I use AWS OpsHub with a Snow Family device that I ordered before AWS OpsHub launched?**

Yes. However, the task automation features are available for only Snow Family devices ordered after AWS OpsHub launched on April 16, 2020. All other functionality will be available for all devices, including those ordered before AWS OpsHub launched.

**Q: When do I use AWS OpsHub compared to the AWS Management Console?**

You use AWS OpsHub to manage and operate your AWS Snow Family devices and the AWS services that run on them. AWS OpsHub is an application that runs on a local client machine, such as a laptop, and can operate in disconnected or connected environments. In contrast, you use the AWS Management Console to manage and operate the AWS services running in the cloud. The AWS Management Console is a web-based application that operates when you have a connection to the internet.

**Q: How do I keep my AWS OpsHub software up to date?**

AWS OpsHub will automatically check for AWS OpsHub software updates when the client machine that AWS OpsHub is running on is connected to the internet. When there is a software update, you will be notified on the application and will be given the option to download and update the latest software. Additionally, you can visit the [Snowball resources page](https://aws.amazon.com/snowball/resources/) and check for the latest version of AWS OpsHub.

**Q: Does AWS OpsHub validate and encrypt the data I transfer to the AWS Snow Family devices?**

Yes. When you copy data to AWS Snow Family devices using AWS OpsHub, checksums are used to ensure that the data you copy to the device is the same as the original. Also, all data written to AWS Snow Family devices is encrypted by default.  

## Billing

**Q: How much does it cost to use Snowball Edge?**

Please see our [AWS Snowball Edge pricing page](https://aws.amazon.com/snowball/pricing/) for pricing details.

**Q: How am I charged for Amazon S3 usage?**

Snowball Edge transfers data on your behalf into AWS services such as Amazon S3. Standard AWS service charges apply. Data transferred IN to AWS does not incur any data transfer fees, and Standard [Amazon S3 pricing](https://aws.amazon.com/s3/pricing/) fees apply for data stored in S3.

**Q: How am I charged for Amazon S3 compatible on Snowball Edge Compute Optimized devices for edge compute jobs?**

There is an additional charge for Amazon S3 compatible storage with increased resiliency, scale and expanded API feature-set. The pricing is based on S3 capacity provisioned at the time of placing order. Please see our [pricing pag](https://aws.amazon.com/snowball/pricing/)e for details.  

**Q: Is there any additional pricing for Snowball Edge block storage?**

No, there is no additional charge for this feature.

**Q: Can I purchase a Snowball Edge device?**

Devices are only available on a per-job pay-as-you-go basis, and are not available for purchase.  

## Tape Data Migration

**Q: Why should I use AWS Snowball to migrate my tape data?** 

When you use a Snowball Edge Storage Optimized device with Tape Gateway, you can quickly and securely migrate petabyte-scale physical tape data to S3 Glacier Flexible Retrieval or S3 Glacier Deep Archive—reducing your data storage costs without changing your tape-based backup workflows. 

**Q: How do I get started with Snowball to migrate my tape data?** 

To get started, in the AWS Snow Family console, order a Snowball Edge Storage Optimized device with Tape Gateway. When you receive your device, unlock it, and connect to your local network. Then start Tape Gateway, which looks like a physical tape library. Connect to AWS and copy data from physical tapes to virtual tapes on Tape Gateway using your existing backup application. 

After you complete your data copy, ship the Snowball Edge device back to AWS. Your data will be stored in either S3 Glacier Flexible Retrieval or S3 Glacier Deep Archive storage class. You can view your virtual tapes stored on AWS through the AWS Storage Gateway console and access data on them through a Tape Gateway that runs on premises as a virtual machine or hardware appliance or on an Amazon Elastic Compute Cloud (Amazon EC2) instance. 

**Q: Can I export virtual tapes stored on AWS to my on-premises data center using Snowball?** 

No, you cannot export your virtual tapes stored on AWS to your data center using Snowball. You can use a Snowball Edge Storage Optimized device with Tape Gateway to import data into AWS. To retrieve virtual tapes stored on AWS, you can use a Tape Gateway that runs on premises as a virtual machine or hardware appliance, or on an Amazon EC2 instance. 

**Q: When can I delete the data on my physical tapes after I’ve copied the data to Snowball and shipped the device back to AWS?** 

Before you delete any data on your physical tapes, wait for confirmation that your Snowball Edge Optimized device has been received by AWS and your data has been successfully transferred as virtual tapes to S3 Glacier Flexible Retrieval or S3 Glacier Deep Archive. To access your virtual tapes, navigate to your AWS Storage Gateway console. While AWS verifies the integrity of data copied to your Snowball Edge device during the migration, it is your responsibility to verify the integrity of data before deleting it from your physical tapes. AWS is not liable for any lost or corrupted data during copy or transit. 

**Q: Where are my virtual tapes stored on AWS?** 

You can choose to store your virtual tapes in either S3 Glacier Flexible Retrieval or S3 Glacier Deep Archive storage class in the AWS Region you specified when you ordered a Snowball Edge Storage Optimized device in the AWS Snow Family console. 

**Q: How do I access my data on virtual tapes?** 

You can read-from and write-to virtual tapes on Snowball until you export virtual tapes from your backup application. After you export virtual tapes, your data stored on Snowball is inaccessible. After you ship a Snowball Edge Storage Optimized device back to AWS and the transfer of your physical tapes to virtual tapes is complete, you can access data stored on virtual tapes through a Tape Gateway that runs on premises as a virtual machine or a hardware appliance or on an Amazon EC2 instance on AWS. 

**Q: Is my network connection to AWS used for data migration?** 

No, your network connection to AWS is not used for data migration. Data from your backup application is copied to your Snowball Edge Storage Optimized device and not synchronized with AWS over the network. 

**Q: Where can I learn more about Tape Gateway in AWS Storage Gateway?** 

Tape Gateway is a tape storage interface in Storage Gateway. [Learn more about Tape Gateway](https://aws.amazon.com/storagegateway/vtl/).  

## Workflow Integration Tools

**Q: Does the Snowball Edge support API access?**

Yes. The Snowball Job Management API provides programmatic access to the job creation and management features of a Snowball or Snowball Edge. It is a simple, standards-based REST web service interface, designed to work with any Internet development environment.

**Q: What can I do with the Snowball Job Management API?**

The [AWS Snowball Job Management API](https://docs.aws.amazon.com/snowball/latest/api-reference/api-reference.html) allows partners and customers to build custom integrations to manage the process of requesting Snowballs and communicating job status. The API provides a simple web service interface that you can use to create, list, update, and cancel jobs from anywhere on the web. Using this web service, developers can easily build applications that manage Snowball jobs. To learn more, please refer to [AWS Snowball documentation](https://docs.aws.amazon.com/snowball/latest/ug/whatissnowball.html).

**Q: What is the S3 Adapter?**

The [S3 SDK Adapter for Snowball](https://aws.amazon.com/snowball/resources/#tools) provides an S3-compatible interface for reading and writing data on a Snowball or Snowball Edge for data migration use cases.

**Q: What can I do with the S3 Adapter?**

The S3 Adapter allows customers to help applications write data from file and non-file sources to S3 buckets on the Snowball or Snowball Edge device. It also includes interfaces to copy data with the same encryption as is available through the Snowball client. To learn more, please refer to the [AWS Snowball documentation](https://docs.aws.amazon.com/snowball/latest/api-reference/api-reference.html).

**Q: Why would I use the S3 Adapter rather than the Snowball Client?**

The [Snowball Client](https://aws.amazon.com/snowball/resources/#Tools) is a turnkey tool that makes it easier to copy file-based data to Snowball. Customers who prefer a tighter integration can use the S3 Adapter to easily extend their existing applications and workflows to seamlessly integrate with Snowball for data migration use cases.

**Q: How is my data secured when I use the S3 Adapter?**

The S3 Adapter writes data using the same advanced encryption mechanism that the Snowball Client provides.

**Q: Which programming languages does the Snowball S3 Adapter support?**

The S3 Adapter communicates over REST which is language-agnostic.  

## Amazon S3 Compatible Storage on Snow

**Q: Why should I use Amazon S3 compatible storage on Snow?**

You use Amazon S3 compatible storage on Snow to run applications that require S3 object storage in rugged, mobile edge or disconnected environments for local data processing or residency use cases. For example, applications that leverage Amazon S3 in Region for machine learning inference or data analytics can now be deployed on AWS Snow devices at the edge to make real-time decisions proximal to end users, or to meet data residency requirements.

**Q: What S3 APIs and features are supported by Amazon S3 compatible storage on Snow?**

Amazon S3 compatible storage on Snow supports bucket and object APIs such as GetObject, PutObject, DeleteObject(s), multi part uploads, object tagging, CreateBuckets, DeleteBuckets, BucketLifecycle and List. Amazon S3 compatible storage on Snow supports encryption using SSE-S3 or SSE-C, authentication and authorization using Snow IAM, advanced features such as built-in resiliency, and flexible multi-node (3-16) deployment options. Amazon S3 compatible storage on Snow is an enhancement to the current S3 Adapter implementation on Snow, which has limited API support designed primarily for data transfer use cases

**Q: What AWS Snow Family devices can I use with Amazon S3 compatible storage?**

Amazon S3 compatible storage is available on Snowball Edge Compute Optimized devices for local edge compute and storage use case.

**Q: How do I monitor the health status of Amazon S3 compatible storage on Snow?**

Amazon S3 compatible storage on Snow continuously monitors health status of device or cluster. Background processes respond to data inconsistencies and temporary failures to heal and recover data in order to ensure resiliency. In the case of non-recoverable hardware failures, Amazon S3 compatible storage on Snow can continue operations, and provides proactive notifications through emails, prompting customers to work with AWS to replace failed devices. While devices are connected, AWS also receives these notifications when remote monitoring feature is turned on, for proactive customer engagement. Service and device health status are available to you locally on OpsHub at all times.  

**Q: Is my data stored on Amazon S3 compatible storage on Snow encrypted?**

Yes. Data stored in Amazon S3 compatible storage on Snow is encrypted using server-side encryption. Amazon S3 compatible storage on Snow supports both SSE-S3 and SSE-C encryption option. Server-side encryption encrypts only the object data, not object metadata.

**Q: How much capacity can I allocate for Amazon S3 compatible storage on Snow?**

S3 capacity on Amazon S3 compatible storage on Snow depends on the quantity and type of Snow device. For single node deployment, you can provision granular S3 capacity up to a maximum of 31TB on Snowball Edge Compute optimized device for a multi-node cluster setup, all storage capacity on device is allocated to Amazon S3 compatible storage on Snow. You can provision, up to a maximum 500TB on a 16-node cluster of Snowball Edge Compute optimized devices.Q.  How do I monitor the health status of Amazon S3 compatible storage on Snow?Amazon S3 compatible storage on Snow continuously monitors health status of device or cluster. Background processes respond to data inconsistencies and temporary failures to heal and recover data in order to ensure resiliency. In the case of non-recoverable hardware failures, Amazon S3 compatible storage on Snow can continue operations, and provides proactive notifications through emails and MQTT messages, prompting customers to work with AWS to replace failed devices. While devices are connected, AWS also receives these notifications when remote monitoring feature is turned on, for proactive customer engagement. Service and device health status are available to you locally on OpsHub at all times.