---
tags:
  - cloud/aws
---
![[Pasted image 20240214151657.png]]

![[Module 5- adding a database layer#**Amazon Aurora**| Aurora]]

![](https://i.imgur.com/6EQeH4R.png)


**Amazon Aurora** is <mark style="background: #BBFABBA6;">a relational database service that combines the speed and availability of high-end commercial databases with the simplicity and cost-effectiveness of open-source databases.</mark>

- Aurora is an AWS proprietary database.
- Fully managed service.
- High performance, low price.
- <mark style="background: #FFB86CA6;">2 copies of data are kept in each AZ with a minimum of 3 AZ’s (6 copies).</mark>

<mark style="background: #ABF7F7A6;">Can handle the loss of up to</mark> <mark style="background: #FFF3A3A6;">two copies of data without affecting DB write availability</mark> and up to <mark style="background: #ADCCFFA6;">three copies without affecting read availability</mark>.

The following diagram depicts how Aurora Fault Tolerance and Replicas work:

![Amazon Aurora Fault Tolerance](https://digitalcloud.training/wp-content/uploads/2022/01/amazon-aurora-fault-tolerance.jpeg)

## Aurora Replicas
There are two types of replication: **Aurora replica (up to 15)**,  
**MySQL Read Replica (up to 5)**.

The table below describes the differences between the two replica options:

|   |   |   |
|---|---|---|
|**Feature**|**Aurora Replica**|**MySQL Replica**|
|Number of replicas|Up to 15|Up to 5|
|Replication type|Asynchronous (milliseconds)|Asynchronous (seconds)|
|Performance impact on primary|Low|High|
|Replica location|In-region|Cross-region|
|Act as failover target|Yes (no data loss)|Yes (potentially minutes of data loss)|
|Automated failover|Yes|No|
|Support for user-defined replication delay|No|Yes|
|Support for different data or schema vs. primary|No|Yes|

You can create read replicas for an Amazon Aurora database in up to five AWS regions. This capability is available for Amazon Aurora with MySQL compatibility.

## Cross-Region Read Replicas

<mark style="background: #CACFD9A6;">Cross-region read replicas allow you to improve your disaster recovery posture, scale read operations in regions closer to your application users, and easily migrate from one region to another.</mark>

- <mark style="background: #FFB86CA6;">Cross-region replicas provide fast local reads to your users.</mark>
- Each region can have an additional 15 Aurora replicas to further scale local reads.
- You can choose between [**Global Database**](https://aws.amazon.com/rds/aurora/global-database/), which provides the best replication performance, and traditional binlog-based replication.

You can also set up your own binlog replication with external MySQL databases.

The following diagram depicts the Cross-Region Read Replica topology:

![Aurora Cross Region Replica](https://digitalcloud.training/wp-content/uploads/2022/01/aurora-cross-region-replica.jpeg)

## Global Database

For globally distributed applications, you can use [**Global Database**](https://aws.amazon.com/rds/aurora/global-database/), <mark style="background: #D2B3FFA6;">where a single Aurora database can span multiple AWS regions to enable fast local reads and quick disaster recovery.</mark>
   
<mark style="background: #FFF3A3A6;">Global Database uses storage-based replication to replicate a database across multiple AWS Regions, with typical latency of less than 1 second.</mark>
- <mark style="background: #FFB8EBA6;">You can use a secondary region as a backup option in case you need to recover quickly from a regional degradation or outage.</mark>
- <mark style="background: #CACFD9A6;">A database in a secondary region can be promoted to full read/write capabilities in less than 1 minute.</mark>

The following table depicts the Aurora Global Database topology:

![Aurora Global Database](https://digitalcloud.training/wp-content/uploads/2022/01/aurora-global-database.jpeg)

## Multi-Master
**Amazon Aurora Multi-Master** is <mark style="background: #FFF3A3A6;">a new feature of the Aurora MySQL-compatible edition that adds the ability to scale out write performance across multiple Availability Zones</mark>, <mark style="background: #ADCCFFA6;">allowing applications to direct read/write workloads to multiple instances in a database cluster and operate with higher availability.</mark>

<mark style="background: #FF5582A6;">Aurora Multi-Master is designed to achieve high availability and ACID transactions across a cluster of database nodes</mark> with configurable read after write consistency.

## Architecture

<mark style="background: #ABF7F7A6;">An Aurora cluster consists of a set of compute (database) nodes and a shared storage volume.  
</mark>  
<mark style="background: #BBFABBA6;">The storage volume consists of six storage nodes placed in three Availability Zones for high availability and durability of user data.</mark>

- Every database node in the cluster is a writer node that can run read and write statements.
- There is no single point of failure in the cluster.
- Applications can use any writer node for their read/write and DDL needs.

<mark style="background: #BBFABBA6;">A database change made by a writer node is written to six storage nodes in three Availability Zones, providing data durability and resiliency against storage node and Availability Zone failures.</mark>

The writer nodes are all functionally equal, and a failure of one writer node does not affect the availability of the other writer nodes in the cluster.

## High Availability

Aurora Multi-Master improves upon the high availability of the single-master version of Amazon Aurora because all the nodes in the cluster are read/write nodes.

With single-master Aurora, a failure of the single writer node requires the promotion of a read replica to be the new writer.

In the case of Aurora Multi-Master, the failure of a writer node merely requires the application using the writer to open connections to another writer.

## Aurora Serverless

<mark style="background: #BBFABBA6;">Amazon Aurora Serverless is an on-demand, auto-scaling configuration for Amazon Aurora.</mark>

- Available for MySQL-compatible and PostgreSQL-compatible editions.
- <mark style="background: #CACFD9A6;">The database automatically starts up, shuts down, and scales capacity up or down based on application needs.</mark>
- <mark style="background: #BBFABBA6;">It enables you to run a database in the cloud without managing any database instances.</mark> It’s a simple, cost-effective option for infrequent, intermittent, or unpredictable workloads.

You simply create a database endpoint and optionally specify the desired database capacity range and connect applications.

<mark style="background: #ADCCFFA6;">With Aurora Serverless, you only pay for database storage and the database capacity and I/O your database consumes while it is active.</mark>

- Pay on a per-second basis for the database capacity you use when the database is active.
- <mark style="background: #BBFABBA6;">Can migrate between standard and serverless configurations with a few clicks in the Amazon RDS Management Console.</mark>

The table below provides a few example use cases for Amazon Aurora Serverless:

|   |   |
|---|---|
|**Use Case**|**Example**|
|Infrequently Used Applications|==Application that is only used for a few minutes several times per day or week==. Need a cost-effective database that only requires you to pay when it’s active. <mark style="background: #FF5582A6;">With Aurora Serverless, you only pay for the database resources you consume.</mark> |
|New Applications|==Deploying a new application and are unsure which instance size you need.== With Aurora Serverless, you simply create an endpoint and let the database auto-scale to the capacity requirements of your application. |
|Variable Workloads|<mark style="background: #ADCCFFA6;">Running a lightly used application, with peaks of 30 minutes to several hours a few times each day or several times per year.</mark> Now you only pay for what the resources needed based on load – avoiding paying for unused resources or risking poor performance. |
|Unpredictable Workloads|Running workloads where there is database usage throughout the day, and peaks of activity that are hard to predict. With Aurora Serverless, your database will auto-scale capacity to meet the needs of the application’s peak load and scale back down when the surge of activity is over.|
|Development and Test Databases|Software development and QA teams are using databases during work hours, but don’t need them on nights or weekends. With Aurora Serverless, your database automatically shuts down when not in use, and starts up much more quickly when work starts the next day.|
|Multitenant Applications|Web-based application with a database for each of your customers. Now you don’t have to manage database capacity individually for each application in your fleet. Aurora manages individual database capacity for you, saving you valuable time.|

![[AWS Solutions Architect Skillbuilder#Amazon Aurora Serverless]]

## Fault-Tolerant and Self-Healing Storage

Each 10GB chunk of your database volume is replicated six ways, across three Availability Zones.

<mark style="background: #FFB8EBA6;">Amazon Aurora storage is fault-tolerant, transparently handling the loss of up to two copies of data without affecting database write availability and up to three copies without affecting read availability.  
</mark>  
<mark style="background: #FF5582A6;">Amazon Aurora storage is also self-healing; data blocks and disks are continuously scanned for errors and replaced automatically.</mark>

## Aurora Auto Scaling
<mark style="background: #BBFABBA6;">Aurora Auto Scaling dynamically adjusts the number of Aurora Replicas provisioned for an Aurora DB cluster using single-master replication. </mark>  
<mark style="background: #FFF3A3A6;">Aurora Auto Scaling is available for both Aurora MySQL and Aurora PostgreSQL.</mark>  
Aurora Auto Scaling enables your Aurora DB cluster to handle sudden increases in connectivity or workload.  
<mark style="background: #ADCCFFA6;">When the connectivity or workload decreases, Aurora Auto Scaling removes unnecessary Aurora Replicas so that you don’t pay for unused provisioned DB instances.</mark>

## Backup and Restore
<mark style="background: #FFB86CA6;">Amazon Aurora’s backup capability enables point-in-time recovery for your instance</mark>.  
<mark style="background: #CACFD9A6;">This allows you to restore your database to any second during your retention period, up to the last five minutes.</mark>

- Your automatic backup retention period can be configured up to thirty-five days.

- Automated backups are stored in [**Amazon S3**](https://aws.amazon.com/s3/), which is designed for 99.999999999% durability. <mark style="background: #FFF3A3A6;">Amazon Aurora backups are automatic, incremental, and continuous and have no impact on database performance.</mark>

- <mark style="background: #BBFABBA6;">When automated backups are turned on for your DB Instance, Amazon RDS automatically performs a full daily snapshot of your data</mark> (during your preferred backup window) and captures transaction logs (as updates to your DB Instance are made).
- Automated backups are enabled by default and data is stored on S3 and is equal to the size of the DB.
- Amazon RDS retains backups of a DB Instance for a limited, user-specified period called the retention period, which by default is 7 days but can be up to 35 days.

There are two methods to backup and restore RDS DB instances:
- Amazon RDS automated backups.
- User initiated manual backups.

Both options back up the entire DB instance and not just the individual DBs.

Both options create a storage volume snapshot of the entire DB instance.

You can make copies of automated backups and manual snapshots.

Automated backups backup data to multiple AZs to provide for data durability.

Multi-AZ backups are taken from the standby instance (for MariaDB, MySQL, Oracle, and PostgreSQL).

The DB instance must be in an Active state for automated backups to happen.

Only automated backups can be used for point-in-time DB instance recovery.

The granularity of point-in-time recovery is 5 minutes.

Amazon RDS creates a daily full storage volume snapshot and captures transaction logs regularly.

You can choose the backup window.

There is no additional charge for backups, but you will pay for storage costs on S3.

You can disable automated backups by setting the retention period to zero (0).

An outage occurs if you change the backup retention period from zero to a non-zero value or the other way around.

The retention period is the period AWS keeps the automated backups before deleting them.

Retention periods:

- By default the retention period is 7 days if configured from the console for all DB engines except Aurora.
- The default retention period is 1 day if configured from the API or CLI.
- The retention period for Aurora is 1 day regardless of how it is configured.
- You can increase the retention period up to 35 days.

During the backup window I/O may be suspended.

Automated backups are deleted when you delete the RDS DB instance.

Automated backups are only supported for InnoDB storage engine for MySQL (not for myISAM).

When you restore a DB instance the default DB parameters and security groups are applied – you must then apply the custom DB parameters and security groups.

You cannot restore from a DB snapshot into an existing DB instance.

Following a restore the new DB instance will have a new endpoint.

The storage type can be changed when restoring a snapshot.


![[Module 9 - Implementing Elasticity, High Availability, and Monitoring#Scaling with Amazon Aurora]]

><mark style="background: #083CA4A6;">Aurora supports On-Demand, Reserved, and Serverless pricing methods.</mark>

>Users must be authenticated and must have permissions to access tables in Aurora.  
>IAM policies can be used to assign permissions to users.  
>Security groups are used to control access to your database.  
>For more information, see [Amazon Aurora Security](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/Aurora.Overview.Security.html).

>Aurora Serverless manages database instances for you.  
><mark style="background: #FFF3A3A6;">Aurora can have up to 15 read replicas and is managed by Amazon RDS.</mark>  
>For more information on read replicas, see [Replication with Amazon Aurora](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/Aurora.Replication.html).

><mark style="background: #FFF3A3A6;">Aurora supports general purpose and memory-optimized instance classes. </mark>  
>It <mark style="background: #ADCCFFA6;">also supports the burstable performance instance feature</mark>.  
>For more information, see [Amazon RDS Instance Types](https://aws.amazon.com/rds/instance-types/).




# FAQ
## General

### What is Amazon Aurora?

[Amazon Aurora](https://aws.amazon.com/rds/aurora/) is a modern [relational database](https://aws.amazon.com/relational-database/) service <mark style="background: #BBFABBA6;">offering performance and high availability at scale, fully open-source MySQLand PostgreSQL-compatible editions, and a range of developer tools for building serverless and machine learning (ML)-driven applications. </mark>
  
<mark style="background: #FFB86CA6;">Aurora features a distributed, fault-tolerant, and self-healing storage system that is decoupled from compute resources and auto-scales up to 128 TiB per database instance. </mark>  
It delivers high performance and availability with up to 15 low-latency read replicas, point-in-time recovery, continuous backup to Amazon Simple Storage Service (Amazon S3), and replication across three Availability Zones (AZs).  
  
<mark style="background: #ADCCFFA6;">Aurora is also a fully managed service that automates time-consuming administration tasks such as hardware provisioning, database setup, patching, and backups while providing the security, availability, and reliability of commercial databases at one-tenth of the cost. </mark>

### Is Amazon Aurora MySQL Compatible?

Amazon Aurora is drop-in [compatible with existing MySQL](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/Aurora.AuroraMySQL.html) open-source databases and adds support for new releases regularly. This means <mark style="background: #CACFD9A6;">you can easily migrate MySQL databases to and from Aurora using standard import/export tools or snapshots</mark>.  
 It also means that most of the code, applications, drivers, and tools you already use with MySQL databases today can be used with Aurora with little or no change. This makes it easy to move applications between the two engines.

### Is Amazon Aurora PostgreSQL Compatible?

Amazon Aurora is drop-in [compatible with existing PostgreSQL](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/Aurora.AuroraPostgreSQL) open-source databases and adds support for new releases regularly. This means you can easily [migrate PostgreSQL databases to and from Aurora using standard import/export tools or snapshots](https://docs.aws.amazon.com/dms/latest/sbs/dms-sbs-welcome). It also means that most of the code, applications, drivers, and tools you already use with PostgreSQL databases today can be used with Aurora with [little or no change](https://aws.amazon.com/dms/pricing/).

You can see the current Amazon Aurora PostgreSQL release compatibility information in the [documentation](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/AuroraPostgreSQL.Updates.20180305).  

### How is Aurora PostgreSQL Supported for Issues Related to PostgreSQL Extensions?

Amazon fully supports Aurora PostgreSQL and all extensions available with Aurora. If you need support for Aurora PostgreSQL, reach out to AWS Support. If you have an active AWS Premium Support account, you can contact AWS Premium Support for Aurora specific issues.  

### How Do I Get Started with Aurora?

To try Aurora, sign in to the [AWS Management Console](https://console.aws.amazon.com/), select RDS under the Database category, and choose Amazon Aurora as your database engine. For detailed guidance and resources, check out our [Getting started with Aurora](https://aws.amazon.com/rds/aurora/getting-started/) page.  

### In Which AWS Regions is Aurora Available?

You can see Region availability for Aurora [here](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/Concepts.AuroraFeaturesRegionsDBEngines.grids).  

### How Can I Migrate from MySQL to Aurora and the other way Around?

If you want to migrate from MySQL to Aurora and the other way around, you have several options:  
- <mark style="background: #083CA4A6;">You can use the standard mysqldump utility to export data from MySQL and mysqlimport utility to import data to Aurora, and the other way around.</mark>
- You can also use [Amazon RDS DB Snapshot](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/AuroraMySQL.Migrating.RDSMySQL) migration feature to <mark style="background: #ABF7F7A6;">migrate an Amazon RDS for MySQL DB Snapshot to Aurora using the AWS Management Console.</mark>

Migration to Aurora completes for most customers in under an hour, though the duration depends on format and dataset size. For more information see [Best Practices for Migrating MySQL Databases to Amazon Aurora](https://d1.awsstatic.com/whitepapers/RDS/Migrating%20your%20databases%20to%20Amazon%20Aurora.pdf).  

### How Can I Migrate from PostgreSQL to Aurora and the other way Around?

If you want to migrate from PostgreSQL to Aurora and the other way around, you have several options:

- You can <mark style="background: #083CA4A6;">use the standard</mark> **pg\_dump utility** <mark style="background: #083CA4A6;">to export data from PostgreSQL</mark> and **pg\_restore utility** <mark style="background: #083CA4A6;">to import data to Aurora, and the other way around.</mark>
- You can also use [RDS DB Snapshot](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_CreateSnapshot) migration feature to <mark style="background: #ABF7F7A6;">migrate an Amazon RDS for PostgreSQL DB Snapshot to Aurora using the AWS Management Console.</mark>

**Migration to Aurora completes for most customers in under an hour**, though the duration depends on format and dataset size.

To migrate SQL Server databases to Amazon Aurora PostgreSQL-Compatible Edition, you can use [Babelfish for Aurora PostgreSQL](https://aws.amazon.com/rds/aurora/babelfish/). Your applications will work without any changes. See the [Babelfish documentation](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/babelfish.html) for more information.  

### Do I Need to Change Client Drivers to Use Amazon Aurora PostgreSQL-Compatible Edition?

No, Aurora works with standard PostgreSQL database drivers.  

## Performance

### What Does "five times the Performance of MySQL" Mean?

<mark style="background: #ABF7F7A6;">Amazon Aurora delivers significant increases over MySQL performance by tightly integrating the database engine with an SSD-based virtualized storage layer purpose-built for database workloads, reducing writes to the storage system, minimizing lock contention, and eliminating delays created by database process threads.</mark>

Our tests with SysBench on r3.8xlarge instances show that Amazon Aurora delivers over 500,000 SELECTs/sec and 100,000 UPDATEs/sec, five times higher than MySQL running the same benchmark on the same hardware. Detailed instructions on this benchmark and how to replicate it yourself are provided in the [Amazon Aurora MySQL-Compatible Edition Performance Benchmarking Guide](https://d1.awsstatic.com/product-marketing/Aurora/RDS_Aurora_Performance_Assessment_Benchmarking_v1-2.pdf).  

### What Does "three times the Performance of PostgreSQL" Mean?

Amazon Aurora delivers significant increases over PostgreSQL performance by tightly integrating the database engine with an _SSD-based virtualized storage layer_ purpose-built for database workloads, reducing writes to the storage system, minimizing lock contention, and eliminating delays created by database process threads.

Our tests with SysBench on r4.16xlarge instances show that Amazon Aurora delivers SELECTs/sec and UPDATEs/sec over three times higher than PostgreSQL running the same benchmark on the same hardware. Detailed instructions on this benchmark and how to replicate it yourself are provided in the [Amazon Aurora PostgreSQL-Compatible Edition Performance Benchmarking Guide](https://d1.awsstatic.com/product-marketing/Aurora/RDS_Aurora_PostgreSQL_Performance_Assessment_Benchmarking_V1-0.pdf).  

### How Do I Optimize My Database Workload for Amazon Aurora MySQL-Compatible Edition?

Amazon Aurora is designed to be compatible with MySQL so that existing MySQL applications and tools can run without requiring modification. However, [one area where Amazon Aurora improves upon MySQL is with highly concurrent workloads](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/AuroraMySQL.Managing.Performance). In order to maximize your workload’s throughput on Amazon Aurora, we recommend building your applications to drive a large number of concurrent queries and transactions.  

### How Do I Optimize My Database Workload for Amazon Aurora PostgreSQL-Compatible Edition?

Amazon Aurora is designed to be compatible with PostgreSQL so that existing PostgreSQL applications and tools can run without requiring modification. However, one area where Amazon Aurora improves upon PostgreSQL is with highly concurrent workloads. In order to maximize your workload’s throughput on Amazon Aurora, we recommend building your applications to drive a large number of concurrent queries and transactions.  

## Billing

### How much Does Aurora Cost?

See the [Aurora pricing page](https://aws.amazon.com/rds/aurora/pricing/) for current pricing information.  

### Does Aurora Participate in the AWS Free Tier?

There is no AWS Free Tier offering for Aurora at this time. However, Aurora durably stores your data across three Availability Zones in a Region and charges for only one copy of data. You are not charged for backups of up to 100% of the size of your database cluster. You are also not charged for snapshots during the backup retention period that you’ve configured for your database cluster.

### Aurora Replicates My Data across Three Availability Zones. Does that Mean that My effective Storage Price Will Be Three times what is Shown on the Pricing Page?

No, Aurora replication is bundled into the price. You are charged based on the storage your database consumes at the database layer, not the storage consumed in the virtualized storage layer of Aurora.  

### What Are I/O Operations in Aurora and how Are They Calculated?

I/O operations are performed by the Aurora database engine against its SSD-based virtualized storage layer. Every database page read operation counts as one I/O.  
The Aurora database engine issues reads against the storage layer to fetch database pages not present in memory in the cache:

- If your query traffic can be totally served from memory or the cache, you will not be charged for retrieving any data pages from memory.
- If your query traffic cannot be served entirely from memory, you will be charged for any data pages that need to be retrieved from storage.  
    Each database page is 16 KB in Amazon Aurora MySQL-Compatible Edition and 8 KB in Aurora PostgreSQL-Compatible Edition.

[Aurora was designed to remove unnecessary I/O operations](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/Aurora.Overview.StorageReliability.html) to reduce costs and ensure resources are available for serving read/write traffic. Write I/O operations are only consumed when persisting redo log records in Aurora MySQL-Compatible Edition or write ahead log records in Aurora PostgreSQL-Compatible Edition to the storage layer for the purpose of making writes durable.  
  
Write I/O operations are counted in 4 KB units. For example, a log record that is 1,024 bytes counts as one write I/O operation. However, if the log record is larger than 4 KB, more than one write I/O operation is needed to persist it.  
  
Concurrent write operations whose log records are less than 4 KB might be batched together by the Aurora database engine in order to optimize I/O consumption. Unlike traditional database engines, Aurora never flushes dirty data pages to storage.  
  
You can see how many I/O requests your Aurora instance is consuming by checking the AWS Management Console. To find your I/O consumption, go to the Amazon RDS section of the console, look at your list of instances, select your Aurora instances, then look for the “VolumeReadIOPs” and “VolumeWriteIOPs” metrics in the monitoring section.

For more information on the pricing of I/O operations, visit the [Aurora pricing page](https://aws.amazon.com/rds/aurora/pricing/). You are charged for read and write I/O operations when you configure your database clusters to the Aurora Standard configuration. You are not charged for read and write I/O operations when you configure your database clusters to Amazon Aurora I/O-Optimized.  

### What is Aurora Standard and Aurora I/O-Optimized?

Aurora offers you the flexibility to optimize your database spend by choosing between two configuration options based on your price-performance and price-predictability needs. The two configuration options are Aurora Standard and Aurora I/O-Optimized. Neither option requires upfront I/O or storage provisioning and both can scale I/O operations to support your most demanding applications.  
  
Aurora Standard is a database cluster configuration that offers cost-effective pricing for the vast majority of applications with low to moderate I/O usage. With Aurora Standard, you pay for database instances, storage, and pay-per-request I/O.  
  
Aurora I/O-Optimized is a database cluster configuration that delivers improved price performance for I/O-intensive applications such as payment processing systems, ecommerce systems, and financial applications. Also, if your I/O spend exceeds 25% of your total Aurora database spend, you can save up to 40% on costs for I/O-intensive workloads with Aurora I/O-Optimized. Aurora I/O-Optimized offers predictable pricing for all applications as there are no charges for read and write I/O operations, making this configuration ideal for workloads with high I/O variability.  

### When Should I Use Aurora I/O-Optimized?

Aurora I/O-Optimized is the ideal choice when you need predictable costs for any application. It delivers improved price performance for I/O-intensive applications, which require a high write throughput or run analytical queries processing large amounts of data. For customers with an I/O spend that exceeds 25% of their Aurora bill, you can save up to 40% on costs for I/O-intensive workloads with Aurora I/O-Optimized.  

### How Do I Migrate My Existing Database Cluster to Use Aurora I/O-Optimized?

You can use the one-click experience available in the AWS Management Console to change the storage type of your existing database clusters to be Aurora I/O-Optimized. You can also invoke the AWS Command Line Interface (AWS CLI) or AWS SDK to make this change.  

### Can I Switch back and forth between Aurora I/O-Optimized and Aurora Standard Configuration?

You can switch your existing database clusters once every 30 days to Aurora I/O-Optimized. You can switch back to Aurora Standard at any time.  

### Does Aurora I/O-Optimized Work with Reserved Instances?

Yes, Aurora I/O-Optimized works with existing Aurora Reserved Instances. Aurora automatically accounts for the price difference between Aurora Standard and Aurora I/O-Optimized with Reserved Instances. With Reserved Instance discounts with Aurora I/O-Optimized, you can gain even more savings on your I/O spend.  

### Does the Price of Backtrack, Snapshot, Export, or Continuous Backup Change with Aurora I/O-Optimized?

There are no changes to the price of backtrack, snapshot, export, or continuous backup with Aurora I/O-Optimized.  

### Do I Continue Paying for the I/O Operations Required for Replicating Data across Regions with Aurora Global Database with Aurora I/O-Optimized?

Yes, the charges for the I/O operations required to replicate data across Regions continue to apply. Aurora I/O-Optimized does not charge for read and write I/O operations, which is different from data replication.  

### What is the Cost for Amazon Aurora Optimized Reads for Aurora PostgreSQL?

There are no additional charges for Amazon Aurora Optimized Reads for Aurora PostgreSQL besides the price of Intel-based R6id and Graviton-based R6gd instances. For more information, visit the [Aurora pricing page](https://aws.amazon.com/rds/aurora/pricing/).

## Hardware and Scaling

### What Are the Minimum and Maximum Storage Limits of an Amazon Aurora Database?

The minimum storage is 10 GB. Based on your database usage, your Amazon Aurora storage will automatically grow, up to 128 TiB, in 10 GB increments with no impact to database performance. [There is no need to provision storage in advance](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/Aurora.Overview.StorageReliability).  

### How Do I Scale the Compute Resources Associated with My Amazon Aurora DB Instance?

There are two ways to scale the compute resources associated with my Amazon Aurora DB Instance – via Aurora Serverless and via manual adjustment.

You can use Aurora Serverless, an on-demand, autoscaling configuration for Amazon Aurora to scale database compute resources based on application demand. It enables you to run your database in the cloud without worrying about database capacity management. You can specify the desired database capacity range and your database will scale based on your application’s needs. Read more in the [Aurora Serverless User Guide](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/aurora-serverless-2.html).

You can also [manually scale](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/Aurora.Managing.Performance) your compute resources associated with your database by selecting the desired DB instance type in the AWS Management Console. Your requested change will be applied during your specified maintenance window or you can use the "Apply Immediately" flag to change the DB instance type immediately.

Both of these options will have an availability impact for a few minutes as the scaling operation is performed. Note that any other pending system changes will also be applied.  

## Backup and Restore

### How Do I Enable Backups for My DB Instance?

Automated continuous [backups](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/Aurora.Managing.Backups) are always enabled on Amazon Aurora DB Instances. Backups do not impact database performance.  

### Can I Take DB Snapshots and Keep Them around as long as I Want?

Yes, and there is no performance impact when taking snapshots. Note that restoring data from [DB Snapshots](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/USER_CreateSnapshotCluster) requires the creation of a new DB Instance.  

### If My Database Fails, what is My Recovery Path?

Amazon Aurora automatically makes your data durable across three Availability Zones (AZs)  in a Region and will automatically attempt to recover your database in a healthy AZ with no data loss. In the unlikely event your data is unavailable within Amazon Aurora storage, you can restore from a DB Snapshot or perform a point-in-time restore operation to a new instance. Note that the latest restorable time for a point-in-time restore operation can be up to five minutes in the past.  

### What Happens to My Automated Backups and DB Snapshots if I Delete My DB Instance?

You can choose to create a final DB Snapshot when deleting your DB Instance. If you do, you can use this DB Snapshot to restore the deleted DB Instance at a later date. Amazon Aurora retains this final user-created DB Snapshot along with all other manually created DB Snapshots after the DB Instance is deleted. Only DB Snapshots are retained after the DB Instance is deleted (i.e., automated backups created for point-in-time restore are not kept).  

### Can I Share My Snapshots with Another AWS Account?

Yes. Aurora gives you the ability to create snapshots of your databases, which you can use later to restore a database. You can share a snapshot with a different AWS account, and the owner of the recipient account can use your snapshot to restore a DB that contains your data. You can even choose to make your snapshots public – that is, anybody can restore a DB containing your (public) data.

You can use this feature to share data between your various environments (production, dev/test, staging, etc.) that have different AWS accounts, as well as keep backups of all your data secure in a separate account in case your main AWS account is ever compromised.  

### Will I Be Billed for Shared Snapshots?

There is no charge for sharing snapshots between accounts. However, you may be charged for the snapshots themselves, as well as any databases you restore from shared snapshots. Learn more about [Aurora pricing](https://aws.amazon.com/rds/aurora/pricing/).  

### Can I Automatically Share Snapshots?

We do not support automatic sharing of DB snapshots. To share a snapshot, you must manually create a copy of the snapshot, and then share the copy.  

### How Many Accounts Can I Share Snapshots With?

You may share manual snapshots with up to 20 AWS account IDs. If you want to share the snapshot with more than 20 accounts, you can either share the snapshot as public, or contact support for increasing your quota.  

### In Which Regions Can I Share My Aurora Snapshots?

You can share your Aurora snapshots within each AWS region where Aurora is available.  

### Can I Share My Aurora Snapshots across Different Regions?

No. Your shared Aurora snapshots will only be accessible by accounts in the same region as the account that shares them.  

### Can I Share an Encrypted Aurora Snapshot?

Yes, you can share encrypted Aurora snapshots.  

## High Availability and Replication

### How Does Amazon Aurora Improve My database’s Fault Tolerance to Disk Failures?

Amazon Aurora automatically divides your database volume into 10 GB segments spread across many disks. Each 10 GB chunk of your database volume is replicated six ways, across three AZs. Amazon Aurora is designed to transparently handle the loss of up to two copies of data without affecting database write availability and up to three copies without affecting read availability.

[Amazon Aurora storage is also self-healing](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/Aurora.Overview.StorageReliability). Data blocks and disks are continuously scanned for errors and repaired automatically.  

### How Does Aurora Improve Recovery time after a Database Crash?

Unlike other databases, after a database crash Amazon Aurora does not need to replay the redo log from the last database checkpoint (typically five minutes) and confirm that all changes have been applied before making the database available for operations. This reduces database restart times to less than 60 seconds in most cases.

Amazon Aurora moves the buffer cache out of the database process and makes it available immediately at restart time. This prevents you from having to throttle access until the cache is repopulated to avoid brownouts.  

### What Kind of Replicas Does Aurora Support?

Amazon Aurora MySQL-Compatible Edition and Amazon Aurora PostgreSQL-Compatible Edition support [Amazon Aurora replicas](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/Aurora.Replication), which share the same underlying volume as the primary instance in the same AWS region. Updates made by the primary are visible to all Amazon Aurora Replicas.

With Amazon Aurora MySQL-Compatible Edition, you can also create cross-region MySQL Read Replicas based on MySQL’s binlog-based replication engine. In MySQL [Read Replicas](https://aws.amazon.com/rds/features/read-replicas/), data from your primary instance is replayed on your replica as transactions. For most use cases, including read scaling and high availability, we recommend using Amazon Aurora Replicas.

You have the flexibility to mix and match these two replica types based on your application needs:  

| Feature | Amazon Aurora Replicas  
 | MySQL Replicas |  
| --- | --- | --- |  
| Number of replicas | Up to 15 | Up to 5 |  
| Replication type | Asynchronous (milliseconds) | Asynchronous (seconds) |  
| Performance impact on primary | Low | High |  
| Replica location | In-region  
 | Cross-region |  
| Act as failover target | Yes (no data loss) | Yes (potentially minutes of data loss) |  
| Automated failover | Yes | No |  
| Support for user-defined replication delay | No | Yes |  
| Support for different data or schema vs. primary | No | Yes |

You have two additional replication options in addition to the ones listed above. You can use [Amazon Global Database](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/aurora-global-database) for much faster physical replication between Aurora clusters in different regions. And for replication between Aurora and non-Aurora MySQL-Compatible Edition databases (even outside of AWS), you can set up your own, self-managed binlog replication.  

### Can I Have Cross-region Replicas with Amazon Aurora?

Yes, you can set up cross-region Aurora replicas using either physical or logical replication. Physical replication, called [Amazon Aurora Global Database](https://aws.amazon.com/rds/aurora/global-database/), uses dedicated infrastructure that leaves your databases entirely available to serve your application, and can replicate up to five secondary regions with typical latency of under a second. It's available for both Aurora MySQL-Compatible Edition and Aurora PostgreSQL-Compatible Edition.

**For low-latency global reads and disaster recovery, we recommend using Amazon Aurora Global Database.**  
Aurora supports native logical replication in each database engine (binlog for MySQL and PostgreSQL replication slots for PostgreSQL), so you can replicate to Aurora and non-Aurora databases, even across Regions.

Aurora MySQL-Compatible Edition also offers an easy-to-use logical cross-region read replica feature that supports up to five secondary AWS regions. It is based on single threaded MySQL binlog replication, so the replication lag will be influenced by the change/apply rate and delays in network communication between the specific regions selected.  

### Can I Create Aurora Replicas on the Cross-region Replica Cluster?

Yes, you can add up to 15 Aurora Replicas on each cross-region cluster, and they will share the same underlying storage as the cross-region replica. A cross-region replica acts as the primary on the cluster and the Aurora Replicas on the cluster will typically lag behind the primary by tens of milliseconds.  

### Can I Fail over My Application from My Current Primary to the Cross-region Replica?

Yes, you can promote your cross-region replica to be the new primary from the Amazon RDS console. For logical (binlog) replication, the promotion process typically takes a few minutes depending on your workload. The cross-region replication will stop once you initiate the promotion process.

With Amazon Aurora Global Database, you can promote a secondary region to take full read/write workloads in under a minute.  

### Can I Prioritize Certain Replicas as Failover Targets over Others?

Yes. You can assign a promotion priority tier to each instance on your cluster. When the primary instance fails, Amazon RDS will promote the replica with the highest priority to primary. If two or more Aurora Replicas share the same priority, then Amazon RDS promotes the replica that is largest in size. If two or more Aurora Replicas share the same priority and size, then Amazon RDS promotes an arbitrary replica in the same promotion tier.

For more information on failover logic, read the [Amazon Aurora User Guide](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/CHAP_AuroraOverview).  

### Can I Modify Priority Tiers for Instances after They Have Been Created?

Yes, you can modify the priority tier for an instance at any time. Simply modifying priority tiers will not trigger a failover.  

### Can I Prevent Certain Replicas from Being Promoted to the Primary Instance?

You can assign lower priority tiers to replicas that you don’t want promoted to the primary instance. However, if the higher priority replicas on the cluster are unhealthy or unavailable for some reason, then Amazon RDS will promote the lower priority replica.  

### How Can I Improve upon the Availability of a Single Amazon Aurora Database?

You can add Amazon Aurora Replicas. Aurora Replicas in the same AWS Region share the same underlying storage as the primary instance. Any Aurora Replica can be promoted to primary without any data loss, and therefore can be used to enhance fault tolerance in the event of a primary DB Instance failure.

To increase database availability, simply create one to 15 replicas, in any of three AZs, and Amazon RDS will automatically include them in failover primary selection in the event of a database outage. You can use Amazon Aurora Global Database if you want your database to span multiple AWS Regions. This will replicate your data with no impact on database performance and provide disaster recovery from region-wide outages.  

### What Happens during Failover and how long Does it Take?

Failover is handled automatically by Amazon Aurora so your applications can resume database operations as quickly as possible without manual administrative intervention.  

- If you have an Aurora Replica in the same or a different AZ when failing over, Aurora flips the canonical name record (CNAME) for your DB Instance to point at the healthy replica, which is promoted to become the new primary. Start-to-finish, failover typically completes within 30 seconds. For improved resiliency and faster failovers, consider using [Amazon RDS Proxy](https://aws.amazon.com/rds/proxy/) which automatically connects to the failover DB instance while preserving application connections. Proxy makes failovers transparent to your applications and reduces failover times by up to 66%.
- If you are running Aurora Serverless v1 and the DB instance or AZ become unavailable, Aurora will automatically recreate the DB instance in a different AZ. Aurora Serverless v2 works like provisioned for failover and other high availability features. For more information, see [Aurora Serverless v2 and high availability.](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/aurora-serverless-v2.how-it-works.html#aurora-serverless.ha). 
- If you do not have an Aurora Replica (i.e., single instance) and are not running Aurora Serverless, Aurora will attempt to create a new DB Instance in the same Availability Zone as the original instance. This replacement of the original instance is done on a best-effort basis and may not succeed, for example, if there is an issue that is broadly affecting the Availability Zone.  
    

Your application should retry database connections in the event of connection loss. Disaster recovery across regions is a manual process, where you promote a secondary region to take read/write workloads.  

### If I Have a Primary Database and an Amazon Aurora Replica Actively Taking Read Traffic and a Failover Occurs, what Happens?

Amazon Aurora will automatically detect a problem with your primary instance and trigger a failover. If you are using the Cluster Endpoint, your read/write connections will be automatically redirected to an Amazon Aurora Replica that will be promoted to primary.

In addition, the read traffic that your Aurora Replicas were serving will be briefly interrupted. If you are using the Cluster Reader Endpoint to direct your read traffic to the Aurora Replica, the read only connections will be directed to the newly promoted Aurora Replica until the old primary node is recovered as a replica.  

### How far behind the Primary Will My Replicas Be?

Since Amazon Aurora Replicas share the same data volume as the primary instance in the same AWS Region, there is virtually no replication lag. We typically observe lag times in the tens of milliseconds.

For cross-region replication, binlog-based logical replication lag can grow indefinitely based on change/apply rate as well as delays in network communication. However, under typical conditions, under a minute of replication lag is common. Cross-region replicas using Amazon Aurora Global Database’s physical replication will have a typical lag of under a second.  

### Can I Set up Replication between My Aurora MySQL-Compatible Edition Database and an External MySQL Database?

Yes, you can set up binlog replication between an Aurora MySQL-Compatible Edition instance and an external MySQL database. The other database can run on Amazon RDS, or as a self-managed database on AWS, or completely outside of AWS.  

If you're running Aurora MySQL-Compatible Edition 5.7, consider setting up GTID-based binlog replication. This will provide complete consistency so your replication won’t miss transactions or generate conflicts, even after failover or downtime.  

### What is Amazon Aurora Global Database?

[Amazon Aurora Global Database](https://aws.amazon.com/rds/aurora/global-database/) is a feature that allows a single Amazon Aurora database to span multiple AWS regions. It replicates your data with no impact on database performance, enables fast local reads in each Region with typical latency of less than a second, and provides disaster recovery from region-wide outages. In the unlikely event of a regional degradation or outage, a secondary region can be promoted to full read/write capabilities in less than one minute. This feature is available for both Aurora MySQL-Compatible Edition and Aurora PostgreSQL-Compatible Edition.  

### How Do I Create an Amazon Aurora Global Database?

You can create an Aurora Global Database with just a few clicks in the Amazon RDS console. Alternatively, you can use the AWS Software Development Kit (SDK) or AWS Command-Line Interface (CLI). You need to provision at least one instance per region in your Amazon Aurora Global Database.  

### How Many Secondary Regions Can an Amazon Aurora Global Database Have?

You can create up to five secondary regions for an Amazon Aurora Global Database.  

### If I Use Amazon Aurora Global Database, Can I also Use Logical Replication (binlog) on the Primary Database?

Yes. If your goal is to analyze database activity, consider using Aurora advanced auditing, general logs, and slow query logs instead, to avoid impacting the performance of your database.  

### Will Aurora Automatically Fail over to a Secondary Region of an Amazon Aurora Global Database?

No. If your primary region becomes unavailable, you can manually remove a secondary region from an Amazon Aurora Global Database and promote it to take full reads and writes. You will also need to point your application to the newly promoted region.  

## Security

### Can I Use Amazon Aurora in Amazon Virtual Private Cloud (Amazon VPC)?

Yes, all Amazon Aurora DB Instances must be created in a VPC. With Amazon VPC, you can define a virtual network topology that closely resembles a traditional network you might operate in your own datacenter. This gives you complete control over who can access your Amazon Aurora databases.  

### Does Amazon Aurora Encrypt My Data in Transit and at Rest?

Yes. Amazon Aurora uses SSL (AES-256) to secure the connection between the database instance and the application. Amazon Aurora allows you to encrypt your databases using keys you manage through [AWS Key Management Service](https://aws.amazon.com/kms/) (AWS KMS).

On a database instance running with Amazon Aurora encryption, data stored at rest in the underlying storage is encrypted, as are its automated backups, snapshots, and replicas in the same cluster. Encryption and decryption are handled seamlessly. For more information about the use of AWS KMS with Amazon Aurora, see the [Amazon RDS User's Guide](http://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Overview.Encryption).  

### Can I Encrypt an Existing Unencrypted Database?

Currently, encrypting an existing unencrypted Aurora instance is not supported. To use Amazon Aurora encryption for an existing unencrypted database, create a new DB Instance with encryption enabled and migrate your data into it.  

### How Do I Access My Amazon Aurora Database?

Aurora databases must be accessed through the database port entered on database creation. This provides an additional layer of security for your data. Step-by-step instructions on how to connect to your Amazon Aurora database are provided in the [Amazon Aurora Connectivity Guide](https://d1.awsstatic.com/product-marketing/Aurora/RDS_Aurora_Connectivity_Guide_v5-2.pdf).  

### Can I Use Amazon Aurora with Applications that Require HIPAA Compliance?

Yes, the MySQLand PostgreSQL-compatible editions of Aurora are [HIPAA-eligible](https://aws.amazon.com/compliance/hipaa-eligible-services-reference/). You can use them to build HIPAA-compliant applications and store healthcare-related information, including protected health information (PHI) under an executed Business Associate Addendum (BAA) with AWS. If you have already entered into a BAA with AWS, no further action is necessary to begin using these services in the account(s) covered by your BAA. For more information about using AWS to build compliant applications, see [Healthcare Providers](https://aws.amazon.com/health/providers/).  

### Where Can I Access a List of Common Vulnerabilities and Exposures (CVE) Entries for Publicly Known Cybersecurity Vulnerabilities for Amazon Aurora Releases?

You can currently find a list of CVEs at [Amazon Aurora Security Updates](https://aws.amazon.com/rds/aurora/faqs1/security-updates/).  

### How Can I Detect Security Threats to My Aurora Database?

Aurora is integrated with [Amazon GuardDuty](https://aws.amazon.com/guardduty) to help you identify potential threats to data stored in Aurora databases. GuardDuty RDS Protection profiles and monitors login activity and new databases in your account, and uses tailored ML models to detect suspicious logins to Aurora databases. For more information, see [Monitoring threats with GuardDuty RDS Protection](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/guard-duty-rds-protection.html) and the [GuardDuty RDS Protection User Guide](https://docs.aws.amazon.com/guardduty/latest/ug/rds-protection.html).

## Serverless

### What is Amazon Aurora Serverless?

Aurora Serverless is an on-demand, auto-scaling configuration for [Amazon Aurora](https://aws.amazon.com/rds/aurora/). With Aurora Serverless, you can run your database in the cloud without managing database capacity. Manually managing database capacity can be time consuming and lead to inefficient use of database resources. With Aurora Serverless, you create a database, specify the desired database capacity range, and connect your application. Aurora automatically adjusts the capacity within the range specified based on your application’s needs.

You pay on a per-second basis for the database capacity you use when the database is active. Learn more about [Aurora Serverless](https://aws.amazon.com/rds/aurora/serverless/) and get started in a few steps in the [Amazon RDS Management Console](https://console.aws.amazon.com/rds/).  

### What is the Difference between Aurora Serverless V2 and V1?

[Aurora Serverless v2](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/aurora-serverless-v2.html) supports every type of database workload, from development and test environments, websites, and applications that have infrequent, intermittent, or unpredictable workloads to the most demanding, business critical applications that require high scale and high availability. It scales in place by adding more CPU and memory without having to failover the database to a larger or smaller database instance. As a result, it can scale even when there are long running transactions, table locks, and more.

In addition, it scales database capacity in increments as small as 0.5 Aurora Capacity Units (ACUs) so your database capacity closely matches your application’s needs.

[Aurora Serverless v1](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/aurora-serverless) is a simple, cost-effective option for infrequent, intermittent, or unpredictable workloads. It automatically starts up, scales compute capacity to match your application's usage, and shuts down when it's not in use. Visit the [Aurora User Guide](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/aurora-serverless-v2.upgrade.html#aurora-serverless-v2.move-from-serverless-v1) to learn more.  

### Which Aurora Features Does Aurora Serverless V2 Support?

[Aurora Serverless v2](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/aurora-serverless-2.how-it-works.html) supports all features of provisioned Aurora, including [read replica](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/Aurora.Replication), [Multi-AZ configuration](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/Concepts.AuroraHighAvailability), [Aurora Global Database](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/aurora-global-database), [RDS Proxy](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/rds-proxy), and [Performance Insights](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/USER_PerfInsights).

### Can I Start Using Aurora Serverless V2 with Provisioned Instances in My Existing Aurora DB Cluster?

Yes, you can start using Aurora Serverless v2 to manage database compute capacity in your existing Aurora DB cluster. A cluster containing both provisioned instances as well as Aurora Serverless v2 is referred to as a mixed-configuration cluster. You can choose to have any combination of provisioned instances and Aurora Serverless v2 in your cluster.

To test Aurora Serverless v2, you add a reader to your Aurora DB cluster and select Serverless v2 as the instance type. Once the reader is created and available, you can start using it for read-only workloads. Once you confirm that the reader is working as expected, you can initiate a failover to start using Aurora Serverless v2 for both reads and writes. This option provides a minimal downtime experience to get started with Aurora Serverless v2.  

### Can I Migrate from Aurora Serverless V1 to Aurora Serverless V2?

Yes, you can migrate from Aurora Serverless v1 to Aurora Serverless v2. Refer to the [Aurora User Guide](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/aurora-serverless-v2.upgrade) to learn more.  

### Which Versions of Amazon Aurora Are Supported for Aurora Serverless?

[Aurora Serverless v1 compatibility information can be seen here](https://docs.amazonaws.cn/en_us/AmazonRDS/latest/AuroraUserGuide/aurora-serverless.relnotes). [Aurora Serverless v2 compatibility information can be seen here](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/aurora-serverless-v2.requirements).  

### Can I Migrate an Existing Aurora DB Cluster to Aurora Serverless?

Yes, you can restore a snapshot taken from an existing Aurora provisioned cluster into an Aurora Serverless DB Cluster and the other way around.  

### How Do I Connect to an Aurora Serverless DB Cluster?

You access an Aurora Serverless DB cluster from within a client application running in the same VPC. You can't give a public IP address to an Aurora Serverless DB.  

### Can I Explicitly Set the Capacity of an Aurora Serverless Cluster?

While Aurora Serverless automatically scales based on the active database workload, in some cases, capacity might not scale fast enough to meet a sudden workload change, such as a large number of new transactions. In these cases, you can set the capacity explicitly to a specific value with the AWS Management Console, the AWS CLI, or the Amazon RDS API.  

### Why Isn't My Aurora Serverless DB Cluster Automatically Scaling?

Once a scaling operation is initiated, Aurora Serverless attempts to find a scaling point, which is a point in time at which the database can safely complete scaling. Aurora Serverless might not be able to find a scaling point if you have long-running queries or transactions in progress, or temporary tables or table locks in use.  

### How Am I Billed for Aurora Serverless?

In Aurora Serverless, database capacity is measured in ACUs. You pay a flat rate per second of ACU usage. Compute costs for running your workloads on Aurora Serverless will depend on the database cluster configuration that you choose: Aurora Standard or Aurora I/O-Optimized. Visit the [Aurora pricing page](https://aws.amazon.com/rds/aurora/pricing/) for information about pricing and Regional availability.  

## Parallel Query

### What is Amazon Aurora Parallel Query?

[Amazon Aurora Parallel Query](https://aws.amazon.com/rds/aurora/parallel-query/) refers to the ability to push down and distribute the computational load of a single query across thousands of CPUs in Aurora’s storage layer. Without Parallel Query, a query issued against an Amazon Aurora database would be executed wholly within one instance of the database cluster; this would be similar to how most databases operate.  

### What's the Target Use Case?

Parallel Query is a good fit for analytical workloads requiring fresh data and good query performance, even on large tables. Workloads of this type are often operational in nature.  

### What Benefits Does Parallel Query Provide?

Parallel Query results in faster performance, speeding up analytical queries by up to two orders of magnitude. It also delivers operational simplicity and data freshness as you can issue a query directly over the current transactional data in your Aurora cluster. And, Parallel Query enables transactional and analytical workloads on the same database by allowing Aurora to maintain high transaction throughput alongside concurrent analytical queries.  

### What Specific Queries Improve under Parallel Query?

Most queries over large data sets that are not already in the buffer pool can expect to benefit. The initial version of Parallel Query can push down and scale out of the processing of more than 200 SQL functions, equijoins, and projections.  

### What Performance Improvement Can I Expect?

The improvement to a specific query’s performance depends on how much of the query plan can be pushed down to the Aurora storage layer. Customers have reported more than an order of magnitude improvement to query latency.  

### Is there Any Chance that Performance Will Be Slower?

Yes, but we expect such cases to be rare.  

### What Changes Do I Need to Make to My Query to Take Advantage of Parallel Query?

Changes in query syntax are not required. The query optimizer will automatically decide whether to use Parallel Query for your specific query. To check if a query is using Parallel Query, you can view the query execution plan by running the EXPLAIN command. If you wish to bypass the heuristics and force Parallel Query for test purposes, use the aurora\_pq\_force session variable.  

### How Do I Turn Parallel Query Feature on or Off?

Parallel Query can be enabled and disabled dynamically at both the global and session level using the aurora\_pq parameter.  

### Are there Any Additional Charges Associated with Using Parallel Query?

No. You aren’t charged for anything other than what you already pay for instances, I/O, and storage.  

### Since Parallel Query Reduces I/O, Will Turning it on Reduce My Aurora IO Charges?

No, Parallel Query I/O costs for your query are metered at the storage layer, and will be the same or larger with Parallel Query turned on. Your benefit is the improvement in query performance.

There are two reasons for potentially higher I/O costs with Parallel Query. First, even if some of the data in a table is in the buffer pool, Parallel Query requires all data to be scanned at the storage layer, incurring I/O. Second, a side effect of avoiding contention in the buffer pool is that running a Parallel Query does not warm up the buffer pool. As a result, consecutive runs of the same Parallel Query query will incur the full I/O cost.

Learn more about [Parallel Query in the Documentation](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/aurora-mysql-parallel-query).  

### Is Parallel Query Available with All Instance Types?

No. At this time, you can use Parallel Query with instances in the R\* instance family.  

### What Versions of Amazon Aurora Support Parallel Query?

Parallel Query is available for the MySQL 5.7 and MySQL 8.0 compatible version of Amazon Aurora.

### Is Parallel Query Compatible with All other Aurora Features?

Parallel Query is compatible with Aurora Serverless v2 and Backtrack.

### If Parallel Query Speeds up Queries with only Rare Performance Losses, Should I Simply Turn it on All the Time?

No. While we expect Parallel Query to improve query latency in most cases, you may incur higher I/O costs. We recommend that you thoroughly test your workload with the feature enabled and disabled. Once you're convinced that Parallel Query is the right choice, you can rely on the query optimizer to automatically decide which queries will use Parallel Query. In the rare case when the optimizer doesn’t make the optimal decision, you can override the setting.  

### Can Aurora Parallel Query Replace My Data Warehouse?

Aurora Parallel Query is not a data warehouse and doesn’t provide the functionality typically found in such products. It’s designed to speed up query performance on your relational database and is suitable for use cases such as operational analytics, when you need to perform fast analytical queries on fresh data in your database.

For an exabyte scale cloud data warehouse, please consider [Amazon Redshift](https://aws.amazon.com/pm/redshift/).  

## Optimized Reads

### What is Amazon Aurora Optimized Reads for Aurora PostgreSQL?

[Amazon Aurora Optimized Reads](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/AuroraPostgreSQL.optimized.reads.html) available for Aurora PostgreSQL is a new price-performance option that delivers up to 8x improved query latency and up to 30% cost savings compared to instances without it. It is ideal for applications with large datasets that exceed the memory capacity of a database instance.

### How Do Amazon Aurora Optimized Reads for Aurora PostgreSQL Improve Query Performance?

Amazon Aurora Optimized Reads instances use local NVMe-based SSD block-level storage (available on Graviton-based r6gd and Intel-based r6id instances) to improve query latency of applications with data sets exceeding the memory capacity of a database instance. Optimized Reads includes performance enhancements such as tiered caching and temporary objects.

Tiered caching delivers up to 8x improved query latency and up to 30% cost savings for read-heavy, I/O-intensive applications such as operational dashboards, anomaly detection, and vector-based similarity searches. These benefits are realized by automatically caching data evicted from the in-memory database buffer cache onto local storage to speed up subsequent accesses of that data. Tiered caching is only available for Amazon Aurora PostgreSQL-Edition with the Aurora I/O-Optimized configuration.

Temporary objects achieve faster query processing by placing temporary tables generated by Aurora PostgreSQL on local storage, improving the performance of queries involving sorts, hash aggregations, high-load joins, and other data-intensive operations.

### When Should I Use Amazon Aurora Optimized Reads for Aurora PostgreSQL?

[Amazon Aurora Optimized Reads](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/AuroraPostgreSQL.optimized.reads.html) for Aurora PostgreSQL offers customers with latency-sensitive applications and large working sets a compelling price-performance alternative to meet their business SLAs and do even more with their instances.

### Which Database Instance Types Support Amazon Aurora Optimized Reads for Aurora PostgreSQL? In what Regions Are They Available?

Amazon Aurora Optimized Reads is available on Intel-based R6id and Graviton-based R6gd instances. You can see Region availability for Aurora [here](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/Concepts.AuroraFeaturesRegionsDBEngines.grids).

### What Engine Versions of Amazon Aurora Does Aurora Optimized Reads for Aurora PostgreSQL Support?

Amazon Aurora Optimized Reads is available for the PostgreSQL-Compatible Edition of Aurora on R6id and R6gd instances. Supported engine versions are 15.4 and higher and 14.9 and higher on Aurora PostgreSQL.

### Can I Use Amazon Aurora Optimized Reads for Aurora PostgreSQL with Aurora Serverless V2?

Amazon Aurora Optimized Reads is unavailable on Aurora Serverless v2 (ASv2).

### Can I Use Amazon Aurora Optimized Reads for Aurora PostgreSQL with Aurora Standard and Aurora I/O-Optimized Configurations?

Yes, Amazon Aurora Optimized Reads is available with both configurations. On both configurations, Optimized Reads-enabled instances automatically map temporary tables to the NVMe-based local storage to improve the performance of analytical queries and index rebuilds.

For I/O intensive workloads which are read heavy, Optimized Reads-enabled instances on Aurora PostgreSQL configured to use Aurora I/O-Optimized automatically cache data evicted from memory on NVMe-based local storage to deliver up to 8x improved query latency and up to 30% cost savings compared to instances without it, for applications with large datasets that exceed the memory capacity of a database instance.

### How Do I Get Started with Amazon Aurora Optimized Reads for Aurora PostgreSQL?

Customers can get started with Amazon Aurora Optimized Reads through the AWS Management Console, CLI, and SDK. Optimized Reads is available on all R6id and R6gd instances by default. To use this capability, customers can simply modify their existing Aurora database clusters to include R6id and R6gd instances, or create new database clusters using these instances. See the [Amazon Aurora Optimized Reads documentation](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/AuroraPostgreSQL.optimized.reads.html) to get started.

### How much of the Available Local Storage is Available for Amazon Aurora Optimized Reads for Aurora PostgreSQL?

Approximately 90% of the available local storage on R6id and R6gd instances is available for Optimized Reads, Aurora reserves 10% of the NVMe storage to reduce the impact of SSD write amplification. The allocation of the available storage depends on which Optimized Reads features are enabled.

When using Optimized Reads with both the Temporary Objects and the Tiered Caching features, the space available for temporary objects in local storage is equivalent to 2x the size of memory available on these database instances. This matches the current size of temporary object storage on Aurora PostgreSQL. The remaining local storage diskspace is available for caching data.

When using Optimized Reads only with the Temporary Objects feature, all available local storage diskspace is available for temporary objects. For example, when using an r6gd.8xlarge instance with both the Temporary Objects and Tiered Caching features, 534 GiB (2x memory capacity) are reserved for temporary objects, and 1054 GiB for tiered cache.

### What Happens in the case of Local Storage Failure?

If the local storage fails, Aurora automatically performs a host replacement. In a multi-node database cluster, this triggers an in-region failover.

### How Does Amazon Aurora Optimized Reads for Aurora PostgreSQL Impact Query Latency in the Event of a Database Failover?

In the event of a database failover, the query latency will temporarily increase after failover. This latency increase will reduce over time and eventually catch up to the query latency prior to failover. This catch-up duration can be expedited by enabling [cluster cache management (CCM)](https://docs.aws.amazon.com/prescriptive-guidance/latest/ccm-and-qpm-aurora-postgresql/cluster-cache-management.html). With CCM, customers can designate a specific Aurora PostgreSQL database instance as the failover target.

When CCM is enabled, the local storage cache of the designated failover target closely mirrors the local storage cache of the primary instance, reducing the catch-up time post failover. However, enabling CCM could impact the long-term efficacy of the local storage cache if the designated failover target is also being used to serve a read workload separate from the workload on the writer instance.

Therefore, customers running workloads that require a reader to be designated as the stand-by failover must enable CCM to increase their likelihood of quickly regaining their query latency post failover. Customers running separate workloads on their designated failover targets may want to balance their needs for immediate latency recovery post failover with long term effectiveness of the cache performance, prior to enabling CCM.

## Generative AI

### What is Pgvector?

pgvector is an open-source extension for PostgreSQL supported by Amazon Aurora PostgreSQL-Compatible Edition.

### What Capabilities Does Pgvector Enable for Aurora PostgreSQL?

You can use pgvector to store, search, index, and query billions of embeddings that are generated from machine learning (ML) and artificial intelligence (AI) models in your database, such as those from Amazon Bedrock (limited preview) or Amazon SageMaker. A vector embedding is a numerical representation that represents the semantic meaning of content such as text, images, and video.

With pgvector, you can query embeddings in your Aurora PostgreSQL database to perform efficient semantic similarity searches of these data types, represented as vectors, combined with other tabular data in Aurora. This enables the use of generative AI and other AI/ML systems for new types of applications such as personalized recommendations based on similar text descriptions or images, candidate match based on interview notes, customer service next best action recommendations based on successful transcripts or chat session dialogs, and more. 

Read our [blog on vector database capabilities](https://aws.amazon.com/blogs/database/leverage-pgvector-and-amazon-aurora-postgresql-for-natural-language-processing-chatbots-and-sentiment-analysis/) and learn how to store embeddings using the pgvector extension in an Aurora PostgreSQL database, create an interactive question answering chatbot, and use the native integration between pgvector and [Aurora machine learning](https://aws.amazon.com/rds/aurora/machine-learning/) for sentiment analysis.

### Does Pgvector Work with Aurora Machine Learning?

Yes. [Aurora machine learning](https://aws.amazon.com/rds/aurora/machine-learning/) (ML) exposes ML models as SQL functions, allowing you to use standard SQL to call ML models, pass data to them, and return predictions as query results. pgvector requires vector embeddings to be stored in the database, which requires running the ML model on source text or image data to generate embeddings and then moving the embeddings in batch into Aurora PostgreSQL.

Aurora ML can make this a real-time process enabling embeddings to be kept up-to-date in Aurora PostgreSQL by making periodic calls to [Amazon SageMaker](https://aws.amazon.com/sagemaker/) which returns the most recent embeddings from your model.

### How Does Aurora Optimized Reads for Aurora PostgreSQL Help with Pgvector Performance?

Amazon Aurora PostgreSQL Optimized Reads with [pgvector](https://aws.amazon.com/rds/aurora/faqs/#Generative_AI) increases queries per second for vector search by up to 9x in workloads that exceed available instance memory. This is possible due to the tiered caching capability available in Optimized Reads that automatically caches data evicted from the in-memory database buffer cache onto local storage to speed up subsequent accesses of that data.

## Zero-ETL Integrations

### When Should I Use Aurora zero-ETL Integration with Amazon Redshift?

You should use [Amazon Aurora zero-ETL integration with Amazon Redshift](https://aws.amazon.com/rds/aurora/zero-etl/) when you need near real-time access to transactional data. This integration allows you to take advantage of Amazon Redshift ML with straightforward SQL commands.

### What Engines and Versions of Aurora Support zero-ETL Integrations?

Aurora zero-ETL integration with Amazon Redshift is available on the Aurora MySQL-Compatible Edition for Aurora MySQL 3.05 version (compatible with MySQL 8.0.32) and higher in the US East (Ohio), US East (N. Virginia), US West (Oregon), Asia Pacific (Singapore), Asia Pacific (Sydney), Asia Pacific (Tokyo), Europe (Frankfurt), Europe (Ireland), and Europe (Stockholm) Regions. Aurora zero-ETL integration with Amazon Redshift is available on the Aurora PostgreSQL-Compatible Edition for Aurora PostgreSQL 15.4 in the [US East (Ohio) Region](https://us-east-2.console.aws.amazon.com/rds-preview/home?region=us-east-2).  

### What Benefits Does zero-ETL Integration Provide?

[Aurora zero-ETL integration with Amazon Redshift](https://aws.amazon.com/rds/aurora/zero-etl/) removes the need for you to build and maintain complex data pipelines. You can consolidate data from a single or multiple Aurora database clusters to a single Amazon Redshift database cluster and run near real-time analytics and ML using Amazon Redshift on petabytes of transactional data from Aurora. 

### Is zero-ETL Integration Compatible with Aurora Serverless V2?

[Aurora zero-ETL integration with Amazon Redshift](https://aws.amazon.com/rds/aurora/zero-etl/) is compatible with Aurora Serverless v2. When using both [Aurora Serverless v2](https://aws.amazon.com/rds/aurora/serverless/) and [Amazon Redshift Serverless](https://aws.amazon.com/redshift/redshift-serverless/) you can generate near real-time analytics on transactional data without having to manage any infrastructure for data pipelines.

### How Do I Start a zero-ETL Integration?

You can get started by using the Amazon RDS console to create the zero-ETL integration by specifying the Aurora source and Amazon Redshift destination. Once the integration has been created, the Aurora database will be replicated to Amazon Redshift and you can start querying the data once initial seeding is completed. For more information, read the getting started guide for [Aurora zero-ETL integrations with Amazon Redshift](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/zero-etl.html).

### How much Does zero-ETL Integration Cost?

Zero-ETL and ongoing processing of data changes is offered at no additional charges. You pay for existing Amazon RDS and Amazon Redshift resources used to create and process the change data generated as part of a zero-ETL integration. These resources could include:

- Additional [I/O and storage](https://aws.amazon.com/rds/aurora/faqs/#What_are_I.2FO_operations_in_Aurora_and_how_are_they_calculated.3F) used by enabling enhanced binlog
- [Snapshot export costs](https://aws.amazon.com/rds/aurora/pricing/#Snapshotorclusterexportcosts) for the initial data export to seed your Amazon Redshift databases
- Additional Amazon Redshift storage for storing replicated data
- Cross-AZ [data transfer costs](https://aws.amazon.com/rds/aurora/pricing/#datatransfercosts) for moving data from source to target

For more information, visit the [Aurora pricing page](https://aws.amazon.com/rds/aurora/pricing/).

## Amazon DevOps Guru for RDS

### What is Amazon DevOps Guru for RDS?

[Amazon DevOps Guru for RDS](https://aws.amazon.com/devops-guru/features/devops-guru-for-rds/) is a new ML-powered capability for [Amazon RDS](https://aws.amazon.com/rds/) (which includes Amazon Aurora) that is designed to automatically detect and diagnose database performance and operational issues, enabling you to resolve issues in minutes rather than days.

Amazon DevOps Guru for RDS is a feature of [Amazon DevOps Guru](https://docs.aws.amazon.com/devops-guru/latest/userguide/welcome.html), which is designed to detect operational and performance issues for all Amazon RDS engines and dozens of other resource types. DevOps Guru for RDS expands the capabilities of DevOps Guru to detect, diagnose, and remediate a wide variety of database-related issues in Amazon RDS (e.g. resource over-utilization, and misbehavior of certain SQL queries).

When an issue occurs, Amazon DevOps Guru for RDS is designed to immediately notify developers and DevOps engineers and provides diagnostic information, details on the extent of the problem, and intelligent remediation recommendations to help customers quickly resolve database-related performance bottlenecks and operational issues.  

### Why Should I Use DevOps Guru for RDS?

Amazon DevOps Guru for RDS is designed to remove manual effort and shorten time (from hours and days to minutes) to detect and resolve hard to find performance bottlenecks in your relational database workload.

You can enable DevOps Guru for RDS for every Amazon Aurora database, and it will automatically detect performance issues for your workloads, send alerts to you on each issue, explain findings, and recommend actions to resolve.  
DevOps Guru for RDS helps make database administration more accessible to non-experts and assists database experts so that they can manage even more databases.  

### How Does Amazon DevOps Guru for RDS Work?

Amazon DevOps Guru for RDS uses ML to analyze telemetry data collected by [Amazon RDS Performance Insights](https://aws.amazon.com/rds/performance-insights/) (PI). DevOps Guru for RDS does not use any of your data stored in the database in its analysis. [PI measures database load](https://aws.amazon.com/rds/performance-insights/faqs/), a metric that characterizes how an application spends time in the database and selected metrics generated by the database, such as server status variables in MySQL and pg\_stat tables in PostgreSQL.  

### How Can I Get Started with Amazon DevOps Guru for RDS?

To get started with DevOps Guru for RDS, ensure [Performance Insights](https://aws.amazon.com/rds/performance-insights/) is enabled through the RDS console, and then simply enable DevOps Guru for your Amazon Aurora databases. With DevOps Guru, you can choose your analysis coverage boundary to be your entire AWS account, prescribe the specific [AWS CloudFormation](https://aws.amazon.com/cloudformation/) stacks that you want DevOps Guru to analyze, or use AWS tags to create the resource grouping you want DevOps Guru to analyze.  

### What Types of Issues Can Amazon DevOps Guru for RDS Detect?

Amazon DevOps Guru for RDS helps identify a wide range of performance issues that may affect application service quality, such as lock pile-ups, connection storms, SQL regressions, CPU and I/O contention, and memory issues.  

### How is DevOps Guru for RDS Different from Amazon RDS Performance Insights?

[Amazon RDS Performance Insights](https://aws.amazon.com/rds/performance-insights/) is a database performance tuning and monitoring feature that collects and visualizes Amazon RDS database performance metrics, helping you quickly assess the load on your database, and determine when and where to take action. Amazon DevOps Guru for RDS is designed to monitor those metrics, detect when your database is experiencing performance issues, analyze the metrics, and then tell you what’s wrong and what you can do about it.  

## Data API

### When Should I Use Data API with Aurora instead of Database Drivers?

You should use [Data API](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/data-api.html) for new modern applications, particularly those built with [AWS Lambda](https://aws.amazon.com/lambda/) that need to access Aurora in a request/response model. You should use database drivers instead of Data API and manage persistent database connections when an existing application is highly coupled with database drivers, when there are long-running queries, or when the developer wants to take advantage of database features such as temporary tables or use session variables.

### What Aurora Engines and Versions Support Data API?

Data API AWS Region and database version availability for [Aurora Serverless v2](https://aws.amazon.com/rds/aurora/serverless/) and Aurora provisioned instances may be found in our [documentation](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/data-api.html). Customers currently using Data API for Aurora Serverless v1 are encouraged to migrate to Aurora Serverless v2 to take advantage of the redesigned Data API and the more granular scaling of Aurora Serverless v2.

### What Benefits Does Data API Provide?

Data API will enable you to simplify and accelerate modern application development. Data API is an easy-to-use secure HTTP based API that eliminates the need to deploy database drivers, manage client-side connection pools, or set up complex VPC networking between the application and the database. Data API also improves scalability by automatically pooling and sharing database connections, which reduces computational overhead from applications that open and close connections frequently.   

### Does Data API Support Aurora Global Database or Aurora Serverless V1?

The existing Data API for Aurora Serverless v1 will remain a feature of Aurora Serverless v1 for both the PostgreSQL-Compatible Edition and MySQL-Compatible Edition of Aurora. Data API for Aurora Serverless v2 and Aurora provisioned instances does not support Aurora Serverless v1. Data API for Aurora Serverless v2 and Aurora provisioned instances support Aurora Global Database writer instances.  

### How Do I Authenticate with the Database Using Data API?

Users can invoke Data API operations only if they are authorized to do so. Administrators can give a user permission to use the Data API by attaching an [AWS Identity and Access Management (IAM)](https://aws.amazon.com/iam/) policy that defines their privileges. You can also attach the policy to a role if you're using IAM roles. When you call the Data API, you can pass credentials for the Aurora DB cluster by using a secret in [AWS](https://aws.amazon.com/secrets-manager/) [Secrets Manager](https://aws.amazon.com/secrets-manager/). 

### How much Does Data API Cost?

Data API usage with Aurora Serverless v1 remains available at no additional charge. Data API for Aurora Serverless v2 and Aurora provisioned instances is priced by API request volume as described on the [Aurora pricing page](https://aws.amazon.com/rds/aurora/pricing/). Data API for Aurora Serverless v2 and Aurora provisioned instances uses AWS CloudTrail data plane events to log activity instead of management events, as was the case with Data API for Aurora Serverless v1.

You may enable data events logging through the CloudTrail console, CLI, or SDK if you want to track this activity. This will incur charges as set forth on the [CloudTrail pricing page](https://aws.amazon.com/cloudtrail/pricing/). Additionally, the use of AWS Secrets Manager will incur charges as set forth on the [AWS Secrets Manager pricing page](https://aws.amazon.com/secrets-manager/pricing/). 

### Why Did AWS Begin Using Data Plane Events for Data API instead of CloudTrail Management Events?

[AWS CloudTrail](https://aws.amazon.com/pm/cloudtrail/) captures AWS API activity as management events or data events. CloudTrail management events (also known as "control plane operations") show management operations that are performed on resources in your AWS account, such as create, update, and delete a resource. CloudTrail data events (also known as "data plane operations") show the resource operations performed on or within a resource in your AWS account.

Data API performs data plane operations since it performs queries on data within your Aurora database. Therefore, we will be logging Data API activity as data events as this is the correct categorization of the events. Charges will only be incurred for CloudTrail data events if you enable data events logging.

### Does Data API Have a Free Tier?

Yes, the Data API free tier includes one million requests per month, aggregated across all AWS Regions, for the first year’s usage. After one year, customers will begin paying for Data API as described on the [Aurora pricing page](https://aws.amazon.com/rds/aurora/pricing/).

## Amazon RDS Blue/Green Deployments

### What Versions Do Amazon RDS Blue/Green Deployments Support?

[Amazon RDS Blue/Green Deployments](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/blue-green-deployments.html) are available in Amazon Aurora MySQL-Compatible Edition versions 5.6 and higher and Amazon Aurora PostgreSQL-Compatible Edition versions 11.21 and higher, 12.16 and higher, 13.12 and higher, 14.9 and higher, and 15.4 and higher. Learn more about available versions in the [Aurora documentation](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/Concepts.Aurora_Fea_Regions_DB-eng.Feature.BlueGreenDeployments.html).

### What Regions Do Amazon RDS Blue/Green Deployments Support?

[Amazon RDS Blue/Green Deployments](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/blue-green-deployments.html) are available in all applicable AWS Regions and the AWS GovCloud Regions.

### When Should I Use Amazon RDS Blue/Green Deployments?

Amazon RDS Blue/Green Deployments allow you to make safer, simpler, and faster database changes. Blue/Green Deployments are ideal for use cases such as major or minor version database engine upgrades, operating system updates, schema changes on green environments that do not break logical replication, like adding a new column at the end of a table, or database parameter setting changes.

You can use Blue/Green Deployments to make multiple database updates at the same time using a single switchover. This allows you to stay current on security patches, improve database performance, and access newer database features with short, predictable downtime. If you are looking to perform just a minor version upgrade on Aurora, we recommend that you use [Aurora Zero Downtime Patching (ZDP)](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/Concepts.Aurora_Fea_Regions_DB-eng.Feature.ZDP.html).

### What is the Cost of Using Amazon RDS Blue/Green Deployments?

You will incur the same price for running your workloads on green instances as you do for blue instances. The cost of running on blue and green instances include our [current standard pricing](https://aws.amazon.com/rds/pricing/) for db.instances, cost of storage, cost of read/write I/Os, and any enabled features, such as cost of backups and [Amazon RDS Performance Insights.](https://aws.amazon.com/rds/performance-insights/) Effectively, you are paying approximately 2x the cost of running workloads on db.instance for the lifespan of the blue-green-deployment.  

For example: You have Aurora MySQL-Compatible Edition 5.7 cluster running on two r5.2xlarge db.instances, a primary writer instance and a reader instance, in us-east-1 AWS region. Each of the r5.2xlarge db.instances are configured for 40 GiB Storage and have 25 Million I/Os per month. You create a clone of the blue instance topology using Amazon RDS Blue/Green Deployments, run it for 15 days (360 hours) and each green instance has 3 million I/O reads during that time. You then delete the blue instances after a successful switchover. The blue instances (writer and reader) cost $849.2 for 15 days at an on-demand rate of $1.179/hr (Instance + Storage+ I/O). The green instances (writer and reader) cost $840.40 for 15 days at an on-demand rate of $1.167/hr (Instance +Storage+ I/O). The total cost to you for using Blue/Green Deployments for those 15 days is $1689.60, which is approximately 2x the cost of running blue instances for that time period.  

### What Kind of Changes Can I Make with Amazon RDS Blue/Green Deployments?

Amazon RDS Blue/Green Deployments help you make safer, simpler, and faster database changes, such as major or minor version upgrades, schema changes, instance scaling, engine parameter changes, and maintenance updates.

### What is the “blue environment” in Amazon RDS Blue/Green Deployments? What is the “green environment”?”

In Amazon RDS Blue/Green Deployments, the blue environment is your current production environment. The green environment is your staging environment that will become your new production environment after switchover.

### How Do Switchovers Work with Amazon RDS Blue/Green Deployments?

When Amazon RDS Blue/Green Deployments initiate a switchover, they block writes to both the blue and green environments, until switchover is complete. During switchover, the staging environment, or green environment, catches up with the production system, ensuring data is consistent between the staging and production environment. Once the production and staging environment are in complete sync, Blue/Green Deployments promote the staging environment as the new production environment by redirecting traffic to the newly promoted production environment.

Amazon RDS Blue/Green Deployments are designed to enable writes on the green environment after switchover is complete, ensuring zero data loss during the switchover process.

### After Amazon RDS Blue/Green Deployments Switches Over, what Happens to My Old Production Environment?

Amazon RDS Blue/Green Deployments do not delete your old production environment. If needed, you can access it for additional validations and performance/regression testing. If you no longer need the old production environment, you can delete it. Standard billing charges apply on old production instances until you delete them.

### What Do Amazon RDS Blue/Green Deployments Switchover Guardrails Check For?

Amazon RDS Blue/Green Deployments switchover guardrails block writes on your blue and green environments until your green environment catches up before switching over. Blue/Green Deployments also perform health checks of your primary and replicas in your blue and green environments. They also perform replication health checks, for example, to see if replication has stopped or if there are errors. They detect long running transactions between your blue and green environments. You can specify your maximum tolerable downtime, as low as 30 seconds, and if you have an ongoing transaction that exceeds this your switchover will time out.

### Can I Use Blue/Green Deployments when I Have a Blue Database as a subscriber/publisher for a Self-managed Logical Replica?

If your blue environment is a self-managed logical replica, or subscriber, we will block switchover. We recommend that you first stop replication to the blue environment, proceed with the switchover, and then resume replication. In contrast, if your blue environment is a source for a self-managed logical replica, or publisher, you can continue to switchover. However, you will need to update the self-managed replica to replicate from the green environment post switchover.

### Do Amazon RDS Blue/Green Deployments Support Amazon Aurora Global Databases, Amazon RDS Proxy, or cross-Region Read Replicas?

No, Amazon RDS Blue/Green Deployments do not support Amazon Aurora Global Databases, Amazon RDS Proxy, or cross-Region read replicas.   

### Can I Use Amazon RDS Blue/Green Deployments to Rollback Changes?

No, at this time you cannot use Amazon RDS Blue/Green Deployments to rollback changes.

## Trusted Language Extensions for PostgreSQL

### Why Should I Use Trusted Language Extensions for PostgreSQL?

[Trusted Language Extensions (TLE) for PostgreSQL](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/PostgreSQL_trusted_language_extension.html) enables developers to build high performance PostgreSQL extensions and run them safely on [Amazon Aurora](https://aws.amazon.com/rds/aurora/). In doing so, TLE improves your time to market and removes the burden placed on database administrators to certify custom and third-party code for use in production database workloads. You can move forward as soon as you decide an extension meets your needs. With TLE, independent software vendors (ISVs) can provide new PostgreSQL extensions to customers running on Aurora.

### What Are Traditional Risks of Running Extensions in PostgreSQL and how Does TLE for PostgreSQL Mitigate Those Risks?

PostgreSQL extensions are executed in the same process space for high performance. However, extensions might have software defects that can crash the database.

[TLE for PostgreSQL](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/PostgreSQL_trusted_language_extension.html) offers multiple layers of protection to mitigate this risk. TLE is designed to limit access to system resources. The **rds\_superuser** role can determine who is permitted to install specific extensions. However, these changes can only be made through the TLE API. TLE is designed to limit the impact of an extension defect to a single database connection. In addition to these safeguards, TLE is designed to provide DBAs in the **rds\_superuser** role fine-grained, online control over who can install extensions and they can create a permissions model for running them. Only users with sufficient privileges will be able to run and create using the “CREATE EXTENSION” command on a TLE extension. DBAs can also allow-list “PostgreSQL hooks” required for more sophisticated extensions that modify the database’s internal behavior and typically require elevated privilege.  

### How Does TLE for PostgreSQL Relate to/work with other AWS Services?

[TLE for PostgreSQL](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/PostgreSQL_trusted_language_extension.html) is available for [Amazon Aurora PostgreSQL-Compatible Edition](https://aws.amazon.com/rds/aurora/) on versions 14.5 and higher. TLE is implemented as a PostgreSQL extension itself and you can activate it from the rds\_superuser role similar to other extensions supported on Aurora.  

### In what Versions of PostgreSQL Can I Run TLE for PostgreSQL?

You can run [TLE for PostgreSQL](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/PostgreSQL_trusted_language_extension.html) in PostgreSQL 14.5 or higher in [Amazon Aurora](https://aws.amazon.com/rds/aurora/).

### In what Regions is Trusted Language Extensions for PostgreSQL Available?

[TLE for PostgreSQL](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/PostgreSQL_trusted_language_extension.html) is currently available in all AWS Regions (excluding AWS China Regions) and the AWS GovCloud Regions.  

### How much Does it Cost to Run TLE?

[TLE for PostgreSQL](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/PostgreSQL_trusted_language_extension.html) is available to [Aurora](https://aws.amazon.com/rds/aurora/) customers at no additional cost.  

### How is TLE for PostgreSQL Different from Extensions Available on Amazon Aurora and Amazon RDS Today?

[Aurora](https://aws.amazon.com/rds/aurora/) and [Amazon RDS](https://aws.amazon.com/rds/) support a curated set of over [85 PostgreSQL extensions](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/CHAP_PostgreSQL.html#PostgreSQL.Concepts.General.FeatureSupport.Extensions). AWS manages the security risks for each of these extensions under the [AWS shared responsibility model](https://aws.amazon.com/compliance/shared-responsibility-model/). The extension that implements [TLE for PostgreSQL](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/PostgreSQL_trusted_language_extension.html) is included in this set. Extensions that you write or that you obtain from third-party sources and install in TLE are considered part of your application code. You are responsible for the security of your applications that use TLE extensions.  

### What Are Some Examples of Extensions I Could Run with TLE for PostgreSQL?

You can build developer functions, such as bitmap compression and differential privacy (such as publicly accessible statistical queries that protect privacy of individuals).  

### What Programming Languages Can I Use to Develop TLE for PostgreSQL?

[TLE for PostgreSQL](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/PostgreSQL_trusted_language_extension.html) currently supports JavaScript, PL/pgSQL, Perl, and SQL.  

### How Do I Deploy a TLE for PostgreSQL Extension?

Once the rds\_superuser role activates [TLE for PostgreSQL](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/PostgreSQL_trusted_language_extension.html), you can deploy TLE extensions using the SQL CREATE EXTENSION command from any PostgreSQL client, such as psql. This is similar to how you would create a user-defined function written in a procedural language, such as PL/pgSQL or PL/Perl. You can control which users have permission to deploy TLE extensions and use specific extensions.  

### How Do TLE for PostgreSQL Extensions Communicate with the PostgreSQL Database?

[TLE for PostgreSQL](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/PostgreSQL_trusted_language_extension.html) access your PostgreSQL database exclusively through the TLE API. The TLE supported trusted languages include all functions of the PostgreSQL server programming interface (SPI) and support for PostgreSQL hooks, including the check password hook.  

### Where Can I Learn More about the TLE for PostgreSQL Open-source Project?

You can learn more about the [TLE for PostgreSQL](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/PostgreSQL_trusted_language_extension.html) project on the official [TLE GitHub page](https://github.com/aws/pg_tle).

## Amazon RDS Extended Support

### Can I Use RDS Extended Support with Any Minor Version?

No, [Amazon RDS Extended Support](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/extended-support.html) is only available on certain minor versions. See [Aurora User Guide](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/Aurora.VersionPolicy.html#Aurora.VersionPolicy.MinorVersions) for details.   

### How Can I Estimate My RDS Extended Support Charges?

Amazon RDS Extended Support charges depend on three factors: 1. number of vCPUs or ACUs running on the instance, 2. AWS Region, and 3. number of years past end of standard support.

To estimate your charges, [determine the number of vCPUs on your instance](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Concepts.DBInstanceClass.html#Concepts.DBInstanceClass.Summary.) and the appropriate calendar year pricing for your engine version. If your version is within the year 1-2 pricing and you are using provisioned instances, you will be charged `**#vCPUs x Year 1 and Year 2 pricing per hour of usage for your chosen Region**`. If your version is on year 3 pricing and you are using provisioned instances, you will be charged `**#vCPUs x Year 3 pricing per hour of usage for your chosen Region.**`

For example, if you are running a Aurora MySQL-Compatible 2 db.r5.large instance in N. Virginia on December 30, 2024, which is within the first year of RDS Extended Support, you will be charged $0.200 per hour, or 2 vCPUs x $0.100 per vCPU-hr.

### When Does Amazon Aurora Start Charging for RDS Extended Support?

You will begin to receive charges for Amazon RDS Extended Support the day after the Aurora MySQL-Compatible Edition's major version end of standard support date. This will be in addition to the instance, storage, backup, and/or data transfer charges incurred for the life of the instance.

For example, Aurora MySQL-Compatible 2 standard support ends on November 30, 2024. If you run an Aurora MySQL-Compatible 2 instance after November, 30, 2024 you will be charged for RDS Extended Support on that instance.

### Do I Have to Pay for RDS Extended Support on My DB Snapshots?

No, Amazon RDS Extended Support pricing does not apply to DB snapshots. However, when you restore a snapshot to a new DB instance that uses a version on RDS Extended Support, the instance will be charged RDS Extended Support pricing until you upgrade it to a standard support version or delete the instance.

### When Do I Stop Receiving Charges for RDS Extended Support?

Upgrading your instance to a newer engine version that’s available in standard support will prevent your instance from being charged RDS Extended Support pricing. RDS Extended Support charges automatically stop when you shut down or delete an instance that is running a major engine version beyond its end of standard support date.

### There Are Two Different Prices Listed for Each Engine Version. How Do I Know Which of Those I’m Being Charged?

The RDS Extended Support price you are charged depends on the engine version, AWS Region, and the number of calendar years since standard support expired for that version. You will be charged the year 1 and year 2 pricing in your chosen Region per vCPU-hr for the first two years after the end of standard support. If RDS Extended Support is offered for a third year, you will be charged the year 3 pricing in your chosen Region per vCPU-hr starting on the first day of the third year.

For example, Aurora PostgreSQL-Compatible 11 reaches end of standard support on February 29, 2024. If you are deployed in US East (Ohio), you will be charged $0.100 per vCPU-hr between April 1, 2024 to March 31, 2026. Starting April 1, 2026, you will be charged $0.200 per vCPU-hr.

### How Can I Avoid Being Charged for RDS Extended Support?

We recommend upgrading your instance as early as possible to a major engine version that is within its standard support term. This will help avoid incurring RDS Extended Support charges.

### Can I Use Amazon RDS Blue/Green Deployments to Migrate from a RDS Extended Support Version to a Standard Support Version?

You can use Amazon RDS Blue/Green Deployments to migrate your instances using RDS Extended Support, so long as Blue/Green Deployments supports your instance’s engine, Region, and major version type. Blue/Green Deployments is available for Aurora MySQL-Compatible Edition. For information on available versions, see the [Blue/Green Deployments documentation](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Concepts.RDS_Fea_Regions_DB-eng.Feature.BlueGreenDeployments.html).

### Do Reserved Instance Discounts Apply to RDS Extended Support?

No, RDS Extended Support charges are independent of instance charges. Therefore, Reserved Instance discounts are not applicable to RDS Extended Support charges.

### Will I Get Charged for RDS Extended Support even if I Move from RDS for MySQL 5.7 to Aurora MySQL 2 (based on MySQL 5.7)?

If you migrate from RDS for MySQL 5.7 to Aurora MySQL 2 before February 29, 2024, you will not be charged for RDS Extended Support. If you migrate after February 29, 2024 and before November 30, 2024, you will be charged for RDS Extended Support for the number of hours you were running MySQL 5.7 on Amazon RDS.

If you migrate after November 30, 2024 or use Aurora MySQL-Compatible 2 after November 30, 2024, you will also be charged for RDS Extended Support on your Aurora database. For additional details, please refer to the [Amazon Aurora](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/Aurora.VersionPolicy.html#Aurora.VersionPolicy.MajorVersions) and [Amazon RDS documentation](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/MySQL.Concepts.VersionMgmt.html#MySQL.Concepts.VersionMgmt.ReleaseCalendar).

### What Happens to DB Snapshots I Created on a Version that is no Longer on Standard Support? Will I Have to Pay RDS Extended Support Price for Them?

No, you will not be charged RDS Extended Support pricing on DB snapshots. However, when you restore a DB snapshot to a new DB instance after end of standard support, you will be charged RDS Extended Support pricing for that instance.

For example, if you restore a DB snapshot to a new DB instance on Aurora MySQL-Compatible 2 after November 30, 2024, the instance will be charged the Aurora MySQL-Compatible 2 RDS Extended Support pricing until you upgrade it to Aurora MySQL-Compatible version 3 or newer or delete the instance.

### If I Create a New Instance on a Major Version Engine after it Reaches End of Standard Support, Will I Be Charged for RDS Extended Support?

Yes, if you create an instance or restore a DB snapshot to an instance running on a version that has reached its end of standard support date, you will be charged for RDS Extended Support pricing in addition to the instance, storage, backup, and data transfer charges.