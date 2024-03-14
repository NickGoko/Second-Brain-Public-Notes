---
tags:
  - cloud/aws
---
- **Amazon FSx** provides fully managed third-party file systems.
- Amazon FSx <mark style="background: #ABF7F7A6;">provides you with the native compatibility of third-party file systems</mark> with feature sets for workloads such as Windows-based storage, high-performance computing (HPC), machine learning, and electronic design automation (EDA).

- <mark style="background: #ADCCFFA6;">You don’t have to worry about managing file servers and storage, as Amazon FSx automates the time-consuming administration tasks such as hardware provisioning, software configuration, patching, and backups.</mark>
- Amazon FSx integrates the file systems with cloud-native AWS services, making them even more useful for a broader set of workloads.

Amazon FSx provides you with four file systems to choose from:
- Amazon FSx for Windows File Server for Windows-based applications
- Amazon FSx for Lustre for compute-intensive workloads.
- Amazon FSx for NetApp ONTAP.  
	  ![[Pasted image 20240213105514.png]]
- Amazon FSX for OpenZFS.  
		![[Pasted image 20240213105629.png]]


![[Pasted image 20240213105104.png]]
# Amazon FSx for Windows File Server

### Overview of FSx for Windows File Server
![[Pasted image 20240213105234.png]]  
**Amazon FSx for Windows File Server** <mark style="background: #CACFD9A6;">provides a fully managed native Microsoft Windows file system so you can easily move your Windows-based applications that require shared file storage to AWS.</mark>

Built on Windows Server, Amazon FSx provides the compatibility and features that your Microsoft applications rely on, including full support for the _SMB protocol_, _Windows NTFS_, and _Microsoft Active Directory (AD)_ integration.

Amazon FSx uses SSD storage to provide fast performance with low latency.

This compatibility, performance, and scalability enables business-critical workloads such as home directories, media workflows, and business applications.

Amazon FSx helps you optimize TCO with Data Deduplication, reducing costs by 50-60% for general-purpose file shares.

User quotas give you the option to better monitor and control costs. You pay for only the resources used, with no upfront costs, or licensing fees.

### Details and Benefits

**High availability:** Amazon FSx automatically replicates your data within an Availability Zone (AZ) it resides in (which you specify during creation) to protect it from component failure, continuously monitors for hardware failures, and automatically replaces infrastructure components in the event of a failure.

**Multi-AZ:** Amazon FSx offers a multiple availability (AZ) deployment option, designed to provide continuous availability to data, even if an AZ is unavailable. Multi-AZ file systems include an active and standby file server in separate AZs, and any changes written to disk in your file system are synchronously replicated across AZs to the standby.

Supports Windows-native file system features:
- Access Control Lists (ACLs), shadow copies, and user quotas.
- NTFS file systems that can be accessed from up to thousands of compute instances using the SMB protocol.

Works with Microsoft Active Directory (AD) to easily integrate file systems with Windows environments.

Built on SSD-storage, Amazon FSx provides fast performance with up to 2 GB/second throughput per file system, hundreds of thousands of IOPS, and consistent sub-millisecond latencies.

Can choose a throughput level that is independent of your file system size.

Using DFS Namespaces, you can scale performance up to tens of gigabytes per second of throughput, with millions of IOPS, across hundreds of petabytes of data.

Amazon FSx can connect file systems to Amazon EC2, VMware Cloud on AWS, Amazon WorkSpaces, and Amazon AppStream 2.0 instances.

Amazon FSx also supports on-premises access via AWS Direct Connect or AWS VPN, and access from multiple VPCs, accounts, and regions using VPC Peering or AWS Transit Gateway.

Amazon FSx automatically encrypts your data at-rest and in-transit.

Assessed to comply with ISO, PCI-DSS, and SOC certifications, and is HIPAA eligible.

Integration with AWS CloudTrail monitors and logs your API calls letting you see actions taken by users on Amazon FSx resources.

Pay only for the resources you use, with no minimum commitments or up-front fees.

Can optimize costs by removing redundant data with Data Deduplication.

User quotas provide tracking, monitoring, and enforcing of storage consumption to help reduce costs.  
![[AWS Solutions Architect Skillbuilder#File Storage Amazon FSx for Windows File Server]]
### FAQ

**Q: What is Amazon FSx for Windows File Server?[](https://aws.amazon.com/fsx/sla/)**

A: **Amazon FSx for Windows File Server** <mark style="background: #FFF3A3A6;">provides fully managed, highly reliable, and scalable file storage that is accessible over the industry-standard Service Message Block (SMB) protocol</mark>.  
It is built on Windows Server, delivering a wide range of administrative features such as user quotas, end-user file restore, and Microsoft Active Directory (AD) integration.

To support a wide spectrum of workloads, Amazon FSx provides high levels of throughput and IOPS, and consistent sub-millisecond latencies.

Amazon FSx is accessible from Windows, Linux, and MacOS compute instances and devices. Thousands of compute instances and devices can access a file system concurrently. [Amazon FSx File Gateway](https://aws.amazon.com/storagegateway/file/fsx/) provides low-latency, on-premises access to fully managed file shares in the cloud.  

**Q: What is an Amazon FSx for Windows File Server file system, and what is a file share?**

A: A file system is the primary resource in Amazon FSx. It’s where you store and access your files and folders. It is associated with a storage amount and a throughput capacity, as well as a DNS name for accessing it.

A file share is a specific folder (and its subfolders) within your file system that you make accessible to your compute instances – every file system comes with a default Windows file share, named “share” and you can create and manage as many other Windows file shares as you’d like.

**Q: How do I get started with FSx for Windows File Server?**

A: To use Amazon FSx, you must have an AWS account. If you do not already have an AWS account, you can [sign up for an AWS account](https://portal.aws.amazon.com/billing/signup).

Once you have created an AWS account, you can create a file system via the AWS Management Console, the AWS Command Line Interface (AWS CLI), and Amazon FSx API (and various language-specific SDKs).

**Q: What instance types and OS versions can I access my file system from?**

A: By supporting the SMB protocol, Amazon FSx can connect your file system to Amazon EC2, Amazon ECS, VMware Cloud on AWS, Amazon WorkSpaces, and Amazon AppStream 2.0 instances. To ensure compatibility with your applications, Amazon FSx supports all Windows versions starting from Windows Server 2008 and Windows 7, and current versions of Linux (using the cifs-utils tool).

**Q: How do I access Amazon FSx for Windows File Server from Amazon Elastic Container Service (Amazon ECS) containers?  
**

A: You can use Amazon FSx to enable persistent, shared storage for your containerized applications running on Amazon ECS. You can easily access Amazon FSx for Windows Server file systems on Amazon ECS by referencing your file systems in your task definition. Getting started instructions can be found in the [Amazon ECS documentation](https://docs.aws.amazon.com/fsx/latest/WindowsGuide/supported-fsx-clients.html#supported-clients-fsx).

**Q: How do I access data on my Amazon FSx file system?**

A: From within Windows, use the “Map Network Drive” feature to map a drive letter (e.g., Z:) to a file share on your Amazon FSx file system. You can also access your file system from Linux using the cifs-utils tool to mount your file share. Once you've done this, you can work with the files and folders in your Amazon FSx file system just like you would with a local file system.

**Q: How do I manage a file system?**

A: Amazon FSx is a fully-managed service, so all of the file storage infrastructure is managed for you. When you use Amazon FSx, you avoid the complexity of deploying and maintaining complex file system infrastructure.

To create, view, tag, and delete file systems and backups, you can use the AWS Management Console, the AWS command-line interface (CLI), or the Amazon FSx API (and various language-specific SDKs). To administer file systems, including managing file shares, active user sessions and open files, shadow copies, user quotas, and Data Deduplication, you can use the Amazon FSx remote management CLI via PowerShell.  

**Q: How do I migrate my existing file data into an Amazon FSx file system?**

A: If you’d like to migrate your existing files to Amazon FSx for Windows File Server file systems, we recommend the use of AWS DataSync, an online data transfer service designed to simplify, automate, and accelerate copying large amounts of data to and from AWS storage services. DataSync copies data over the internet or AWS Direct Connect. As a fully managed service, DataSync removes much of the need to modify applications, develop scripts, or manage infrastructure. For more information, see [Migrating Existing Files to Amazon FSx for Windows File Server Using AWS DataSync guide](https://docs.aws.amazon.com/fsx/latest/WindowsGuide/migrate-files-to-fsx-datasync.html).  

A secondary option is Windows’s Robust File Copy (RoboCopy) to copy your files directly to Amazon FSx.  

Once you have moved your file and folder data, Amazon FSx offers programmatic share management support to help you easily migrate your file share configuration. You must include security ACLs (SACLs) in your data migration to keep using your existing audit controls for file access auditing. Learn more about migrating your existing file shares in the [documentation guide](https://docs.aws.amazon.com/fsx/latest/WindowsGuide/migrate-to-fsx.html).

**Q: How do I monitor my file system’s activity?**

A: You can monitor storage capacity and file system activity using Amazon CloudWatch, monitor all Amazon FSx API calls using AWS CloudTrail, and monitor end user actions with file access auditing using Amazon CloudWatch Logs and Amazon Kinesis Data Firehose.  

**Q: What workloads is Amazon FSx for Windows File Server designed for?**

A: Amazon FSx was designed for a broad set of use cases that require Windows shared file storage, like CRM, ERP, custom or .NET applications, home directories, data analytics, media and entertainment workflows, web serving and content management, software build environments, and Microsoft SQL Server.

**Q: How do I use Amazon FSx with Microsoft SQL Server?**  

High availability (HA) Microsoft SQL Server is typically deployed across multiple database nodes in a Windows Server Failover Cluster (WSFC), with each node having access to shared file storage. Amazon FSx for Windows File Server can be used as shared storage for High Availability (HA) Microsoft SQL Server deployments in two ways: as storage for active data files and as an SMB file share witness. For more information, see [Using Amazon FSx with Microsoft SQL Server](https://docs.aws.amazon.com/fsx/latest/WindowsGuide/sql-server.html) or read the [Simplify Your Microsoft SQL Server High Availability deployments](https://aws.amazon.com/blogs/storage/simplify-your-microsoft-sql-server-high-availability-deployments-using-amazon-fsx-for-windows-file-server/) blog.

**Q: When should I use Amazon FSx for Windows File Server vs. other Amazon FSx file system types?**

A: Please refer to the [Choosing an Amazon FSx file system](https://aws.amazon.com/fsx/when-to-choose-fsx/) page for a guide on how to choose between the different Amazon FSx file storage offerings.

**Q: How does Amazon FSx support access from my on-premises environment?**

A: Yes, you can access Amazon FSx file systems from your on-premises environment using an [AWS Direct Connect](https://aws.amazon.com/directconnect/) or [AWS VPN](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_VPN.html) connection between your on-premises datacenter and your Amazon VPC. With support for AWS Direct Connect, Amazon FSx allows you to access your file system over a dedicated network connection from your on-premises environment. With support for AWS VPN, Amazon FSx allows you to access your file system from your on-premises devices over a secure and private tunnel.

[Amazon FSx File Gateway](https://aws.amazon.com/storagegateway/file/fsx/) optimizes on-premises access to fully managed, low-latency file shares in the cloud. By maintaining a local cache of frequently accessed data, Amazon FSx File Gateway enables faster performance and reduced data transfer cost for file-based workloads and business applications such as user shares, documents, and content management workflows.  

With on-premises access, you can use Amazon FSx for hosting user shares accessible by on-premises end-users, for cloud bursting workloads to offload your application processing to the cloud, and for backup and disaster recovery solutions. For more information, see [Accessing Amazon FSx from on-premises](https://docs.aws.amazon.com/fsx/latest/WindowsGuide/supported-fsx-clients.html#on-premise-access).

**Q: Does Amazon FSx support access from multiple VPCs, accounts, and regions?**

A: Yes, you can access your Amazon FSx file systems from multiple Amazon VPCs, AWS accounts, and AWS Regions using [VPC Peering](https://docs.aws.amazon.com/vpc/latest/peering/Welcome.html) connections or [AWS Transit Gatewa](https://docs.aws.amazon.com/vpc/latest/tgw/tgw-getting-started.html)y. A VPC Peering connection is a networking connection between two VPCs that enables you to route traffic between them. A transit gateway is a network transit hub that you can use to interconnect your VPCs. With VPC Peering and AWS Transit Gateway, you can even interconnect VPCs across AWS accounts and AWS Regions.

With access to your file systems via VPC Peering and Transit Gateway, you can share your file data sets across users and applications in multiple VPCs, AWS accounts, and/or AWS Regions. For more information, see [Accessing Amazon FSx from multiple VPCs, accounts or regions](https://docs.aws.amazon.com/fsx/latest/WindowsGuide/supported-fsx-clients.html#different-vpc-account-access).

**Q: Does Amazon FSx support shared VPCs?**

A: Yes, with Amazon FSx, you can create and use file systems in shared Amazon Virtual Private Clouds (VPCs) from both owner accounts and participant accounts with which the VPC has been shared. VPC sharing enables you to reduce the number of VPCs that you need to create and manage, while you still benefit from using separate accounts for billing and access control.  

**Q: What regions is Amazon FSx for Windows File Server available in?**

A: Please refer to [Regional Products and Services](https://aws.amazon.com/about-aws/global-infrastructure/regional-product-services/) for details of Amazon FSx for Windows File Server service availability by region.

**Q: Does Amazon FSx offer a Service Level Agreement (SLA)?**

A: Yes. The [Amazon FSx SLA](https://aws.amazon.com/fsx/sla/) provides for a service credit if a customer's monthly uptime percentage is below our service commitment in any billing cycle.

# Amazon FSx for Lustre
![[Pasted image 20240213105145.png]]
### Overview of FSx for Lustre

Amazon FSx for Lustre provides a high-performance file system optimized for fast processing of workloads such as machine learning, **high performance computing (HPC)**, video processing, financial modeling, and electronic design automation (EDA).

These workloads commonly require data to be presented via a fast and scalable file system interface, and typically have data sets stored on long-term data stores like Amazon S3.

Amazon FSx for Lustre provides a fully managed high-performance Lustre file system that allows file-based applications to access data with hundreds of gigabytes per second of data, millions of IOPS, and sub millisecond latencies.

Amazon FSx works natively with Amazon S3, letting you transparently access your S3 objects as files on Amazon FSx to run analyses for hours to months.

You can then write results back to S3, and simply delete your file system. FSx for Lustre also enables you to burst your data processing workloads from on-premises to AWS, by allowing you to access your FSx file system over AWS Direct Connect or VPN.

You can also use FSx for Lustre as a standalone high-performance file system to burst your workloads from on-premises to the cloud.

By copying on-premises data to an FSx for Lustre file system, you can make that data available for fast processing by compute instances running on AWS.

- Metadata stored on Metadata Targets (MST).
- Performance is based on the size of the filesystem.
  
[  **Amazon Fsx for Lustre Summary**](#)
- provides easy and cost effective way to launch and run the world’s most popular high-performance file system.
- is a type of parallel distributed file system, for large-scale computing
- Lustre is derived from “Linux” and “cluster”
- Machine Learning, High Performance Computing (HPC) esp. _Video Processing, Financial Modeling, Electronic Design Automation_
- scales up to 100s GB/s, millions of IOPS, sub-ms latencies
- seamless integration with S3, it transparently presents S3 objects as files and allows you to write changed data back to S3.
- can “read S3” as a file system (through FSx)
- can write the output of the computations back to S3 (through FSx)
- supports encryption of data at rest and in transit
- can be used from on-premise servers

### Details and Benefits

Lustre is a popular open-source parallel file system that is designed for high-performance workloads. These workloads include HPC, machine learning, analytics, and media processing.

A parallel file system provides high throughput for processing large amounts of data and performs operations with consistently low latencies.

It does so by storing data across multiple networked servers that thousands of compute instances can interact with concurrently.

The Lustre file system provides a POSIX-compliant file system interface.

Amazon FSx can scale up to hundreds of gigabytes per second of throughput, and millions of IOPS.

Amazon FSx provides high throughput for processing large amounts of data and performs operations with consistent, sub-millisecond latencies.

Amazon FSx for Lustre supports file access to thousands of EC2 instances, enabling you to provide file storage for your high-performance workloads, like genomics, seismic exploration, and video rendering.

Amazon S3:

- Amazon FSx works natively with Amazon S3, making it easy to access your S3 data to run data processing workloads.
- Your S3 objects are presented as files in your file system, and you can write your results back to S3.
- This lets you run data processing workloads on FSx for Lustre and store your long-term data on S3 or on-premises data stores.

On-premises:

- You can use Amazon FSx for Lustre for on-premises workloads that need to burst to the cloud due to peak demands or capacity limits.
- To move your existing on-premises data into Amazon FSx, you can mount your Amazon FSx for Lustre file system from an on-premises client over AWS Direct Connect or VPN, and then use parallel copy tools to import your data to your Amazon FSx for Lustre file system.
- At any time you can write your results back to be durably stored in your data lake.

Security:

- All Amazon FSx file system data is encrypted at rest.
- You can access your file system from your compute instances using the open-source Lustre client.
- Once mounted, you can work with the files and directories in your file system just like you would with a local file system.
- FSx for Lustre is compatible with the most popular Linux-based AMIs, including Amazon Linux, Red Hat Enterprise Linux (RHEL), CentOS, Ubuntu, and SUSE Linux.
- You access your Amazon FSx file system from endpoints in your Amazon VPC, which enables you to isolate your file system in your own virtual network.
- You can configure security group rules and control network access to your Amazon FSx file systems.
- Amazon FSx is integrated with AWS Identity and Access Management (IAM).
- This integration means that you can control the actions your AWS IAM users and groups can take to manage your file systems (such as creating and deleting file systems).
- You can also tag your Amazon FSx resources and control the actions that your IAM users and groups can take based on those tags.

Can be deployed in persistent or scratch.

#### Scratch

Scratch is designed for best performance for short term or temporary use cases.

Does not provide HA or replication.

Larger files systems require more servers and disks (more chance of failure).

Auto heals when hardware failure occurs.

Min size is 1.2 TiB with increments of 2.4 TiB.

#### Persistent

Longer term use cases.

Provides HA in one AZ and self-healing.

50 MB/s, 100 MB/s, and 200 MB/s per TiB of storage.

Burst up to 1,300 Mb/s per TiB (uses a credit system).

![[AWS Solutions Architect Skillbuilder#File Storage Amazon FSx for Lustre]]


---
# File Storage: Amazon FSx for NetApp ONTAP
![](https://i.imgur.com/vESFpE8.png)


![[AWS Solutions Architect Skillbuilder#File Storage Amazon FSx for NetApp ONTAP]]

---

# File Storage: Amazon FSx for OpenZFS
![](https://i.imgur.com/p48nJ79.png)



![[AWS Solutions Architect Skillbuilder#File Storage Amazon FSx for OpenZFS]]


# Amazon FSx for Lustre FAQs

### What is Amazon FSx for Lustre?

Amazon FSx for Lustre makes it easy and cost effective to launch, run, and scale the world’s most popular high-performance file system.

The open source Lustre file system is designed for applications that require fast storage – where you want your storage to keep up with your compute. Lustre was built to solve the problem of quickly and cheaply processing the world’s ever-growing data sets, and it’s the most widely used file system for the 500 fastest computers in the world.

As a fully managed service, Amazon FSx brings Lustre to the masses, allowing you to use it for any workload where storage speed matters. Amazon FSx eliminates the traditional complexity of setting up and managing high-performance Lustre file systems, allowing you in minutes to spin up, run, and scale a battle-tested high-performance file system. It also provides multiple deployment options so you can optimize cost for your needs.

Amazon FSx also integrates with [Amazon S3](https://aws.amazon.com/s3/) , making it easy for you to process cloud data sets with the Lustre high-performance file system. When linked to an S3 bucket, an FSx for Lustre file system transparently presents S3 objects as files and can automatically update the contents of the linked S3 bucket as files are added to, changed in, or deleted from the file system.

### What Use Cases Does Amazon FSx for Lustre Support?

Use Amazon FSx for Lustre for workloads where speed matters, such as machine learning, [high performance computing (HPC)](https://aws.amazon.com/hpc/) , video processing, financial modeling, genome sequencing, and electronic design automation (EDA).

### How Do I Get Started with Amazon FSx for Lustre?

To use Amazon FSx for Lustre, you must have an AWS account. If you do not have one, sign up on [Sign up for AWS](https://portal.aws.amazon.com/billing/signup) .

With an AWS account, you can easily create a file system from the [AWS Management Console,](https://signin.aws.amazon.com/signin?redirect_uri=https%3A%2F%2Fconsole.aws.amazon.com%2Ffsx%2Fhome%3Fstate%3DhashArgs%2523%26isauthcode%3Dtrue&client_id=arn%3Aaws%3Aiam%3A%3A015428540659%3Auser%2Ffsx&forceMobileApp=0&code_challenge=xSUlsKLm1M_dnIsA2Nu62AzhluQs3A5vPFUyh_-7CYM&code_challenge_method=SHA-256) the AWS Command Line Interface (AWS CLI), or the Amazon FSx API (and various language-specific SDKs). Within minutes, your file system is running and accessible to your compute instances. Learn more about [getting started with FSx for Lustre.](https://docs.aws.amazon.com/fsx/latest/LustreGuide/getting-started.html)

### What is the Difference between Scratch and Persistent Deployment Options?

Amazon FSx for Lustre provides two deployment options: scratch and persistent.

Scratch file systems are designed for temporary storage and shorter-term processing of data. Data is not replicated and does not persist if a file server fails.

Persistent file systems are designed for longer-term storage and workloads. The file servers are highly available, and data is automatically replicated within the [AWS Availability Zone (AZ)](https://aws.amazon.com/about-aws/global-infrastructure/) that is associated with the file system. The data volumes attached to the file servers are replicated independently from the file servers to which they are attached.

### How Do I Choose the Right Storage Type for My Application?

Choose SSD storage for latency-sensitive workloads or workloads requiring the highest levels of IOPS/throughput. Choose HDD storage for throughput-focused workloads that aren’t latency-sensitive. For HDD-based file systems, the optional SSD cache improves performance by automatically placing your most frequently read data on SSD (the cache size is 20% of your file system size).

### What Instance Types and AMIs Work with Amazon FSx for Lustre?

FSx for Lustre is compatible with the most popular Linux-based AMIs, including Amazon Linux, Amazon Linux 2, Red Hat Enterprise Linux (RHEL), CentOS, SUSE Linux and Ubuntu. FSx for Lustre is also compatible with both x86-based EC2 instances and Arm-based EC2 instances powered by the [AWS Graviton2](https://aws.amazon.com/ec2/graviton/) processor. With FSx for Lustre, you can mix and match the instance types and Linux AMIs that are connected to a single file system.

### How Do I Access an FSx for Lustre File System from a Compute Instance?

To access your file system from a Linux instance, you first install the open-source Lustre client on that instance. Once it’s installed, you can mount your file system using standard Linux commands. Once mounted, you can work with the files and directories in your file system just like you would with a local file system.

The Lustre client is included with Amazon Linux 2 and Amazon Linux. For Red Hat Enterprise Linux, CentOS, and Ubuntu, an AWS repository for the Lustre client is supported that provides clients compatible with these operating systems. See the [FSx for Lustre documentation](https://docs.aws.amazon.com/fsx/latest/LustreGuide/install-lustre-client.html) for details.

### How Do I Access an Amazon FSx for Lustre File System from an Amazon Elastic Kubernetes Service (EKS) Cluster?

You can use persistent storage volumes backed by FSx for Lustre using the FSx for Lustre CSI driver from Amazon EKS or your self-managed Kubernetes on AWS. See the [Amazon EKS documentation](https://docs.aws.amazon.com/eks/latest/userguide/fsx-csi.html) for details.

### How Do I Manage an FSx for Lustre File System?

Amazon FSx is a fully managed service, so all of the file storage infrastructure is managed for you. When you use Amazon FSx, you avoid the complexity of deploying and maintaining complex file system infrastructure.

You can administer a file system via the [AWS Management Console](https://console.aws.amazon.com/fsx/) , the AWS command-line interface (CLI), or the Amazon FSx API (and various language-specific SDKs). The Console, API, and SDK provide the ability to create, scale, and delete file systems; create and edit file system tags, and display detailed information about file systems. 

### How Can I Set and Enforce Storage Limits for File System Users?

You can set and enforce storage limits based on the number of files or storage capacity consumed by a specific user, group or project. You can choose to set a hard limit that denies users, groups or projects from consuming additional storage after exceeding their quota, or set a soft limit that provides users with a grace period to complete their workloads before converting into a hard limit. To simplify file system administration, you can also monitor user-, groupand project-level storage usage on FSx for Lustre file systems. To learn more, visit the FSx for Lustre [Storage Quotas documentation](https://docs.aws.amazon.com/fsx/latest/LustreGuide/lustre-quotas.html) .

### How Do I Use Data Compression?

You can enable data compression on your file system by clicking Update in the Amazon FSx Console, or by calling “UpdateFileSystem” in the AWS CLI/API and specifying “LZ4” as the Data Compression Type. Once the feature is enabled, all newly-written files will be automatically compressed on FSx for Lustre before they are written to disk and uncompressed when they are read. Since the LZ4 data compression algorithm is lossless, the original data can be fully reconstructed from the compressed data. Files loaded on the file system prior to enabling the data compression feature can also be compressed using the “lfs\_migrate” command.

### How Do I See the Impact of Data Compression on My File System Storage?

You can use CloudWatch Metrics to see the total logical disk usage (without compression) and total physical disk usage (with compression) of your file system. See [Amazon FSx for Lustre Data Compression documentation](https://docs.aws.amazon.com/fsx/latest/LustreGuide/data-compression.html) for additional information.

### How Does Data Compression Impact File System Performance?

The data compression feature on FSx for Lustre uses the LZ4 compression algorithm. Since the LZ4 compression algorithm is optimized for compression speed, enabling data compression will not adversely impact file system performance.

To provide fast reads and writes from RAM cache, FSx for Lustre file servers are equipped with higher levels of network bandwidth on the front-end network interface cards (NICs) than is available between the file servers and storage disks. Since data compression reduces the amount of data sent between file servers and storage disks, you will see an increase in overall file system throughput capacity when using data compression. Increases in throughput capacity related to data compression will be capped once you saturate the front-end NIC of your file system. See [FSx for Lustre documentation](https://docs.aws.amazon.com/fsx/latest/LustreGuide/data-compression.html) for more details on throughput performance when using data compression.

### How Do I Monitor My File system’s Activity?

Amazon FSx for Lustre provides native CloudWatch integration, allowing you to monitor file system health and performance metrics in real time. Example metrics include storage consumed, number of compute instance connections, throughput, and number of file operations per second. You can log all Amazon FSx API calls using AWS CloudTrail.

### How Do I Use Amazon FSx for Lustre to Speed up My Amazon SageMaker Machine Learning Training Jobs?

Amazon FSx for Lustre can be an input data source for Amazon SageMaker. When you use FSx for Lustre as an input data source, Amazon SageMaker ML training jobs can be accelerated by eliminating the initial S3 download step. SageMaker jobs are started as soon as the FSx for Lustre file system is linked with the S3 bucket without needing to download the full machine learning training dataset from S3. Data is lazy loaded as needed from Amazon S3 for processing jobs. FSx for Lustre can also help you reduce total cost of ownership (TCO) by avoiding the repeated download of common objects (so you can save S3 request costs) for iterative jobs on the same dataset.

### How Do I Use Amazon FSx for Lustre with AWS Batch?

Amazon FSx for Lustre integrates with AWS Batch through EC2 Launch Templates. AWS Batch is a cloud-native batch scheduler for HPC, ML, and other asynchronous workloads. AWS Batch will automatically and dynamically size instances to job resource requirements, and use existing FSx for Lustre file systems when launching instances and running jobs.

### How Do I Use Amazon FSx for Lustre with AWS ParallelCluster?

AWS ParallelCluster is an AWS-supported open-source cluster management tool that helps you to deploy and manage High Performance Computing (HPC) clusters on AWS. AWS ParallelCluster supports automatic creation of a new Amazon FSx for Lustre file system or the ability to use an existing Amazon FSx for Lustre file system as part of the cluster creation process.

### What Regions is Amazon FSx for Lustre Available In?

Please refer to [Regional Products and Services](https://aws.amazon.com/about-aws/global-infrastructure/regional-product-services/) for details of Amazon FSx for Lustre service availability by region.

### If I Have Data On-premises how Do I Make it Available to Amazon FSx for Lustre to Process It?

If you have high-performance or data processing workloads running on-premises and demand for computing capacity spikes, you can cloud burst your workloads to Amazon FSx for Lustre by using Amazon Direct Connect or VPN.

## S3 Integration

Close all

### If I Have Data in S3, how Do I Access it from Amazon FSx for Lustre?

You can link your Amazon FSx for Lustre file system to your Amazon S3 buckets, and FSx for Lustre makes your S3 data transparently accessible in your file system.

You can link your file system to S3 buckets by creating data repository associations using the Amazon FSx console, the AWS CLI, or the Amazon FSx API. The names of objects in your S3 buckets will appear as file and directory listings on the file system. The actual content of a given object is imported automatically from S3 only when you access the associated file on the file system for the first time—meaning an object’s data doesn’t consume space on your file system unless it’s accessed at least once on the file system.

When linked to an S3 bucket, FSx for Lustre can update the file system's contents automatically as objects are added to, changed in, or deleted from your S3 bucket. FSx for Lustre can also automatically update the contents of the linked S3 bucket as files are added to, changed in, or deleted from the file system.

Amazon FSx for Lustre uses parallel data transfer techniques to transfer data to and from S3 at up to hundreds of GB/s

### How Does Amazon FSx for Lustre Stay Synchronized with My S3 Buckets?

You can configure FSx for Lustre to keep content synchronized in both directions between the file system and the linked S3 buckets. As you make changes to objects in your S3 bucket, FSx for Lustre automatically detects and imports the changes to your file system. As you make changes to files in your file system, FSx for Lustre automatically exports the changes to your S3 bucket.

For both automatic import and automatic export, you can choose to import or export additions, changes, and deletions of files. You can set these preferences when you link an S3 bucket or at a later time by updating your data repository associations using the AWS CLI, the Amazon FSx API, or the Amazon FSx console. For more information about monitoring both automatic import and export, please see [Monitoring with Amazon CloudWatch](https://docs.aws.amazon.com/fsx/latest/LustreGuide/monitoring-cloudwatch.html) .

Alternatively, instead of using automatic import and automatic export, you also have the option to import and export batches of new and changed data between the file system and S3 for fine-grained control over data synchronization. You can run an Import or Export task using the AWS CLI, API, or console.

You can modify files in either S3 or the file system and each will persist updates in the order they receive them. If you modify the same file in both the S3 bucket and the file system, you should coordinate updates at the application level to prevent conflicts. FSx for Lustre will not prevent conflicting writes in multiple locations.

Learn more about [using data repositories](https://docs.aws.amazon.com/fsx/latest/LustreGuide/fsx-data-repositories.html) .

### How Are Directories, Symbolic Links, POSIX Metadata, and POSIX Permissions Imported from and Exported to Amazon S3?

FSx for Lustre stores directories and symbolic links (symlinks) as separate objects in your S3 bucket. For example, a directory is stored as an S3 object with a key name that ends with a slash ("/").

Amazon FSx for Lustre also automatically transfers Portable Operating System Interface (POSIX) metadata and permissions for files and directories when importing data from and exporting data to S3. The POSIX metadata is stored as S3 object metadata in the same format used by other AWS services.

See [POSIX metadata support for data repositories](https://docs.aws.amazon.com/fsx/latest/LustreGuide/overview-data-repo.html) for more details.

### Can I Link My S3 Bucket to Multiple FSx for Lustre File Systems?

Yes, you can create multiple FSx for Lustre file systems linked to the same S3 bucket. Doing so allows you to maintain a common data set in S3 that is reflected in multiple FSx for Lustre file systems, or to share results of computation on one FSx file system with users processing data on other file systems. You can modify files in any of the linked file systems. S3 and each file system will persist updates in the order they receive them. If you modify the same file in multiple file systems, you should coordinate updates at the application level to prevent conflicts. FSx for Lustre will not prevent conflicting writes in multiple locations.

### How Do I Release Inactive Data from My File System?

You can release inactive data from S3-linked file systems by using a data repository task. When you create a data repository task to release file data, you can specify the paths of directories or files you would like to release and optionally specify a minimum amount of time since last access for a file to be eligible for release.

Learn more about [releasing file system data](https://docs.aws.amazon.com/fsx/latest/LustreGuide/file-release.html) .

### Does Releasing File System Data Ensure My File System Will Never Become Full?

No. Releasing file system data will not ensure your file system will never become full. Releasing file system data optimizes your available storage by enabling you to remove inactive data that has been exported to a linked Amazon S3 bucket.

## Scale and Performance

Close all

### What Performance Can I Expect from Amazon FSx for Lustre?

Amazon FSx for Lustre file systems scale to TB/s of throughput and millions of IOPS. FSx for Lustre also supports concurrent access to the same file or directory from thousands of compute instances. FSx for Lustre provides consistent, sub-millisecond latencies for file operations.

See [Amazon FSx Performance documentation](https://docs.aws.amazon.com/fsx/latest/LustreGuide/performance.html) for more details.

### How Does Throughput Scale with Storage Capacity?

FSx for Lustre file systems automatically provision throughput for each TiB of storage provisioned. SSD-based file systems can be provisioned with 125, 250, 500, or 1,000 MB/s of throughput per TiB of storage provisioned. HDD-based file systems can be provisioned with 12 or 40 MB/s of throughput per TiB of storage provisioned.

### How Do I Change My File System's Storage Capacity?

You can increase the storage capacity of your file system by clicking “Update" in the Amazon FSx Console, or by calling “UpdateFileSystem” in the AWS CLI/API and specifying the desired storage capacity.

### When Should I Change My File system’s Throughput Tier? When Should I Change My File system’s Storage Capacity?

You should change your file system’s throughput tier if you want to adjust the read/write performance of your file system but do not plan to add data to your file system. You should change your file system’s storage capacity if you want to add data to your file system, or if your file system is at the highest supported throughput tier (e.g. 1000 MB/s) and you want to improve read/write performance.

### How Does Amazon FSx Grow the Storage Capacity of My File System? How long Does it Take?

Amazon FSx for Lustre stores data across multiple network file servers and stores file metadata on a dedicated metadata server with its own storage. When you request an update to your file system’s storage capacity, Amazon FSx automatically adds new network file servers and scales your metadata server. While scaling storage capacity, the file system may be unavailable for a few minutes. Client requests sent while the file system is unavailable will transparently retry and eventually succeed after scaling is complete.

After scaling, FSx transparently optimizes your file system by redistributing your data across the old and newly added file servers. This optimization process runs in the background, and can take between a few hours to a few days depending on the amount of data stored on your file system. The background optimization process has minimal impact on your workload performance. You can track the progress of the optimization process at any time using the Amazon FSx Console or AWS CLI/API. See the [Managing Storage Capacity](https://docs.aws.amazon.com/fsx/latest/LustreGuide/managing-storage-capacity.html) documentation for more information.

### How Does Amazon FSx Change the Throughput Tier of My File System? How long Does it Take?

Amazon FSx changes the throughput tier of your file system by switching out the file servers</p>

powering your file system to meet the requested throughput configuration. While scaling throughput on file systems smaller than 100 TiB, the file system will be unavailable for a few minutes. For file systems larger than 100 TiB, the file system may be unavailable for up to an hour. Client requests sent while the file system is unavailable will transparently retry and eventually succeed after scaling is complete.

In some cases, after scaling, FSx optimizes your file system, at which point your file system’s network I/O, CPU, and memory resources correspond with your new throughput level. This optimization process can take between a few hours to a few days. During this time, your new disk I/O performance level is available for write operations, and your read operations have disk I/O performance between the previous level and the new level. You can track the optimization process at any time using the Amazon FSx Console or AWS CLI/API. See the [Managing storage and throughput capacity](https://docs.aws.amazon.com/fsx/latest/LustreGuide/managing-storage-capacity.html) documentation for more information.

### How Frequently and in what Increments Can I Increase My File system’s Storage Capacity?

You can increase your file system’s storage capacity every six hours, and in the same increments that you can provision new file systems. Note that your previous scaling request, including optimization, must be complete when you issue a new scaling request.

### How Many Instances Can Connect to a File System?

An FSx for Lustre file system can be concurrently accessed by thousands of compute instances.

### What File System Sizes Are Supported by FSx for Lustre and what is the Increment Granularity?

Scratch and persistent SSD-based file systems can be created in sizes of 1.2 TiB or in increments of 2.4 TiB. Persistent HDD-based file systems with 12 MB/s and 40 MB/s of throughput per TiB can be created in increments of 6.0 TiB and 1.8 TiB, respectively.

### How Many File Systems Can I Create?

There is a 100-file system limit per account, which can be increased upon request.

## Security and compliance

Close all

### Does Amazon FSx for Lustre Support Data Encryption?

Yes. Amazon FSx for Lustre always encrypts your file system data and your backups at-rest using keys you manage through AWS Key Management Service (KMS). Amazon FSx encrypts data-in-transit when accessed from supported [EC2 instances](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/data-protection.html) . See the [Amazon FSx documentation](https://docs.aws.amazon.com/fsx/latest/LustreGuide/encryption-in-transit-fsxl.html) for details on regions where in-transit encryption is supported.

### What Access Control Capabilities Does Amazon FSx Provide?

Every FSx for Lustre resource is owned by an AWS account, and permissions to create or access a resource are governed by permissions policies. You specify the Amazon Virtual Private Cloud (VPC) in which your file system is made accessible, and you control which resources within the VPC have access to your file system using VPC Security Groups. You control who can administer your file system and backup resources (create, delete, etc.) using AWS IAM.

### Does Amazon FSx Support Shared VPCs?

Yes, with Amazon FSx, you can create and use file systems in shared Amazon Virtual Private Clouds (VPCs) from both owner accounts and participant accounts with which the VPC has been shared. VPC sharing enables you to reduce the number of VPCs that you need to create and manage, while you still benefit from using separate accounts for billing and access control.

### What compliance Programs Does Amazon FSx Support?

AWS has the longest-running compliance program in the cloud and is committed to helping customers navigate their requirements. Amazon FSx has been assessed to meet global and industry security standards. It complies with [PCI DSS](https://aws.amazon.com/compliance/pci-dss-level-1-faqs/) , ISO [9001](https://aws.amazon.com/compliance/iso-9001-faqs/) , [27001](https://aws.amazon.com/compliance/iso-27001-faqs/) , [27017](https://aws.amazon.com/compliance/iso-27017-faqs/) , and [27018](https://aws.amazon.com/compliance/iso-27018-faqs/) , and [SOC 1, 2, and 3](https://aws.amazon.com/compliance/soc-faqs/) , in addition to being [HIPAA eligible](https://aws.amazon.com/compliance/hipaa-compliance/) . That makes it easier for you to verify our security and meet your own obligations. For more information and resources, visit our [compliance pages](https://aws.amazon.com/compliance/) . You can also go to the [Services in Scope by Compliance Program page](https://aws.amazon.com/compliance/services-in-scope/) to see a full list of services and certifications.

## Availability and Durability

Close all

### When and why Should I Use the Persistent FSx for Lustre versus the Scratch FSx for Lustre Deployment Option?

Use scratch file systems when you need cost-optimized storage for short-term, processing-heavy workloads.

Use persistent file systems for workloads that run for extended periods or indefinitely, and may be sensitive to disruptions in availability.

### Does Amazon FSx Offer a Service Level Agreement (SLA)?

Yes. The [Amazon FSx SLA](https://aws.amazon.com/fsx/sla/) provides for a service credit if a customer's monthly uptime percentage is below our service commitment in any billing cycle. 

### What Are the Availability and Durability Characteristics of FSx for Lustre File Systems?

Amazon FSx for Lustre provides a parallel file system. In parallel file systems, data is stored across multiple network file servers to maximize performance and reduce bottlenecks, and each server has multiple disks. Larger file systems have more file servers and disks than smaller file systems.

On a persistent file system, if a file server becomes unavailable it is replaced automatically and within minutes. In the meantime, client requests for data on that server transparently retry and eventually succeed after the file server is replaced. With persistent file systems, data is replicated on disks and any failed disks are automatically replaced behind the scenes, transparently.

On a scratch file system, file servers are not replaced if they fail and data is not replicated. If a file server or a storage disk becomes unavailable, files stored on other servers are still accessible. If clients try to access files that are on the unavailable server, they will get an I/O error. The following table provides the availability/durability for which scratch ﬁle systems of example sizes are designed. As larger file systems have more file servers and more disks, the probabilities of failure are increased.

Table: Availability/durability of scratch file systems of various example sizes 

Scratch file system size (TiB)Number of file serversAvailability/durability during one dayAvailability/durability during one week1.2299.9%99.4%2.4299.9%99.4%4.8399.8%99.2%9.6599.8%98.6%50.42299.1%93.9%Please refer to the [Amazon FSx for Lustre documentation](https://docs.aws.amazon.com/fsx/latest/LustreGuide/using-fsx-lustre.html) for more information.

## Data Protection

Close all

### How Do I Take Backups on Amazon FSx for Lustre?

Amazon FSx takes daily automatic backups of your file systems, and allows you to take additional backups at any point. Amazon FSx backups are incremental, which means that only the changes after your most recent backup are saved, thus saving on backup storage costs by not duplicating data.

Alternatively, you can use data repository associations to keep the data in your FSx for Lustre file system synchronized with S3 buckets or prefixes. FSx will not take automatic backups of the file system if it is linked to S3.

### What Durability and Consistency Does Amazon FSx provide for Backups?

Backups are highly durable and file-system-consistent. To ensure high durability, Amazon FSx stores backups with 99.999999999% (11 9's) of durability on Amazon S3. Backups also present a consistent view of your file system, meaning that if metadata exists for a file in the backup, then the file’s associated data is also included in the backup.

### What is the Daily Backup Window?

The daily backup window is a 30-minute window that you specify when creating a file system. Amazon FSx takes the daily automatic backup of your file system during this window. At some point during the daily backup window, storage I/O will be brieﬂy suspended while the backup process initializes (typically a few seconds).

### What is the Daily Backup Retention Period?

The daily backup retention period specified for your file system (7 days by default) determines the number of days your daily automatic backups are kept.

### What Happens to My Backups if I Delete My File System?

When you delete your file system, all automatic daily backups associated with the file system are deleted. Any user-initiated backups you created will remain.

### Can I Take a Backup of Any FSx for Lustre File System?

You can take a backup of any FSx for Lustre file system that has persistent storage and is a standalone file system (i.e., not linked to an Amazon S3 bucket).

Backups aren’t supported on scratch file systems because these file systems are designed for temporary storage and shorter-term processing of data.

Backups aren’t supported on file systems linked to an Amazon S3 bucket because in this case the S3 bucket serves as the primary storage location for your full dataset—the file system does not necessarily contain the full dataset at any given time. With these file systems, FSx for Lustre can automatically export new, changed, or deleted files from the file system to your S3 bucket.

### How Do I Protect My FSx for Lustre Resources Using AWS Backup?

You first enable Amazon FSx as a protected service in AWS Backup. You can then configure backups of your Amazon FSx resources via the AWS Backup console, API or CLI. You can create both scheduled and on-demand backups of Amazon FSx resources via AWS Backup and restore these backups as new Amazon FSx file systems. Amazon FSx file systems can be added to backup plans in the same way as other AWS resources, either by specifying the ARN or by tagging the Amazon FSx file system for protection in the backup plan. Learn more in the [AWS Backup documentation](https://docs.aws.amazon.com/aws-backup/latest/devguide/working-with-other-services.html) .

### How Do I Copy Backups of My Amazon FSx File Systems across AWS Regions and AWS Accounts?

You can configure your backup plans on AWS Backup to periodically create and copy backups of your Amazon FSx file systems to other AWS Regions, other AWS accounts, or both, with your desired frequency and retention policy. For cross-account backup copies, you use your AWS Organizations management account to designate source and destination accounts.

## Pricing and Billing

Close all

### How Will I Be Charged and Billed for My Use of Amazon FSx for Lustre?

You pay only for the resources you use. See the [Amazon FSx for Lustre pricing page](https://aws.amazon.com/fsx/lustre/pricing/) for details.

### How Am I Billed when Scaling the Storage Capacity of My File System?

Storage capacity scaling requests are processed by adding new storage capacity to your file system. You will be billed for new storage capacity once the new file servers have been added to your file system, and the file system status changes from UPDATING to AVAILABLE.

### How Am I Billed when Scaling the Throughput Tier of My File System?

Throughput scaling requests are processed by replacing the file servers powering your file system. You will be billed for your new throughput tier once the file servers have been replaced, and the file system status changes from UPDATING to AVAILABLE.