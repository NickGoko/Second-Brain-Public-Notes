---
tags:
  - cloud/aws
---
![[Pasted image 20240214152720.png]]


![[AWS Solutions Architect Skillbuilder#Use Case 5]]

# FAQ

## General

### What is Amazon DocumentDB (with MongoDB compatibility)?

Amazon DocumentDB (with MongoDB compatibility) is a fast, scalable, highly available, and fully managed enterprise [document database](https://aws.amazon.com/nosql/document/) service that supports native JSON workloads. As a document database, Amazon DocumentDB makes it easy to store, query, and index [JSON](https://aws.amazon.com/documentdb/what-is-json/) data. Developers can use the same MongoDB application code, drivers, and tools as they do today to run, manage, and scale workloads on Amazon DocumentDB. Enjoy improved performance, scalability, and availability without worrying about managing the underlying infrastructure.  

Customers can use [AWS Database Migration Service (DMS)](https://aws.amazon.com/dms/) to easily migrate their on-premises or [Amazon Elastic Compute Cloud (EC2)](https://aws.amazon.com/ec2/) MongoDB non-relational databases to Amazon DocumentDB with virtually no downtime. There are no upfront investments required to use Amazon DocumentDB, and customers only pay for the capacity they use.  

### What Use Cases Are Well-suited for a Document Database like Amazon DocumentDB?

Document-oriented databases are one of the fastest growing categories of [noSQL](https://aws.amazon.com/nosql/) databases, with the primary reason being that document databases offer both flexible schemas and extensive query capabilities. The document model is a great choice for use cases with dynamic datasets that require ad-hoc querying, indexing, and aggregations. With the scale that Amazon DocumentDB provides, it is used by a wide variety of [customers](https://aws.amazon.com/documentdb/customers/) for use cases such as content management, personalization, catalogs, mobile and web applications, IoT, and profile management.  

### What Does "MongoDB-compatible" Mean?

“[MongoDB](https://aws.amazon.com/documentdb/what-is-mongodb/) compatible” means that Amazon DocumentDB interacts with the Apache 2.0 open source MongoDB 3.6, 4.0, and 5.0 APIs. As a result, you can use the same MongoDB drivers, applications, and tools with Amazon DocumentDB with little or no changes. While Amazon DocumentDB supports a vast majority of the MongoDB APIs that customers actually use, it does not support every MongoDB API. Our focus has been to deliver the capabilities that customer actually use and need.  

Since launch, we have continued to work backwards from customers and have delivered an additional 80+ capabilities, including MongoDB 4.0 and 5.0 compatibility, transactions, and sharding. To learn more about the supported MongoDB APIs, see the [compatibility documentation](https://docs.aws.amazon.com/documentdb/latest/developerguide/mongo-apis.html). To learn more about recent Amazon DocumentDB launches, see “Amazon DocumentDB Announcements” on the [Amazon DocumentDB resources page.](https://aws.amazon.com/documentdb/resources/)  

### Is Amazon DocumentDB Restricted by the MongoDB SSPL License?

No. Amazon DocumentDB does not utilize any MongoDB SSPL code and thus is not restricted by this license. Instead, Amazon DocumentDB interacts with the Apache 2.0 open-source MongoDB 3.6, 4.0, and 5.0 APIs. We will continue to listen and work backward from our customers to deliver the capabilities that they need. To learn more about the supported MongoDB APIs, see the [compatibility documentation](https://docs.aws.amazon.com/documentdb/latest/developerguide/mongo-apis.html). To learn more about recent Amazon DocumentDB launches, see “Amazon DocumentDB Announcements” on the [Amazon DocumentDB resources page](https://aws.amazon.com/documentdb/resources/).  

### How Can I Migrate Data from an Existing MongoDB Database to Amazon DocumentDB?

Customers can use [AWS Database Migration Service (DMS)](https://aws.amazon.com/dms/) to easily migrate their on-premises or [Amazon Elastic Compute Cloud (EC2)](https://aws.amazon.com/ec2/) MongoDB databases to Amazon DocumentDB with virtually no downtime. With DMS, you can migrate from a MongoDB replica set or from a sharded cluster to Amazon DocumentDB. Additionally, you can use most existing tools to migrate data from a MongoDB database to Amazon DocumentDB, including [mongodump/mongorestore, mongoexport/mongoimport](https://docs.aws.amazon.com/documentdb/latest/developerguide/backup_restore-dump_restore_import_export_data.html), and third-party tools that support Change Data Capture (CDC) via the oplog. For more information, see [Migrating to Amazon DocumentDB](https://aws.amazon.com/documentdb/migrating-self-managed-mongodb-databases/).  

### Do I Need to Change Client Drivers to Use Amazon DocumentDB?

No, Amazon DocumentDB works with a vast majority of MongoDB drivers compatible with MongoDB 3.4+.  

### Does Amazon DocumentDB Support ACID Transactions?

Yes. With the launch of support for MongoDB 4.0 compatibility, Amazon DocumentDB supports the ability to perform [atomicity, consistency, isolation, durability (ACID) transactions](https://docs.aws.amazon.com/athena/latest/ug/acid-transactions.html) across multiple documents, statements, collections, and databases.  

### Is Amazon DocumentDB Subject to MongoDB's End of Life (EOL) Schedule?

No, Amazon DocumentDB does not follow the same support lifecycles as MongoDB and MongoDB's EOL schedule does not apply to Amazon DocumentDB.  

### How Do I Access My Amazon DocumentDB Cluster?

Amazon DocumentDB clusters are deployed within a customer's [Amazon VPC](https://aws.amazon.com/vpc/) (VPC) and can be accessed directly by Amazon Elastic Compute Cloud (EC2) instances or other AWS services that are deployed in the same VPC. Additionally, Amazon DocumentDB can be accessed by Amazon EC2 instances or other AWS services in different VPCs in the same region or other regions via VPC peering. Access to Amazon DocumentDB clusters must be done through the mongo shell or with MongoDB drivers. Amazon DocumentDB requires that you authenticate when connecting to a cluster. For additional options, see [Connecting to an Amazon DocumentDB Cluster from Outside an Amazon VPC](https://docs.aws.amazon.com/documentdb/latest/developerguide/connect-from-outside-a-vpc.html).  

### Why Are Amazon RDS Permissions and Resources Required to Use Amazon DocumentDB?

For certain management features such as instance lifecycle management, encryption-at-rest with Amazon Key Management Service (KMS) keys and security groups management, Amazon DocumentDB leverages operational technology that is shared with [Amazon Relational Database Service](https://aws.amazon.com/rds/?c=db&sec=srv) (RDS) and [Amazon Neptune](https://aws.amazon.com/neptune/?c=db&sec=srv). When using the describe-db-instances and describe-db-clusters AWS CLI APIs, we recommend filtering for Amazon DocumentDB resources using the following parameter: "--filter Name=engine,Values=docdb".  

### What Instances Types Does Amazon DocumentDB Offer?

Please see the Amazon DocumentDB [pricing page](https://aws.amazon.com/documentdb/pricing/) for current information on available instance types per region.  

### How Do I Try Amazon DocumentDB?

To try Amazon DocumentDB, please see the [Getting Started](https://aws.amazon.com/documentdb/getting-started/) guide.  

### Does Amazon DocumentDB Have an SLA?

Yes. For more information, please see [Amazon DocumentDB (with MongoDB compatibility) Service Level Agreement](https://aws.amazon.com/documentdb/sla/).  

## Performance

### What Type of Performance Can I Expect from Amazon DocumentDB?

When writing to storage, Amazon DocumentDB only persists a write-ahead logs, and does not need to write full buffer page syncs. As a result of this optimization, which does not compromise durability, Amazon DocumentDB writes are typically faster than traditional databases. Amazon DocumentDB clusters can scale out to millions of reads per second with up to [15-read replicas](https://docs.aws.amazon.com/documentdb/latest/developerguide/replication.html).  

## Pricing

### How much Does Amazon DocumentDB Cost and in Which AWS Regions is Amazon DocumentDB Available?

Please see the Amazon DocumentDB [pricing page](https://aws.amazon.com/documentdb/pricing/) for current information on regions and prices.  

### Does Amazon DocumentDB Have a Free Tier and Can You Get Started for Free?

Yes, you can try Amazon DocumentDB for free using the 1-month free trial. If you have not used Amazon DocumentDB before, you are eligible for a one month free trial. Your organization gets 750 hours per month of t3.medium instance usage, 30 million IOs, 5 GB of storage, and 5 GB of backup storage for free for 30 days. Once your one month free trial expires or your usage exceeds the free allowance, you can shut down your cluster to avoid any charges, or keep it running at our [standard on-demand rates](https://aws.amazon.com/documentdb/pricing/). To learn more, refer to the [DocumentDB free trial page](https://aws.amazon.com/documentdb/free-trial/).  

### Why Should I Use Amazon DocumentDB I/O-Optimized?

Amazon DocumentDB I/O-Optimized is the ideal choice when you need predictable costs or have I/O intensive applications. If you expect your I/O costs to exceed 25% of your total Amazon DocumentDB database costs, this option offers enhanced price performance. Refer to our [Amazon DocumentDB I/O-Optimized documentation](https://docs.aws.amazon.com/documentdb/latest/developerguide/db-cluster-storage-configs.html) to learn more, including how to get started.

### Can I Switch back and forth between the I/O-Optimized and Standard Storage Configurations?

You can switch your existing database clusters once every 30 days to Amazon DocumentDB I/O-Optimized. You can switch back to Amazon DocumentDB standard storage configurations at any time.

### With Amazon DocumentDB I/O-Optimized, Do I Continue Paying for the I/Os Required for Replicating Data across Regions with Global Clusters?

Yes, the charges for the I/O operations required to replicate data across regions continue to apply. Amazon DocumentDB I/O-Optimized does not charge for read and write I/O operations, which is different from data replication. Refer to our [Amazon DocumentDB I/O-Optimized documentation](https://docs.aws.amazon.com/documentdb/latest/developerguide/db-cluster-storage-configs.html) to learn more.

## Elastic Clusters

### What is Amazon DocumentDB Elastic Clusters?

Amazon DocumentDB Elastic Clusters enables you to elastically scale your document database to handle millions of writes and reads, with petabytes of storage capacity. Elastic Clusters simplifies how customers interact with Amazon DocumentDB by automatically managing the underlying infrastructure and removing the need to create, remove, upgrade, or scale instances.  

### How Do I Get Started with Elastic Clusters?

You can create an Elastic Clusters cluster using the Amazon DocumentDB API, SDK, CLI, CloudFormation (CFN), or the AWS console. When provisioning your cluster, you specify how many shards and the compute per shard that your workload needs. Once you have created your cluster, you are ready to start leveraging Elastic Clusters’ elastic scalability. Now, you can connect to the Elastic Clusters cluster and read or write data from your application. Elastic Clusters is elastic. Depending on your workload’s needs, you can add or remove compute by modifying your shard count and/or compute per shard using the AWS console, API, CLI, or SDK. Elastic Clusters will automatically provision/de-provision the underlying infrastructure and rebalance your data.

### How Does Elastic Clusters Work?

Elastic Clusters uses sharding to partition data across Amazon DocumentDB’s distributed storage system. Sharding, also known as partitioning, splits large data sets into small data sets across multiple nodes enabling customers to scale out their database beyond vertical scaling limits of a single database. Elastic Clusters utilizes the separation of compute and storage in Amazon DocumentDB. Rather than re-partitioning collections by moving small chunks of data between compute nodes, Elastic Clusters can copy data efficiently within the distributed storage system.  

### What Types of Sharding Does Elastic Clusters Support?

Elastic Clusters supports hash-based partitioning.  

### How is Elastic Clusters Different from MongoDB Sharding?

With Elastic Clusters, you can easily scale out or scale in your workload on Amazon DocumentDB typically with little to no application downtime or impact to performance regardless of data size. A similar operation on MongoDB would impact application performance and take hours, and in some cases days. Elastic Clusters also offers differentiated management capabilities such as no impact backups and rapid point in time restore enabling customers to focus more time on their applications rather than managing their database.  

### Do I Need to Make Any Changes to My Application to Use Elastic Clusters?

No. You do not need to make any changes to your application to use Elastic Clusters.

### Can I Convert My Existing Amazon DocumentDB Cluster to an Elastic Clusters Cluster?

No, in the near-term, you can leverage AWS Database Migration service (DMS) to migrate data from an existing Amazon DocumentDB cluster to an Elastic Clusters cluster.  

### How Do I Define a Shard Key?

Choosing an optimal shard key for Elastic Clusters is no different than other databases. A great shard key has two characteristics - high frequency and high cardinality. For example, if your application stores user\_orders in DocumentDB, then generally you have to retrieve the data by the user. Therefore, you want all orders related to a given user to be in one shard. In this case, user\_id would be a good shard key. [Read more information](https://docs.aws.amazon.com/documentdb/shard_key). 

### What Are the Concepts Associated with Elastic Clusters?

- <u>Elastic Clusters</u>: An Amazon DocumentDB cluster that allows you to scale your workload’s throughput to millions of reads/writes per second and storage to petabytes. An Elastic Cluster cluster comprises of one or more shards for compute and a storage volume, and is highly available across multiple Availability Zones by default.  
    
- <u>Shard</u>: A shard provides compute for Elastic Clusters cluster. A shard by default will have three nodes, one writer node and two reader nodes. You can have a maximum of 32 shards and each shard can have a maximum of 64 vCPUs.  
    
- <u>Shard key</u>: Shard key is an optional field in your JSON documents that Elastic Clusters uses to distribute read and write traffic to the matching shard. You are advised to pick a key that has lots of unique values. A good shard key will evenly partition your data across the underlying shards, giving your workload the best throughput and performance.   
    
- <u>Sharded collection</u>: A collection whose data is distributed across an Elastic Clusters cluster.  
    

### How Does Elastic Clusters Relate to other AWS Services?

Elastic Clusters integrates with other AWS services in the same way DocumentDB does today. First, you can use AWS Database Migration Service (DMS) to migrate from MongoDB and other relational databases to Elastic Clusters. Second, you can monitor the health and performance of your Elastic Clusters cluster using Amazon CloudWatch. Third, you can set up authentication and authorization through AWS IAM users and roles and use AWS VPC for secure VPC-only connections. Last, you can use AWS Glue to import and export data from/to other AWS services such as S3, Redshift and OpenSearch.  

### Can I Migrate My Existing MongoDB Sharded Workloads to Elastic Clusters?

Yes. You can migrate your existing MongoDB sharded workloads to Elastic Clusters. You can either use the AWS Database Migration Service or native MongoDB tools, such as mongodump and mongorestore, to migrate your MongoDB workload to Elastic Clusters. Elastic Clusters also supports MongoDB’s commonly used APIs, such as shardCollection(), giving you the flexibility to reuse existing tooling and scripts with Amazon DocumentDB.

## Hardware, Scaling, and Storage

### What Are the Minimum and Maximum Storage Limits of an Amazon DocumentDB Cluster?

The minimum storage is 10 GB. Based on your cluster usage, your [Amazon DocumentDB storage](https://docs.aws.amazon.com/documentdb/latest/developerguide/limits.html) will automatically grow, up to 128 TiB in 10 GB increments with no impact on performance. With Amazon DocumentDB Elastic Clusters, storage will automatically grow up to 4 PiB in 10 GB increments. For either case, there is no need to provision storage in advance.  

### How Does Amazon DocumentDB Scale?

Amazon DocumentDB [scales](https://docs.aws.amazon.com/documentdb/latest/developerguide/db-cluster-manage-performance.html) in two dimensions: storage and compute. Amazon DocumentDB's storage automatically scales from 10 GB to 128 TiB in Instance-based Clusters, and up to 4 PiB for Amazon DocumentDB Elastic Clusters. Amazon DocumentDB's compute capacity can be scaled up by creating larger instances and horizontally (for greater read throughput) by adding additional replica instances to the cluster.  

### How Do I Scale the Compute Resources Associated with My Amazon DocumentDB Cluster?

You can scale the compute resources allocated to your instance in the AWS Management Console by selecting the desired instance and clicking the “modify” button. Memory and CPU resources are modified by [changing your instance class](https://docs.aws.amazon.com/documentdb/latest/developerguide/db-instance-modify.html).

When you modify your instance class, your requested changes will be applied during your specified maintenance window. Alternatively, you can use the "Apply Immediately" flag to apply your scaling requests immediately. Both of these options will have an availability impact for a few minutes as the scaling operation is performed. Bear in mind that any other pending system changes will also be applied.  

## Backup and Restore

### How Do I Enable Backups for My Cluster?

Automated backups are always enabled on Amazon DocumentDB clusters. Amazon DocumentDB’s [simple database backup capability](https://docs.aws.amazon.com/documentdb/latest/developerguide/backup_restore.html) enables point-in-time recovery for your clusters. You can increase your backup window for point-in-time restores up to 35 days. Backups do not impact database performance.  

### Can I Take Cluster Snapshots and Keep Them around as long as I Want?

Yes. [Manual snapshots](https://docs.aws.amazon.com/documentdb/latest/developerguide/backup_restore-create_manual_cluster_snapshot.html) can be retained beyond the backup window and there is no performance impact when taking snapshots. Note that [restoring data from cluster snapshots](https://docs.aws.amazon.com/documentdb/latest/developerguide/backup_restore-restore_from_snapshot.html) requires creating a new cluster.  

### If My Instance Fails, what is My Recovery Path?

Amazon DocumentDB automatically makes your data durable across three Availability Zones (AZs) within a Region and will automatically attempt to recover your instance in a healthy AZ with no data loss. In the unlikely event your data is unavailable within Amazon DocumentDB storage, you can [restore from a cluster snapshot](https://docs.aws.amazon.com/documentdb/latest/developerguide/backup_restore-restore_from_snapshot.html) or perform a [point-in-time restore operation](https://docs.aws.amazon.com/documentdb/latest/developerguide/backup_restore-point_in_time_recovery.html) to a new cluster. Note that the latest restorable time for a point-in-time restore operation can be up to five minutes in the past.

### What Happens to My Automated Backups and Cluster Snapshots if I Delete My Cluster?

You can choose to create a final snapshot when [deleting your instance](https://docs.aws.amazon.com/documentdb/latest/developerguide/db-cluster-delete.html). If you do, you can use this snapshot to [restore the deleted instance](https://docs.aws.amazon.com/documentdb/latest/developerguide/backup_restore.html) at a later date. Amazon DocumentDB retains this final user-created snapshot along with all other manually created snapshots after the instance is deleted. Only snapshots are retained after the instance is deleted (i.e., automated backups created for [point-in-time restore](https://docs.aws.amazon.com/documentdb/latest/developerguide/backup_restore-point_in_time_recovery.html) are not kept).  

### What Happens to My Automated Backups and Cluster Snapshots if I Delete My Account?

Deleting your AWS account will delete all automated backups and snapshot backups contained in the account.  

### Can I Share My Snapshots with Another AWS Account?

Yes. Amazon DocumentDB gives you the ability to [create snapshots of your cluster](https://docs.aws.amazon.com/documentdb/latest/developerguide/backup_restore-create_manual_cluster_snapshot.html), which you can use later to restore a cluster. You can [share a snapshot](https://docs.aws.amazon.com/documentdb/latest/developerguide/backup_restore-share_cluster_snapshots.html) with a different AWS account, and the owner of the recipient account can use your snapshot to restore a cluster that contains your data. You can even choose to make your snapshots public – that is, anybody can restore a cluster containing your (public) data. You can use this feature to share data between your various environments (production, dev/test, staging, etc.) that have different AWS accounts, as well as keep backups of all your data secure in a separate account in case your main AWS account is ever compromised.  

### Will I Be Billed for Shared Snapshots?

There is no charge for sharing snapshots between accounts. However, you may be charged for the snapshots themselves, as well as any clusters that you restore from shared snapshots.  

### Can I Automatically Share Snapshots?

We do not support sharing automatic cluster snapshots. To share an automatic snapshot, you must manually create a copy of the snapshot, and then share the copy.  

### Can I Share My Amazon DocumentDB Snapshots across Different Regions?

No. Your shared Amazon DocumentDB snapshots will only be accessible by accounts in the same region as the account that shares them.  

### Can I Share an Encrypted Amazon DocumentDB Snapshot?

Yes. You can share [encrypted Amazon DocumentDB snapshots](https://docs.aws.amazon.com/documentdb/latest/developerguide/encryption-at-rest.html). The recipient of the shared snapshot must have access to the KMS key that was used to encrypt the snapshot.  

### Can I Use Amazon DocumentDB Snapshots outside of the Service?

No. Amazon DocumentDB snapshots can only be used inside of the service.  

### What Happens to My Backups if I Delete My Cluster?

You can choose to create a final snapshot when [deleting your cluster](https://docs.aws.amazon.com/documentdb/latest/developerguide/db-cluster-delete.html). If you do, you can use this snapshot to restore the deleted cluster at a later date. Amazon DocumentDB retains this final user-created snapshot along with all other manually created snapshots after the cluster is deleted.  

## High Availability and Replication

### How Does Amazon DocumentDB Improve My cluster’s Fault Tolerance to Disk Failures?

Amazon DocumentDB automatically divides your storage volume into 10 GB segments spread across many disks. Each 10 GB chunk of your storage volume is replicated six ways, across three Availability Zones (AZs). Amazon DocumentDB is designed to transparently [handle the loss of up to two copies of data](https://docs.aws.amazon.com/documentdb/latest/developerguide/security.disaster-recovery-resiliency.html) without affecting write availability and up to three copies without affecting read availability. Amazon DocumentDB’s storage volume is also self-healing. Data blocks and disks are continuously scanned for errors and repaired automatically.  

### How Does Amazon DocumentDB Improve Recovery time after a Database Crash?

Unlike other databases, after a [database crash](https://docs.aws.amazon.com/documentdb/latest/developerguide/security.disaster-recovery-resiliency.html), Amazon DocumentDB does not need to replay the redo log from the last database checkpoint (typically five minutes) and confirm that all changes have been applied, before making the database available for operations. This reduces database restart times to less than 60 seconds in most cases. Amazon DocumentDB moves the cache out of the database process and makes it available immediately at restart time. This prevents you from having to throttle access until the cache is repopulated to avoid brownouts.  

### What Kind of Replicas Does Amazon DocumentDB Support?

Amazon DocumentDB supports [read replicas](https://docs.aws.amazon.com/documentdb/latest/developerguide/replication.html), which share the same underlying storage volume as the primary instance. Updates made by the primary instance are visible to all Amazon DocumentDB replicas.  

- **Feature:** Amazon DocumentDB read replicas
- **Number of replicas:** Up to 15  
    
- **Replication Type:** Asynchronous (typically milliseconds)
- **Performance impact on primary:** Low
- **Act as failover target:** Yes (no data loss)
- **Automated failover:** Yes  
    

### Can I Have Cross-region Replicas with Amazon DocumentDB?

Yes, you can replicate your data across regions using the [Global Cluster feature](https://aws.amazon.com/documentdb/global-clusters/). Global Clusters span across multiple AWS Regions. Global clusters replicate your data to clusters in up to five Regions with little to no impact on performance. Global clusters provide faster recovery from Region-wide outages and enable low-latency global reads. To learn more see our [blog post](https://aws.amazon.com/blogs/database/introducing-amazon-documentdb-with-mongodb-compatibility-global-clusters/).  

### Can I Prioritize Certain Replicas as Failover Targets over Others?

Yes. You can [assign a promotion priority tier](https://docs.aws.amazon.com/documentdb/latest/developerguide/db-cluster-fault-tolerance.html) to each instance on your cluster. If the primary instance fails, Amazon DocumentDB will promote the replica with the highest priority to primary. If there are inconsistencies between two or more replicas in the same priority tier, then Amazon DocumentDB will promote the replica that is the same size as the primary instance.  

### Can I Modify Priority Tiers for Instances after They Have Been Created?

You can [modify the priority tier](https://docs.aws.amazon.com/documentdb/latest/developerguide/db-cluster-fault-tolerance.html) for an instance at any time. Simply modifying priority tiers will not trigger a [failover](https://docs.aws.amazon.com/documentdb/latest/developerguide/failover.html).  

### Can I Prevent Certain Replicas from Being Promoted to the Primary Instance?

You can assign lower priority tiers to replicas that you do not want promoted to the primary instance. However, if the higher priority replicas on the cluster are unhealthy or unavailable for some reason, then Amazon DocumentDB will promote the lower priority replica.  

### How Does Amazon DocumentDB Assure High Availability of My Cluster?

Amazon DocumentDB can be deployed in a high-availability configuration by using replica instances in multiple AWS Availability Zones as failover targets. In the event of a primary instance failure, a replica instance is automatically promoted to be the new primary with minimal service interruption.  

### How Can I Improve upon the Availability of a Single Amazon DocumentDB Instance?

You can add additional Amazon DocumentDB replicas. Amazon DocumentDB replicas share the same underlying storage as the primary instance. Any Amazon DocumentDB replica can be promoted to become primary without any data loss and therefore can be used for enhancing fault tolerance in the event of a primary instance failure. To increase cluster availability, simply create one to 15 replicas, in multiple AZs, and Amazon DocumentDB will automatically include them in failover primary selection in the event of an instance outage.  

### What Happens during Failover and how long Does it Take?

[Failover](https://docs.aws.amazon.com/documentdb/latest/developerguide/failover.html) is automatically handled by Amazon DocumentDB so that your applications can resume database operations as quickly as possible without manual administrative intervention.  

- If you have an Amazon DocumentDB replica instance in the same or a different Availability Zone, when failing over, Amazon DocumentDB flips the canonical name record (CNAME) for your instance to point at the healthy replica, which is in turn promoted to become the new primary. Start-to-finish, failover typically completes within 30 seconds. 
- If you do not have an Amazon DocumentDB replica instance (i.e. a single instance cluster), Amazon DocumentDB will attempt to create a new instance in the same Availability Zone as the original instance. This replacement of the original instance is done on a best-effort basis and may not succeed, for example, if there is an issue that is broadly affecting the Availability Zone. 

Your application should retry database connections in the event of connection loss.  

### If I Have a Primary Instance and an Amazon DocumentDB Replica Instance Actively Taking Read Traffic and a Failover Occurs, what Happens?

Amazon DocumentDB will automatically detect a problem with your primary instance and begin routing your read/write traffic to an Amazon DocumentDB replica instance. On average, this failover will complete within 30 seconds. In addition, the read traffic that your Amazon DocumentDB replicas instances were serving will be briefly interrupted.  

### How far behind the Primary Will My Replicas Be?

Since Amazon DocumentDB replicas share the same data volume as the primary instance, there is virtually no replication lag. We typically observe lag times in the 10s of milliseconds.  

## Security and compliance

### Can I Use Amazon DocumentDB in Amazon Virtual Private Cloud (Amazon VPC)?

Yes. All Amazon DocumentDB clusters must be created in a [VPC](https://aws.amazon.com/vpc/). With Amazon VPC, you can define a virtual network topology that closely resembles a traditional network that you might operate in your own datacenter. This gives you complete control over who can access your Amazon DocumentDB clusters.  

### Does Amazon DocumentDB Support Role-based Access Control (RBAC)?

Amazon DocumentDB supports RBAC with built-in roles. RBAC enables you to enforce least privilege as a best practice by restricting the actions that users are authorized to perform. For more information, see [Amazon DocumentDB role-based access control](https://docs.aws.amazon.com/documentdb/latest/developerguide/role_based_access_control.html).  

### How Do the Existing MongoDB Authentication Modes Work with Amazon DocumentDB?

Amazon DocumentDB utilizes VPC’s strict network and authorization boundary. Authentication and authorization for Amazon DocumentDB management APIs is provided by [IAM users](https://docs.aws.amazon.com/whitepapers/latest/get-started-documentdb/security-and-compliance.html), roles, and policies. Authentication to an Amazon DocumentDB database are done via standard MongoDB tools and drivers with Salted Challenge Response Authentication Mechanism (SCRAM), the default authentication mechanism for MongoDB.  

### Does Amazon DocumentDB Support Encrypting My Data-at-rest?

Yes. Amazon DocumentDB allows you to encrypt your clusters using keys you manage through [AWS Key Management Service (KMS)](https://docs.aws.amazon.com/documentdb/latest/developerguide/security.encryption.ssl.public-key.html). On a cluster running with Amazon DocumentDB encryption, data stored at rest in the underlying storage is encrypted, as are its automated backups, snapshots, and replicas in the same cluster. Encryption and decryption are handled seamlessly. For more information about the use of KMS with Amazon DocumentDB, see the [Encrypting Amazon DocumentDB Data at Rest](https://docs.aws.amazon.com/documentdb/latest/developerguide/encryption-at-rest.html).  

### Can I Encrypt an Existing Unencrypted Cluster?

Currently, encrypting an existing unencrypted Amazon DocumentDB cluster is not supported. To use Amazon DocumentDB encryption for an existing unencrypted cluster, create a new cluster with encryption enabled and migrate your data into it.  

### What compliance Certifications Does Amazon DocumentDB Meet?

Amazon DocumentDB was designed to meet the highest security standards and to make it easy for you to verify our security and meet your own regulatory and compliance obligations. Amazon DocumentDB has been assessed to comply with [PCI DSS](https://aws.amazon.com/compliance/pci-dss-level-1-faqs/), [ISO 9001](https://aws.amazon.com/compliance/iso-9001-faqs/), [27001](https://aws.amazon.com/compliance/iso-27001-faqs/), [27017](https://aws.amazon.com/compliance/iso-27017-faqs/), and [27018](https://aws.amazon.com/compliance/iso-27018-faqs/), [SOC 1, 2 and 3](https://aws.amazon.com/compliance/services-in-scope/), and [Health Information Trust Alliance (HITRUST) Common Security Framework (CSF) certification](https://aws.amazon.com/compliance/services-in-scope/), in addition to being [HIPAA eligible](https://aws.amazon.com/compliance/hipaa-compliance/). AWS compliance reports are available for download in [AWS Artifact](https://aws.amazon.com/artifact/).  

## Major Version Upgrade

### What is In-place Major Version Upgrade?

In-place major version upgrade (MVU) lets you upgrade Amazon DocumentDB 3.6 or 4.0 clusters to Amazon DocumentDB 5.0 using the AWS Console, Software Development Kit (SDK), or Command Line Interface (CLI). With in-place MVU, there is no need to create new clusters or change your end points. Except in AWS GovCloud (US) Region, in-place MVU is available in all regions where Amazon DocumentDB 5.0 is available. To get started with in-place MVU, please review [in-place MVU documentation](https://docs.aws.amazon.com/documentdb/latest/developerguide/docdb-mvu.html).

### Why Should I Use In-place MVU?

In-place MVU lets you seamlessly upgrade your Amazon DocumentDB 3.6 or 4.0 clusters to version 5.0 without the need to perform backup and restore to another cluster and without using other data migration tools. In doing so, it reduces the time and effort associated with usual upgrade process which entail configuring the source and target end points, migrating indexes and data, changing application code, and more.

You won't need to change your endpoint in your applications post upgrade. Since the data stays in the same cluster, there is no additional cost to upgrade using feature.

### What is the Downtime when Upgrading with In-place MVU?

Downtime can vary from cluster to cluster depending on number of collections, indexes, databases, and instances. Before running in-place major version upgrade on your production cluster, we strongly recommend running it in a lower environment to test downtime, performance, and also verify that your applications work as expected post upgrade.

You can also utilize Amazon DocumentDB’s [fast clone feature](https://docs.aws.amazon.com/documentdb/latest/developerguide/db-cluster-cloning.html) to clone your cluster data for testing. Depending on the complexity of your Amazon DocumentDB implementation, you can engage our database solutions architect for additional help.

### What Engine Versions Does In-place MVU Support Today?

In-place MVU is only supported with Amazon DocumentDB 3.6 or 4.0 as a source and version 5.0 as target. It is not supported for Amazon DocumentDB Global Clusters or Elastic Clusters or with DocumentDB 4.0 as target.

## Machine Learning

### How Can I Use My Data in Amazon DocumentDB to Build Machine Learning Models?

Amazon DocumentDB integrates with [Amazon SageMaker Canvas](https://aws.amazon.com/sagemaker/canvas/), making it easy to build machine learning (ML) models and customize foundation models using data stored in Amazon DocumentDB without writing a single line of code. You no longer need to develop custom data and ML pipelines between Amazon DocumentDB and SageMaker Canvas. You can launch SageMaker Canvas from within the Amazon DocumentDB console and add existing Amazon DocumentDB databases as a data source to start building your machine learning models. You can use your data in DocumentDB in SageMaker Canvas to build models to predict customer churn, detect fraud, predict maintenance failures, forecast financial metrics and sales, optimize inventory, summarize content, and generate content.

### What is the Cost Associated with Using Amazon DocumentDB as a Data Source in Amazon SageMaker Canvas to Build Machine Learning Models?

Amazon SageMaker Canvas offers a no-code interface to build machine learning models using data from various data sources including Amazon DocumentDB. You are charged for your use of SageMaker Canvas and for the resulting I/Os when SageMaker Canvas reads data from your Amazon DocumentDB instance. There is no additional charge to use DocumentDB as a data source in Amazon SageMaker Canvas. Visit the [Amazon DocumentDB pricing page](https://aws.amazon.com/documentdb/pricing/) and [SageMaker Canvas pricing](https://aws.amazon.com/sagemaker/pricing) page to learn more.

## Generative AI and Machine Learning

### What is Vector Search?

Vector search is a method used in machine learning (ML) to find similar data points to a given data point by comparing their vector representations using distance or similarity metrics. The closer the two vectors are in the vector space, the more similar the underlying items are considered to be. This technique helps capture the meaning or semantics of the data. This approach is useful in various applications, such as recommendation systems, natural language processing, and image recognition.  

### Why Should I Use Vector search for Amazon DocumentDB?

Vector search for Amazon DocumentDB combines the flexibility and rich querying capability of a JSON-based document database with the power of vector search. You can use your existing Amazon DocumentDB data, or a flexible document data structure, to build machine learning and generative AI use cases such as semantic search experiences, product recommendations, personalization, chatbots, fraud detection, and anomaly detection. Visit the [vector search for Amazon DocumentDB documentation](https://docs.aws.amazon.com/documentdb/latest/developerguide/vector-search.html) to learn more.  

### Which Versions of Amazon DocumentDB Support Vector Search?

Vector search for Amazon DocumentDB is available on Amazon DocumentDB 5.0 instance-based clusters.  

### How Does Implementation of Semantic search Differ from Keyword search with Amazon DocumentDB?

Vector search for Amazon DocumentDB enables the use of semantic search so you can capture the meaning, context, and intent behind your data. Keyword search finds the document based on the actual text or pre-defined synonym mappings. For example, in a traditional e-commerce application, a red dress might return products that have the words “red” and “dress” in their descriptions. Semantic search will retrieve results with dresses in different shades of red which can improve the user experience.  

### What is the Cost Associated with Using Vector search for Amazon DocumentDB?

There is no additional cost to use vector search for Amazon DocumentDB. Standard compute, I/O, storage, and backup charges will apply as you store, index, and search vectors in Amazon DocumentDB. Visit the [Amazon DocumentDB pricing page](https://aws.amazon.com/documentdb/pricing/) to learn more.  

### Why Should I Use No-code Machine Learning with Amazon DocumentDB and Amazon SageMaker Canvas?

Amazon DocumentDB integrates with [Amazon SageMaker Canvas](https://aws.amazon.com/sagemaker/canvas/) making it easy to build generative artificial intelligence (AI) and machine learning (ML) applications using data stored in Amazon DocumentDB. You no longer need to develop custom data and ML pipelines between Amazon DocumentDB and SageMaker Canvas. The in-console integration removes the undifferentiated heavy lifting to connect and access data to accelerate ML development with a low code no code (LCNC) experience. You can launch SageMaker Canvas from within the Amazon DocumentDB console and add existing Amazon DocumentDB databases as a data source.

### What is the Cost Associated with Using Amazon DocumentDB as a Data Source in Amazon SageMaker Canvas to Build Machine Learning Models?

Amazon SageMaker Canvas offers a no-code interface to build machine learning models using data from various data sources including Amazon DocumentDB. You are charged for your use of SageMaker Canvas and for the resulting I/Os when SageMaker Canvas reads data from your Amazon DocumentDB instance. There is no additional charge to use DocumentDB as a data source in Amazon SageMaker Canvas. Visit the [Amazon DocumentDB pricing page](https://aws.amazon.com/documentdb/pricing/) and [SageMaker Canvas pricing](https://aws.amazon.com/sagemaker/pricing) page to learn more.