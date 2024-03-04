---
tags:
  - cloud/aws
reviewed: 2023-12-16
review-frequency: normal
---
![[Pasted image 20240213123734.png]]<mark style="background: #BBFABBA6;">Whilst there are many companies who are cloud native, or fully migrated away from their data centers, there is a large contingent of AWS customers who still maintain an on-premises footprint, whether it is for compliance reasons, or because they simply haven’t migrated yet.</mark>

For these Hybrid Cloud customers, there is a range of tools and services that AWS has to offer, one of them being AWS Data Sync.

## What is AWS DataSync?

<mark style="background: #ABF7F7A6;">With AWS DataSync, AWS allows you to migrate your data in a simple and secure way. AWS Data Sync allows you to transfer between on-premises and AWS, between AWS storage services and even between different cloud providers.</mark>

The AWS DataSync service is <mark style="background: #ADCCFFA6;">a secure, online data transfer service for moving large amounts of data, efficiently, and automatically, to and from many different locations.</mark> You can migrate and replicate any of your sets of data natively within DataSync. 

This can all be done whilst avoiding building custom solutions or wasting time on difficult and repetitive tasks.

<mark style="background: #ADCCFFA6;">AWS DataSync supports a number of different data formats, spanning file systems, object storage both within cloud environments and from an on-premises environment. </mark> 
  
DataSync is available through the console or the AWS CLI (Command Line Interface) and can be used to move data between many different sources and destinations==.==

<mark style="background: #BBFABBA6;">If you want to perform any kind of migration, or any kind of data relocation where the end point is within AWS – AWS DataSync will likely help you achieve your goals. </mark>  
![[Pasted image 20240213124107.png]]  
![[Pasted image 20240213124152.png]]
## Features

**AWS DataSync** has a number of different features which make it a desirable tool to use for any kind of data migration. 

As with many AWS services, AWS employs their own custom features. In this case their own custom transfer protocol – which decides the specifics of how data is sent over a network and when. This is all designed to speed up data migration compared to traditional tools. 

<mark style="background: #ADCCFFA6;">It is possible to schedule tasks to run periodically, to detect and copy changes from your source storage system to the destination storage system.</mark>  
<mark style="background: #D2B3FFA6;">In order to move files directly into your Amazon VPC, DataSync supports VPC endpoints (powered by AWS PrivateLink).</mark>

<mark style="background: #BBFABBA6;">You can create tasks based on a schedule with AWS DataSync, to perform migrations on a time-oriented basis as and when you require. </mark>

<mark style="background: #FFB86CA6;">Files can be copied into EFS using AWS DataSync, and files that have not been accessed for a specified period can be migrated to Infrequent Access (IA) storage.</mark>

<mark style="background: #D2B3FFA6;">DataSync is a fully managed service, which means that there is no infrastructure that you must provision.  
</mark>  
<mark style="background: #083CA4A6;">DataSync integrates seamlessly with Amazon EventBridge. You can set it to trigger an event when a transfer completes, thereby automating your workflows. </mark>

During transit and in rest, DataSync performs integrity checks to ensure your data arrives intact. 

At rest, encryption is either done by SSE-S3 or by the Key Management Service. In transit, it uses TLS 1.2 and in transit it uses TLS 1.2 and SSE-S3. 

When you use DataSync with S3, it supports storing data directly into any S3 storage class. You do not need to use lifecycle policies or manually transfer data from S3. 

## Use Cases

- <mark style="background: #D2B3FFA6;">Data migration to Amazon S3, Amazon EFS, or Amazon FSx for Windows File Server can all take place.</mark>
- <mark style="background: #FFF3A3A6;">You can use AWS DataSync to transfer expensive archival storage into S3 Glacier Flexible Retrieval, Glacier Instant Retrieval, as well as the archival classes – Glacier and Glacier Deep archive</mark>.
- Some organizations have AWS environments that use both an on-premises data center and a cloud-based solution.  
	Large volumes of data might be generated in the on-premises environment that need to be transferred to AWS for processing.

To ensure your data is protected, you can use AWS DataSync to back up your on-premises solutions to AWS.

- DataSync can be used to replicate and store a copy of your data in Amazon Web Services. To ensure that your data is stored securely at rest, you can turn on the encryption settings on all of these services. 

<mark style="background: #ABF7F7A6;">DataSync Agent allows you to run DataSync on-premises as a virtual machine, supporting hybrid cloud deployments. </mark>  
	The DataSync VM image is provided as an Amazon Machine Image (AMI) to be run on an EC2 instance.  
	To communicate with AWS, the agent VM needs access to certain endpoints. You must configure your firewall to allow this communication.

## Pricing

DataSync charges a flat fee per gigabyte for network acceleration technology, managed cloud infrastructure, data validation, and automation capabilities. 

AWS services, such as Amazon S3, Amazon EFS, Amazon FSx for Windows File Server, and AWS Key Management Service (KMS) charge standard request, storage, and data transfer rates.

You pay AWS Data Transfer at your standard rate when copying data from AWS to an on-premises storage system. In addition, Amazon CloudWatch Logs, Amazon CloudWatch Events, and Amazon CloudWatch Metrics are charged at standard rates.

The AWS PrivateLink service will charge you for interface VPC endpoints that you create to manage and control traffic between your agent(s) and the DataSync service.

## Limits

![](https://lh5.googleusercontent.com/zp6PrnDMi2qAFP1b5iCMBcnDv9hb-WRVOGdwMfjX9DvlAvIyBewcBF6V68d__TeYJBlmcK8iWDrBSbFY7DzhXygEo5Y_DYiG2ZbuqTCPusOnyCruXbw12U6bFRjmvGnXmsKa4QkFxJc3Qu9YkQ)

![[AWS Solutions Architect Skillbuilder#AWS DataSync]]

# FAQ
## General

**Q: What is AWS DataSync?**

A: AWS DataSync is an online data movement and discovery service that simplifies and accelerates data migrations to AWS as well as moving data to and from on-premises storage, edge locations, other cloud providers, and AWS Storage services.

AWS DataSync Discovery helps you simplify migration planning and accelerate your data migration to AWS by giving you visibility into your on-premises storage performance and utilization, and providing recommendations for migrating your data to AWS Storage services. DataSync Discovery enables you to better understand your on-premises storage performance and capacity usage through automated data collection and analysis, enabling you to quickly identify data to be migrated and use generated recommendations to select AWS Storage services that align to your performance and capacity needs.

For online data transfers, AWS DataSync simplifies, automates, and accelerates copying large amounts of data to and from on-premises storage, edge locations, other cloud providers, and AWS Storage services. DataSync can copy data to and from Network File System (NFS) shares, Server Message Block (SMB) shares, Hadoop Distributed File Systems (HDFS), self-managed object storage, Google Cloud Storage, Azure Files, Azure Blob Storage including Azure Data Lake Storage Gen2, Wasabi Cloud Storage, Oracle Cloud Storage, Cloudflare R2 Storage, DigitalOcean Spaces, Backblaze B2 Cloud Storage, [AWS Snowcone](https://aws.amazon.com/snowcone/), Amazon S3 compatible storage on Snow, Amazon Simple Storage Service ([Amazon S3](https://aws.amazon.com/s3/)), Amazon Elastic File System ([Amazon EFS](https://aws.amazon.com/efs/)) file systems, [Amazon FSx for Windows File Server](https://aws.amazon.com/fsx/windows/) file systems, [Amazon FSx for Lustre](https://aws.amazon.com/fsx/lustre/ "Amazon FSx for Lustre") file systems, [Amazon FSx for OpenZFS](https://aws.amazon.com/fsx/openzfs/ "Amazon FSx for OpenZFS") file systems, and [Amazon FSx for NetApp ONTAP](https://aws.amazon.com/fsx/netapp-ontap/) file systems.

**Q: Why should I use AWS DataSync?**

A: AWS DataSync enables you to discover and move your data, securely and quickly. Using DataSync Discovery, you can better understand your on-premises storage utilization and receive recommendations to inform your cost estimates and plans for migrating to AWS. For data movement, you can use DataSync to copy large datasets with millions of files, without having to build custom solutions with open-source tools, or license and manage expensive commercial network acceleration software. You can use DataSync to migrate active data to AWS, archive data to free up on-premises storage capacity, replicate data to AWS for business continuity, or transfer data to the cloud for analysis and processing.

**Q: What problem does AWS DataSync Discovery solve for me?**

A: AWS DataSync Discovery simplifies and accelerates data migration to AWS. Using DataSync Discovery, you can automatically collect data about your on-premises storage systems and view the aggregated results in the DataSync console. DataSync Discovery analyzes performance, capacity, and utilization from the collected data and recommends AWS Storage services for migration. With DataSync Discovery you can better understand your on-premises storage utilization, quickly identify data to be migrated, and select AWS Storage services that meet your performance needs and optimize your storage costs.  

**Q: What problem does AWS DataSync solve for me?**

A: AWS DataSync reduces the complexity and cost of online data transfer, making it simple to transfer datasets to and from on-premises storage, edge locations, other cloud providers and AWS Storage services. DataSync connects to existing storage systems and data sources with standard storage protocols (NFS, SMB), as an HDFS client, using the Amazon S3 API, or using other cloud storage APIs. It uses a purpose-built network protocol and scale-out architecture to accelerate data transfer between storage systems and AWS services. DataSync automatically scales and handles moving files and objects, scheduling data transfers, monitoring the progress of transfers, encryption, verification of data transfers, and notifying customers of any issues. With DataSync you pay only for the amount of data copied, with no minimum commitments or upfront fees.

### Discovery

**Q: What storage systems are supported by AWS DataSync Discovery?**

AWS DataSync Discovery currently supports NetApp FAS and AFF series arrays running ONTAP 9.7 or later. Support for additional storage systems will be added over time.

**Q: What information does AWS DataSync Discovery collect about my storage system?**

AWS DataSync Discovery uses your storage management API interface to collect information about your storage system along with performance and utilization metrics. System information includes attributes such as total storage capacity, volume configuration, export/share names, and more. Storage system metrics include performance such as volume throughput and IOPS along with utilization metrics such as allocated and used capacity. DataSync Discovery uses the collected system information and metrics to generate recommendations for migrating to AWS Storage.

**Q: How does AWS DataSync Discovery determine its recommendations?**

AWS DataSync Discovery analyzes the data collected from your on-premises storage system and matches it against the features, capacity, and performance capabilities of AWS storage services. Where appropriate, DataSync Discovery will recommend one or more AWS storage services for your consideration.

**Q: Can I use AWS DataSync Discovery with my production systems? What impact will it have on my users and applications?**

There will be no noticeable impact to users and applications when AWS DataSync Discovery is used with your on-premises storage systems.

**Q: Where does AWS DataSync Discovery store data collected about my storage systems?**

Collected data will be stored and managed by the DataSync service. Data can be viewed in the AWS DataSync console or accessed using the AWS CLI or AWS Software Development Kit (SDK).

**Q: How long does AWS DataSync Discovery store data collected by a discovery job?**

Collected data and recommendations will be retained for 60 days following the end of a discovery job.

### Data Movement

**Q: Where can I move data to and from?**
>DataSync supports the following storage location types: Network File System (NFS) shares, Server Message Block (SMB) shares, Hadoop Distributed File Systems (HDFS), self-managed object storage, Google Cloud Storage, Azure Files, Azure Blob Storage including Azure Data Lake Storage Gen2, Wasabi Cloud Storage, Oracle Cloud Storage, Cloudflare R2 Storage, DigitalOcean Spaces, Backblaze B2 Cloud Storage, AWS Snowcone, Amazon S3 compatible storage on Snow, Amazon Simple Storage Service (Amazon S3), Amazon Elastic File System (Amazon EFS) file systems, Amazon FSx for Windows File Server file systems, Amazon FSx for Lustre file systems, Amazon FSx for OpenZFS file systems, and Amazon FSx for NetApp ONTAP file systems.

**Q:  How do I use AWS DataSync to migrate data to AWS?**

A: You can use AWS DataSync to migrate data located on premises, at the edge, or in other clouds to <mark style="background: #FFF3A3A6;">Amazon S3, Amazon EFS, Amazon FSx for Windows File Server, Amazon FSx for Lustre, Amazon FSx for OpenZFS, and Amazon FSx for NetApp ONTAP</mark>.  
Configure DataSync to make an initial copy of your entire dataset, and schedule subsequent incremental transfers of changing data until the final cut-over from on-premises to AWS.  
<mark style="background: #CACFD9A6;">DataSync includes encryption and integrity validation to help make sure your data arrives securely, intact, and ready to use</mark>.  
To minimize impact on workloads that rely on your network connection, you can schedule your migration to run during off-hours, or limit the amount of network bandwidth that DataSync uses by configuring the built-in bandwidth throttle. DataSync preserves metadata between storage systems that have similar metadata structures, enabling a smooth transition of end users and applications to using your target AWS Storage service.

Read the storage blog, "[Migrating storage with AWS DataSync](https://aws.amazon.com/blogs/storage/migrating-storage-with-aws-datasync/)," to learn more about migration best practices and tips.  

**Q: How do I use AWS DataSync to archive cold data?**

A: You can use AWS DataSync to move cold data from on-premises storage systems directly to durable and secure long-term storage, such as [Amazon S3 Glacier Flexible Retrieval](https://aws.amazon.com/s3/storage-classes/glacier/) (formerly S3 Glacier) or [Amazon S3 Glacier Deep Archive](https://aws.amazon.com/s3/storage-classes/glacier/). Use [DataSync’s filtering functionality](https://aws.amazon.com/blogs/storage/excluding-and-including-specific-data-in-transfer-tasks-using-aws-datasync-filters/) to exclude copying temporary files and folders or copying only a subset of files from your source location. You can select the most cost-effective storage service for your needs: transfer data to any [S3 storage class](https://aws.amazon.com/s3/storage-classes/), or use DataSync with EFS Lifecycle Management to store data in [Amazon EFS Infrequent Access storage class (EFS IA)](https://docs.aws.amazon.com/efs/latest/ug/lifecycle-management-efs.html). Use the built-in task scheduling functionality to regularly archive data that should be retained for compliance or auditing purposes, such as logs, raw footage, or electronic medical records.   

**Q: How do I use AWS DataSync to replicate data to AWS for business continuity?**

A: With AWS DataSync, you can periodically replicate files into any Amazon S3 storage classes, or send the data to Amazon EFS, Amazon FSx for Windows File Server, Amazon FSx for Lustre, Amazon FSx for OpenZFS, or Amazon FSx for NetApp ONTAP for a standby file system. Use the built-in task scheduling functionality to ensure that changes to your dataset are regularly copied to your destination storage. Read this AWS Storage blog to [learn more about data protection using AWS DataSync](https://aws.amazon.com/blogs/storage/protect-your-file-and-backup-archives-using-aws-datasync-and-amazon-s3-glacier/).  

**Q: How do I use AWS DataSync for recurring transfers between on-premises and AWS for ongoing workflows?**

A: You can use AWS DataSync for ongoing transfers from on-premises systems into or out of AWS for processing. DataSync can help speed up your critical hybrid cloud storage workflows in industries that need to move active files into AWS quickly. This includes machine learning in life sciences, video production in media and entertainment, big data analytics in financial services, and seismic research in oil and gas. DataSync provides timely delivery to ensure dependent processes are not delayed. You can specify [exclude filters, include filters, or both](https://aws.amazon.com/blogs/storage/excluding-and-including-specific-data-in-transfer-tasks-using-aws-datasync-filters/), to determine which files, folders or objects gets transferred each time your task runs.  

**Q: Can I use AWS DataSync to copy data from other clouds to AWS?**

A: Yes. Using AWS DataSync, you can copy data from Google Cloud Storage using the Amazon S3 API, from [Azure Files using the SMB protocol](https://aws-blogs-prod.amazon.com/storage/how-to-move-data-from-azure-files-smb-shares-to-aws-using-aws-datasync/), or from Azure Blob Storage including Azure Data Lake Storage Gen 2. You can also move data from Wasabi Cloud Storage, Oracle Cloud Storage, Cloudflare R2 Storage, DigitalOcean Spaces, and Backblaze B2 Cloud Storage. Deploy the DataSync agent in your cloud environment or on Amazon EC2,  create your source and destination locations, and then start your task to begin copying data. [Learn more](https://aws-blogs-prod.amazon.com/storage/how-to-move-data-from-azure-files-smb-shares-to-aws-using-aws-datasync/) about AWS solutions for hybrid and multicloud environments.

**Q: Can I use AWS DataSync to build my data lake?**

A: Yes. With AWS DataSync, you can easily build your data lake, by automating the transfer of on-premises datasets or data in other clouds to Amazon S3. DataSync enables a simple and fast transfer of your entire data set using standard storage protocols (NFS, SMB), as an HDFS client, using the Amazon S3 API, or using other cloud storage APIs. After transferring your initial dataset, you can schedule subsequent transfers of new data to AWS. DataSync includes encryption and integrity validation to help make sure your data arrives securely, intact, and ready to use. To minimize impact on workloads that rely on your network connection, you can schedule transfer tasks to run during off-hours, or limit the amount of network bandwidth that DataSync uses by configuring the built-in bandwidth throttle. Once your data lands in Amazon S3, you can use native AWS services to run big data analytics, artificial intelligence (AI), machine learning (ML), high-performance computing (HPC) and media data processing applications to gain insights from your unstructured data sets. Read the [AWS data lake storage web page](https://aws.amazon.com/products/storage/data-lake-storage/) to learn more about building and leveraging your data lake.  

**Q: How do I use AWS DataSync to transfer data between AWS Storage services?**

A: You can use DataSync to transfer files or objects between Amazon S3, Amazon EFS, Amazon FSx for Windows File Server, Amazon FSx for Lustre, Amazon FSx for OpenZFS, or Amazon FSx for NetApp ONTAP within the same AWS account. You can transfer data between AWS services in the same AWS Region, between services in different Commercial AWS Regions except for China, or between AWS GovCloud (US-East and US-West) Regions. This does not require deploying a DataSync agent, and can be configured end to end using the AWS DataSync console, AWS Command Line Interface (CLI), or AWS Software Development Kit (SDK).

## Usage

**Q: How do I get started using AWS DataSync Discovery?**

Get started by deploying an AWS DataSync agent into your on-premises [VM environment.](https://docs.aws.amazon.com/datasync/latest/userguide/agent-requirements.html) Using the DataSync console, CLI, or SDK, configure DataSync Discovery to connect to your on-premises storage and run discovery jobs to collect data about your storage system along with performance, capacity, and utilization metrics. While your discovery jobs run, information about your storage systems can be viewed from dashboards in the DataSync console. When a discovery job completes, the collected data is analyzed to produce recommendations for migrating to AWS storage services such as Amazon EFS, Amazon FSx, and Amazon S3. These recommendations can be used to guide your selection of AWS Storage services and you can use AWS DataSync to move your data.

**Q: How do I get started moving my data with AWS DataSync?**

A: You can transfer data using AWS DataSync with a few clicks in the [AWS Management Console](https://docs.aws.amazon.com/datasync/latest/userguide/getting-started.html) or through the [AWS Command Line Interface (CLI)](https://docs.aws.amazon.com/datasync/latest/userguide/using-cli.html). To get started, follow these 3 steps:

<u>1. To transfer data between on-premises, edge, or other cloud storage systems and AWS Storage services, deploy an agent</u> - Deploy a DataSync agent and associate it to your AWS account via the Management Console or API. The agent will be used to access your NFS server, SMB file share, Hadoop cluster, or self-managed or cloud object storage to read data from it or write data to it. Deploying an agent is not required to transfer data between AWS Storage services within the same AWS account.

<u>2. Create a data transfer task</u> - Create a task by specifying the location of your data source and destination, and any options you want to use to configure the transfer, such as scheduling the task and enabling task reports.

<u>3. Start the transfer</u> - Start the task, monitor data movement in the console or with [Amazon CloudWatch](https://aws.amazon.com/cloudwatch/), and audit transfer tasks using [task reports.  
](https://docs.aws.amazon.com/datasync/latest/userguide/what-is-datasync.html)

**Q: How do I deploy an AWS DataSync agent?  
**

A: You deploy an AWS DataSync agent to your on-premises hypervisor, in your public cloud environment, or in [Amazon EC2](https://aws.amazon.com/ec2/). To copy data to or from an on-premises file server or Amazon S3 compatible storage on Snow, you download the agent virtual machine image from the AWS Console and deploy to your on-premises VMware ESXi, Linux Kernel-based Virtual Machine (KVM), or Microsoft Hyper-V hypervisor. The agent must be deployed so that it can access your file server using the NFS, SMB protocol, access NameNodes and DataNodes in your Hadoop cluster, or access your object storage using the [Amazon S3 API](https://docs.aws.amazon.com/AmazonS3/latest/API/Type_API_Reference.html "Amazon S3 API"). To set up transfers between your S3 on AWS Outposts buckets and S3 buckets in AWS Regions, [deploy the agent on your Outpost](https://docs.aws.amazon.com/datasync/latest/userguide/deploy-agents.html#outposts-agent). To set up transfers between your AWS Snowcone device and AWS storage, use the [DataSync agent AMI that comes pre-installed on your device](https://docs.aws.amazon.com/datasync/latest/userguide/deploy-agents.html#snowcone-agent).

When copying data between your public cloud environment and AWS Storage, you can either deploy the DataSync agent in your cloud environment or on Amazon EC2. Because AWS DataSync compresses data in flight between the AWS DataSync agent and AWS Storage services, you may be able to reduce egress fees by deploying the AWS DataSync agent in your public cloud environment.    

Deploying an agent is not required to transfer data between AWS Storage services within the same AWS account. To copy data to or from a self-managed in-cloud file server, or between AWS Storage services in different AWS accounts, you launch an Amazon EC2 instance using a DataSync agent AMI.  

**Q: What are the resource requirements for the AWS DataSync agent?  
**

A: You can find the minimum required resources to run the agent [here](https://docs.aws.amazon.com/datasync/latest/userguide/agent-requirements.html).

**Q: How do I start an AWS DataSync data transfer task?  
**

A: AWS DataSync copies data when you initiate a task via the [AWS Management Console](https://docs.aws.amazon.com/datasync/latest/userguide/getting-started.html) or [AWS Command Line Interface (CLI)](https://docs.aws.amazon.com/datasync/latest/userguide/using-cli.html). Each time a task runs, it scans the source and destination for changes, and performs a copy of any data and metadata differences between the source to the destination. You can configure which characteristics of the source are used to determine what changed, define [filters to include and exclude specific files or folders](https://docs.aws.amazon.com/datasync/latest/userguide/filtering.html), and control if files or objects in the destination should be overwritten when changed in the source or deleted when not found in the source.

**Q: How does AWS DataSync ensure my data is copied correctly?** 

A: As AWS DataSync transfers and stores data, it performs integrity checks to ensure the data written to the destination matches the data read from the source. Additionally, an optional verification check can be performed to compare source and destination at the end of the transfer. DataSync will calculate and compare full-file checksums of the data stored in the source and in the destination. You can check either the entire dataset or just the files or objects that DataSync transferred.

**Q: How can I audit and monitor the status of data being transferred by AWS DataSync?**

A: You can use [task reports](https://docs.aws.amazon.com/datasync/latest/userguide/task-reports.html) to audit your data transfer processes by verifying the transfer operations across all of your task executions. Using task reports, you can get a summary report along with detailed reports for all files transferred, skipped, verified, and deleted, for each task execution. Task reports give you the total number of files and bytes transferred, and include file attributes such as size, path, timestamps, file checksums, and object version IDs where applicable. You can also leverage AWS Glue, Amazon Athena, and Amazon QuickSight to automatically catalog, query, and visualize task reports to gain critical insights into your data transfer processes.

You can use the AWS Management Console or CLI to monitor the status and progress of data being transferred. Using Amazon CloudWatch Metrics, you can see the [number of files and amount of data which has been copied](https://docs.aws.amazon.com/datasync/latest/userguide/monitor-datasync.html#metrics). You can also [enable logging of individual files to CloudWatch Logs](https://docs.aws.amazon.com/datasync/latest/userguide/create-task.html), to identify what was transferred at a given time, as well as the results of the content integrity verification performed by DataSync.

These solutions together simplify auditing, monitoring, reporting, and troubleshooting, and enable you to provide timely updates to stakeholders.

**Q: Can I filter the files and folders that AWS DataSync transfers?**

A: Yes. You can specify an exclude filter, an include filter, or both to limit which files, folders, or objects are transferred each time a task runs. Include filters specify the file paths or object keys that should be included when the task runs and limits the scope of what is scanned by DataSync on the source and destination. Exclude filters specify the file paths or object keys that should be excluded from being copied. If no filters are configured, each time a task runs it will transfer all changes from the source to the destination. When creating or updating a task, you can configure both exclude and include filters. When starting a task, you can override filters configured on the task. Read this [AWS storage blog to learn more about using common filters with DataSync](https://aws.amazon.com/blogs/storage/excluding-and-including-specific-data-in-transfer-tasks-using-aws-datasync-filters/) for more detail.  

**Q: Can I configure AWS DataSync to transfer on a schedule?**

A: Yes. You can schedule your tasks using the AWS DataSync Console or AWS Command Line Interface (CLI), without needing to write and run scripts to manage repeated transfers. Task scheduling automatically runs tasks on the schedule you configure, with hourly, daily, or weekly options provided directly in the Console. This enables you to ensure that changes to your dataset are automatically detected and copied to your destination storage.  

**Q: Does AWS DataSync preserve the directory structure when copying files?**

A: Yes. When transferring files, AWS DataSync creates the same directory structure on the destination as on the source location's structure.  

**Q: What happens if an AWS DataSync task is interrupted?**

A: If a task is interrupted, for instance, if the network connection goes down or the AWS DataSync agent is restarted, the next run of the task will transfer missing files, and the data will be complete and consistent at the end of this run. Each time a task is started it performs an incremental copy, transferring only the changes from the source to the destination.

**Q: Can I use AWS DataSync with AWS Direct Connect?  
**

A: You can use AWS DataSync with your Direct Connect link to access public service endpoints or [private VPC endpoints](https://docs.aws.amazon.com/datasync/latest/userguide/datasync-in-vpc.html). When using VPC endpoints, data transferred between the DataSync agent and AWS services does not traverse the public internet or need public IP addresses, increasing the security of data as it is copied over the network. DataSync Discovery is currently only supported with public service endpoints.  

**Q: Does AWS DataSync support VPC endpoints or AWS PrivateLink?**

A: Yes, VPC endpoints are supported for data movement use cases. You can [use VPC endpoints](https://docs.aws.amazon.com/datasync/latest/userguide/datasync-in-vpc.html) to ensure data transferred between your AWS DataSync agent, either deployed on-premises or in-cloud, doesn't traverse the public internet or need public IP addresses. Using VPC endpoints increases the security of your data by keeping network traffic within your [Amazon Virtual Private Cloud (Amazon VPC)](https://aws.amazon.com/vpc/). VPC endpoints for DataSync are powered by [AWS PrivateLink](https://aws.amazon.com/privatelink/), a highly available, scalable technology that enables you to privately connect your VPC to supported AWS services.

**Q: How do I configure AWS DataSync to use VPC endpoints?**

A: To use VPC endpoints with AWS DataSync, you create an [AWS PrivateLink](https://aws.amazon.com/privatelink/) interface VPC endpoint for the DataSync service in your chosen VPC, and then choose this endpoint elastic network interface (ENI) when creating your DataSync agent. Your agent will connect to this ENI to activate, and subsequently all data transferred by the agent will remain within your configured VPC. You can use either the [AWS DataSync Console](https://console.aws.amazon.com/datasync/home), AWS Command Line Interface (CLI), or AWS SDK, to configure VPC endpoints. To learn more, see [Using AWS DataSync in a Virtual Private Cloud](https://docs.aws.amazon.com/datasync/latest/userguide/datasync-in-vpc.html).  

## Moving to and from AWS Storage

**Q: Can I copy my data into Amazon S3 Glacier Instant Retrieval, Amazon S3 Glacier Flexible Retrieval (formerly S3 Glacier), Amazon S3 Glacier Deep Archive, or other S3 storage classes?**

A: Yes. When configuring an S3 bucket for use with AWS DataSync, you can select the S3 storage class that DataSync uses to store objects. DataSync supports storing data directly into S3 Standard, S3 Intelligent-Tiering, S3 Standard-Infrequent Access (S3 Standard-IA), S3 One Zone-Infrequent Access (S3 One Zone-IA), Amazon S3 Glacier Instant Retrieval, Amazon S3 Glacier Flexible Retrieval, and Amazon S3 Glacier Deep Archive (S3 Glacier Deep Archive). More information on [Amazon S3 storage classes](https://aws.amazon.com/s3/storage-classes/) can be found in the [Amazon Simple Storage Service Developer Guide](https://docs.aws.amazon.com/AmazonS3/latest/dev/Welcome.html).

Objects smaller than the minimum charge capacity per object will be stored in S3 Standard. For example, folder objects, which are zero-bytes in size and hold only metadata, will be stored in S3 Standard. Read about [considerations when working with Amazon S3 storage classes](https://docs.aws.amazon.com/datasync/latest/userguide/create-s3-location.html#using-storage-classes) in our documentation and [evaluating S3 request costs when using DataSync](https://docs.aws.amazon.com/datasync/latest/userguide/create-s3-location.html#create-s3-location-s3-requests). For more information on minimum charge capacities see [Amazon S3 Pricing](https://aws.amazon.com/s3/pricing/).

**Q: Can I copy data out of S3 Standard-IA and S3 One Zone-IA storage classes?**A: Yes. When using S3 as the source location for an AWS DataSync task, the service will retrieve all objects from the bucket which need to be copied to the destination. Retrieving objects from S3 Standard-IA and S3 One Zone-IA storage will incur a retrieval fee based on the size of the objects. Read about [considerations when working with Amazon S3 storage classes](https://docs.aws.amazon.com/datasync/latest/userguide/create-s3-location.html#using-storage-classes) in our documentation.

**Q: Can I copy data out of Amazon S3 Glacier Instant Retrieval. Amazon S3 Glacier Flexible Retrieval (formerly S3 Glacier) and Amazon S3 Glacier Deep Archive?**A: When using S3 as the source location for an AWS DataSync task, the service will attempt to retrieve all objects from the bucket which need to be copied to the destination. Retrieving objects which are archived in the S3 Glacier Instant Retrieval storage class will incur higher retrieval fees based on the size of the objects. Retrieving objects which are archived in the S3 Glacier Flexible Retrieval or S3 Glacier Deep Archive storage class results in an error. Any errors retrieving archived objects will be logged by DataSync and will result in a failed task completion status. Read about [considerations when working with Amazon S3 storage classes](https://docs.aws.amazon.com/datasync/latest/userguide/create-s3-location.html#using-storage-classes) and [evaluating S3 request costs when using DataSync](https://docs.aws.amazon.com/datasync/latest/userguide/create-s3-location.html#create-s3-location-s3-requests) in our documentation.

**Q: How does AWS DataSync access my Amazon S3 bucket?**A: AWS DataSync assumes an IAM role that you provide. The policy you attach to the role determines which actions the role can perform. DataSync can auto generate this role on your behalf or you can [manually configure a role](https://docs.aws.amazon.com/datasync/latest/userguide/create-s3-location.html#create-role-manually "AWS Documentation").

**Q: How does AWS DataSync convert files and folders to or from objects in Amazon S3?**A: When files or folders are copied to Amazon S3, there is a one-to-one relationship between a file or folder and an object. File and folder timestamps and POSIX permissions, including user ID, group ID, and permissions, are stored in [S3 user metadata](https://docs.aws.amazon.com/datasync/latest/userguide/working-with-locations.html#special-files). For NFS shares, file metadata stored in S3 user metadata is fully interoperable with [File Gateway](https://aws.amazon.com/storagegateway/file/), providing on-premises file-based access to data stored in Amazon S3 by AWS DataSync.

When DataSync copies objects that contain this user metadata back to an NFS server, the file metadata is restored. Symbolic links and hard links are also restored when copying back from NFS to S3.

When copying from an SMB file share, default POSIX permissions are stored in S3 user metadata. When copying back to an SMB file share, ownership is set based on the user that was configured in DataSync to access that file share, and default permissions are assigned.

When copying from HDFS, file and folder timestamps, user and group ownership, and POSIX permissions are stored in S3 user metadata. When copying from Amazon S3 back to HDFS, file and folder metadata are restored.  

Learn more about how [DataSync stores files and metadata](https://docs.aws.amazon.com/datasync/latest/userguide/special-files.html) in our documentation.

**Q: What object metadata is preserved when transferring objects between self-managed object storage or Azure Blob Storage and Amazon S3?**

A: When transferring objects between self-managed object storage or Azure Blob Storage and Amazon S3, DataSync copies objects together with object metadata and tags.

**Q: What object metadata is preserved when transferring objects between Amazon S3 buckets?**

A: When transferring objects between Amazon S3 buckets, DataSync copies objects together with object metadata and tags. DataSync does not copy other object information such as object ACLs or prior object versions.  

**Q: Which Amazon S3 request and storage costs apply when using S3 storage classes with AWS DataSync?**A: Some S3 storage classes have behaviors that can affect your cost, such as data retrieval, minimum storage capacities, and minimum storage durations. DataSync automates management of data to address these factors, and provides settings to minimize data retrieval.

To avoid minimum capacity charge per object, AWS DataSync automatically stores small objects in S3 Standard. To minimize data retrieval fees, you can configure DataSync to verify only files that were transferred by a given task. To avoid minimum storage duration charges, DataSync has controls for overwriting and deleting objects. Read about [cost considerations when working with Amazon S3 storage classes](https://docs.aws.amazon.com/datasync/latest/userguide/create-s3-location.html#create-s3-location-considerations) in our documentation and [evaluating S3 request costs when using DataSync.](https://docs.aws.amazon.com/datasync/latest/userguide/create-s3-location.html#create-s3-location-s3-requests)  

**Q: Can I copy object data to and from Amazon S3 buckets on AWS Outposts?**A: Yes. You can copy objects between Amazon S3 on AWS Outposts and Amazon S3 buckets in AWS Regions. AWS DataSync copies objects together with object metadata and object tags. For DataSync to access your Amazon S3 on Outposts buckets, [deploy a DataSync EC2 agent on your Outpost](https://docs.aws.amazon.com/datasync/latest/userguide/deploy-agents.html#outposts-agent).

When using DataSync with Amazon S3 on Outposts, you can only transfer data to and from Amazon S3 buckets in AWS Regions. You can learn more about supported sources and destinations for DataSync tasks in our [documentation](https://docs.aws.amazon.com/datasync/latest/userguide/working-with-locations.html).  

## Amazon EFS

**Q:  How does AWS DataSync access my Amazon EFS file system?**

A: AWS DataSync accesses your Amazon EFS file system using the NFS protocol. The DataSync service mounts your file system from within your VPC from Elastic Network Interfaces (ENIs) managed by the DataSync service. DataSync fully manages the creation, use, and deletion of these ENIs on your behalf. You can choose to mount your EFS file system using a mount target or an [EFS Access Point](https://docs.aws.amazon.com/efs/latest/ug/efs-access-points.html).  

**Q:  Can I use AWS DataSync with all Amazon EFS storage classes?**

A: Yes. You can use AWS DataSync to copy files into Amazon EFS and configure [EFS Lifecycle Management](https://docs.aws.amazon.com/efs/latest/ug/lifecycle-management-efs.html) to migrate files that have not been accessed for a set period of time to the Infrequent Access (IA) storage class.  

**Q:  How do I use AWS DataSync with Amazon EFS file system resource policies?**

A: You can use both IAM identity policies and resource policies to control client access to Amazon EFS resources in a way that is scalable and optimized for cloud environments. When you create a DataSync location for your EFS file system, you can specify an IAM role that DataSync will assume when accessing EFS. You can then use [EFS file system policies](https://docs.aws.amazon.com/efs/latest/ug/iam-access-control-nfs-efs.html) to configure access for the IAM role. Because DataSync mounts EFS file systems as the root user, your IAM policy must allow the following action: elasticfilesystem:ClientRootAccess.  

**Q: Can I use AWS DataSync to replicate my Amazon EFS file system to a different AWS Region?**

A: Yes. In addition to the built-in [replication](https://docs.aws.amazon.com/efs/latest/ug/efs-replication.html) provided by Amazon EFS, you can also use AWS DataSync to schedule periodic replication of your Amazon EFS file system to a second Amazon EFS file system within the same AWS account. This capability is available for both same-region and cross-region deployments, and does not require using a DataSync agent.  

**Q: What metadata is preserved when copying data between an NFS share and Amazon EFS, or between two Amazon EFS file systems?**

A: AWS DataSync copies file and folder timestamps and POSIX permissions, including user ID, group ID, and permissions. You can learn more and see the complete list of copied metadata in our [documentation](https://docs.aws.amazon.com/datasync/latest/userguide/special-files.html).

**Q: What metadata is preserved when copying data between HDFS and Amazon EFS?**

A: AWS DataSync copies file and folder timestamps and POSIX permissions and applies default values for user ID and group ID. You can learn more and see the complete list of copied metadata in our [documentation](https://docs.aws.amazon.com/datasync/latest/userguide/special-files.html "DataSync documentation").

## Amazon FSx for Windows File Server

**Q: How does AWS DataSync access my Amazon FSx for Windows File Server file system?**

A: AWS DataSync accesses your [Amazon FSx for Windows File Server](https://aws.amazon.com/fsx/windows/) file system using the SMB protocol, authenticating with the username and password you configure in the AWS Console or CLI. The DataSync service mounts your file system from within your VPC from Elastic Network Interfaces (ENIs) managed by the DataSync service. DataSync fully manages the creation, use, and deletion of these ENIs on your behalf.

**Q: What Windows metadata is transferred when copying between an SMB share to Amazon FSx for Windows File Server file system, or between two Amazon FSx file systems?**A: AWS DataSync copies Windows metadata, including file timestamps, file owner, standard file attributes, NTFS discretionary access lists (DACLs), and NTFS system access control lists (SACLs). You can learn more and see the complete list of copied metadata in our [documentation](https://docs.aws.amazon.com/datasync/latest/userguide/special-files.html).

**Q: Can I use AWS DataSync to replicate my Amazon FSx for Windows File Server file system to a different AWS Region?**

A: Yes. You can use AWS DataSync to schedule periodic replication of your Amazon FSx for Windows File Server file system to a second file system within the same AWS account. This capability is available for both same-region and cross-region deployments, and does not require using a DataSync agent.  

## Amazon FSx for Lustre

**Q: How does AWS DataSync access my Amazon FSx for Lustre file system?**  

A: When you create a DataSync task to copy to or from your FSx for Lustre file system, the DataSync service will create Elastic Network Interfaces (ENIs) in the same VPC and subnet where your file system is located.  DataSync uses these ENIs to access your FSx for Lustre file system using the Lustre protocol as the root user.  When you create a DataSync location resource for your FSx for Lustre file system, you can specify up to five security groups to apply to the ENIs and configure outbound access from the DataSync service.  The security groups must be configured to allow outbound traffic on the [network ports required by FSx for Lustre](https://docs.aws.amazon.com/fsx/latest/LustreGuide/limit-access-security-groups.html "AWS Documentation").  The security groups on your FSx for Lustre file system should be configured to allow inbound access from the security groups you assigned to the DataSync location resource for your FSx for Lustre file system.  

**Q: What metadata is preserved when either copying data between an NFS share or Amazon EFS file system and Amazon FSx for Lustre, or between two Amazon FSx for Lustre file systems?**A: AWS DataSync copies file and folder timestamps and POSIX permissions, including user ID, group ID, and permissions. You can learn more and see the complete list of copied metadata in our [documentation](https://docs.aws.amazon.com/datasync/latest/userguide/special-files.html "AWS Documentation").  

**Q: Can I use AWS DataSync to migrate data from one FSx for Lustre file system to another?**

A: Yes. You can use AWS DataSync to copy from your FSx for Lustre file system to a second file system within the same AWS account. This capability is available for both same-region and cross-region deployments, and does not require using a DataSync agent.  

**Q: Can I use AWS DataSync to replicate my Amazon FSx for Lustre file system to a different AWS Region?**

A: Yes. You can use AWS DataSync to schedule periodic replication of your Amazon FSx for Lustre file system to a second file system within the same AWS account. This capability is available for both same-region and cross-region deployments, and does not require using a DataSync agent.  

**Q: Will DataSync copy the striping or layout settings when copying from one Amazon FSx for Lustre file system to another?**

A: No. Files are written using the file layout and striping configuration on the destination’s file system.  

## Amazon FSx for OpenZFS

**Q: How does AWS DataSync access my Amazon FSx for OpenZFS file system?**

A: When you create a DataSync task to copy to or from your FSx for OpenZFS file system, the DataSync service will create Elastic Network Interfaces (ENIs) in the same VPC and subnet where your file system is located.  DataSync uses these ENIs to access your FSx for OpenZFS file system using the OpenZFS protocol as the root user.  When you create a DataSync location resource for your FSx for OpenZFS file system, you can specify up to five security groups to apply to the ENIs and configure outbound access from the DataSync service.  The security groups must be configured to allow outbound traffic on the [network ports required by FSx for OpenZFS](https://docs.aws.amazon.com/datasync/latest/userguide/what-is-datasync.html "AWS Documentation"). The security groups on your FSx for OpenZFS file system should be configured to allow inbound access from the security groups you assigned to the DataSync location resource for your FSx for OpenZFS file system.  

**Q: What metadata is preserved when either copying data between an NFS share or Amazon EFS file system and Amazon FSx for OpenZFS, or between two Amazon FSx for OpenZFS file systems?**A: AWS DataSync copies file and folder timestamps and POSIX permissions, including user ID, group ID, and permissions. You can learn more and see the complete list of copied metadata in our [documentation](https://docs.aws.amazon.com/datasync/latest/userguide/special-files.html "AWS Documentation").  

**Q: Can I use AWS DataSync to migrate data from one FSx for OpenZFS file system to another?**

A: Yes. You can use AWS DataSync to copy from your FSx for OpenZFS file system to a second file system within the same AWS account. This capability is available for both same-region and cross-region deployments, and does not require using a DataSync agent.  

**Q: Can I use AWS DataSync to replicate my Amazon FSx for OpenZFS file system to a different AWS Region?**

A: Yes. You can use AWS DataSync to schedule periodic replication of your Amazon FSx for OpenZFS file system to a second file system within the same AWS account. This capability is available for both same-region and cross-region deployments, and does not require using a DataSync agent.  

## Amazon FSx for NetApp ONTAP

**Q:  How does AWS DataSync access my Amazon FSx for Netapp ONTAP file system?**

A: When you create a task, DataSync creates Elastic Network Interfaces (ENIs) in the Preferred Subnet of the same VPC where your [Amazon FSx for NetApp ONTAP](https://aws.amazon.com/fsx/netapp-ontap/) file system is located. The Preferred Subnet is configured when you create your FSx for ONTAP file system, and DataSync uses the ENIs it creates in that subnet to access your FSx for ONTAP file system. When you create a DataSync Location resource for your FSx for ONTAP file system, you can specify up to 5 security groups to apply to the ENIs to configure outbound access from the DataSync service. You should configure the security groups on your FSx for ONTAP file system to allow inbound access from the security groups you assigned to the DataSync Location resource for your FSx for ONTAP file system .

**Q:  Which protocol versions can AWS DataSync use with Amazon FSx for NetApp ONTAP?**

A: AWS DataSync supports using NFSv3, SMB 2.1, and SMB 3. DataSync does not currently support using NFSv4 or above with FSx for ONTAP.

**Q:  Does AWS DataSync preserve file system metadata when copying data to or from my Amazon FSx for NetApp ONTAP file system?**

A: Yes, AWS DataSync copies file and folder timestamps and POSIX permissions, including user ID, group ID, and permissions, when using the NFS protocol. When using the SMB protocol, DataSync copies file and folder timestamps, ownership, and ACLs. You can learn more and see the complete list of copied metadata in our [documentation](https://docs.aws.amazon.com/datasync/latest/userguide/special-files.html).

**Q:  Which protocol should I use when migrating my data to Amazon FSx for NetApp ONTAP?**

A: When migrating from Windows servers or NAS shares that serve users through the SMB protocol, use a DataSync SMB source location and the SMB protocol for your FSx for ONTAP location, ensuring that the security style for your FSx for ONTAP volume is configured for NTFS. When migrating from Unix or Linux servers or NAS shares that serve users through the NFS protocol, use a DataSync NFS source location and the NFS protocol for your FSx for ONTAP location, ensuring the security style for your FSx for ONTAP volume is configured for Unix. For multi-protocol migrations, you should review the best practices covered in the blog [Enabling multiprotocol workloads with Amazon FSx for NetApp ONTAP](https://aws.amazon.com/blogs/storage/enabling-multiprotocol-workloads-with-amazon-fsx-for-netapp-ontap/), and use the SMB protocol to preserve file system metadata with the highest fidelity. For more information on configuring security styles for your FSx for ONTAP volumes, see the documentation on [managing FSx for ONTAP volumes](https://docs.aws.amazon.com/fsx/latest/ONTAPGuide/managing-volumes.html).

**Q:  Can I use AWS DataSync to access the same Amazon FSx for NetApp ONTAP file system using different protocols?**

A: Yes, however you will need to create a separate DataSync location and task resource for each protocol (NFS or SMB). To avoid issues with overwriting data and data verification, we do not recommend using multiple DataSync tasks to copy to the same volume path at the same time (whether using the same protocol or different protocols).

**Q:  Can I use AWS DataSync to transfer data to or from Amazon FSx for NetApp ONTAP iSCSI LUNs?**

A: No, DataSync only supports copying file data to or from FSx for ONTAP volumes using NFS or SMB protocols.

**Q:  Can I use AWS DataSync to copy data from one Amazon FSx for NetApp ONTAP file system to another?**

A: Yes. You can use AWS DataSync to copy from your FSx for ONTAP file system to a second file system within the same AWS account. This capability is available for both same-Region and cross-Region deployments, and does not require using a DataSync agent.

**Q:  Can I use AWS DataSync to replicate my Amazon FSx for NetApp ONTAP file system to a different file system in another AWS Region?**

A: While DataSync can be used to replicate data between your file systems, we recommend using [NetApp SnapMirror](https://docs.aws.amazon.com/fsx/latest/ONTAPGuide/scheduled-replication.html) to replicate between your FSx for ONTAP file systems. SnapMirror enables you to achieve low RPOs, regardless of the number or size of files in your file system.

**Q:  How do I configure AWS DataSync to not copy snapshot directories?**

A: DataSync will automatically exclude folders named “.snapshot”. You can also use [exclude filters](https://docs.aws.amazon.com/datasync/latest/userguide/filtering.html#exclude-filters) to avoid copying files and folders that match patterns you specify.

## Moving to and from AWS Snow Family Devices

**Q:  How do I move data between AWS Snowcone and AWS storage services?**

A: The DataSync agent is pre-installed on your [Snowcone](https://aws.amazon.com/snowcone/) device as an AMI. To move data online to AWS, connect the AWS Snowcone device to the external network and use [AWS OpsHub](https://docs.aws.amazon.com/snowball/latest/snowcone-guide/aws-opshub.html) or the CLI to launch the DataSync agent AMI. Activate the agent using the AWS Management Console or CLI, and set up your online data move task between AWS Snowcone’s NFS store, and Amazon S3, Amazon EFS, Amazon FSx for Windows File Server, Amazon FSx for Lustre, Amazon FSx for OpenZFS, or Amazon FSx for NetApp ONTAP.

**Q:  How do I move data between Amazon S3 compatible storage on Snow and AWS  
storage services?**

A: Start by deploying a DataSync agent in your on-premises environment. Activate the agent using the AWS Management Console or CLI, and set up your DataSync task to move data between a bucket on your Amazon S3 compatible storage, and Amazon S3, Amazon EFS, or any Amazon FSx file system.  

## Performance

**Q:  How fast can AWS DataSync copy my file system to AWS?**

A: The rate at which AWS DataSync can copy a given dataset is a function of amount of data, I/O bandwidth achievable from the source and destination storage, network bandwidth available, and network conditions. For data transfer between on premises and AWS Storage services, a single DataSync task is capable of fully utilizing a 10 Gbps network link.  

**Q:  Can I control the amount of network bandwidth that an AWS DataSync task uses?**

A: Yes. You can control the amount of network bandwidth that AWS DataSync will use by [configuring the built-in bandwidth throttle](https://docs.aws.amazon.com/datasync/latest/userguide/create-task.html). You can increase or decrease this limit while your data transfer task is running. This enables you to minimize impact on other users or applications who rely on the same network connection.  

**Q:  Will AWS DataSync affect the performance of my source file system?**

A: Depending on the capacity of your on-premises file store, and the quantity and size of files to be transferred, AWS DataSync may affect the response time of other clients when accessing the same source data store, because the agent reads or writes data from that storage system. [Configuring a bandwidth limit](https://docs.aws.amazon.com/datasync/latest/userguide/create-task.html) for a task will reduce this impact by limiting the I/O against your storage system.

## Security and compliance

**Q: How does AWS DataSync Discovery access my on-premises storage?**

AWS DataSync Discovery uses the DataSync agent to access the management/API interfaces of your storage systems. All access is read-only. See the [DataSync documentation](https://docs.aws.amazon.com/datasync/latest/userguide/what-is-datasync.html) for more information on the APIs used to access your storage.

**Q: When using AWS DataSync Discovery, how do I specify the credentials for my on-premises storage systems and how are they protected?**

When you configure AWS DataSync Discovery to discover your storage system, you provide a username and password for accessing the API interface of your storage. AWS DataSync Discovery will then automatically create a secret in AWS Secrets Manager to store the credentials. When DataSync Discovery runs a discovery job, it retrieves the password from the secret, re-encrypts it, and sends the encrypted password to the agent used for your job. The password is retained in memory on the agent only for the duration of the job and at no time is the password persisted outside of memory.

**Q: How does AWS DataSync access my NFS server or SMB file share?**

A: AWS DataSync uses an agent that you deploy into your IT environment or into Amazon EC2 to access your files through the NFS or SMB protocol. This agent connects to DataSync service endpoints within AWS, and is securely managed from the AWS Management Console or CLI.

**Q: How does AWS DataSync access HDFS on my Hadoop cluster?**

A: AWS DataSync uses an agent that you deploy into your IT environment or into Amazon EC2 to access your Hadoop cluster. The DataSync agent acts as an HDFS client and communicates with the NameNodes and DataNodes in your clusters. When you start a task, DataSync queries the primary NameNode to determine the locations of files and folders on the cluster. DataSync then communicates with the DataNodes in the cluster to copy files and folders to, or from, HDFS.

**Q: How does AWS DataSync access my self-managed or cloud object storage that supports the Amazon S3 protocol?**

A: AWS DataSync uses an agent that you deploy into your data center or public cloud environment, or into Amazon EC2 to access your objects using the Amazon S3 API. This agent connects to DataSync service endpoints within AWS, and is securely managed from the AWS Management Console or CLI.

**Q: How does AWS DataSync access my Azure Blob Storage containers?**

A: AWS DataSync uses an agent that you deploy into your Azure environment or into Amazon EC2 to access objects in your Azure Blob Storage containers. The agent connects to DataSync service endpoints within AWS, and is securely managed from the AWS Management Console or CLI. The agent authenticates to your Azure container using a SAS token that you specify when creating a DataSync Azure Blob location.

**Q:  Does AWS DataSync require setting up a VPN to connect to my destination storage?**

A: No. When copying data to or from your premises, there is no need to setup a VPN/tunnel or allow inbound connections. Your AWS DataSync agent can be configured to route through a firewall using standard network ports. You can also [deploy DataSync within your Amazon Virtual Private Cloud (Amazon VPC)](https://docs.aws.amazon.com/datasync/latest/userguide/datasync-in-vpc.html) using VPC endpoints. When using VPC endpoints, data transferred between the DataSync agent and AWS services does not need to traverse the public internet or need public IP addresses.

**Q: How do my AWS DataSync agents securely connect to AWS?**

A: Your AWS DataSync agent connects to DataSync service endpoints within your chosen [AWS Region](https://aws.amazon.com/about-aws/global-infrastructure/regional-product-services/). You can choose to have the agent connect to public internet facing endpoints, Federal Information Processing Standards (FIPS) validated endpoints, or endpoints within one of your VPCs. Activating your agent securely associates it with your AWS account. To learn more, see [Choose a Service Endpoint](https://docs.aws.amazon.com/datasync/latest/userguide/choose-service-endpoint.html) and [Activate Your Agent](https://docs.aws.amazon.com/datasync/latest/userguide/activate-agent.html).  

**Q:  How is my AWS DataSync agent patched and updated?**

A: Updates to the agent VM, including both the underlying operating system and the AWS DataSync software packages, are automatically applied by AWS once the agent is activated. Updates are applied non-disruptively when the agent is idle and not executing a data transfer task.

**Q:  Which compliance programs does AWS DataSync support?**

A: AWS has the longest-running compliance program in the cloud. AWS is committed to helping customers navigate their requirements. AWS DataSync has been assessed to meet global and industry security standards. DataSync complies with [PCI DSS](https://aws.amazon.com/compliance/pci-dss-level-1-faqs/), ISO [9001](https://aws.amazon.com/compliance/iso-9001-faqs/), [27001](https://aws.amazon.com/compliance/iso-27001-faqs/), [27017](https://aws.amazon.com/compliance/iso-27017-faqs/), and [27018](https://aws.amazon.com/compliance/iso-27018-faqs/); [SOC 1, 2, and 3](https://aws.amazon.com/compliance/soc-faqs/); in addition to being [HIPAA eligible](https://aws.amazon.com/compliance/hipaa-compliance/). DataSync is also authorized in the AWS US East/West Regions under FedRAMP Moderate and in the AWS GovCloud (US) Regions under FedRamp High. That makes it easier for you to verify our security and meet your own obligations. For more information and resources, visit our [compliance pages](https://aws.amazon.com/compliance/). You can also go to the [Services in Scope by Compliance Program page](https://aws.amazon.com/compliance/services-in-scope/) to see a full list of services and certifications.

**Q:  Is AWS DataSync PCI compliant?**

A: Yes. AWS DataSync is [PCI-DSS](https://aws.amazon.com/compliance/pci-dss-level-1-faqs/) compliant, which means you can use it to transfer payment information. You can download the PCI Compliance Package in [AWS Artifact](https://aws.amazon.com/artifact/) to learn more about how to achieve PCI Compliance on AWS.

**Q:  Is AWS DataSync HIPAA eligible?**

A: Yes. AWS DataSync is HIPAA eligible, which means if you have a [HIPAA BAA in place with AWS](https://aws.amazon.com/compliance/hipaa-compliance/), you can use DataSync to transfer protected health information (PHI).

**Q:  Does AWS DataSync have FedRAMP JAB Moderate Provisional Authorization in the AWS US East/West?**

A: Yes. AWS DataSync has received a Provisional Authority to Operate (P-ATO) from the Joint Authorization Board (JAB) at the Federal Risk and Authorization Management Program (FedRAMP) Moderate baseline in the US East/West Regions. If you are a federal or commercial customer, you can use AWS DataSync in the AWS East/West Region's authorization boundary with data up to the moderate impact level.

**Q:  Does AWS DataSync have FedRAMP JAB High Provisional Authorization in the AWS GovCloud (US) Regions?**

A: Yes. AWS DataSync has received a Provisional Authority to Operate (P-ATO) from the Joint Authorization Board (JAB) at the Federal Risk and Authorization Management Program (FedRAMP) High baseline in the US GovCloud Region. If you are a federal or commercial customer, you can use AWS DataSync in the AWS GovCloud (US) Region’s authorization boundary with data up to the high impact level.

## When to Choose AWS DataSync

**Q:  How is AWS DataSync different from using command line tools such as rsync or the Amazon S3 command line interface?**

A: AWS DataSync fully automates and accelerates moving large active datasets to AWS. It is natively integrated with Amazon S3, Amazon EFS, Amazon FSx, [Amazon CloudWatch](https://aws.amazon.com/cloudwatch/), and [AWS CloudTrail](https://aws.amazon.com/cloudtrail/), which provides seamless and secure access to your storage services, as well as detailed monitoring of the transfer.

DataSync uses a purpose-built network protocol and scale-out architecture to transfer data. For data transfer between on premises and AWS Storage services, a single DataSync task is capable of fully utilizing a 10 Gbps network link.

DataSync fully automates the data transfer. It comes with retry and network resiliency mechanisms, network optimizations, built-in task scheduling, auditing via task reports, monitoring via the DataSync API and Console, and CloudWatch metrics, events and logs that provide granular visibility into the transfer process. DataSync performs data integrity verification both during the transfer and at the end of the transfer.

DataSync provides end-to-end security, and integrates directly with AWS storage services. All data transferred between the source and destination is encrypted via TLS, and access to your AWS storage is enabled via built-in AWS security mechanisms such as IAM roles. DataSync with VPC endpoints are enabled to ensure that data transferred between an organization and AWS does not traverse the public internet, further increasing the security of data as it is copied over the network.

**Q: To transfer objects between my buckets, when do I use AWS DataSync, when do I use S3 Replication, and when do I use S3 Batch Operations?**

A: AWS provides multiple tools to copy objects between your buckets.

Use AWS DataSync for ongoing data distribution, data pipelines, and data lake ingest, as well as for consolidating or splitting data between multiple buckets.

Use [S3 Replication](https://docs.aws.amazon.com/AmazonS3/latest/dev/replication.html) for continuous replication of data to a specific destination bucket.

Use [S3 Batch Operations](https://docs.aws.amazon.com/AmazonS3/latest/user-guide/batch-ops.html) for large-scale batch operations on S3 objects, such as to copy objects, set object tags or access control lists (ACLs), initiate object restores from Amazon S3 Glacier Flexible Retrieval (formerly S3 Glacier), invoke an AWS Lambda function to perform custom actions using your objects, manage S3 Object Lock legal hold, or manage S3 Object Lock retention dates.

**Q:  When do I use AWS DataSync and when do I use AWS Snowball Edge?**

A: AWS DataSync is ideal for online data transfers. You can use DataSync to migrate active data to AWS, transfer data to the cloud for analysis and processing, archive data to free up on-premises storage capacity, or replicate data to AWS for business continuity.

[AWS Snowball Edge](https://aws.amazon.com/snowball-edge/) is ideal for offline data transfers, for customers who are bandwidth constrained, or transferring data from remote, disconnected, or austere environments. 

**Q:  When do I use AWS DataSync and when do I use AWS Storage Gateway?**

A: Use AWS DataSync to migrate existing data to Amazon S3, and subsequently use the File Gateway configuration of [AWS Storage Gateway](https://aws.amazon.com/storagegateway/) to retain access to the migrated data and for ongoing updates from your on-premises file-based applications.

You can use a combination of DataSync and File Gateway to minimize your on-premises infrastructure while seamlessly connecting on-premises applications to your cloud storage. AWS DataSync enables you to automate and accelerate online data transfers to AWS Storage services. After the initial data transfer phase using AWS DataSync, File Gateway provides your on-premises applications with low latency access to the migrated data. When using DataSync with NFS shares, POSIX metadata from your source on-premises storage is preserved, and permissions from the source storage apply when accessing your files using File Gateway.

**Q: When do I use AWS DataSync, and when do I use Amazon S3 Transfer Acceleration?**

A: If your applications are already integrated with the Amazon S3 API, and you want higher throughput for transferring large files to S3, you can use [S3 Transfer Acceleration](https://aws.amazon.com/s3/transfer-acceleration/). If you want to transfer data from existing storage systems (e.g., Network Attached Storage), or from instruments that cannot be changed (e.g., DNA sequencers, video cameras), or if you want multiple destinations, you use AWS DataSync. DataSync also automates and simplifies the data transfer by providing additional functionality, such as built-in retry and network resiliency mechanisms, data integrity verification, and flexible configuration to suit your specific needs, including bandwidth throttling, etc.

**Q: When do I use AWS DataSync and when do I use AWS Transfer Family?**

A: If you currently use SFTP to exchange data with third parties, [AWS Transfer Family](https://aws.amazon.com/aws-transfer-family/) provides a fully managed SFTP, FTPS, FTP, and AS2 transfer directly into and out of Amazon S3, while reducing your operational burden.

If you want an accelerated and automated data transfer between NFS servers, SMB file shares, Hadoop clusters, self-managed or cloud object storage, AWS Snowcone, Amazon S3, Amazon EFS, and Amazon FSx, you can use AWS DataSync. DataSync is ideal for customers who need online migrations for active data sets, timely transfers for continuously generated data, or replication for business continuity. 
