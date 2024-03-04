---
tags:
  - cloud/aws
---
**AWS Backup** provides centralized and automated data protection.  
![](https://i.imgur.com/GJx5DSt.png)  
![](https://i.imgur.com/2rd3wbL.png)  
![](https://i.imgur.com/MlhPLU5.png)  
![](https://i.imgur.com/eoYzDIj.png)

Works across AWS services and hybrid workloads.

Helps to support regulatory compliance and business policies for data protection.

- Let’s understand some AWS Backup terminology:
	- **Backup vault** – A container that you organize your backups in.
	- **Backup plan** – A policy expression that defines when and how you want to back up your AWS resources. The backup plan is attached to a backup vault.
	- **Resource assignment** – This defines which resources should be backed up. You can select resources by tags or by resource ARN.
	- **Recovery point** – A snapshot or backup of a resource backed up by AWS Backup. Each recovery point can be restored with AWS Backup.

- Integrates with AWS Organizations for central deployment of data protection policies.

Configure, manage, and govern backup activities across AWS accounts and resources.

---
AWS Backup can protect many AWS resources including:
- Amazon EC2 instances.
- Amazon EBS volumes.
- Amazon RDS databases.
- Amazon DynamoDB tables.
- Amazon Neptune databases.
- Amazon DocumentDB databases.
- Amazon EFS file systems.
- Amazon FSx for Lustre and Windows File Server file systems.
- AWS Storage Gateway volumes.
- VMware workloads on-premises and in VMware Cloud on AWS.
- Amazon S3 buckets.
---

AWS Backup can be used to copy backups across multiple AWS services to different Regions.

Cross-Region backup copies can be deployed manually or automatically using scheduling.

Cross-account backup can also be configured for accounts within an AWS Organization.

## Policy-based Backup

With AWS Backup, you can create backup policies called **backup plans**.

<mark style="background: #ADCCFFA6;">Backup plans are used to define backup requirements.</mark>

Backup plans are then applied to the AWS resources you want to back up.

You can create separate backup plans that meet specific business and regulatory compliance requirements.

Backup plans make it easy to implement your backup strategy across your organization and across your applications.

## Tag-based Backup Policies

<mark style="background: #BBFABBA6;">AWS Backup allows you to apply backup plans to your AWS resources by simply tagging them.</mark>

Ensure that all your AWS resources are backed up and protected according to your strategy.

AWS tags are a great way to organize and classify your AWS resources.

Integration with AWS tags enables you to quickly apply a backup plan to a group of AWS resources so that they are backed up in a consistent and compliant manner.

## Automated Backup Scheduling

AWS Backup allows you to create backup schedules that you can customize to meet your business and regulatory backup requirements.

You can also choose from predefined backup schedules based on common best practices.

AWS Backup will automatically back up your AWS resources according to the policies and schedules you define.

A backup schedule includes the backup start time, backup frequency, and backup window.

## Automated Retention Management

You can configure backup retention policies that automatically retain and expire backups according to business and regulatory compliance requirements.

Automated backup retention management minimizes backup storage costs by retaining backups only if they are needed.

## AWS Backup Vault Lock

AWS Backup Vault Lock allows you to protect your backups from deletion or changes to their lifecycle by inadvertent or malicious changes.

You can use the AWS CLI, AWS Backup API, or AWS Backup SDK to apply the AWS Backup Vault Lock protection to an existing vault or a new one.

![[AWS Solutions Architect Skillbuilder#AWS Backup]]



---
[Tutorial](https://aws.amazon.com/getting-started/hands-on/amazon-ec2-backup-and-restore-using-aws-backup/)

# FAQ
## General

Close all

### What is AWS Backup?

AWS Backup is<mark style="background: #ADCCFFA6;"> a fully managed service that centralizes and automates data protection across AWS services</mark> like Amazon Simple Storage Service (S3), Amazon FSx, Amazon Elastic Compute Cloud (EC2), and Amazon Relational Database Service (RDS), and hybrid workloads like VMware on premises, VMware Cloud on AWS, and VMware Cloud on AWS Outposts.  
AWS Backup offers a cost-effective, fully managed, policy-based service that further simplifies data protection at scale. Using the AWS Backup Audit Manager, you can audit and report on the compliance of your data protection policies to help meet your business and regulatory needs. Together with AWS Organizations, use AWS Backup to centrally deploy data protection policies to configure, manage, and govern your backup activities across your AWS accounts and resources.

### How Does AWS Backup Work?

<mark style="background: #BBFABBA6;">With AWS Backup, you can define a central data protection policy</mark> called a **backup plan** that works across AWS services for compute, storage, and databases.  
<mark style="background: #ADCCFFA6;">The backup plan defines parameters such as backup frequency and backup retention period</mark>.  
<mark style="background: #FFB86CA6;">Once you define your data protection policies and assign AWS resources to the policies</mark>, AWS Backup automates the creation of backups and stores those backups in an encrypted backup vault that you designate.  
The centralized policies in AWS Backup also help you define access controls and automate backup access management across all your accounts within your AWS Organizations.  
You can use AWS Backup’s central console to view your AWS resources that are being protected, restore from a backup, and monitor backup and restore activity. Additionally, with AWS Backup, you can generate reports on compliance metrics such as backup frequency, data retention period, and backup coverage across your AWS resources, and demonstrate compliance to auditors.

### Why Should I Use AWS Backup?

Protecting your data is an important step towards achieving business and regulatory compliance requirements. Even durable resources are susceptible to threats such as bugs in your application that can cause accidental deletions or corruption. Building and managing your own backup workflows across all your applications in a compliant and consistent manner can be complex and costly. AWS Backup removes the need for costly, custom solutions or manual processes by providing a fully managed, policy-based data protection solution.

### What Are the Key Features of AWS Backup?

AWS Backup provides a centralized console, automated backup scheduling, backup retention management, and backup monitoring and alerting. AWS Backup offers advanced features such as lifecycle policies to transition backups to a low-cost storage tier. It also includes backup storage and encryption independent from its source data, audit and compliance reporting capabilities with AWS Backup Audit Manager, and delete protection with AWS Backup Vault Lock.

### What Can I back up Using AWS Backup?

You can use AWS Backup to create and manage the backups of the following AWS services:

Amazon Elastic Block Store (EBS) volumes

Amazon EC2 instances (including Windows applications)

AWS CloudFormation stacks

Windows Volume Shadow Copy Service (VSS) supported applications (including Windows Server, Microsoft SQL Server, and Microsoft Exchange Server) on EC2.

Amazon RDS databases (including Amazon Aurora clusters)

Amazon DynamoDB tables, Amazon Elastic File System (EFS) file systems

Amazon FSx for NetApp ONTAP file systems

Amazon FSx for OpenZFS file systems

Amazon FSx for Windows File Server file systems

Amazon FSx for Lustre file systems

Amazon Neptune databases

Amazon DocumentDB (with MongoDB compatibility) databases

AWS Storage Gateway volumes

Amazon S3

VMware CloudTM on AWS and on-premises VMware virtual machines

Amazon Redshift manual snapshot

SAP HANA on EC2

Amazon Timestream databases

### Can I Use AWS Backup to back up On-premises Data?

Yes, you can use AWS Backup can back up on-premises Storage Gateway volumes and VMware virtual machines, providing a common way to manage the backups of your application data both on premises and on AWS.

### Can I Use AWS Backup to Access Backups Created by Services with Existing Backup Capabilities?

Yes. Backups created using services with existing backup capabilities, such as EBS Snapshots, can be accessed using AWS Backup. Similarly, backups created by AWS Backup can be accessed using the source service.

### How Does AWS Backup Work with other AWS Services that Have Backup Capabilities?

AWS services offer backup features to protect your data, such as Amazon S3 Replication, Amazon EBS Snapshots, Amazon RDS snapshots, Amazon FSx backups, Amazon DynamoDB backups, and AWS Storage Gateway snapshots. All existing per-service backup capabilities remain unchanged. AWS Backup provides a common way to manage backups across AWS services both on AWS and on premises. AWS Backup is a centralized service that offers backup scheduling, retention management, and backup monitoring. AWS Backup supports existing backup functionality provided by S3, EBS, RDS, Amazon FSx, DynamoDB, and Storage Gateway. For AWS services with backup functionality built on AWS Backup, such as Amazon EFS and DynamoDB, AWS Backup provides backup management capabilities. Additional features include lifecycle policies to transition backups to a low-cost storage tier, backup storage and encryption independent from its source data, and backup access policies.

### How Does AWS Backup Relate to Amazon Data Lifecycle Manager and when Should I Use One over the Other?

Amazon Data Lifecycle Manager policies and backup plans created in AWS Backup work independently from each other and provide two ways to manage EBS snapshots. Amazon Data Lifecycle Manager provides a streamlined way to manage the lifecycle of EBS resources, such as volume snapshots. Use Amazon Data Lifecycle Manager when you want to automate the creation, retention, and deletion of EBS snapshots. Use AWS Backup to manage and monitor backups across the AWS services you use, including EBS volumes, from a single place.

### What Monitoring and Reporting Capabilities Are Available in the AWS Backup Console?

AWS Backup includes dashboards to track backup activities such as backup, copy, and restore jobs. AWS Backup’s native dashboard provides you with a scalable mechanism to monitor backup health across multiple environments through cross account and cross region support. Furthermore, you can surface and pinpoint specific failure jobs across your organizations using built-in metrics.

In Regions where AWS Backup’s native dashboard is not supported, [Amazon CloudWatch](https://aws.amazon.com/cloudwatch/) dashboards are included in the AWS Backup console, allowing customers to see metrics on completed or failed backup, copy, and restore jobs. Within this dashboard, you can view job status by time period, customized to the schedule you desire.

AWS Backup integrates with [AWS CloudTrail,](https://aws.amazon.com/cloudtrail/) providing a consolidated view of backup activity logs and simplifying the audit process for protected resources.

AWS Backup integrates with [Amazon Simple Notification Service (Amazon SNS)](https://aws.amazon.com/sns/), automating alerting for backup activities such as when a backup succeeds or a restore is initiated.

For a fully managed experience, you can use [AWS Backup Audit Manager](https://docs.aws.amazon.com/aws-backup/latest/devguide/aws-backup-audit-manager.html) to monitor and report your backup activity across your accounts and Regions.

## Core Concepts

Close all

### What is a Recovery Point?

A recovery point represents the content of a resource at a specified time. Recovery points also include metadata such as information about the resource, restore parameters, and tags.

### What is a Backup Plan?

A backup plan is a policy expression that defines when and how you want to back up your AWS resources, such as DynamoDB tables or EFS file systems. You assign resources to backup plans and AWS Backup will then automatically make and retain backups for those resources according to the backup plan. Backup plans are composed of one or more backup rules. Each backup rule is composed of 1) a backup schedule, which includes the backup frequency (Recovery Point Objective \[RPO\]) and backup window; 2) a lifecycle rule that specifies when to transition a backup from one storage tier to another and when to expire the recovery point; 3) the backup vault in which to place the created recovery points; and 4) the tags to be added to backups upon creation. For example, a backup plan might have a “daily backup rule” and a “monthly backup rule.” The daily rule backs up resources every day at midnight and retains the backups for one month. The monthly rule takes a backup once a month on the beginning of every month and retains the backups for one year.

### What is a Backup Vault?

A backup vault is an encrypted storage location in your AWS account that stores and organizes your backups (recovery points). You can create new backup vaults in each AWS Region where AWS Backup is available. Enable delete-protection on the backup vaults using AWS Backup Vault Lock to prevent malicious actors from re-encrypting your data. AWS Backup stores your continuous backups and periodic snapshots in the backup vault of your preference and lets you browse and restore as per your requirements.

### How Does the AWS Backup Lifecycle Feature Work?

The AWS Backup lifecycle feature can automatically transition your recovery points from a warm storage tier to a lower-cost cold storage tier. Cold storage tier is available only for backups of EFS, DynamoDB, Timestream and VMware virtual machines.

### How Does Encryption Work in AWS Backup?

Backups for EFS, DynamoDB, S3, Timestream, and VMware virtual machines are encrypted in transit and at rest independently from source services, adding an additional layer of protection. Encryption is configured at the backup vault level. Backups from other services (EC2, EBS, Amazon FSx, RDS, Aurora, Amazon DocumentDB, Neptune, Storage Gateway) are encrypted using the source service’s backup encryption methodology. For example, EBS snapshots are encrypted using the encryption key of the volume the snapshot was created from.

### How Do I Use Access Policies in a Backup Vault to Control Access to Backups?

AWS Backup can set resource-based policies on backup vaults, enabling you to control access to the backup vault and the backups in it.

### What Services provide Support for AWS Backup Advanced Features?

Services with backup functionality built on AWS Backup support additional backup features, like lifecycle tiering of backups to a low-cost storage tier, backup storage and encryption independent from its source data, and backup access policies. Currently, S3, EFS, Timestream, SAP HANA on EC2 and DynamoDB support AWS Backup advanced features with backup functionality integrated with AWS Backup. To activate AWS Backup advanced features for DynamoDB, you must opt in through settings. EFS, S3, Timestream, SAP HANA on EC2 and VMware virtual machines automatically support AWS Backup advanced features. AWS Backup for S3 supports backup access policies and encryption of backups with a different key, but does not support cold storage tier.

### How Does Delegated Administrator Work?

Delegate backup policy management in AWS Organizations and cross-account monitoring in AWS Backup. This enables delegating backup management to dedicated backup administration accounts, removing the need for member accounts to access management accounts for backup administration. Delegated backup administrators can create and manage backup policies, and monitor backup activity across accounts. You can securely centralize backup management at scale through organization-wide backup administration delegation.

## Compliance

Close all

### What is AWS Backup Audit Manager?

Audit and report on the compliance of your data protection policies with AWS Backup Audit Manager. AWS Backup helps you centralize and automate data protection policies across AWS services based on organizational best practices and regulatory standards. AWS Backup Audit Manager helps maintain and demonstrate compliance with those policies.

### Why Should I Use AWS Backup Audit Manager?

With AWS Backup Audit Manager, verify that the workloads that you create in (or migrate to) AWS meet your data protection requirements. AWS Backup Audit Manager simplifies implementing, tracking, and demonstrating adherence to your backup governance and compliance policies.

### How Can I Use AWS Backup Audit Manager?

You can use AWS Backup Audit Manager through the AWS Management Console, CLI, API, or SDK. AWS Backup Audit Manager provides built-in compliance controls. You can customize these controls to define your data protection policies. It is designed to automatically detect violations of your defined data protection policies and will prompt you to take corrective actions. With AWS Backup Audit Manager, continuously evaluate backup activity and generate audit reports to demonstrate compliance with regulatory requirements.

### What is an AWS Backup Audit Manager Control and Framework?

An AWS Backup Audit Manager control is a procedure designed to audit the compliance of a backup requirement, such as backup frequency or backup retention period. An AWS Backup Audit Manager framework is a collection of controls that can be deployed and managed as a single entity.

### How Does an AWS Backup Audit Manager Control Work?

An AWS Backup Audit Manager control evaluates the configuration of your backup resources against your defined configuration settings. If the resource meets the configuration defined in the control, then the compliance status of the resource for that control is COMPLIANT. If it does not, then the status is NON\_COMPLIANT. If all the resources evaluated by an AWS Backup Audit Manager control are compliant, then the compliance status of the control is COMPLIANT. Similarly, if all the controls in a framework are compliant, then the compliance status of the framework is COMPLIANT.

### How Can I view the compliance Results of My AWS Backup Audit Manager Controls and Frameworks?

On the AWS Backup console, navigate to the AWS Backup Audit Manager Frameworks section and select the framework name to view the compliance status of your framework and controls.

### What Kind of Reports Can I Create in AWS Backup Audit Manager?

You can create reports related to your AWS Backup activity. These reports help you get details of your backup, copy, and restore jobs. You can use these reports to monitor your operational posture and identify any failures that might need further action.

### How Does AWS Backup Audit Manager Work with other AWS Services?

[AWS Conﬁg](https://aws.amazon.com/config/) continuously monitors and records your AWS resource configurations so you can automate the evaluation of recorded configurations against desired configurations. AWS Backup Audit Manager integrates with AWS Config to track your backup activity and transcribe your data protection policies into backup controls. Once you have deployed your backup controls, AWS Backup Audit Manager evaluates your backup activity against your controls and records backup compliance status. You can also generate reports for auditing and monitoring purposes. With AWS Backup Audit Manager, you can create multi-Region and multi-account reports from your AWS Organization's management account.

### How Does the AWS Backup Restore Testing Feature Work and Help with Compliance?

You can automate restore testing using a restore testing plan that defines the frequency of restore tests, target start time, and criteria for recovery point selection. Then, you assign the resources to your plan and specify the default restore parameters and retention period for performing the internal tests before clean up.

After the restore test plan execution completes, you can use the results to meet compliance and governance requirements by showing the successful completion of restore test scenarios and the completion times for the restore job. 

### Which compliance Programs Does AWS Backup Support?

AWS has the longest-running compliance program in the cloud and is committed to helping customers navigate their requirements. AWS Backup has been assessed to meet global and industry security standards. It complies with [PCI DSS](https://aws.amazon.com/compliance/pci-dss-level-1-faqs/) , ISO [9001](https://aws.amazon.com/compliance/iso-9001-faqs/) , [27001](https://aws.amazon.com/compliance/iso-27001-faqs/) , [27017](https://aws.amazon.com/compliance/iso-27017-faqs/) , and [27018](https://aws.amazon.com/compliance/iso-27018-faqs/) , in addition to being [HIPAA eligible](https://aws.amazon.com/compliance/hipaa-compliance/) . That makes it simplified for you to verify our security and meet your own obligations. For more information and resources, visit our [compliance pages](https://aws.amazon.com/compliance/) . You can also go to the [Services in Scope by Compliance Program page](https://aws.amazon.com/compliance/services-in-scope/) to see a full list of services and certifications.

### Is AWS Backup PCI Compliant?

Yes. AWS Backup is [PCI-DSS](https://aws.amazon.com/compliance/pci-dss-level-1-faqs/) compliant, which means you can use it to transfer payment information. You can download the PCI Compliance Package in [AWS Artifact](https://aws.amazon.com/artifact/) to learn more about how to achieve PCI Compliance on AWS.

### Is AWS Backup HIPAA Eligible?

Yes. AWS Backup is HIPAA eligible, which means if you have a [HIPAA BAA in place with AWS](https://aws.amazon.com/compliance/hipaa-compliance/) , you can use AWS Backup to transfer protected health information (PHI).

## Write-Once-Read-Many (WORM)

Close all

### What is AWS Backup Vault Lock?

AWS Backup Vault Lock is a feature that helps you prevent changes to backup lifecycle as well as prevent manual deletion of backups, helping you meet your compliance requirements. AWS Backup Vault Lock implements safeguards that verifies you are storing your backups using a Write-Once-Read-Many (WORM) model.

### Why Should I Use AWS Backup Vault Lock?

AWS Backup Vault Lock verifies that no user, including administrators or perpetrators of malicious actions, can delete your backups or change their lifecycle settings such as retention periods and transition to cold storage. AWS Backup keeps these backups according to your scheduled retention periods, helping you meet your business continuity goals. AWS Backup Vault Lock also works with backup policies such as retention periods, cold storage transitioning, and cross-account/Region copy. This provides an additional layer of protection and helps meet your compliance requirements. AWS Backup Vault Lock protects you from keeping backups that don’t meet your acceptable minimum and maximum retention periods.

### How Does AWS Backup Vault Lock Differ from S3 Glacier Vault Lock?

While AWS Backup Vault Lock applies to data residing in your AWS Backup backup vault, S3 Glacier Vault Lock applies to an individual S3 Glacier Vault. AWS Backup Vault Lock prevents manual deletion of backups and changes to backup lifecycle settings to help you centrally protect backups across AWS services. S3 Glacier Vault Lock enables you to enforce compliance controls that are designed to support long-term record retention for individual S3 Glacier vaults. 

### How Does AWS Backup Vault Lock Work?

AWS Backup Vault Lock is an optional configuration at the AWS Backup vault level and comprises three properties: minimum acceptable retention days, maximum acceptable retention days, and grace time. It blocks backup deletion operations and changes to their lifecycle.

If you activate the AWS Backup Vault Lock configuration, then AWS Backup will protect all newly created recovery points in the vault against deletion and changes to their lifecycle. AWS Backup will also fail all backup jobs with retention periods not meeting the AWS Backup Vault Lock acceptable retention periods.

AWS Backup Vault Lock verifies that your backups are available until they reach their retention periods and expire. If any user, including the root account user, attempts to delete a backup or update its lifecycle properties in a locked vault, AWS Backup denies the operation.

With grace time, you can test the feature for a number of days you define. You can update and remove the AWS Backup Vault Lock configuration as long as the grace time has not expired. Once the grace time expires, AWS Backup will not allow any change to the configuration.

### What is Legal Hold?

Legal holds, also known as litigation holds, are used when an organization must retain certain data either for preservation, auditing, or as evidence in legal proceedings and e-Discovery. These holds prevent backups from being deleted, even if their retention period is over, and remain in place until explicitly released.

## AWS Backup for Amazon S3

Close all

### How Does AWS Backup for S3 Work?

With AWS Backup, you can define a central backup policy to manage backup and restore for your application across AWS services for compute, storage, and database services. Once you define your backup policy and assign S3 resources, AWS Backup automates the creation of S3 backups, and stores those backups in an encrypted storage vault that you designate. Create continuous point-in-time backups or periodic backups of S3 buckets, including object data, object tags, access control lists (ACLs), and user-defined metadata. The first backup is a full snapshot, while subsequent backups are incremental. If there is a data disruption event, choose a backup from the backup vault and restore an S3 bucket (or individual S3 objects) to a new or existing S3 bucket. The centralized policies in AWS Backup also help you define access controls and automate backup access management across all your accounts within your AWS Organizations.

### How Are These Capabilities Different from what Amazon S3 Provides?

Both AWS Backup and Amazon S3 offer capabilities that help you manage the business continuity of your applications. While you can centrally manage backup and restore for your applications across multiple AWS services with AWS Backup, with Amazon S3 you can manage data in S3 buckets and objects. If you’re a backup administrator responsible for the backups, restores, and compliance of your applications across multiple AWS services, you can use AWS Backup to meet those needs. Amazon S3 capabilities such as [Versioning](https://docs.aws.amazon.com/AmazonS3/latest/userguide/Versioning.html) , [Object Lock](https://docs.aws.amazon.com/AmazonS3/latest/userguide/object-lock.html) , and [Replication](https://docs.aws.amazon.com/AmazonS3/latest/userguide/replication.html) help storage administrators preserve data and prevent the unintended deletion of Amazon S3 data. You can use both sets of capabilities together to manage backup and restore across your organization.

### Can I Use an Existing Backup Plan in AWS Backup to Start Backing up Amazon S3?

If you already have a backup plan for your application and want to use it for Amazon S3, add your Amazon S3 resources to the existing backup plan using tags or S3 bucket ARNs. AWS Backup matches the tags in S3 buckets to those assigned to your backup plan and backs up those resources, along with other AWS services your application uses.

### What Backup Options Are Available in AWS Backup for Amazon S3?

You have two backup options available for Amazon S3 resources in AWS Backup: continuous and periodic. Continuous backups can restore Amazon S3 resources to any point in time within the last 35 days. You can use this point-in-time feature to restore your Amazon S3 resources to their condition at any time within the last 35 days. Periodic backups retain data for an infinite period. You can schedule snapshots using frequencies such as 1 hour, 12 hours, 1 day, 1 week, or 1 month, or create them on demand. Continuous backups are useful for undoing accidental deletions, while periodic snapshots can help you meet long-term data retention needs.

### Are there Any Prerequisites to Creating Backups of S3 Buckets?

Yes, turning on S3 Versioning is a prerequisite to creating backups of S3 buckets and objects. [Set a lifecycle expiration period](https://docs.aws.amazon.com/AmazonS3/latest/userguide/how-to-set-lifecycle-configuration-intro.html) for your versions as well—if you don’t, your S3 costs might increase since AWS Backup backs up and stores all unexpired versions of your S3 data. See the [technical documentation](https://docs.aws.amazon.com/aws-backup/latest/devguide/s3-backups.html) for more information.

## AWS Backup Support for VMWare

Close all

### How Does AWS Backup Help with VMware Data Protection?

AWS Backup extends its in-cloud, fully managed service capabilities to your VMware environment, helping you provide a unified view of backups across your AWS and on-premises AWS environments. AWS Backup integrates with VMware ESXi VMs, schedules and manages VMware backups, and stores backups in AWS, so you can fully manage VMware data protection from AWS. Using AWS Backup, you can efficiently store backups in AWS, and copy them across AWS Regions and accounts for business continuity and ransomware protection. You can restore VMware backups on premises or in AWS for business continuity validation and test/dev use cases. The AWS Backup policy-driven approach helps you centrally manage protection of VMware workloads along with supported AWS services for compute, storage, and databases in an automated, scalable way.

### How Does AWS Backup Support for VMware Work?

AWS Backup connects to VMware workloads using AWS Backup gateway, which you’ll deploy in your VMware environment. AWS Backup gateway discovers VMs through VMware vCenter Server, takes VM snapshots, and manages backup and restore data between AWS Backup and your VMware environment. You can use tags, VM Resource IDs, or group assignment by VM folder or hypervisor to assign VMs to your backup policies. These centrally govern data protection of VMware VMs with supported AWS Backup services. After completing these steps, AWS Backup starts backing up VMs securely into its storage vaults. You can view your VMware backups from AWS Backup and restore the backups on premises or in AWS as per your requirement.

### Which VMware Versions and Features Do You Support Using AWS Backup?

AWS Backup supports VMware ESXi 6.7.X, and 7.0.X VMs running on NFS, VMFS, and VSAN datastores on premises, in VMware CloudTM on AWS, and on VMware CloudTM on AWS Outposts. And AWS Backup supports both SCSI Hot-Add and Network Block Device (NBD) transport modes for copying data from source virtual machines (VMs) to AWS.

### What VMware CloudTM on AWS Outposts Deployment Use Cases Do You Support?

You can use AWS Backup to protect your VMs on VMware CloudTM on AWS Outposts. AWS Backup stores your VM backups in the AWS Region your VMware CloudTM on AWS Outposts is connected to. You can use AWS Backup to protect your VMware CloudTM on AWS Outposts VMs when using VMware CloudTM to meet your low latency and local data processing needs for your application data. Based on your data residency requirements, you can choose AWS Backup to store backups of your application data in the parent AWS Region that your Outposts is connected to.

### Where Can I Restore VMware Backups?

You can restore VMware backups to a new on-premises VMware virtual host, VMware CloudTM on AWS, VMware CloudTM on AWS Outposts, Amazon EBS, or Amazon EC2 from the AWS Backup console.

### Can I Transition VMware Backups to a Cold Storage Tier?

Yes, based on your organizational needs, you can configure lifecycle policies in AWS Backup to automatically transition your VMware backups from warm storage to low-cost cold storage. Backups that are transitioned to cold storage have a minimum 90 days of storage, and backups deleted before 90 days incur a pro-rated charge equal to the storage charge for the remaining days.

### What Backup Modes Do You Support for VMware?

AWS Backup supports first full, then incremental-forever backups of VMware VMs that you can create on demand or through the schedule as configured in your backup plan.

### What Level of Consistency Do You Support for VMware Backups?

AWS Backup, by default, captures app-consistent backups of VMware VMs using the VMware Tools quiescence setting on the VM. If the quiescence capability is not available, AWS Backup captures crash-consistent backups.

### Does AWS Backup Support Compression for VMware Backups?

Yes, AWS Backup compresses VMware backups in transit to AWS, helping you optimally use your network connection to AWS.

### Are My VMware Backups Encrypted?

Yes, your VM backups are encrypted in transit and at rest using AES-256 encryption algorithm. You can also use customer-managed keys to encrypt backups stored in the cloud.

### Can I Copy VMware Backups to Another AWS Region?

Store a copy of VMware backups in a different AWS Region from your production backups to meet business continuity, disaster recovery, and compliance requirements.

### Can I Copy VMware Backups to Another AWS Account?

Yes, you can copy VMware backups to another AWS account, helping you use backups between your production and dev/test environments, or between different department and project accounts. Copying VMware backups to another AWS account, which is enabled by AWS Backup’s integration with AWS Organizations, also provides an extra level of account isolation and security.

### How much Network Bandwidth Do I Need to back up VMware VMs to AWS?

The required network bandwidth depends on the VMware VMs you want to protect, the size of each VM, incremental data generated per VM, and your backup window and restore requirements. We recommend you have at least 100-Mbps bandwidth to AWS to back up on-premises VMware VMs using AWS Backup.

### Can I Deploy an AWS Backup Gateway on My Private Non-routable Network? Does AWS Backup Gateway Support AWS PrivateLink?

Yes. You can deploy a AWS Backup gateway on a private, non-routable network if that network is connected to your Amazon VPC through Direct Connect or VPN. Backup gateway traffic is routed through VPC endpoints powered by AWS PrivateLink, which enables private connectivity between AWS services using elastic network interfaces (ENI) with private IPs in your VPCs.

### What is the Cost for Using VPC Endpoints with AWS Backup Gateway?

You will be billed for each hour that your VPC endpoint remains provisioned. Data processing charges also apply for each Gigabyte processed through the VPC endpoint regardless of the traffic’s source or destination. Visit [AWS PrivateLink](https://aws.amazon.com/privatelink/pricing/) pricing to learn more.