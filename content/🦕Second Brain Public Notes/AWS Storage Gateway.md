---
tags:
  - cloud/aws
---
<mark style="background: #D2B3FFA6;">The AWS Storage Gateway service enables hybrid storage between on-premises environments and the AWS Cloud.</mark>

<mark style="background: #BBFABBA6;">It provides low-latency performance by caching frequently accessed data on premises, while storing data securely and durably in Amazon cloud storage services.</mark>

- <mark style="background: #ADCCFFA6;">Implemented using a virtual machine that you run on-premises (VMware or Hyper-V virtual appliance).</mark>

- <mark style="background: #CACFD9A6;">Provides local storage resources backed by</mark> [**Amazon S3**](https://digitalcloud.training/amazon-s3-and-glacier/) and [**Glacier**](https://digitalcloud.training/amazon-s3-and-glacier/).
- Often used in disaster recovery preparedness to sync data to AWS.

AWS Storage Gateway supports three storage interfaces: **file**, **volume**, and **tape**.

The table below shows the different gateways available and the interfaces and use cases:  
![[Pasted image 20240213111231.png]]

|   |   |   |   |
|---|---|---|---|
|**New Name**|**Old Name**|**Interface**|**Use Case**|
|**File Gateway**|None|NFS, SMB|Allow on-prem or EC2 instances to store objects in S3 via NFS or SMB mount points|
|**Volume Gateway Stored Mode**|Gateway-Stored Volumes|iSCSI|Asynchronous replication of on-prem data to S3|
|**Volume Gateway Cached Mode**|Gateway-Cached Volumes|iSCSI|Primary data stored in S3 with frequently accessed data cached locally on-prem|
|**Tape Gateway**|Gateway-Virtual Tape Library|ISCSI|Virtual media changer and tape library for use with existing backup software|

Each gateway you have can provide one type of interface.

All data transferred between any type of gateway appliance and AWS storage is encrypted using SSL.

By default, all data stored by AWS Storage Gateway in S3 is encrypted server-side with Amazon S3-Managed Encryption Keys (SSE-S3).

When using the file gateway, you can optionally configure each file share to have your objects encrypted with AWS KMS-Managed Keys using SSE-KMS.

## File Gateway

- File gateway provides a virtual on-premises file server, which enables you to store and retrieve files as objects in Amazon S3.
- Can be used for on-premises applications, and for Amazon EC2-resident applications that need file storage in S3 for object-based workloads.
- Used for flat files only, stored directly on S3.

- <mark style="background: #FFB86CA6;">File gateway offers SMB or NFS-based access to data in Amazon S3 with local caching.</mark>
- <mark style="background: #FFF3A3A6;">File gateway supports Amazon S3 Standard, S3 Standard – Infrequent Access (S3 Standard – IA) and S3 One Zone – IA.</mark>
- File gateway supports clients connecting to the gateway using NFS v3 and v4.1.
- Microsoft Windows clients that support SMB can connect to file gateway.
- The maximum size of an individual file is 5 TB.

![[Pasted image 20240213111400.png]]  
![[Pasted image 20240213111545.png]]


## Volume Gateway
The volume gateway represents the family of gateways that support _block-based volumes_, previously referred to as **gateway-cached** and **gateway-stored modes.**
 
<mark style="background: #FF5582A6;">Block storage – iSCSI based</mark>.  
![[Pasted image 20240213111629.png]]  
**Cached Volume mode** – <mark style="background: #ADCCFFA6;">the entire dataset is stored on S3, and a cache of the most frequently accessed data is cached on-site.</mark>

**Stored Volume mode** – <mark style="background: #FFF3A3A6;">the entire dataset is stored on-site and is asynchronously backed up to S3</mark> (EBS point-in-time snapshots). Snapshots are incremental and compressed.

- <mark style="background: #FFB8EBA6;">Each volume gateway can support up to 32 volumes.</mark>

- In cached mode, each volume can be up to 32 TB for a maximum of 1 PB of data per gateway (32 volumes, each 32 TB in size).
- In stored mode, each volume can be up to 16 TB for a maximum of 512 TB of data per gateway (32 volumes, each 16 TB in size).

## Gateway Virtual Tape Library
![[Pasted image 20240213111833.png]]
- Used for backup with popular backup software.
- Each gateway is preconfigured with a media changer and tape drives. Supported by NetBackup, Backup Exec, Veeam etc.
- When creating virtual tapes, you select one of the following sizes: 100 GB, 200 GB, 400 GB, 800 GB, 1.5 TB, and 2.5 TB.
- A tape gateway can have up to 1,500 virtual tapes with a maximum aggregate capacity of 1 PB.

Managing AWS Storage Gateway

You might need to shut down or reboot your VM for maintenance, such as when applying a patch to your hypervisor. Before you shut down the VM, you must first stop the gateway.

- For file gateway, you just shut down your VM.
- For volume and tape gateways, stop the gateway, reboot the VM, then start the gateway.

![[Pasted image 20240213112231.png]]

## Monitoring AWS Storage Gateway

The following metrics are useful when [**monitoring**](https://docs.aws.amazon.com/storagegateway/latest/userguide/Main_monitoring-gateways-common.html) cache usage for file, cached-volume, and tape gateways.

|   |   |   |
|---|---|---|
|**Metric**|**Description**|**Applies to**|
|CacheHitPercent|Percent of application reads served from the cache. The sample is taken at the end of the reporting period.  <br>Unit: Percent|File, cached-volume, and tape gateways.|
|CacheUsed|The total number of bytes being used in the gateway’s cache storage. The sample is taken at the end of the reporting period.  <br>Unit: Bytes|File, cached-volume, and tape gateways.|
# FAQ
**Q: What is Amazon S3 File Gateway?**

[Amazon S3 File Gateway](https://aws.amazon.com/storagegateway/file/s3/) is a configuration of the AWS Storage Gateway service that provides your applications a file interface to seamlessly store files as objects in Amazon S3, and access them using industry standard file protocols.

**Q: What can I do with Amazon S3 File Gateway?**

Use cases for [Amazon S3 File Gateway](https://aws.amazon.com/storagegateway/file/s3/) include: (a) migrating on-premises file data to Amazon S3, while maintaining fast local access to recently accessed data, (b) backing up on-premises file data as objects in Amazon S3 (including Microsoft SQL Server and Oracle databases and logs), with the ability to use S3 capabilities such as lifecycle management and cross region replication, and, (c) hybrid cloud workflows using data generated by on-premises applications for processing by AWS services such as machine learning, big data analytics or serverless functions.

**Q: What are the benefits of using File Gateway to store data in S3?**

Amazon S3 File Gateway enables your existing file-based applications, devices, and workflows to use Amazon S3, without modification. Amazon S3 File Gateway securely and durably stores both file contents and metadata as objects, while providing your on-premises applications low-latency access to cached data.

**Q: Which Amazon S3 storage classes does S3 File Gateway support?**

Amazon S3 File Gateway supports Amazon S3 Standard, S3 Intelligent-Tiering, S3 Standard - Infrequent Access (S3 Standard-IA) and S3 One Zone-IA. For details on storage classes, refer to the [Amazon S3 documentation](https://docs.aws.amazon.com/AmazonS3/latest/dev/storage-class-intro.html). You configure the initial storage class for objects that the gateway creates, and then you can use bucket lifecycle policies to move files from Amazon S3 to Amazon S3 Glacier. If an application attempts to access a file/object stored through Amazon File Gateway that is now in Amazon S3 Glacier, you will receive a generic I/O error.

**Q: What protocols does Amazon S3 File Gateway support?**

Amazon S3 File Gateway supports Linux clients connecting to the gateway using Network File System (NFS) versions 3 and 4.1, and supports Windows clients connecting to the gateway using Server Message Block (SMB) versions 2 and 3.

**Q: How can I create and use a file share?**

You can create an NFS or SMB file share using the AWS Management Console or service API and associate the file share with a new or existing Amazon S3 bucket. To access the file share from your applications, you mount it from your application using standard UNIX or Windows commands. For convenience, example command lines for each environment are shown in the management console.

**Q: What options do I have to configure an NFS file share?**

You can configure your NFS file share with administrative controls such as limiting access to specific NFS clients or networks, read-only or read-write, or enabling user permission squashing.

**Q: What options do I have to configure an SMB file share?**

You can configure your SMB file share to be accessed by Active Directory (AD) users only or provide authenticated guest access to users in your organization. You can further limit access to the file share as read-only or read-write, or to specific AD users and groups.

**Q: Does Amazon S3 File Gateway support access-based enumeration for SMB file shares?**

Yes, you can configure access-based enumeration for your SMB file shares to prevent users from seeing folders and files that they would not be able to open based on their access permissions. You can also control whether the file shares on the Amazon S3 File Gateway are browsable by users.

**Q: Does Amazon S3 File Gateway support integration with on-premises Microsoft Active Directory (AD)?**

Yes, Amazon S3 File Gateway integrates with Microsoft Active Directory on-premises as well as with in-cloud Active Directory solutions such as Managed Microsoft AD.

**Q: Can I export an SMB file share without Active Directory?**

Yes. You can export an SMB file share using a guest username and password. You will need to change the default password using the Console or service API before setting up your file share for guest access.

**Q: Can I export a mix of NFS and SMB file shares on the same gateway?**

Yes.

**Q: Can I export an NFS and SMB file share on the same bucket?**

No. Currently, file metadata, such as ownership, stored as S3 object metadata cannot be mapped across different protocols.

**Q: How does Amazon S3 File Gateway access my S3 bucket?**

Amazon S3 File Gateway uses an AWS Identity and Access Management (IAM) role to access your S3 bucket. You can [set up an IAM role yourself](https://docs.aws.amazon.com/storagegateway/latest/userguide/managing-gateway-file.html#grant-access-s3) or have it automatically set up by the AWS Storage Gateway Management Console. For automatic setup, AWS Storage Gateway will create a new IAM role in your account and associate it with an IAM Access Policy to access your S3 bucket. The IAM role and IAM access policy are created in your account and you can fully manage them yourself.

**Q: How does my application access my file share?**

To use the file share, you mount it from your application using standard UNIX or Windows commands. For convenience, example command lines are shown in the management console.

**Q: How is my file share mapped to my S3 bucket?**

The file share can be mapped to the root of the S3 bucket or it can be mapped to an S3 prefix within an S3 bucket. If you specify an S3 prefix when creating a file share you are tying the file share to the S3 prefix. If you do not create an S3 prefix when creating a file share then the file share is tied to the root of the S3 bucket.

**Q: Can I give my file share a custom name?**

Yes, the file share name does not have to be the same as the S3 bucket or S3 prefix names.

**Q: Can I change my file share name?**

Yes, you can change your file share name.

**Q: What is the relationship between files and objects?**

Files are stored as objects in your S3 buckets and you can configure the initial storage class for objects that File Gateway creates. There is a one-to-one relationship between files and objects, and you can configure the initial storage class for objects that Amazon S3 File Gateway creates.

The object key is derived from the file path within the file system. For example, if you have a gateway with hostname _file.amazon.com_ and have mapped _my-bucket/my-prefix_, then File Gateway will expose a mount point called _file.amazon.com:/export/my-bucket/my-prefix_. If you then mount this locally on _/mnt/my-bucket/my-prefix_ and create a file named file.html in a directory _/mnt/my-bucket/my-prefix/dir_ this file will be stored as an object in the bucket my-bucket with a key of _my-prefix/dir/file.html_. Creating sparse files will result in a non-sparse zero-filled object in S3.  

**Q: What file system operations are supported by Amazon S3 File Gateway?**

Your clients can create, read, update, and delete files and directories. Your clients can also change permissions and ownership of files and folders. Files are stored as individual objects in Amazon S3. Directories are managed as folder objects in S3, using the same syntax as the S3 console. Symbolic links and hard links are not supported. Attempting to create a link will result in an error. Common file operations change file metadata, which results in the deletion of the current S3 object and the creation of a new S3 object.

Rename operations will appear atomic to your clients, but S3 does not support renaming of objects. When you rename a file or directory the gateway performs copy-put requests to create a copy of the objects in S3 under the new keys and then deletes the original objects. This avoids having to re-send large files over the network. Renaming directories containing a large number of files is not instantaneous, will result in 2 copies of your data being stored in S3, and operations in the directories will be blocked until the rename operation completes.  

**Q: What file system metadata can my client access and where is the metadata stored?**

Your clients can access POSIX-style metadata including ownership, permissions, and timestamps that are durably stored in S3 in the user metadata of the object associated with the file. When you create a file share on an existing bucket, the stored metadata will be restored and made accessible to your clients.

**Q: How do I set the Content-Type for files uploaded to S3?**

For each file share, you can enable guessing of MIME types for uploaded objects [upon creation](http://docs.aws.amazon.com/storagegateway/latest/userguide/GettingStartedCreateFileShare.html) or [enable the feature later](http://docs.aws.amazon.com/storagegateway/latest/userguide/managing-gateway-file.html#update-file-share). If enabled, File Gateway will use the filename extension to determine the MIME type for the file and set the S3 objects Content-Type accordingly. This is beneficial if you are using File Gateway to manage objects in S3 that you access directly via URL or distribute through Amazon CloudFront.

**Q: Can I directly access objects stored in S3 by using Amazon S3 File Gateway?**

Yes. Once objects are stored in S3, you can access them directly in AWS for in-cloud workloads without requiring Amazon S3 File Gateway. Your objects inherit the properties of the S3 bucket in which they are stored, such as lifecycle management, and cross-region replication.

An object that needs to be accessed by using a file share should only be managed by the gateway. If you directly overwrite or update an object previously written by Amazon S3 File Gateway, it results in undefined behavior when the object is accessed through the file share.

**Q: What if my bucket already contains objects?**

If your bucket already contains objects when you configure it for use with Amazon S3 File Gateway, object keys will be used to present the objects as files to the NFS and SMB clients. The files are given default file system metadata.

To reduce latency and number of Amazon S3 requests, Amazon S3 File Gateway only scans the headers for file metadata associated with the objects when you explicitly list the files or directories. File metadata is collected as a part of that scan; file contents are downloaded only when the object is read.  

**Q: How are buckets accessed by the gateway? Are entire bucket or file contents downloaded?**

The gateway does not automatically download full objects or all the data that exists in your bucket; data is only downloaded when it is explicitly accessed by your clients. Additionally, to reduce data transfer overhead, File Gateway uses multipart uploads and copy put, so only changed data in your files is uploaded to S3.

**Q: What metadata can my NFS client access for objects created outside of the gateway?**

For objects uploaded to the S3 bucket directly, i.e. not using File Gateway and an NFS share, you can configure default ownership and permissions.

**Q: What metadata can my SMB client access for objects created outside of the gateway?**

For objects uploaded to the S3 bucket directly, i.e. without using Amazon S3 File Gateway and an SMB share, metadata such as ownership and permissions will be inherited from the object’s parent folder. Permissions at the root of the share are fixed and objects created directly under the root folder will inherit these fixed permissions. Refer to the documentation on metadata settings of objects created outside the gateway.

**Q: Can I use multiple NFS clients with a single Amazon S3 File Gateway?**

You can have multiple NFS clients accessing a single File Gateway. However, as with any NFS server, concurrent modification from multiple NFS clients can lead to unpredictable behavior. Application level coordination is required to do this in a safe way.

**Q: Can I have multiple writers to my S3 bucket?**

No. We recommend a single writer to objects in your S3 bucket. If you directly overwrite or update an object previously written by File Gateway, it results in undefined behavior when the object is accessed through the file share. Concurrent modification of the same object (e.g. via the S3 API and the Amazon S3 File Gateway) can lead to unpredictable results and we recommend against this configuration.

**Q: Can I have two gateways writing independent data to the same bucket?**

We do not recommend configuring multiple writers to a single bucket because it can lead to unpredictable results. You could enforce unique object names or prefixes through your application workflow. S3 File Gateway will emit Health Notifications when conflicts occur in such a setup.

**Q: Can I have multiple gateways reading data from the same bucket?**

Yes, you can have multiple readers on a bucket managed through an Amazon S3 File Gateway. You can configure a file share as read-only, and allow multiple gateways to read objects from the same bucket. Additionally, you can refresh the inventory of objects that your gateway knows about using the [Storage Gateway Console](https://docs.aws.amazon.com/storagegateway/latest/userguide/managing-gateway-file.html#refresh-cache), the automated periodic cache refresh process, or the [RefreshCache API](http://docs.aws.amazon.com/storagegateway/latest/APIReference/API_RefreshCache.html).

Note however that if you do not configure a file share as read-only, Amazon S3 File Gateway does not monitor or restrict these readers from inadvertently writing to the bucket. It is up to you to maintain a single writer/multi reader configuration from your application.

**Q: Can I monitor my file share using Amazon CloudWatch?**

Yes, you can monitor usage of your file share using Amazon CloudWatch metrics and get notified on completion of file operations through CloudWatch Events. To learn more, visit [Monitoring your File Share](https://docs.aws.amazon.com/storagegateway/latest/userguide/monitoring-file-gateway.html).

**Q: How do I know when my file is uploaded?**

When you write files to your file share with Amazon S3 File Gateway, the data is stored locally first and then asynchronously uploaded to your S3 bucket. You can request [notifications through AWS CloudWatch Events](https://docs.aws.amazon.com/storagegateway/latest/userguide/monitoring-file-gateway.html#get-notification) when the upload of an individual file completes. These notifications can be used to trigger additional workflows, such as invoking an AWS Lambda function or Amazon EC2 Systems Manager Automation, which is dependent upon the data that is now available in S3. To learn more, please refer to [the documentation for File Upload Notification](https://docs.aws.amazon.com/storagegateway/latest/userguide/monitoring-file-gateway.html#get-file-upload-notification).

**Q: How is a file upload notification different from an S3 event notification?**

The file upload notification provides a notification for each individual file that is uploaded to Amazon S3 through S3 File Gateway. S3 event notifications provide notifications that include partial file uploads so there is no way to tell from the S3 event notification that the file upload has completed.

**Q: How do I know when my working file set is uploaded?**

When you write files to your file share with Amazon S3 File Gateway, the data is stored locally first and then asynchronously uploaded to your S3 bucket. You can [request notifications through Amazon CloudWatch Events](https://docs.aws.amazon.com/storagegateway/latest/userguide/monitoring-file-gateway.html#get-notification) when the upload of a working file set completes. These notifications can be used to trigger additional workflows, such as invoking an AWS Lambda function or Amazon EC2 Systems Manager Automation, which is dependent upon the data that is now available in S3. To learn more, please refer to [the documentation for Working File Set Upload Notification](http://docs.aws.amazon.com/storagegateway/latest/APIReference/API_NotifyWhenUploaded.html).

**Q: Can I update my Amazon S3 File Gateway’s view of a bucket to see objects created from an object-based workload or another File Gateway?**

Yes, you can refresh the inventory of objects that your Amazon S3 File Gateway knows about using the Console, the file system driven cache refresh process, or the RefreshCache API. You will receive [notifications through AWS CloudWatch Events](https://docs.aws.amazon.com/storagegateway/latest/userguide/monitoring-file-gateway.html#get-notification) when the RefreshCache API operation has completed. These notifications can be used to send emails using Amazon Simple Notification Service (SNS), or trigger local processing using the updated contents. To learn more, please refer to [the documentation](https://docs.aws.amazon.com/storagegateway/latest/userguide/monitoring-file-gateway.html#refresh-cache-notification).

**Q: Can I use the gateway to update data in a bucket that belongs to another AWS account?**

Yes, you can use the gateway for cross-account access to buckets. To learn more, please refer to the [documentation for Using File Share for Cross-Account access](https://docs.aws.amazon.com/storagegateway/latest/userguide/managing-gateway-file.html#cross-account-access).

**Q: Can I use the gateway to access data in Requester Pays S3 buckets?**

Yes, when creating your file share you can enable access to [Requester Pays S3 buckets](https://docs.aws.amazon.com/AmazonS3/latest/dev/RequesterPaysBuckets.html). As a requester, you will incur the charges associated with accessing data from Requester Pays buckets.

**Q: How do I create multiple shares per bucket in a gateway?**

You can create multiple file shares for a single S3 bucket by specifying an S3 prefix during file share creation process.

**Q: How many file shares can I create per gateway?**

You can create up to 50 shares for an S3 bucket in a single gateway. We do not limit the number of file shares per bucket across multiple gateways but each gateway is limited to 50 shares. However, we recommend having a single writer to the bucket, either an Amazon S3 File Gateway or client accessing S3 directly.

**Q: Can I change the name of a file share?**

Yes, you can change the name of a file share.

**Q: What is the maximum size of an individual file?**

The maximum size of an individual file is 5 TB, which is the maximum size of an individual object in S3. If you write a file larger than 5 TB, you will get a "file too large" error message and only the first 5 TB of the file will be uploaded.

**Q: My application checks storage size before copying data. What storage size does the gateway return?**

The gateway returns a large number (8 EB) as your total capacity. Amazon S3 does not limit total storage.

**Q: Can I use Amazon S3 lifecycle, cross-region replication, and S3 event notification with File Gateway?**

Yes. Your bucket policies for lifecycle management, cross-region replication, and S3 event notification, apply directly to objects stored in your bucket through AWS Storage Gateway.

You can use S3 lifecycle policies to change an object's storage tier or delete old objects or object versions. In the case of objects deleted by lifecycle policy, you will need to enable the periodic cache refresh feature or call the [RefreshCache API](http://docs.aws.amazon.com/storagegateway/latest/APIReference/API_RefreshCache.html) to reflect these changes to your NFS clients.

When using an S3 bucket that is the target for cross-region replication, you may need to enable the periodic cache refresh feature or use the [RefreshCache API](http://docs.aws.amazon.com/storagegateway/latest/APIReference/API_RefreshCache.html) to ensure the gateway cache and S3 bucket are in sync.

If using S3 event notifications you may receive events for partial files created by the gateway to ensure your data is durably stored in S3. Partial files may occur for a number of reasons, such as the gateway needing to free up cache space, or a high rate of writes to a file. These partial files may not be application consistent.

**Q: Can I use Amazon S3 File Gateway with my backup application?**

Amazon S3 File Gateway supports SMB versions 2 and 3 as well as NFS versions 3, 4.0, and 4.1. We are continuing to do ongoing testing with common backup apps. Please let us know via AWS Support or through your AWS account team of any specific apps with which you'd like to see compatibility tested.

**Q: Can I use Amazon S3 File Gateway to write files to EFS?**

No. Amazon S3 File Gateway allows you to store files as objects in S3.

**Q: When should I use Amazon S3 File Gateway vs. the S3 API?**

You can use Amazon S3 File Gateway when you want to access objects in S3 as files using standard filesystem operations. Amazon S3 File Gateway additionally provides low-latency local access and efficient data transfer. You can use the S3 API when your application doesn’t require file system operations and can manage data transfer directly.

**Q: How does Amazon S3 File Gateway manage the local cache? What data gets stored locally?**

Local disk storage on the gateway is used to temporarily hold changed data that needs to be transferred to AWS, and to locally cache data for low-latency read access. File Gateway automatically manages the cache maintaining the most recently accessed data based on client read and write operations. Data is evicted from the cache only when space is needed to store more recently used data.

To maximize write performance, the gateway uses a write-back mechanism where data is first persisted to disk and then asynchronously uploaded to S3. The gateway serves data from the local cache to maximize read performance. If not present, data is efficiently synchronously fetched from Amazon S3 using byte-range gets.

The local cache should generally be sized for the working set of data that you need low-latency access to. If the cache is too small then read latencies will increase as data being requested must be fetched from S3, and writes could fail if there is no free cache space to store data locally pending upload to S3.

**Q: What guidance should I use to provision the size of the gateway’s cache disk? What happens if I provision a smaller cache disk?**

You should provision your cache based on:  
1/ The size of your working dataset to which you need low-latency access, so you can reduce read latencies by decreasing the frequency with which data is requested from S3, and  
2/ The size of files written to the gateway by your applications.

Smaller cache disks can result in poor performance and failures during writes if there is no free cache space to store data locally when pending upload to S3. To learn more about monitoring your cache usage, refer to [Monitoring Your File Share](https://docs.aws.amazon.com/storagegateway/latest/userguide/monitoring-file-gateway.html) in the documentation.

**Q: When does data in the cache get evicted?**

Data written to the cache from your applications or through retrieval from Amazon S3 is evicted from the cache only when space is needed to store more recently accessed data.

**Q: Does Amazon S3 File Gateway perform data reduction (deduplication or compression)?**

No. Files are mapped to objects one-to-one in your bucket without modification, enabling you to access your data directly in S3 without needing to use the gateway or deploy additional software to rehydrate your data.

Amazon S3 File Gateway uses multipart uploads and copy put, so only changed data is uploaded to S3, which can reduce data transfer. The gateway does not automatically download full objects or all the data that exists in your bucket; data is only downloaded when explicitly accessed by your NFS client.

**Q: Can I use Amazon S3 File Gateway with Amazon S3 Transfer Acceleration?**

File Gateway will not use the accelerated endpoints even if your bucket is configured for S3 Transfer Acceleration.