---
tags:
  - cloud/aws
---
**Amazon EFS** is <mark style="background: #BBFABBA6;">a fully managed service for hosting Network File System (NFS) filesystems in the cloud.</mark>

![[Pasted image 20240212132255.png]]

![[AWS Solutions Architect Skillbuilder#File Storage Overview]]
- It is an implementation of a NFS file share and is accessed using the <mark style="background: #ABF7F7A6;">NFS protocol.</mark>
- **It provides elastic storage capacity and pay for what you use (in contrast to Amazon EBS with which you pay for what you provision).**
- <mark style="background: #ABF7F7A6;">You can configure mount-points in one, or many, AZs.</mark>
- <mark style="background: #ADCCFFA6;">You can mount an AWS EFS filesystem from on-premises systems ONLY if you are using AWS Direct Connect or a VPN connection.</mark>
- Typical use cases include big data and analytics, media processing workflows, content management, web serving, home directories etc.
- <mark style="background: #BBFABBA6;">Uses a pay for what you use model with no pre-provisioning required.</mark>
- <mark style="background: #ABF7F7A6;">AWS EFS can scale up to petabytes.</mark>
- <mark style="background: #CACFD9A6;">AWS EFS is elastic and grows and shrinks as you add and remove data.</mark>
- You can concurrently connect up to thousands of Amazon EC2 instances, from multiple AZs.
- A file system can be accessed concurrently from all AZs in the region where it is located.

![[AWS Solutions Architect Skillbuilder#Amazon EFS]]

The following diagram depicts the various options for mounting an EFS filesystem:

![](https://i.imgur.com/UJjkOFg.png)

- <mark style="background: #BBFABBA6;">Access to AWS EFS file systems from on-premises servers can be enabled via AWS Direct Connect or AWS VPN.</mark>
- <mark style="background: #FFB8EBA6;">You mount an AWS EFS file system on your on-premises Linux server using the standard Linux mount command for mounting a file system via the NFS protocol.</mark>
- The Amazon VPC of the connecting instance must have DNS hostnames enabled.
- EFS provides a file system interface, file system access semantics (such as strong consistency and file locking).
- Data is stored across multiple AZs within a region.
- Read after write consistency.
- Need to create mount targets and choose AZs to include (recommended to include all AZ’s).

- Instances can be behind an Elastic Load Balancer (ELB).
- Amazon EFS is compatible with all Linux-based AMIs for Amazon EC2.
- Using the EFS-to-EFS Backup solution, you can schedule automatic incremental backups of your Amazon EFS file system.

The following table provides a comparison of the storage characteristics of EFS vs EBS:

|   |   |   |
|---|---|---|
||**Amazon EFS**|**Amazon EBS Provisioned IOPS**|
|**Availability and durability**|Data is stored redundantly across multiple AZs|Data is stored redundantly in a single AZ|
|**Access**|Up to thousands of Amazon EC2 instances, from multiple AZs, can connect concurrently to a file system|A single Amazon EC2 instance in a single AZ can connect to a file system|
|**Use cases**|Big data and analytics, media processing and workflows, content management, web serving and home directories|Boot volumes, transactional and NoSQL databases, data warehousing and ETL|

## Backups and Lifecycle Management

- Automatic backups are enabled by default and use AWS Backup.
- Lifecycle management moves files that have not been accessed for a period of time to the EFS Infrequent Access Storage class.

<mark style="background: #FF5582A6;">Amazon EFS Performance</mark>  
There are two performance modes:
- “<mark style="background: #ABF7F7A6;">General Purpose</mark>” performance mode is appropriate for most file systems.
- “<mark style="background: #ABF7F7A6;">Max I/O</mark>” performance mode <mark style="background: #083CA4A6;">is optimized for applications where tens, hundreds, or thousands of EC2 instances are accessing the file system.</mark>

- Amazon EFS <mark style="background: #BBFABBA6;">is designed to burst to allow high throughput levels for periods of time. </mark>  
There are two throughput modes:
- “**Bursting**” – <mark style="background: #D2B3FFA6;">throughput scales with file system size</mark>.
- “**Provisioned**” – <mark style="background: #D2B3FFA6;">Throughput is fixed at the specified amount</mark>.  
![](https://i.imgur.com/7yUw1bP.png)


<mark style="background: #FFF3A3A6;">Amazon EFS file systems are distributed across an unconstrained number of storage servers, enabling file systems to grow elastically to petabyte scale and allowing massively parallel access from Amazon EC2 instances to your data.</mark>

This distributed data storage design means that multithreaded applications and applications that concurrently access data from multiple Amazon EC2 instances can drive substantial levels of aggregate throughput and IOPS.

The table below compares high-level performance and storage characteristics for AWS’s file  (EFS) and block (EBS) cloud storage offerings:

|   |   |   |
|---|---|---|
||**Amazon EFS**|**Amazon EBS Provisioned IOPS**|
|**Per-operation latency**|Low, consistent latency|Lowest, consistent latency|
|**Throughput scale**|10+ GB per second|Up to 2 GB per second|  
![](https://i.imgur.com/r46ZqLn.png)

## Amazon EFS Encryption

- EFS offers the ability to encrypt data at rest and in transit.
- Encryption keys are managed by the AWS Key Management Service (KMS).

Encryption in transit:
- <mark style="background: #BBFABBA6;">Data encryption in transit uses Transport Layer Security (TLS)</mark> 1.2 to encrypt data sent between your clients and EFS file systems.
- <mark style="background: #FFB86CA6;">Encryption in transit is enabled when mounting the file system.</mark>

Encryption at rest:
- Enable encryption at rest in the EFS console or by using the AWS CLI or SDKs.
- <mark style="background: #ADCCFFA6;">Encryption at rest MUST be enabled at file system creation time.</mark>
- Data encrypted at rest is transparently encrypted while being written, and transparently decrypted while being read.

Encryption of data at rest and of data in transit can be configured together or separately.

## Amazon EFS Access Control

- <mark style="background: #CACFD9A6;">When you create a file system, you create endpoints in your VPC</mark> called “**mount targets**”.

When mounting from an EC2 instance, your file system’s DNS name, which you provide in your mount command, resolves to a mount target’s IP address.

You can control who can administer your file system using IAM (user-based and resource-based policies)

You can control the NFS clients that can access your file systems (resource-based policies).

You can control access to files and directories with POSIX-compliant user and group-level permissions.

POSIX permissions allow you to restrict access from hosts by user and group.

EFS Security Groups act as a firewall, and the rules you add define the traffic flow.

Monitoring and Reporting

The Amazon EFS console shows the following monitoring information for your file systems:

- The current metered size.
- The number of mount targets.
- The lifecycle state.

Amazon EFS reports metrics for Amazon CloudWatch.  A few useful metrics are:

- TotalIOBytes – use the daily Sum statistic to determine throughput.
- ClientConnections – use the daily Sum statistic to track the number of connections from EC2 instances.
- BurstCreditBalance – monitor the burst credit balance.

## Logging and Auditing

Amazon EFS is integrated with AWS CloudTrail.

CloudTrail captures all API calls for Amazon EFS as events, including calls from the Amazon EFS console and from code calls to Amazon EFS API operations.


![[Storage- Amazon S3 & EFS]]


# FAQ
## General
### What is Amazon Elastic File System?

Amazon Elastic File System (EFS) is designed to provide serverless, fully elastic file storage that lets you share file data without provisioning or managing storage capacity and performance. With a few selections in the AWS Management Console, you can create file systems that are accessible to [Amazon Elastic Compute Cloud](https://aws.amazon.com/ec2/) (EC2) instances, Amazon container services ([Amazon Elastic Container Service](https://aws.amazon.com/ecs/)  \[ECS\], [Amazon Elastic Kubernetes Service](https://aws.amazon.com/eks/)  \[EKS\], and [AWS Fargate](https://aws.amazon.com/fargate/) ), and [AWS Lambda](https://aws.amazon.com/lambda/)  functions through a file system interface (using standard operating system file I/O APIs). They also support full file system access semantics, such as strong consistency and file locking.

Amazon EFS file systems can automatically scale from gigabytes to petabytes of data without needing to provision storage. Tens, hundreds, or even thousands of compute instances can access an Amazon EFS file system at the same time, and Amazon EFS provides consistent performance to each compute instance. Amazon EFS is designed to be highly durable and highly available. With Amazon EFS, there is no minimum fee or setup costs, and you pay only for what you use.

### What Use Cases Does Amazon EFS Support?

Amazon EFS provides performance for a broad spectrum of workloads and applications: big data and analytics, media processing workflows, content management, web serving, and home directories.

Amazon EFS Standard storage classes are ideal for workloads that require the highest levels of durability and availability.

EFS One Zone storage classes are ideal for workloads such as development, build, and staging environments. They are also ideal for analytics, simulation, and media transcoding, and for backups or replicas of on-premises data that don’t require Multi-AZ resilience.

### When Should I Use Amazon EFS vs. Amazon Elastic Block Store (Amazon EBS) vs. Amazon S3?

AWS offers cloud storage services to support a wide range of storage workloads.

EFS is a [file storage service](https://aws.amazon.com/what-is-cloud-file-storage/)  for use with Amazon compute (EC2, containers, serverless) and on-premises servers. EFS provides a file system interface, file system access semantics (such as strong consistency and file locking), and concurrently accessible storage for up to thousands of EC2 instances.

[Amazon EBS](https://aws.amazon.com/ebs/)  is a block-level storage service for use with EC2. EBS can deliver performance for workloads that require the lowest-latency access to data from a single EC2 instance.

[Amazon S3](https://aws.amazon.com/s3/)  is an object storage service. S3 makes data available through an internet API that can be accessed anywhere.

[Learn more](https://aws.amazon.com/efs/when-to-choose-efs/)  about what to evaluate when considering Amazon EFS.

### What Regions is Amazon EFS Currently Available In?

Refer to [Regional Products and Services](https://aws.amazon.com/about-aws/global-infrastructure/regional-product-services/) for details of Amazon EFS service availability by Region.

### How Do I Start Using Amazon EFS?

To use Amazon EFS, you must have an AWS account. If you don’t already have one, you can sign up for an AWS account, and instantly get access to the [AWS Free Tier](https://aws.amazon.com/free/) .

Once you have created an AWS account, refer to the EFS [Getting started](https://docs.aws.amazon.com/efs/latest/ug/getting-started.html)  guide to begin using EFS. You can create a file system through the console, the AWS Command Line Interface (CLI) and the EFS API (and various language-specific SDKs).

### How Do I Access a File System from an EC2 Instance?

To access your file system, mount the file system on an EC2 Linux-based instance using the standard Linux mount command and the file system’s DNS name. To simplify accessing your Amazon EFS file systems, we recommend using the Amazon EFS mount helper utility. Once mounted, you can work with the files and directories in your file system like you would with a local file system.

EFS uses the Network File System version 4 (NFS v4) protocol. For a step-by-step example of how to access a file system from an EC2 instance, see the [guide here](https://docs.aws.amazon.com/efs/latest/ug/gs-mount-fs-on-ec2instance-and-test.html) .

### How Do I Manage a File System?

Amazon EFS is a fully managed service, so all of the file storage infrastructure is managed for you. When you use Amazon EFS, you avoid the complexity of deploying and maintaining complex file system infrastructure. An Amazon EFS file system grows and shrinks automatically as you add and remove files, so you don’t need to manage storage procurement or provisioning.

You can administer a file system through the console, CLI, or the EFS API (and various language-specific SDKs). The console, API, and SDK provide the ability to create and delete file systems, configure how file systems are accessed, create and edit file system tags, enable features such as Provisioned Throughput and Lifecycle Management, and display detailed information about file systems.  

### How Do I Load Data into a File System?

[AWS DataSync](https://aws.amazon.com/datasync/)  provides a fast way to securely sync existing file systems with Amazon EFS. DataSync works over any network connection, including with [AWS Direct Connect](https://aws.amazon.com/directconnect/)  or [AWS VPN](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_VPN.html) . EFS, DataSync, and Direct Connect without Amazon or AWS. You can also use standard Linux copy tools to move data files to Amazon EFS.

For more information about accessing a file system from an on-premises server, see the [On-premises access](https://aws.amazon.com/efs/faq/)  section of this FAQ.

For more information about moving data to the Amazon cloud, see the [Cloud Data Migration](https://aws.amazon.com/cloud-data-migration/)  page.

## Scale and Performance

Close all

### How much Data Can I Store?

You can store petabytes of data with Amazon EFS. Amazon EFS file systems are elastic, automatically growing and shrinking as you add and remove files. There’s no need to provision file system size up front, and you pay only for what you use.

### How Many EC2 Instances Can Connect to a File System?

Amazon EFS supports one to thousands of Amazon Elastic Compute Cloud (EC2) instances connecting to a file system concurrently.

### How Many File Systems, Mount Targets, or Access Points Can I Create?

Please visit the [Amazon EFS Limits page](https://docs.aws.amazon.com/efs/latest/ug/limits.html) for more information on Amazon EFS limits.

### What Latency, Throughput, and IOPS Performance Can I Expect for My Amazon EFS File System?

The expected performance for your Amazon EFS file system depends on its specific configuration (for instance, storage class and thoroughput mode) and the specific file system operation type (read or write). Please see the [File System Performance documentation for more information on expected latency](https://docs.aws.amazon.com/efs/latest/ug/limits-throughput.html) , maximum throughput, and maximum IOPS performance for Amazon EFS file systems.

### What Throughput Modes Are Available for My File System?

Elastic Throughput is the default throughput mode and is suitable for most file workloads. With the default Elastic Throughput mode, performance automatically scales with your workload activity, and you only pay for the throughput you use (data transferred for your file systems per month). Elastic Throughput is ideal if you’re unsure of your application’s peak throughput needs or if your application is very spiky, with a low baseline activity (such that it uses less than 5% of capacity on average when you provision for peak needs).

You can optionally change your throughput mode to Provisioned Throughput if you know your workload’s peak throughput requirements and you expect your workload to consume a higher share (more than 5% on average) of your application’s peak throughput capacity.

The amount of throughput you can deliver depends on the throughput mode you choose. Please see the documentation on File System Performance for more information.  Please visit [File System Performance](https://docs.aws.amazon.com/efs/latest/ug/limits-throughput.html) for more information.

### How Do I Monitor My Amazon EFS File System?

You can monitor your file system using [Amazon CloudWatch](https://aws.amazon.com/cloudwatch/) or from the Monitoring tab in the Amazon EFS Console. Please visit the documentation on [Monitoring Amazon EFS](https://docs.aws.amazon.com/efs/latest/ug/monitoring_overview.html) for more information.

## Durability and Availability

Close all

### What Types of File Systems Does Amazon EFS Offer?

Amazon EFS offers two file system types that you can choose from based on your durability and availability needs. EFS Regional file systems (recommended) offer the highest levels of durability and availability by storing data with and across multiple Availability Zones (AZs). EFS One Zone file systems store data redundantly within a single AZ, so data in these file systems will be unavailable and might be lost during a disaster or other fault within the AZ.

### How Durable is Amazon EFS?

Amazon EFS is designed to provide 99.999999999% (11 nines) of durability over a given year. EFS Regional file systems are designed to sustain data if an AZ is lost. Because EFS One Zone file systems store data in a single AZ, data stored in these storage classes might be lost during a disaster or other fault within the AZ.  

As with any environment, the best practice is to have a backup and to put in place safeguards against accidental deletion. For Amazon EFS data, the best practice includes replicating your file system across Regions using Amazon EFS Replication, and a functioning, regularly tested backup using AWS Backup. File systems using EFS One Zone storage classes are configured to automatically back up files by default at file system creation.

### How is Amazon EFS Designed to provide High Durability and Availability?

Every EFS Regional file system object (such as directory, file, and link) is redundantly stored across multiple AZs. With EFS One Zone file systems, your data is redundantly stored within a single AZ. Amazon EFS is designed to sustain concurrent device failures by quickly detecting and repairing any lost redundancy.  

EFS file system data is accessed using AZ-specific EFS mount targets, which are designed to be highly available within an AZ. EFS Regional file systems support concurrent access from EFS mount targets in all AZs in the Region where they are located. That means you can architect your application to failover from one AZ to other AZs in the Region to achieve the highest level of application availability. EFS One Zone file systems support only one highly available EFS mount target in a single AZ, which means data may become unavailable during a disaster or other fault within that AZ. For more information on availability, see the [Amazon EFS Service Level Agreement](https://aws.amazon.com/efs/sla/).

### What Additional Failure Modes Should I Consider when Using Amazon EFS One Zone File Systems?

EFS One Zone file systems are not resilient to a complete AZ outage. During an AZ outage, you will experience a loss of availability, because your file system data is not replicated to a different AZ. During a disaster or fault within an AZ affecting all copies of your data, you might experience loss of data that has not been protected using [EFS Backups or EFS Replication](https://aws.amazon.com/efs/faq/). EFS Backups are enabled by default for all EFS One Zone file systems.

## Storage Classes and Lifecycle Management

Close all

### What Storage Classes Does Amazon EFS Offer?

Amazon EFS offers three storage classes: EFS Standard, EFS Infrequent Access, and EFS Archive. Data that is frequently accessed tends to have higher performance needs, so EFS provides an SSD-powered EFS Standard class designed to deliver sub-millisecond latencies. For data that’s infrequently accessed, you can use EFS’s two cost-optimized storage classes that provide low double-digit millisecond latencies: EFS Infrequent Access (IA), designed for data accessed only a few times a quarter, and EFS Archive, designed for data accessed a few times a year or less. EFS IA offers an up to 95% lower cost than EFS Standard for infrequently accessed data. Providing a more cost-optimized experience for even colder data, EFS Archive offers an up to 50% lower cost than EFS Infrequent Access, with a higher request charge when that data is accessed. EFS Archive is optimized for and supported on EFS Regional file systems using EFS’s default Elastic Throughput mode. See [EFS storage classes](https://aws.amazon.com/efs/storage-classes/) and [EFS Pricing](https://aws.amazon.com/efs/pricing/) for more information.

### How Do I Move Files to EFS Standard, IA and Archive Storage Classes?

By enabling EFS Lifecycle Management, you can automatically tier files between storage classes based on your access patterns. The default, recommended lifecycle policy will tier files from EFS Standard to EFS IA after 30 consecutive days without access and to EFS Archive after 90 consecutive days without access. You can also specify a custom policy for transitioning files between storage classes based on the number of days since a file’s last access.

You can also enable EFS Intelligent-Tiering to promote files from EFS IA and EFS Archive back to EFS Standard when they are accessed, which provides subsequent reads of those files with the faster, sub-millisecond latencies of EFS Standard. Once promoted, these files will transition back to the appropriate IA or Archive storage class based on your lifecycle policy.

### What Performance Can I Expect from EFS’s Cost-optimized IA and Archive Storage Classes?

Compared to the EFS Standard class, EFS IA and Archive offer the same throughput and IOPS scalability but with higher first-byte latencies (i.e., low double-digit millisecond read latencies vs. sub-millisecond read latencies on EFS Standard). For more information, see the [Amazon EFS performance](https://docs.aws.amazon.com/efs/latest/ug/performance.html) documentation.

### Is there a Minimum Storage Duration for EFS’s Cost-optimized Storage Classes, EFS IA and EFS Archive?

EFS IA has no minimum storage duration. Data that is tiered to EFS Archive has a minimum storage duration of 90 days. Files deleted or truncated prior to the minimum duration will incur a pro-rated charge for the remaining days, based on the size of the file prior to the corresponding action.

### Is there a Minimum File Size for EFS’s Cost-optimized Storage Classes, EFS IA and EFS Archive?

EFS’s cost-optimized storage classes (IA, Archive) are designed for storing colder, inactive data, which is typically comprised of larger files. There is no minimum file size for IA or Archive, but files tiered to these storage classes that are smaller than 128 KiB will incur storage charges as if they were 128 KiB.

## Data Protection

Close all

### What is Amazon EFS Replication?

Amazon EFS Replication copies your file system data into a new or existing file system in the Region of your choice. It keeps the two file systems synchronized by automatically transferring only incremental changes without requiring additional infrastructure or a custom process. EFS Replication is designed to provide a recovery point objective (RPO) and a recovery time objective (RTO) of minutes, helping you meet your compliance and business continuity goals.

### Why Should I Use EFS Replication?

You should use EFS Replication to maintain a replica of your file system many miles apart for disaster recovery, compliance, or business continuity planning. In the event of a disaster, you can failover to your replica file system, and resume operations for your business-critical applications within minutes. Once the disaster event is over, you can failback by transferring only incremental changes from your replica back to your original file system. While EFS Replication is enabled, your applications can use the replica file system in read-only mode for low network latency cross-Region access. With Amazon EFS Replication, you can configure your replica file system independent of your original file system to use cost-optimized storage classes and shorter age-off lifecycle management policy to save up to 92% on your costs. EFS Replication also makes it streamlined to monitor and alarm on your RPO status using Amazon CloudWatch.

### Is My Replica File System Point-in-time Consistent?

No. EFS Replication doesn't provide point-in-time consistent replication. EFS Replication publishes a timestamp metric on Amazon CloudWatch called TimeSinceLastSync. All changes made to your source file system at least as of the published time will be copied over to the replica. Changes to your source file system after the recorded time might not have be replicated over. You can monitor the health of your EFS Replication using Amazon CloudWatch. If you interrupt the replication process due to a disaster recovery event, files from the source file system might have transferred but are not yet copied to their final locations. These files and their contents can be found on your replica file system in a lost+found directory created by EFS Replication under the root directory.

### What is Amazon EFS Backup?

Amazon EFS Backup is powered by AWS Backup, which is a fully managed backup service that centrally manages and automates backups of your Amazon EFS file systems. It protects your file system against a data loss event by making incremental copies of your file system in a centralized location automatically, on a schedule. AWS Backup provides a centralized console, automated backup scheduling, backup retention management, and restore activity. To learn more please read the [AWS Backup documentation](https://docs.aws.amazon.com/aws-backup/latest/devguide/whatisbackup.html) or [FAQs](https://aws.amazon.com/backup/faqs/).

### How Does Amazon EFS Backup Work?

Amazon EFS is natively integrated with AWS Backup. You can use the EFS console, API, and AWS Command Line Interface (AWS CLI) to enable automatic backups, which uses a default backup plan with the AWS Backup recommended settings. During the initial backup, a copy of the entire file system is made in the backup vault. All subsequent backups of that file system are incremental in nature, i.e. only files and directories that have been changed, added, or removed are copied. With each incremental backup, AWS Backup retains the necessary reference data to allow a full restore. In the event of data loss, you can perform a full or partial restore of your file system using the AWS Backup console or the CLI.   

## Security

Close all

### How Do I Control Which Amazon EC2 Instances Can Access My File System?

You control which EC2 instances can access your file system using [VPC security group rules](https://docs.aws.amazon.com/efs/latest/ug/security-considerations.html) and IAM policies. Use VPC security groups to control the network traffic to and from your file system. Attach an IAM policy to your file system to control which clients can mount your file system and with what permissions, and use EFS Access Points to manage application access. Control access to files and directories with POSIX-compliant [user and group-level permissions](https://docs.aws.amazon.com/efs/latest/ug/accessing-fs-nfs-permissions.html) .

### How Can I Use IAM Policies to Manage File System Access?

Using the Amazon EFS console, you can apply common policies to your file system, such as disabling root access, enforcing read-only access, or enforcing that all connections to your file system are encrypted. You can also apply [more advanced policies](https://docs.aws.amazon.com/efs/latest/ug/auth-and-access-control.html) , such as granting access to specific IAM roles, including those in other AWS accounts.

### What is an Amazon EFS Access Point?

An EFS Access Point is a network endpoint that users and applications can use to access an EFS file system and enforce file and folderlevel permissions (POSIX) based on fine-grained access control and policy-based permissions defined in IAM.

### Why Should I Use Amazon EFS Access Points?

EFS Access Points gives you the flexibility to create and manage multi-tenant environments for your file applications in a cloud-native way, helping you simplify data sharing. Unlike traditional POSIX ACLs to control file system access, or Kerberos to control authentication, both requiring complex set-up, management, and maintenance, and which often introduce risk, EFS Access Points integrates with IAM to enable cloud native applications to use POSIX-based shared file storage. Use cases that can benefit from Amazon EFS Access Points include container-based environments where developers build and deploy their own containers, data science applications that require access to production data, and sharing a specific directory in your file system with other AWS accounts.

### How Do Amazon EFS Access Points Work?

When you create an Amazon EFS Access Point, you can configure an operating system user and group, and a root directory for all connections that use it. If you specify the root directory’s owner, EFS will automatically create it with the permissions you provide the first time a client connects to the access point. You can also update your file system’s IAM policy to apply to your access points. For example, you can apply a policy that requires a specific IAM identity in order to connect to a given access point. For more information, see the [Amazon EFS user guide](https://docs.aws.amazon.com/efs/latest/ug/efs-access-points.html).

### What is Amazon EFS Encryption?

Amazon EFS offers the ability to encrypt data at rest and in transit.

Data encrypted at rest is transparently encrypted while being written, and transparently decrypted while being read, so you don’t have to modify your applications. Encryption keys are managed by the AWS KMS, eliminating the need to build and maintain a secure key management infrastructure.

Data encryption in transit uses industry-standard Transport Layer Security (TLS) 1.2 to encrypt data sent between your clients and EFS file systems.

Encryption of data at rest and data in transit can be configured together or separately to help meet your unique security requirements.

For more details, see the [user documentation on Encryption](https://docs.aws.amazon.com/efs/latest/ug/encryption.html).

### What is the AWS Key Management Service (KMS)?

AWS KMS is a managed service that makes it easier for you to create and control the encryption keys used to encrypt your data. AWS KMS is integrated with AWS services, including EFS, EBS, and S3, making it simpler to encrypt your data with encryption keys that you manage. [AWS KMS](https://aws.amazon.com/kms/)  is also integrated with [AWS CloudTrail](https://aws.amazon.com/cloudtrail/)  to provide you with logs of all key usage to help meet your regulatory and compliance needs.

### How Do I Enable Encryption for My Amazon EFS File System?

You can enable encryption at rest in the EFS console by using the CLI or SDKs. When creaking a new file system in the EFS console, select “Create File System” and then select the checkbox to enable encryption.

Data can be encrypted in transit between your Amazon EFS file system and its clients by using the Amazon EFS mount helper.

Encryption of data at rest and data in transit can be configured together or separately to help meet your unique security requirements.

For more details, see the [user documentation on Encryption](https://docs.aws.amazon.com/efs/latest/ug/encryption.html).

### Does Encryption Impact Amazon EFS Performance?

Encrypting your data has a minimal effect on I/O latency and throughput.

## On-premises Access

Close all

### How Do I Access an Amazon EFS File System from Servers in My On-premises Datacenter?

Change to To access EFS file systems from on premises, you must have a [Direct Connect](https://aws.amazon.com/directconnect/)  or [AWS VPN](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_VPN.html)  connection between your on-premises datacenter and your Amazon Virtual Private Cloud (VPC).

You mount an Amazon EFS file system on your on-premises Linux server using the standard Linux mount command for mounting a file system using the NFS v4.1 protocol.

For more information about accessing Amazon EFS file systems from on-premises servers, see the [documentation](https://docs.aws.amazon.com/efs/latest/ug/how-it-works.html) .

### What Can I Do by Enabling Access to My Amazon EFS File Systems from My On-premises Servers?

You can mount your Amazon EFS file systems on your on-premises servers, and move file data to and from Amazon EFS using standard Linux tools and scripts or AWS DataSync. The ability to move file data to and from Amazon EFS file systems allows for three use cases.

First, you can migrate data from on-premises datacenters to permanently reside in EFS file systems.

Second, you can support cloud bursting workloads to off-load your application processing to the cloud. You can move data from your on-premises servers into your Amazon EFS file systems, analyze it on a cluster of EC2 instances in your Amazon VPC, and store the results permanently in your Amazon EFS file systems or move the results back to your on-premises servers.

Third, you can periodically copy your on-premises file data to Amazon EFS to support backup and disaster recovery scenarios.

### Can I Access My Amazon EFS File System Concurrently from My On-premises Datacenter Servers as well as EC2 Instances?

Yes. You can access your Amazon EFS file system concurrently from servers in your on-premises datacenter as well as EC2 instances in your Amazon VPC. Amazon EFS provides the same file system access semantics, such as strong data consistency and file locking, across all EC2 instances and on-premises servers accessing a file system.

### What is the Recommended Best Practice when Moving File Data to and from On-premises Servers?

Because of the propagation delay tied to data traveling over long distances, the network latency of the network connection between your on-premises datacenter and your Amazon VPC can be tens of milliseconds. If your file operations are serialized, the latency of the network connection directly impacts your read and write throughput; in essence, the volume of data you can read or write during a period of time is bounded by the amount of time it takes for each read and write operation to complete. To maximize your throughput, parallelize your file operations so that multiple reads and writes are processed by Amazon EFS concurrently. Standard tools like GNU parallel help you to parallelize the copying of file data. For more information, see the online [documentation](https://www.gnu.org/software/parallel/) .

### How Do I Copy Existing Data from On-premises File Storage to Amazon EFS?

There are a number of methods to copy existing on-premises data into Amazon EFS. AWS DataSync provides a fast and simple way to securely sync existing file systems into EFS and works over any network, including AWS Direct Connect.

[AWS Direct Connect](https://aws.amazon.com/directconnect/) provides a high-bandwidth and lower-latency dedicated network connection over which you can mount your EFS file systems. Once mounted, you can use DataSync to copy data into EFS up to 10 times faster than standard Linux copy tools.

For more information on AWS DataSync, see the [Data transfer section](https://aws.amazon.com/efs/faq/) of this FAQ.

## Data Transfer

Close all

### What AWS-native Options Do I Have to Transfer Data into My File System?

[DataSync](https://aws.amazon.com/datasync/)  is an online data transfer service that makes it faster and simpler to move data between on-premises storage and Amazon EFS. DataSync uses a purpose-built protocol to accelerate and secure transfer over the internet or Direct Connect, at speeds up to 10 times faster than open-source tools. Using DataSync, you can perform one-time data migrations, transfer on-premises data for timely in-cloud analysis, and automate replication to AWS for data protection and recovery.

[AWS Transfer Family](https://aws.amazon.com/aws-transfer-family/)  is a fully managed file transfer service that provides support for Secure File Transfer Protocol (SFTP), File Transfer Protocol over SSL (FTPS), and File Transfer Protocol (FTP). The AWS Transfer Family provides you with a fully managed, highly available file transfer service with auto scaling capabilities, eliminating the need for you to manage file transfer–related infrastructure. Your end users’ workflows remain unchanged, while data uploaded and downloaded over the chosen protocols is stored in your Amazon EFS file system.

### How Do I Transfer Data into or out of My Amazon EFS File System?

To get started with DataSync, you can use the console or CLI to connect the agent to your on-premises or in-cloud file systems using the Network File System (NFS) protocol, select your Amazon EFS file system, and start copying data. You must first deploy a software agent that is available for download from the console, except when copying files between two Amazon EFS file systems.

To get started with AWS Transfer Family, first ensure that your file system’s directories are accessible by the POSIX users that you plan to assign to AWS Transfer. Then you can use the console, CLI, or API to create a Transfer Family endpoint and user(s). Once complete, your end users can use their SFTP, FTP, or FTPS clients to access data stored in your Amazon EFS file system.

### Can Amazon EFS Data Be Transferred between Regions?

You can use DataSync to transfer files between two Amazon EFS file systems, including ones in different AWS Regions. AWS Transfer Family endpoints must be in the same Region as your Amazon EFS file system.

### Can I Access My File System with Another AWS Account?

Yes. You can use DataSync to copy files to an Amazon EFS file system in another AWS account.

You can also configure your Amazon EFS file system to be accessed by AWS Transfer Family using another account as long as the account has been granted permissions to do so. To learn more about granting Transfer Family permissions to external AWS accounts via file system policies, see the [documentation](https://docs.aws.amazon.com/efs/latest/ug/using-aws-transfer-integration.html) .

## Compatibility

Close all

### What Interoperability and Compatibility is there between Existing AWS Services and Amazon EFS?

EFS is integrated with a number of other AWS services, including CloudWatch, AWS CloudFormation, CloudTrail, IAM, and AWS tagging services.

CloudWatch helps you monitor file system activity using metrics. CloudFormation helps you create and manage file systems using templates.

CloudTrail helps you record all EFS API calls in log files.

IAM helps you control who can administer your file system. AWS tagging services helps you label your file systems with metadata that you define.

You can plan and manage your Amazon EFS file system costs by using AWS Budgets. You can work with AWS Budgets from the AWS Billing and Cost Management console. To use [AWS Budgets](https://aws.amazon.com/aws-cost-management/aws-budgets/) , you create a monthly cost budget for your Amazon EFS file systems.

### What Type of Locking Does Amazon EFS Support?

Locking in Amazon EFS follows the NFS v4.1 protocol for advisory locking and allows your applications to use both whole file and byte range locks.

### Are File System Names Global (like S3 Bucket names)?

Every file system has an automatically generated ID number that is globally unique. You can tag your file system with a name, and these names don’t need to be unique.

## Pricing and Billing

Close all

### How much Does Amazon EFS Cost?

With Amazon EFS, you pay only for the primary and backup storage you use and for your read, write, and tiering activity to your EFS file system. You pay for read and write access using Elastic Throughput (but you can optionally provision throughput performance up-front using Provisioned Throughput), and for tiering data to EFS’s Infrequent Access and Archive storage classes.

Amazon EFS offers three storage classes: EFS Standard, which delivers sub-millisecond latency performance for actively-used data; EFS Infrequent Access (EFS IA), which is cost-optimized for data accessed only a few times a quarter; and EFS Archive, which is cost-optimized for long-lived data accessed a few times a year or less.

EFS also offers data protection for your files with EFS Backup and EFS Replication. With EFS Backup, you pay only for the amount of backup storage you use and the amount of backup data you restore in the month. There is no minimum fee and there are no setup charges. Visit [AWS Backup](https://aws.amazon.com/backup/) to learn more. Use EFS Replication to replicate your file system to a Region or Availability Zone (AZ) of your choice without having to manage additional infrastructure or custom processes.

You can estimate your monthly bill using the [Amazon EFS Pricing Calculator](https://calculator.aws/#/addService/EFS).

### How Will I Be Charged for the Use of Amazon EFS?

There are no setup charges or commitments to begin using Amazon EFS. At the end of the month, you will automatically be charged for that month’s usage. You can view your charges for the current billing period at any time by logging into your Amazon Web Services account, and selecting the 'Billing Dashboard' associated with your console profile.

With the [AWS Free Usage Tier\*](https://aws.amazon.com/free/), your usage for the Free Tier is calculated each month across all AWS Regions except the AWS GovCloud Region and automatically applied to your bill; unused monthly usage will not roll over to the next month. Upon sign up, new EFS customers receive 5 GB of Amazon EFS Standard each month for one year. The AWS Free Tier is not applicable to files stored in the EFS One Zone file system type. Restrictions apply; see [offer terms](https://aws.amazon.com/free/?all-free-tier.sort-by=item.additionalFields.SortRank&all-free-tier.sort-order=asc&awsf.Free%20Tier%20Types=*all&awsf.Free%20Tier%20Categories=*all) for more details.

Amazon EFS charges you for the following types of usage. Note that the calculations below assume there is no AWS Free Tier in place.

**Storage Used:**

The Amazon EFS amount billed in a month is based on storage, throughput, and data protection usage in a month. The storage costs are calculated based on the average storage space used throughout the month. Your storage usage is measured in "GB-Month," which are added up at the end of the month to generate your monthly charges. 

### Storage Example

The following example reflects a scenario where your file access patterns change over time, and includes each of EFS IA and EFS Archive's pricing dimensions. The example assumes that the two EFS Lifecycle policies to move files between EFS Standard, EFS Infrequent Access (IA), and EFS Archive are set.

Assume that your file system is located in the US East (N. Virginia) Region. At the beginning of a 31-day month, your file system stores 200 GB of files on EFS Standard, 500 GB of files on EFS IA, and 2 TB of files on EFS Archive. On the 15th day of the month, EFS Lifecycle Management moves 50% of your EFS Standard files to the EFS IA class and 10% of your EFS IA files to the EFS Archive class after 14 days of having not been accessed. Once per month, 10 different clients read 800 GB of files from your EFS IA and 100 GB of files from your EFS Archive classes.

First, we calculate the pro-rated storage usage:

**Standard Storage:**  
200 GB of EFS Standard storage for 14 days (GB-Hours): 200 GB x 14 days x (24 hours / day) = 67,200 GB-Hours  
100 GB of EFS Standard storage for 17 days (GB-Hours): 100 GB x 17 days x (24 hours / day) = 40,800 GB-Hours  
Total EFS Standard storage usage (GB-Hours): 67,200 GB-Hours + 40,800 GB-Hours = 108,000 GB-Hours

**IA Storage:**  
500 GB of EFS IA for 14 days (GB-Hours): 500 GB x 14 x (24 hours / day) = 168,000 GB-Hours  
100 GB of files from EFS Standard to EFS IA for 17 days (GB-Hours) = 100 GB x 17 x (24 hours / day) = 40,800 GB-Hours  
450 GB of EFS IA (after 50 GB is moved to EFS Archive) = 450 GB x 17 x (24 hours / day) = 183,600 GB-Hours

Total EFS IA usage (GB-Hours): 168,000 GB-Hours + 40,800 GB-Hours + 326,400 GB-Hours = 392,400 GB-Hours

**Archive Storage:**  
2 TB of EFS IA for 31 days (GB-Hours): 1,000 GB x 14 x (24 hours / day) = 1,488,000 GB-Hours  
50 GB of files from EFS IA to EFS Archive for 17 days (GB-Hours): 50 GB x 17 x (24 hours / day) = 20,400 GB-Hours  
Total EFS Archive storage usage (GB-Hours): 1,488,000 GB-Hours + 20,400 GB-Hours = 1,508,400 GB-Hours

Next, we convert the storage usage into GB-months and calculate the storage charge:  
Total EFS Standard charge: 108,000 GB-Hours x (1 month / 744 hours) x $0.30/GB-month = $43.55  
Total EFS IA charge: 392,400 GB-Hours x (1 month / 744 hours) x $0.0165/GB-month = $8.70  
Total EFS Archive charge: 1,508,400 GB-Hours x (1 month / 744 hours) x $0.008/GB-month = $16.22  
Total EFS storage charge: $43.55 + $8.70 + $16.22 = $68.47

Next, we calculate the access charges for files in EFS IA and EFS Archive:

**IA Data Tiering:**  
Data Tiering (files moved from EFS Standard to EFS IA): 100 GB \* $0.01/GB = $1.00  
Lifecycle transition to EFS Standard due to reads to files in EFS IA: 800 GB \* $0.01/GB = $8.00 (once for 10 clients)  
Total EFS IA access charges: $1.00 + $8.00 = $9.00

**Archive Data Tiering:**  
Data Tiering (files moved from Infrequent Access to Archive): 50 GB \* $0.03/GB = $1.50  
Lifecycle transition to EFS IA due to reads to files in EFS Archive: 100 GB \* $0.06/GB = $6.00 (once for 10 clients)  
Total EFS IA access charges: $1.50 + $6.00 = $7.50  
Total EFS access charge: $9.00 + $7.50 = $16.50

Finally, we calculate the total EFS charge for the month:

Total monthly charges = Total storage charge + Total access charge = $68.47 + $16.50 = $84.97 (TCO - $0.0315/GB)

### Throughput Used

You can access your data for read and write operations using Elastic Throughput. With Elastic Throughput, performance automatically scales with your workload activity, and you only pay for the throughput you use (data transferred for your file systems per month). The Elastic Throughput amount billed in a month is based on the read and write data transferred within a month and measured in “GB transferred.”

You can use Provisioned Throughput if you know your application’s throughput usage and peak throughput requirements. Provisioned Throughput amount billed in a month is based on the average throughput provisioned in excess of what your EFS Standard allows for the month, up to the prevailing Bursting baseline throughput limits in the AWS Region, and measured in "MB/s-Month."

**Elastic Throughput Example:**

Assume your file system is located in the US East (N. Virginia) Region and has 100 GB of EFS Standard storage, for the entirety of a 31-day month. Assume that your workload’s data transfer is 75% read operations and 25% write operations, drives a peak throughput of 100 MB/s for 3 hours a day and 3 days a week, and is idle for the remainder of the time.  

Total monthly Elastic Throughput charge

Assuming all of your data transferred is to EFS Standard Storage, at the end of the month, you would have the following usage in GB:

Total Elastic Throughput Data (GB) in the month: 100 MB/s x (60 minutes x 60 seconds x 3 hours) x 3 days x 4 weeks/1000 = 12,960 GB  
Total Elastic Throughput Read Data (GB): 75% x 12,960 GB = 9,720 GB  
Total Elastic Throughput Write Data (GB): 25% x 12,960 GB = 3,240 GB

We then calculate the total monthly charges for Elastic Throughput: 

Elastic Throughput Read Data charges: 9,720 GB x $0.03/GB = $291.60  
Elastic Throughput Write Data charges: 3,240 GB x $0.06/GB = $194.40  
We then calculate the total monthly charges for Elastic Throughput:  
Total Monthly Elastic Throughput Charge = $291.60 + $194.40 = $486.00

**Provisioned Throughput Example:**

Assuming the same assumptions as the Elastic Throughput example above (your file system is located in the US East (N. Virginia) Region and has 100 GB of EFS Standard storage, for the entirety of a 31-day month. Assume that your workload’s data transfer is 75% read operations and 25% write operations, drives a peak throughput of 100 MB/s for 3 hours a day and 3 days a week, and  
is idle for the remainder of the time). The throughput amount billed in a month is based on the average throughput provisioned in excess of what your EFS Standard storage allows for the month (50 KBps of Baseline throughput per 1 GB of Standard storage)

Baseline throughput (MB/s-Month) =100 GB standard storage \* 50 KBps/1000 = 5 MB/s-Month.  
Total billable Provisioned Throughput (MB/s-Month) = Throughput Configured –  
Baseline throughput = 100 MB/s-Month – 5 MB/s-Month = 95 MB/s-Month  
Total monthly Provisioned Throughput Charge = 95 MB/s-Month \* $6/MB/s-month = $570.00

### Data Protection

You may optionally use EFS Replication or AWS Backup to protect your data. With EFS Replication, you pay for the storage, access charges from Infrequent Access and Archive classes, and data transfer changes if your destination file system is in a different AWS Region. With AWS Backup, you pay for the average amount of data backed up and restored in a month.

**Replication**

This example reflects a scenario where you are replicating file systems across Regions using EFS Replication. The example is focused on costs directly related to EFS Replication.

Assume you have an EFS file system in the US East (North Virginia) Region with 1 TB of data. This file system is being replicated to the US West (Oregon) Region. Assume the destination file system uses a 7-day EFS Lifecycle Management Policy to move files into the EFS IA class.

When replication is first turned on, the entire source file system is copied to the destination file system. The replicated data will first land in the EFS Standard class in the destination file system. If files aren’t accessed for the duration of the EFS Lifecycle Management policy (7 days), they will move to the EFS IA class.

**Initial sync:**

First, we calculate the pro-rated storage usage for the destination file system:  
Total EFS Standard usage (GB-hours): 1,000 GB \* 7 days \* (24 hours / day) = 168,000 GB-hours  
Total EFS IA usage (GB-hours): 1,000 GB \* 24 days \* (24 hours / day / 31-day month) = 576,000 GB-hours

Next, we convert the storage usage into GB-months and calculate the storage charge for the destination file system:

Total EFS Standard charge: 168,000 \* (1 month / 744 hours) \* $0.30/GB-month = $67.74  
Total EFS IA charge: 576,000 \* (1 month / 744 hours) \* $0.025/GB-month = $19.36  
Total storage charges for initial sync = $67.74 + $19.36 = $87.10  
Then we calculate the Data transfer charges for the source file system’s initial replication to the destination file system:  
Total EFS Replication data transfer charges for 1 TB of data: 1,000 GB \* $0.02/GB = $20.00

Total charges for initial sync = Total storage charges for initial sync + Total data transfer charges for initial sync = $87.10 + $20.00 = $107.10

**Incremental replication:**

Consider that the source file systems add 150 GB of new data after 7 days. The new data will be replicated to the destination file system and will reside in the EFS Standard class for 7 days based on the Lifecycle Management Policy as before. The pro-rated storage usage for 150 GB of new data is calculated as follows:

Total EFS Standard usage (GB-hours): 150 GB \* 7 days \* (24 hours / day) = 25,200 GB-hours  
Total EFS IA usage (GB-hours): 150 GB \* 17 days \* (24 hours / day) = 61,200 GB-hours

Next, we convert the storage usage into GB-months and calculate the storage charge for the 150 GB of new data added to the destination file system: 

Total EFS Standard charge: 25,200 \* (1 month / 744 hours) \* $0.30/GB-month = $10.16  
Total EFS IA charge: 61,200 \* (1 month / 744 hours) \* $0.025/GB-month = $2.06  
Total storage charges for incremental replication = $10.16 + $2.06 = $12.22

Lastly, we calculate the data transfer charges for 150 GB of incremental data:

Total data transfer charges for incremental replication: 150 GB \* $0.02/GB = $3.00  
Total charges for incremental replication = Total storage charges for incremental replication + Total data transfer charges for incremental replication = $12.22 + $3.00 = $15.22

Total charges related to EFS Replication = Total charges for initial sync + Total charges for incremental replication = $107.10 + $15.22 = $122.32

**Backup**

See [AWS Backup Pricing](https://aws.amazon.com/efs/pricing/) for Backup pricing examples.

For more EFS pricing information, visit the [Amazon EFS Pricing page](https://aws.amazon.com/efs/pricing/).

### Do Your Prices Include Taxes?

Except as otherwise noted, our prices are exclusive of applicable taxes and duties, including VAT and applicable sales tax. For customers with a Japanese billing address, use of AWS services is subject to Japanese Consumption Tax. [Learn more](https://aws.amazon.com/c-tax-faqs/) .

## Access from AWS Services

Close all

### Can I Access Amazon EFS from Amazon ECS Containers?

Yes. You can access EFS from containerized applications launched by [Amazon ECS](https://aws.amazon.com/ecs/) using both EC2 and Fargate launch types by referencing an EFS file system in your task definition. Find instructions for getting started in the [ECS documentation](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/tutorial-efs-volumes.html) .

### Can I Access Amazon EFS from Amazon Elastic Kubernetes Service (EKS) Pods?

Yes. You can access EFS from containerized applications launched by [Amazon EKS](https://aws.amazon.com/eks/) , with either [EC2](https://aws.amazon.com/ec2/)  or [Fargate](https://aws.amazon.com/fargate/)  launch types, using the EFS CSI driver. Find instructions for getting started in the [EKS documentation](https://docs.aws.amazon.com/eks/latest/userguide/efs-csi.html) .

### Can I Access Amazon EFS from AWS Lambda Functions?

Yes. You can access EFS from functions running in [Lambda](https://aws.amazon.com/lambda/)  by referencing an EFS file system in your function settings. Find instructions for getting started in the [Lambda documentation](https://docs.aws.amazon.com/lambda/latest/dg/configuration-filesystem.html) .

### Can I Access Amazon EFS from Amazon SageMaker?

Yes. You can access training data in EFS from [Amazon SageMaker](https://aws.amazon.com/sagemaker/) training jobs by referencing an EFS file system in your [CreateTrainingJob request](https://docs.aws.amazon.com/sagemaker/latest/APIReference/API_CreateTrainingJob.html) . EFS is also automatically used for home directories created by [SageMaker Studio](https://docs.aws.amazon.com/sagemaker/latest/dg/studio-tasks.html) .