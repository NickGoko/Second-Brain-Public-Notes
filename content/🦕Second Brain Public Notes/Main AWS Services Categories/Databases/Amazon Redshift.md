---
tags:
  - cloud/aws
---
![[Pasted image 20240214155712.png]]  
![[Pasted image 20240214162820.png]]

![[Module 5- adding a database layer#^0be5e5|Amazon Redshift]]

Amazon RedShift is <mark style="background: #D2B3FFA6;">a fast, fully managed data warehouse that makes it simple and cost-effective to analyze all your data using standard SQL and existing Business Intelligence (BI) tools.</mark>  
<mark style="background: #BBFABBA6;">Amazon RedShift is a clustered peta-byte scale data warehouse and is an SQL based data warehouse used for</mark> **analytics applications**.

Amazon RedShift is an **Online Analytics Processing (OLAP)** type of Database which <mark style="background: #FF5582A6;">can be used for running complex analytic queries against petabytes of structured data, using sophisticated query optimization, columnar storage on high-performance local disks, and massively parallel query execution</mark>.  
Amazon RedShift is also ideal for processing large amounts of data for business intelligence.

![[Pasted image 20240214163547.png]]
## Advantages of Amazon RedShift

_The benefits of Amazon RedShift are as follows:_
- Amazon RedShift is extremely cost-effective as compared to some other on-premises data warehouse platforms.
- Amazon RedShift is PostgreSQL compatible with JDBC and ODBC drivers available; compatible with most Business Intelligence tools out of the box.
- Features parallel processing and columnar data stores which are optimized for complex queries.
- <mark style="background: #FFB86CA6;">Option to query directly from data files on S3 via Amazon RedShift Spectrum</mark>.  
	  ![[Pasted image 20240214163633.png]]
- Amazon RedShift is 10x faster than a traditional SQL DB.
- <mark style="background: #FFB86CA6;">Amazon RedShift can store huge amounts of data but cannot ingest huge amounts of data in real time.</mark>

Amazon RedShift uses columnar data storage:
- <mark style="background: #FFB8EBA6;">Data is stored sequentially in columns instead of rows</mark>.
- <mark style="background: #FFF3A3A6;">Columnar based DB is ideal for data warehousing and analytics</mark>.
- <mark style="background: #FFB8EBA6;">Requires fewer I/Os which greatly enhances performance</mark>.

Amazon RedShift provides advanced compression:
- Data is stored sequentially in columns which allows for much better performance and less storage space.
- Amazon RedShift automatically selects the compression scheme.

Amazon RedShift provides good query performance and compression.

Amazon RedShift provides Massively Parallel Processing (MPP) by distributing data and queries across all nodes.

## Availability and Durability
![](https://i.imgur.com/xRMjzIG.png)

**Amazon RedShift** <mark style="background: #BBFABBA6;">uses replication and continuous backups to enhance availability and improve durability and can automatically recover from component and node failures.</mark>

- <mark style="background: #ADCCFFA6;">Only available in one AZ but you can restore snapshots into another AZ.</mark>

Alternatively, <mark style="background: #D2B3FFA6;">you can run data warehouse clusters in multiple AZ’s by loading data into two Amazon RedShift data warehouse clusters in separate AZs from the same set of Amazon S3 input files</mark>.

Amazon RedShift <mark style="background: #FFF3A3A6;">replicates your data within your data warehouse cluster and continuously backs up your data to Amazon S3.</mark>

Amazon RedShift always keeps three copies of your data:
- The original.
- <mark style="background: #CACFD9A6;">A replica of compute nodes (within the cluster)</mark>.
- <mark style="background: #CACFD9A6;">A backup copy on S3.</mark>

Amazon RedShift provides continuous/incremental backups:
- Multiple copies within a cluster.
- <mark style="background: #FFB86CA6;">Continuous and incremental backups to S3</mark>.
- Continuous and incremental backups across regions.
- Streaming restore.

Amazon RedShift provides fault tolerance for the following failures: 
- Disk failures.
- Node failures.
- Network failures.
- AZ/region level disasters.

For node failures the data warehouse cluster will be unavailable for queries and updates until a replacement node is provisioned and added to the DB.

High availability for Amazon RedShift:
- Currently, Amazon RedShift does not support Multi-AZ deployments.
- The <mark style="background: #FFF3A3A6;">best HA option is to use a multi-node cluster which supports data replication and node recovery.</mark>
- A single node Amazon RedShift cluster does not support data replication and you’ll have to restore from a snapshot on S3 if a drive fails.

<mark style="background: #FFF3A3A6;">Amazon RedShift can asynchronously replicate your snapshots to S3 in another region for DR</mark>.

Single-node clusters do not support data replication (in a failure scenario you would need to restore from a snapshot).

Scaling requires a period of unavailability of a few minutes (typically during the maintenance window).

During scaling operations Amazon RedShift moves data in parallel from the compute nodes in your existing data warehouse cluster to the compute nodes in your new cluster.

By default, Amazon RedShift retains backups for 1 day. You can configure this to be up to 35 days.

If you delete the cluster, you can choose to have a final snapshot taken and retained.

Manual backups are not automatically deleted when you delete a cluster.

## Security

You can load encrypted data from S3.

Supports SSL Encryption in-transit between client applications and Amazon RedShift data warehouse cluster.

VPC for network isolation.

Encryption for data at rest (AES 256).

Audit logging and AWS CloudTrail integration.

Amazon RedShift takes care of key management, or you can manage your own through HSM or KMS.

## Charges

Charged for compute nodes hours, 1 unit per hour (only compute node, not leader node).

Backup storage – storage on S3.

Data transfer – no charge for data transfer between Amazon RedShift and S3 within a region but for other scenarios you may pay charges.

HDD and SSD storage options.

The size of a single node is 160GB and clusters can be created up to a petabyte or more.

Multi-node consists of:

Leader node:

- Manages client connections and receives queries.
- Simple SQL endpoint.
- Stores metadata.
- Optimizes query plan.
- Coordinates query execution.

Compute nodes:

- Stores data and performs queries and computations.
- Local columnar storage.
- Parallel/distributed execution of all queries, loads, backups, restores, resizes.
- Up to 128 compute nodes.

Amazon RedShift Spectrum is a feature of Amazon RedShift that enables you to run queries against exabytes of unstructured data in Amazon S3, with no loading or ETL required.

## Use Cases of Amazon RedShift

A data warehouse for enterprise operations: Many organizations work with data from multiple sources, such as advertising, customer relationship management, and customer support.

As a centralized repository, Redshift can be used to store data from multiple sources in a unified schema and structure. This can then feed enterprise-wide reporting and analytics.

In business intelligence and analytics, Redshift’s fast query execution against terabyte-scale data makes it an excellent selection. BI tools such as Tableau often use Redshift as the underlying database (which would otherwise struggle to perform queries and joins of large datasets).

Organizations may choose to monetize their data by exposing it to their customers through embedded analytics and analytics as a service. In these scenarios, Redshift’s data sharing, search, and aggregation capabilities make it ideal, as it allows customers to access only relevant subsets of data while keeping other databases, tables, or rows confidential.

As long as the cluster is adequately resourced, Redshift’s performance is consistent and predictable. It is therefore a popular choice for data-driven applications, such as reporting and calculations.

Database migration and change data capture: AWS Database Migration Service (DMS) can be used to replicate changes in an operational data store into Amazon Redshift. It is typically done to provide more flexibility in analysis, or when migrating from legacy data warehouses.

# FAQ
## General

Close all

### What is Amazon Redshift?

Tens of thousands of customers use Amazon Redshift every day to run SQL analytics in the cloud, processing exabytes of data for business insights. Whether your growing data is stored in operational data stores, data lakes, streaming data services or third-party datasets, Amazon Redshift helps you securely access, combine, and share data with minimal movement or copying. Amazon Redshift is deeply integrated with AWS database, analytics, and machine learning services to employ Zero-ETL approaches or help you access data in place for near real-time analytics, build machine learning models in SQL, and enable Apache Spark analytics using data in Redshift. Amazon Redshift Serverless enables your engineers, developers, data scientists, and analysts to get started easily and scale analytics quickly in a zero-administration environment. With its Massively Parallel Processing (MPP) engine and architecture that separates compute and storage for efficient scaling, and machine learning driven performance innovations (for example: AutoMaterialized Views), Amazon Redshift is built for scale and delivers up to 5x better price performance than other cloud data warehouses.

### What Are the top Reasons Customers Choose Amazon Redshift?

Thousands of customers choose Amazon Redshift to accelerate their time to insights because it is a powerful analytics system that integrates well with database and machine learning services, is streamlined to use, and can become a central service to deliver on all their analytics needs. Amazon Redshift Serverless automatically provisions and scales data warehouse capacity to deliver high performance for demanding and unpredictable workloads. Amazon Redshift offers leading price performance for diverse analytics workloads, whether it is dashboarding, application development, data sharing, ETL (Extract, Transform, Load) jobs or several others. With tens of thousands of customers running analytics on terabytes to petabytes of data, Amazon Redshift optimizes real-world customer workload performance, based on fleet performance telemetry, and delivers performance that scales linearly to the workload, while keeping costs low. Performance innovations are available to customers at no additional cost. Amazon Redshift lets you get insights from running real-time and predictive analytics on all your data across your operational databases, data lake, data warehouse, streaming data, and third-party datasets. Amazon Redshift supports industry-leading security with built-in identity management and federation for single sign-on (SSO), multi-factor authentication, column-level access control, row-level security, role-based access control, Amazon Virtual Private Cloud (Amazon VPC), and faster cluster resize.

### How Does Amazon Redshift Simplify Data Warehouse and Analytics Management?

Amazon Redshift is fully managed by AWS so you no longer need to worry about data warehouse management tasks such as hardware provisioning, software patching, setup, configuration, monitoring nodes and drives to recover from failures, or backups. AWS manages the work needed to set up, operate, and scale a data warehouse on your behalf, freeing you to focus on building your applications. Amazon Redshift Serverless automatically provisions and scales the data warehouse capacity to deliver high performance for demanding and unpredictable workloads, and you pay only for the resources you use. Amazon Redshift also has automatic tuning capabilities, and surfaces recommendations for managing your warehouse in Redshift Advisor. With Redshift Spectrum, Amazon Redshift manages all the computing infrastructure, load balancing, planning, scheduling, and execution of your queries on data stored in Amazon S3. Amazon Redshift enables analytics on all your data with deep integration into database services with features like Amazon Aurora Zero-ETL to Amazon Redshift and federated querying to access data in place from operational databases like Amazon RDS and your Amazon S3 data lake. Redshift enables streamlined data ingestion with no-code, automated data pipelines that ingest streaming data or Amazon S3 files automatically. Redshift is also integrated with AWS Data Exchange enabling users to find, subscribe to, and query third party datasets and combine with their data for comprehensive insights. With native integration into Amazon SageMaker, customers can stay right within their data warehouse and create, train, and build machine learning models in SQL. Amazon Redshift delivers on all your SQL analytics needs with up to 5x better price performance than other cloud data warehouses.

### What Are the Deployment Options for Amazon Redshift?

Amazon Redshift is a fully managed service and offers both provisioned and serverless options, making it more efficient for you to run and scale analytics without having to manage your data warehouse. You can spin up a new Amazon Redshift Serverless endpoint to automatically provision the data warehouse in seconds or you can choose the provisioned option for predictable workloads.

### How Do I Get Started with Amazon Redshift?

With just a few steps in the AWS Management Console, you can start querying data. You can take advantage of pre-loaded sample datasets, including benchmark datasets TPC-H, TPC-DS, and other sample queries to kick start analytics immediately. To get started with Amazon Redshift Serverless, choose “Try Amazon Redshift Serverless” and start querying data. [Get started here](https://aws.amazon.com/redshift/getting-started/).

### How Does the Performance of Amazon Redshift Compare to that of other Data Warehouses?

TPC-DS benchmark results show that Amazon Redshift provides the best price performance out of the box, even for a comparatively small 3 TB dataset. Amazon Redshift delivers up to 5x better price performance than other cloud data warehouses. This means that you can benefit from Amazon Redshift’s leading price performance from the start without manual tuning. Based on our performance fleet telemetry, we also know that most workloads are short query workloads (workloads that run in less than 1 second). For these workloads, the latest benchmarks demonstrate that Amazon Redshift offers up to 7x better price performance on high concurrency, low latency workloads than other cloud data warehouses. [Learn more here](https://aws.amazon.com/blogs/big-data/amazon-redshift-continues-its-price-performance-leadership/).

### Can I Get Help to Learn More about and Onboard to Amazon Redshift?

Yes, Amazon Redshift specialists are available to answer questions and provide support. [Contact us](https://aws.amazon.com/contact-us/sales-support-redshift/) and you’ll hear back from us in one business day to discuss how AWS can help your organization.

### What is Amazon Redshift Managed Storage?

Amazon Redshift managed storage is available with serverless and RA3 node types and lets you scale and pay for compute and storage independently so you can size your cluster based only on your compute needs. It automatically uses high-performance SSD-based local storage as tier-1 cache and takes advantage of optimizations such as data block temperature, data block age, and workload patterns to deliver high performance while scaling storage automatically to Amazon S3 when needed without requiring any action.

### How Do I Use Amazon Redshift’s Managed Storage?

If you are already using Amazon Redshift Dense Storage or Dense Compute nodes, you can use Elastic Resize to upgrade your existing clusters to the new compute instance RA3. Amazon Redshift Serverless and clusters using the RA3 instance automatically use Redshift-managed storage to store data. No other action outside of using Amazon Redshift Serverless or RA3 instances is required to use this capability.

### How Can I Run Queries from Redshift for the Data Stored in the AWS Data Lake?

Amazon Redshift Spectrum is a feature of Amazon Redshift that lets you run queries against your data lake in Amazon S3, with no data loading or ETL required. When you issue an SQL query, it goes to the Amazon Redshift endpoint, which generates and optimizes a query plan. Amazon Redshift determines what data is local and what is in Amazon S3, generates a plan to minimize the amount of S3 data that must be read, and requests Amazon Redshift Spectrum workers out of a shared resource pool to read and process data from Amazon S3.

### When Should I Consider Using RA3 Instances?

Consider choosing RA3 node types in these cases:

- You need the flexibility to scale and pay for compute separate from storage.
- You query a fraction of your total data.
- Your data volume is growing rapidly or is expected to grow rapidly.
- You want the flexibility to size the cluster based only on your performance needs.

As the scale of data continues to grow, reaching petabytes, the amount of data you ingest into your Amazon Redshift data warehouse is also growing. You might be looking for ways to cost-effectively analyze all your data.

With new Amazon Redshift RA3 instances with managed storage, you can choose the number of nodes based on your performance requirements, and pay only for the managed storage that you use. This gives you the flexibility to size your RA3 cluster based on the amount of data you process daily without increasing your storage costs. Built on the AWS Nitro System, RA3 instances with managed storage use high performance SSDs for your hot data and Amazon S3 for your cold data, providing ease of use, cost-effective storage, and fast query performance.

### What Feature Can I Use for Location-based Analytics?

Amazon Redshift spatial provides location-based analytics for rich insights into your data. It seamlessly integrates spatial and business data to provide analytics for decision making. [Amazon Redshift launched native spatial data processing support in November 2019](https://aws.amazon.com/about-aws/whats-new/2019/11/amazon-redshift-announces-support-spatial-data/), with a polymorphic data type GEOMETRY and several key SQL spatial functions. We now support GEOGRAPHY data type, and our library of SQL spatial functions has grown to 80. We support all the common spatial data types and standards, including Shapefiles, GeoJSON, WKT, WKB, eWKT, and eWKB. To learn more, visit the [documentation](https://docs.aws.amazon.com/redshift/latest/dg/geospatial-overview.html) page or the [Amazon Redshift spatial tutorial](https://docs.aws.amazon.com/redshift/latest/dg/spatial-tutorial.html) page.

### How Does Athena’s SQL Support Compare to Redshift, and how Do I Choose between the Two Services?

Amazon Athena and Amazon Redshift Serverless address different needs and use cases even if both services are serverless and enable SQL users.

With its Massively Parallel Processing (MPP) architecture that separates storage and compute and machine learning led automatic optimization capabilities, a data warehouse like Amazon Redshift, whether it's serverless or provisioned, is a great choice for customers that need the best price performance at any scale for complex BI and analytics workloads. Customers can use Amazon Redshift as a central component of their data architecture with deep integrations available to access data in place or ingest or move data easily into the warehouse for high performance analytics, through ZeroETL and no-code methods. Customers can access data stored in Amazon S3, operational databases like Aurora and Amazon RDS, third party data warehouses through the integration with AWS Data Exchange, and combine with data stored in the Amazon Redshift data warehouse for analytics. They can get data warehousing started easily and conduct machine learning on top of all this data.

Amazon Athena is well suited for interactive analytics and data exploration of data in your data lake or any data source through an extensible connector framework (includes 30-plus out-of-box connectors for applications and on premises or other cloud analytics systems) without worrying about ingesting or processing data. Amazon Athena is built on open-source engines and frameworks such as Spark, Presto, and Apache Iceberg, giving customers the flexibility to use Python or SQL or work on open data formats. If customers want to do interactive analytics using open-source frameworks and data formats, Amazon Athena is a great place to start.

## Serverless

Close all

### What is Amazon Redshift Serverless?

Amazon Redshift Serverless is a serverless option of Amazon Redshift that makes it more efficient to run and scale analytics in seconds without the need to set up and manage data warehouse infrastructure. With Redshift Serverless, any user—including data analysts, developers, business professionals, and data scientists—can get insights from data by simply loading and querying data in the data warehouse.

### How Do I Get Started with Amazon Redshift Serverless

With just a few steps in the AWS Management Console, you can choose "configure Amazon Redshift Serverless" and begin querying data. You can take advantage of preloaded sample datasets, such as weather data, census data, and benchmark datasets, along with sample queries to kick start analytics immediately. You can create databases, schemas, tables, and load data from Amazon S3, Amazon Redshift data shares, or restore from an existing Redshift provisioned cluster snapshot. You can also directly query data in open formats (such as Parquet or ORC) in the Amazon S3 data lake, or query data in operational databases, such as Amazon Aurora and Amazon RDS PostgreSQL and MySQL. See Getting Started Guide.

### What Are the Benefits of Using Amazon Redshift Serverless?

If you don't have data warehouse management experience, you don’t have to worry about setting up, configuring, managing clusters or tuning the warehouse. You can focus on deriving meaningful insights from your data or delivering on your core business outcomes through data. You pay only for what you use, keeping costs manageable. You continue to benefit from all of Amazon Redshift’s top-notch performance, rich SQL features, seamless integration with data lakes and operational data warehouses, and built-in predictive analytics and data sharing capabilities. If you need fine-grained control of your data warehouse, you can provision Redshift clusters.

### How Does Amazon Redshift Serverless Work with other AWS Services?

You can continue to use all the rich analytics functionality of Amazon Redshift, such as complex joins, direct queries to data in the Amazon S3 data lake and operational databases, materialized views, stored procedures, semistructured data support, and ML, as well as high performance at scale. All the related services that Amazon Redshift integrates with (such as Amazon Kinesis, AWS Lambda, Amazon QuickSight, Amazon SageMaker, Amazon EMR, AWS Lake Formation, and AWS Glue) continue to work with Amazon Redshift Serverless.

### What Use Cases Can I Handle with Amazon Redshift Serverless?

You can continue to run all analytics use cases. With a simple getting started workflow, automatic scaling, and the ability to pay for use, the Amazon Redshift Serverless experience now makes it even more efficient and more cost-effective to run development and test environments that must get started quickly, ad-hoc business analytics, workloads with varying and unpredictable compute needs, and intermittent or sporadic workloads.

## Data Ingestion and Loading

Close all

### How Do I Load Data into My Amazon Redshift Data Warehouse?

You can load data into Amazon Redshift from a range of data sources including [Amazon S3](https://aws.amazon.com/s3), [Amazon RDS](https://aws.amazon.com/rds), [Amazon DynamoDB](https://aws.amazon.com/dynamodb/), [Amazon EMR](https://aws.amazon.com/emr/), [AWS Glue](https://aws.amazon.com/glue/), [AWS Data Pipeline](https://aws.amazon.com/datapipeline), and or any SSH-enabled host on Amazon EC2 or on-premises. Amazon Redshift attempts to load your data in parallel into each compute node to maximize the rate at which you can ingest data into your data warehouse cluster. Clients can connect to Amazon Redshift using ODBC or JDBC and issue 'insert' SQL commands to insert the data. Please note this is slower than using S3 or DynamoDB since those methods load data in parallel to each compute node while SQL insert statements load through the single leader node. For more details on loading data into Amazon Redshift, please view our [Getting-started guide](https://docs.aws.amazon.com/redshift/latest/gsg/welcome.html).

### How is Redshift Auto-copy Different than the Copy Command?

Redshift auto-copy provides the ability to automate copy statements by tracking Amazon S3 folders and ingesting new files without customer intervention. Without auto-copy, a copy statement immediately starts the file ingestion process for existing files. Auto-copy extends the existing copy command and provides the ability to 1/ automate file ingestion process by monitoring specified Amazon S3 paths for new files, 2/ re-use copy configurations, reducing the need to create and run new copy statements for repetitive ingestion tasks and 3/ keep track of loaded files to avoid data duplication.

### How Do I Get Started with Redshift Auto-copy?

To get started, customers should have an Amazon S3 folder, which can be accessed by their Redshift cluster/serverless endpoint using associated IAM roles, and create a Redshift table to be used as a target. Once an Amazon S3 path and the Redshift table are ready, customers can create a copy job by using the copy command. Once the copy job is created, Redshift starts tracking the specified Amazon S3 path behind the scenes and initiates the user defined copy statements to automatically copy new files into the target table.

### What Are the Use Cases for Amazon Redshift Integration for Apache Spark?

The key use cases include: 1/ Customers using Amazon EMR and AWS Glue to run Apache Spark jobs that access and load data into Amazon Redshift as part of the data ingestion and transformation pipelines (batch and streaming) 2/ Customers using Amazon SageMaker to perform machine learning using Apache Spark and must access data stored in Amazon Redshift for feature engineering and transformation. 3/Amazon Athena customers using Apache Spark to perform interactive analysis on data in Amazon Redshift.

### What Are the Benefits of Amazon Redshift Integration for Apache Spark?

Baikal provides the following benefits:

- Ease of use for getting started and running Apache Spark applications on data in Amazon Redshift without having to worry about manual steps involved to setup and maintain uncertified versions of the Spark
- Convenience of using Apache Spark from various AWS services such as Amazon EMR, AWS Glue, Amazon Athena, and Amazon SageMaker with Amazon Redshift with minimal configuration
- Improved performance while running Apache Spark applications on Amazon Redshift

### When Should I Use Amazon Aurora Zero-ETL to Amazon Redshift instead of Federated Querying?

Amazon Aurora Zero-ETL to Amazon Redshift enables Amazon Aurora and Amazon Redshift customers to run near real-time analytics and machine learning on petabytes of transactional data by offering a fully managed solution for making transactional data from Amazon Aurora available in Amazon Redshift within seconds of being written. With Amazon Aurora Zero-ETL to Amazon Redshift, customers simply choose the Amazon Aurora tables containing the data they want to analyze with Amazon Redshift, and the feature seamlessly replicates the schema and data into Amazon Redshift. It reduces the need for customers to build and manage complex data pipelines, so they can instead focus on improving their applications. With Amazon Aurora Zero-ETL to Amazon Redshift, customers can replicate data from multiple Amazon Aurora database clusters into the same Amazon Redshift instance to derive comprehensive insights across several applications, while also consolidating their core analytics assets, gaining significant cost savings and operational efficiencies. With Amazon Aurora Zero-ETL to Amazon Redshift, customers can also access the core analytics and machine learning capabilities of Amazon Redshift such as materialized views, data sharing, and federated access to multiple data stores and data lakes. This enables customers to combine near real-time and core analytics to effectively derive time sensitive insights that inform business decisions. Furthermore, customers use Amazon Aurora for transactions and Amazon Redshift for analytics, so there are no shared compute resources, yielding a performant and operationally stable solution.

### How Does Amazon Aurora Zero-ETL to Amazon Redshift Relate to/work with other AWS Services?

Amazon Aurora Zero-ETL Integration with Amazon Redshift offers seamless integration between the two services for transactional analytics.

### How Does Streaming Ingestion Work?

Streaming data are different from traditional database tables in that when you query a stream, you are capturing the evolution of a time-varying relation. Tables, on the other hand, capture a point-in-time snapshot of this time-varying relation. Amazon Redshift’s customers are accustomed to operating on regular tables and perform downstream processing (i.e. transformations) of data using a traditional batch model, for example “ELT”. We provide a method to use Redshift Materialized Views (MVs) so that customers can easily materialize a point-in-time view of the stream, as accumulated up to the time it is queried, as fast as possible to support ELT workflows.

## Data Sharing

Close all

### What Are the Use Cases for Data Sharing?

Key use cases include:

- A central ETL cluster sharing data with many BI/analytics clusters to provide read workload isolation and optional charge-ability.
- A data provider sharing data to external consumers.
- Sharing common datasets such as customers, products across different business groups and collaborating for broad analytics and data science.
- Decentralizing a data warehouse to simplify management.
- Sharing data between development, test, and production environments.
- Accessing Redshift data from other AWS analytic services.

### What Are Cross-database Queries in Amazon Redshift?

With cross-database queries, you can seamlessly query and join data from any Redshift database that you have access to, regardless of which database you are connected to. This can include databases local on the cluster and also shared datasets made available from remote clusters. Cross-database queries give you flexibility to organize data as separate databases to support multi-tenant configurations.

### Who Are the Primary Users of AWS Data Exchange?

[AWS Data Exchange](https://aws.amazon.com/data-exchange/) makes it more efficient for AWS customers to securely exchange and use third-party data in AWS. Data analysts, product managers, portfolio managers, data scientists, quants, clinical trial technicians, and developers in nearly every industry would like access to more data to drive analytics, train ML models, and make data-driven decisions. But there is no one place to find data from multiple providers and no consistency in how providers deliver data, leaving them to deal with a mix of shipped physical media, FTP credentials, and bespoke API calls. Conversely, many organizations would like to make their data available for research or commercial purposes, but it’s too hard and expensive to build and maintain data delivery, entitlement, and billing technology, which further depresses the supply of valuable data.

## Scalability and Concurrency

Close all

### How Do I Scale the Size and Performance of My Amazon Redshift Data Warehouse Cluster?

Amazon Redshift Serverless automatically provisions data warehouse capacity and intelligently scales the underlying resources. Amazon Redshift Serverless adjusts capacity in seconds to deliver consistently high performance and simplified operations for even the most demanding and volatile workloads. With the Concurrency Scaling feature, you can support unlimited concurrent users and concurrent queries, with consistently fast query performance. When concurrency scaling is enabled, Amazon Redshift automatically adds cluster capacity when your cluster experiences increase in query queueing.

For manual scaling, If you would like to increase query performance or respond to CPU, memory, or I/O overutilization, you can increase the number of nodes within your data warehouse cluster using Elastic Resize through the [AWS Management Console](https://aws.amazon.com/console/) or the [ModifyCluster](https://docs.aws.amazon.com/redshift/latest/APIReference/API_ModifyCluster.html) API. When you modify your data warehouse cluster, your requested changes will be applied immediately. Metrics for compute utilization, storage utilization, and read/write traffic to your Redshift data warehouse cluster are available free of charge through the AWS Management Console or Amazon CloudWatch APIs. You can also add user-defined metrics through [Amazon CloudWatch](https://aws.amazon.com/cloudwatch/) custom metric functionality.

With Amazon Redshift Spectrum, you can run multiple Redshift clusters accessing the same data in Amazon S3. You can use different clusters for different use cases. For example, you can use one cluster for standard reporting and another for data science queries. Your marketing team can use their own clusters different from your operations team. Redshift Spectrum automatically distributes the execution of your query to several Redshift Spectrum workers out of a shared resource pool to read and process data from Amazon S3, and pulls results back into your Redshift cluster for any remaining processing.

### Will My Data Warehouse Cluster Remain Available during Scaling?

It depends. When you using the Concurrency Scaling feature, the cluster is fully available for read and write during concurrency scaling. With Elastic resize, the cluster is unavailable for four to eight minutes of the resize period. With the Redshift RA3 storage elasticity in managed storage, the cluster is fully available and data is automatically moved between managed storage and compute nodes.

### What is Elastic Resize and how is it Different from Concurrency Scaling?

Elastic Resize adds or removes nodes from a single Redshift cluster within minutes to manage its query throughput. For example, an ETL workload for certain hours in a day or month-end reporting might need additional Amazon Redshift resources to complete on time. Concurrency Scaling adds additional cluster resources to increase the overall query concurrency.

### Can I Access the Concurrency Scaling Clusters Directly?

No. Concurrency Scaling is a massively scalable pool of Amazon Redshift resources and customers do not have direct access.

## Security

Close all

### How Does Amazon Redshift Keep My Data Secure?

Amazon Redshift supports industry-leading security with built-in identity management and federation for single sign-on (SSO), multi-factor authentication, column-level access control, row-level security, role-based access control, and Amazon Virtual Private Cloud (Amazon VPC). With Amazon Redshift, your data is encrypted in transit and at rest. All Amazon Redshift security features are offered out-of-the-box at no additional cost to satisfy the most demanding security, privacy, and compliance requirements. You get the benefit of AWS supporting more security standards and compliance certifications than any other provider, including ISO 27001, SOC, HIPAA/HITECH, and FedRAMP.

### Does Redshift Support Granular Access Controls?

Yes, Amazon Redshift provides support for role-based access control. Row-level access control allows you to assign one or more roles to a user, and assign system and object permissions by role. You can use out-of-the-box system roles–root user, dba, operator, and security admins, or create your own roles.

### Does Amazon Redshift Support Data Masking or Data Tokenization?

AWS Lambda user-defined functions (UDFs) enable you to use an AWS Lambda function as a UDF in Amazon Redshift and invoke it from Redshift SQL queries. This functionality enables you to write custom extensions for your SQL query to achieve tighter integration with other services or third-party products. You can write Lambda UDFs to enable external tokenization, data masking, identification or de-identification of data by integrating with vendors like Protegrity, and protect or unprotect sensitive data based on a user’s permissions and groups, in query time.

With support for dynamic data masking, customers can easily protect their sensitive data and control granular access by managing Data Masking policies. Suppose you have applications that have multiple users and objects with sensitive data that cannot be exposed to all the users. You have requirements to provide a different granular security level that you want to give different groups of users. Redshift Dynamic Data Masking is configurable to allow customers to define consistent, format-preserving, and irreversible masked data values. Once the feature is GA, you begin using it immediately. The security admins can create and apply policies with just a few commands.

### Does Amazon Redshift Support Single Sign-on?

Yes. Customers who want to use their corporate identity providers such as Microsoft Azure Active Directory, Active Directory Federation Services, Okta, Ping Federate, or other SAML compliant identity providers can configure Amazon Redshift to provide single sign-on. You can sign on to Amazon Redshift cluster with Microsoft Azure Active Directory (AD) identities. This allows you to be able to sign on to Redshift without duplicating Azure Active Directory identities in Redshift.

### Does Amazon Redshift Support Multi-factor Authentication (MFA)?

Yes. You can use multi-factor authentication (MFA) for additional security when authenticating to your Amazon Redshift cluster.

## Availability and Durability

Close all

### What Happens to My Data Warehouse Cluster Availability and Data Durability in the Event of Individual Node Failure?

Amazon Redshift will automatically detect and replace a failed node in your data warehouse cluster. On Dense Compute (DC) and Dense Storage (DS2) clusters, the data is stored on the compute nodes to ensure high data durability. When a node is replaced, the data is refreshed from the mirror copy on the other node. RA3 clusters and Redshift serverless are not impacted the same way since the data is stored in Amazon S3 and the local drive is just used as a data cache. The data warehouse cluster will be unavailable for queries and updates until a replacement node is provisioned and added to the DB. Amazon Redshift makes your replacement node available immediately and loads your most frequently accessed data from Amazon S3 first to allow you to resume querying your data as quickly as possible. Single node clusters do not support data replication. In the event of a drive failure, you must restore the cluster from snapshot on S3. We recommend using at least two nodes for production.

### What Happens to My Data Warehouse Cluster Availability and Data Durability if My Data Warehouse Cluster's Availability Zone (AZ) Has an Outage?

If your Amazon Redshift data warehouse is a single-AZ deployment and the cluster's Availability Zone becomes unavailable, then Amazon Redshift will automatically move your cluster to another AWS Availability Zone (AZ) without any data loss or application changes. To activate this, you must enable the relocation capability in your cluster configuration settings.

### Why Should I Use a Redshift Multi-AZ Deployment?

Unlike single-AZ deployments, customers can now improve availability of Redshift by running their data warehouse in a multi-AZ deployment. A multi-AZ deployment allows you to run your data warehouse in multiple AWS Availability Zones (AZ) simultaneously and continue operating in unforeseen failure scenarios. No application changes are required to maintain business continuity since the Multi-AZ deployment is managed as a single data warehouse with one endpoint. Multi-AZ deployments reduce recovery time by guaranteeing capacity to automatically recover and are intended for customers with business-critical analytics applications that require the highest levels of availability and resiliency to AZ failures. This also allows customers to implement a solution that is more compliant with the recommendations of the Reliability Pillar of the AWS Well-Architected Framework. To learn more about Amazon Redshift Multi-AZ refer here.

### What is RPO and RTO? What RPO and RTO Are Supported with a Multi-AZ Deployment?

RPO is an acronym for Recovery Point Objective and is a term to describe the data recency guarantee in the event of failures. RPO is the maximum acceptable amount of time since the last data recovery point. This determines what is considered an acceptable loss of data between the last recovery point and the interruption of service. Redshift Multi-AZ supports RPO = 0 meaning data is guaranteed to be current and up to date in the event of a failure. Our pre-launch tests found that RTO with Amazon Redshift Multi-AZ deployments is under 60 seconds or less in the unlikely case of an AZ failure.

### How Does Redshift Multi-AZ Compare to the Existing Redshift Relocation Feature?

Redshift Relocation is enabled by default on all new RA3 clusters and serverless endpoints, which allows a data warehouse to be re-started in another AZ in the event of a large-scale outage, without any data loss or additional cost. While using Relocate is free, the limitations are that it is a best-effort approach subject to resource availability in the AZ being recovered in and Recovery Time Objective (RTO) can be impacted by other issues related to starting up a new cluster. This can result in recovery times between 10 and 60 minutes. Redshift Multi-AZ supports high availability requirements by delivering an RTO measured in tens of seconds and offers guaranteed continued operation since it will not be subject to capacity limitations or other potential issues creating a new cluster.

## Querying and Analytics

Close all

### Are Amazon Redshift and Redshift Spectrum Compatible with My Preferred Business Intelligence Software Package and ETL Tools?

Yes, Amazon Redshift uses industry-standard SQL and is accessed using standard JDBC and ODBC drivers. You can download Amazon Redshift custom JDBC and ODBC drivers from the Connect Client tab of the [Redshift Console](https://console.aws.amazon.com/redshift/). We have validated integrations with popular [BI and ETL vendors](https://aws.amazon.com/redshift/partners/), a number of which are offering [free trials](https://aws.amazon.com/redshift/free-trial/) to help you get started loading and analyzing your data. You can also go to the [AWS Marketplace](https://aws.amazon.com/partners/aws-marketplace/) to deploy and configure solutions designed to work with Amazon Redshift in minutes.

Amazon Redshift Spectrum supports all Amazon Redshift client tools. The client tools can continue to connect to the Amazon Redshift cluster endpoint using ODBC or JDBC connections. No changes are required.

You use exactly the same query syntax and have the same query capabilities to access tables in Redshift Spectrum as you have for tables in the local storage of your Redshift cluster. External tables are referenced using the schema name defined in the CREATE EXTERNAL SCHEMA command where they were registered.

### What Data Formats and Compression Formats Does Amazon Redshift Spectrum Support?

Amazon Redshift Spectrum currently supports many open-source data formats, including Avro, CSV, Grok, Amazon Ion, JSON, ORC, Parquet, RCFile, RegexSerDe, Sequence, Text, and TSV.<br>Amazon Redshift Spectrum currently supports Gzip and Snappy compression.

### What Happens if a Table in My Local Storage Has the Same name as an External Table?

Just like with local tables, you can use the schema name to pick exactly which one you mean by using schema\_name.table\_name in your query.

### I Use a Hive Metastore to Store Metadata about My S3 Data Lake. Can I Use Redshift Spectrum?

Yes. The CREATE EXTERNAL SCHEMA command supports Hive Metastores. We do not currently support DDL against the Hive Metastore.

### How Do I Get a List of All External Database Tables Created in My Cluster?

You can query the system table SVV\_EXTERNAL\_TABLES to get that information.

### Does Redshift Support the Ability to Use Machine Learning with SQL?

Yes, the Amazon Redshift ML feature makes it easy for SQL users to create, train, and deploy machine learning (ML) models using familiar SQL commands. Amazon Redshift ML allows you to leverage your data in Amazon Redshift with Amazon SageMaker, a fully managed ML service. Amazon Redshift supports both unsupervised learning (K-Means) and supervised learning (Autopilot, XGBoost, MLP algorithms). You can also use AWS Language AI services to translate, redact, and analyze text fields in SQL queries with prebuilt Lambda UDF functions - [see blog post](https://aws.amazon.com/blogs/machine-learning/translate-and-analyze-text-using-sql-functions-with-amazon-redshift-amazon-translate-and-amazon-comprehend/).

### Does Amazon Redshift provide an API to Query Data?

Amazon Redshift provides a [Data API](https://docs.aws.amazon.com/redshift/latest/mgmt/data-api.html) that you can use to painlessly access data from Amazon Redshift with all types of traditional, cloud-native, and containerized, serverless web services-based and event-driven applications. The Data API simplifies access to Amazon Redshift because you don’t need to configure drivers and manage database connections. Instead, you can run SQL commands to an Amazon Redshift cluster by simply calling a secured API endpoint provided by the Data API. The Data API takes care of managing database connections and buffering data. The Data API is asynchronous, so you can retrieve your results later. Your query results are stored for 24 hours.

### What Types of Credentials Can I Use with Amazon Redshift Data API?

The Data API supports both IAM credentials and using a secret key from AWS Secrets Manager. The Data API federates AWS Identity and Access Management (IAM) credentials so you can use identity providers like Okta or Azure Active Directory or database credentials stored in Secrets Manager without passing database credentials in API calls.

### Can I Use Amazon Redshift Data API from AWS CLI?

Yes, you can use the Data API from AWS CLI using the aws redshift-data command line option.

### Is the Redshift Data API Integrated with other AWS Services?

You can use the Data API from other services such as AWS Lambda, AWS Cloud9, AWS AppSync and Amazon EventBridge.

### Do I Have to Pay Separately for Using the Amazon Redshift Data API?

No, there is no separate charge for using the Data API.

## Zero-ETL Integrations

Close all

### When Should I Use Amazon Aurora zero-ETL Integration with Amazon Redshift?

You should use [Aurora zero-ETL integration with Amazon Redshift](https://aws.amazon.com/rds/aurora/zero-etl/) when you need near real-time access to transactional data. This integration allows you to take advantage of Amazon Redshift ML with straightforward SQL commands.

### What Engines and Versions of Amazon Aurora Support zero-ETL Integrations?

Aurora zero-ETL integration with Amazon Redshift is available on the Aurora MySQL-Compatible Edition for Aurora MySQL 3.05 version (compatible with MySQL 8.0.32) and higher in the US East (Ohio), US East (N. Virginia), US West (Oregon), Asia Pacific (Singapore), Asia Pacific (Sydney), Asia Pacific (Tokyo), Europe (Frankfurt), Europe (Ireland), and Europe (Stockholm) Regions. Aurora zero-ETL integration with Amazon Redshift is available on the Aurora PostgreSQL-Compatible Edition for Aurora PostgreSQL 15.4 in the US East (Ohio) Region.

### What Benefits Does zero-ETL Integration Provide?

[Aurora zero-ETL integration with Amazon Redshift](https://aws.amazon.com/rds/aurora/zero-etl/) removes the need for you to build and maintain complex data pipelines. You can consolidate data from a single or multiple Aurora database clusters to a single Amazon Redshift database cluster and run near real-time analytics and ML using Amazon Redshift on petabytes of transactional data from Amazon Aurora.

### Is zero-ETL Integration Compatible with Amazon Redshift Serverless?

[Aurora zero-ETL integration with Amazon Redshift](https://aws.amazon.com/rds/aurora/zero-etl/) is compatible with Amazon Redshift Serverless and Amazon Aurora Serverless v2. When using both Aurora Serverless v2 and Amazon Redshift Serverless you can generate near real-time analytics on transactional data without having to manage any infrastructure for data pipelines.

### How Do I Start a zero-ETL Integration?

You can begin by using the Amazon RDS console to create the zero-ETL integration through specifying the Aurora source and Amazon Redshift destination. Once the integration has been created, the Aurora database will be replicated to Amazon Redshift, and you can start querying the data once initial seeding is completed. For more information, read the getting started guide for [Aurora zero-ETL integrations with Amazon Redshift](https://aws.amazon.com/rds/aurora/zero-etl/).

### How Does zero-ETL Integration Handle Transactions? Are They Atomically Committed when Replicated?

The Aurora to Amazon Redshift zero-ETL integration atomically replicates transactions to ensure data consistency between the source Aurora database and the target Amazon Redshift cluster.  
Here are some key points about the atomicity of transactions with this integration:

- Only committed transactions in Aurora are replicated to Amazon Redshift. Uncommitted or rolled-back transactions are not applied.
- The integration uses a two-phase commit process to atomically apply each transaction to Amazon Redshift. Either all data changes in the transaction are applied, or if an error occurs none are applied.
- Transaction consistency is maintained between the source and target. After replication, the data for a given transaction will be consistent in both Aurora and Amazon Redshift.
- Schema changes through DDL or DML are also atomically applied to maintain integrity.
- The atomic application of transactions ensures no partial transactions or inconsistent data states can occur between the databases.

### In what order Are the Changes I Make on Aurora Replicated in Amazon Redshift?

The Aurora zero-ETL integration with Amazon Redshift maintains full transactional consistency between the source Aurora database and the target Amazon Redshift cluster.

### How Are Schema Changes Handled with zero-ETL Integration?

Here are some key points on how schema changes are handled:

- DDL statements like CREATE TABLE, ALTER TABLE, DROP TABLE and so on are automatically replicated from Aurora to Amazon Redshift.
- The integration makes the necessary checks and adjustments in Amazon Redshift tables for replicated schema changes. For example, adding a column in Aurora will add the column in Amazon Redshift.
- The replication and schema sync automatically happen in real time with minimal lag between source and target databases.
- Schema consistency is maintained even as DML changes occur in parallel to DDL changes.

### How Do I Run Transformations on My Data Using zero-ETL?

You can create materialized views in your local Amazon Redshift database to transform data replicated through zero-ETL integration. Connect to your local database and use cross-database queries to access the destination databases. You can use either fully qualified object names with three-part notation (_destination-database-name.schema-name.table-nam_e) or create an external schema referencing the destination database and schema pair and use two-part notation (_external-schema-name.table-name_).

### How much Does zero-ETL Integration Cost?

Zero-ETL and ongoing processing of data changes is offered at no additional charges. You pay for existing Amazon RDS and Amazon Redshift resources used to create and process the change data generated as part of a zero-ETL integration. These resources could include:

- Additional I/O and storage used by enabling enhanced binlog
- Snapshot export costs for the initial data export to seed your Amazon Redshift databases
- Additional Amazon Redshift storage for storing replicated data
- Cross-AZ data transfer costs for moving data from source to target

For more information, visit the [Aurora pricing page](https://aws.amazon.com/rds/aurora/pricing/).

## Backup and Restore

Close all

### How Does Amazon Redshift Backup My Data? How Do I Restore My Cluster from a Backup?

Amazon Redshift RA3 clusters and Amazon Redshift Serverless use Redshift Managed Storage, which always has the latest copy of the data available. DS2 and DC2 clusters mirror the data on the cluster to ensure the latest copy is available in the event of a failure. Backups are automatically created on all Redshift cluster types and retained for 24 hours, and on serverless recovery points are provided for the past 24 hours

You can also create your own backups that can be retained indefinitely. These backups can be created at any time, and the Amazon Redshift automated backups or Amazon Redshift Serverless recovery points can be converted into a user backup for longer retention.

Amazon Redshift can also asynchronously replicate your snapshots or recovery points to Amazon S3 in another Region for disaster recovery.

On a DS2 or DC2 cluster, free backup storage is limited to the total size of storage on the nodes in the data warehouse cluster and only applies to active data warehouse clusters.

For example, if you have total data warehouse storage of 8 TB, we will provide at most 8 TB of backup storage at no additional charge. If you would like to extend your backup retention period beyond one day, you can do so using the [AWS Management Console](https://aws.amazon.com/console/) or the [Amazon Redshift APIs](https://docs.aws.amazon.com/redshift/latest/APIReference/Welcome.html). For more information on automated snapshots, please refer to the [Amazon Redshift Management Guide](https://docs.aws.amazon.com/redshift/latest/mgmt/overview.html).

Amazon Redshift only backs up data that has changed, so most snapshots use only a small amount of your free backup storage. When you need to restore a backup, you have access to all the automated backups within your backup retention window. Once you choose a backup from which to restore, we will provision a new data warehouse cluster and restore your data to it.

### How Do I Manage the Retention of My Automated Backups and Snapshots?

You can use the [AWS Management Console](https://aws.amazon.com/console/) or [ModifyCluster](https://docs.aws.amazon.com/redshift/latest/APIReference/API_ModifyCluster.html) API to manage the period of time your automated backups are retained by modifying the RetentionPeriod parameter. If you wish to turn off automated backups altogether, you can set up the retention period to 0 (not recommended).

### What Happens to My Backups if I Delete My Data Warehouse Cluster?

When you delete a data warehouse cluster, you have the ability to specify whether a final snapshot is created upon deletion. This enables a restore of the deleted data warehouse cluster at a later date. All previously created manual snapshots of your data warehouse cluster will be retained and billed at [standard Amazon S3 rates](https://aws.amazon.com/s3/pricing), unless you choose to delete them.

## Monitoring and Maintenance

Close all

### How Do I Monitor the Performance of My Amazon Redshift Data Warehouse Cluster?

Metrics for compute utilization, storage utilization, and read/write traffic to your Amazon Redshift data warehouse cluster are available free of charge through the [AWS Management Console](https://aws.amazon.com/console/) or [Amazon CloudWatch](https://aws.amazon.com/cloudwatch/) APIs. You can also add additional, user-defined metrics through Amazon CloudWatch’s custom metric functionality. The AWS Management Console provides a monitoring dashboard that helps you monitor the health and performance of all your clusters. Amazon Redshift also provides information on query and cluster performance through the AWS Management Console. This information enables you to see which users and queries are consuming the most system resources to diagnose performance issues by viewing query plans and execution statistics. In addition, you can see the resource utilization on each of your compute nodes to ensure that you have data and queries that are well-balanced across all nodes.

### What is a Maintenance Window? Will My Data Warehouse Cluster Be Available during Software Maintenance?

Amazon Redshift periodically performs maintenance to apply fixes, enhancements and new features to your cluster. You can change the scheduled maintenance windows by modifying the cluster, either programmatically or by using the [Redshift Console](https://console.aws.amazon.com/redshift/). During these maintenance windows, your Amazon Redshift cluster is not available for normal operations. For more information about maintenance windows and schedules by Region, see [Maintenance Windows](https://docs.aws.amazon.com/redshift/latest/mgmt/working-with-clusters.html#rs-maintenance-windows) in the Amazon Redshift Management Guide.

