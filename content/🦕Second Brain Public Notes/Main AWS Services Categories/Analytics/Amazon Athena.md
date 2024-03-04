---
tags:
  - cloud/aws
---



**Amazon Athena** is <mark style="background: #BBFABBA6;">an interactive query service that makes it easy to analyze data in Amazon S3 using standard SQL.</mark>

Athena is a serverless product so <mark style="background: #FFB86CA6;">with Amazon Athena AWS  manages all the infrastructure for you, and you pay only for the queries that you run</mark>.

With Amazon Athena AWS makes it <mark style="background: #BBFABBA6;">extremely easy to use – simply point to your data in Amazon S3, define the schema, and start querying using standard SQL</mark>.

Amazon Athena uses Presto with full standard SQL support and works with a variety of standard data formats, including _CSV_, _JSON_, _ORC_, _Apache Parquet_ and _Avro_.

<mark style="background: #ADCCFFA6;">While Amazon Athena is ideal for quick, ad-hoc querying and integrates with Amazon QuickSight for easy visualization, it can also handle complex analysis, including large joins, window functions, and arrays.</mark>

Amazon Athena uses a managed Data Catalog to store information and schemas about the databases and tables that you create for your data stored in Amazon S3.

With Amazon Athena, you don’t have to worry about managing or tuning clusters to get fast performance.

Amazon Athena is optimized for fast performance with Amazon S3.

<mark style="background: #CACFD9A6;">Amazon Athena automatically executes queries in parallel, so that you get query results in seconds, even on large datasets.</mark>

Most results are delivered within seconds.

With Amazon Athena, <mark style="background: #FFF3A3A6;">there’s no need for complex ETL jobs to prepare data for analysis.</mark>

This makes it easy for anyone with SQL skills to quickly analyze large-scale datasets.

Amazon Athena is out-of-the-box integrated with AWS Glue Data Catalog, allowing you to create a unified metadata repository across various services, crawl data sources to discover schemas and populate your Catalog with new and modified table and partition definitions, and maintain schema versioning.

You can also use Glue’s fully managed ETL capabilities to transform data or convert it into columnar formats to optimize cost and improve performance.  
![[Pasted image 20240214154845.png]]  
![[Pasted image 20240214155030.png]]
## Amazon Athena Features

- You can query Amazon Athena using Standard SQL
- <mark style="background: #ADCCFFA6;">Amazon Athena uses Presto, an open source, distributed SQL query engine optimized for low latency, interactive data analysis. </mark>
- Athena supports a wide variety of data formats such as CSV, JSON, ORC, Avro, or Parquet. 
- With Athena’s federated data source connectors, you can query additional data stores and join the data with data stored in Amazon S3. 
- <mark style="background: #CACFD9A6;">You can access Athena and run queries from the Athena console, API, CLI, AWS SDK,</mark>

On Amazon Athena AWS supports the integration with business intelligence and SQL development applications through Athena’s JDBC and ODBC drivers.

With Amazon Athena AWS use the highly redundant Global infrastructure to maintain high availability. 

Whenever a particular facility is unavailable, Amazon Athena routes queries to another facility based on the available compute resources.

In Amazon Athena AWS uses Amazon S3 as an origin, making your data highly available and durable. 

In addition to providing durable infrastructure for keeping important data, Amazon S3 is designed for 99.999999999% durability on a per object basis.

Amazon Athena integrates directly with Identity and Access Management and you can leverage the use of bucket policies within S3 also. 

By granting IAM policies to IAM users, you can easily control S3 buckets for your users. By controlling access to data in S3, you can restrict users from querying it using Athena.

Additionally, Athena allows you to query encrypted data stored in Amazon S3 and write encrypted results back to your bucket. 

Athena provides connectors for enterprise data sources including Amazon DynamoDB, Amazon Redshift, Amazon OpenSearch, MySQL, PostgreSQL, Redis, and other popular third-party data stores. 

## Amazon Athena Limitations

In terms of optimization capabilities, AWS Athena doesn’t offer much in the way of capabilities. 

<mark style="background: #CACFD9A6;">Although Amazon Athena is a highly scalable and reliable service, it is hosted in a muti-tenant environment. </mark>
  
<mark style="background: #BBFABBA6;">This multi-tenancy approach might trigger throttling from time to time, leading to potential issues.</mark> 

<mark style="background: #ADCCFFA6;">Amazon Athena doesn’t include any kind of Data Manipulation interface for inserting, deleting, and updating data. </mark>

<mark style="background: #ABF7F7A6;">If you intend to run your SQL queries efficiently, you might want to partition the data sets stored in Amazon S3.</mark>  
The number of partitions that you manage to create will substantially affect the speed and performance.

<mark style="background: #FFB8EBA6;">Indexing is not natively supported within Amazon Athena, which is built upon AWS.</mark>

## Use Cases

Query services like Amazon Athena, data warehouses like Amazon Redshift, and sophisticated data processing frameworks like Amazon EMR, all address different needs and use cases.

<mark style="background: #FFB86CA6;">Amazon Redshift provides the fastest query performance for enterprise reporting and business intelligence workloads, particularly those involving extremely complex SQL with multiple joins and sub-queries.</mark>

<mark style="background: #D2B3FFA6;">Amazon EMR makes it simple and cost effective to run highly distributed processing frameworks such as Hadoop, Spark, and Presto when compared to on-premises deployments.</mark> <mark style="background: #BBFABBA6;">Amazon EMR is flexible – you can run custom applications and code, and define specific compute, memory, storage, and application parameters to optimize your analytic requirements.</mark>

<mark style="background: #FFF3A3A6;">Amazon Athena provides the easiest way to run ad-hoc queries for data in S3 without the need to setup or manage any servers.</mark>  
With Athena, you can analyze unstructured, semistructured, and structured data stored in Amazon S3. Examples include CSV, JSON, or columnar data formats such as Apache Parquet and Apache ORC. 

<mark style="background: #FFF3A3A6;">In Athena, ANSI SQL queries can be run ad-hoc without aggregating or loading the data.</mark>

<mark style="background: #FFF3A3A6;">Data visualization is made simple with Athena’s integration with Amazon QuickSight. </mark>

Using Athena, you will be able to generate reports or to explore your data with the help of business intelligence tools or SQL clients that are connected to a JDBC or ODBC driver to generate reports or to explore data.

With AWS Glue Data Catalog, AWS Athena integrates with your data to create a persistent metadata store in Amazon S3, which will allow you to access your data from anywhere. 

<mark style="background: #FFB8EBA6;">With AWS Glue, you can create tables and query data in Athena using a central metadata store that is accessible throughout your Amazon Web Services account.</mark>

In order to troubleshoot a performance issue on your website, Athena is useful for running a quick query on web logs. A table for your data can be defined quickly with Athena, and you can start querying using the standard SQL language.

You should use Amazon Athena if you want to interact with your Cost and Usage Report stored in S3 to gain extremely specific information on how your AWS bill is being calculated. This can be done natively within the console.

The table below shows the primary use case and situations for using a few AWS query and analytics services:

|   |   |   |
|---|---|---|
|**AWS Service**|**Primary Use Case**|**When to use**|
|Amazon Athena|Query|Run interactive queries against data directly in Amazon S3 without worrying about formatting data or managing infrastructure. Can use with other services such as Amazon RedShift|
|Amazon RedShift|Data Warehouse|Pull data from many sources, format and organize it, store it, and support complex, high speed queries that produce business reports.|
|Amazon EMR|Data Processing|Highly distributed processing frameworks such as Hadoop, Spark, and Presto. Run a wide variety of scale-out data processing tasks for applications such as machine learning, graph analytics, data transformation, streaming data.|
|AWS Glue|ETL Service|Transform and move data to various destinations. Used to prepare and load data for analytics. Data source can be S3, RedShift or another database. Glue Data Catalog can be queried by Athena, EMR and RedShift Spectrum|

## Best Practices

[**Best practices**](https://aws.amazon.com/blogs/big-data/top-10-performance-tuning-tips-for-amazon-athena/) for performance with Athena:

- **Partition your data** – Partition the table into parts and keeps the related data together based on column values such as date, country, region, etc. Athena supports Hive partitioning.
- **Bucket your data** – Partition your data is to bucket the data within a single partition.
- **Use Compression** – AWS recommend using either Apache Parquet or Apache ORC.
- **Optimize file sizes** – Queries run more efficiently when reading data can be parallelized and when blocks of data can be read sequentially.
- **Optimize columnar data store generation** – Apache Parquet and Apache ORC are popular columnar data stores.
- **Optimize ORDER BY** – The ORDER BY clause returns the results of a query in sort order.
- **Optimize GROUP BY** – The GROUP BY operator distributes rows based on the GROUP BY columns to worker nodes, which hold the GROUP BY values in memory.
- **Use approximate functions** – For exploring large datasets, a common use case is to find the count of distinct values for a certain column using COUNT(DISTINCT column).
- **Only include the columns that you need** – When running your queries, limit the final SELECT statement to only the columns that you need instead of selecting all columns.

## Pricing

With Amazon Athena, you pay only for the queries that you run.

You are charged based on the amount of data scanned by each query.

You can get significant cost savings and performance gains by compressing, partitioning, or converting your data to a columnar format, because each of those operations reduces the amount of data that Athena needs to scan to execute a query.

## Amazon Athena Frequently Asked Questions (FAQs)

## General

Close all

### What is Amazon Athena?

Athena is an interactive analytics service that makes it simple to analyze data in Amazon Simple Storage Service (S3) using Python. Athena is serverless, so there is no infrastructure to set up or manage, and you can start analyzing data immediately. You don’t even need to load your data into Athena; it works directly with data stored in Amazon S3. Amazon Athena for SQL uses Trino and Presto with full standard SQL support and works with various standard data formats, including CSV, JSON, Apache ORC, Apache Parquet, and Apache Avro. Athena for Apache Spark supports Python and allows you to use Apache Spark, an open-source, distributed processing system used for big data workloads. To get started, log in to the Athena Management Console and start interacting with your data using the query editor or notebooks.

### What Can I Do with Athena?

With Athena, you can analyze data stored in S3 and 30 different data sources, including on-premises data sources or other cloud systems. You can use Athena to run interactive analytics using ANSI SQL or Python without the need to aggregate or load the data into Athena. Athena can process unstructured, semi-structured, and structured datasets. Examples include CSV, JSON, Avro, or columnar data formats such as Parquet and ORC. Amazon Athena for SQL integrates with Amazon QuickSight for visualizing your data or creating dashboards. You can also use Athena to generate reports or explore data with business intelligence tools or SQL clients, connected with an [ODBC](https://docs.aws.amazon.com/athena/latest/ug/connect-with-odbc.html) or [JDBC](https://docs.aws.amazon.com/athena/latest/ug/connect-with-jdbc.html) driver. 

### How Do I Get Started with Athena?

To get started with Athena, log in to the AWS Management Console for Athena and create your schema by writing Data Definition Language (DDL) statements on the console or by using a create table wizard. You can then start querying data using a built-in query editor. Athena queries data directly from S3, so there’s no loading required.

## Amazon Athena for SQL

Close all

### How Do You Access Athena?

Amazon Athena for SQL can be accessed through the AWS Management Console, AWS SDK and CLI, or Athena's ODBC or JDBC driver. You can programmatically run queries, add tables, or partitions using the [ODBC](https://docs.aws.amazon.com/athena/latest/ug/connect-with-odbc.html) or [JDBC](https://docs.aws.amazon.com/athena/latest/ug/connect-with-jdbc.html) driver.

### What is the Underlying Technology behind Athena for SQL?

Athena for SQL uses [Trino](https://trino.io/) with full standard SQL support and works with various standard data formats, including CSV, JSON, ORC, Avro, and Parquet. Athena can handle complex analysis, including large joins, window functions, and arrays. With [Amazon Athena](https://aws.amazon.com/athena) SQL engine version 3 built on Trino, we continue to increase performance and provide new features, similar to our approach on Amazon Athena engine version 2 built on Presto. One of the most exciting aspects of v3 is its new continuous integration approach to open source software management that will keep customers up to date with Trino and PrestoDB projects. We aim to stay within 60-90 days of open-source Trino launches. The Athena development team is actively contributing bug fixes and security, scalability, performance, and feature enhancements back to these open-source code bases, so anyone using [Trino](https://trino.io/), [Presto](https://prestodb.io/), and [Apache Iceberg](https://iceberg.apache.org/) can benefit from the team’s contributions.

### How Does Athena for SQL Store Table Definitions and Schema?

Athena for SQL uses a managed AWS Glue Data Catalog to store information and schemas about the databases and tables that you create for your data stored in S3. In Regions where AWS Glue is available, you can upgrade to using the Data Catalog with Athena. In Regions where AWS Glue is not available, Athena uses an internal catalog.

You can modify the catalog using DDL statements or through the AWS Management Console. Any schemas that you define are automatically saved unless you explicitly delete them. Athena uses schema-on-read technology, which means that your table definitions are applied to your data in S3 when queries are being applied. There’s no data loading or transformation required. You can delete table definitions and schema without impacting the underlying data stored in S3.

### Why Should I Upgrade to Data Catalog?

[AWS Glue](https://aws.amazon.com/glue/) is a fully managed extract, transform, and load (ETL) service. AWS Glue has three main components: 1) a crawler that automatically scans your data sources, identifies data formats, and infers schemas, 2) a fully managed ETL service that allows you to transform and move data to various destinations, and 3) a Data Catalog that stores metadata information about databases and tables either stored in S3 or an [ODBC](https://docs.aws.amazon.com/athena/latest/ug/connect-with-odbc.html)\- or [JDBC](https://docs.aws.amazon.com/athena/latest/ug/connect-with-jdbc.html)\-compliant data store. To use the benefits of AWS Glue, you must upgrade from using Athena’s internal Data Catalog to the Glue Data Catalog.

Benefits of upgrading to the Data Catalog include the following:

- Unified metadata repository: AWS Glue is integrated across various AWS services. AWS Glue supports data stored in Amazon Aurora, Amazon Relational Database Service (RDS) for MySQL, Amazon RDS for PostgreSQL, Amazon Redshift, and S3, as well as MySQL and PostgreSQL databases in your Amazon Virtual Private Cloud (VPC) running on Amazon Elastic Compute Cloud (EC2). AWS Glue provides out-of-the-box integration with Athena, Amazon EMR, Amazon Redshift Spectrum, and applications compatible with Apache Hive metastore.
- Automatic schema and partition recognition: AWS Glue automatically crawls your data sources, identifies data formats, and suggests schemas and transformations. Crawlers can help automate table creation and automatic loading of partitions.

To learn more about the Data Catalog, review the [AWS Glue](https://aws.amazon.com/glue/) webpage.

### Is there a Step-by-step Process to Upgrade to the Data Catalog

Yes. For a step-by-step process, review the Amazon Athena User Guide: [Integration with AWS Glue](https://docs.aws.amazon.com/athena/latest/ug/glue-athena.html).

### In Which Regions is Athena Available?

For details of Athena service availability by Region, review the [AWS Regional Services List](https://aws.amazon.com/about-aws/global-infrastructure/regional-product-services/).

### What Are the Service Limits Associated with Athena?

To learn more about service limits, review the Amazon Athena User Guide: Service Quotas.

## Creating Tables, Data Formats, and Partitions

Close all

### How Do I Create Tables and Schemas for My Data on S3?

Athena uses Apache Hive DDL to define tables. You can run DDL statements using the Athena console, with an [ODBC](https://docs.aws.amazon.com/athena/latest/ug/connect-with-odbc.html) or [JDBC](https://docs.aws.amazon.com/athena/latest/ug/connect-with-jdbc.html) driver, through the API, or using the Athena create table wizard. If you use the Data Catalog with Athena, you can also use AWS Glue crawlers to automatically infer schemas and partitions. An AWS Glue crawler connects to a data store, progresses through a prioritized list of classifiers to extract the schema of your data and other statistics, and then populates the Data Catalog with this metadata. Crawlers can run periodically to detect the availability of new data and changes to existing data, including table definition changes. Crawlers automatically add new tables, new partitions to existing table, and new versions of table definitions. You can customize AWS Glue crawlers to classify your own file types. 

When you create a new table schema in Athena, the schema is stored in the Data Catalog and used when running queries, but it does not modify your data in S3. Athena uses an approach known as schema-on-read, which allows you to project your schema onto your data when you run a query. This decreases the need for any data loading or transformation. Learn more about [creating tables](http://docs.aws.amazon.com/athena/latest/ug/creating-tables.html). 

### Which Data Formats Does Athena Support?

Athena supports various data formats like CSV, TSV, JSON, or Textfiles and also supports open-source columnar formats, such as ORC and Parquet. Athena also supports compressed data in Snappy, Zlib, LZO, and GZIP formats. You can improve performance and reduce your costs by compressing, partitioning, and using columnar formats. 

### Which Kinds of Data Types Does Athena Support?

Athena supports both simple data types, such as INTEGER, DOUBLE, and VARCHAR, and complex data types, such as MAPS, ARRAY, and STRUCT.  

### Can I Run Any Hive Query on Athena?

Athena uses Hive only for DDL and creation/modification and deletion of tables or partitions. For a complete list of statements supported, review the Amazon Athena User Guide: [DDL statements](https://docs.aws.amazon.com/athena/latest/ug/language-reference.html). Athena uses Trino and Presto when you run SQL queries on S3. You can run ANSI-compliant SQL SELECT statements to query your data on S3.

### What is a SerDe?

SerDe stands for Serializer/Deserializer, which are libraries that tell Hive how to interpret data formats. Hive DDL statements require you to specify a SerDe so that the system knows how to interpret the data that you’re pointing to. Athena uses SerDes to interpret the data read from S3. The concept of SerDes in Athena is the same as the concept used in Hive. Amazon Athena supports the following SerDes:

- Apache Web Logs: "org.apache.hadoop.hive.serde2.RegexSerDe"
- CSV: "org.apache.hadoop.hive.serde2.lazy.LazySimpleSerDe"
- TSV: "org.apache.hadoop.hive.serde2.lazy.LazySimpleSerDe"
- Custom Delimiters: "org.apache.hadoop.hive.serde2.lazy.LazySimpleSerDe"
- Parquet: "org.apache.hadoop.hive.ql.io.parquet.serde.ParquetHiveSerDe"
- Orc: "org.apache.hadoop.hive.ql.io.orc.OrcSerde"
- JSON: “org.apache.hive.hcatalog.data.JsonSerDe” or "org.openx.data.jsonserde.JsonSerDe"

### Can I Add My Own SerDe to Athena?

Currently, you cannot add your own SerDe to Athena. We appreciate your feedback, so if there are any SerDes that you would like to see added, contact the Athena team at [athena-feedback@amazon.com](mailto:Athena-feedback@amazon.com).

### If I Created Parquet/ORC Files Using Spark/Hive, Will I Be Able to Query Them in Athena?

Yes, Parquet and ORC files created with Spark can be read in Athena.

### If I Have Data from Amazon Kinesis Data Firehose, how Can I Query it Using Athena?

If your Kinesis Data Firehose data is stored in S3, you can query it using Athena. Create a schema for your data in Athena and start querying. We recommend that you organize the data into partitions to enhance performance. You can add partitions created by Data Firehose using ALTER TABLE DDL statements. Learn more about [partitioning data](https://docs.aws.amazon.com/athena/latest/ug/partitions.html). 

### Does Athena Support Data Partitioning?

Yes. You can partition your data on any column with Athena. Partitions allow you to limit the amount of data that each query scans, leading to cost savings and faster performance. You can specify your partitioning scheme using the PARTITIONED BY clause in the CREATE TABLE statement. [Amazon Athena](https://aws.amazon.com/athena/) supports [AWS Glue Data Catalog](https://docs.aws.amazon.com/glue/latest/dg/components-overview.html) partition indexes to optimize query planning and reduce query runtime. When you query a table containing a large number of partitions, Athena retrieves the available partitions from the AWS Glue Data Catalog and determines which are required by your query. As new partitions are added, the time needed to retrieve the partitions increases and can cause query runtime to increase. AWS Glue Data Catalog allows customers to create [partition indexes](https://docs.aws.amazon.com/glue/latest/dg/partition-indexes.html) which reduce the time required to retrieve and filter partition metadata on tables with tens and hundreds of thousands of partitions.

### How Do I Add New Data to an Existing Table in Athena?

If your data is partitioned, you will need to run a metadata query (ALTER TABLE ADD PARTITION) to add the partition to Athena after new data becomes available on S3. If your data is not partitioned, adding the new data (or files) to the existing prefix automatically adds the data to Athena. Learn more about [partitioning data](https://docs.aws.amazon.com/athena/latest/ug/partitions.html).

### If I Already Have Large Quantities of Log Data on S3, Can I Use Athena to Query It?

Yes, Athena streamlines the running of standard SQL queries on your existing log data. Athena queries data directly from S3, so there’s no data movement or loading required. Define your schema using DDL statements and start querying your data right away.

## Querying, Data Formats, and Multicloud

Close all

### Which Kinds of Queries Does Athena Support?

Athena supports ANSI SQL queries. Athena uses Trino, an open-source, in-memory, distributed SQL engine, and can handle complex analysis, including large joins, window functions, and arrays.

### Can I Use QuickSight with Athena?

Yes. Athena integrates with QuickSight, so you can seamlessly visualize your data stored in S3. 

### Does Athena Support other Business Intelligence (BI) Tools and SQL Clients?

Yes. Athena comes with an ODBC and JDBC driver that you can use with other BI tools and SQL clients. Learn more about using an [ODBC](https://docs.aws.amazon.com/athena/latest/ug/connect-with-odbc.html) or [JDBC](https://docs.aws.amazon.com/athena/latest/ug/connect-with-jdbc.html) driver with Athena. 

### How Do I Access the Functions Supported by Athena?

Learn more about [functions](https://docs.aws.amazon.com/athena/latest/ug/language-reference.html) supported by Athena. 

### How Do I Improve the Performance of My Query?

You can improve the performance of your query by compressing, partitioning, or converting your data into columnar formats. Athena supports open-source columnar data formats, such as Parquet and ORC. Converting your data into a compressed, columnar format lowers your cost and improves query performance by enabling Athena to scan less data from S3 when running your query.

### Does Athena Support User-defined Functions (UDFs)?

Yes. Athena supports UDFs so that you can write custom scalar functions and invoke them in SQL queries. While Athena provides built-in functions, UDFs help you perform custom processing, such as compressing and decompressing data, redacting sensitive data, or applying customized decryption.

You can write UDFs in Java using the Athena Query Federation SDK. When a UDF is used in a SQL query submitted to Athena, it is invoked and run on AWS Lambda. UDFs can be used in both SELECT and FILTER clauses of a SQL query. You can invoke multiple UDFs in the same query. 

### What is the User Experience when Writing a UDF?

You can use the Athena Query Federation SDK to write your UDF. Review [UDF examples](https://github.com/awslabs/aws-athena-query-federation/tree/master/athena-udfs). You can upload your function to Lambda and then invoke it in your Athena query. To get started, refer to the Amazon Athena User Guide: [Creating and deploying a UDF using Lambda](https://docs.aws.amazon.com/athena/latest/ug/querying-udf.html#udf-creating-and-deploying).

Athena will invoke your UDF on a batch of dataset rows to enhance performance. 

### Does Athena Support Multicloud Analytics?

Yes, Athena offers several data source connectors that you can use to analyze data in other cloud service providers and other cloud storage services without moving or transforming the data. Data source connectors are available for 30 data sources, including Azure Synapse, Azure Data Lake Storage, Google BigQuery, and Google Cloud Storage. Learn more about AWS solutions for [hybrid and multicloud environments](https://aws.amazon.com/hybrid-multicloud/).

## Federated Query

Close all

### What is a Federated Query?

If you have data in sources other than S3, you can use Athena to query the data in place or build pipelines that extract data from multiple data sources and store them on S3. With Athena Federated Query, you can run SQL queries across data stored in relational, nonrelational, object, and custom data sources.

### Why Should I Use Federated Queries in Athena?

Organizations often store data in a data source that meets the needs of their applications or business processes. These can include relational, key-value, document, in-memory, search, graph, time-series, and ledger databases in addition to storing data in an S3 data lake. Performing analytics on such diverse sources can be complex and time consuming because it typically requires learning new programming languages or database constructs and building complex pipelines to extract, transform, and duplicate data before it can be used for analysis. Athena reduces this complexity by allowing you to run SQL queries on the data where it is. You can use well-known SQL constructs to query data across multiple data sources for quick analysis, or use scheduled SQL queries to extract and transform data from multiple data sources and store them on S3 for further analysis.

### Which Data Sources Are Supported?

Athena provides built-in connectors to 30 popular AWS, on-premises, and other cloud data stores, including Amazon Redshift, Amazon DynamoDB, Google BigQuery, Google Cloud Storage, Azure Synapse, Azure Data Lake Storage, Snowflake, and SAP Hana. You can use these connectors to enable SQL analytics use cases on structured, semistructured, object, graph, time series, and other data storage types. For a list of supported sources, see [Using Athena data source connectors](https://docs.aws.amazon.com/athena/latest/ug/athena-prebuilt-data-connectors.html).

  
You can also use the Athena data connector SDK to create a custom data source connector and query it with Athena. Get started by reviewing [the documentation](https://docs.aws.amazon.com/athena/latest/ug/athena-prebuilt-data-connectors.html) and example connector implementation.

### Which Use Cases Does Federated Query Enable?

With Athena, you can use your existing SQL knowledge to extract insights from various data sources without learning a new language, developing scripts to extract (and duplicate) data, or managing infrastructure. Using Amazon Athena, you can perform the following tasks:

- Run on-demand analysis on data spread across multiple data stores using a single tool and SQL dialect.
- Visualize data in BI applications that push complex, multisource joins down to Athena’s distributed compute engine over [ODBC](https://docs.aws.amazon.com/athena/latest/ug/connect-with-odbc.html) and [JDBC](https://docs.aws.amazon.com/athena/latest/ug/connect-with-jdbc.html) interfaces.
- Design self-service ETL pipelines and event-based data-processing workflows with Athena integration with AWS Step Functions.
- Unify diverse data sources to produce rich input features for ML model-training workflows.
- Develop user-facing data-as-a-product applications that surface insights across data mesh architectures.
- Support analytics use cases while your organization migrates on-premises sources to AWS.

### Can I Use Federated Query for ETL?

Athena saves query results to a file on S3. This means you can use Athena to make federated data available to other users and applications. If you want to perform analysis on the data using Athena without repeatedly querying the underlying source, use the Athena CREATE TABLE AS function. You can also use the Athena UNLOAD function to query the data and store the results in a specific file format on S3

### How Do Data Source Connectors Work?

A data source connector is a piece of code that runs on Lambda that translates between your target data source and Athena. When you use a data source connector to register a data store with Athena, you can run SQL queries on federated data stores. When a query runs on a federated source, Athena calls the Lambda function and tasks it with running the parts of your query that are specific to the federated source. To learn more, review the Amazon Athena User Guide: [Using Amazon Athena Federated Query](https://docs.aws.amazon.com/athena/latest/ug/connect-to-a-data-source.html). 

## Machine Learning

Close all

### Which Use Cases Does Athena Support for Embedded ML?

Athena use cases for ML span different industries, as in the following examples. Financial risk data analysts can run what-if analysis and Monte Carlo simulations. Business analysts might run linear regression or forecasting models to predict future values to help them create richer and forward-looking business dashboards that forecast revenues. Marketing analysts can use k-means clustering models to help determine their different customer segments. Security analysts can use logistic regression models to find anomalies and detect security incidents from logs.

### Which ML Models Can Be Used with Athena?

Athena can invoke any ML model that is deployed on SageMaker. You have the flexibility to train your own model using your proprietary data, or use a model that is pretrained and deployed on SageMaker. For example, cluster analysis would likely be trained on your own data because you want to categorize new records into the same categories that you used for previous records. Alternatively, for predicting real-world sports events, you could use a publicly available model because the training data used would be in the public domain already. Domain-specific or industry-specific predictions will typically be trained on your own data in SageMaker, while undifferentiated ML needs might use external models.

### Can I Train My ML Model Using Athena?

You cannot train and deploy your ML models on SageMaker using Athena. You can train your ML model or use an existing pretrained model that is deployed on SageMaker using Athena. Read the documentation detailing [training steps on SageMaker](https://aws.amazon.com/getting-started/tutorials/build-train-deploy-machine-learning-model-sagemaker/).

### Can I Run Inference on Models Deployed on other Services such as Comprehend, Forecasting, or Models Deployed on My Own EC2 Cluster?

Athena only supports invoking ML models deployed on SageMaker. We welcome feedback on what other services that you want to use with Athena. Email us your feedback to: [athena-feedback@amazon.com](mailto:athena-feedback@amazon.com).

### What Are the Performance Implications of Using Athena Queries for SageMaker Inference?

Operational performance improvements are constantly being added to our features and services. To enhance performance of your Athena ML queries, rows are batched when invoking your SageMaker ML model for inference. At this time, user-provided row batch size overrides are not supported.

### Which Features Does Athena ML Support?

Athena offers ML inference (prediction) capabilities wrapped by a SQL interface. You can also call an Athena UDF to invoke preor post-processing logic on your result set. Inputs can include any column, record, or table, and multiple calls can be batched together for higher scalability. You can run inference in the Select phase or in the Filter phase. To learn more, refer to the Amazon Athena User Guide: [Using Machine Learning (ML) with Amazon Athena](https://docs.aws.amazon.com/athena/latest/ug/querying-mlmodel.html).

### Which ML Models Can I Use?

SageMaker supports various ML algorithms. You can also create your proprietary ML model and deploy it on SageMaker. For example, cluster analysis would likely be trained on your own data because you want to categorize new records into the same categories that you used for previous records. Alternatively, for predicting real-world sports events, you could use a publicly available model because the training data used would be in the public domain.

We expect that domainor industry-specific predictions will typically be trained on your own data in SageMaker, while undifferentiated ML needs such as machine translation will use external models. 

## Security and Availability

Close all

### How Do I Control Access to My Data?

Amazon Athena supports fine-grained access control with AWS Lake Formation. AWS Lake Formation allows for centrally managing permissions and access control for data catalog resources in your S3 data lake. You can enforce fine-grained access control policies in Athena queries for data stored in any supported file format using table formats such as Apache Iceberg, Apache Hudi, and Apache Hive. You get the flexibility to choose the table and file format best suited for your use case and get the benefit of centralized data governance to secure data access when using Athena. For example, you can use Iceberg table format to store data in your S3 data lake for reliable write transactions at scale together with row-level security filters in Lake Formation so that data analysts residing in different countries get access to data only for customers located in their own country to meet the regulatory requirements. The new expanded support for table and file formats does not require any change in how you set up fine-grained access control policies in Lake Formation and requires [Athena engine version 3](https://docs.aws.amazon.com/athena/latest/ug/engine-versions-reference.html#engine-versions-reference-0003) which [offers new features and improved query performance](https://aws.amazon.com/blogs/big-data/upgrade-to-athena-engine-version-3-to-increase-query-performance-and-access-more-analytics-features/). Athena also allows you to control access to your data by using AWS Identity and Access Management (IAM) policies, access control lists (ACLs), and S3 bucket policies. With IAM policies, you can grant IAM users fine-grained control to your S3 buckets. By controlling access to data on S3, you can restrict users from querying it using Athena.

### Can Athena Query Encrypted Data in S3?

Yes, you can query data that’s encrypted using server-side encryption (SSE) with S3-managed encryption keys, SSE with AWS Key Management Service (KMS)–managed keys, and client-side encryption (CSE) with keys managed by AWS KMS. Athena also integrates with AWS KMS and provides you with an option to encrypt your result sets.

### Is Athena Highly Available?

Yes. Athena is highly available and runs queries using compute resources across multiple facilities, automatically routing queries appropriately if a particular facility is unreachable. Athena uses S3 as its underlying data store, making your data highly available and durable. S3 provides durable infrastructure to store important data. Your data is redundantly stored across multiple facilities and multiple devices in each facility.

### Can I provide Cross-account Access to Someone else’s S3 Bucket?

Yes, you can provide cross-account access to S3.

## Pricing and Billing

Close all

### How is Athena Priced?

With Athena, you can choose to pay per query based on data scanned or based on the compute needed by your queries. Per query is pricing per query is based on the amount of data scanned, in terabytes (TB), by the query. You can store data in various formats on S3. If you compress your data, partition, or convert it to a columnar storage formats, you’ll pay less because your queries scan less data. Converting data to a columnar format allows Athena to read only the columns that it must process the query. With Provisioned Capacity, you pay an hourly price for query processing capacity, not data scanned. You can use per query billing and compute-based billing within the same account. For more details, review the [Amazon Athena pricing](https://aws.amazon.com/athena/pricing/) page.

### Why Do I Get Charged less when I Use a Columnar Format?

With per query billing, Athena charges based the amount of data scanned per query. Compressing your data allows Athena to scan less data. Converting your data to columnar formats allows Athena to selectively read only required columns to process the data. Partitioning your data also allows Athena to restrict the amount of data scanned. This leads to cost savings and improved performance. For more details, review the [Amazon Athena pricing](https://aws.amazon.com/athena/pricing/) page.

### How Do I Lower My Costs?

With per query billing, you can save 30% to 90% per query and get better performance by compressing, partitioning, and converting your data into columnar formats. Each of these operations reduces the amount of data scanned and time required for execution. These operations are recommended when using Provisioned Capacity, too, because they often reduce the amount of time a query spends executing.

### Does Athena charge Me for Failed Queries?

With per query pricing, you are not charged for failed queries.

### Does Athena charge Me for Canceled Queries?

Yes. If you cancel a query, you are charged for the amount of data scanned up to the point at which you canceled the query.

### Are there Any Additional Charges Associated with Athena?

Athena queries data directly from S3, so your source data is billed at S3 rates. When Athena runs a query, it stores the results in an S3 bucket of your choice. You are then billed at standard S3 rates for these result sets. It is recommended that you monitor these buckets and use lifecycle policies to control how much data gets retained.

### Will I Be Charged for Using Data Catalog?

Yes. You are charged separately for using the Data Catalog. To learn more about Data Catalog pricing, review the [AWS Glue pricing](https://aws.amazon.com/glue/pricing/) page. 

## Amazon Athena for Apache Spark

Close all

### What is Amazon Athena for Apache Spark?

Athena supports Apache Spark framework to enable data analysts and data engineers with the interactive, fully managed experience of Athena. Apache Spark is a popular open-source, distributed processing system that is enhanced for fast analytics workloads against data of any size that offers a rich system of open-source libraries. You can now build Spark applications in expressive languages, such as Python, using a simplified notebook experience in the Athena console or through Athena APIs. You can query data from various sources, chain together multiple calculations, and visualize the results of their analyses. For interactive Spark applications, you spend less time waiting and are more productive as Athena starts running applications under a second. Customers get a simplified and purpose-built Spark experience that minimizes work required for version upgrades, performance tuning, and integration with other AWS services.

### Why Should I Use Athena for Apache Spark?

Use Athena for Apache Spark when you need an interactive, fully managed analytics experience and a tight integration with AWS services. You can use Spark to perform analytics in Athena using familiar, expressive languages such as Python and the growing environment of Spark packages. You can also enter their Spark applications through Athena APIs or into simplified notebooks in the Athena console, and begin running Spark applications under a second without setting up and tuning the underlying infrastructure. Like the SQL query capabilities of Athena, Athena offers a fully managed Spark experience and handles the performance tuning, machine configurations, and software patching automatically so that you do not need to worry about keeping current with version upgrades. Also, Athena is tightly integrated with other analytics services in the AWS system such as Data Catalog. Therefore, you can create Spark applications on data in S3 data lakes by referencing tables from your Data Catalog.

### How Do I Start Working with Athena for Apache Spark?

To get started with Athena for Apache Spark, you can start a notebook in the Athena console or start a session using the AWS Command Line Interface (CLI) or Athena API. In your notebook, you can start entering and shutting down Spark applications using Python. Athena also integrates with Data Catalog, so you can work with any data source referenced in the catalog, including data directly in S3 data lakes. Using notebooks, you can now query data from various sources, chain together multiple calculations, and visualize the results of their analyses. On your Spark applications, you can check the execution status and review logs and execution history in the Athena console.

### Which Spark Version is Athena Based On?

Athena for Apache Spark is based on the stable Spark 3.2 release. As a fully managed engine, Athena will provide a custom build of Spark and will handle most Spark version updates automatically in a backward-compatible way without requiring your involvement

### How is Athena for Apache Spark Priced?

You only pay for the time your Apache Spark application takes to run. You are charged an hourly rate based on the number of Data Processing Units (or DPUs) used to run your Apache Spark application. A single DPU provides 4 vCPU and 16 GB of memory. You will be billed in increments of 1 second, rounded up to the nearest minute.

When you start a Spark session either by starting a notebook on the Athena console or using Athena API, two nodes are provisioned for your application: a notebook node that will act as the server for the notebook user interface and a Spark driver node that coordinated that Spark application and communicates with all the Spark worker nodes. Athena will charge you for driver and worker nodes during the duration of the session. Amazon Athena provides notebooks on the console as a user interface for creating, submitting, and executing Apache Spark applications and offers it to you at no additional cost. Athena does not charge for the notebook nodes used during the Spark session.

## When to Use Athena versus other Big Data Services

Close all

### What is the Difference between Athena, Amazon EMR, and Amazon Redshift?

Query services like Athena, data warehouses like Amazon Redshift, and sophisticated data processing frameworks like Amazon EMR all address different needs and use cases. You just need to choose the right tool for the job. Amazon Redshift provides the fastest query performance for enterprise reporting and business intelligence workloads, particularly those involving complex SQL with multiple joins and subqueries. Amazon EMR simplifies the process and makes it and cost effective to run highly distributed processing frameworks, such as Apache Hadoop, Spark, and Presto when compared to on-premises deployments. Amazon EMR is flexible—you can run custom applications and code and define specific compute, memory, storage, and application parameters to enhance your analytic requirements. Athena provides a simplified way to run interactive queries for data in S3 without the need to set up or manage any servers.

### How Does the Athena SQL Support Compare to Redshift, and how Do I Choose between the Two Services?

Amazon Athena and Amazon Redshift Serverless address different needs and use cases even if both services are serverless and enable SQL users.

With its Massively Parallel Processing (MPP) architecture that separates storage and compute and machine learning–led automatic optimization capabilities, a data warehouse such as Amazon Redshift, whether its serverless or provisioned, is a great choice for customers that need the best price performance at any scale for complex BI and analytics workloads. Redshift is best suited for driving scaled analytics and massive, structured, and semi-structured datasets. It performs well for enterprise reporting and business intelligence workloads, particularly those involving extremely complex SQL with multiple joins and subqueries. Redshift offers deep integration with AWS database, analytics, and ML services so customers access data in place or ingest or move data easily into the warehouse for high performance analytics, through minimal ETL and no-code methods. With federated query capabilities, Amazon Redshift Spectrum, integration with Amazon Aurora, AWS Data Exchange, streaming data services, and others, Redshift lets you use data from multiple sources, combine with the data in the warehouse, and conduct analytics and machine learning on top of it. Redshift offers both provisioned and serverless options to get started with analytics easily without managing infrastructure.

Athena is well suited for interactive analytics and data exploration of data in Amazon Simple Storage Service (S3) or any data source through an extensible connector framework (includes over 30 out-of-box connectors for applications and on-premises or other cloud analytics systems) with an easy-to-use SQL syntax. Amazon Athena is built on open-source engines and frameworks such as Spark, Presto, and Apache Iceberg, giving customers the flexibility to use Python or SQL or work on open-data formats. If customers want to do interactive analytics using open-source frameworks and data formats, Amazon Athena is a great place to start. It is completely serverless, meaning there’s no infrastructure to manage or set up. The openness of Athena increases the data portability, allowing our customer to move data among different application, programs, and even cloud service providers. It has recently adopted a new continuous integration approach to open-source software management that will constantly integrate the latest features from the Trino, PrestoDB, and Apache Iceberg projects.

### When Should I Use Amazon EMR versus Athena?

Amazon EMR goes far beyond just running SQL queries. With Amazon EMR, you can run various scale-out data processing tasks for applications, such as machine learning (ML), graph analytics, data transformation, streaming data, and virtually anything that you can code. Use Amazon EMR if you use custom code to process and analyze large datasets with the latest big data processing frameworks, such as Apache HBase, Spark, Hadoop, or Presto. Amazon EMR gives you full control over the configuration of your clusters and the software installed on them.

You should use Athena if you want to run interactive SQL queries against data on S3 without having to manage any infrastructure or clusters.

### How Does Athena’s Spark Support Compare to EMR Serverless for Spark? When Would a Customer Use Spark in Athena instead of EMR Serverless?

EMR Serverless is the easiest way to run Spark and Hive applications in the cloud and the only serverless Hive solution in the industry. With EMR Serverless, you can eliminate the operational overhead of tuning, rightsizing, securing, patching, and managing clusters, and only pay for the resources that your applications actually use. With EMR’s performance optimized runtime, you get 2x+ faster performance than standard open source, so your applications run faster, and reduce your compute costs. EMR’s performance-optimized runtime is 100% API compatible with standard open source, so you do not have to rewrite your applications to run them on EMR. You also do not need deep Spark expertise to turn them on since these are turned on by default. EMR provides the option to run applications on EMR clusters, EKS clusters, or EMR Serverless. EMR clusters are suitable for customers that need maximum control and flexibility over how to run their application. With EMR clusters, customers can choose the EC2 instance type, customize the Amazon Linux Image AMI, customize EC2 instance configuration, customize and extend open-source frameworks, and install additional custom software on cluster instances. EMR on EKS is suitable for customers that want to standardize on EKS to manage clusters across applications or use different versions of an open-source framework on the same cluster. EMR Serverless is suitable for customers who want to avoid managing and operating clusters and simply want to run applications using open-source frameworks.

If customers want an instant on, an interactive experience similar to the interactive SQL-based query experience with Amazon Athena, then they can choose Amazon Athena for Apache Spark. The customer experience in Athena is optimized for interactive applications with short runtimes and requiring sub-second startup time. Amazon Athena handles the performance tuning, configurations, software patching, and updates automatically without customer involvement. For the data analyst and developer with PySpark programming language depth and interest in data exploration and running interactive analytics immediately, Amazon Athena for Apache Spark offers an easy to use experience.

### Can I Use Athena to Query Data that I Process Using Amazon EMR?

Yes, Athena supports many of the same data formats as Amazon EMR. The Athena Data Catalog is compatible with the Hive metastore. If you're using Amazon EMR and already have a Hive metastore, you run your DDL statements on Athena, and then you can start querying your data right away without impacting your Amazon EMR jobs. 

### How Does Federated Query in Athena SQL Relate to other AWS Services?

Federated query in Athena provides you with a unified way to run SQL queries across various relational, nonrelational, and custom data sources.

### How Does ML in Athena Relate to other AWS Services?

Athena SQL queries can invoke ML models deployed on Amazon SageMaker. You can specify the S3 location where they want to store results of these Athena SQL queries.