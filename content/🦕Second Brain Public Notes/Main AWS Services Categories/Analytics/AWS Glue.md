---
tags:
  - cloud/aws
---

![[Pasted image 20240214171521.png]]  
![](https://i.imgur.com/FgtIxoV.png)

AWS Glue is <mark style="background: #BBFABBA6;">a fully-managed, pay-as-you-go, extract, transform, and load (ETL) service that automates the time-consuming steps of data preparation for analytics.</mark>

AWS Glue automatically discovers and profiles data via the Glue Data Catalog, recommends and generates ETL code to transform your source data into target schemas.

AWS Glue runs the ETL jobs on a fully managed, scale-out Apache Spark environment to load your data into its destination.

AWS Glue also allows you to setup, orchestrate, and monitor complex data flows.

You can create and run an ETL job with a few clicks in the AWS Management Console.

Simply point AWS Glue to your data stored on AWS, and AWS Glue discovers data and stores the associated metadata (e.g. table definition and schema) in the AWS Glue Data Catalog.

Once cataloged, data is immediately searchable, queryable, and available for ETL.

AWS Glue consists of a Data Catalog which is a central metadata repository, an ETL engine that can automatically generate Scala or Python code, and a flexible scheduler that handles dependency resolution, job monitoring, and retries.

Together, these automate much of the undifferentiated heavy lifting involved with discovering, categorizing, cleaning, enriching, and moving data, so you can spend more time analyzing your data.  
![[Pasted image 20240214171649.png]]  
![[Pasted image 20240214171920.png]]
## AWS Glue Crawlers

You can <mark style="background: #083CA4A6;">use a crawler to populate the AWS Glue Data Catalog with tables</mark>.  
	This is the primary method used by most AWS Glue users.

<mark style="background: #ADCCFFA6;">A crawler can crawl multiple data stores in a single run.</mark>

<mark style="background: #CACFD9A6;">Upon completion, the crawler creates or updates one or more tables in your Data Catalog. </mark>  
<mark style="background: #BBFABBA6;">Extract, transform, and load (ETL) jobs that you define in AWS Glue use these Data Catalog tables as sources and targets.</mark>

The ETL job reads from and writes to the data stores that are specified in the source and target Data Catalog tables.

AWS Glue crawlers connect to a source or target data store, progress through a prioritized list of classifiers to determine the schema for the data, and then <mark style="background: #FFF3A3A6;">creates metadata in the AWS Glue Data Catalog</mark>.

<mark style="background: #FFB86CA6;">The metadata is stored in tables in a data catalog and used in the authoring process of ETL jobs.</mark>

<mark style="background: #ADCCFFA6;">You can run crawlers on a schedule, on-demand, or trigger them based on an event to ensure that your metadata is up-to-date.</mark>

<mark style="background: #FFB86CA6;">AWS Glue automatically generates the code to extract, transform, and load data.</mark>

<mark style="background: #D2B3FFA6;">Simply point AWS Glue to a source and target, and AWS Glue creates ETL scripts to transform, flatten, and enrich the data.</mark>

The code is generated in Scala or Python and written for Apache Spark.

AWS Glue helps <mark style="background: #BBFABBA6;">clean and prepare data for analysis by providing a Machine Learning Transform</mark> called **FindMatches** for deduplication and finding matching records.

## Use Cases

<mark style="background: #FFF3A3A6;">Use AWS Glue to discover properties of data, transform it, and prepare it for analytics.</mark>

Glue can automatically discover <mark style="background: #CACFD9A6;">both structured and semi-structured data</mark> stored in data lakes on [**Amazon S3**](https://aws.amazon.com/s3/), data warehouses in [**Amazon Redshift**](https://aws.amazon.com/redshift/), and various databases running on AWS.

It provides a unified view of data via the Glue Data Catalog that is available for ETL, querying and reporting using services like [**Amazon Athena**](https://aws.amazon.com/athena/), [**Amazon EMR**](https://aws.amazon.com/emr/), and [**Amazon Redshift Spectrum**](https://aws.amazon.com/redshift/).

Glue automatically generates Scala or Python code for ETL jobs that you can further customize using tools you are already familiar with.

AWS Glue is serverless, so there are no compute resources to configure and manage.

# FAQ
## General

**Q: What is AWS Glue?**

AWS Glue is a serverless data integration service that makes it easier to discover, prepare, and combine data for analytics, machine learning (ML), and application development. AWS Glue provides all the capabilities needed for data integration, so you can start analyzing your data and putting it to use in minutes instead of months. AWS Glue provides both visual and code-based interfaces to make data integration easier. Users can more easily find and access data using the AWS Glue Data Catalog. Data engineers and ETL (extract, transform, and load) developers can visually create, run, and monitor ETL workflows in a few steps in AWS Glue Studio. Data analysts and data scientists can use AWS Glue DataBrew to visually enrich, clean, and normalize data without writing code.  

**Q: How do I get started with AWS Glue?**

To start using AWS Glue, sign in to the AWS Management Console and navigate to Glue under the Analytics category. You can follow one of our guided tutorials that will walk you through an example use case for AWS Glue. You can also find sample ETL code in our [GitHub repository](https://github.com/awslabs/aws-glue-samples) under AWS Labs.

**Q. What are the main components of AWS Glue?**

AWS Glue consists of a Data Catalog, which is a central metadata repository; an ETL engine that can automatically generate Scala or Python code; a flexible scheduler that handles dependency resolution, job monitoring, and retries; and AWS Glue DataBrew for cleaning and normalizing data with a visual interface. Together, these features automate much of the undifferentiated heavy lifting involved with discovering, categorizing, cleaning, enriching, and moving data, so you can spend more time analyzing your data.  

**Q: When should I use AWS Glue?**

Use AWS Glue to discover properties of the data you own, transform it, and prepare it for analytics. AWS Glue can automatically discover both structured and semi-structured data stored in your data lake on [Amazon Simple Storage Service (Amazon S3)](https://aws.amazon.com/s3/), data warehouse in [Amazon Redshift](https://aws.amazon.com/redshift/), and various databases running on AWS. It provides a unified view of your data via the Data Catalog that is available for ETL, querying and reporting using services like [Amazon Athena](https://aws.amazon.com/athena/), [Amazon EMR](https://aws.amazon.com/emr/), and [Amazon Redshift Spectrum](https://aws.amazon.com/redshift/). AWS Glue automatically generates Scala or Python code for your ETL jobs that you can further customize using tools that you are already familiar with. You can use DataBrew to visually clean up and normalize data without writing code.

**Q: What data sources does AWS Glue support?**

AWS Glue can integrate with more than 80 data sources on AWS, on premises, and on other clouds. The service natively supports data stored in the following databases in your Amazon Virtual Private Cloud (Amazon VPC) running on Amazon Elastic Compute Cloud (Amazon EC2):

- [Amazon Aurora](https://aws.amazon.com/rds/aurora/)
- [Amazon RDS for MySQL](https://aws.amazon.com/rds/mysql/)
- [Amazon RDS for Oracle](https://aws.amazon.com/rds/oracle/)
- [Amazon RDS for PostgreSQL](https://aws.amazon.com/rds/postgresql/)
- [Amazon RDS for SQL Server](https://aws.amazon.com/rds/sqlserver/)
- [Amazon Redshift](https://aws.amazon.com/redshift/)
- [Amazon DynamoDB](https://aws.amazon.com/dynamodb/)
- [Amazon S3](https://aws.amazon.com/s3/)
- MySQL, Oracle, Microsoft SQL Server, and PostgreSQL

AWS Glue also supports data streams from Amazon Managed Streaming for Apache Kafka (Amazon MSK), Amazon Kinesis Data Streams, and Apache Kafka. You can add connectors, including Snowflake, GCP BigQuery, and Teradata, from the AWS Marketplace.  

You can also write custom Scala or Python code and import custom libraries and Jar files into your AWS Glue ETL jobs to access data sources not natively supported by AWS Glue. For more details on importing custom libraries, refer to our [documentation](https://docs.aws.amazon.com/glue/index.html).

**Q: How does AWS Glue relate to AWS Lake Formation?**

Lake Formation uses a shared infrastructure with AWS Glue, including console controls, ETL code creation and job monitoring, a common Data Catalog, and serverless architecture. While AWS Glue is still focused on these types of functions, Lake Formation encompasses AWS Glue features _and_ provides additional capabilities designed to help build, secure, and manage a data lake. See the [AWS Lake Formation pages](https://aws.amazon.com/lake-formation/) for more details.  

## AWS Glue Data Catalog
![[Pasted image 20240214171757.png]]  
**Q: What is the AWS Glue Data Catalog?**

The **Data Catalog** is <mark style="background: #FFB86CA6;">a central repository to store structural and operational metadata for all your data assets</mark>. For a given dataset, you can store its table definition and physical location, add business-relevant attributes, and track how this data has changed over time.

The Data Catalog is Apache Hive Metastore compatible and is a drop-in replacement for the Apache Hive Metastore for Big Data applications running on Amazon EMR. For more information about setting up your Amazon EMR cluster to use the Data Catalog as an Apache Hive Metastore, read the [AWS Glue Documentation](https://docs.aws.amazon.com/glue/index.html).

The Data Catalog also provides built-in integration with [Amazon Athena](https://aws.amazon.com/athena/), [Amazon EMR](https://aws.amazon.com/emr/), and [Amazon Redshift Spectrum](https://aws.amazon.com/redshift/). Once you add your table definitions to the Data Catalog, they are available for ETL and also readily available for querying in Amazon Athena, Amazon EMR, and Amazon Redshift Spectrum so that you can have a common view of your data between these services.

**Q: How do I get my metadata into the Data Catalog?**

AWS Glue provides numerous ways to populate metadata into the Data Catalog. AWS Glue crawlers scan various data stores that you own to automatically infer schemas, partition structure, and populate the Data Catalog with corresponding table definitions and statistics. You can also schedule crawlers to run periodically so that your metadata is always up to date and i -sync with the underlying data. Alternately, you can add and update table details manually by using the AWS Glue console or by calling the API. You can also run Hive DDL statements through the [Amazon Athena](https://aws.amazon.com/athena/) console or a Hive client on an [Amazon EMR](https://aws.amazon.com/emr/) cluster. Finally, if you already have a persistent Apache Hive Metastore, you can perform a bulk import of that metadata into the Data Catalog by using our import script.

**Q: What are AWS Glue crawlers?**

An AWS Glue crawler connects to a data store, progresses through a prioritized list of classifiers to extract the schema of your data and other statistics, and then populates the Data Catalog with this metadata. Crawlers can run periodically to detect the availability of new data as well as changes to existing data, including table definition changes. Crawlers automatically add new tables, new partitions to existing table, and new versions of table definitions. You can customize AWS Glue crawlers to classify your own file types.

**Q: How do I import data from my existing Apache Hive Metastore to the Data Catalog?**

You can run an ETL job that reads from your Hive Metastore, exports the data to an intermediate format in [Amazon S3](https://aws.amazon.com/s3/), and then imports that data into the Data Catalog.

**Q: Do I need to maintain my Hive Metastore if I am storing my metadata in the Data Catalog?**

No. The Data Catalog is Hive Metastore compatible. You can point to the Data Catalog endpoint and use it as a Hive Metastore replacement. For more information about how to configure your cluster to use the Data Catalog as a Hive Metastore, read the [AWS Glue Documentation](https://docs.aws.amazon.com/glue/index.html).

**Q: If I am already using Amazon Athena or Amazon Redshift Spectrum and have tables in the Amazon Athena internal data catalog, how can I start using the AWS Glue Data Catalog as my common metadata repository?**

Before you can start using the AWS Glue Data Catalog as a common metadata repository between [Amazon Athena](https://aws.amazon.com/athena/), [Amazon Redshift Spectrum](https://aws.amazon.com/redshift/), and AWS Glue, you must upgrade your Amazon Athena data catalog to the AWS Glue Data Catalog. For steps required for the upgrade, read the [Amazon Athena User Guide](http://docs.aws.amazon.com/athena/latest/ug/glue-athena.html).

## AWS Glue Schema Registry

**Q: What is the AWS Glue Schema Registry?**

You can use the [Schema Registry](https://docs.aws.amazon.com/glue/latest/dg/schema-registry.html), a serverless feature of AWS Glue, to validate and control the evolution of streaming data using schemas registered in Apache Avro and JSON Schema data formats, at no additional charge. Through Apache-licensed serializers and deserializers, the Schema Registry integrates with Java applications developed for Apache Kafka, [Amazon MSK](https://aws.amazon.com/msk/), [Amazon Kinesis Data Streams](https://aws.amazon.com/kinesis/data-streams/), Apache Flink, [Amazon Kinesis Data Analytics for Apache Flink](https://aws.amazon.com/kinesis/data-analytics/), and [AWS Lambda](https://aws.amazon.com/lambda/). When data streaming applications are integrated with the Schema Registry, you can improve data quality and safeguard against unexpected changes using compatibility checks that govern schema evolution. Additionally, you can create or update AWS Glue tables and partitions using Apache Avro schemas stored within the registry.

**Q: Why should I use the Schema Registry?**  

With the Schema Registry, you can do the following:

1. **Validate schemas**. When data streaming applications are integrated with the Schema Registry, schemas used for data production are validated against schemas within a central registry, allowing you to centrally control data quality.
2. **Safeguard schema evolution**. You can set rules on how schemas can and cannot evolve using one of eight compatibility modes.
3. **Improve data quality**. Serializers validate schemas used by data producers against those stored in the registry, improving data quality when it originates and reducing downstream issues from unexpected schema drift.
4. **Save costs**. Serializers convert data into a binary format and can compress it before it is delivered, reducing data transfer and storage costs.
5. **Improve processing efficiency**. In many cases, a data stream contains records of different schemas. The Schema Registry enables applications that read from data streams to selectively process each record based on the schema without having to parse its contents, which increases processing efficiency.  
    

**Q: Which data format, client language, and integrations are supported by the Schema Registry?**

The Schema Registry supports Apache Avro and JSON Schema data formats and Java client applications. There are plans to continue expanding support for other data formats and non-Java clients. The Schema Registry integrates with applications developed for Apache Kafka, [Amazon MSK](https://aws.amazon.com/msk/), [Amazon Kinesis Data Streams](https://aws.amazon.com/kinesis/data-streams/), Apache Flink, [Amazon Kinesis Data Analytics for Apache Flink](https://aws.amazon.com/kinesis/data-analytics/), and [AWS Lambda](https://aws.amazon.com/lambda/).

**Q: Which kinds of evolution rules does the Schema Registry support?**

The following compatibility modes are available for you to manage your schema evolution: Backward, Backward All, Forward, Forward All, Full, Full All, None, and Disabled. Visit the [AWS Glue Schema Registry user documentation](https://docs.aws.amazon.com/glue/latest/dg/schema-registry.html) to learn more about compatibility rules.

**Q: How does the Schema Registry maintain high availability for my applications?**

The Schema Registry storage and control plane is designed for high availability and is backed by the [AWS Glue Service Level Agreement](https://aws.amazon.com/glue/sla/). The serializers and deserializers use best-practice caching techniques to maximize schema availability within clients.

**Q: Is the Schema Registry open source?**

Schema Registry storage is an AWS service, while the serializers and deserializers are Apache-licensed open-source components.

**Q: Does the Schema Registry provide encryption at rest and in transit?**

Yes. Your clients communicate with the Schema Registry through API calls, which encrypt data in transit using TLS encryption over HTTPS. Schemas stored in the Schema Registry are always encrypted at rest using a service-managed KMS key.

**Q: How can I privately connect to the Schema Registry?**

You can use AWS PrivateLink to connect your data producer’s virtual private cloud (VPC) to AWS Glue by defining an interface VPC endpoint for AWS Glue. When you use a VPC interface endpoint, communication between your VPC and AWS Glue is conducted entirely within the AWS network. For more information, please read the [AWS Glue Developer Guide](https://docs.aws.amazon.com/glue/latest/dg/what-is-glue.html). 

**Q: How can I monitor my Schema Registry usage?**

AWS CloudWatch metrics are available as part of the CloudWatch free tier. You can access these metrics in the CloudWatch console. Visit the [AWS Glue Schema Registry user documentation](https://docs.aws.amazon.com/glue/latest/dg/schema-registry.html) for more information.

**Q: Does the Schema Registry provide tools to manage user authorization?**

Yes. The Schema Registry supports both resource-level permissions and identity-based IAM policies.

**Q: How do I migrate from an existing schema registry to the  Schema Registry?**

Steps to migrate from a third-party schema registry to the Schema Registry are available in the [AWS Glue Schema Registry user documentation](https://docs.aws.amazon.com/glue/latest/dg/schema-registry.html).  

## Extract, Transform, and Load (ETL)

**Q: Does AWS Glue have a no-code interface for visual ETL?**

Yes. AWS Glue Studio offers a graphical interface for authoring AWS Glue jobs to process your data. After you define the flow of your data sources, transformations and targets in the visual interface, AWS Glue Studio will generate Apache Spark code on your behalf.  

**Q: What programming language can I use to write my ETL code for AWS Glue?**

You can use either Scala or Python.

**Q: How can I customize the ETL code generated by AWS Glue?**

The AWS Glue ETL script recommendation system generates Scala or Python code. It uses the AWS Glue custom ETL library to simplify access to data sources and manage job execution. You can find more details about the library in the [AWS Glue Documentation](https://docs.aws.amazon.com/glue/index.html). You can write ETL code using the AWS Glue custom library. You can also write arbitrary code in Scala or Python using inline editing through the AWS Glue console script editor, downloading the auto-generated code, and editing it in your own integrated development environment (IDE). You can also start with one of the many samples hosted in our [GitHub repository](https://github.com/awslabs/aws-glue-samples) and customize that code.

**Q: Can I import custom libraries as part of my ETL script?**

Yes. You can import custom Python libraries and Jar files into your AWS Glue ETL job. For more details, read the [AWS Glue Documentation](https://docs.aws.amazon.com/glue/index.html).

**Q: Can I bring my own code?**

Yes. You can write your own code using the AWS Glue ETL library. You can also write your own Scala or Python code and upload it to an AWS Glue ETL job. For more details, read the [AWS Glue Documentation](https://docs.aws.amazon.com/glue/index.html).

**Q: How can I develop my ETL code using my own IDE?**

You can create and connect to development endpoints that offer ways to connect your notebooks and IDEs.

**Q: How can I build a complete ETL workflow using multiple jobs in AWS Glue?**

In addition to the ETL library and code generation, AWS Glue provides a robust set of orchestration features that helps you manage dependencies between multiple jobs to build complete ETL workflows. AWS Glue ETL jobs can either be triggered on a schedule or on a job completion event. Multiple jobs can be triggered in parallel or sequentially by triggering them on a job completion event. You can also trigger one or more AWS Glue jobs from an external source such as an [AWS Lambda](https://aws.amazon.com/lambda/) function.

**Q: How does AWS Glue monitor dependencies?**

AWS Glue manages dependencies between two or more jobs or dependencies on external events using triggers. Triggers can watch one or more jobs as well as invoke one or more jobs. You can either have a scheduled trigger that invokes jobs periodically, an on-demand trigger, or a job completion trigger.

**Q: How does AWS Glue handle ETL errors?**

AWS Glue monitors job event metrics and errors, and pushes all notifications to [Amazon CloudWatch](https://aws.amazon.com/cloudwatch/). With CloudWatch, you can configure a host of actions that can be triggered based on specific notifications from AWS Glue. For example, if you get an error or a success notification from AWS Glue, you can trigger an [AWS Lambda](https://aws.amazon.com/lambda/) function. AWS Glue also provides default retry behavior that will retry all failures three times before sending an error notification.

**Q: Can I run my existing ETL jobs with AWS Glue?**

Yes. You can run your existing Scala or Python code on AWS Glue. Simply upload the code to [Amazon S3](https://aws.amazon.com/s3/) and create one or more jobs that use that code. You can reuse the same code across multiple jobs by pointing them to the same code location on Amazon S3.

**Q: How can I use AWS Glue to support ETL streaming data?**

AWS Glue supports ETL on streams from Amazon Kinesis Data Streams, Apache Kafka, and Amazon MSK. Add the stream to the Data Catalog, and then choose it as the data source when setting up your AWS Glue job.  

**Q: Do I have to use both the Data Catalog and AWS Glue ETL to use the service?**

No. While we do believe that using both the Data Catalog and ETL provides a complete ETL experience, you can use either one of them independently without using the other.

**Q: When should I use AWS Glue Streaming and when should I use Amazon Kinesis Data Analytics?**

Both AWS Glue and Kinesis Data Analytics can be used to process streaming data. AWS Glue is recommended when your use cases are primarily ETL and you want to run jobs on a serverless Apache Spark-based platform. Kinesis Data Analytics is recommended when your use cases are primarily analytics and you want to run jobs on a serverless Apache Flink-based platform.

Streaming ETL in AWS Glue enables advanced ETL on streaming data using the same serverless pay-as-you-go platform that you currently use for your batch jobs. AWS Glue generates customizable ETL code to prepare your data while in transit and has built-in functionality to process streaming data that is semi-structured or has an evolving schema. Use AWS Glue to apply both its built-in and Spark-native transforms to data streams and load them into your data lake or data warehouse.

Use Kinesis Data Analytics to build sophisticated streaming applications to analyze streaming data in real time. It provides a serverless Apache Flink runtime that automatically scales without servers and durably saves application state. Use Kinesis Data Analytics for real-time analytics and more general stream data processing.

**Q: When should I use AWS Glue and when should I use Amazon Kinesis Data Firehose?**

Both AWS Glue and Kinesis Data Firehose can be used for streaming ETL. AWS Glue is recommended for complex ETL, including joining streams, and partitioning the output in Amazon S3 based on the data content. Kinesis Data Firehose is recommended when your use cases focus on data delivery and preparing data to be processed after it is delivered.

Streaming ETL in AWS Glue enables advanced ETL on streaming data using the same serverless pay-as-you-go platform that you currently use for your batch jobs. AWS Glue generates customizable ETL code to prepare your data while in transit and has built-in functionality to process streaming data that is semi-structured or has an evolving schema. Use AWS Glue to apply complex transforms to data streams, enrich records with information from other streams and persistent data stores, and then load records into your data lake or data warehouse.

Stream ETL in Kinesis Data Firehose to more easily capture, transform, and deliver streaming data. Kinesis Data Firehose provides ETL capabilities including serverless data transformation through AWS Lambda and format conversion from JSON to Parquet. It includes ETL capabilities that are designed to make data easier to process after delivery, but it does not include the advanced ETL capabilities that AWS Glue supports.  

## Deduplicate Data

**Q: What kind of problems does the AWS Glue FindMatches ML transform solve?**  

FindMatches generally solves record linkage and data deduplication problems. You must deduplicate when you are trying to identify records in a database that are conceptually “the same” but for which you have separate records. This problem is trivial if duplicate records can be identified by a unique key (for instance, if products can be uniquely identified by a UPC Code), but it becomes challenging when you have to do a “fuzzy match.”

Record linkage is a similar problem as data deduplication, but this term usually means that you are doing a “fuzzy join” of two databases that do not share a unique key rather than deduplicating a single database. As an example, consider the problem of matching a large database of customers to a small database of known fraudsters. FindMatches can be used on both record linkage and deduplication problems.

For instance, the FindMatches ML transform can help you with the following problems:

- Linking patient records between hospitals so that doctors have more background information and are better able to treat patients by using FindMatches on separate databases that both contain common fields like name, birthday, home address, phone number, and so on.
- Deduplicating a database of movies containing columns like “title,” “plot synopsis,” “year of release,” “run time,” and “cast.” For instance, the same movie might be variously identified as “Star Wars,” “Star Wars: A New Hope,” and “Star Wars: Episode IV—A New Hope (Special Edition).”
- Automatically group all related products together in your storefront by identifying equivalent items in an apparel product catalog where you want to define “equivalent” to mean that they are the same, ignoring differences in size and color. Hence “Levi 501 Blue Jeans, size 34x34” is defined to be the same as “Levi 501 Jeans—black, Size 32x31.”  
    

**Q: How does AWS Glue deduplicate my data?**  

The FindMatches ML transform makes it easier to find and link records that refer to the same entity but don’t share a reliable identifier. Before FindMatches, developers would commonly solve data-matching problems deterministically, by writing huge numbers of hand-tuned rules. FindMatches uses ML algorithms behind the scenes to learn how to match records according to each developer's own business criteria. FindMatches first identifies records for the customer to label as to whether they match or do not match and then uses ML to create an ML transform. Customers can then execute this transform on their database to find matching records. Or, they can ask FindMatches to give them additional records to label to push their ML transform to higher levels of accuracy.  

**Q: What are ML transforms?**

ML transforms provide a destination for creating and managing machine-learned transforms. Once created and trained, these ML transforms can then be executed in standard AWS Glue scripts. Customers select a particular algorithm (for example, the FindMatches ML transform) and input datasets, training examples, and the tuning parameters needed by that algorithm. AWS Glue uses those inputs to build an ML transform that can be incorporated into a normal ETL Job workflow.  

**Q: How do ML transforms work?**

AWS Glue includes specialized ML-based dataset transformation algorithms that customers can use to create their own ML transforms. These include record deduplication and match finding.

Customers start by navigating to the ML Transforms tab in the console (or using the ML transforms service endpoints or accessing ML transforms training through CLI) to create their first ML transform model. The ML Transforms tab provides a user-friendly view for management of user transforms. ML transforms require distinct workflow requirements from other transforms, including the need for separate training, parameter tuning, and execution workflows; the need for estimating the quality metrics of generated transformations; and the need to manage and collect additional truth labels for training and active learning.

To create an ML transform through the console, customers first select the transform type (such as Record Deduplication or Record Matching) and provide the appropriate data sources previously discovered in the Data Catalog. Depending on the transform, customers may then be asked to provide ground truth label data for training or additional parameters. Customers can monitor the status of their training jobs and view quality metrics for each transform. (Quality metrics are reported using a hold-out set of the customer-provided label data.)

Once satisfied with the performance, customers can promote ML transform models for use in production. ML transforms can then be used during ETL workflows, both in code autogenerated by the service and in user-defined scripts submitted with other jobs, similar to pre-built transforms offered in other AWS Glue libraries.  

## AWS Glue Data Quality

**Q: What is AWS Glue Data Quality?**

AWS Glue Data Quality is a feature of AWS Glue that reduces manual data quality effort by automatically measuring and monitoring the quality of data in data lakes and pipelines. In data lakes, it then automatically recommends data quality rules. You can modify these rules, add additional rules from built-in rule types, and configure actions to alert teams when quality issues occur. Rules can also be included in AWS Glue data pipelines and scheduled to run periodically. This feature then measures data quality by evaluating these rules and calculates data quality scores. You can view these data quality scores in the Data Catalog. Data quality issues can be remediated by modifying data pipelines and tracking quality score improvements using AWS Glue Data Quality.

**Q:** **What is data quality and why is it important?**

Data quality is the measure of how well suited a dataset is to serve its specific purpose, such as analytics to improve operations, business decision making, and planning. Hundreds of thousands of customers use data lakes on AWS, but customers struggle to use their data assets effectively due to poor data quality.

**Q: Why should I use AWS** **Glue Data Quality?**

AWS Glue Data Quality reduces the manual effort and time that it takes to set up data quality checks in your data lakes and pipelines. It automates the process of analyzing data to determine the appropriate data quality rules, and then it applies those checks on a schedule that you choose. It also provides built-in options for monitoring and alerting.

**Q: What rules does AWS** **Glue Data Quality support?**

AWS Glue Data Quality currently supports 18 built-in rule types under four categories:

1. **Consistency** **rules** check if data across different columns agrees by looking at column correlations.
2. **Accuracy rules** check if record counts meet a set threshold and if columns are not empty, match certain patterns, have valid data types, and have valid values.
3. **Integrity rules** check if duplicates exist in a dataset.
4. **Completeness** **rules** check if data in your datasets do not have missing values.

These rule types are high-level groupings of data quality rules that address several use cases. For any missing requirements, you can author custom rules using SQL.

**Q: How can I get started with AWS Glue Data Quality?**

To get started, go to Data Quality in the Data Catalog and select a table. Then choose the Data Quality tab to get started. Alternatively, you can set up data quality rules within your pipelines by adding a Data Quality transform on AWS Glue Studio. You can also use APIs to set up data quality rules and run them.

**Q: How does AWS Glue Data Quality generate recommendations?**

AWS Glue Data Quality uses Deequ, an Amazon developed open-source framework that many Amazon teams use to manage the quality of Amazon internal datasets at petabyte scale. One Amazon team uses Deequ to check dataset quality in their 60 PB data lake. Deequ uses Apache Spark to gather data statistics, such as averages, correlations, patterns, and other advanced statistics. It then uses these statistics to identify the right set of checks or rules to validate data quality.

**Q: How can I edit the recommended rules or add new rules?**

You can view and edit recommended rules in the Data Catalog. If you are using other AWS services, you can programmatically access your recommendations using the AWS Glue Data Quality API. You can also add new rules in the Data Catalog.

**Q: How does AWS Glue Data Quality verify that my rules are relevant when data changes?**

You can schedule the recommendation process to get new recommendations based on recent data. AWS Glue Data Quality will provide new recommendations based on recent data patterns.

**Q: What built-in actions are available on AWS Glue Data Quality?**

You can use actions to respond to a data quality issue. In the Data Catalog, you can write the metrics to Amazon CloudWatch and set up alerts in CloudWatch to notify you when scores go below a threshold. On AWS Glue Studio, you can fail a job when quality deteriorates, preventing bad data from moving into data lakes. 

**Q: How can I evaluate my data’s quality?**

After you create data quality rules in the Data Catalog, you can create a data quality task and run it immediately or schedule it to run at certain intervals. Data quality rules on your pipelines evaluate your data quality as data is brought into your data lake through your pipelines.

**Q: Where can I view AWS Glue Data Quality scores?**

You can make confident data-driven decisions using data quality scores. You can view data quality scores on the Data Quality tab of your table from the Data Catalog. You can view your data pipeline scores on AWS Glue Studio by opening an AWS Glue Studio job and choosing Data Quality. You can configure your data quality tasks to write results to an Amazon S3 bucket. You can then query this data using Amazon Athena or Amazon QuickSight.

**Q: What is the difference between data quality rules on DataBrew, the Data Catalog, and AWS Glue Studio?**

Business analysts and data analysts use DataBrew to transform data without writing any code. Data stewards and data engineers use the Data Catalog to manage metadata. Data engineers use AWS Glue Studio to author scalable data integration pipelines. These user types must manage data quality in their workflows. Also, data engineers need more technical data quality rules compared to business analysts who write functional rules. Therefore, data quality features are made available in each of these experiences to meet unique user requirements.

## AWS Glue DataBrew

**Q: What is AWS Glue DataBrew?**

DataBrew is a visual data preparation tool that makes it easy for data analysts and data scientists to prepare data with an interactive, point-and-click visual interface without writing code. With Glue DataBrew, you can easily visualize, clean, and normalize terabytes, and even petabytes of data directly from your data lake, data warehouses, and databases, including Amazon S3, Amazon Redshift, Amazon Aurora, and Amazon RDS. 

**Q: Who can use DataBrew?**

DataBrew is built for users who need to clean and normalize data for analytics and ML. Data analysts and data scientists are the primary users. For data analysts, examples of job functions are business intelligence analysts, operations analysts, market intelligence analysts, legal analysts, financial analysts, economists, quants, or accountants. For data scientists, examples of job functions are materials scientists, bioanalytical scientists, and scientific researchers.

**Q: What types of transformations are supported in DataBrew?**

You can choose from over 250 built-in transformations to combine, pivot, and transpose data without writing code. DataBrew also automatically recommends transformations such as filtering anomalies; correcting invalid, incorrectly classified, or duplicate data; normalizing data to standard date and time values; or generating aggregates for analyses. For complex transformations, such as converting words to a common base or root word, DataBrew provides transformations that use advanced ML techniques such as natural language processing (NLP). You can group multiple transformations together, save them as recipes, and apply the recipes directly to the new incoming data.

**Q: Which file formats does DataBrew support?**

For input data, DataBrew supports commonly used file formats, such as comma-separated values (.csv), JSON and nested JSON, Apache Parquet and nested Apache Parquet, and Excel sheets. For output data, DataBrew supports comma-separated values (.csv), JSON, Apache Parquet, Apache Avro, Apache ORC, and XML.

**Q: Do I need to use the Data Catalog or Lake Formation to use DataBrew?**

No. You can use DataBrew without using either the Data Catalog or Lake Formation. However, if you use either the Data Catalog or Lake Formation, DataBrew users can select the datasets available to them from their centralized data catalog.  

**Q: Can I retain a record of all changes made to my data?**

Yes. You can visually track all the changes made to your data in the [AWS Glue DataBrew console](https://console.aws.amazon.com/databrew/home). The visual view makes it easier to trace the changes and relationships made to the datasets, projects and recipes, and all other associated jobs. In addition, DataBrew keeps all account activities as logs in AWS CloudTrail.

## AWS Glue Flex Jobs

**Q: What is AWS Glue Flex?**

AWS Glue Flex is a flexible execution job class that allows you to reduce the cost of your nonurgent data integration workloads (for example, preproduction jobs, testing, and data loads) by up to 35%. AWS Glue has two job execution classes: standard and flexible. The standard execution class is ideal for time-sensitive workloads that require fast job startup and dedicated resources. The flexible execution class is appropriate for nonurgent jobs whose start and completion times may vary. AWS Glue Flex can reduce the cost of your non-time-sensitive workloads (for example, nightly batch ETL jobs, weekend jobs, and one-time bulk data ingestion jobs).

**Q: How do the AWS Glue standard and flexible execution classes differ?**

The AWS Glue standard and flexible execution classes have different execution properties. With the standard execution class, jobs start immediately and have dedicated resources while running. Flexible execution class jobs run on non-dedicated compute resources on AWS that can be reclaimed while a job is running, and their start and completion times vary. As a result, the two execution classes are appropriate for different workloads. The standard execution class is ideal for time-sensitive workloads that require fast job startup and dedicated resources. The flexible execution class is less expensive and suitable for nonurgent jobs where variance in start and completion times is acceptable.

**Q: How do I get started with AWS Glue Flex flexible execution class jobs?**

The flexible execution class is available for AWS Glue Spark jobs. To use the flexible execution class, you change the default setting of the execution class parameter from STANDARD to FLEX. You can do this through AWS Glue Studio or a command line interface (CLI). Read the [AWS Glue Documentation](https://docs.aws.amazon.com/glue/index.html) for more information.

**Q: What types of data integration and ETL workloads are not appropriate for AWS Glue Flex flexible execution class?**

AWS Glue Flex flexible execution class is not appropriate for time-sensitive workloads that require consistent job start and run times, or for jobs that must complete execution by a specific time. AWS Glue Flex is also not recommended for long-running data integration workloads because they are more likely to get interrupted, resulting in frequent cancellations.

**Q: How often should I expect jobs running with AWS Glue Flex flexible execution class to be interrupted?**

The availability and interruption frequency of AWS Glue Flex depends on several factors, including the AWS Region and Availability Zone, time of day, and day of week. Resource availability determines whether AWS Glue Flex jobs will start at all. While the interruption rate can be between 5% and 10% during peak hours, we expect the interruption rate of AWS Glue Flex jobs to be about 5% or the failure rate due to interruption to be less than 5%.

**Q: Is the flexible execution class always available?**

Yes. You can always choose the flexible execution class to run your AWS Glue jobs. However, the ability of AWS Glue to execute these jobs is based on the availability of non-dedicated AWS capacity and the number of workers selected for your job. It is possible that, during peak times, AWS Glue may not have adequate capacity for your job. In that case, your job will not start. You can specify a timeout value after which AWS Glue will cancel the job. The longer the timeout value, the greater the chance that your job will be executed.  

**Q: What happens if an AWS Glue Flex job is interrupted during execution?**

If an AWS Glue Flex job is interrupted because there are no longer sufficient workers to complete the job based on the number of workers specified, the job will fail. AWS Glue will retry failed jobs up to the specified maximum number of [retries on the job definition](https://docs.aws.amazon.com/glue/latest/dg/aws-glue-api-jobs-job.html#aws-glue-api-jobs-job-Job) before canceling the job. You should not use the flexible execution class for any job that has a downstream dependency on other systems or processes.

**Q: What types of AWS Glue jobs are supported by the flexible execution class?**

The flexible execution class supports only AWS Glue Spark jobs. Python Shell and streaming are not supported. AWS Glue Flex is supported by AWS Glue version 3.0 and later. The flexible execution class does not currently support streaming workloads.

## AWS Glue for Ray

**Q: What is AWS Glue for Ray?**

AWS Glue for Ray is an engine option that data engineers can use to process large datasets using Python and popular Python libraries. AWS Glue for Ray combines the AWS Glue serverless data integration service with Ray ([ray.io](http://ray.io/)), a popular new open-source framework that helps scale Python workloads. You pay only for the resources that you use while running code and don’t need to configure or tune any resources.  

**Q: Why should I use AWS Glue for Ray?**

With AWS Glue for Ray, you use the same data processing tools that you currently use (for example, Python libraries for data cleansing, computation, and ML) on large datasets. You don’t need to switch to other big data frameworks or rewrite your code to work on large datasets. AWS Glue for Ray helps you run distributed Python scripts over multi-node clusters. It also simplifies the process of orchestrating large numbers of tasks that must be run in parallel.  

**Q. What is Ray?**

Ray ([ray.io](https://www.ray.io/)) is an open-source distributed compute framework that scales Python applications from a laptop to a cluster consisting of hundreds of compute nodes. It provides simplified primitive types for building and running distributed applications. You can parallelize single-machine code with a few additional lines of code. You can also build complex applications using a straightforward programming model (Ray Core) and a collection of high-level libraries and tools.

**Q: How do I start using AWS Glue for Ray?**

You can create and run Ray jobs by using the existing AWS Glue jobs, CLIs, and APIs, and selecting the Ray engine through notebooks (Amazon SageMaker or a local notebook) or by using AWS Glue Studio. When a Ray job is ready, you can run it manually or on a schedule.  

**Q: What infrastructure do I need to manage to support AWS Glue for Ray users?**

AWS Glue for Ray is fully serverless, so there is no infrastructure to manage. However, administrators can manage how much infrastructure is provisioned for users by setting defaults and limits for the size of AWS Glue for Ray clusters on a per-account, per-user, and per-role basis. They can also set usage limits that will automatically initiate alerts and stop code from running when usage thresholds are exceeded.

## AWS Product Integrations

**Q: When should I use AWS Glue versus AWS Data Pipeline?**

<mark style="background: #BBFABBA6;">AWS Glue provides a managed ETL service that runs on a serverless Apache Spark environment</mark>. <mark style="background: #ADCCFFA6;">This allows you to focus on your ETL job and not worry about configuring and managing the underlying compute resources</mark>. AWS Glue takes a data-first approach and allows you to focus on the data properties and data manipulation to transform the data to a form where you can derive business insights.  
It provides an integrated Data Catalog that makes metadata available for ETL as well as querying through [Amazon Athena](https://aws.amazon.com/athena/) and [Amazon Redshift Spectrum](https://aws.amazon.com/redshift/).

[Data Pipeline](https://aws.amazon.com/datapipeline/) <mark style="background: #CACFD9A6;">provides a managed orchestration service that gives you greater flexibility in terms of the execution environment, access and control over the compute resources that run your code, and the code itself that does data processing</mark>. <mark style="background: #FFF3A3A6;">Data Pipeline launches compute resources in your account, giving you direct access to the Amazon EC2 instances</mark> or [Amazon EMR](https://aws.amazon.com/emr/) clusters.

Furthermore, <mark style="background: #CACFD9A6;">AWS Glue ETL jobs are Scala or Python based</mark>. If your use case requires you to use an engine other than Apache Spark or if you want to run a heterogeneous set of jobs that run on various engines like Hive and Pig, then Data Pipeline would be a better choice.

**Q: When should I use AWS Glue versus Amazon EMR?**

AWS Glue works on top of the Apache Spark environment to provide a scale-out execution environment for your data transformation jobs. AWS Glue infers, evolves, and monitors your ETL jobs to greatly simplify the process of creating and maintaining jobs.

[Amazon EMR](https://aws.amazon.com/emr/) provides you with direct access to your Hadoop environment, affording you lower-level access and greater flexibility in using tools beyond Spark.

**Q: When should I use AWS Glue versus AWS Database Migration Service (AWS DMS)?**

[AWS DMS](https://aws.amazon.com/dms/) helps you migrate databases to AWS more easily and securely. AWS DMS is recommended for use cases that require a database migration from on premises to AWS or database replication between on-premises sources and sources on AWS. Once your data is on AWS, you can use AWS Glue to move, combine, replicate, and transform data from your data source into another database or data warehouse, such as [Amazon Redshift](https://aws.amazon.com/redshift/).

**Q: When should I use AWS Glue versus AWS Batch?**

Use [AWS Batch](https://aws.amazon.com/batch/) to  efficiently run any batch computing job on AWS, regardless of the nature of the job. AWS Batch creates and manages the compute resources in your AWS account, giving you full control and visibility into the resources being used.

AWS Glue is a fully managed ETL service that provides a serverless Apache Spark environment to run your ETL jobs. For your ETL use cases, we recommend you explore using AWS Glue. For other batch-oriented use cases, including some ETL use cases, AWS Batch might be a better fit.

## Pricing and Billing

**Q: How am I charged for AWS Glue?**

You will pay a simple monthly fee, above the AWS Glue Data Catalog free tier, for storing and accessing the metadata in the Data Catalog. You will pay an hourly rate, billed per second, for the crawler run with a 10-minute minimum. If you choose to use a development endpoint to interactively develop your ETL code, you will pay an hourly rate, billed per second, for the time that your development endpoint is provisioned, with a 10-minute minimum. Additionally, you will pay an hourly rate, billed per second, for the ETL job with either a 1-minute minimum or 10-minute minimum based on the AWS Glue version that you select. For more details, see [AWS Glue Pricing](https://aws.amazon.com/glue/pricing/).

**Q: When does billing for my AWS Glue jobs begin and end?**

Billing commences as soon as the job is scheduled for execution and continues until the entire job completes. With AWS Glue, you only pay for the time for which your job runs and not for the environment provisioning or shutdown time.

## Security and Availability

**Q: How does AWS Glue keep my data secure?**

We provide server-side encryption for data at rest and SSL for data in motion.

**Q: What are the service limits associated with AWS Glue?**

Please refer the [AWS Glue Documentation](https://docs.aws.amazon.com/glue/index.html) to learn more about service limits.

**Q: Which Regions is AWS Glue in?**

Please refer to the [AWS Region Table](https://aws.amazon.com/about-aws/global-infrastructure/regional-product-services/) for details of AWS Glue service availability by Region.

**Q: How many DPUs (data processing units) are allocated to the development endpoint?**

A development endpoint is provisioned with 5 DPUs by default. You can configure a development endpoint with a minimum of 2 DPUs and a maximum of 5 DPUs.

**Q: How do I scale the size and performance of my AWS Glue ETL jobs?**

You can specify the number of DPUs that you want to allocate to your ETL job. An AWS Glue ETL job requires a minimum of 2 DPUs. By default, AWS Glue allocates 10 DPUs to each ETL job.

**Q: How do I monitor the execution of my AWS Glue jobs?**

AWS Glue provides the status of each job and pushes all notifications to [CloudWatch](https://aws.amazon.com/cloudwatch/). You can set up SNS notifications through CloudWatch actions to be informed of job failures or completions.

## Service Level Agreement (SLA)

**Q: What does the AWS Glue SLA guarantee?**

Our AWS Glue SLA guarantees a Monthly Uptime Percentage of at least 99.9% for AWS Glue.  

**Q: How do I know if I qualify for an SLA Service Credit?**

You are eligible for an SLA credit for AWS Glue under the AWS Glue SLA if more than one Availability Zone in which you are running a task, within the same Region, has a Monthly Uptime Percentage of less than 99.9% during any monthly billing cycle.
