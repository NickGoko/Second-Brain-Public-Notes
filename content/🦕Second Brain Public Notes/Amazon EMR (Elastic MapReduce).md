---
tags:
  - cloud/aws
---
![[Pasted image 20240214170145.png]]  
![[Pasted image 20240214170428.png]]

Amazon EMR is <mark style="background: #FFB86CA6;">a web service that enables businesses, researchers, data analysts, and developers to process vast amounts of data.</mark>

<mark style="background: #BBFABBA6;">EMR utilizes a hosted Hadoop framework running on Amazon EC2 and Amazon S3</mark>.

<mark style="background: #ADCCFFA6;">With EMR you can run petabyte-scale analysis at less than half of the cost of traditional on-premises solutions and over 3x faster than standard Apache Spark.</mark>

<mark style="background: #FFF3A3A6;">You can run workloads on Amazon EC2 instances, on Amazon Elastic Kubernetes Service (EKS) clusters, or on-premises using EMR on AWS Outposts.</mark>

Runs in one Availability Zone within an Amazon VPC.

Supports Apache Spark, HBase, Presto and Flink.

<mark style="background: #BBFABBA6;">Most used for log analysis, financial analysis, or extract, translate and loading (ETL) activities.</mark>

A Step is a programmatic task for performing some process on the data (e.g. count words).

A cluster is a collection of EC2 instances provisioned by EMR to run your Steps.

EMR is a good place to deploy Apache Spark, an open-source distributed processing used for big data workloads which utilizes in-memory caching and optimized query execution.

You can also launch Presto clusters. Presto is an open source distributed SQL query engine designed for fast analytic queries against large datasets.

EMR launches all nodes for a given cluster in the same Amazon EC2 Availability Zone.

You can access Amazon EMR by using the AWS Management Console, Command Line Tools, SDKs, or the EMR API.

With EMR you have access to the underlying operating system (you can SSH in).

# FAQ
**Q: What does EMR Connector to Kinesis enable?**

<mark style="background: #FFB86CA6;">The connector enables EMR to directly read and query data from Kinesis streams</mark>.  
 You can now perform batch processing of Kinesis streams using existing Hadoop ecosystem tools such as Hive, Pig, MapReduce, Hadoop Streaming, and Cascading.

**Q: What does the EMR connector to Kinesis enable that I couldn’t have done before?**

Reading and processing data from a Kinesis stream would require you to write, deploy and maintain independent stream processing applications. These take time and effort. However, <mark style="background: #ABF7F7A6;">with this connector, you can start reading and analyzing a Kinesis stream by writing a simple Hive or Pig script</mark>. This means you can analyze Kinesis streams using SQL! Of course, other Hadoop ecosystem tools could be used as well. You don’t need to developed or maintain a new set of processing applications.

**Q: Who will find this functionality useful?**

The following types of users will find this integration useful:

- Hadoop users who are interested in utilizing the extensive set of Hadoop ecosystem tools to analyze Kinesis streams.  
    
- Kinesis users who are looking for an easy way to get up and running with stream processing and ETL of Kinesis data.  
    
- Business analysts and IT professionals who would like to perform ad-hoc analysis of data in Kinesis streams using familiar tools like SQL (via Hive) or scripting languages like Pig.  
    

**Q: What are some use cases for this integration?**

The following are representative use cases are enabled by this integration:

- Streaming Log Analysis: You can analyze streaming web logs to generate a list of top 10 error type every few minutes by region, browser, and access domains.  
    
- Complex Data Processing Workflows: You can join Kinesis stream with data stored in S3, Dynamo DB tables, and HDFS. You can write queries that join clickstream data from Kinesis with advertising campaign information stored in a DynamoDB table to identify the most effective categories of ads that are displayed on particular websites.  
    
- Ad-hoc Queries: You can periodically load data from Kinesis into HDFS and make it available as a local Impala table for fast, interactive, analytic queries.  
    

**Q: What EMR AMI version do I need to be able to use the connector?**

You need to use EMR’s AMI version 3.0.4 and later.

**Q: Is this connector a stand-alone tool?**

No, it is a built in component of the Amazon distribution of Hadoop and is present on EMR AMI versions 3.0.4 and later. Customer simply needs to spin up a cluster with AMI version 3.0.4 or later to start using this feature.

**Q: What data format is required to allow EMR to read from a Kinesis stream?**

The EMR Kinesis integration is not data format-specific. You can read data in any format. Individual Kinesis records are presented to Hadoop as standard records that can be read using any Hadoop MapReduce framework. Individual frameworks like Hive, Pig and Cascading have built in components that help with serialization and deserialization, making it easy for developers to query data from many formats without having to implement custom code. For example, in Hive users can read data from JSON files, XML files and SEQ files by specifying the appropriate Hive SerDe when they define a table. Pig has a similar component called Loadfunc/Evalfunc and Cascading has a similar component called a [Tap](http://docs.cascading.org/cascading/2.1/userguide/html/ch03s05.html). Hadoop users can leverage the extensive ecosystem of Hadoop adapters without having to write format-specific code. You can also implement custom deserialization formats to read domain specific data in any of these tools.

**Q: How do I analyze a Kinesis stream using Hive in EMR?**

Create a table that references a Kinesis stream. You can then analyze the table like any other table in Hive. Please see our [tutorials](http://docs.aws.amazon.com/ElasticMapReduce/latest/DeveloperGuide/emr-kinesis.html) for page more details.

**Q: Using Hive, how do I create queries that combine Kinesis stream data with other data source?**

First create a table that references a Kinesis stream. Once a Hive table has been created, you can join it with tables mapping to other data sources such as Amazon S3, Amazon Dynamo DB, and HDFS. This effectively results in joining data from Kinesis stream to other data sources.

**Q: Is this integration only available for Hive?**

No, you can use Hive, Pig, MapReduce, Hadoop Streaming, and Cascading.

**Q: How do I setup scheduled jobs to run on a Kinesis stream?**

The EMR Kinesis input connector provides features that help you configure and manage scheduled periodic jobs in traditional scheduling engines such as Cron. For example, you can develop a Hive script that runs every N minutes. In the configuration parameters for a job, you can specify a **Logical Name** for the job. The Logical Name is a label that will inform the EMR Kinesis input connector that individual instances of the job are members of the same periodic schedule. The Logical Name allows the process to take advantage of iterations, which are explained next.

Since MapReduce is a batch processing framework, to analyze a Kinesis stream using EMR, the continuous stream is divided in to batches. Each batch is called an **Iteration**. Each Iteration is assigned a number, starting with 0. Each Iteration’s boundaries are defined by a start sequence number and end sequence number. Iterations are then processed sequentially by EMR.

In the event of an attempt’s failure, the EMR Kinesis input connector will re-try the iteration within the Logical Name from the known start sequence number of the iteration. This functionality ensures that successive attempts on the same iteration will have precisely the same input records from the Kinesis stream as the previous attempts. This guarantees idempotent (consistent) processing of a Kinesis stream.

You can specify Logical Names and Iterations as runtime parameters in your respective Hadoop tools. For example, in the [tutorial](http://docs.aws.amazon.com/ElasticMapReduce/latest/DeveloperGuide/emr-kinesis.html) section “Running queries with checkpoints”, the code sample shows a scheduled Hive query that designates a Logical Name for the query and increments the iteration with each successive run of the job.

Additionally, a sample cron scheduling script is provided in the [tutorials](http://docs.aws.amazon.com/ElasticMapReduce/latest/DeveloperGuide/emr-kinesis.html).

**Q: Where is the metadata for Logical Names and Iterations stored?**

The metadata that allows the EMR Kinesis input connector to work in scheduled periodic workflows is stored in Amazon DynamoDB. You must provision an Amazon Dynamo DB table and specify it as an input parameter to the Hadoop Job. It is important that you configure appropriate IOPS for the table to enable this integration. Please refer to the getting started [tutorial](http://docs.aws.amazon.com/ElasticMapReduce/latest/DeveloperGuide/emr-kinesis.html) for more information on setting up your Amazon Dynamo DB table.

**Q: What happens when an iteration processing fails?**

Iterations identifiers are user-provided values that map to specific boundary (start and end sequence numbers) in a Kinesis stream. Data corresponding to these boundaries is loaded in the Map phase of the MapReduce job. This phase is managed by the framework and will be automatically re-run (three times by default) in case of job failure. If all the retries fail, you would still have options to retry the processing starting from last successful data boundary or past data boundaries. This behavior is controlled by providing kinesis.checkpoint.iteration.no parameter during processing. Please refer to the getting started [tutorial](http://docs.aws.amazon.com/ElasticMapReduce/latest/DeveloperGuide/emr-kinesis.html) for more information on how this value is configured for different tools in the Hadoop ecosystem.

**Q: Can I run multiple queries on the same iteration?**

Yes, you can specify a previously run iteration by setting the kinesis.checkpoint.iteration.no parameter in successive processing. The implementation ensures that successive runs on the same iteration will have precisely the same input records from the Kinesis stream as the previous runs.

**Q: What happens if records in an Iteration expire from the Kinesis stream?**

In the event that the beginning sequence number and/or end sequence number of an iteration belong to records that have expired from the Kinesis steam, the Hadoop job will fail. You would need to use a different Logical Name to process data from the beginning of the Kinesis stream.

**Q: Can I push data from EMR into Kinesis stream?**

No. The EMR Kinesis connector currently does not support writing data back into a Kinesis stream.

**Q: Does the EMR Hadoop input connector for Kinesis enable continuous stream processing?**

The Hadoop MapReduce framework is a batch processing system. As such, it does not support continuous queries. However there is an emerging set of Hadoop ecosystem frameworks like Twitter Storm and Spark Streaming that enable to developers build applications for continuous stream processing. A Storm connector for Kinesis is available at on GitHub [here](https://github.com/awslabs/kinesis-storm-spout) and you can find a tutorial explaining how to setup Spark Streaming on EMR and run continuous queries [here](http://aws.amazon.com/articles/4926593393724923).

Additionally, developers can utilize the Kinesis client library to develop real-time stream processing applications. You can find more information on developing custom Kinesis applications in the Kinesis documentation [here](http://docs.aws.amazon.com/kinesis/latest/dev/step-three-build-an-app.html).

**Q: Can I specify access credential to read a Kinesis stream that is managed in another AWS account?**

Yes. You can read streams from another AWS account by specifying the appropriate access credentials of the account that owns the Kinesis stream. By default, the Kinesis connector utilizes the user-supplied access credentials that are specified when the cluster is created. You can override these credentials to access streams from other AWS Accounts by setting the kinesis.accessKey and kinesis.secretKey parameters. The following examples show how to set the kinesis.accessKey and kinesis.secretKey parameters in Hive and Pig.

Code sample for Hive:  
...  
STORED BY  
'com.amazon.emr.kinesis.hive.KinesisStorageHandler'  
TBLPROPERTIES(  
"kinesis.accessKey"="AwsAccessKey",  
"kinesis.secretKey"="AwsSecretKey",  
);

Code sample for Pig:  
…  
raw\_logs = LOAD 'AccessLogStream' USING com.amazon.emr.kinesis.pig.Kin  
esisStreamLoader('kinesis.accessKey=AwsAccessKey', 'kinesis.secretKey=AwsSecretKey'  
) AS (line:chararray);

**Q: Can I run multiple parallel queries on a single Kinesis Stream? Is there a performance impact?**

Yes, a customer can run multiple parallel queries on the same stream by using separate logical names for each query. However, reading from a shard within a Kinesis stream is subjected to a rate limit of 2MB/sec. Thus, if there are N parallel queries running on the same stream, each one would get roughly (2/N) MB/sec egress rate per shard on the stream. This may slow down the processing and in some cases fail the queries as well.

**Q: Can I join and analyze multiple Kinesis streams in EMR?**

Yes, for example in Hive, you can create two tables mapping to two different Kinesis streams and create joins between the tables.

**Q: Does the EMR Kinesis connector handle Kinesis scaling events, such as merge and split events?**

Yes. The implementation handles split and merge events. The Kinesis connector ties individual Kinesis shards (the logical unit of scale within a Kinesis stream) to Hadoop MapReduce map tasks. Each unique shard that exists within a stream in the logical period of an Iteration will result in exactly one map task. In the event of a shard split or merge event, Kinesis will provision new unique shard Ids. As a result, the MapReduce framework will provision more map tasks to read from Kinesis. All of this is transparent to the user.

**Q: What happens if there are periods of “silence” in my stream?**

The implementation allows you to configure a parameter called kinesis.nodata.timeout. For example, consider a scenario where kinesis.nodata.timeout is set to 2 minutes and you want to run a Hive query every 10 minutes. Additionally, consider some data has been written to the stream since the last iteration (10 minutes ago). However, currently no new records are arriving, i.e. there is a silence in the stream. In this case, when the current iteration of the query launches, the Kinesis connector would find that no new records are arriving. The connector will keep polling the stream for 2 minutes and if no records arrive for that interval then it will stop and process only those records that were already read in the current batch of stream. However, if new records start arriving before kinesis.nodata.timeout interval is up, then the connector will wait for an additional interval corresponding to a parameter called kinesis.iteration.timeout. Please look at the [tutorials](http://docs.aws.amazon.com/ElasticMapReduce/latest/DeveloperGuide/emr-kinesis.html) to see how to define these parameters.

**Q: How do I debug a query that continues to fail in each iteration?**

In the event of a processing failure, you can utilize the same tools they currently do when debugging Hadoop Jobs. Including the Amazon EMR web console, which helps identify and access error logs. More details on debugging an EMR job can be found [here](http://docs.aws.amazon.com/ElasticMapReduce/latest/DeveloperGuide/emr-plan-debugging.html).

**Q: What happens if I specify a DynamoDB table that I don’t have access to?**

The job would fail and the exception would show up in error logs for the job.

**Q: What happens if job doesn’t fail but checkpointing to DynamoDB fails?**

The job would fail and the exception would show up in error logs for the job.

**Q: How do I maximize the read throughput from Kinesis stream to EMR?**

Throughput from Kinesis stream increases with instance size used and record size in the Kinesis stream. We recommend that you use m1.xlarge and above for both master and core nodes for this feature.