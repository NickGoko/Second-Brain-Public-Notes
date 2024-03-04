---
tags:
  - cloud/aws
---
**EBS is the Amazon Elastic Block Store.**

![[AWS Solutions Architect Skillbuilder#Block Storage Amazon EBS]]  
**EBS volumes** are <mark style="background: #CACFD9A6;">network attached storage that can be attached to</mark> [[Amazon EC2]] instances.
- <mark style="background: #ADCCFFA6;">EBS volume data persists independently of the life of the instance.</mark>
- EBS volumes do not need to be attached to an instance.
- You can attach multiple EBS volumes to an instance.
- <mark style="background: #ABF7F7A6;">You can attach an EBS volume to multiple instances with specific constraints</mark>.  
<mark style="background: #ADCCFFA6;">For most use cases where you need a shared volume across EC2 instances use Amazon EFS.</mark>
- <mark style="background: #ADCCFFA6;">EBS volume data is replicated across multiple servers in an AZ.  
EBS volumes must be in the same AZ as the instances they are attached to.</mark>
- <mark style="background: #ABF7F7A6;">EBS is designed for an annual failure rate of 0.1%-0.2% & an SLA of 99.95%.</mark>
- <mark style="background: #CACFD9A6;">Termination protection is turned off by default and must be manually enabled (keeps the volume/data when the instance is terminated).</mark>
- Root EBS volumes are deleted on termination by default.
- Extra non-boot volumes are not deleted on termination by default.
- The behavior can be changed by altering the “DeleteOnTermination” attribute.
- You can now create AMIs with encrypted root/boot volumes as well as data volumes (you can also use separate CMKs per volume).
- Volume sizes and types can be upgraded without downtime (except for magnetic standard).

**Elastic Volumes allow you to increase volume size, adjust performance, or change the volume type while the volume is in use.**

<mark style="background: #ABF7F7A6;">To migrate volumes between AZ’s create a snapshot then create a volume in another AZ from the snapshot (possible to change size and type).</mark>

- Auto-enable IO setting prevents the stopping of IO to a disk when AWS detects inconsistencies.
- The root device is created under /dev/sda1 or /dev/xvda.
- Magnetic EBS is for workloads that need throughput rather than IOPS.
- Throughput optimized EBS volumes cannot be a boot volume.
- Each instance that you launch has an associated root device volume, either an Amazon EBS volume or an instance store volume.

You can use block device mapping to specify additional EBS volumes or instance store volumes to attach to an instance when it’s launched.
- You can also attach additional EBS volumes to a running instance.
- You cannot decrease an EBS volume size.
- When changing volumes the new volume must be at least the size of the current volume’s snapshot.  
Images can be made public but not if they’re encrypted.  
AMIs can be shared with other accounts.  
You can have up to 5,000 EBS volumes by default.  
You can have up to 10,000 snapshots by default.

## Instance Store
An instance store provides _temporary_ (non-persistent) block-level storage for your instance.

This is different to EBS which provides persistent storage but is also a block storage service that can be a root or additional volume.

Instance store storage is located on disks that are physically attached to the host computer.

Instance store is ideal for temporary storage of information that changes frequently, such as buffers, caches, scratch data, and other temporary content, or for data that is replicated across a fleet of instances, such as a load-balanced pool of web servers.

You can specify instance store volumes for an instance only when you launch it.

You can’t detach an instance store volume from one instance and attach it to a different instance.

The instance type determines the size of the instance store available, and the type of hardware used for the instance store volumes.

Instance store volumes are included as part of the instance’s usage cost.

Some instance types use NVMe or SATA-based solid-state drives (SSD) to deliver high random I/O performance.

This is a good option when you need storage with very low latency, but you don’t need the data to persist when the instance terminates, or you can take advantage of fault-tolerant architectures.

**_EXAM TIP:_** _Instance stores offer very high performance and low latency. If you can afford to lose an instance, i.e. you are replicating your data, these can be a good solution for high performance/low latency requirements. Look out for questions that mention distributed or replicated databases that need high I/O. Also, remember that the cost of instance stores is included in the instance charges so it can also be more cost-effective than EBS Provisioned IOPS._  
![[AWS Solutions Architect Skillbuilder#Amazon Elastic Block Store(Amazon EBS) Primer]]
## EBS Vs Instance Store

- EBS-backed means the root volume is an EBS volume and storage is persistent.
- Instance store-backed means the root volume is an instance store volume and storage is not persistent.

On an EBS-backed instance, the default action is for the root EBS volume to be deleted upon termination.

Instance store volumes are sometimes called Ephemeral storage (non-persistent).

Instance store backed instances cannot be stopped. If the underlying host fails the data will be lost.

Instance store volume root devices are created from AMI templates stored on S3.

EBS backed instances can be stopped. You will not lose the data on this instance if it is stopped (persistent).

EBS volumes can be detached and reattached to other EC2 instances.

EBS volume root devices are launched from AMI’s that are backed by EBS snapshots.

Instance store volumes cannot be detached/reattached.

When rebooting the instances for both types data will not be lost.

By default, both root volumes will be deleted on termination unless you configured otherwise.

## EBS Volume Types

#### SSD, General Purpose – gp2/gp3:
- Volume size from 1 GiB to 16 TiB.
- Up to 16,000 IOPS per volume.
- Performance:
    - 3 IOPS/GiB for gp2.
    - Up to 500 IOPS/GiB for gp3.
- Can be a boot volume.
- EBS multi-attach not supported.
- Use cases:
    - Low-latency interactive apps.
    - Development and test environments.

#### SSD, Provisioned IOPS – io1/io2:
- More than 16,000 IOPS.
- Up to 64,000 IOPS per volume (Nitro instances).
- Up to 32,000 IOPS per volume for other instance types.
- Performance:
    - Up to 50 IOPS/GiB for io1.
    - Up to 500 IOPS/Gib for io2.
- Can be a boot volume.
- EBS multi-attach is supported.
- Use cases:
    - Workloads that require sustained IOPS performance or more than 16,000 IOPS.
    - I/O-intensive database workloads.

#### HDD, Throughput Optimized – (st1):
- Frequently accessed, throughput intensive workloads with large datasets and large I/O sizes, such as MapReduce, Kafka, log processing, data warehouse, and ETL workloads.
- Throughput measured in MiB/s and includes the ability to burst up to 250 MiB/s per TB, with a baseline throughput of 40 MB/s per TB and a maximum throughput of 500 MiB/s per volume.
- Cannot be a boot volume.
- EBS multi-attach not supported.

#### HDD, Cold – (sc1):
- Lowest cost storage – cannot be a boot volume.
- Less frequently accessed workloads with large, cold datasets.
- These volumes can burst up to 80 MiB/s per TiB, with a baseline throughput of 12 MiB/s.
- Cannot be a boot volume.
- EBS multi-attach not supported.

## EBS Optimized Instances:
- Dedicated capacity for Amazon EBS I/O.
- EBS-optimized instances are designed for use with all EBS volume types.
- Max bandwidth: 400 Mbps – 12000 Mbps.
- IOPS: 3000 – 65000.
- GP-SSD within 10% of baseline and burst performance 99.9% of the time.
- PIOPS within 10% of baseline and burst performance 99.9% of the time.
- Additional hourly fee.
- Available for select instance types.
- Some instance types have EBS-optimized enabled by default.

The following EBS volumes appear most often on the AWS exams:

|   |   |   |   |   |
|---|---|---|---|---|
|**Volume Type**|**EBS Provisioned IOPS SSD (io1/io2)**|**EBS General Purpose SSD (gp2/gp3)**|**Throughput Optimized HDD (st1)**|**Cold HDD (sc1)**|
|**Short Description**|Highest performance SSD volume designed for latency-sensitive transactional workloads|General Purpose SSD volume that balances price performance for a wide variety of transactional workloads|Low-cost HDD volume, designed for frequently accessed. Throughput intensive workloads|Lowest cost HDD volume designed for less frequently accessed workloads|
|**Use Cases**|I/O-intensive NoSQL and relational databases|Boot volumes, low-latency interactive apps, dev & test|Big-data, data warehouses, log processing|Colder data requiring fewer scans per day|
|**Volume Size**|4 GiB – 16 TiB|1 GiB – 16 TiB|125 GB – 16 TiB|125 GB – 16 TiB|
|**Max IOPS** / Volume**|64,000|16,000|500|250|
|**Max Throughput***Volume**|1,000 MiB/s|250 MiB/s (gp2)<br><br>1000 MiB/s (gp3)|500 MiB/s|250 MiB/s|
|**Can be boot volume?**|Yes|Yes|No|No|
|**EBS Multi-attach**|Supported|Not Supported|Not Supported|Not Supported|

![[Pasted image 20240206203259.png]]

![[Pasted image 20240206205055.png]]  
![[Pasted image 20240206205739.png]]


## Amazon EBS Snapshots

Snapshots capture a point-in-time state of an instance.  
Cost-effective and easy backup strategy.  
Share data sets with other users or accounts.
- <mark style="background: #BBFABBA6;">Can be used to migrate a system to a new AZ or region.</mark>
- <mark style="background: #ABF7F7A6;">Can be used to convert an unencrypted volume to an encrypted volume.</mark>
- **Snapshots are stored on Amazon S3.**  
Does not provide granular backup (not a replacement for backup software).
- If you make periodic snapshots of a volume, the snapshots are incremental, which means that only the blocks on the device that have changed after your last snapshot are saved in the new snapshot.
- Even though snapshots are saved incrementally, the snapshot deletion process is designed so that you need to retain only the most recent snapshot to restore the volume.
- Snapshots can only be accessed through the EC2 APIs.
- EBS volumes are AZ specific, but snapshots are region specific.
- <mark style="background: #ADCCFFA6;">Volumes can be created from EBS snapshots that are the same size or larger.</mark>
- Snapshots can be taken of non-root EBS volumes while running.  
To take a consistent snapshot, writes must be stopped (paused) until the snapshot is complete. if this is not possible the volume needs to be detached; or if it’s an EBS root volume the instance must be stopped.

- To lower storage costs on S3 a full snapshot and subsequent incremental updates can be created.
- You are charged for data traffic to S3 and storage costs on S3.
- You are billed only for the changed blocks.
- Deleting a snapshot removes only the data not needed by any other snapshot.

<mark style="background: #BBFABBA6;">You can resize volumes through restoring snapshots with different sizes (configured when taking the snapshot).</mark>

<mark style="background: #ABF7F7A6;">Snapshots can be copied between regions (and be encrypted). </mark>  
Images are then created from the snapshot in the other region which creates an AMI that can be used to boot an instance.

You can create volumes from snapshots and choose the availability zone within the region.

## Encryption
<mark style="background: #FFF3A3A6;">You can encrypt both the boot and data volumes of an EC2 instance. </mark>  
<mark style="background: #ADCCFFA6;">When you create an encrypted EBS volume and attach it to a supported instance type, the following types of data are encrypted</mark>:  
	- <mark style="background: #ABF7F7A6;">Data at rest inside the volume.</mark>  
	- <mark style="background: #ABF7F7A6;">All data moving between the volume and the instance.</mark>  
	- <mark style="background: #FFB86CA6;">All snapshots created from the volume.</mark>  
	- <mark style="background: #ABF7F7A6;">All volumes created from those snapshots.</mark>

Encryption is supported by all EBS volume types.  
- <mark style="background: #FFF3A3A6;">Expect the same IOPS performance on encrypted volumes as on unencrypted volumes.</mark>  
- All instance families support encryption.  
<mark style="background: #FFB86CA6;">Amazon EBS encryption is available on the instance types listed below:</mark>
- **General purpose**: A1, M3, M4, M5, M5a, M5ad, M5d, T2, T3, and T3a.
- **Compute optimized**: C3, C4, C5, C5d, and C5n.
- **Memory optimized**: cr1.8xlarge, R3, R4, R5, R5a, R5ad, R5d, u-6tb1.metal, u-9tb1.metal, u-12tb1.metal, X1, X1e, and z1d.
- **Storage optimized**: D2, h1.2xlarge, h1.4xlarge, I2, and I3.
- **Accelerated computing**: F1, G2, G3, G4, P2, and P3.

<mark style="background: #FF5582A6;">EBS encrypts your volume with a data key using the industry-standard AES-256 algorithm.</mark>

<mark style="background: #FFF3A3A6;">Your data key is stored on-disk with your encrypted data, but not before EBS encrypts it </mark>with your CMK. <mark style="background: #CACFD9A6;">Your data key never appears on disk in plaintext. .</mark>

The same data key is shared by snapshots of the volume and any subsequent volumes created from those snapshots.

Snapshots of encrypted volumes are encrypted automatically.

EBS volumes restored from encrypted snapshots are encrypted automatically.

EBS volumes created from encrypted snapshots are also encrypted.

You can share snapshots, but if they’re encrypted it must be with a custom CMK key.

You can check the encryption status of your EBS volumes with AWS Config.

<mark style="background: #FFB86CA6;">There is no direct way to change the encryption state of a volume.</mark>

Either create an encrypted volume and copy data to it or take a snapshot, encrypt it, and create a new encrypted volume from the snapshot.

To encrypt a volume or snapshot you need an encryption key, these are customer managed keys (CMK), and they are managed by the AWS Key Management Service (KMS).

A default CMK key is generated for the first encrypted volumes.

Subsequent encrypted volumes will use their own unique key (AES 256 bit).

The CMK used to encrypt a volume is used by any snapshots and volumes created from snapshots.

You cannot share encrypted volumes created using a default CMK key.

You cannot change the CMK key that is used to encrypt a volume.

You must create a copy of the snapshot and change encryption keys as part of the copy.

This is required to be able to share the encrypted volume.

<mark style="background: #CACFD9A6;">By default only the account owner can create volumes from snapshots.</mark>

You can share unencrypted snapshots with the AWS community by making them public.
- You can also share unencrypted snapshots with other AWS accounts by making them private and selecting the accounts to share them with.
- You cannot make encrypted snapshots public.
- You can share encrypted snapshots with other AWS accounts using a non-default CMK key and configuring cross-account permissions to give the account access to the key, mark as private and configure the account to share with.  
The receiving account must copy the snapshot before they can then create volumes from the snapshot.
- It is recommended that the receiving account re-encrypt the shared and encrypted snapshot using their own CMK key.

The following information applies to snapshots:
- Snapshots are created asynchronously and are incremental.
- You can copy unencrypted snapshots (optionally encrypt).
- You can copy an encrypted snapshot (optionally re-encrypt with a different key).
- Snapshot copies receive a new unique ID.
- You can copy within or between regions.
- You cannot move snapshots, only copy them.
- You cannot take a copy of a snapshot when it is in a “pending” state, it must be “complete”.
- S3 Server Side Encryption (SSE) protects data in transit while copying.
- User defined tags are not copied.
- You can have up to 5 snapshot copy requests running in a single destination per account.
- You can copy Import/Export service, AWS Marketplace, and AWS Storage Gateway snapshots.
- If you try to copy an encrypted snapshot without having access to the encryption keys it will fail silently (cross-account permissions are required).

Copying snapshots may be required for:
- Creating services in other regions.
- DR – the ability to restore from snapshot in another region.
- Migration to another region.
- Applying encryption.
- Data retention.

To take application-consistent snapshots of RAID arrays:
- Stop the application from writing to disk.
- Flush all caches to the disk.
- Freeze the filesystem.
- Unmount the RAID array.
- Shut down the associated EC2 instance.

## AMIs

An Amazon Machine Image (AMI) is a special type of virtual appliance that is used to create a virtual machine within the Amazon Elastic Compute Cloud (“EC2”).

An AMI includes the following:
- A template for the root volume for the instance (for example, an operating system, an application server, and applications).
- Launch permissions that control which AWS accounts can use the AMI to launch instances.
- A block device mapping that specifies the volumes to attach to the instance when it’s launched.

AMIs are either instance store-backed or EBS-backed.

Instance store-backed:
- Launch an EC2 instance from an AWS instance store-backed AMI.
- Update the root volume as required.
- Create the AMI which will upload to a user specified S3 bucket (user bucket).
- Register the AMI with EC2 (creates another EC2 controlled S3 image).
- To make changes update the source then deregister and reregister.
- Upon launch the image is copied to the EC2 host.
- Deregister an image when the AMI is not needed anymore (does not affect existing instances created from the AMI).
- Instance store-backed volumes can only be created at launch time.

EBS-backed:
- Must stop the instance to create a consistent image and then create the AMI.
- AWS registers the AMIs automatically.
- During creation AWS creates snapshots of all attached volumes – there is no need to specify a bucket, but you will be charged for storage on S3.
- You cannot delete the snapshot of the root volume if the AMI is registered (deregister and delete).
- You can now create AMIs with encrypted root/boot volumes as well as data volumes (can also use separate CMKs per volume).

Copying AMIs:
- You can copy an Amazon Machine Image (AMI) within or across an AWS region using the AWS Management Console, the AWS Command Line Interface or SDKs, or the Amazon EC2 API, all of which support the CopyImage action.
- You can copy both Amazon EBS-backed AMIs and instance store-backed AMIs.
- You can copy encrypted AMIs and AMIs with encrypted snapshots.

## Deployment and Provisioning
- Termination protection is turned off by default and must be manually enabled (keeps the volume/data when the instance is terminated).
- Root EBS volumes are deleted on termination by default.
- Extra non-boot volumes are not deleted on termination by default.

The behavior can be changed by altering the “DeleteOnTermination” attribute.

Volume sizes and types can be upgraded without downtime (except for magnetic standard).

Elastic Volumes allow you to increase volume size, adjust performance, or change the volume type while the volume is in use.

To migrate volumes between AZ’s create a snapshot then create a volume in another AZ from the snapshot (possible to change size and type).

## EBS Copying, Sharing and Encryption Methods

The following diagram aims to articulate the various possible options for copying EBS volumes, sharing AMIs and snapshots and applying encryption:

![EBS Copying Sharing and Encryption](https://digitalcloud.training/wp-content/uploads/2022/01/ebs-copying-sharing-and-encryption.jpeg)

## RAID

- RAID can be used to increase IOPS.
- RAID 0 = 0 striping – data is written across multiple disks and increases performance but no redundancy.
- RAID 1 = 1 mirroring – creates 2 copies of the data but does not increase performance, only redundancy.
- RAID 10 = 10 combination of RAID 1 and 2 resulting in increased performance and redundancy (at the cost of additional disks).
- You can configure multiple striped gp2 or standard volumes (typically RAID 0).
- You can configure multiple striped PIOPS volumes (typically RAID 0).
- RAID is configured through the guest OS.
- EBS optimized EC2 instances are another way of increasing performance.

Ensure the EC2 instance can handle the bandwidth required for the increased performance.

Use EBS optimized instances or instances with a 10 Gbps network interface.

Not recommended to use RAID for root/boot volumes.

## Monitoring and Reporting

Amazon Elastic Block Store (Amazon EBS) sends data points to CloudWatch for [several metrics](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using_cloudwatch_ebs.html).

A few specific metrics to understand for the exam:

- DiskReadBytes / DiskWriteBytes:
    - Relates to Instance Store volumes NOT to EBS.
    - Included in the AWS/EC2 namespace.
- VolumeReadBytes / VolumeWriteBytes:
    - Relates to the EBS volume.
    - Included in the AWS/EBS namespace.

There are two types of Amazon CloudWatch monitoring available for Amazon EBS volumes:

- Basic – Data is available automatically in 5-minute periods at no charge. This includes data for the root device volumes for EBS-backed instances.
- Detailed – Provisioned IOPS SSD (io1) volumes automatically send one-minute metrics to CloudWatch.

Amazon EBS General Purpose SSD (gp2), Throughput Optimized HDD (st1) , Cold HDD (sc1), and Magnetic (standard) volumes automatically send five-minute metrics to CloudWatch.

Provisioned IOPS SSD (io1) volumes automatically send one-minute metrics to CloudWatch. Data is only reported to CloudWatch when the volume is attached to an instance.

Volume [status checks](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/monitoring-volume-status.html) enable you to better understand, track, and manage potential inconsistencies in the data on an Amazon EBS volume.

|   |   |   |
|---|---|---|
|**Volume Status**|**I/O Enabled Status**|**I/O performance status (only available for Provisioned IOPS volumes)**|
|ok|Enabled (I/O Enabled or I/O Auto-Enabled)|Normal (Volume performance is expected)|
|warning|Enabled (I/O Enabled or I/O Auto-Enabled)<br><br>Disabled (Volume is offline and pending recovery or is waiting for the user to enable I/O).|Degraded (Volume performance is below expectations)<br><br>Severely Degraded (Volume performance is well below expectations)|
|impaired|Enabled (I/O Enabled or I/O Auto-Enabled)<br><br>Disabled (Volume is offline and pending recovery, or is waiting for the user to enable I/O)|Stalled (Volume performance is severely impacted)<br><br>Not Available (Unable to determine I/O performance because I/O is disabled)|
|insufficient-data|Enabled (I/O Enabled or I/O Auto-Enabled)<br><br>Insufficient Data|Insufficient Data|

## Logging and Auditing

Amazon EC2 and Amazon EBS are integrated with AWS CloudTrail, a service that provides a record of actions taken by a user, role, or an AWS service in Amazon EC2 and Amazon EBS.

CloudTrail captures all API calls for Amazon EC2 and Amazon EBS as events, including calls from the console and from code calls to the APIs.

## Amazon Data Lifecycle Manager (DLM)

Automates the creation, retention, and deletion of EBS snapshots and EBS-backed AMIs.

- Protect valuable data by enforcing a regular backup schedule.
- Create standardized AMIs that can be refreshed at regular intervals.
- Retain backups as required by auditors or internal compliance.
- Reduce storage costs by deleting outdated backups.
- Create disaster recovery backup policies that back up data to isolated accounts.

## EBS Limits (per region)

|   |   |
|---|---|
|**Name**|**Default Limit**|
|Provisioned IOPS|300,000|
|Provisioned IOPS (SSD) volume storage (TiB)|300|
|General Purpose (SSD) volume storage (TiB)|300|
|Magnetic volume storage (TiB)|300|
|Max Cold HDD (sc1) Storage in (TiB)|300|
|Max Throughput Optimized HDD (st1) Storage (TiB)|300|

# FAQ

## General

Close all

### Are Amazon EBS Volume and Snapshot ID Lengths Changing in 2018?

Yes, please visit the [EC2 FAQs](https://aws.amazon.com/ec2/faqs/#longer-ids) page for more details.

### What Happens to My Data when an Amazon EC2 Instance Terminates?

Unlike the data stored on a local instance store (which persists only as long as that instance is alive), data stored on an Amazon EBS volume can persist independently of the life of the instance. Therefore, we recommend that you use the local instance store only for temporary data. For data requiring a higher level of durability, we recommend using Amazon EBS volumes or backing up the data to Amazon S3. If you are using an Amazon EBS volume as a root partition, set the Delete on termination flag to "No" if you want your Amazon EBS volume to persist outside the life of the instance.

### What Kind of Performance Can I Expect from Amazon EBS Volumes?

Amazon EBS provides six volume types: Provisioned IOPS SSD (io2 Block Express and io1), General Purpose SSD (gp3 and gp2), Throughput Optimized HDD (st1) and Cold HDD (sc1). These volume types differ in performance characteristics and price, allowing you to tailor your storage performance and cost to the needs of your applications. The average latency between EC2 instances and EBS is single-digit milliseconds, while the average latency of io2 Block Express volumes is sub-millisecond. For more performance information, see the [EBS product details page](https://aws.amazon.com/ebs/). For more information about Amazon EBS performance guidelines, see [Increasing EBS Performance](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/EBSPerformance.html).

### Which Volume Should I Choose?

Amazon EBS includes two major categories of storage: SSD-backed storage for transactional workloads (performance depends primarily on IOPS, latency, and durability) and HDD-backed storage for throughput workloads (performance depends primarily on throughput, measured in MB/s). SSD-backed volumes are designed for transactional, IOPS-intensive database workloads, boot volumes, and workloads that require high IOPS. SSD-backed volumes include Provisioned IOPS SSD (io2 Block Express and io1) and General Purpose SSD (gp3 and gp2). Io2 Block Express of the Provisioned IOPS SSD volumes is designed to provide 100X durability of 99.999%, making it ideal for business-critical applications that need higher uptime. Gp3 is the latest generation of General Purpose SSD volumes that provides the right balance of price and performance for most applications that don’t require the highest IOPS performance or 99.999% durability. HDD-backed volumes are designed for throughput-intensive and big-data workloads, large I/O sizes, and sequential I/O patterns. HDD-backed volumes include Throughput Optimized HDD (st1) and Cold HDD (sc1).

### Since Io2 Block Express Provides Higher Volume Durability, Should I Still Take Snapshots and Plan to Replicate Io2 Block Express Volumes across Availability Zones (AZs) for High Durability?

High volume durability, snapshots, and replicating volumes across AZs protect against different types of failures, and customers can choose to use one, two, or all of these approaches based on their data durability requirements. Higher volume durability reduces the probability of losing the primary copy of your data. Snapshots protect against the unlikely event of a volume failure. Replicating volumes across AZs protects against an AZ level failure and also provides faster recovery in case of failure.

### What Are Best Practices for High Availability on Amazon EBS?

Amazon EBS volumes are designed to be highly available, reliable, and durable. At no additional charge to you, <mark style="background: #BBFABBA6;">Amazon EBS volume data is replicated across multiple servers in an Availability Zone to prevent the loss of data from the failure of any single component.</mark> Depending on the degree of high availability (HA) that your application requires, we recommend these guidelines to achieve a robust degree of high availability:  
1. Design the system to have no single point of failure. For more details, see [High Availability and Scaling on AWS](https://docs.aws.amazon.com/whitepapers/latest/real-time-communication-on-aws/high-availability-and-scalability-on-aws.html).  
2. Use automated monitoring, failure detection, and failover mechanisms. See [Monitoring the Status of your EBS volumes](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/monitoring-volume-status.html) and [Monitoring EBS Volumes using CloudWatch](https://aws.amazon.com/blogs/storage/valuable-tips-for-monitoring-and-understanding-amazon-ebs-performance-using-amazon-cloudwatch/) for more details on monitoring your EBS Volume’s performance.  
3. Prepare operating procedures for manual mechanisms to respond to, mitigate, and recover from any failures. This includes detaching unavailable volumes and attaching a backup recovery volume in cases of failure. For more details, see the documentation on [Replacing an EBS volume](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ebs-restoring-volume.html).

### How Do I Modify the Capacity, Performance, or Type of an Existing EBS Volume?

Changing a volume configuration is easy. The [Elastic Volumes](https://aws.amazon.com/ebs/features/#Amazon_EBS_Elastic_Volumes) feature allows you to increase capacity, tune performance, or change your volume type with a single CLI call, API call or a few console clicks. For more information about Elastic Volumes, see the Elastic Volumes documentation.

### Are EBS Standard Volumes Still Available?

EBS Standard Volumes have been renamed to EBS Magnetic volumes. Any existing volumes will not have been changed as a result of this and there are no functional differences in the EBS Magnetic offering compared to EBS Standard. The name of this offering was changed to avoid confusion with our General Purpose SSD (gp2) volume type which is our recommended default volume type.

### Are Provisioned IOPS SSD (io2 Block Express and io1) Volumes Available for All Amazon EC2 Instance Types?

Provisioned IOPS SSD io2 Block Express and io1 volumes are available on all EC2 instance types. Use EBS-optimized EC2 instances to deliver consistent and predictable IOPS on io2 Block Express and io1 volumes. [EBS-optimized instances](https://aws.amazon.com/ebs/features/#Amazon_EBS-Optimized_instances) provide dedicated throughput between Amazon EC2 and Amazon EBS, with options ranging from 62.5 MB/s to 12,500 MB/s based on the instance type used. To achieve the limit of 256,000 IOPS and 4,000 MB/s throughput, you must use io2 Block Express volumes attached to [Nitro System-based instances](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/instance-types.html#ec2-nitro-instances).

## Performance

Close all

### What Level of Performance Consistency Can I Expect to See from My Provisioned IOPS SSD (io2 Block Express and io1) Volumes?

When attached to EBS-optimized instances, Provisioned IOPS SSD (io2 Block Express and io1) volumes are designed to deliver within 10% of the provisioned IOPS performance 99.9% of the time in a given year. Your exact performance depends on your application’s I/O requirements.

### What Level of Performance Latency Can I Expect to See from My Provisioned IOPS SSD (io2 Block Express and io1) Volumes?

When attached to EBS-optimized instances, Provisioned IOPS io2 Block Express volumes can achieve sub-millisecond latency, and io1 volumes can achieve single-digit millisecond latencies. Your exact performance depends on your application’s I/O requirements.

### Does the I/O Size of My Application Reads and Writes Affect the Rate of IOPS I Get from My Provisioned IOPS SSD (io2 Block Express) Volumes?

Yes, it does. When you provision IOPS for io2 Block Express volumes, the IOPS rate you get depends on the I/O size of your application reads and writes. Provisioned IOPS volumes have a base I/O size of 16KB. So, if you have provisioned a volume with 40,000 IOPS for an I/O size of 16KB, it will achieve up to 40,000 IOPS at that size. If the I/O size is increased to 256 KB, then you will achieve up to 16,000 IOPS, since the maximum throughput of 4000 MiB/s is achieved at 16,000 IOPS. For more details, please visit the technical documentation on [Provisioned IOPS volumes](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/provisioned-iops.html). You can use [Amazon CloudWatch](https://aws.amazon.com/cloudwatch/) to monitor your throughput and I/O sizes.

### What Factors Can Affect the Performance Consistency I See with Provisioned IOPS SSD (io2 Block Express and io1) Volumes?

Provisioned IOPS SSD (io2 Block Express and io1) volumes attached to EBS-optimized instances are designed to offer consistent performance, delivering within 10% of the provisioned IOPS performance 99.9% of the time over a given year. <mark style="background: #D2B3FFA6;">For maximum performance consistency with new volumes created from a snapshot, we recommend enabling Fast Snapshot Restore (FSR) on your snapshots. EBS volumes restored from FSR-enabled snapshots instantly receive their full performance.</mark>

Another factor that can impact your performance is if your application isn’t sending enough I/O requests. This can be monitored by looking at your <mark style="background: #FFB8EBA6;">volume’s queue depth</mark>.  
The <mark style="background: #CACFD9A6;">queue depth is the number of pending I/O requests from your application to your volume</mark>.  
 For maximum consistency, a Provisioned IOPS volume must maintain an average queue depth (rounded to the nearest whole number) of one for every 1000 provisioned IOPS in a minute. For example, for a volume provisioned with 3000 IOPS, the queue depth average must be 3. For more information about ensuring consistent performance of your volumes, see [Increasing EBS Performance](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/EBSPerformance.html).

### What Level of Performance Consistency Can I Expect to See from My HDD-backed Volumes?

When attached to EBS-optimized instances, Throughput Optimized HDD (st1) and Cold HDD (sc1) volumes are designed to deliver within 10% of the expected throughput performance 99% of the time in a given year. Your exact performance depends on your application’s I/O requirements and the performance of your EC2 instance.

### Does the I/O Size of My Application Reads and Writes Affect the Rate of Throughput I Get from My HDD-backed Volumes?

Yes. The throughput rate you get depends on the I/O size of your application reads and writes. HDD-backed volumes process reads and writes in I/O sizes of 1MB. Sequential I/Os are merged and processed as 1 MB units while each non-sequential I/O is processed as 1MB even if the actual I/O size is smaller. Thus, while a transactional workload with small, random IOs, such as a database, won't perform well on HDD-backed volumes, sequential I/Os and large I/O sizes will achieve the advertised performance of st1 and sc1 for a longer period of time.

### What Factors Can Affect the Performance Consistency of My HDD-backed Volumes?

Throughput Optimized HDD (st1) and Cold HDD (sc1) volumes attached to EBS-optimized instances are designed to offer consistent performance, delivering within 10% of the expected throughput performance 99% of the time in a given year. There are several factors that could affect the level of consistency you see. For example, the relative balance between random and sequential I/O operations on the volume can impact your performance. Too many random small I/O operations will quickly deplete your I/O credits and lower your performance down to the baseline rate. Your throughput rate may also be lower depending on the instance selected. Although st1 can drive throughput up to 500 MB/s, performance will be limited by the separate instance-level limit for EBS traffic. Another factor is taking a snapshot which will decrease expected write performance down to the baseline rate, until the snapshot completes. This is specific to st1 and sc1.

Your performance can also be impacted if your application isn’t sending enough I/O requests. This can be monitored by looking at your volume’s queue depth and I/O size. The queue depth is the number of pending I/O requests from your application to your volume. For maximum consistency, HDD-backed volumes must maintain an average queue depth (rounded to the nearest whole number) of four or more for every 1 MB sequential I/O. For more information about ensuring consistent performance of your volumes, see [Increasing EBS Performance](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/EBSPerformance.html).

### Can I Stripe Multiple Volumes together to Get Better Performance?

Yes. You can stripe multiple volumes together to achieve up to 400,000 IOPS or 12,500 Mbps when attached to larger EC2 instances. We recommend using io2 Block Express volumes for higher performance requirements without needing the operational management of striping multiple volumes. Performance for st1 and sc1 scales linearly with volume size so there may not be as much of a benefit to stripe these volumes together.

### How Does Amazon EBS Handle Issues like Storage Contention?

EBS is a multi-tenant block storage service. We employ rate limiting as a mechanism to avoid resource contention. This starts with having defined performance criteria for the volumes – our volume types (gp2, PIOPS, st1, and sc1) all have defined performance characteristics in terms of IOPS and throughput. The next step is defining performance at the instance level. Each EBS Optimized instance has defined performance (both throughput and IOPS) for the set of EBS volumes attached to the instance. A customer can, therefore, size instances and volumes to get the desired level of performance. In addition, customers can use our reported metrics to observe instance level and volume level performance. They can set alarms to determine if what they are seeing does not match the expected performance – the metrics can also help determine if customers are configured at the right type of instance with the right amount of performance at the volume level or not. On the EBS end, we use the configured performance to inform how we allocate the appropriate instance and EBS infrastructure to support the volumes. By appropriately allocating infrastructure, we avoid resource contention. Additionally, we constantly monitor our infrastructure. This monitoring allows us to detect infrastructure failure (or imminent infrastructure failure) and therefore, move the volumes pro-actively to functioning hardware while the underlying infrastructure is either repaired or replaced (as appropriate).

### What Level of Performance Consistency Can I Expect to See from My General Purpose SSD (gp3 and gp2) Volumes?

When attached to EBS-optimized instances, General Purpose SSD (gp3 and gp2) volumes are designed to deliver within 10% of the provisioned IOPS performance 99% of the time in a given year. Your exact performance depends on your application’s I/O requirements.

### What Level of Performance Latency Can I Expect to See from My General Purpose SSD (gp3 and gp2) Volumes?

When attached to EBS-optimized instances, General Purpose SSD (gp3 and gp2) volumes can achieve single digit millisecond latencies. Your exact performance depends on your application’s I/O requirements.

### Do General Purpose SSD (gp3) Volumes Have Burst?

No. All General Purpose SSD (gp3) volumes include 3,000 IOPS and 125 MB/s of consistent performance at no additional cost. Volumes can sustain the full 3,000 IOPS and 125 MB/s indefinitely.

### How Does Burst Work on General Purpose SSD (gp2) Volumes?

General Purpose SSD (gp2) volumes that are under 1,000 GB receive burst IOPS performance up to 3,000 IOPS for at least 30 min of sustained performance. Additionally, gp2 volumes deliver consistent performance of 3 IOPS per provisioned GB. For example, a 500 GB volume is capable of driving 1,500 IOPS consistently, and bursting to 3,000 IOPS for 60 minutes (3,000 IOPS \* 60 seconds \* 30 minutes / 1,500 IOPS / 60 seconds).

### What is EBS Block Express?

EBS Block Express is the next generation of Amazon EBS storage server architecture purpose-built to deliver the highest levels of performance with sub-millisecond latency for block storage at cloud scale. Block Express does this by using Scalable Reliable Datagrams (SRD), a high-performance lower-latency network protocol, to communicate with Nitro System-based EC2 instances. This is the same high performance and low latency network interface that is used for inter-instance communication in Elastic Fabric Adapter (EFA) for High Performance Computing (HPC) and Machine Learning (ML) workloads. Additionally, Block Express offers modular software and hardware building blocks that can be assembled in many different ways, giving us the flexibility to design and deliver improved performance and new features at a faster rate.

### What Workloads Are Suited for Io2 Block Express?

io2 Block Express is suited for performance and capacity intensive workloads that benefit from lower latency, higher IOPS, higher throughput, or larger capacity in a single volume. These workloads include relational and NoSQL databases such as SAP HANA, Oracle, MS SQL, PostgreSQL, MySQL, MongoDB, Cassandra, and critical business operation workloads such as SAP Business Suite, NetWeaver, Oracle eBusiness, PeopleSoft, Siebel, and ERP workloads such as Info LN and Info M3.

## Snapshots

Close all

### How Can I Use EBS Direct APIs for Snapshots?

This feature can be used via the following APIs that can be called using AWS CLI or via AWS SDK.

- List Snapshot Blocks: The ListSnapshotBlocks API operation returns the block indexes and block tokens for blocks in the specified snapshot.
- List Changed Blocks: The ListChangedBlocks API operation returns the block indexes and block tokens for blocks that are different between two specified snapshots of the same volume/snapshot lineage.
- Get Snapshot Blocks: The GetSnapshotBlock API operation returns the data in a block for the specified snapshot ID, block index, and block token.
- Start Snapshot: The StartSnapshot operation starts a snapshot, either as an incremental snapshot of an existing one or as a new snapshot. The started snapshot remains in a pending state until it is completed using the CompleteSnapshot action.
- Put Snapshot Block: The PutSnapshot operation adds data in the form of individual blocks to a started snapshot that is in a pending state. You must specify a Base64-encoded SHA256 checksum for the block of data transmitted. The service validates the checksum after the transmission is completed. The request fails if the checksum computed by service doesn’t match what you speciﬁed.
- Complete Snapshot: The CompleteSnapshot operation completes a started snapshot that is in a pending state. The snapshot is then changed to a completed state.

For more information, please refer to [technical documentation](https://docs.aws.amazon.com/ebs/latest/APIReference/Welcome.html).

### What Block Sizes Are Supported by GetSnapshotBlock and PutSnapshotBlock APIs?

GetSnapshotBlock and PutSnapshotBlock APIs support 512KiB block size.

### Will I Be Able to Access My Snapshots Using the Regular Amazon S3 API?

No, snapshots are only available through the Amazon EC2 API.

### Do Volumes Need to Be Un-mounted to Take a Snapshot?

No, snapshots can be done in real time while the volume is attached and in use. However, snapshots only capture data that has been written to your Amazon EBS volume, which might exclude any data that has been locally cached by your application or OS. To ensure consistent snapshots on volumes attached to an instance, we recommend detaching the volume cleanly, issuing the snapshot command, and then reattaching the volume. For Amazon EBS volumes that serve as root devices, we recommend shutting down the machine to take a clean snapshot.

### Does it Take Longer to Snapshot an Entire 16 TB Volume as Compared to an Entire 1 TB Volume?

By design, an EBS Snapshot of an entire 16 TB volume should take no longer than the time it takes to snapshot an entire 1 TB volume. However, the actual time taken to create a snapshot depends on several factors including the amount of data that has changed since the last snapshot of the EBS volume.

### Are Snapshots Versioned? Can I Read an Older Snapshot to Do a Point-in-time Recovery?

Each snapshot is given a unique identifier, and customers can create volumes based on any of their existing snapshots.

### How Can I Discover Amazon EBS Snapshots that Are Shared with Me?

You can find snapshots that are shared with you by selecting Private Snapshots from the list in the Snapshots section of the AWS Management Console. This section lists both snapshots that you own and snapshots that are shared with you.

### How Can I Find Which Amazon EBS Snapshots Are Shared Globally?

You can find snapshots that are shared globally by selecting Public Snapshots from the list in the Snapshots section of the AWS Management Console. You can also restrict public access to snapshots in an account by enabling [Block Public Access for EBS Snapshots](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/block-public-access-snapshots.html).

### How Can I Find a List of Amazon Public Datasets Stored in Amazon EBS Snapshots?

You can use the AWS Management Console to find public datasets stored as Amazon Snapshots. Log into the console, select the Amazon EC2 Service, select Snapshots and then filter on [Public Snapshots](https://console.aws.amazon.com/ec2/v2/home#Snapshots:visibility=public;sort=startTime). All information on public datasets is available in our [AWS Public Datasets](https://aws.amazon.com/public-datasets/) resource center.

### When Would I Use Fast Snapshot Restore (FSR)?

You should enable FSR on snapshots if you are concerned about latency of data access when you restore data from a snapshot to a volume and want to avoid the initial performance hit during initialization. FSR is intended to help with use cases such as virtual desktop infrastructure (VDI), backup & restore, test/dev volume copies, and booting from custom AMIs. By enabling FSR on your snapshot, you will see improved and predictable performance whenever you need to restore data from that snapshot.

### Does Enabling FSR for My Snapshot Speed up Snapshot Creation?

No. FSR-enabled snapshots improve restoring backup data from your snapshot to your volumes. FSR-enabled snapshots do not speed up snapshot creation time.

### How Do I Enable Fast Snapshot Restore (FSR)?

To use the feature, invoke the new enable-fast-snapshot-restores API on a snapshot within the availability zone (AZ) where initialized volumes are to be restored.

The FSR-enabled snapshot may be in any one of the following states: enabling, optimizing, enabled, disabling, disabled. State transitions are published as CloudWatch events and the FSR state can be checked via the describe-fast-snapshot-restores API.

Enabling FSR on a snapshot does not change any existing snapshot API interactions, and existing workflows will not need to change. FSR can be enabled or disabled on account-owned snapshots only. FSR cannot be applied to shared snapshots. You can view the list of your FSR-enabled snapshots via API or the console.

### How Do I Use Fast Snapshot Restore (FSR)?

Volumes created from an FSR-enabled snapshot are fully initialized. However, there are limits on the number of volumes that can be created with immediate full performance. These limits are expressed in the form of a credit bucket that is associated with an FSR-enabled snapshot in a given AZ. The important things to know regarding credits:

1\. A single volume create operation consumes a single credit  
2\. The number of credits is a function of the FSR-enabled snapshot size  
3\. Credits refill over time  
4\. Maximum credit bucket size is 10

To estimate your credit bucket size and fill rate, divide 1,024 by your snapshot size. For example, a 100 GiB FSR-enabled snapshot will have the maximum balance of 10 credits with a fill rate of 10 credits every hour. A 4 TiB snapshot will have a maximum balance of 1 with a fill rate of 1 credit every 4 hours.

It's important to note that the credit bucket size is a function of the FSR-enabled snapshot size, not the size of the volumes that are created. For example, it is possible to create up to ten 1TiB volumes from a 100GiB snapshot at once.

Lastly, each AZ in which the snapshot is FSR-enabled gets its own credit bucket independent of other AZs.

### How Many Concurrent Volumes Can I Create and what Happens when I Surpass This Limit?

The size of the create credit bucket represents the maximum number and the balance of the credit bucket represents the number of creates available. When filled, up to 10 initialized volumes can be created from an FSR-enabled snapshot at once. Both the maximum size of the credit bucket and the credit bucket balance are published as CloudWatch metrics. Volume creations beyond the limit will proceed as if FSR is not enabled on the snapshot.

### How Do I Know when a Volume Was Created from an FSR-enabled Snapshot?

When using FSR, a new EBS-specific attribute (fastRestored) is added in the DescribeVolumes API to denote the status at create time. When a volume is created from an FSR-enabled snapshot without sufficient volume-create credits, the create will succeed but the volume will not be initialized.

### What Happens to FSR when I Delete a Snapshot?

When you delete a snapshot, the FSR for your snapshot is automatically disabled and FSR billing for the snapshot will be terminated.

### Can I Enable FSR for Public and Private Snapshots Shared with Me?

Yes, you can enable FSR for public snapshots as well as all private snapshots shared with your account. To enable FSR for shared snapshots, you can use the same set of API calls that you use for enabling FSR on snapshots you own.

### How Am I Billed for Enabling FSR on a Snapshot Shared with Me?

When you enable FSR on your shared snapshot, you will be billed at standard FSR rates (see [pricing pages](https://aws.amazon.com/ebs/pricing/)). Note that only your account will be billed for the FSR of the shared snapshot. The owner of the snapshot will not get billed when you enable FSR on the shared snapshot.

### What Happens to the FSR for a Shared Snapshot when the Owner of the Snapshot Stops Sharing the Snapshot or Deletes It?

When the owner of your shared snapshot deletes the snapshot, or stops sharing the snapshot with you by revoking your permissions to create volumes from this snapshot, the FSR for your shared snapshot is automatically disabled and FSR billing for the snapshot will be terminated.

### How Do I Automate Application-consistent EBS Snapshots?

You can use Amazon Data Lifecycle Manager and AWS Systems Manager (SSM) to coordinate freeze, flush I/O, and unfreeze of your application or database as well as the initialization of EBS Snapshots. You will need to provide commands to perform the actions that are specific to your application or database. You can also refer to our [documentation](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/automate-app-consistent-backups.html) for AWS-provided code and SSM documents for MySQL, PostgreSQL, and Windows applications.

## Encryption

Close all

### What is Amazon EBS Encryption?

Amazon EBS encryption offers seamless encryption of EBS data volumes, boot volumes and snapshots, eliminating the need to build and maintain a secure key management infrastructure. <mark style="background: #BBFABBA6;">EBS encryption enables data at rest security by encrypting your data using Amazon-managed keys, or keys you create and manage using </mark>the [AWS Key Management Service (KMS)](https://docs.aws.amazon.com/kms/latest/developerguide/concepts.html#master_keys). The encryption occurs on the servers that host EC2 instances, providing encryption of data as it moves between EC2 instances and EBS storage. For more details, see Amazon EBS encryption in the [Amazon EC2 User Guide](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/EBSEncryption.html).

### What is the AWS Key Management Service (KMS)?

[AWS KMS](https://aws.amazon.com/kms/) is a managed service that makes it easy for you to create and control the encryption keys used to encrypt your data. AWS Key Management Service is integrated with other AWS services including Amazon EBS, Amazon S3, and Amazon Redshift, to make it simple to encrypt your data with encryption keys that you manage. AWS Key Management Service is also integrated with AWS CloudTrail to provide you with logs of all key usage to help meet your regulatory and compliance needs. To learn more about KMS, visit the AWS Key Management Service product page.

### Why Should I Use EBS Encryption?

You can use Amazon EBS encryption to meet security and encryption compliance requirements for data at rest encryption in the cloud. Pairing encryption with existing IAM access control policies improves your company’s defense-in-depth strategy.

### How Are My Amazon EBS Encryption Keys Managed?

Amazon EBS encryption handles key management for you. Each newly created volume gets a unique 256-bit AES key; Volumes created from the encrypted snapshots share the key. These keys are protected by our own key management infrastructure, which implements strong logical and physical security controls to prevent unauthorized access. Your data and associated keys are encrypted using the industry-standard AES-256 algorithm.

### Does EBS Encryption Support Boot Volumes?

Yes.

### Can I Create an Encrypted Data Volume at the time of Instance Launch?

Yes, using [customer master keys (CMKs)](https://docs.aws.amazon.com/kms/latest/developerguide/concepts.html#master_keys) that are either AWS-managed or customer-managed. You can specify the volume details and encryption through a [RunInstances API](https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_RunInstances.html) call with the [BlockDeviceMapping](https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_BlockDeviceMapping.html) parameter or through the Launch Wizard in the EC2 Console.

### Can I Create Additional Encrypted Data Volumes at the time of Instance Launch that Are not part of the AMI?

Yes, you can create encrypted data volume with either default or custom CMK encryption at the time of instances launch. You can specify the volume details and encryption through [BlockDeviceMapping](https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_BlockDeviceMapping.html) object in [RunInstances API](https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_RunInstances.html) call or through Launch Wizard in EC2 Console.

### Can I Launch an Encrypted EBS Instance from an Unencrypted AMI?

Yes. See [technical documentation](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/AMIEncryption.html) for details.

### Can I Share Encrypted Snapshots and AMIs with other Accounts?

Yes. You can share encrypted snapshots and AMIs using a [customer-managed customer master key (CMK)](https://docs.aws.amazon.com/kms/latest/developerguide/concepts.html) with other AWS accounts. See [technical documentation](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/sharingamis-explicit.html) for details.

### Can I Ensure that All New Volumes Created Are Always Encrypted?

Yes, you can enable EBS encryption by default with a single setting per region. This ensures that all new volumes are always encrypted. Refer to [technical documentation](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/EBSEncryption.html) for more details. 

## Billing and Metering

Close all

### Will I Be Billed for the IOPS Provisioned on a Provisioned IOPS Volume when it is Disconnected from an Instance?

Yes, you will be billed for the IOPS provisioned when it is disconnected from an instance. When a volume is detached, we recommend you consider creating a snapshot and deleting the volume to reduce costs. For more information, see the "Underutilized Amazon EBS Volumes" cost optimization check in [Trusted Advisor](https://aws.amazon.com/support/trustedadvisor/). This item checks your Amazon Elastic Block Store (Amazon EBS) volume configurations and warns when volumes appear to be underused.

### Do Your Prices Include Taxes?

Except as otherwise noted, our prices are exclusive of applicable taxes and duties, including VAT and applicable sales tax. For customers with a Japanese billing address, use of AWS services is subject to Japanese Consumption Tax. [Learn more](https://aws.amazon.com/c-tax-faqs/).

## Multi-Attach

Close all

### Is there an Additional Fee to Enable Multi-Attach?

No. Multi-Attach can be enabled on an EBS Provisioned IOPS volume and there will be charges for the storage (GB-Mo) and IOPS (IOPS-Mo) provisioned.

### Can I Boot an EC2 Instance Using a Multi-Attach Enabled Volume?

No.

### What Happens if All of My Attached Instances Do not Have the ‘deleteOnTermination’ Flag Set?

The volume's deleteOnTermination behavior is determined by the configuration of the last attached instance that is terminated. To ensure predictable delete on termination behavior, enable or disable 'deleteOnTermination' for all of the instances to which the volume is attached.

If you want the volume to be deleted when the attached instances are terminated, enable ‘deleteOnTermination’ for all of instances to which the volume is attached. If you want to retain the volume after the attached instances have been terminated, disable ‘deleteOnTermination’ for all attached instances. For more information, see [Multi-Attach](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ebs-volumes-multi.html) technical documentation.

### Can My Application Use Multi-Attach?

Your application can use Multi-Attach if the application is built on Windows Server Failover Cluster, coordinates safe access to shared storage using NVMe reservations, or coordinates safe access at the application-level.