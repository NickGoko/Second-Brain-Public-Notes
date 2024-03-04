---
tags:
  - cloud/aws
Associations:
---

[Amazon RDS UserGuide](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Welcome.html)

![](https://i.imgur.com/OMTBhMt.png)


### DB Instance Classes
The DB instance class determines the computation and memory capacity of an Amazon RDS DB instance. The DB instance class that you need depends on your processing power and memory requirements.  
![](https://i.imgur.com/hhA5Vz7.png)


![[Module 5- adding a database layer#** Amazon RDS **]]



![[Module 5- adding a database layer#Securing Amazon RDS Databases]]



![[Module 5- adding a database layer#**[AWS Database Migration Service]( )**]]



## Amazon RDS FAQs
<mark style="background: #FF5582A6;">When would i use Amazon RDS vs. Amazon EC2 Relational Database AMIs?</mark>  
- Amazon RDS enables you to run a fully managed and fully featured relational database <mark style="background: #FFF3A3A6;">while offloading database administration</mark>  
- Using one of many relational database AMIs on Amazon EC2 <mark style="background: #FFF3A3A6;">allows you to manage your own relational database in the cloud.</mark>

<mark style="background: #FF5582A6;">Are there hybrid or on premises deployment option for Amazon RDS </mark>  
- Yes. YOU can run Amazon RDS on premises using Amazon RDS on Outposts.  
  
<mark style="background: #FF5582A6;"> How do I set up a connection between an application or a SQL based client running on an Amazon EC2 compute instance and my Amazon RDS database instance/cluster?</mark>  
- You can set up a connection between an EC2 compute instance and a new Amazon RDS database using the Amazon RDS console. On the “Create database” page, select “Connect to an EC2 compute resource” option in the Connectivity Section.  
- When you select this option, <mark style="background: #FFF3A3A6;">Amazon RDS automates the manual networking set up tasks such as creating a VPC, security groups, subnets, and ingress/egress rules to establish a connection between your application and database.</mark>  
- Additionally, <mark style="background: #FFF3A3A6;">you can set up a connection between an existing Amazon RDS database and an EC2 compute instance. To do so, open the RDS console, select an RDS database from the database list page, and choose “Set up EC2 connection” from the "Action" menu dropdown list. Amazon RDS automatically sets up your related network settings to enable a secure connection between the selected EC2 instance and the RDS database.</mark>

<mark style="background: #FF5582A6;">How do I set up a connection between a serverless Lambda application and my Amazon RDS or Amazon Aurora database instance and/or cluster?</mark>  
- <mark style="background: #FFF3A3A6;">You can set up a connection between an AWS Lambda function and an Amazon RDS or Amazon Aurora database from the Amazon RDS console. On the RDS console, select an RDS or Aurora database from the database list page, and choose “Set up Lambda connection” from the "Action" menu. Amazon RDS automatically sets up your related network settings to enable a secure connection between the selected Lambda function and the RDS or Aurora database.</mark>  
We recommend that you use RDS Proxy during this connection set up. You can set up this connection either by using an existing RDS Proxy or using a new RDS Proxy that you can auto create during the connection.

<mark style="background: #FF5582A6;"> What is a database instance (DB instance)?</mark>  
- <mark style="background: #FFF3A3A6;">DB instances are simple to create using either the AWS Management Console, Amazon RDS APIs, or AWS Command Line Interface. </mark>
- To launch a DB instance using the AWS Management Console, click "RDS" and then the “Launch DB Instance” button on the Instances tab. From there, you can specify the parameters for your DB instance, including DB engine and version, license model, instance type, storage type and amount, and primary user credentials.

<mark style="background: #FF5582A6;">How many DB instances can I run with Amazon RDS?</mark>  
By default, customers are allowed to have <mark style="background: #FFF3A3A6;">up to a total of 40 Amazon RDS DB instances. Of those 40, up to 10 can be Oracle or SQL Server DB instances </mark>under the "License Included" model. <mark style="background: #FFF3A3A6;">All 40 can be used for Amazon Aurora, MySQL, MariaDB, PostgreSQL, and Oracle </mark>under the "BYOL" model. Note that RDS for SQL Server has a limit of up to 100 databases on a single DB instance.

<mark style="background: #FF5582A6;">How many databases or schemas can I run within a DB instance?</mark>
- RDS for Amazon Aurora: No limit imposed by software
- RDS for MySQL: No limit imposed by software
- RDS for MariaDB: No limit imposed by software
- RDS for Oracle: 1 database per instance; no limit on the number of schemas per database imposed by software
- RDS for SQL Server: Up to 100 databases per instance
- RDS for PostgreSQL: No limit imposed by software

<mark style="background: #FF5582A6;">How do i import data into an Amazon RDS DB instance</mark>  
There are a number of simple ways to import data into Amazon RDS, such as:  
	- [mysqldump](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/MySQL.Procedural.Importing.SmallExisting.html) or [mysqlimport](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/MySQL.Procedural.Importing.AnySource.html) utilities for MySQL;  
	- [Data Pump](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Oracle.Procedural.Importing.DataPump.html), [import/export](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Oracle.Procedural.Importing.ExportImport.html), or [SQL Loader](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Oracle.Procedural.Importing.SQLLoader.html) for Oracle;  
	-  [Import/Export wizard](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/SQLServer.Procedural.Importing.Snapshots.html), full backup files(.bak files), or Bulk Copy Program(BCP) for SQL server; or [pg_dump](https://docs.aws.amazon.com/dms/latest/sql-server-to-aurora-postgresql-migration-playbook/chap-sql-server-aurora-pg.management.exportimport.html) for PostgreSQL  
	- For more information on data import and export, please refer to the [Data Import Guide for MySQL](http://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/MySQL.Procedural.Importing.html), the [Data Import Guide for Oracle](http://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Oracle.Procedural.Importing.html), the [Data Import Guide for SQL Server](http://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/SQLServer.Procedural.Importing.html), or the [Data Import Guide for PostgreSQL](http://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/PostgreSQL.Procedural.Importing.html).  
	In addition, [AWS Database Migration Service](https://aws.amazon.com/dms/) can help you migrate to AWS easily and securely. 



**Amazon Relational Database Service (Amazon RDS)** is a managed service that you can use to launch and manage relational databases on AWS.  
<mark style="background: #BBFABBA6;">Amazon RDS is an Online Transaction Processing (OLTP) type of database.</mark>

- The primary use case is a transactional database (rather than an analytical database).
- It is best suited to structured, relational data store requirements.
- It aims to be drop-in replacement for existing on-premises instances of the same databases.

- Automated backups and patching are applied in customer-defined maintenance windows.

Push-button scaling, replication, and redundancy.

Amazon RDS supports the following database engines:

- Amazon Aurora.
- MySQL.
- MariaDB.
- Oracle.
- SQL Server.
- PostgreSQL.

RDS is a managed service and you do not have access to the underlying EC2 instance (no root access).

The exception to the above rule is Amazon RDS Custom which allows access to the underlying operating system. This is new, available for limited DB engines, and does not appear on the exam yet.

The Amazon RDS managed service includes the following:

- Security and patching of the DB instances.
- Automated backup for the DB instances.
- Software updates for the DB engine.
- Easy scaling for storage and compute.
- Multi-AZ option with synchronous replication.
- Automatic failover for Multi-AZ option.
- Read replicas option for read heavy workloads.

A DB instance is a database environment in the cloud with the compute and storage resources you specify.

Database instances are accessed via endpoints.

Endpoints can be retrieved via the DB instance description in the AWS Management Console, **DescribeDBInstances** API or **describe-db-instances** command.

By default, customers are allowed to have up to a total of 40 Amazon RDS DB instances (only 10 of these can be Oracle or MS SQL unless you have your own licenses).

Maintenance windows are configured to allow DB instances modifications to take place such as scaling and software patching (some operations require the DB instance to be taken offline briefly).

You can define the maintenance window or AWS will schedule a 30-minute window.

Windows integrated authentication for SQL only works with domains created using the AWS directory service – need to establish a trust with an on-premises AD directory.

Events and Notifications:

- Amazon RDS uses AWS SNS to send RDS events via SNS notifications.
- You can use API calls to the Amazon RDS service to list the RDS events in the last 14 days (DescribeEvents API).
- You can view events from the last 14 days using the CLI.
- Using the AWS Console you can only view RDS events for the last 1 day.

## Use Cases, Alternatives and Anti-Patterns

The table below provides guidance on when best to use RDS and several other AWS database/data store services:

|   |   |
|---|---|
|**Data Store**|**When to Use**|
|Database on EC2|- Ultimate control over database<br>- Preferred DB not available under RDS|
|Amazon RDS|- Need traditional relational database for OLTP<br>- Your data is well formed and structured<br>- Existing apps requiring RDBMS|
|Amazon DynamoDB|- Name/value pair data or unpredictable data structure<br>- In-memory performance with persistence<br>- High I/O needs<br>- Scale dynamically|
|Amazon RedShift|- Massive amounts of data<br>- Primarily OLAP workloads|
|Amazon Neptune|- Relationships between objects a major portion of data value|
|Amazon Elasticache|- Fast temporary storage for small amounts of data<br>- Highly volatile data|
|Amazon S3|- BLOBs<br>- Static Websites|

**Alternative to Amazon RDS:**

If your use case isn’t supported on RDS, you can run databases on Amazon EC2.

Consider the following points when considering a DB on EC2:

- You can run any database you like with full control and ultimate flexibility.
- You must manage everything like backups, redundancy, patching and scaling.
- Good option if you require a database not yet supported by RDS, such as IBM DB2 or SAP HANA.
- Good option if it is not feasible to migrate to AWS-managed database.

**Anti-Patterns:**

Anti-patterns are certain patterns in architecture or development that are considered bad, or sub-optimal practices – i.e. there may be a better service of method to produce the best result.

The following table describes requirements that are not a good fit for RDS:

|   |   |
|---|---|
|**Requirement**|**More Suitable Service**|
|Lots of large binary objects (BLOBs)|S3|
|Automated Scalability|DynamoDB|
|Name/Value Data Structure|DynamoDB|
|Data is not well structured or unpredictable|DynamoDB|
|Other database platforms like IBM DB2 or SAP HANA|EC2|
|Complete control over the database|EC2|

## Encryption

You can encrypt your Amazon RDS instances and snapshots at rest by enabling the encryption option for your Amazon RDS DB instance.

Encryption at rest is supported for all DB types and uses AWS KMS.

When using encryption at rest the following elements are also encrypted:

- All DB snapshots.
- Backups.
- DB instance storage.
- Read Replicas.

You cannot encrypt an existing DB, you need to create a snapshot, copy it, encrypt the copy, then build an encrypted DB from the snapshot.

Data that is encrypted at rest includes the underlying storage for a DB instance, its automated backups, Read Replicas, and snapshots.

A Read Replica of an Amazon RDS encrypted instance is also encrypted using the same key as the master instance when both are in the same region.

If the master and Read Replica are in different regions, you encrypt using the encryption key for that region.

You can’t have an encrypted Read Replica of an unencrypted DB instance or an unencrypted Read Replica of an encrypted DB instance.

Encryption/decryption is handled transparently.

RDS supports SSL encryption between applications and RDS DB instances.

RDS generates a certificate for the instance.

## DB Subnet Groups
A DB subnet group is a collection of subnets (typically private) that you create in a VPC and that you then designate for your DB instances.

Each DB subnet group should have subnets in at least two Availability Zones in a given region.

It is recommended to configure a subnet group with subnets in each AZ (even for standalone instances).

During the creation of an RDS instance you can select the DB subnet group and the AZ within the group to place the RDS DB instance in.

You cannot pick the IP within the subnet that is allocated.

## Billing and Provisioning
AWS Charge for:
- DB instance hours (partial hours are charged as full hours).
- Storage GB/month.
- I/O requests/month – for magnetic storage.
- Provisioned IOPS/month – for RDS provisioned IOPS SSD.
- Egress data transfer.
- Backup storage (DB backups and manual snapshots).

Backup storage for the automated RDS backup is free of charge up to the provisioned EBS volume size.

However, AWS replicate data across multiple AZs and so you are charged for the extra storage space on S3.

For multi-AZ you are charged for:

- Multi-AZ DB hours.
- Provisioned storage.
- Double write I/Os.

For multi-AZ you are not charged for DB data transfer during replication from primary to standby.

Oracle and Microsoft SQL licenses are included, or you can bring your own (BYO).

<mark style="background: #FFB86CA6;">On-demand and reserved instance pricing available.</mark>

_Reserved instances_ are defined based on the following attributes which must not be changed:
- DB engine.
- DB instance class.
- Deployment type (standalone, multi-AZ_.
- License model.
- Region.

Reserved instances:
- Can be moved between AZs in the same region.
- Are available for multi-AZ deployments.
- Can be applied to Read Replicas if DB instance class and region are the same.
- Scaling is achieved through changing the instance class for compute and modifying storage capacity for additional storage allocation.

## Scalability

You can only scale RDS up (compute and storage).

You cannot decrease the allocated storage for an RDS instance.

You can scale storage and change the storage type for all DB engines except MS SQL.

For MS SQL the workaround is to create a new instance from a snapshot with the new configuration.

Scaling storage can happen while the RDS instance is running without outage however there may be performance degradation.

Scaling compute will cause downtime.

You can choose to have changes take effect immediately, however the default is within the maintenance window.

Scaling requests are applied during the specified maintenance window unless “apply immediately” is used.

All RDS DB types support a maximum DB size of 64 TiB except for Microsoft SQL Server (16 TiB)

## Performance

Amazon RDS uses EBS volumes (never uses instance store) for DB and log storage.

There are three storage types available: General Purpose (SSD), Provisioned IOPS (SSD), and Magnetic.

General Purpose (SSD):

- Use for Database workloads with moderate I/O requirement.
- Cost effective.
- Also called gp2.
- 3 IOPS/GB.
- Burst up to 3000 IOPS.

Provisioned IOPS (SSD):

- Use for I/O intensive workloads.
- Low latency and consistent I/O.
- User specified IOPS (see table below).

For provisioned IOPS storage the table below shows the range of Provisioned IOPS and storage size range for each database engine.

|   |   |   |
|---|---|---|
|**Database Engine**|**Range of Provisioned IOPS**|**Range of Storage**|
|MariaDB|1,000-80,000 IOPS|100 GiB-64TiB|
|SQL Server|1,000-64,000 IOPS|20 GiB-16TiB|
|MySQL|1,000-80,000 IOPS|100 GiB-64TiB|
|Oracle|1,000-256,000 IOPS|100 GiB-64TiB|
|PostgreSQL|1,000-80,000 IOPS|100 GiB-64TiB|

Magnetic:

- Not recommended anymore, available for backwards compatibility.
- Doesn’t allow you to scale storage when using the SQL Server database engine.
- Doesn’t support elastic volumes.
- Limited to a maximum size of 4 TiB.
- Limited to a maximum of 1,000 IOPS.

## Multi-AZ and Read Replicas

Multi-AZ and Read Replicas are used for high availability, fault tolerance and performance scaling.

The table below compares multi-AZ deployments to Read Replicas:

|   |   |
|---|---|
|**Multi-AZ Deployments**|**Read Replicas**|
|Synchronous Replication – highly durable|Asynchronous replication – highly scalable|
|Only database engine on primary instance is active|All read replicas are accessible and can be used for read scaling|
|Automated backups are taken from standby|No backups configured by default|
|Always span two availability zones within a single region|Can be within an Availability Zone, Cross-AZ, or Cross-Region|
|Database engine version upgrades happen on primary|Database engine version upgrade is independent from source instance|
|Automatic failover to standby when a problem is detected|Can be manually promoted to a standalone database instance|      
![](https://i.imgur.com/4Uk7lXK.png)
## Instances & Availability Zones

- A Single AZ instance creates a single DB instance in any specified AZ.
- A [Multi-AZ DB Instance](https://jayendrapatil.com/aws-rds-multi-az-db-instance/) deployment creates a Primary and a Standby instance in two different AZs
- A [Multi-AZ DB Cluster](https://jayendrapatil.com/aws-rds-multi-az-db-cluster/) <mark style="background: #D2B3FFA6;">deployment creates a Primary Writer and two Readable Standby instances in three different AZs</mark>  
	  ![](https://i.imgur.com/pqU5vCJ.png)
	- When a change is made on the writer DB instance, it’s sent to each reader DB instance. Acknowledgment from at least one reader DB instance is required for a change to be committed.
	- Reader DB instances act as automatic failover targets and also serve read traffic to increase application read throughput.
	- If an outage occurs on the writer DB instance, RDS manages failover to one of the reader DB instances. RDS does this based on which reader DB instance has the most recent change record.
	- Multi-AZ DB clusters typically have lower write latency when compared to Multi-AZ DB instance deployments.
## Use Cases
- Single AZ deployments are suitable for non-critical dev, test environments.
- Multi-AZ deployments are suitable for critical, production-based environments requiring high availability, data redundancy, and scalability for read workloads.
## Replication Mode

- Multi-AZ DB instance deployment synchronously replicates the data from the primary DB instance to a standby instance in a different AZ.
- Multi-AZ DB cluster deployment semi-synchronously replicates data from the writer DB instance to both reader DB instances using the DB engine’s native replication capabilities.

## Standby Instance Can Accept Reads

- Multi-AZ DB instance deployment is a high-availability solution and the standby instance does not support requests.
- Multi-AZ DB cluster deployment provides readable standby instances to increase application read-throughput.
### Multi-AZ

<mark style="background: #BBFABBA6;">Multi-AZ RDS creates a replica in another AZ and synchronously replicates to it</mark> (DR only).

- There is an option to choose multi-AZ during the launch wizard.
- <mark style="background: #ADCCFFA6;">AWS recommends the use of provisioned IOPS storage for multi-AZ RDS DB instances.</mark>
- Each AZ runs on its own physically distinct, independent infrastructure, and is engineered to be highly reliable.

- <mark style="background: #BBFABBA6;">You cannot choose which AZ in the region will be chosen to create the standby DB instance.</mark>
- You can view which AZ the standby DB instance is created in.

A failover may be triggered in the following circumstances:
- Loss of primary AZ or primary DB instance failure.
- Loss of network connectivity on primary.
- Compute (EC2) unit failure on primary.
- Storage (EBS) unit failure on primary.
- The primary DB instance is changed.
- Patching of the OS on the primary DB instance.
- Manual failover (reboot with failover selected on primary).

<mark style="background: #FFB86CA6;">During failover RDS automatically updates configuration (including DNS endpoint) to use the second node.</mark>

- Depending on the instance class it can take 1 to a few minutes to failover to a standby DB instance.
- It is recommended to implement DB connection retries in your application.
- <mark style="background: #FFB86CA6;">Recommended to use the endpoint rather than the IP address to point applications to the RDS DB.</mark>

- The method to <mark style="background: #CACFD9A6;">initiate a manual RDS DB instance failover is to reboot </mark>selecting the option to failover.

- <mark style="background: #FFF3A3A6;">A DB instance reboot is required for changes to take effect when you change the DB parameter group or when you change a static DB parameter.</mark>  
	The DB parameter group is a configuration container for the DB engine configuration.

- You will be alerted by a DB instance event when a failover occurs.
- The secondary DB in a multi-AZ configuration cannot be used as an independent read node (read or write).
- <mark style="background: #BBFABBA6;">There is no charge for data transfer between primary and secondary RDS instances.</mark>

- <mark style="background: #FF5582A6;">System upgrades like OS patching, DB Instance scaling and system upgrades, are applied first on the standby, before failing over and modifying the other DB Instance.</mark>
- <mark style="background: #BBFABBA6;">In multi-AZ configurations snapshots and automated backups are performed on the standby to avoid I/O suspension on the primary instance.</mark>

Read Replica Support for Multi-AZ:
- Amazon RDS Read Replicas for MySQL, MariaDB, PostgreSQL, and Oracle support Multi-AZ deployments.
- <mark style="background: #BBFABBA6;">Combining Read Replicas with Multi-AZ enables you to build a resilient disaster recovery strategy and simplify your database engine upgrade process.</mark>
- <mark style="background: #ADCCFFA6;">A Read Replica in a different region than the source database can be used as a standby database and promoted to become the new production database in case of a regional disruption.</mark>
- This allows you to scale reads whilst also having multi-AZ for DR.

- The process for implementing maintenance activities is as follows:
	- Perform operations on standby.
	- Promote standby to primary.
	- Perform operations on new standby (demoted primary).

- You can manually upgrade a DB instance to a supported DB engine version from the AWS Console.  
  By default upgrades will take effect during the next maintenance window.  
  You can optionally force an immediate upgrade.
  
<mark style="background: #ADCCFFA6;">In multi-AZ deployments version upgrades will be conducted on both the primary and standby at the same time causing an outage of both DB instance.</mark>

Ensure security groups and NACLs will allow your application servers to communicate with both the primary and standby instances.

![Amazon RDS Multi-AZ](https://digitalcloud.training/wp-content/uploads/2022/01/amazon-rds-multi-az.jpeg)

### Read Replicas

- <mark style="background: #FFB86CA6;">Read replicas are used for read-heavy DBs and replication is asynchronous.</mark>
- Read replicas are for workload sharing and offloading.
- Read replicas provide read-only DR.
- Read replicas are created from a snapshot of the master instance.  
Must have automated backups enabled on the primary (retention period > 0).

Only supported for transactional database storage engines (InnoDB not InnoDB).

- Read replicas are available for MySQL, PostgreSQL, MariaDB, Oracle, Aurora, and SQL Server.
- For the MySQL, MariaDB, PostgreSQL, and Oracle database engines, Amazon RDS creates a second DB instance using a snapshot of the source DB instance.  
	It then uses the engines’ native asynchronous replication to update the read replica whenever there is a change to the source DB instance.

[[Amazon Aurora]] employs an SSD-backed virtualized storage layer purpose-built for database workloads.

You can take snapshots of PostgreSQL read replicas but cannot enable automated backups.

You can enable automatic backups on MySQL and MariaDB read replicas.

You can enable writes to the MySQL and MariaDB Read Replicas.

You can have 5 read replicas of a production DB.

You cannot have more than four instances involved in a replication chain.

You can have read replicas of read replicas for MySQL and MariaDB but not for PostgreSQL.

Read replicas can be configured from the AWS Console or the API.

You can specify the AZ the read replica is deployed in.

The read replicas storage type and instance class can be different from the source but the compute should be at least the performance of the source.

You cannot change the DB engine.

In a multi-AZ failover the read replicas are switched to the new primary.

Read replicas must be explicitly deleted.

If a source DB instance is deleted without deleting the replicas each replica becomes a standalone single-AZ DB instance.

You can promote a read replica to primary.

Promotion of read replicas takes several minutes.

Promoted read replicas retain:

- Backup retention window.
- Backup window.
- DB parameter group.

Existing read replicas continue to function as normal.

Each read replica has its own DNS endpoint.

Read replicas can have multi-AZ enabled and you can create read replicas of multi-AZ source DBs.

Read replicas can be in another region (uses asynchronous replication).

This configuration can be used for centralizing data from across different regions for analytics.

![Amazon RDS Read Replicas](https://digitalcloud.training/wp-content/uploads/2022/01/amazon-rds-read-replicas.jpeg)


## RDS Cross-Region Read Replicas
- RDS Cross-Region Read Replicas<mark style="background: #BBFABBA6;"> create an asynchronously replicated read-only DB instance in a secondary AWS Region.</mark>
- Supported for MySQL, PostgreSQL, MariaDB, Oracle, and SQL Server
- Cross-Region Read Replicas help to improve
    - disaster recovery capabilities (reduces RTO and RPO),
    - scale read operations into a region closer to end users,
    - migration from a data center in one region to another region  
![](https://i.imgur.com/x99YK68.png)



### RDS Cross-Region Read Replicas Process
- RDS configures the source DB instance as a replication source and setups the specified read replica in the destination AWS Region.
    
- RDS creates an automated DB snapshot of the source DB instance in the source AWS Region.
- RDS begins a cross-Region snapshot copy for the initial data transfer.
- RDS then uses the copied DB snapshot for the initial data load on the read replica. When the load is complete the DB snapshot copy is deleted.
- RDS starts by replicating the changes made to the source instance since the start of the create read replica operation.

### RDS Cross-Region Read Replicas Considerations
- A source DB instance can have cross-region read replicas in multiple AWS Regions.
- Replica lags are higher for Cross-region replicas. This lag time comes from the longer network channels between regional data centers.
- RDS can’t guarantee more than five cross-region read replica instances, due to the limit on the number of access control list (ACL) entries for a VPC
- Read Replica uses the default DB parameter group and DB option group for the specified DB engine when configured from AWS console
- Read Replica uses the default security group.
- Cross-Region RDS read replica can be created from a source RDS DB instance that is not a read replica of another RDS DB instance for Microsoft SQL Server, Oracle, and PostgreSQL DB instances. This limitation doesn’t apply to MariaDB and MySQL DB instances.
- Deleting the source for a cross-region read replica will result in
    - read replica promotion for MariaDB, MySQL, and Oracle DB instances
    - no read replica promotion for PostgreSQL DB instances and the replication status of the read replica is set to `terminated`.
## DB Snapshots
DB Snapshots are user-initiated and enable you to back up your DB instance in a known state as frequently as you wish, and then restore to that specific state.

Cannot be used for point-in-time recovery.

Snapshots are stored on S3.

Snapshots remain on S3 until manually deleted.

Backups are taken within a defined window.

I/O is briefly suspended while backups initialize and may increase latency (applicable to single-AZ RDS).

DB snapshots that are performed manually will be stored even after the RDS instance is deleted.

Restored DBs will always be a new RDS instance with a new DNS endpoint.

Can restore up to the last 5 minutes.

Only default DB parameters and security groups are restored – you must manually associate all other DB parameters and SGs.

It is recommended to take a final snapshot before deleting an RDS instance.

Snapshots can be shared with other AWS accounts.

## High Availability Approaches for Databases

If possible, choose DynamoDB over RDS because of inherent fault tolerance.

If DynamoDB can’t be used, choose Aurora because of redundancy and automatic recovery features.

If Aurora can’t be used, choose Multi-AZ RDS.

Frequent RDS snapshots can protect against data corruption or failure, and they won’t impact performance of Multi-AZ deployment.

Regional replication is also an option but will not be strongly consistent.

If the database runs on EC2, you must design the HA yourself.

## Migration

AWS Database Migration Service helps you migrate databases to AWS quickly and securely.

Use along with the Schema Conversion Tool (SCT) to migrate databases to AWS RDS or EC2-based databases.

The source database remains fully operational during the migration, minimizing downtime to applications that rely on the database.

The AWS Database Migration Service can migrate your data to and from most widely used commercial and open-source databases.

Schema Conversion Tool can copy database schemas for homogeneous migrations (same database) and convert schemas for heterogeneous migrations (different database).

DMS is used for smaller, simpler conversions and supports MongoDB and DynamoDB.

SCT is used for larger, more complex datasets like data warehouses.

DMS has replication functions for on-premises to AWS or to Snowball or S3.

## Monitoring, Logging and Reporting

You can use the following automated monitoring tools to watch Amazon RDS and report when something is wrong:

- **Amazon RDS Events** – Subscribe to Amazon RDS events to be notified when changes occur with a DB instance, DB snapshot, DB parameter group, or DB security group.
- **Database log files** – View, download, or watch database log files using the Amazon RDS console or Amazon RDS API operations. You can also query some database log files that are loaded into database tables.
- **Amazon RDS Enhanced Monitoring** — Look at metrics in real time for the operating system.
- **Amazon RDS Performance Insights** — Assess the load on your database and determine when and where to act.
- **Amazon RDS Recommendations** — Look at automated recommendations for database resources, such as DB instances, read replicas, and DB parameter groups.

In addition, Amazon RDS integrates with Amazon CloudWatch, Amazon EventBridge, and AWS CloudTrail for additional monitoring capabilities:

- **Amazon CloudWatch Metrics** – Amazon RDS automatically sends metrics to CloudWatch every minute for each active database. You don’t get additional charges for Amazon RDS metrics in CloudWatch.
- **Amazon CloudWatch Alarms** – You can watch a single Amazon RDS metric over a specific time period. You can then perform one or more actions based on the value of the metric relative to a threshold that you set.
- **Amazon CloudWatch Logs** – Most DB engines enable you to monitor, store, and access your database log files in CloudWatch Logs.
- **Amazon CloudWatch Events and Amazon EventBridge** – You can automate AWS services and respond to system events such as application availability issues or resource changes. Events from AWS services are delivered to CloudWatch Events and EventBridge nearly in real time. You can write simple rules to indicate which events interest you and what automated actions to take when an event matches a rule
- **AWS CloudTrail** – You can view a record of actions taken by a user, role, or an AWS service in Amazon RDS. CloudTrail captures all API calls for Amazon RDS as events. These captures include calls from the Amazon RDS console and from code calls to the Amazon RDS API operations. If you create a trail, you can enable continuous delivery of CloudTrail events to an Amazon S3 bucket, including events for Amazon RDS. If you don’t configure a trail, you can still view the most recent events in the CloudTrail console in **Event history**.

## Authorization and Access Control

Amazon RDS supports [identity-based policies](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/security_iam_service-with-iam.html#security_iam_service-with-iam-resource-based-policies).

RDS does not support resource-based policies.

The following AWS managed policies, which you can attach to users in your account, are specific to Amazon RDS:

- **AmazonRDSReadOnlyAccess** – Grants read-only access to all Amazon RDS resources for the AWS account specified.
- **AmazonRDSFullAccess** – Grants full access to all Amazon RDS resources for the AWS account specified.

You can authenticate to your DB instance using AWS Identity and Access Management (IAM) database authentication. IAM database authentication works with MySQL and PostgreSQL. With this authentication method, you don’t need to use a password when you connect to a DB instance. Instead, you use an authentication token.

IAM database authentication provides the following benefits:

- Network traffic to and from the database is encrypted using Secure Sockets Layer (SSL).
- You can use IAM to centrally manage access to your database resources, instead of managing access individually on each DB instance.
- For applications running on Amazon EC2, you can use profile credentials specific to your EC2 instance to access your database instead of a password, for greater security.


![[Module 9 - Implementing Elasticity, High Availability, and Monitoring#Scaling with Amazon RDS]]

><mark style="background: #BBFABBA6;">Spot and Provisioned Instance pricing are available with other AWS service but not with Amazon RDS</mark>. For more information, see [Amazon RDS Pricing](https://aws.amazon.com/rds/pricing/).

![[AWS Solutions Architect Skillbuilder#Use Case 1]]

# FAQ
## General

### What is Amazon RDS?

[Amazon Relational Database Service (Amazon RDS)](https://aws.amazon.com/rds/) is a managed service that makes it easy to set up, operate, and scale a [relational database](https://aws.amazon.com/relational-database/) in [the cloud](https://aws.amazon.com/what-is-cloud-computing/). It provides cost-efficient and resizable capacity, while managing time-consuming database administration tasks, freeing you to focus on your applications and business.

Amazon RDS gives you access to the capabilities of a familiar [RDS for PostgreSQL](https://aws.amazon.com/rds/postgresql/), [RDS for MySQL](https://aws.amazon.com/rds/mysql/), [RDS for MariaDB](https://aws.amazon.com/rds/mariadb/), [RDS for SQL Server](https://aws.amazon.com/rds/sqlserver/), [RDS for Oracle](https://aws.amazon.com/rds/oracle/), or [RDS for Db2](https://aws.amazon.com/rds/db2/) database. This means that the code, applications, and tools you already use today with your existing databases should work seamlessly with Amazon RDS. Amazon RDS can automatically back up your database and keep your database software up to date with the latest version. You benefit from the flexibility of being able to scale the compute resources or storage capacity associated with your relational database instance. In addition, Amazon RDS makes it easy to use replication to enhance database availability, improve data durability, or scale beyond the capacity constraints of a single database instance for read-heavy database workloads. As with all AWS services, there are no upfront investments required, and you pay only for the resources you use.

### When Would I Use Amazon RDS vs. Amazon EC2 Relational Database AMIs?

Amazon Web Services provides a number of database alternatives for developers. Amazon RDS enables you to run a fully managed and fully featured relational database while offloading database administration. Using one of our many relational database AMIs on [Amazon EC2](https://aws.amazon.com/ec2/) allows you to manage your own relational database in the cloud. There are important differences between these alternatives that may make one more appropriate for your use case. See [Cloud Databases with AWS](https://aws.amazon.com/running_databases/) for guidance on which solution is best for you.

### Are there Hybrid or On-premises Deployment Options for Amazon RDS?

Yes, you can run Amazon RDS on premises using Amazon RDS on Outposts. Please see the [Amazon RDS on Outposts FAQs](https://aws.amazon.com/rds/outposts/faqs/) for additional information.

### Can I Get Help to Learn More about and Onboard to Amazon RDS?

Yes, Amazon RDS specialists are available to answer questions and provide support. [Contact Us](https://aws.amazon.com/contact-us/sales-support-rds/) and you’ll hear back from us in one business day to discuss how AWS can help your organization.

### How Do I Set up a Connection between an Application or a SQL Based Client Running on an Amazon EC2 Compute Instance and My Amazon RDS Database instance/cluster?

You can set up a connection between an EC2 compute instance and a new Amazon RDS database using the Amazon RDS console. On the “Create database” page, select “Connect to an EC2 compute resource” option in the Connectivity Section. When you select this option, Amazon RDS automates the manual networking set up tasks such as creating a VPC, security groups, subnets, and ingress/egress rules to establish a connection between your application and database.

Additionally, you can set up a connection between an existing Amazon RDS database and an EC2 compute instance. To do so, open the RDS console, select an RDS database from the database list page, and choose “Set up EC2 connection” from the "Action" menu dropdown list. Amazon RDS automatically sets up your related network settings to enable a secure connection between the selected EC2 instance and the RDS database.

This connectivity automation improves productivity for new users and application developers. Users can now quickly and seamlessly connect an application or a client using SQL on an EC2 compute instance to an RDS database within minutes.

### How Do I Set up a Connection between a Serverless Lambda Application and My Amazon RDS or Amazon Aurora Database Instance and/or Cluster?

You can set up a connection between an AWS Lambda function and an Amazon RDS or Amazon Aurora database from the Amazon RDS console. On the RDS console, select an RDS or Aurora database from the database list page, and choose “Set up Lambda connection” from the "Action" menu. Amazon RDS automatically sets up your related network settings to enable a secure connection between the selected Lambda function and the RDS or Aurora database.

We recommend that you use RDS Proxy during this connection set up. You can set up this connection either by using an existing RDS Proxy or using a new RDS Proxy that you can auto create during the connection. This connectivity set up automation can improve productivity for new users and application developers. Users can now quickly and seamlessly connect a serverless application or Lambda function to an RDS or Aurora database within minutes.

## Database Instances

### What is a Database Instance (DB instance)?

You can think of a [DB instance](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Overview.DBInstance.html) as a database environment in the cloud with the compute and storage resources you specify. You can create and delete DB instances, define/refine infrastructure attributes of your DB instance(s), and control access and security via the [AWS Management Console](https://console.aws.amazon.com/), [Amazon RDS APIs](https://docs.aws.amazon.com/AmazonRDS/latest/APIReference/Welcome.html), and [AWS Command Line Interface](http://docs.aws.amazon.com/cli/latest/reference/rds/index.html). You can run one or more DB instances and each DB instance can support one or more databases or database schemas, depending on engine type.

### How Do I Create a DB Instance?

DB instances are simple to create using either the AWS Management Console, Amazon RDS APIs, or AWS Command Line Interface. To launch a DB instance using the AWS Management Console, click "RDS" and then the “Launch DB Instance” button on the Instances tab. From there, you can specify the parameters for your DB instance, including DB engine and version, license model, instance type, storage type and amount, and primary user credentials.

You also have the ability to change your DB instance’s backup retention policy, preferred backup window, and scheduled maintenance window. Alternatively, you can create your DB instance using the [CreateDBInstance API](https://docs.aws.amazon.com/AmazonRDS/latest/APIReference/API_CreateDBInstance.html) or [create-db-instance command](http://docs.aws.amazon.com/cli/latest/reference/rds/create-db-instance.html).

### How Do I Access My Running DB Instance?

Once your DB instance is available, you can retrieve its endpoint via the DB instance description in the AWS Management Console, [DescribeDBInstances API](https://docs.aws.amazon.com/AmazonRDS/latest/APIReference/API_DescribeDBInstances.html) or [describe-db-instances command](http://docs.aws.amazon.com/cli/latest/reference/rds/describe-db-instances.html). Using this endpoint, you can construct the connection string required to connect directly with your DB instance using your favorite database tool or programming language. In order to allow network requests to your running DB instance, you will need to authorize access. For a detailed explanation of how to construct your connection string and get started, please refer to our [Getting Started Guide](http://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/CHAP_GettingStarted.html).

### How Many DB Instances Can I Run with Amazon RDS?

By default, customers are allowed to have up to a total of 40 Amazon RDS DB instances. Of those 40, up to 10 can be RDS for Oracle or RDS for SQL Server DB instances under the "License Included" model. All 40 can be used for Amazon Aurora, RDS for PostgreSQL, RDS for MySQL, RDS for MariaDB, and RDS for Oracle under the Bring Your Own Licence (BYOL) model. Note that RDS for SQL Server has a limit of up to 100 databases on a single DB instance. To learn more, see the [Amazon RDS for SQL Server User Guide](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/CHAP_SQLServer.html#SQLServer.Concepts.General.FeatureSupport.Limits).

### How Many Databases or Schemas Can I Run within a DB Instance?

- RDS for Amazon Aurora: No limit imposed by software
- RDS for MySQL: No limit imposed by software
- RDS for MariaDB: No limit imposed by software
- RDS for Oracle: 1 database per instance; no limit on the number of schemas per database imposed by software
- RDS for SQL Server: Up to 100 databases per instance
- RDS for PostgreSQL: No limit imposed by software
- RDS for Db2: Up to 8 databases per instance

### How Do I Import Data into an Amazon RDS DB Instance?

The following are a number of ways to import data into Amazon RDS:

- MySQL: [mysqldump](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/MySQL.Procedural.Importing.SmallExisting.html) or [mysqlimport](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/MySQL.Procedural.Importing.AnySource.html) utilities
- Oracle: [Data Pump](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Oracle.Procedural.Importing.DataPump.html), [import/export](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Oracle.Procedural.Importing.ExportImport.html), or [SQL Loader](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Oracle.Procedural.Importing.SQLLoader.html)
- SQL Server: [Import/Export Wizard](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/SQLServer.Procedural.Importing.Snapshots.html), full backup files (.bak), or Bulk Copy Program (BCP)
- PostgreSQL: [pg\_dump](https://docs.aws.amazon.com/dms/latest/sql-server-to-aurora-postgresql-migration-playbook/chap-sql-server-aurora-pg.management.exportimport.html)

For more information on data import and export, refer to the [Data Import Guide for MySQL](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/MySQL.Procedural.Importing.html), the [Data Import Guide for Oracle](http://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Oracle.Procedural.Importing.html), the [Data Import Guide for SQL Server](http://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/SQLServer.Procedural.Importing.html), the [Data Import Guide for PostgreSQL](http://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/PostgreSQL.Procedural.Importing.html), or the [Data Import Guide for Db2](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/db2-native-db2-tools.html).

In addition, [AWS Database Migration Service](https://aws.amazon.com/dms/) can help you securely migrate databases to AWS.

### What is a Maintenance Window? Will My DB Instance Be Available during Maintenance Events?

The [Amazon RDS maintenance window](https://aws.amazon.com/premiumsupport/knowledge-center/rds-maintenance-window/) is your opportunity to control when DB instance modifications, database engine version upgrades, and software patching occurs, in the event they are requested or required. If a maintenance event is scheduled for a given week, it will be initiated during the maintenance window you identify.

Maintenance events that require Amazon RDS to take your DB instance offline are scale compute operations (which generally take only a few minutes from start-to-finish), database engine version upgrades, and required software patching. Required software patching is automatically scheduled only for patches that are security and durability related. Such patching occurs infrequently (typically once every few months) and should seldom require more than a fraction of your maintenance window.

If you do not specify a preferred weekly maintenance window when [creating your DB instance](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_CreateDBInstance.html), a 30-minute default value is assigned. If you wish to modify when maintenance is performed on your behalf, you can do so by modifying your DB instance in the AWS Management Console, the [ModifyDBInstance API](https://docs.aws.amazon.com/AmazonRDS/latest/APIReference/API_ModifyDBInstance.html), or the [modify-db-instance command](http://docs.aws.amazon.com/cli/latest/reference/rds/modify-db-instance.html). Each of your DB instances can have different preferred maintenance windows, if you so choose.

Running your DB instance as a Multi-AZ deployment can further reduce the impact of a maintenance event. Please refer to the [Amazon RDS User Guide](http://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_UpgradeDBInstance.Maintenance.html) for more information on maintenance operations.

### What Should I Do if My Queries Seem to Be Running Slowly?

For production databases, we encourage you to enable [Enhanced Monitoring](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_Monitoring.OS.overview.html), which provides access to over 50 CPU, memory, file system, and disk I/O metrics. You can enable these features on a per-instance basis and you can choose the granularity (all the way down to 1 second). High levels of CPU utilization can reduce query performance and in this case, you may want to consider scaling your DB instance class. For more information on monitoring your DB instance, refer to the [Amazon RDS User Guide](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/CHAP_Monitoring.html).

If you are using RDS for MySQL or MariaDB, you can [access the slow query logs for your database](https://aws.amazon.com/premiumsupport/knowledge-center/rds-mysql-slow-query/) to determine if there are slow-running SQL queries and, if so, the performance characteristics of each. You could set the "slow\_query\_log" DB Parameter and query the mysql.slow\_log table to review the slow-running SQL queries. Please refer to the [Amazon RDS User Guide](http://docs.amazonwebservices.com/AmazonRDS/latest/UserGuide/Appendix.MySQL.CommonDBATasks.html) to learn more.

If you are using RDS for Oracle, you can use the Oracle trace file data to identify slow queries. For more information on accessing trace file data, please refer to [Amazon RDS User Guide](http://docs.amazonwebservices.com/AmazonRDS/latest/UserGuide/Appendix.Oracle.CommonDBATasks.html#Appendix.Oracle.CommonDBATasks.WorkingWithTracefiles). 

If you are using RDS for SQL Server, you can use the client side SQL Server traces to identify slow queries. For information on accessing server side trace file data, please refer to [Amazon RDS User Guide](http://docs.amazonwebservices.com/AmazonRDS/latest/UserGuide/Appendix.SQLServer.CommonDBATasks.html#Appendix.SQLServer.CommonDBATasks.WorkingWithTracefiles).

## Database Engine Versions

### Which Relational Database Engine Versions Does Amazon RDS Support?

For the list of supported database engine versions, please refer to the documentation for each engine:

- [Amazon Aurora](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Aurora.DatabaseEngineUpdates.html)
- [Amazon RDS for PostgreSQL](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/CHAP_PostgreSQL.html)
- [Amazon RDS for MySQL](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/CHAP_MySQL.html)
- [Amazon RDS for MariaDB](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/CHAP_MariaDB.html)
- [Amazon RDS for SQL Server](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/CHAP_SQLServer.html)
- [Amazon RDS for Oracle](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/CHAP_Oracle.html)
- [Amazon RDS for Db2](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/CHAP_Db2.html)

### How Does Amazon RDS Distinguish between “major” and “minor” DB Engine Versions?

Refer to the FAQs page for each Amazon RDS database engine for specifics on version numbering:

- [Amazon RDS for MySQL](https://aws.amazon.com/rds/mysql/faqs/)
- [Amazon RDS for MariaDB](https://aws.amazon.com/rds/mariadb/faqs/)
- [Amazon RDS for PostgreSQL](https://aws.amazon.com/rds/postgresql/faqs/)
- [Amazon RDS for Oracle](https://aws.amazon.com/rds/oracle/faqs/)
- [Amazon RDS for SQL Server](https://aws.amazon.com/rds/sqlserver/faqs/)
- [Amazon Aurora](https://aws.amazon.com/rds/aurora/faqs/)
- [Amazon RDS for Db2](https://aws.amazon.com/rds/db2/faqs/)

### Does Amazon RDS provide Guidelines for Support of New DB Engine Versions?

Over time, Amazon RDS adds support for [new major and minor database engine versions](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_UpgradeDBInstance.Upgrading.html). The number of new versions supported will vary based on the frequency and content of releases and patches from the engine’s vendor or development organization and the outcome of a thorough vetting of these releases and patches by our database engineering team. However, as a general guidance, we aim to support new engine versions within 5 months of their general availability.

### How Do I Specify Which Supported DB Engine Version I Would like My DB Instance to Run?

You can specify any currently supported version (major and minor) when creating a new DB instance via the Launch DB Instance operation in the AWS Management Console or the CreateDBInstance API. Please note that not every database engine version is available in every AWS region.

### How Do I Control if and when the Engine Version of My DB Instance is Upgraded to New Supported Versions?

Amazon RDS strives to keep your database instance up to date by providing you with newer versions of the supported database engines. After a new version of a database engine is released by the vendor or development organization, it is thoroughly tested by our database engineering team before it is made available in Amazon RDS.

We recommend that you [keep your database instance upgraded](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_UpgradeDBInstance.Upgrading.html) to the most current minor version as it will contain the latest security and functionality fixes. Unlike major version upgrades, minor version upgrades only include database changes that are backward-compatible with previous minor versions (of the same major version) of the database engine. 

If a new minor version does not contain fixes that would benefit Amazon RDS customers, we may choose not to make it available in Amazon RDS. Soon after a new minor version is available in Amazon RDS, we will set it to be the preferred minor version for new DB instances. 

To manually upgrade a database instance to a supported engine version, use the Modify DB Instance command on the AWS Management Console or the ModifyDBInstance API and set the DB Engine Version parameter to the desired version. By default, the upgrade will be applied during your next [maintenance window](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_UpgradeDBInstance.Maintenance.html#Concepts.DBMaintenance). You can also choose to upgrade immediately by selecting the Apply Immediately option in the console API.

If we determine that a new engine minor version contains significant bug fixes compared to a previously released minor version, we will schedule automatic upgrades for DB instances that have the Auto Minor Version Upgrade setting to “Yes”. These upgrades will be scheduled to occur during customer-specified maintenance windows.

We schedule them so you can plan around them because downtime is required to upgrade a DB engine version, even for Multi-AZ instances. If you wish to turn off automatic minor version upgrades you can do so by setting the Auto Minor Version Upgrade setting to “No”.

In the case of RDS for Oracle and RDS for SQL Server, if the upgrade to the next minor version requires a change to a different edition, then we may not schedule automatic upgrades even if you have enabled the Auto Minor Version Upgrade setting. The determination on whether to schedule automatic upgrades in such situations will be made on a case-by-case basis.

Since major version upgrades involve some compatibility risk, they will not occur automatically and must be initiated by you (except in the case of major version deprecation, see below). For more information about upgrading a DB instance to a new DB engine version, refer to the [Amazon RDS User Guide](http://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_UpgradeDBInstance.Upgrading.html).

### Can I Test My DB Instance with a New Version before Upgrading?

Yes. You can do so by creating a DB snapshot of your existing DB instance, restoring from the DB snapshot to create a new DB instance, and then initiating a version upgrade for the new DB instance. You can then experiment safely on the upgraded copy of your DB instance before deciding whether or not to upgrade your original DB instance.

For more information about restoring a DB snapshot, refer to the [Amazon RDS User Guide](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_RestoreFromSnapshot.html).

### Does Amazon RDS provide Guidelines for Deprecating Database Engine Versions that Are Currently Supported?

- We intend to support major version releases (e.g., MySQL 5.6, PostgreSQL 9.6) for at least 3 years after they are initially supported by Amazon RDS.
- We intend to support minor versions (e.g., MySQL 5.6.37, PostgreSQL 9.6.1) for at least 1 year after they are initially supported by Amazon RDS.

Periodically, we will deprecate major or minor engine versions. Major versions are made available at least until the community end of life for the corresponding community version or the version is no longer receiving software fixes or security updates. For minor versions, this is when a minor version has significant bugs or security issues that have been resolved in a later minor version.

While we strive to meet these guidelines, in some cases we may deprecate specific major or minor versions sooner, such as when there are security issues. In the unlikely event that such cases occur, Amazon RDS will automatically upgrade your database engine to address the issue. Specific circumstances may dictate different timelines depending on the issue being addressed.

### What Happens when an Amazon RDS DB Engine Version is Deprecated?

When a minor version of a database engine is deprecated in Amazon RDS, we will provide a three (3) month period after the announcement before beginning automatic upgrades. At the end of this period, all instances still running the deprecated minor version will be scheduled for automatic upgrade to the latest supported minor version during their scheduled maintenance windows.

When a major version of the database engine is deprecated in Amazon RDS, we will provide a minimum six (6) month period after the announcement of a deprecation for you to initiate an upgrade to a supported major version. At the end of this period, an automatic upgrade to the next major version will be applied to any instances still running the deprecated version during their scheduled maintenance windows.

### Why Can I not Create a Particular Version?

In some cases, we may deprecate specific major or minor versions without prior notice, such as when we discover a version does not meet our high quality, performance, or security bar. In the unlikely event that such cases occur, Amazon RDS will discontinue the creation of new database instances and clusters with these versions. Existing customers may continue to be able to run their databases. Specific circumstances may dictate different timelines depending on the issue being addressed.

## Billing

### How Will I Be Charged and Billed for My Use of Amazon RDS?

You pay only for what you use and there are no minimum or setup fees. You are billed based on:

- DB instance hours – Based on the class (e.g. db.t2.micro, db.m4.large) of the DB instance consumed. Partial DB instance hours consumed are billed in one-second increments with a 10 minute minimum charge following a billable status change, such as creating, starting, or modifying the DB instance class. For additional details, read our [what's new announcement](https://aws.amazon.com/about-aws/whats-new/2019/04/aws-rds-per-second-billing/).
- Storage (per GB per month) – [Storage capacity](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_PIOPS.StorageTypes.html) you have provisioned to your DB instance. If you scale your provisioned storage capacity within the month, your bill will be pro-rated.
- I/O requests per month – Total number of [storage I/O requests](https://aws.amazon.com/blogs/database/planning-i-o-in-amazon-aurora/) you have _(for Amazon RDS Magnetic Storage and Amazon Aurora only)_
- Provisioned IOPS per month – Provisioned IOPS rate, regardless of IOPS consumed _(for Amazon RDS Provisioned IOPS (SSD) Storage only)_
- Backup Storage – Backup storage is the storage associated with your automated database backups and any customer-initiated database snapshots. Increasing your backup retention period or taking additional database snapshots increases the backup storage consumed by your database.
- Data transfer – [Internet data transfer in and out of your DB instance](https://aws.amazon.com/blogs/architecture/overview-of-data-transfer-costs-for-common-architectures/).

For Amazon RDS pricing information, please visit the [pricing section on the Amazon RDS product page](https://aws.amazon.com/rds/pricing/).

### When Does Billing of My Amazon RDS DB Instances Begin and End?

Billing commences for a DB instance as soon as the DB instance is available. Billing continues until the DB instance terminates, which would occur upon deletion or in the event of an instance failure.

### What Defines Billable Amazon RDS Instance Hours?

[DB instance hours](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/User_DBInstanceBilling.html) are billed for each hour your DB instance is running in an available state. If you no longer wish to be charged for your DB instance, you must stop or delete it to avoid being billed for additional instance hours. Partial DB instance hours consumed are billed in one-second increments with a 10 minute minimum charge following a billable status change, such as creating, starting, or modifying the DB instance class.

### How Will I Be Billed for a Stopped DB Instance?

While your database instance is stopped, you are charged for provisioned storage (including Provisioned IOPS) and backup storage (including manual snapshots and automated backups within your specified retention window), but not for DB instance hours.

### How Will I Be Billed for Backups Storage?

Free backup storage is provided up to your account's total provisioned database storage across the entire region. For example, if you have a MySQL DB instance with 100 GB of provisioned storage over the month, and a PostgreSQL DB instance with 150 GB of provisioned storage over the month, both in the same region and same account, we will provide 250 GB of backup storage in this account and region at no additional charge. You will only be charged for backup storage that exceeds this amount.

Each day, your account's total provisioned database storage in the region is compared against your total backup storage in the region, and only the excess backup storage is charged. For example, if you have exactly 10 GB of excess backup storage each day, you will be charged for 10 GB-month of backup storage for the month. Alternatively, if you have 300 GB of provisioned storage each day, and 500 GB of backup storage each day, but only for half the month, then you will only be charged for 100 GB-month of backup storage (not 200 GB-month), since the charge is calculated daily (prorated), and the backups did not exist for the entire month. Please note that the free backup storage is account-specific and region-specific.

The size of your backups are directly proportional to the amount of data on your instance. For example, if you have a DB instance with 100 GB of provisioned storage, but only store 5 GB of data on it, your first backup will only be approximately 5 GB (not 100 GB). Subsequent backups are incremental, and will only store the changed data on your DB instance. Please note that the backup storage size is not displayed in RDS Console nor in the [DescribeDBSnapshots](https://docs.aws.amazon.com/AmazonRDS/latest/APIReference/API_DescribeDBSnapshots.html) API response.

### Why Does My Additional Backup Storage Cost More than the Allocated DB Instance Storage?

The storage provisioned to your DB instance for your primary data is located within a single Availability Zone. When your database is backed up, the backup data (including transactions logs) is geo-redundantly replicated across [multiple Availability Zones](https://docs.aws.amazon.com/whitepapers/latest/real-time-communication-on-aws/use-multiple-availability-zones.html) to provide even greater levels of data durability. The price for backup storage beyond your free allocation reflects this extra replication that occurs to maximize the durability of your critical backups.

### How Will I Be Billed for Multi-AZ DB Instance Deployments?

If you specify that your DB instance should be a Multi-AZ deployment, you will be billed according to the Multi-AZ pricing posted on the [Amazon RDS pricing page](https://aws.amazon.com/rds/pricing/). Multi-AZ billing is based on:

- Multi-AZ DB instance hours – Based on the class (e.g. db.t2.micro, db.m4.large) of the DB instance consumed. As with standard deployments in a single Availability Zone, Partial DB instance hours consumed are billed in one-second increments with a 10 minutes minimum charge following a billable status change, such as creating, starting, or modifying the DB instance class. If you convert your DB instance deployment between standard and Multi-AZ within a given hour, you will be charged both applicable rates for that hour.
- Provisioned storage (for Multi-AZ DB instance) – If you convert your deployment between standard and Multi-AZ within a given hour, you will be charged the higher of the applicable storage rates for that hour.
- I/O requests per month – Total number of storage I/O requests you have. Multi-AZ deployments consume a larger volume of I/O requests than standard DB instance deployments, depending on your database write/read ratio. Write I/O usage associated with database updates will double as Amazon RDS synchronously replicates your data to the standby DB instance. Read I/O usage will remain the same.
- Backup Storage – Your backup storage usage will not change whether your DB instance is a standard or Multi-AZ deployment. Backups will simply be taken from your standby to avoid I/O suspension on the DB instance primary.
- Data transfer – You are not charged for the data transfer incurred in replicating data between your primary and standby. Internet data transfer in and out of your DB instance is charged the same as with a standard deployment.

### Do Your Prices Include Taxes?

Except as otherwise noted, our prices are exclusive of applicable taxes and duties, including VAT and applicable sales tax. For customers with a Japanese billing address, the use of AWS services is subject to Japanese Consumption Tax. [Learn more](https://aws.amazon.com/c-tax-faqs/).

## Free Tier

Close all

### What Does the AWS Free Tier for Amazon RDS Offer?

The [AWS Free Tier for Amazon RDS](https://aws.amazon.com/rds/free/) offer provides free use of Single-AZ Micro DB instances running MySQL, MariaDB, PostgreSQL, and SQL Server Express Edition. The free usage tier is capped at 750 instance hours per month. Customers also receive 20 GB of General Purpose (SSD) database storage and 20 GB of backup storage for free per month.

### For what time Period Will the AWS Free Tier for Amazon RDS Be Available to Me?

New AWS accounts receive 12 months of AWS Free Tier access. Please see the [AWS Free Tier FAQs](https://aws.amazon.com/free/faqs/) for more information.

### Can I Run More than One DB Instance under the AWS Free Usage Tier for Amazon RDS?

Yes. You can run more than one Single-AZ Micro DB instance simultaneously and be eligible for usage counted under the AWS Free Tier for Amazon RDS. However, any use exceeding 750 instance hours, across all Amazon RDS Single-AZ Micro DB instances and across all eligible database engines and regions, will be billed at standard Amazon RDS prices.

For example, if you run two Single-AZ Micro DB instances for 400 hours each in a single month, you will accumulate 800 instance hours of usage, of which 750 hours will be free. You will be billed for the remaining 50 hours at the standard Amazon RDS price.

### Do I Have Access to 750 Instance Hours Each of the MySQL, MariaDB, PostgreSQL, and SQL Server Micro DB Instances under the AWS Free Tier?

No. A customer with access to the AWS Free Tier can use up to 750 instance hours of Micro instances running either MySQL, PostgreSQL, or SQL Server Express Edition. Any use exceeding 750 instance hours, across all Amazon RDS Single-AZ Micro DB instances and across all eligible database engines and regions, will be billed at standard Amazon RDS prices.

### How Am I Billed when My Instance-hour Usage Exceeds the Free Tier Benefit?

You are billed at standard Amazon RDS prices for instance hours beyond what the Free Tier provides. See the [Amazon RDS pricing page](https://aws.amazon.com/rds/pricing/) for details.

## Reserved Instances

Close all

### What is a Reserved Instance (RI)?

[Amazon RDS reserved instances](https://aws.amazon.com/rds/reserved-instances/) give you the option to reserve a DB instance for a one or three year term and in turn receive a significant discount compared to the on-demand instance pricing for the DB instance. There are three RI payment options -- No Upfront, Partial Upfront, All Upfront -- which enable you to balance the amount you pay upfront with your effective hourly price.

### How Are Reserved Instances Different from On-demand DB Instances?

Functionally, reserved instances and on-demand DB instances are exactly the same. The only difference is how your DB instance(s) are billed. With Reserved Instances, you purchase a oneor three-year reservation and in return receive a lower effective hourly usage rate (compared with on-demand DB instances) for the duration of the term. Unless you purchase reserved instances in a Region, all DB instances will be billed at on-demand hourly rates.

### How Do I Purchase and Create Reserved Instances?

You can purchase a reserved instance in the "Reserved Instance" section of the AWS Management Console for Amazon RDS. Alternatively, you can use the Amazon RDS API or AWS Command Line Interface to list the reservations available for purchase and then purchase a DB instance reservation.

Once you have made a reserved purchase, using a reserved DB instance is no different than an On-Demand DB instance. Launch a DB instance using the same instance class, engine, and region for which you made the reservation. As long as your reservation purchase is active, Amazon RDS will apply the reduced hourly rate for which you are eligible to the new DB instance.

### Do Reserved Instances Include a Capacity Reservation?

Amazon RDS reserved instances are purchased for a Region rather than for a specific Availability Zone. As RIs are not specific to an Availability Zone, they are not capacity reservations. This means that even if capacity is limited in one Availability Zone, reservations can still be purchased in the Region and the discount will apply to matching usage in any Availability Zone within that Region.

### How Many Reserved Instances Can I Purchase?

You can purchase up to 40 reserved DB instances. If you wish to run more than 40 DB instances, please complete the [Amazon RDS DB Instance request form](https://aws.amazon.com/contact-us/request-to-increase-the-amazon-rds-db-instance-limit/).

### What if I Have an Existing DB Instance that I’d like to Cover with a Reserved Instance?

Simply purchase a DB instance reservation with the same DB instance class, DB engine, Multi-AZ option, and License Model within the same Region as the DB instance you are currently running and would like to reserve. If the reservation purchase is successful, Amazon RDS will automatically apply your new hourly usage charge to your existing DB instance.

### If I Sign up for a Reserved Instance, when Does the Term Begin? What Happens to My DB Instance when the Term Ends?

Pricing changes associated with a reserved instance are activated once your request is received while the payment authorization is processed. You can follow the status of your reservation on the AWS Account Activity page or by using the DescribeReservedDBInstances API or describe-reserved-db-instances command. If the one-time payment cannot be successfully authorized by the next billing period, the discounted price will not take effect.

When your reservation term expires, your reserved instance will revert to the appropriate On-Demand hourly usage rate for your DB instance class and Region.

### How Do I Control Which DB Instances Are Billed at the Reserved Instance Rate?

The Amazon RDS operations for creating, modifying, and deleting DB instances do not distinguish between on-demand and reserved instances. When computing your bill, our system will automatically apply your Reservation(s) such that all eligible DB instances are charged at the lower hourly reserved DB instance rate.

### If I Scale My DB Instance Class up or Down, what Happens to My Reservation?

Each reservation is associated with the following set of attributes: DB engine, DB instance class, Multi-AZ deployment option, license model, and Region.

A reservation for a DB engine and license model that is eligible for size-flexibility (MySQL, MariaDB, PostgreSQL, Amazon Aurora, or Oracle "Bring Your Own License") will automatically apply to a running DB instance of any size within the same instance family (e.g. M4, T2, or R3) for the same database engine and Region. In addition, the reservation will also apply to DB instances running in either Single-AZ or Multi-AZ deployment options.

For example, let’s say you purchased a db.m4.2xlarge MySQL reservation. If you decide to scale up the running DB instance to a db.m4.4xlarge, the discounted rate of this RI will cover 1/2 of the usage of the larger DB instance.

If you are running a DB engine or license model that is not eligible for size-flexibility (Microsoft SQL Server or Oracle "License Included"), each reservation can only be applied to a DB instance with the same attributes for the duration of the term. If you decide to modify any of these attributes of your running DB instance before the end of the reservation term, your hourly usage rates for that DB instance will revert to on demand hourly rates.

For more details on about size flexibility, see the [Amazon RDS User Guide](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_WorkingWithReservedDBInstances.html#USER_WorkingWithReservedDBInstances.SizeFlexible).

### Can I Move a Reserved Instance from One Region or Availability Zone to Another?

Each reserved instance is associated with a specific Region, which is fixed for the lifetime of the reservation and cannot be changed. Each reservation can, however, be used in any of the available AZs within the associated Region.

### Are Reserved Instances Available for Multi-AZ Deployments?

Yes. When you purchase a reserved instance, you can select the Multi-AZ option in the DB instance configuration available for purchase. In addition, if you are using a DB engine and license model that supports reserved [instance size-flexibility](https://aws.amazon.com/premiumsupport/knowledge-center/ri-size-flexibility/), a Multi-AZ reserved instance will cover usage for two Single-AZ DB instances.

### Are Reserved Instances Available for Read Replicas?

A DB instance reservation can be applied to a [read replica](https://aws.amazon.com/rds/features/read-replicas/), provided the DB instance class and Region are the same. When computing your bill, our system will automatically apply your Reservation(s), such that all eligible DB instances are charged at the lower hourly reserved instance rate.

### Can I Cancel a Reservation?

No, you cannot cancel your reserved DB instance and the one-time payment (if applicable) is not refundable. You will continue to pay for every hour during your Reserved DB instance term regardless of your usage.

### How Do the Payment Options Impact My Bill?

When you purchase an RI under the All Upfront payment option, you pay for the entire term of the RI in one upfront payment. You can choose to pay nothing upfront by choosing the No Upfront option. The entire value of the No Upfront RI is spread across every hour in the term and you will be billed for every hour in the term, regardless of usage. The Partial Upfront payment option is a hybrid of the All Upfront and No Upfront options. You make a small upfront payment, and you are billed a low hourly rate for every hour in the term regardless of usage.

## Hardware and Scaling

Close all

### How Do I Determine Which Initial DB Instance Class and Storage Capacity Are Appropriate for My Needs?

In order to [select your initial DB instance class and storage capacity](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/CHAP_Tutorials.WebServerDB.CreateDBInstance.html), you will want to assess your application’s compute, memory, and storage needs. For information about the DB instance classes available, please refer to the [Amazon RDS User Guide](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Concepts.DBInstanceClass.html).

### How Do I Scale the Compute Resources and/or Storage Capacity Associated with My Amazon RDS Database Instance?

You can scale the compute resources and [storage capacity](https://aws.amazon.com/about-aws/whats-new/2019/06/rds-storage-auto-scaling/) allocated to your DB instance with the AWS Management Console (selecting the desired DB instance and clicking the Modify button), the Amazon RDS API, or the AWS Command Line Interface. Memory and CPU resources are modified by changing your DB Instance class, and storage available is changed when you modify your storage allocation. 

Please note that when you modify your DB Instance class or allocated storage, your requested changes will be applied during your specified maintenance window. Alternately, you can use the “apply-immediately” flag to apply your scaling requests immediately. Bear in mind that any other pending system changes will be applied as well.

Some older RDS for SQL Server instances may not be eligible for scaled storage. See the [RDS for SQL Server FAQ](https://aws.amazon.com/rds/sqlserver/faqs/) for more information.

### What is the Hardware Configuration for Amazon RDS Storage?

Amazon RDS uses EBS volumes for database and log storage. Depending on the size of storage requested, Amazon RDS automatically stripes across multiple EBS volumes to enhance IOPS performance. For MySQL and Oracle, for an existing DB instance, you may observe some I/O capacity improvement if you scale up your storage. You can scale the storage capacity allocated to your DB Instance using the AWS Management Console, the ModifyDBInstance API, or the modify-db-instance command.

For more information, see [Storage for Amazon RDS](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/CHAP_Storage.html).

### Will My DB Instance Remain Available during Scaling?

The storage capacity allocated to your DB Instance can be increased while maintaining DB Instance availability. However, when you decide to [scale the compute resources available to your DB instance up or down](https://aws.amazon.com/blogs/database/scaling-your-amazon-rds-instance-vertically-and-horizontally/), your database will be temporarily unavailable while the DB instance class is modified. This period of unavailability typically lasts only a few minutes, and will occur during the maintenance window for your DB Instance, unless you specify that the modification should be applied immediately.

### How Can I Scale My DB Instance beyond the Largest DB Instance Class and Maximum Storage Capacity?

Amazon RDS supports a variety of DB instance classes and storage allocations to meet different application needs. If your application requires more compute resources than the largest DB instance class or more storage than the maximum allocation, you can implement partitioning, thereby spreading your data across multiple DB instances.

### What is Amazon RDS General Purpose (SSD) Storage?

[Amazon RDS General Purpose (SSD) Storage](https://aws.amazon.com/blogs/aws/rds-with-ssd-storage/) is suitable for a broad range of database workloads that have moderate I/O requirements. With the baseline of 3 IOPS/GB and ability to burst up to 3,000 IOPS, this storage option provides predictable performance to meet the needs of most applications.

### What is Amazon RDS Provisioned IOPS (SSD) Storage?

[Amazon RDS Provisioned IOPS (SSD) Storage](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/CHAP_Storage.html#USER_PIOPS) is an SSD-backed storage option designed to deliver fast, predictable, and consistent I/O performance. With Amazon RDS Provisioned IOPS (SSD) Storage, you specify an IOPS rate when creating a DB instance, and Amazon RDS provisions that IOPS rate for the lifetime of the DB instance. Amazon RDS Provisioned IOPS (SSD) Storage is optimized for I/O-intensive, transactional (OLTP) database workloads. For more details, please see the [Amazon RDS User Guide](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/CHAP_Storage.html).

### What is Amazon RDS Magnetic Storage?

[Amazon RDS magnetic storage](https://aws.amazon.com/blogs/database/store-and-analyze-time-series-data-with-multi-measure-records-magnetic-storage-writes-and-scheduled-queries-in-amazon-timestream/) is useful for small database workloads where data is accessed less frequently. Magnetic storage is not recommended for production database instances.

### How Do I Choose among the Amazon RDS Storage Types?

Choose the storage type most suited for your workload.

- [High-performance OLTP workloads](https://aws.amazon.com/blogs/database/best-storage-practices-for-running-production-workloads-on-hosted-databases-with-amazon-rds-or-amazon-ec2/): Amazon RDS Provisioned IOPS (SSD) Storage
- Database workloads with moderate I/O requirements: Amazon RDS General Purpose (SSD) Storage

### What Are the Minimum and Maximum IOPS Supported by Amazon RDS?

The IOPS supported by Amazon RDS varies by database engine. For more details, please see the [Amazon RDS User Guide](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Welcome.html).

## Automatic Backups and Database Snapshots

Close all

### What is the Difference between Automated Backups and DB Snapshots?

Amazon RDS provides two different methods for backing up and restoring your DB instance(s) [automated backups](https://aws.amazon.com/rds/features/backup/) and [database snapshots](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_CreateSnapshot.html) (DB Snapshots).

The automated backup feature of Amazon RDS enables [point-in-time recovery](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_PIT.html) of your DB instance. When automated backups are turned on for your DB Instance, Amazon RDS automatically performs a full daily snapshot of your data (during your preferred backup window) and captures transaction logs (as updates to your DB Instance are made). When you initiate a point-in-time recovery, transaction logs are applied to the most appropriate daily backup in order to restore your DB instance to the specific time you requested. 

Amazon RDS retains backups of a DB Instance for a limited, user-specified period of time called the retention period, which by default is 7 days but can be set to up to 35 days. You can initiate a point-in-time restore and specify any second during your retention period, up to the Latest Restorable Time. You can use the [DescribeDBInstances](https://docs.aws.amazon.com/AmazonRDS/latest/APIReference/API_DescribeDBInstances.html) API to return the latest restorable time for you DB instance, which is typically within the last five minutes. 

Alternatively, you can find the Latest Restorable Time for a DB instance by selecting it in the AWS Management Console and looking in the “Description” tab in the lower panel of the Console.

DB Snapshots are user-initiated and enable you to back up your DB instance in a known state as frequently as you wish, and then restore to that specific state at any time. DB Snapshots can be created with the AWS Management Console, CreateDBSnapshot API, or create-db-snapshot command and are kept until you explicitly delete them.

The snapshots which Amazon RDS performs for enabling automated backups are available to you for copying (using the AWS console or the [copy-db-snapshot command](http://docs.aws.amazon.com/cli/latest/reference/rds/copy-db-snapshot.html)) or for the snapshot restore functionality. You can identify them using the "automated" Snapshot Type. In addition, you can identify the time at which the snapshot has been taken by viewing the "Snapshot Created Time" field. 

Alternatively, the identifier of the "automated" snapshots also contains the time (in UTC) at which the snapshot has been taken.

Please note: When you perform a restore operation to a point in time or from a DB Snapshot, a new DB Instance is created with a new endpoint (the old DB Instance can be deleted if so desired). This is done to enable you to create multiple DB Instances from a specific DB Snapshot or point in time.

### Do I Need to Enable Backups for My DB Instance or is it Done Automatically?

By default, Amazon RDS enables automated backups of your DB instance with a 7-day retention period. If you would like to modify your backup retention period, you can do so using the RDS Console, the [CreateDBInstance](https://docs.aws.amazon.com/AmazonRDS/latest/APIReference/API_CreateDBInstance.html) API (when creating a new DB Instance), or the [ModifyDBInstance](https://docs.aws.amazon.com/AmazonRDS/latest/APIReference/API_ModifyDBInstance.html) API (for existing instances). You can use these methods to [change the RetentionPeriod parameter](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_WorkingWithAutomatedBackups.html#USER_WorkingWithAutomatedBackups.BackupRetention) to any number from 0 (which will disable automated backups) to the desired number of days, up to 35. The value cannot be set to 0 if the DB instance is a source to Read Replicas. For more information on automated backups, please refer to the [Amazon RDS User Guide](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/CHAP_CommonTasks.BackupRestore.html).

### What is a Backup Window and why Do I Need It? Is My Database Available during the Backup Window?

The preferred backup window is the user-defined period of time during which your DB Instance is backed up. Amazon RDS uses these periodic data backups in conjunction with your transaction logs to enable you to restore your DB Instance to any second during your retention period, up to the LatestRestorableTime (typically up to the last few minutes). During the backup window, storage I/O may be briefly suspended while the backup process initializes (typically under a few seconds) and you may experience a brief period of elevated latency. There is no I/O suspension for Multi-AZ DB deployments, since the backup is taken from the standby.

### Where Are My Automated Backups and DB Snapshots Stored and how Do I Manage Their Retention?

Amazon RDS DB snapshots and automated backups are stored in [S3](https://aws.amazon.com/s3/).

You can use the AWS Management Console, the ModifyDBInstance API, or the modify-db-instance command to manage the period of time your automated backups are retained by modifying the RetentionPeriod parameter. If you desire to turn off automated backups altogether, you can do so by setting the retention period to 0 (not recommended). You can manage your user-created DB Snapshots via the "Snapshots" section of the Amazon RDS Console. Alternatively, you can see a list of the user-created DB Snapshots for a given DB Instance using the DescribeDBSnapshots API or describe-db-snapshots command and delete snapshots with the [DeleteDBSnapshot API](https://docs.aws.amazon.com/AmazonRDS/latest/APIReference/API_DeleteDBSnapshot.html) or [delete-db-snapshot command](http://docs.aws.amazon.com/cli/latest/reference/rds/delete-db-snapshot.html).

### Why Do I Have More Automated DB Snapshots than the Number of Days in the Retention Period for My DB Instance?

It is normal to have 1 or 2 more automated DB snapshots than the number of days in your retention period. One extra automated snapshot is retained to ensure the ability to perform a point in time restore to any time during the retention period.

For example, if your backup window is set to 1 day, you will require 2 automated snapshots to support restores to any within the previous 24 hours. You may also see an additional automated snapshot as a new automated snapshot is always created before the oldest automated snapshot is deleted.

### What Happens to My Backups and DB Snapshots if I Delete My DB Instance?

When you delete a DB instance, you can create a final DB snapshot upon deletion; if you do, you can use this DB snapshot to restore the deleted DB instance at a later date. Amazon RDS retains this final user-created DB snapshot along with all other manually created DB snapshots after the DB instance is deleted. Refer to the [pricing page](https://aws.amazon.com/rds/pricing/) for details of backup storage costs.

Automated backups are deleted when the DB instance is deleted. Only manually created DB Snapshots are retained after the DB Instance is deleted.

## Security

Close all

### What is Amazon Virtual Private Cloud (VPC) and how Does it Work with Amazon RDS?

Amazon VPC lets you create a virtual networking environment in a private, isolated section of the [AWS cloud](https://aws.amazon.com/what-is-cloud-computing/) where you can exercise complete control over aspects, such as private IP address ranges, subnets, routing tables, and network gateways. With Amazon VPC, you can define a virtual network topology and customize the network configuration to closely resemble a traditional IP network that you might operate in your own data center.

One way that you can take advantage of VPC is when you want to run a public-facing web application while still maintaining non-publicly accessible backend servers in a private subnet. You can create a public-facing subnet for your webservers that has access to the Internet, and place your backend Amazon RDS DB Instances in a private-facing subnet with no Internet access. For more information about Amazon VPC, refer to the [Amazon Virtual Private Cloud User Guide](https://docs.aws.amazon.com/vpc/latest/userguide/what-is-amazon-vpc.html).

### How is Using Amazon RDS inside a VPC Different from Using it on the EC2-Classic Platform (non-VPC)?

If your AWS account was created before 2013-12-04, you may be able to run Amazon RDS in an Amazon Elastic Compute Cloud (EC2)-Classic environment. The basic functionality of Amazon RDS is the same regardless of whether EC2-Classic or EC2-VPC is used. Amazon RDS manages backups, software patching, automatic failure detection, read replicas, and recovery whether your DB Instances are deployed inside or outside a VPC. For more information about the differences between EC2-Classic and EC2-VPC, see the [EC2 documentation](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-vpc.html#differences).

### What is a DB Subnet Group and why Do I Need One?

A [DB Subnet Group](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_VPC.WorkingWithRDSInstanceinaVPC.html#USER_VPC.Subnets) is a collection of subnets that you may want to designate for your Amazon RDS DB Instances in a VPC. Each DB Subnet Group should have at least one subnet for every Availability Zone in a given Region. When creating a DB Instance in VPC, you will need to select a DB Subnet Group. Amazon RDS then uses that DB Subnet Group and your preferred Availability Zone to select a subnet and an IP address within that subnet. Amazon RDS creates and associates an Elastic Network Interface to your DB Instance with that IP address.

Please note that we strongly recommend you use the [DNS Name](https://aws.amazon.com/route53/what-is-dns/) to connect to your DB Instance as the underlying IP address can change (e.g., during failover).

For Multi-AZ deployments, defining a subnet for all Availability Zones in a Region will allow Amazon RDS to create a new standby in another Availability Zone should the need arise. You need to do this even for Single-AZ deployments, just in case you want to convert them to Multi-AZ deployments at some point.

### How Do I Create an Amazon RDS DB Instance in VPC?

For a procedure that walks you through this process, refer to [Creating a DB Instance in a VPC](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_VPC.WorkingWithRDSInstanceinaVPC.html#USER_VPC.InstanceInVPC) in the Amazon RDS User Guide.

### How Do I Control Network Access to My DB Instance(s)?

Visit the [Security Groups](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Overview.RDSSecurityGroups.html) section of the Amazon RDS User Guide to learn about the different ways to control access to your DB Instances.

### How Do I Connect to an Amazon RDS DB Instance in VPC?

DB Instances deployed within a VPC can be accessed by EC2 Instances deployed in the same VPC. If these EC2 Instances are deployed in a public subnet with associated Elastic IPs, you can access the EC2 Instances via the internet. DB Instances deployed within a VPC can be accessed from the Internet or from EC2 Instances outside the VPC via [VPN](https://aws.amazon.com/vpn/) or [bastion hosts](https://aws.amazon.com/premiumsupport/knowledge-center/rds-connect-using-bastion-host-linux/) that you can launch in your public subnet or using Amazon RDS's Publicly Accessible option:

- To use a bastion host, you will need to set up a public subnet with an EC2 instance that acts as a [SSH Bastion](https://aws.amazon.com/blogs/security/securely-connect-to-linux-instances-running-in-a-private-amazon-vpc/). This public subnet must have an internet gateway and routing rules that allow traffic to be directed via the SSH host, which must then forward requests to the private IP address of your Amazon RDS DB instance.
- To use public connectivity, simply create your DB Instances with the Publicly Accessible option set to yes. With Publicly Accessible active, your DB Instances within a VPC will be fully accessible outside your VPC by default. This means you do not need to configure a VPN or bastion host to allow access to your instances.

You can also set up a VPN Gateway that extends your corporate network into your VPC and allows access to the Amazon RDS DB instance in that VPC. Refer to the [Amazon VPC User Guide](https://docs.aws.amazon.com/vpc/latest/userguide/what-is-amazon-vpc.html) for more details.

We strongly recommend you use the DNS Name to connect to your DB Instance as the underlying IP address can change (e.g., during failover).

### Can I Move My Existing DB Instances outside VPC into My VPC?

If your DB instance is not in a VPC, you can use the AWS Management Console to easily move your DB instance into a VPC. See the [Amazon RDS User Guide](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_VPC.WorkingWithRDSInstanceinaVPC.html#USER_VPC.Non-VPC2VPC) for more details. You can also take a snapshot of your DB Instance outside VPC and restore it to VPC by specifying the DB Subnet Group you want to use. Alternatively, you can perform a “Restore to Point in Time” operation as well.

### Can I Move My Existing DB Instances from inside VPC to outside VPC?

[Migration of DB Instances](https://docs.aws.amazon.com/prescriptive-guidance/latest/patterns/migrate-an-amazon-rds-db-instance-to-another-vpc-or-account.html) from inside to outside VPC is not supported. For security reasons, a DB Snapshot of a DB Instance inside VPC cannot be restored to outside VPC. The same is true with “Restore to Point in Time” functionality. 

### What Precautions Should I Take to Ensure that My DB Instances in VPC Are Accessible by My Application?

You are responsible for [modifying routing tables](https://docs.aws.amazon.com/vpc/latest/userguide/WorkWithRouteTables.html) and [networking ACLs](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-network-acls.html) in your VPC to ensure that your DB instance is reachable from your client instances in the VPC. For Multi-AZ deployments, after failover, your client EC2 instance and Amazon RDS DB Instance may be in different Availability Zones. You should [configure your networking ACLs](https://aws.amazon.com/premiumsupport/knowledge-center/security-network-acl-vpc-endpoint/) to ensure that cross-AZ communication is possible.

### Can I Change the DB Subnet Group of My DB Instance?

An existing DB Subnet Group can be updated to add more subnets, either for existing Availability Zones or for new Availability Zones added since the creation of the DB Instance. [Removing subnets from an existing DB Subnet Group](https://aws.amazon.com/premiumsupport/knowledge-center/rds-db-subnet-group/) can cause unavailability for instances if they are running in a particular AZ that gets removed from the subnet group. View the [Amazon RDS User Guide](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_VPC.WorkingWithRDSInstanceinaVPC.html#USER_VPC.VPC2VPC) for more information.

### What is an Amazon RDS Primary User account and how is it Different from an AWS Account?

To begin using Amazon RDS you will need an AWS developer account. If you do not have one prior to signing up for Amazon RDS, you will be prompted to create one when you begin the sign-up process. A primary user account is different from an AWS developer account and used only within the context of Amazon RDS to control access to your DB Instance(s). The primary user account is a native database user account that you can use to connect to your DB Instance. 

You can specify the primary user name and password you want associated with each DB Instance when you create the DB Instance. Once you have created your DB Instance, you can connect to the database using the primary user credentials. Subsequently, you may also want to create additional user accounts so that you can restrict who can access your DB Instance.

### What Privileges Are granted to the Primary User for My DB Instance?

For MySQL, the default privileges for the primary user include: create, drop, references, event, alter, delete, index, insert, select, update, create temporary tables, lock tables, trigger, create view, show view, alter routine, create routine, execute, trigger, create user, process, show databases, grant option.

For Oracle, the primary user is granted the "dba" role. The primary user inherits most of the privileges associated with the role. Please refer to the [Amazon RDS User Guide](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/UsingWithRDS.MasterAccounts.html) for the list of restricted privileges and the corresponding alternatives to perform administrative tasks that may require these privileges.

For SQL Server, a user that creates a database is granted the "db\_owner" role. Please refer to the [Amazon RDS User Guide](https://docs.amazonwebservices.com/AmazonRDS/latest/UserGuide/RDSFAQ.SQLServer.html) for the list of restricted privileges and the corresponding alternatives to perform administrative tasks that may require these privileges.

### Is there Anything Different about User Management with Amazon RDS?

No, everything works the way you are familiar with when using a relational database you manage yourself.

### Can Programs Running on Servers in My Own Data Center Access Amazon RDS Databases?

Yes. You have to intentionally turn on the ability to access your database over the internet by configuring [Security Groups](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Overview.RDSSecurityGroups.html). You can authorize access for only the specific IPs, IP ranges, or subnets corresponding to servers in your own data center.

### Can I Encrypt Connections between My Application and My DB Instance Using SSL/TLS?

Yes, this option is supported for all Amazon RDS engines. Amazon RDS [generates an SSL/TLS certificate for each DB Instance](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/UsingWithRDS.SSL.html). Once an encrypted connection is established, data transferred between the DB Instance and your application will be encrypted during transfer.

While SSL offers security benefits, be aware that SSL/TLS encryption is a compute-intensive operation and will increase the latency of your database connection. SSL/TLS support within Amazon RDS is for encrypting the connection between your application and your DB Instance; it should not be relied on for authenticating the DB Instance itself.

For details on establishing an encrypted connection with Amazon RDS, please visit Amazon RDS's [MySQL User Guide](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/CHAP_MySQL.html#MySQL.Concepts.SSLSupport), [MariaDB User Guide](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/CHAP_MariaDB.html#MariaDB.Concepts.SSLSupport), [PostgreSQL User Guide](http://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/CHAP_PostgreSQL.html#PostgreSQL.Concepts.General.SSL), or [Oracle User Guide](http://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/CHAP_Oracle.html#Oracle.Concepts.SSL). To learn more about how SSL/TLS works with these engines, you can refer directly to the [MySQL documentation](https://dev.mysql.com/doc/refman/8.0/en/encrypted-connections.html), the [MariaDB documentation](https://mariadb.com/kb/en/mariadb/secure-connections-overview/), the [MSDN SQL Server documentation](http://msdn.microsoft.com/en-us/library/ms189067.aspx), the [PostgreSQL documentation](http://www.postgresql.org/docs/9.5/static/ssl-tcp.html), or the [Oracle Documentation](https://docs.oracle.com/database/121/DBSEG/asossl.htm).

### Can I Encrypt Data at Rest on My Amazon RDS Databases?

Amazon RDS supports encryption at rest for all database engines, using keys you manage using [AWS Key Management Service (KMS)](https://aws.amazon.com/kms/). On a database instance running with Amazon RDS encryption, data stored at rest in the underlying storage is encrypted, as are its automated backups, read replicas, and snapshots. Encryption and decryption are handled transparently. For more information about the use of KMS with Amazon RDS, see the [Amazon RDS User's Guide](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Overview.Encryption.html).

You can also add encryption to a previously unencrypted DB instance or DB cluster by creating a DB snapshot and then creating a copy of that snapshot and specifying a KMS encryption key. You can then restore an encrypted DB instance or DB cluster from the encrypted snapshot.

Amazon RDS for Oracle and SQL Server support those engines' [Transparent Data Encryption (TDE)](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Appendix.SQLServer.Options.TDE.html) technologies. For more information, see the Amazon RDS User's Guide for [Oracle](http://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Appendix.Oracle.Options.html#Appendix.Oracle.Options.AdvSecurity) and [SQL Server](http://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Appendix.SQLServer.Options.html#Appendix.SQLServer.Options.TDE).

### How Do I Control the Actions that My Systems and Users Can Take on Specific Amazon RDS Resources?

You can control the actions that your [AWS IAM](https://aws.amazon.com/iam/) users and groups can take on Amazon RDS resources. You do this by referencing the Amazon RDS resources in the [AWS IAM policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/PermissionsAndPolicies.html) that you apply to your users and groups. Amazon RDS resources that can be referenced in an AWS IAM policy include DB instances, DB snapshots, read replicas, DB security groups, DB option groups, DB parameter groups, event subscriptions, and DB subnet groups. 

In addition, you can tag these resources to add additional metadata to your resources. By using tagging, you can categorize your resources (e.g. "Development" DB instances, "Production" DB instances, and "Test" DB instances), and write AWS IAM policies that list the permissions (i.e. actions) that can be taken on resources with the same tags. For more information, refer to [Tagging Amazon RDS Resources](http://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_Tagging.html).

### I Wish to Perform Security Analysis or Operational Troubleshooting on My Amazon RDS Deployment. Can I Get a History of All Amazon RDS API Calls Made on My Account?

Yes. [AWS CloudTrail](https://aws.amazon.com/cloudtrail/features/) is a web service that records AWS API calls for your account and delivers log files to you. The AWS API call history produced by CloudTrail enables security analysis, resource change tracking, and compliance auditing. 

### Can I Use Amazon RDS with Applications that Require HIPAA Compliance?

Yes, all Amazon RDS database engines are [HIPAA-eligible](https://aws.amazon.com/compliance/hipaa-compliance/), so you can use them to build HIPAA-compliant applications and store healthcare-related information, including protected health information (PHI) under an executed Business Associate Agreement (BAA) with AWS.

If you already have an executed BAA, no action is necessary to begin using these services in the account(s) covered by your BAA. If you do not have an executed BAA with AWS, or have any other questions about HIPAA-compliant applications on AWS, please contact your account manager.

## Database Configuration

Close all

### How Do I Choose the Right Configuration Parameters for My DB Instance(s)?

By default, Amazon RDS chooses the optimal configuration parameters for your DB Instance taking into account the instance class and storage capacity. However, if you want to change them, you can do so using the AWS Management Console, the Amazon RDS APIs, or the AWS Command Line Interface. Please note that [changing configuration parameters](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Overview.DBInstance.Modifying.html) from recommended values can have unintended effects, ranging from degraded performance to system crashes, and should only be attempted by advanced users who wish to assume these risks.

### What Are DB Parameter Groups? How Are They Helpful?

A database parameter group (DB Parameter Group) acts as a “container” for engine configuration values that can be applied to one or more DB Instances. If you create a DB Instance without specifying a DB Parameter Group, a default DB Parameter Group is used. This default group contains engine defaults and Amazon RDS system defaults optimized for the DB Instance you are running.

However, if you want your DB Instance to run with your custom-specified engine configuration values, you can simply create a new DB Parameter Group, modify the desired parameters, and modify the DB Instance to use the new DB Parameter Group. Once associated, all DB Instances that use a particular DB Parameter Group get all the parameter updates to that DB Parameter Group.

For more information on configuring DB Parameter Groups, please read the [Amazon RDS User Guide](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_WorkingWithParamGroups.html).

### How Can I Monitor the Configuration of My Amazon RDS Resources?

You can use [AWS Config](https://aws.amazon.com/config/) to continuously record configuration changes to Amazon RDS DB Instances, DB Subnet Groups, DB Snapshots, DB Security Groups, and Event Subscriptions and receive notification of changes through [Amazon Simple Notification Service (SNS)](https://aws.amazon.com/sns/). You can also [create AWS Config Rules](https://docs.aws.amazon.com/config/latest/developerguide/evaluate-config_develop-rules.html) to evaluate whether these Amazon RDS resources have the desired configurations.

## Multi-AZ Deployments

Close all

### What Does it Mean to Run a DB Instance as a Multi-AZ Deployment?

When you create or modify your DB instance to run as a [Multi-AZ deployment](https://aws.amazon.com/rds/features/multi-az/), Amazon RDS automatically provisions and maintains a synchronous “standby” replica in a different Availability Zone. Updates to your DB Instance are synchronously replicated across Availability Zones to the standby in order to keep both in sync and protect your latest database updates against DB instance failure. 

During certain types of planned maintenance, or in the unlikely event of DB instance failure or Availability Zone failure, Amazon RDS will automatically failover to the standby so that you can resume database writes and reads as soon as the standby is promoted. Since the name record for your DB instance remains the same, your application can resume database operation without the need for manual administrative intervention. With Multi-AZ deployments, replication is transparent. You do not interact directly with the standby, and it cannot be used to serve read traffic. More information about Multi-AZ deployments is in the [Amazon RDS User Guide](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Concepts.MultiAZ.html).

### What is an Availability Zone?

[Availability Zones](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Concepts.RegionsAndAvailabilityZones.html) are distinct locations within a Region that are engineered to be isolated from failures in other Availability Zones. Each Availability Zone runs on its own physically distinct, independent infrastructure, and is engineered to be highly reliable. Common points of failures like generators and cooling equipment are not shared across Availability Zones. Additionally, they are physically separate, such that even extremely uncommon disasters such as fires, tornados, or flooding would only affect a single Availability Zone. Availability Zones within the same Region benefit from low-latency network connectivity.

### What Do “primary” and “standby” Mean in the Context of a Multi-AZ Deployment?

When you run a DB instance as a Multi-AZ deployment, the “primary” serves database writes and reads. In addition, Amazon RDS provisions and maintains a “standby” behind the scenes, which is an up-to-date replica of the primary. The standby is “promoted” in failover scenarios. After failover, the standby becomes the primary and accepts your database operations. You do not interact directly with the standby (e.g. for read operations) at any point prior to promotion. If you are interested in scaling read traffic beyond the capacity constraints of a single DB instance, please see the FAQs on [Read Replicas](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_ReadRepl.html).

### What Are the Benefits of a Multi-AZ Deployment?

The chief benefits of running your DB instance as a Multi-AZ deployment are enhanced database durability and availability. The increased availability and fault tolerance offered by Multi-AZ deployments make them a natural fit for production environments.  
 

Running your DB instance as a Multi-AZ deployment safeguards your data in the unlikely event of a DB instance component failure or loss of availability in one Availability Zone. For example, if a storage volume on your primary fails, Amazon RDS automatically initiates a failover to the standby, where all of your database updates are intact. This provides additional data durability relative to standard deployments in a single AZ, where a user-initiated restore operation would be required and updates that occurred after the latest restorable time (typically within the last five minutes) would not be available.  
  
You also benefit from enhanced database availability when running your DB instance as a Multi-AZ deployment. If an Availability Zone failure or DB instance failure occurs, your availability impact is limited to the time automatic failover takes to complete. The availability benefits of Multi-AZ also extend to planned maintenance.  
  
For example, with automated backups, I/O activity is no longer suspended on your primary during your preferred backup window, since backups are taken from the standby. In the case of patching or DB instance class scaling, these operations occur first on the standby, prior to automatic failover. As a result, your availability impact is limited to the time required for automatic failover to complete.  
  
Another implied benefit of running your DB instance as a Multi-AZ deployment is that DB instance failover is automatic and requires no administration. In an Amazon RDS context, this means you are not required to monitor DB instance events and initiate manual DB instance recovery (via the RestoreDBInstanceToPointInTime or RestoreDBInstanceFromSnapshot APIs) in the event of an Availability Zone failure or DB instance failure.

### Are there Any Performance Implications of Running My DB Instance as a Multi-AZ Deployment?

You may observe elevated latencies relative to a standard DB instance deployment in a single Availability Zone as a result of the synchronous data replication performed on your behalf.

### When Running My DB Instance as a Multi-AZ Deployment, Can I Use the Standby for Read or Write Operations?

No, a Multi-AZ standby cannot serve read requests. Multi-AZ deployments are designed to provide enhanced database availability and durability, rather than read scaling benefits. As such, the feature uses synchronous replication between primary and standby. Our implementation makes sure the primary and the standby are constantly in sync, but precludes using the standby for read or write operations. If you are interested in a read scaling solution, please see the FAQs on [Read Replicas](https://aws.amazon.com/rds/features/read-replicas/).

### How Do I Set up a Multi-AZ DB Instance Deployment?

In order to create a Multi-AZ DB instance deployment, simply click the “Yes” option for “Multi-AZ Deployment” when launching a DB Instance with the AWS Management Console.

Alternatively, if you are using the Amazon RDS APIs, you would call the CreateDBInstance API and set the “Multi-AZ” parameter to the value “true.” To convert an existing standard (single-AZ) DB instance to Multi-AZ, modify the DB instance in the AWS Management Console or use the ModifyDBInstance API and set the Multi-AZ parameter to true.

### What Happens when I Convert My Amazon RDS Instance from Single-AZ to Multi-AZ?

For the [RDS for PostgreSQL](https://aws.amazon.com/rds/postgresql/)<u>,</u> [RDS for MySQL](https://aws.amazon.com/rds/mysql/), [RDS for MariaDB](https://aws.amazon.com/rds/mariadb/), [RDS for SQL Server](https://aws.amazon.com/rds/sqlserver/), [RDS for Oracle](https://aws.amazon.com/rds/oracle/)<u>,</u> and [RDS for Db2](https://aws.amazon.com/rds/db2/) database engines, when you elect to convert your Amazon RDS instance from Single-AZ to Multi-AZ, the following happens:

- A snapshot of your primary instance is taken.
- A new standby instance is created in a different Availability Zone, from the snapshot.
- Synchronous replication is configured between primary and standby instances.

As such, there should be no downtime incurred when an instance is converted from Single-AZ to Multi-AZ. However, you might see increased latency while the data on the standby is caught up to match to the primary.

### What Events Would Cause Amazon RDS to Initiate a Failover to the Standby Replica?

Amazon RDS detects and automatically recovers from the most common failure scenarios for Multi-AZ deployments so that you can resume database operations as quickly as possible without administrative intervention. Amazon RDS automatically performs a failover in the event of any of the following:

- Loss of availability in primary Availability Zone
- Loss of network connectivity to primary
- Compute unit failure on primary
- Storage failure on primary

Note: When operations such as DB instance scaling or system upgrades, like OS patching, are initiated for Multi-AZ deployments, for enhanced availability they are applied first on the standby prior to automatic failover. As a result, your availability impact is limited only to the time required for automatic failover to complete. Note that Amazon RDS Multi-AZ deployments do not failover automatically in response to database operations, such as long running queries, deadlocks, or database corruption errors.

### Will I Be Alerted when Automatic Failover Occurs?

Yes, Amazon RDS will emit a DB instance event to inform you that automatic failover occurred. You can click the “Events” section of the Amazon RDS Console or use the DescribeEvents API to return information about events related to your DB instance. You can also use [Amazon RDS Event Notifications](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_Events.html) to be notified when specific DB events occur.

### What Happens during Multi-AZ Failover and how long Does it Take?

Failover is automatically handled by Amazon RDS so that you can resume database operations as quickly as possible without administrative intervention. When failing over, Amazon RDS simply flips the canonical name record (CNAME) for your DB instance to point at the standby, which is in turn promoted to become the new primary. We encourage you to follow best practices and implement database connection retry at the application layer.

Failovers, as defined by the interval between the detection of the failure on the primary and the resumption of transactions on the standby, typically complete within one to two minutes. Failover time can also be affected by whether large uncommitted transactions must be recovered; the use of adequately large instance types is recommended with Multi-AZ for best results. AWS also recommends the use of Provisioned IOPS with Multi-AZ instances, for fast, predictable, and consistent throughput performance.

### Can I Initiate a “forced failover” for My Multi-AZ DB Instance Deployment?

Amazon RDS will automatically failover without user intervention under a variety of failure conditions. In addition, Amazon RDS provides an option to initiate a failover when rebooting your instance. You can access this feature via the AWS Management Console or when using the RebootDBInstance API call.

### How Do I control/configure Multi-AZ Synchronous Replication?

With Multi-AZ deployments, you simply set the “Multi-AZ” parameter to true. The creation of the standby, synchronous replication, and failover are all handled automatically. This means you cannot select the Availability Zone your standby is deployed in or alter the number of standbys available (Amazon RDS provisions one dedicated standby per DB instance primary). The standby also cannot be configured to accept database read activity. [Learn more about Multi-AZ configurations.](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Concepts.MultiAZ.html)

### Will My Standby Be in the Same Region as My Primary?

Yes. Your standby is automatically provisioned in a different Availability Zone of the _same Region_ as your DB instance primary.

### Can I See Which Availability Zone My Primary is Currently Located In?

Yes, you can gain visibility into the location of the current primary by using the AWS Management Console or DescribeDBInstances API.

### After Failover, My Primary is now Located in a Different Availability Zone than My other AWS Resources (e.g. EC2 instances). Should I Be Concerned about Latency?

Availability Zones are engineered to provide low latency network connectivity to other Availability Zones in the same Region. In addition, you may want to consider architecting your application and other AWS resources with redundancy across multiple Availability Zones so your application will be resilient in the event of an Availability Zone failure. Multi-AZ deployments address this need for the database tier without administration on your part.

### How Do DB Snapshots and Automated Backups Work with My Multi-AZ Deployment?

You interact with automated backup and DB Snapshot functionality in the same way whether you are running a standard deployment in a Single-AZ or Multi-AZ deployment. If you are running a Multi-AZ deployment, automated backups and DB Snapshots are simply taken from the standby to avoid I/O suspension on the primary. Please note that you may experience increased I/O latency (typically lasting a few minutes) during backups for both Single-AZ and Multi-AZ deployments.

Initiating a restore operation (point-in-time restore or restore from DB Snapshot) also works the same with Multi-AZ deployments as standard, Single-AZ deployments. New DB instance deployments can be created with either the RestoreDBInstanceFromSnapshot or RestoreDBInstanceToPointInTime APIs. These new DB instance deployments can be either standard or Multi-AZ, regardless of whether the source backup was initiated on a standard or Multi-AZ deployment.

## Read Replicas

Open all

### What Does it Mean to Run a DB Instance as a Read Replica?

[Read replicas](https://aws.amazon.com/rds/faqs/) make it easier to take advantage of supported engines' built-in replication functionality to elastically scale out beyond the capacity constraints of a single DB instance for read-heavy database workloads.

You can [create a read replica](https://aws.amazon.com/premiumsupport/knowledge-center/create-read-replica-rds/) with a few clicks in the AWS Management Console or using the CreateDBInstanceReadReplica API. Once the read replica is created, database updates on the source DB instance will be replicated using a supported engine's native, asynchronous replication. You can create multiple read replicas for a given source DB Instance and distribute your application’s read traffic amongst them.

Since read replicas use supported engines' built-in replication, they are subject to its strengths and limitations. In particular, updates are applied to your read replica(s) after they occur on the source DB instance, and replication lag can vary significantly. Read replicas can be associated with Multi-AZ deployments to gain read scaling benefits in addition to the enhanced database write availability and data durability provided by Multi-AZ deployments.

### When Would I want to Consider Using an Amazon RDS Read Replica?

There are a variety of scenarios where deploying one or more read replicas for a given source DB instance may make sense. Common reasons for deploying a read replica include:

- Scaling beyond the compute or I/O capacity of a single DB instance for read-heavy database workloads. This excess read traffic can be directed to one or more read replicas.
- Serving read traffic while the source DB instance is unavailable. If your source DB Instance cannot take I/O requests (e.g. due to I/O suspension for backups or scheduled maintenance), you can direct read traffic to your read replica(s). For this use case, keep in mind that the data on the read replica may be “stale” since the source DB Instance is unavailable.
- Business reporting or data warehousing scenarios. You may want business reporting queries to run against a read replica rather than your primary, production DB Instance.
- You may use a read replica for disaster recovery of the source DB instance either in the same AWS Region or in another Region.

### Do I Need to Enable Automatic Backups on My DB Instance before I Can Create Read Replicas?

Yes. Enable automatic backups on your source DB Instance before adding read replicas by setting the backup retention period to a value other than 0. Backups must remain enabled for read replicas to work.

### Which Versions of Database Engines Support Amazon RDS Read Replicas?

[Amazon Aurora](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/Aurora.Replication.html): All DB clusters.

[Amazon RDS for MySQL](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_MySQL.Replication.ReadReplicas.html): All DB instances support creation of read replicas. Automatic backups must be and remain enabled on the source DB instance for read replica operations. Automatic backups on the replica are supported only for Amazon RDS read replicas running MySQL 5.6 and later, not 5.5.

[Amazon RDS for PostgreSQL](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_PostgreSQL.Replication.ReadReplicas.html): DB instances with PostgreSQL version 9.3.5 or newer support creation of read replicas. Existing PostgreSQL instances prior to version 9.3.5 need to be upgraded to PostgreSQL version 9.3.5 to take advantage of Amazon RDS read replicas.

[Amazon RDS for MariaDB](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_MariaDB.Replication.ReadReplicas.html): All DB instances support creation of read replicas. Automatic backups must be and remain enabled on the source DB Instance for read replica operations.

[Amazon RDS for Oracle](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/oracle-read-replicas.overview.html): Supported for Oracle version 12.1.0.2.v12 and higher and for all 12.2 versions using the Bring Your Own License model with Oracle Database Enterprise Edition and licensed for the Active Data Guard Option.

[Amazon RDS for SQL Server](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/SQLServer.ReadReplicas.html): Read replicas are supported on Enterprise Edition in the Multi-AZ configuration when the underlying replication technology is using Always On availability groups for SQL Server versions 2016 and 2017.

### How Do I Deploy a Read Replica for a given DB Instance?

You can create a read replica in minutes using the standard CreateDBInstanceReadReplica API or a few steps on the AWS Management Console. When creating a read replica, you can identify it as a read replica by specifying a SourceDBInstanceIdentifier. The SourceDBInstanceIdentifier is the DB Instance Identifier of the “source” DB Instance from which you wish to replicate. As with a standard DB Instance, you can also specify the Availability Zone, DB instance class, and preferred maintenance window. The engine version (e.g., PostgreSQL 9.3.5) and storage allocation of a read replica is inherited from the source DB instance. 

When you initiate the creation of a read replica, Amazon RDS takes a snapshot of your source DB instance and begins replication. As a result, you will experience a brief I/O suspension on your source DB instance as the snapshot occurs. The I/O suspension typically lasts on the order of one minute and is avoided if the source DB instance is a Multi-AZ deployment (in the case of Multi-AZ deployments, snapshots are taken from the standby).

Amazon RDS is also currently working on an optimization (to be released shortly) such that if you create multiple Read Replicas within a 30 minute window, all of them will use the same source snapshot to minimize I/O impact (“catch-up” replication for each Read Replica will begin after creation).

### How Do I Connect to My Read replica(s)?

You can connect to a read replica just as you would connect to a standard DB instance, using the DescribeDBInstance API or AWS Management Console to retrieve the endpoint(s) for your read replica(s). If you have multiple read replicas, it is up to your application to determine how read traffic will be distributed amongst them.

### How Many Read Replicas Can I Create for a given Source DB Instance?

Amazon RDS for MySQL, MariaDB, and PostgreSQL allow you to create up to 15 read replicas for a given source DB instance. Amazon RDS for Oracle and SQL Server allow you to create up to 5 read replicas for a given source DB instance.

### Can I Create a Read Replica in an AWS Region Different from that of the Source DB Instance?

Yes, Amazon RDS (except RDS for SQL Server) supports cross-region read replicas. The amount of time between when data is written to the source DB instance and when it is available in the read replica will depend on the network latency between the two regions.

### Do Amazon RDS Read Replicas Support Synchronous Replication?

No. Read replicas in Amazon RDS for MySQL, MariaDB, PostgreSQL, Oracle, and SQL Server are implemented using those engines' native asynchronous replication. Amazon Aurora uses a different, but still asynchronous, replication mechanism.

### Can I Use a Read Replica to Enhance Database Write Availability or Protect the Data on My Source DB Instance against Failure Scenarios?

If you are looking to use replication to increase database write availability and protect recent database updates against various failure conditions, we recommend you run your DB instance as a Multi-AZ deployment. With Amazon RDS Read Replicas, which employ supported engines' native, asynchronous replication, database writes occur on a read replica after they have already occurred on the source DB instance, and this replication “lag” can vary significantly. 

In contrast, the replication used by Multi-AZ deployments is synchronous, meaning that all database writes are concurrent on the primary and standby. This protects your latest database updates, since they should be available on the standby in the event failover is required. 

In addition, with Multi-AZ deployments replication is fully managed. Amazon RDS automatically monitors for DB instance failure conditions or Availability Zone failure and initiates automatic failover to the standby (or to a read replica, in the case of Amazon Aurora) if an outage occurs.

### Can I Create a Read Replica with a Multi-AZ DB Instance Deployment as Its Source?

Yes. Since Multi-AZ DB instances address a different need than read replicas, it makes sense to use the two in conjunction for production deployments and to associate a read replica with a Multi-AZ DB Instance deployment. The “source” Multi AZ-DB instance provides you with enhanced write availability and data durability, and the associated read replica would improve read traffic scalability.

### Can I Configure My Amazon RDS Read Replicas Themselves Multi-AZ?

Yes. Amazon RDS for MySQL, MariaDB, PostgreSQL, and Oracle allow you to enable Multi-AZ configuration on read replicas to support disaster recovery and minimize downtime from engine upgrades.

### If My Read replica(s) Use a Multi-AZ DB Instance Deployment as a Source, what Happens if Multi-AZ Failover Occurs?

In the event of Multi-AZ failover, any associated and available read replicas will automatically resume replication once failover has completed (acquiring updates from the newly promoted primary).

### Can I Create a Read Replica of Another Read Replica?

Amazon Aurora, Amazon RDS for MySQL, and MariaDB: You can create three tiers of read replicas. A second-tier read replica from an existing first-tier read replica and a third tier replica from second tier read replicas. By creating a second-tier and third-tier read replica, you may be able to move some of the replication load from the primary database instance to different tiers of Read Replica based on your application needs.

Please note that a second-tier Read Replica may lag further behind the primary because of additional replication latency introduced as transactions are replicated from the primary to the first tier replica and then to the second-tier replica. Similarly, the third tier replica may lag behind the second-tier read replica.

Amazon RDS for Oracle and Amazon RDS for SQL Server: Read Replicas of Read Replicas are not currently supported.

### Can My Read Replicas only Accept Database Read Operations?

Read replicas are designed to serve read traffic. However, there may be use cases where advanced users wish to complete Data Definition Language (DDL) SQL statements against a read replica. Examples might include adding a database index to a read replica that is used for business reporting without adding the same index to the corresponding source DB instance.

Amazon RDS for MySQL can be configured to permit DDL SQL statements against a read replica. If you wish to enable operations other than reads for a given read replica, modify the active DB parameter group for the read replica setting the “read\_only” parameter to “0.”

Amazon RDS for PostgreSQL does not currently support the execution of DDL SQL statements against a read replica.

### Can I Promote My Read Replica into a “standalone” DB Instance?

Yes. Refer to the [Amazon RDS User Guide](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_ReadRepl.html) for more details.

### Will My Read Replica Be Kept Up-to-date with Its Source DB Instance?

Updates to a source DB instance will automatically be replicated to any associated read replicas. However, with supported engines' asynchronous replication technology, a read replica can fall behind its source DB instance for a variety of reasons. Typical reasons include:

- Write I/O volume to the source DB instance exceeds the rate at which changes can be applied to the read replica (this problem is particularly likely to arise if the compute capacity of a read replica is less than the source DB Instance)
- Complex or long-running transactions to the source DB Instance hold up replication to the read replica
- Network partitions or latency between the source DB instance and a read replica

Read Replicas are subject to the strengths and weaknesses of supported engines' native replication. If you are using Read Replicas, you should be aware of the potential for a lag between a Read Replica and its source DB Instance or “inconsistency”.

### How Do I See the Status of My Active Read replica(s)?

You can use the standard DescribeDBInstances API to return a list of all the DB Instances you have deployed (including Read Replicas) or simply click on the "Instances" tab of the Amazon RDS Console.

Amazon RDS allows you to gain visibility into how far a read replica has fallen behind its source DB instance. The number of seconds that the read replica is behind the primary is published as an Amazon CloudWatch metric ("Replica Lag") available via the AWS Management Console or Amazon CloudWatch APIs.

For Amazon RDS for MySQL, the source of this information is the same as that displayed by issuing a standard "Show Replica Status" MySQL command against the read replica. For Amazon RDS for PostgreSQL, you can use the pg\_stat\_replication view on the source DB instance to explore replication metrics.

Amazon RDS monitors the replication status of your Read Replicas and updates the Replication State field in the AWS Management console to "Error" if replication stops for any reason (e.g. attempting DML queries on your replica that conflict with the updates made on the primary database instance could result in a replication error). You can review the details of the associated error thrown by the MySQL engine by viewing the Replication Error field and take appropriate action to recover from it. You can learn more about troubleshooting replication issues in the [Troubleshooting a Read Replica Problem section of the User Guide](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_ReadRepl.html#USER_ReadRepl.Troubleshooting) for Amazon RDS for MySQL or PostgreSQL. 

If a replication error is fixed, the Replication State changes to Replicating.

### I Scaled the Compute and/or Storage Capacity of My Source DB Instance. Should I Scale the Resources for Associated Read replica(s) as Well?

For replication to work effectively, we recommend that read replicas have as much or more compute and storage resources as their respective source DB instances. Otherwise replication lag is likely to increase or your read replica may run out of space to store replicated updates.

### How Do I Delete a Read Replica? Will it Be Deleted Automatically if Its Source DB Instance is Deleted?

You can delete a read replica with a few steps of the AWS Management Console or by passing its DB Instance identifier to the DeleteDBInstance API. 

An Amazon Aurora replica will stay active and continue accepting read traffic even after its corresponding source DB Instance has been deleted. One of the replicas in the cluster will automatically be promoted as the new primary and will start accepting write traffic.

An Amazon RDS for MySQL or MariaDB read replica will stay active and continue accepting read traffic even after its corresponding source DB instance has been deleted. If you desire to delete the Read Replica in addition to the source DB instance, you must explicitly do so using the DeleteDBInstance API or AWS Management Console.

If you delete an Amazon RDS for PostgreSQL DB Instance that has read replicas, all Read Replicas will be promoted to standalone DB Instances and will be able to accept both read and write traffic. The newly promoted DB Instances will operate independently of one another. If you desire to delete these DB Instances in addition to the original source DB Instance, you must explicitly do so using the DeleteDBInstance API or AWS Management Console.

### How much Do Read Replicas Cost? When Does Billing Begin and End?

A read replica is billed as a standard DB Instance and at the same rates. Just like a standard DB instance, the rate per “DB Instance hour” for a read replica is determined by the DB instance class of the read replica – please see [pricing page](https://aws.amazon.com/rds/pricing/) for up-to-date pricing. You are not charged for the data transfer incurred in replicating data between your source DB instance and read replica within the same AWS Region.

Billing for a read replica begins as soon as the replica has been successfully created (i.e. when the status is listed as “active”). The read replica will continue being billed at standard Amazon RDS DB instance hour rates until you issue a command to delete it.

## Enhanced Monitoring

Close all

### What is Enhanced Monitoring for Amazon RDS?

[Enhanced Monitoring](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_Monitoring.OS.overview.html) for Amazon RDS gives you deeper visibility into the health of your Amazon RDS instances. Just [turn on the “Enhanced Monitoring” option](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_Monitoring.OS.Enabling.html) for your Amazon RDS DB Instance and set a granularity and Enhanced Monitoring will collect vital operating system metrics and process information, at the defined granularity.

For an even deeper level of diagnostics and visualization of your database load, and a longer data retention period, you can try [Performance Insights](https://aws.amazon.com/rds/performance-insights/).

### Which Metrics and Processes Can I Monitor in Enhanced Monitoring?

Enhanced Monitoring captures your Amazon RDS instance system level metrics, such as the CPU, memory, file system, and disk I/O among others. The complete list of metrics can be found in the [documentation](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_Monitoring.html).

### Which Engines Are Supported by Enhanced Monitoring?

Enhanced Monitoring supports all Amazon RDS database engines.

### Which Instance Types Are Supported by Enhanced Monitoring?

Enhanced Monitoring supports every instance type except t1.micro and m1.small. The software uses a small amount of CPU, memory, and I/O, and for general purpose monitoring, we recommend switching on higher granularities for instances that are medium or larger. For non-production DB Instances, the default setting for Enhanced Monitoring is “off” and you have the choice of leaving it disabled or modifying the granularity when it is on.

### What Information Can I view on the Amazon RDS Dashboard?

You can view all the system metrics and process information for your Amazon RDS DB Instances in a graphical format on the console. You can manage which metrics you want to monitor for each instance and customize the dashboard according to your requirements.

### Will All the Instances in My Amazon RDS account Sample Metrics at the Same Granularity?

No. You can set different granularities for each DB Instance in your Amazon RDS account. You can also choose the instances on which you want to enable Enhanced Monitoring as well as modify the granularity of any instance whenever you want.

### How far back Can I See the Historical Metrics on the Amazon RDS Console?

You can see the performance values for all the metrics up to 1 hour back at a granularity of up to 1 second based on your settings.

### How Can I Visualize the Metrics Generated by Amazon RDS Enhanced Monitoring in CloudWatch?

The metrics from Amazon RDS Enhanced Monitoring are delivered into your CloudWatch Logs account. You can create metrics filters in CloudWatch from CloudWatch Logs and display the graphs on the CloudWatch dashboard. For more details, please visit the [Amazon CloudWatch](https://aws.amazon.com/cloudwatch/pricing/) page.

### When Should I Use CloudWatch instead of the Amazon RDS Console Dashboard?

You should use CloudWatch if you want to view historical data beyond what is available on the Amazon RDS console dashboard. You can monitor your Amazon RDS instances in CloudWatch to diagnose the health of your entire AWS stack in a single location. Currently, CloudWatch supports granularities of up to 1 minute and the values will be averaged out for granularities less than that.

### Can I Set up Alarms and Notifications Based on Specific Metrics?

Yes. You can create an alarm in CloudWatch that sends a notification when the alarm changes state. The alarm watches a single metric over a time period that you specify and performs one or more actions based on the value of the metric relative to the specified threshold over a number of time periods. For more details on CloudWatch alarms, please visit the [Amazon CloudWatch Developer Guide](https://docs.aws.amazon.com/AmazonCloudWatch/latest/DeveloperGuide/AlarmThatSendsEmail.html).

### How Do I Integrate Enhanced Monitoring with My Tool that I Currently Use?

Amazon RDS Enhanced Monitoring provides a set of metrics formed as JSON payloads that are delivered into your CloudWatch Logs account. The JSON payloads are delivered at the granularity last configured for the Amazon RDS instance.

There are two ways you can consume the metrics via a third-party dashboard or application. Monitoring tools can use [CloudWatch Logs Subscriptions](https://docs.aws.amazon.com/AmazonCloudWatch/latest/DeveloperGuide/Subscriptions.html) to set up a near real time feed for the metrics. Alternatively, you can use filters in CloudWatch Logs to bridge metrics across to CloudWatch and integrate your application with CloudWatch. Please visit [Amazon CloudWatch Documentation](http://docs.aws.amazon.com/AmazonCloudWatch/latest/DeveloperGuide/CWL_ES_Stream.html) for more details.

### How Can I Delete Historical Data?

Since Enhanced Monitoring delivers JSON payloads into a log in your CloudWatch Logs account, you can control its retention period just like any other CloudWatch Logs stream. The default retention period configured for Enhanced Monitoring in CloudWatch Logs is 30 days. For details on how to change retention settings, please visit [Amazon CloudWatch Developer Guide](https://docs.aws.amazon.com/managedservices/latest/userguide/log-customize-retention.html).

### What Impact Does Enhanced Monitoring Have on My Monthly Bills?

Since the metrics are ingested into CloudWatch Logs, your charges will be based on CloudWatch Logs data transfer and storage rates once you exceed CloudWatch Logs free tier. Pricing details can be found [here](https://aws.amazon.com/cloudwatch/pricing/). The amount of information transferred for an Amazon RDS instance is directly proportional to the defined granularity for the Enhanced Monitoring feature. Administrators can set different granularities for different instances in their accounts to manage costs.

The approximate volume of data ingested into CloudWatch Logs by Enhanced Monitoring for an instance is as shown below:

<table><tbody><tr><td><strong>Granularity</strong></td><td><strong>60 seconds</strong></td><td><strong>30 seconds</strong></td><td><strong>15 seconds</strong></td><td><strong>10 seconds</strong></td><td><strong>5 seconds</strong></td><td><strong>1 second</strong></td></tr><tr><td><p>Data ingested in CloudWatch Logs* (GB per month)</p></td><td><p>0.27</p></td><td><p>0.53</p></td><td><p>1.07</p></td><td><p>1.61</p></td><td><p>3.21</p></td><td><p>16.07</p></td></tr></tbody></table>

## Amazon RDS Proxy

Close all

### What is Amazon RDS Proxy?

[Amazon RDS Proxy](https://aws.amazon.com/rds/proxy/) is a fully managed, highly available database proxy feature for Amazon RDS. RDS Proxy makes applications more scalable, more resilient to database failures, and more secure.

### Why Would I Use Amazon RDS Proxy?

Amazon RDS Proxy is a fully managed, highly available, and easy-to-use database proxy feature of Amazon RDS that enables your applications to: 1) improve scalability by pooling and sharing database connections, 2) improve availability by reducing database failover times by up to 66% and preserving application connections during failovers, and 3) improve security by optionally enforcing AWS IAM authentication to databases and securely storing credentials in AWS Secrets Manager.

### What Use Cases Does Amazon RDS Proxy Address?

Amazon RDS Proxy addresses a number of [use cases](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/rds-proxy.html) related to scalability, availability, and security of your applications, including:

Applications with unpredictable workloads: Applications that support highly variable workloads may attempt to open a burst of new database connections. Amazon RDS Proxy’s connection governance allows you to gracefully scale applications dealing with unpredictable workloads by efficiently reusing database connections. First, RDS Proxy enables multiple application connections to share a database connection for efficient use of database resources. Second, RDS Proxy allows you to maintain predictable database performance by regulating the number of database connections that are opened. Third, RDS Proxy removes requests that cannot be served to preserve the overall performance and availability of the application.

Applications that frequently open and close database connections: Applications built on technologies such as Serverless, PHP, or Ruby on Rails may open and close database connections frequently to serve application requests. Amazon RDS Proxy maintains a pool of database connections to avoid unnecessary stress on database compute and memory for establishing new connections.

Applications that keep connections open but idle: Applications in industries such as SaaS or eCommerce may keep database connections idling to minimize the response time when a customer reengages. Instead of overprovisioning databases to support mostly idling connections, you can use Amazon RDS Proxy to hold idling connections while only establishing database connections as required to optimally serve active requests.

Applications requiring availability through transient failures: With Amazon RDS Proxy, you can build applications that can transparently tolerate database failures without needing to write complex failure handling code. RDS Proxy automatically routes traffic to a new database instance while preserving application connections. RDS Proxy also bypasses Domain Name System (DNS) caches to reduce failover times by up to 66% for Amazon RDS and Aurora Multi-AZ databases. During database failovers, the application may experience increased latencies and ongoing transactions may have to be retried.

Improved security and centralized credentials management: Amazon RDS Proxy aids you in building more secure applications by giving you a choice to enforce IAM based authentication with relational databases. RDS Proxy also enables you to centrally manage database credentials through AWS Secrets Manager.

### When Should I Connect to the Database Directly versus Using Amazon RDS Proxy?

Depending on your workload, Amazon RDS Proxy can add an average of 5 milliseconds of network latency to query or transaction response time. If your application cannot tolerate 5 milliseconds of latency or does not need connection management and other features enabled by RDS Proxy, you may want your application to connect directly to the database endpoint.

### How Will Serverless Applications Benefit from Amazon RDS Proxy?

Amazon RDS Proxy transforms your approach to building modern [serverless applications](https://aws.amazon.com/blogs/aws/amazon-rds-proxy-now-generally-available/) that leverage the power and simplicity of relational databases. First, RDS Proxy enables serverless applications to scale efficiently by pooling and reusing database connections. Second, with RDS Proxy, you no longer need to handle database credentials in your Lambda code. You can use the IAM execution role associated with your Lambda function to authenticate with RDS Proxy and your database. Third, you don’t need to manage any new infrastructure or code to utilize the full potential of serverless applications backed by relational databases. RDS Proxy is fully managed and scales its capacity automatically based on your application demands.

### Which Database Engines Does Amazon RDS Proxy Support?

RDS Proxy is available for Amazon Aurora with MySQL compatibility, Amazon Aurora with PostgreSQL compatibility, Amazon RDS for MariaDB, Amazon RDS for MySQL, Amazon RDS for PostgreSQL, and Amazon RDS for SQL Server. For a list of supported engine versions see the [Amazon Aurora User Guide](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/Concepts.AuroraFeaturesRegionsDBEngines.grids.html#Concepts.Aurora_Fea_Regions_DB-eng.Feature.RDS_Proxy) or the [Amazon RDS User Guide](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/rds-proxy.html#rds-proxy.support).

### How Can I Enable Amazon RDS Proxy?

You enable Amazon RDS Proxy for your Amazon RDS database with just a few clicks in the Amazon RDS console. While enabling RDS Proxy, you specify the VPC and subnets you want to access RDS Proxy from. As a Lambda user, you can enable Amazon RDS Proxy for your Amazon RDS database and set up a Lambda function to access it with just a few clicks in the Lambda console.

### Can I Access Amazon RDS Proxy Using APIs?

Yes. You can use Amazon RDS Proxy APIs to create a proxy and then define target groups to associate the proxy with specific database instances or clusters. For example:

```
aws rds create-db-proxy 
        --db-proxy-name '…' 
        --engine-family &lt;mysql|postgresql&gt;       
        --auth [{}, {}] 
        --role-arn '…'
        --subnet-ids {}
        --require-tls &lt;true|false&gt;
        --tags {}
aws rds register-db-proxy-targets 
        --target-group-name '…'
        --db-cluster-identifier  '…'
        --db-instance-identifier '…'
```

## Trusted Language Extensions for PostgreSQL

Close all

### Why Should I Use Trusted Language Extensions for PostgreSQL?

[Trusted Language Extensions (TLE) for PostgreSQL](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/PostgreSQL_trusted_language_extension.html) enables developers to build high performance PostgreSQL extensions and run them safely on [Amazon Aurora](https://aws.amazon.com/rds/aurora/) and [Amazon RDS](https://aws.amazon.com/rds/). In doing so, TLE improves your time to market and removes the burden placed on database administrators to certify custom and third-party code for use in production database workloads. You can move forward as soon as you decide an extension meets your needs. With TLE, independent software vendors (ISVs) can provide new PostgreSQL extensions to customers running on Aurora and Amazon RDS.

### What Are Traditional Risks of Running Extensions in PostgreSQL and how Does TLE for PostgreSQL Mitigate Those Risks?

PostgreSQL extensions are executed in the same process space for high performance. However, extensions might have software defects that can crash the database.  
  
[TLE for PostgreSQL](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/PostgreSQL_trusted_language_extension.html) offers multiple layers of protection to mitigate this risk. TLE is designed to limit access to system resources. The **rds\_superuser** role can determine who is permitted to install specific extensions. However, these changes can only be made through the TLE API. TLE is designed to limit the impact of an extension defect to a single database connection. In addition to these safeguards, TLE is designed to provide DBAs in the **rds\_superuser** role fine-grained, online control over who can install extensions and they can create a permissions model for running them.  
  
Only users with sufficient privileges will be able to run and create using the “CREATE EXTENSION” command on a TLE extension. DBAs can also allow-list “PostgreSQL hooks” required for more sophisticated extensions that modify the database’s internal behavior and typically require elevated privilege.

### How Does TLE for PostgreSQL Relate to/work with other AWS Services?

[TLE for PostgreSQL](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/PostgreSQL_trusted_language_extension.html) is available for [Amazon Aurora PostgreSQL-Compatible Edition](https://aws.amazon.com/rds/aurora/) and [Amazon RDS on PostgreSQL](https://aws.amazon.com/rds/aurora/) on versions 14.5 and higher. TLE is implemented as a PostgreSQL extension itself and you can activate it from the rds\_superuser role similar to other extensions supported on Aurora and Amazon RDS.

### In what Versions of PostgreSQL Can I Run TLE for PostgreSQL?

You can run [TLE for PostgreSQL](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/PostgreSQL_trusted_language_extension.html) in PostgreSQL 14.5 or higher in [Amazon Aurora](https://aws.amazon.com/rds/aurora/) and [Amazon RDS](https://aws.amazon.com/rds/).  

### In what Regions is Trusted Language Extensions for PostgreSQL Available?

[TLE for PostgreSQL](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/PostgreSQL_trusted_language_extension.html) is currently available in all AWS Regions (excluding AWS China Regions) and the AWS GovCloud Regions.

### How much Does it Cost to Run TLE?

[TLE for PostgreSQL](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/PostgreSQL_trusted_language_extension.html) is available to [Aurora](https://aws.amazon.com/rds/aurora/) and [Amazon RDS](https://aws.amazon.com/rds/) customers at no additional cost.

### How is TLE for PostgreSQL Different from Extensions Available on Amazon Aurora and Amazon RDS Today?

[Aurora](https://aws.amazon.com/rds/aurora/) and [Amazon RDS](https://aws.amazon.com/rds/) support a curated set of over [85 PostgreSQL extensions](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/CHAP_PostgreSQL.html#PostgreSQL.Concepts.General.FeatureSupport.Extensions). AWS manages the security risks for each of these extensions under the [AWS shared responsibility model](https://aws.amazon.com/compliance/shared-responsibility-model/). The extension that implements [TLE for PostgreSQL](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/PostgreSQL_trusted_language_extension.html) is included in this set. Extensions that you write or that you obtain from third-party sources and install in TLE are considered part of your application code. You are responsible for the security of your applications that use TLE extensions.

### What Are Some Examples of Extensions I Could Run with TLE for PostgreSQL?

You can build developer functions, such as bitmap compression and differential privacy (such as publicly accessible statistical queries that protect privacy of individuals).

### What Programming Languages Can I Use to Develop TLE for PostgreSQL?

[TLE for PostgreSQL](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/PostgreSQL_trusted_language_extension.html) currently supports JavaScript, PL/pgSQL, Perl, and SQL.

### How Do I Deploy a TLE for PostgreSQL Extension?

Once the rds\_superuser role activates TLE for PostgreSQL, you can deploy TLE extensions using the SQL CREATE EXTENSION command from any PostgreSQL client, such as psql. This is similar to how you would create a user-defined function written in a procedural language, such as PL/pgSQL or PL/Perl. You can control which users have permission to deploy TLE extensions and use specific extensions.

### How Do TLE for PostgreSQL Extensions Communicate with the PostgreSQL Database?

[TLE for PostgreSQL](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/PostgreSQL_trusted_language_extension.html) accesses your PostgreSQL database exclusively through the TLE API. The TLE supported trusted languages include all functions of the PostgreSQL server programming interface (SPI) and support for PostgreSQL hooks, including the check password hook.

### Where Can I Learn More about the TLE for PostgreSQL Open-source Project?

You can learn more about the [TLE for PostgreSQL](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/PostgreSQL_trusted_language_extension.html) project on the official [TLE GitHub page](https://github.com/aws/pg_tle).

## Amazon RDS Blue/Green Deployments

Close all

### What Engines Support Amazon RDS Blue/Green Deployments?

[Amazon RDS Blue/Green Deployments](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/blue-green-deployments.html) are available in [Amazon Aurora MySQL-Compatible Edition](https://aws.amazon.com/rds/aurora/), [Amazon Aurora PostgreSQL-Compatible Edition](https://aws.amazon.com/rds/aurora/), [Amazon RDS for MySQL,](https://aws.amazon.com/rds/mysql/) [Amazon RDS for MariaDB](https://aws.amazon.com/rds/mariadb/), and [Amazon RDS for PostgreSQL](https://aws.amazon.com/rds/postgresql/). 

### What Versions Does Amazon RDS Blue/Green Deployments Support?

Amazon RDS Blue/Green Deployments are available in for Amazon Aurora MySQL-Compatible Edition versions 5.6 and higher, RDS for MySQL versions 5.7 and higher, and RDS for versions MariaDB versions 10.2 and higher. Blue/Green Deployments are also supported for Amazon Aurora PostgreSQL-Compatible Edition and Amazon RDS for PostgreSQL for versions 11.21 and higher, 12.16 and higher, 13.12 and higher, 14.9 and higher, and 15.4 and higher. Learn more about available versions in the [Amazon Aurora](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/Concepts.Aurora_Fea_Regions_DB-eng.Feature.BlueGreenDeployments.html) and [Amazon RDS documentation](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/blue-green-deployments.html). 

### What Regions Does Amazon RDS Blue/Green Deployments Support?

Amazon RDS Blue/Green Deployments are available in all applicable AWS Regions and the AWS GovCloud Regions.

### When Should I Use Amazon RDS Blue/Green Deployments?

Amazon RDS Blue/Green Deployments allow you to make safer, simpler, and faster database changes. Blue/Green Deployments are ideal for use cases such as major or minor version database engine upgrades, operating system updates, schema changes on green environments that do not break logical replication, like adding a new column at the end of a table, or database parameter setting changes. You can use Blue/Green Deployments to make multiple database updates at the same time using a single switchover. This allows you to stay current on security patches, improve database performance, and access newer database features with short, predictable downtime.

### What is the Cost of Using Amazon RDS Blue/Green Deployments?

You will incur the same price for running your workloads on green instances as you do for blue instances. The cost of running on blue and green instances include our [current standard pricing](https://aws.amazon.com/rds/pricing/) for db.instances, cost of storage, cost of read/write I/Os, and any enabled features, such as cost of backups and [Amazon RDS Performance Insights](https://aws.amazon.com/rds/performance-insights/). Effectively, you are paying approximately 2x the cost of running workloads on db.instance for the lifespan of the blue-green-deployment.

For example: You have an RDS for MySQL 5.7 database running on two r5.2xlarge db.instances, a primary database instance and a read replica, in us-east-1 AWS region with a Multi-AZ (MAZ) configuration. Each of the r5.2xlarge db.instances is configured for 20 GiB General Purpose [Amazon Elastic Block Storge (EBS)](https://aws.amazon.com/ebs/). You create a clone of the blue instance topology using Amazon RDS Blue/Green Deployments, run it for 15 days (360 hours), and then delete the blue instances after a successful switchover. The blue instances cost $1,387 for 15 days at an on-demand rate of $1.926/hr (Instance + EBS cost). The total cost to you for using Blue/Green Deployments for those 15 days is $2,774, which is 2x the cost of running blue instances for that time period.

### What Kind of Changes Can I Make with Amazon RDS Blue/Green Deployments?

Amazon RDS Blue/Green Deployments allow you to make safer, simpler, and faster database changes, such as major or minor version upgrades, schema changes, instance scaling, engine parameter changes, and maintenance updates.

### What is the “blue environment” in Amazon RDS Blue/Green Deployments? What is the “green environment"?

**I**n Amazon RDS Blue/Green Deployments, the blue environment is your current production environment. The green environment is your staging environment that will become your new production environment after switchover.

### How Do Switchovers Work with Amazon RDS Blue/Green Deployments?

When Amazon RDS Blue/Green Deployments initiate a switchover, they block writes to both the blue and green environments, until switchover is complete. During switchover, the staging environment, or green environment, catches up with the production system, ensuring data is consistent between the staging and production environment. Once the production and staging environment are in complete sync, Blue/Green Deployments promote the staging environment as the production environment by redirecting traffic to the newly promoted production environment. Blue/Green Deployments are designed to enable writes on the green environment after switchover is complete, ensuring zero data loss during the switchover process.

### Can I Use Blue/Green Deployments when I Have a Blue Environment as a subscriber/publisher for a Self-managed Logical Replica?

If your blue environment is a self-managed logical replica, or subscriber, we will block switchover. We recommend that you first stop replication to the blue environment, proceed with the switchover, and then resume replication. In contrast, if your blue environment is a source for a self-managed logical replica, or publisher, you can continue to switchover. However, you will need to update the self-managed replica to replicate from the green environment post switchover.

### After Amazon RDS Blue/Green Deployments Switches Over, what Happens to My Old Production Environment?

Amazon RDS Blue/Green Deployments do not delete your old production environment. If needed, you can access it for additional validations and performance/regression testing. If you no longer need the old production environment, you can delete it. Standard billing charges apply on old production instances until you delete them.

### What Do Amazon RDS Blue/Green Deployments Switchover Guardrails Check For?

Amazon RDS Blue/Green Deployments switchover guardrails block writes on your blue and green environments until your green environment catches up before switching over. Blue/Green Deployments also perform health checks of your primary and replicas in your blue and green environments. They also perform replication health checks, for example, to see if replication has stopped or if there are errors. They detect long running transactions between your blue and green environments. You can specify your maximum tolerable downtime, as low as 30 seconds, and if you have an ongoing transaction that exceeds this your switchover will time out.

### Do Amazon RDS Blue/Green Deployments Support Global Databases, Amazon RDS Proxy, cross-Region Read Replicas, or Cascaded Read Replicas?

No, [Amazon RDS Blue/Green Deployments](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/blue-green-deployments.html) do not support [Global Databases](https://aws.amazon.com/rds/aurora/global-database/), [Amazon RDS Proxy](https://aws.amazon.com/rds/proxy/), cross-Region read replicas, or cascaded read replicas.

### Can I Use Amazon RDS Blue/Green Deployments to Rollback Changes?

No, at this time you cannot use Amazon RDS Blue/Green Deployments to rollback changes.

## Amazon RDS Optimized Writes

Close all

### How Does Amazon RDS Optimized Writes Write Data Files Differently than MySQL?

MySQL protects users from data loss by writing data in 16KiB pages in memory twice to durable storage—first to the “doublewrite buffer” and then to table storage[. Amazon RDS Optimized Writes](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/rds-optimized-writes.html) write your 16KiB data pages directly to your data files reliably and durably in one step using the [Torn Write Prevention](https://docs.aws.amazon.com/AWSEC2/latest/WindowsGuide/storage-twp.html) feature of the AWS Nitro System.

### Which RDS for MySQL Database Versions Support Amazon RDS Optimized Writes?

[Amazon RDS Optimized Writes](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/rds-optimized-writes.html) are available for [MySQL major version 8.0.30](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/MySQL.Concepts.VersionMgmt.html) and higher.

### Which Database Instance Types Support Amazon RDS Optimized Writes? In what Regions Are They Available?

[Amazon RDS Optimized Writes](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/rds-optimized-writes.html) are available in db.r6i and db.r5b instances. They are available in all Regions where these instances are available, excluding AWS China Regions.

### When Should I Use Amazon RDS Optimized Writes?

All [Amazon RDS for MySQL](https://aws.amazon.com/rds/mysql/) users should implement [Amazon RDS Optimized Writes](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/rds-optimized-writes.html) for up to 2x improved write transaction throughput. Applications with write-heavy workloads, such as digital payments, financial trading, and online gaming applications will find this feature especially helpful.

### Is Amazon RDS Optimized Writes Supported on Amazon Aurora MySQL-Compatible Edition?

No. [Amazon Aurora MySQL-Compatible Edition](https://aws.amazon.com/rds/aurora/) already avoids the use of the “doublewrite buffer.” Instead, Amazon Aurora replicates data six ways across three Availability Zones (AZs) and uses a quorum-based approach to durably write data and correctly read it thereafter.

### Can Customers Convert Their Existing Amazon RDS Databases to Use Amazon RDS Optimized Writes?

At this time, this initial release does not support enabling [Amazon RDS Optimized Writes](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/rds-optimized-writes.html) for your existing database instances even if the instance class supports Optimized Writes.

### How much Are Amazon RDS Optimized Writes?

[Amazon RDS Optimized Writes](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/rds-optimized-writes.html) are available to RDS for MySQL customers at no additional cost.

## Amazon RDS Optimized Reads

Close all

### How Do Amazon RDS Optimized Reads Speed up Query Performance?

Workloads that use temporary objects in MySQL and MariaDB for query processing benefit from [Amazon RDS Optimized Reads](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/rds-optimized-reads-mariadb.html). Optimized Reads place temporary objects on the database instance's NVMe-based instance storage, instead of the Amazon Elastic Block Store volume. This helps to speed up complex query processing by up to 2X.

### Which RDS for MySQL and RDS for MariaDB Database Versions Support Amazon RDS Optimized Reads?

[Amazon RDS Optimized Reads](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/rds-optimized-reads-mariadb.html) are available for RDS for MySQL on [MySQL versions 8.0.28 and higher](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/MySQL.Concepts.VersionMgmt.html) and on RDS for MariaDB on [MariaDB versions 10.4.25, 10.5.16, 10.6.7 and higher](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/MariaDB.Concepts.VersionMgmt.html).

### Which Database Instance Types Support Amazon RDS Optimized Reads? In what Regions Are They Available?

Amazon RDS Optimized Reads are available in all regions where db.r5d, db.m5d, db.r6gd, and db.m6gd, X2idn, and X2iedn instances are available instances are available. For more information, see the [Amazon RDS DB instance classes documentation](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Concepts.DBInstanceClass.html).

### When Should I Use Amazon RDS Optimized Reads?

Customers should use [Amazon RDS Optimized Reads](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/rds-optimized-reads.html) when they have workloads that require complex queries; general purpose analytics; or require intricate groups, sorts, hash aggregations, high-load joins, and Common Table Expressions (CTEs). These use cases result in the creation of temporary tables, allowing Optimized Reads to speed up your workload’s query processing.

### Can Customers Convert Their Existing Amazon RDS Databases to Use Amazon RDS Optimized Reads?

Yes, customers can convert their existing Amazon RDS database to use [Amazon RDS Optimized Reads](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/rds-optimized-reads.html) by moving your workload to an Optimized Read-enabled instance. Optimized Reads are also available by default on all supported instance classes. If you’re running your workload on db.r5d, db.m5d, db.r6gd, db.m6gd, X2idn, and X2iedn instances, you’re already benefiting from Optimized Reads.