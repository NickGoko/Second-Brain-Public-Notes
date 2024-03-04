---
tags:
  - cloud/aws
---
![[Pasted image 20240214153601.png]]  
![[AWS Solutions Architect Skillbuilder#Use Case 4]]


# FAQ
## General

### What is Amazon Neptune?

Amazon Neptune is a service that includes a graph database engine, graph analytics database engine, graph machine learning (ML), and visualization tools, which can be used individually or together. The Neptune service make it easy to work with graph data on AWS. With Amazon Neptune Database, you can scale your graphs with more than 100,000 queries per second for the most demanding applications using a serverless graph database designed for superior scalability and availability. With Amazon Neptune Analytics, you can get insights and find trends by quickly processing large amounts of graph data. You can get results in seconds by invoking popular graph analytic algorithms.

### What is Amazon Neptune Database?

Amazon Neptune Database provides a purpose-built graph database with a full set of enterprise features and integrations. Neptune Database supports mission-critical graph applications that require high availability, disaster recovery, dynamic scaling, and other capabilities required by enterprise applications.

### What is Amazon Neptune Analytics?

Neptune Analytics is an analytics database engine to quickly analyze large amounts of graph data to get insights and find trends.

### What is Amazon Neptune ML?

Neptune ML is a capability of Neptune Database that uses graph neural networks (GNNs), an ML technique for graphs, to make fast and more accurate predictions using graph data.

### When Would I Use Neptune Database, Neptune Analytics, or Neptune ML?

Neptune Database, with Neptune developer tools, are the right choice for building mission-critical systems at large scale. Systems such as product recommendation engines, identity and access management systems, and compliance systems often require geographically distributed capabilities that are available in Neptune Global Database. Neptune Database stores tens of billions of relationships and can process hundreds of thousands of interactive graph queries per second.

Neptune Analytics, with Neptune notebooks, are the right choice for interacting with data to derive insights. These capabilities empower users to interact with data using familiar tools, such as Pandas, Jupyter, and Python, to discover and pinpoint interactions and patterns of behavior in the data that are indicative of fraud, illegal activities, optimization opportunities, and more.

Some common use cases for Neptune Analytics include ephemeral analytics, running low-latency analytic queries, running built-in graph algorithms, and performing vector similarity search. With vector similarity search, Neptune Analytics can be used for building Retrieval Augmented Generation (RAG) applications that search through dense data representations provided by embeddings. The vector search results can be combined with contextually aware data representations in graphs for providing rich contextual information related to relationships.

Neptune ML can be used for designing, building, optimizing, and predicting relationships and categorizations using state-of-the-art GNNs. For augmenting feature tables, Neptune Analytics can be used for deriving critical features from connected data using common algorithms such as clustering, centrality, and path finding.

### Does Amazon Neptune Have a Service Level Agreement (SLA)?

Yes. Please see the [Amazon Neptune SLA](https://aws.amazon.com/neptune/sla/).

## Amazon Neptune Database

[Client access](https://aws.amazon.com/neptune/faqs//#Client_access) | [Database performance](https://aws.amazon.com/neptune/faqs//#Database_performance) | [Database pricing](https://aws.amazon.com/neptune/faqs//#Database_pricing) | [Hardware and scaling](https://aws.amazon.com/neptune/faqs//#Hardware_and_scaling) | [Backup and restore](https://aws.amazon.com/neptune/faqs//#Backup_and_restore) | [High availability and replication](https://aws.amazon.com/neptune/faqs//#High_availability_and_replication) | [Database security](https://aws.amazon.com/neptune/faqs//#Database_security)

### Client Access

#### What Popular Graph Query Languages Does Neptune Database Support?

Neptune Database supports two query languages for the property graph data model, the open-source [Apache TinkerPop Gremlin](https://tinkerpop.apache.org/gremlin.html) graph traversal language and the [openCypher](http://opencypher.org/) query language, and for the Resource Description Framework (RDF) data model, Neptune supports the [W3C open standard SPARQL](https://www.w3.org/TR/sparql11-overview/) query language.

#### Can I Use Apache TinkerPop Gremlin, openCypher, and RDF/SPARQL on the Same Neptune Database Cluster?

Yes, each Neptune Database cluster can store both property graph data and RDF data. Neptune provides a Gremlin endpoint (HTTPS and WebSocket), openCypher endpoint (HTTPS and Bolt), and a SPARQL 1.1 Protocol REST endpoint.

For property graphs, you can execute either a Gremlin or openCypher query over the same data regardless of which language was used to enter that data. You may find it more convenient to use Gremlin for some workloads and openCypher for others. You cannot execute a query for property graph data (Gremlin or openCypher) over RDF data or vice-versa.

#### How Can I Migrate from an Existing Apache TinkerPop Gremlin Application to Neptune Database?

Neptune Database provides an Apache TinkerPop Gremlin Server that supports both HTTPS and WebSocket connections. Once you provision an instance of Neptune, you can configure your existing TinkerPop application to use the endpoint provided by the service. See also [accessing the Graph via Gremlin](https://docs.aws.amazon.com/neptune/latest/userguide/get-started-graph-gremlin.html).

#### Do I Need to Change Client Drivers to Use Neptune Gremlin Server?

No, Neptune Gremlin Server supports clients that are compatible with Apache TinkerPop using both WebSockets and HTTPS REST connections. The latest version of Neptune Database supports TinkerPop 3.6.x. Please consult the [documentation](https://docs.aws.amazon.com/neptune/latest/userguide/access-graph-gremlin-client.html) for more information.  

#### How Can I Migrate from an Existing openCypher Application to Neptune Database?

With Neptune support for the openCypher query language, you can move most Cypher or Neo4j workloads that use the Bolt protocol or HTTPS to Neptune. For more detailed information on how to migrate an openCypher application, read the [migration guide](https://docs.aws.amazon.com/neptune/latest/userguide/migrating-from-neo4j.html) in the documentation.

#### How Can I Migrate from a Triple Store with a SPARQL Endpoint to Neptune Database?

Neptune provides an HTTPS REST endpoint that implements the [SPARQL 1.1 Protocol](https://docs.aws.amazon.com/neptune/latest/userguide/sparql-graph-store-protocol.html). Once you provision a service instance, you can configure your application to point to the SPARQL endpoint. See also [accessing the Graph via SPARQL](https://docs.aws.amazon.com/neptune/latest/userguide/access-graph-sparql.html).

#### Do I Need to Change Client Drivers to Use Neptune SPARQL Endpoint?

No, the Neptune SPARQL endpoint will work with any client that supports the SPARQL 1.1 Protocol.  

#### Is Neptune Database ACID (Atomicity, Consistency, Isolation, Durability) Compliant?

Yes, Neptune is ACID compliant with immediate consistency on the primary writer instance, and eventual consistency on the read replica instances.  

#### Why Are Amazon RDS Permissions and Resources Required to Use Neptune Database?

Neptune Database is a purpose-built, high-performance graph database engine. For certain management features such as instance lifecycle management, encryption at rest with AWS Key Management Service (AWS KMS) keys, and security groups management, Neptune uses operational technology that is shared with Amazon Relational Database Service (Amazon RDS).

### Database Performance

#### What Types of Graph Query Workloads Are Optimized to Work with Neptune Database?

Neptune Database is designed to support graph applications that require high throughput and low-latency graph queries. With support for up to 15 read replicas, Neptune Database can support hundreds of thousands of queries per second.

#### Does Neptune Database Perform Query Optimization?

Yes, Neptune uses query optimization for Gremlin, openCypher and SPARQL queries. To learn more, see [the Amazon Neptune alternative query engine (DFE)](https://docs.aws.amazon.com/neptune/latest/userguide/neptune-dfe-engine.html).  

#### Is Neptune Database Built on a Relational Database?

No, Neptune is a purpose-built, high-performance graph database engine. Neptune efficiently stores and navigates graph data, and uses a scale-up, in-memory optimized architecture to allow for fast query evaluation over large graphs.  

### Database Pricing

#### How much Does Neptune Database Cost?

See our [pricing page](https://aws.amazon.com/neptune/pricing/) for current pricing information.

#### In Which AWS Regions is Neptune Database Available?

For more information about the AWS Regions where Neptune Database is available, see the [AWS Regions table](https://aws.amazon.com/about-aws/global-infrastructure/regional-product-services/).

#### Neptune Database Replicates Each Chunk of My Database Volume across Three Availability Zones. Does that Mean that My effective Storage Price Will Be Three times what is Shown on the Pricing Page?

No. Neptune Database replication is bundled into the price. You are charged based on the storage your database consumes at the database layer, not the storage consumed in the Neptune virtualized storage layer.

#### What Are I/O Operations in Neptune Database and how Are They Calculated?

Neptune Database was designed to remove unnecessary I/O operations to reduce costs and ensure resources are available for serving read/write traffic. Write I/O operations are only consumed when pushing transaction log records to the storage layer for the purpose of making writes durable. Write I/O operations are counted in 4 KB units. For example, a transaction log record that is 1,024 bytes will count as one I/O operation.

However, concurrent write operations whose transaction log is less than 4 KB can be batched together by the Neptune database engine in order to optimize I/O consumption. Unlike traditional database engines, Neptune never pushes modified database pages to the storage layer, resulting in further I/O consumption savings.

### Hardware and Scaling

#### What Are the Minimum and Maximum Storage Limits of a Neptune Database?

The minimum storage is 10 GiB. Based on your database usage, your Neptune storage will automatically grow, up to 128 TiB, in 10 GiB increments with no impact to database performance. There is no need to provision storage in advance.

#### How Do I Scale the Compute Resources Associated with My Neptune Database Instance?

You can scale the compute resources allocated to your database instance in the AWS Management Console by selecting the desired database instance and choosing the Modify button. Memory and CPU resources are modified by changing your DB Instance class.

When you modify your DB instance class, your requested changes will be applied during your specified maintenance window. Alternatively, you can use the Apply Immediately flag to apply your scaling requests immediately. Both of these options will have an availability impact for a few minutes as the scaling operation is performed. Bear in mind that any other pending system changes will also be applied.

#### Can I Scale My Neptune Database up and down Automatically Based on Usage?

You can automatically scale your database capacity with [Amazon Neptune Serverless](https://aws.amazon.com/neptune/serverless/). Neptune Serverless allows you to run and instantly scale graph workloads, without the need to manage and optimize capacity. Neptune Serverless automatically determines and provisions the compute and memory resources to run the graph database, and scales capacity based on the workload’s changing requirements to maintain consistent performance.

#### Does Neptune Database Support Auto-scaling?

Yes, Neptune supports auto-scaling of read replicas of instances. You can configure auto-scaling to automatically add or remove read replicas in response to changes in your connectivity or workload requirements. For more information, see the [documentation](https://docs.aws.amazon.com/neptune/latest/userguide/manage-console-autoscaling.html).

### Backup and Restore

#### How Do I Enable Backups for My Neptune Database Instance?

Automated backups are always enabled on Neptune Database instances. Backups do not impact database performance.

#### Can I Take Database Snapshots and Keep Them around as long as I Want?

Yes, and there is no performance impact when taking snapshots. Note that restoring data from database snapshots requires creating a new database instance.

#### If My Database Fails, what is My Recovery Path?

Neptune Database automatically maintains copies of your data across three Availability Zones and will automatically attempt to recover your database in a healthy Availability Zone with no data loss. In the unlikely event your data is unavailable within Neptune storage, you can restore from a database snapshot or perform a point-in-time restore operation to a new instance. Note that the latest restorable time for a point-in-time restore operation can be up to 5 minutes in the past.

#### What Happens to My Automated Backups and Database Snapshots if I Delete My Database Instance?

You can choose to create a final database snapshot when deleting your database Instance. If you do, you can use this database Snapshot to restore the deleted database instance at a later date. Neptune retains this final user-created database Snapshot along with all other manually created database snapshots after the database instance is deleted. Only database snapshots are retained after the database instance is deleted (for example, automated backups created for point-in-time restore are not kept).

#### Can I Share My Snapshots with Another AWS Account?

Yes. Neptune gives you the ability to create snapshots of your databases, which you can use later to restore a database. You can share a snapshot with a different AWS account, and the owner of the recipient account can use your snapshot to restore a database that contains your data. You can even choose to make your snapshots public–that is, anybody can restore a database containing your (public) data. You can use this feature to share data between your various environments (production, dev/test, staging, and more) that have different AWS accounts, as well as keep backups of all your data secure in a separate account in case your main AWS account is ever compromised.

#### Will I Be Billed for Shared Snapshots?

There is no charge for sharing snapshots between accounts. However, you may be charged for the snapshots themselves, as well as any databases you restore from shared snapshots. Learn more about [Amazon Neptune pricing](https://aws.amazon.com/neptune/pricing/).

#### Can I Automatically Share Snapshots?

We do not support sharing automatic database snapshots. To share an automatic snapshot, you must manually create a copy of the snapshot, and then share the copy.

#### How Many Accounts Can I Share Snapshots With?

You may share manual snapshots with up to 20 AWS account IDs. If you want to share the snapshot with more than 20 accounts, you can either share the snapshot as public, or contact support to increase your quota.

#### In Which Regions Can I Share My Neptune Database Snapshots?

You can share your Neptune Database snapshots in AWS Regions where Neptune is available.

#### Can I Share My Neptune Database Snapshots across Different Regions?

No. Your shared Neptune Database snapshots will only be accessible by accounts in the same Region as the account that shares them.

#### Can I Share an Encrypted Neptune Database Snapshot?

Yes, you can share encrypted Neptune Database snapshots.

#### Can I Use Neptune Snapshots outside of the Service?

No, Neptune snapshots can only be used inside of the service.

### High Availability and Replication

#### How Does Neptune Database Improve My database’s Fault Tolerance to Disk Failures?

A Neptune Database cluster can only be created in an Amazon VPC that has at least two subnets in at least two Availability Zones. By distributing your cluster instances across at least two Availability Zones, Neptune helps ensure that there are instances available in your database cluster in the unlikely event of an Availability Zone failure. The cluster volume for your Neptune Database cluster always spans three Availability Zones to provide durable storage with less possibility of data loss. Neptune is designed to transparently handle the loss of up to two copies of data without affecting database write availability and up to three copies without affecting read availability. Neptune storage is also self-healing. Data blocks and disks are continuously scanned for errors and repaired automatically.

#### How Does Neptune Database Improve Recovery time after a Database Crash?

Unlike other databases, after a database crash, Neptune does not need to replay the redo log from the last database checkpoint (typically 5 minutes) and confirm that all changes have been applied before making the database available for operations. This reduces database restart times to less than 60 seconds in most cases. Neptune moves the buffer cache out of the database process and makes it available immediately at restart time. This prevents you from having to throttle access until the cache is repopulated to avoid brownouts.

#### What Kind of Replication Does Neptune Database Support?

Neptune supports read replicas, which share the same underlying volume as the primary instance. Updates made by the primary are visible to all Amazon Neptune Replicas. One Neptune cluster can have one writer instance and up to 15 read replicas. In the event of a writer instance failure, a read replica will be automatically promoted to a writer instance.

#### Can I Have cross-Region Replicas with Neptune Database?

Yes, Neptune Database supports cross-Region replication by configuring your Neptune cluster to use [Neptune Global Database](https://aws.amazon.com/neptune/global-database/).

#### Can I Prioritize Certain Replicas as Failover Targets over Others?

Yes. You can assign a promotion priority tier to each instance on your cluster. When the primary instance fails, Neptune Database will promote the replica with the highest priority to primary. If there is contention between two or more replicas in the same priority tier, then Neptune will promote the replica that is the same size as the primary instance.

#### Can I Modify Priority Tiers for Instances after They Have Been Created?

You can modify the priority tier for an instance at any time. Simply modifying priority tiers will not trigger a failover.

#### Can I Prevent Certain Replicas from Being Promoted to the Primary Instance?

You can assign lower priority tiers to replicas that you don’t want promoted to the primary instance. However, if the higher priority replicas on the cluster are unhealthy or unavailable for some reason, then Neptune will promote the lower priority replica.

#### How Can I Improve upon the Availability of a Single Neptune Database?

You can add Neptune Replicas, which share the same underlying storage as the primary instance. Any Neptune Replica can be promoted to become primary without any data loss and therefore can be used for enhancing fault tolerance in the event of a primary database Instance failure. To increase database availability, simply create 1 to 15 replicas, and Neptune will automatically include them in failover primary selection in the event of a database outage.

#### What Happens during Failover and how long Does it Take?

Failover is automatically handled by Neptune Database so that your applications can resume database operations as quickly as possible without manual administrative intervention. If you have a Neptune Replica, in the same or a different Availability Zone, when failing over, Neptune flips the canonical name record (CNAME) for your database primary endpoint to a healthy replica, which in turn is promoted to become the new primary. From start to finish, failover typically completes within 30 seconds.

Additionally, the read replicas endpoint doesn't require any CNAME updates during failover. If you do not have a Neptune Replica (such as a single instance), Neptune will first attempt to create a new database instance in the same Availability Zone as the original instance. If unable to do so, Neptune will attempt to create a new database instance in a different Availability Zone. From start to finish, failover typically completes in under 15 minutes. Your application should retry database requests in the event of connection loss.

#### If I Have a Primary Database and an Amazon Neptune Database Replica Actively Taking Read Traffic and a Failover Occurs, what Happens?

Neptune Database will automatically detect a problem with your primary instance and begin routing your read/write traffic to a Neptune Database Replica. On average, this failover will complete within 30 seconds. In addition, the read traffic that your Neptune Database Replicas were serving will be briefly interrupted.

#### How far behind the Primary Will My Replicas Be?

Since Neptune Database Replicas share the same data volume as the primary instance, there is virtually no replication lag. We typically observe lag times in the tens of milliseconds.

### Database Security

#### Can I Use Neptune Database in Amazon Virtual Private Cloud (Amazon VPC)?

Yes, all Amazon Neptune Database instances must be created in a VPC. With Amazon VPC, you can define a virtual network topology that closely resembles a traditional network that you might operate in your own datacenter. This gives you complete control over who can access your Neptune databases.

#### Does Neptune Database Support Encrypting My Data in Transit and at Rest?

Neptune Database supports HTTPS encrypted client connections and also allows you to encrypt your databases using keys you manage through AWS KMS. On a database instance running with Neptune encryption, data stored at rest in the underlying storage is encrypted, as are its automated backups, snapshots, and replicas in the same cluster. Encryption and decryption are handled seamlessly. For more information about the use of KMS with Amazon Neptune, see the [Amazon Neptune User Guide](https://docs.aws.amazon.com/neptune/latest/userguide/intro.html).

#### Can I Encrypt an Existing Unencrypted Database?

Currently, encrypting an existing unencrypted Neptune instance is not supported. To use Neptune encryption for an existing unencrypted database, create a new database instance with encryption enabled and migrate your data into it.

#### How Do I Access My Neptune Database?

Access to Neptune databases must be done through the HTTPS port entered on database creation within your VPC. This is done to provide an additional layer of security for your data. Step-by-step instructions on how to connect to your Neptune database are provided in the [Amazon Neptune User Guide](https://docs.aws.amazon.com/neptune/latest/userguide/intro.html).

## Amazon Neptune Analytics

[Query languages](https://aws.amazon.com/neptune/faqs//#Query_languages) | [Analytics performance](https://aws.amazon.com/neptune/faqs//#Analytics_performance) | [Vector search](https://aws.amazon.com/neptune/faqs//#Vector_search) | [Analytics security](https://aws.amazon.com/neptune/faqs//#Analytics_security) | [Analytics pricing](https://aws.amazon.com/neptune/faqs//#Analytics_pricing)

### Query Languages

#### What Popular Graph Query Languages Does Amazon Neptune Analytics Support?

You can use openCypher, an open-source project that makes it easy to use the Cypher language for graph processing, invoking the Neptune Analytics algorithms, and for vector similarity search.

### Analytics Performance

#### What Types of Graph Query Workloads Are Optimized to Work with Neptune Analytics?

Neptune Analytics is well suited for graph queries that access large parts of a graph or whole graphs. Neptune Analytics is an in-memory engine, and it can load these large graphs into memory to deliver a response in seconds. In addition, Neptune Analytics can serve thousands of analytic queries per second using a library of popular graph analytics algorithms for operations such as ranking social influencers, detecting groups for fraud, or finding patterns in network activity. For generative AI applications, Neptune Analytics can store vector embeddings and provide vector similarity searches.

#### How Can I Use Neptune Analytics with Graphs in My Neptune Database?

You can select an existing Neptune cluster as the data source, which will be automatically loaded into Neptune Analytics.

#### Which Graph Algorithms Are Supported Today?

Neptune Analytics supports 12 algorithms for path finding, detecting communities (clustering), identifying important data (centrality), and quantifying similarity. Path finding algorithms are used for use cases such as route planning for supply chain optimization, while centrality algorithms such as page rank identify the most influential sellers in a graph. Similarly, algorithms such as connected components, clustering, and centrality algorithms can be used for fraud-detection use cases to determine whether the connected network is a group of friends or a fraud ring formed by a set of coordinated fraudsters.

#### Is Neptune Analytics ACID Compliant?

Yes, Neptune Analytics is ACID compliant with strong consistency.

### Vector search

#### What is the Maximum Dimensionality of Vectors Supported with Neptune Analytics?

Neptune Analytics supports a vector search index on embeddings (up to 65,000 dimensions) stored in your graph data.

#### How Many Indices Can I Add?

Neptune Analytics supports one vector search index on embeddings stored in your graph data.

#### Do I Need a Separate Vector Database with Neptune Analytics?

No, you do not need a separate vector database with Neptune Analytics. Neptune Analytics supports a vector search index on embeddings (up to 65,000 dimensions) stored in your graph data. Neptune Analytics provides efficient vector search that can be invoked directly from the openCypher query language that is used for writing your graph queries.

Neptune Analytics stores the vectors and supports Hierarchical Navigable Small Worlds (HNSW) for performing vector indexing and similarity search. You should use a separate vector database if you want to use different indexing and similarity search algorithms or if you want to use multiple indices built on different properties.

### Analytics Security

#### Can I Use Neptune Analytics in Amazon VPC?

Yes, you can use Neptune Analytics in Amazon VPC. For private access, you can create a graph with ‘public-access’ disabled (default) and specify the subnets in a VPC. Neptune Analytics will create a requester-managed VPC interface endpoint per graph in your VPC. You will be able to attach security groups and endpoint policies to the endpoints, but you will not be able to delete the endpoints. Standard VPC interface endpoint charges will apply.

#### Can I Access Neptune Analytics over the Public Internet?

Yes. You can optionally enable a public graph-specific endpoint to connect to the graph over the internet. With Neptune Analytics, all clients must authenticate, all requests need to be SigV4-signed, and all connections must use the graph ID to interact with the graph.

#### Does Neptune Analytics Support High Availability?

Yes, Neptune Analytics offers Multi-AZ deployments with enhanced availability and durability. By default, it provisions a hot standby in a separate Availability Zone. With a hot standby, the failover time is in seconds. Without a standby, the service provisions new underlying compute capacity within minutes.

### Analytics Pricing

#### How much Does Neptune Analytics Cost?

Visit the [Neptune Pricing page](https://aws.amazon.com/neptune/pricing/) for current pricing information.

#### In Which Regions is Neptune Analytics Available?

For more information about the Regions where Neptune Analytics is available, see the [AWS Regions table](https://aws.amazon.com/about-aws/global-infrastructure/regional-product-services/).

## Amazon Neptune ML

#### What Languages Are Supported with Neptune ML?

Gremlin and SPARQL are supported with Neptune ML.