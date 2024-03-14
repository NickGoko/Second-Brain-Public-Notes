---
tags:
  - cloud
  - cloud/aws
---
**Amazon Kinesis** <mark style="background: #FFB86CA6;">makes it easy to collect, process, and analyze real-time, streaming data so you can get timely insights and react quickly to new information.</mark>

<mark style="background: #FFB8EBA6;">Kinesis is a collection of services for processing streams of various data.</mark>

<mark style="background: #BBFABBA6;">Data is processed in “shards” – with each shard able to ingest 1000 records per second.</mark>

There is a default limit of 500 shards, but you can request an increase to unlimited shards.

A record consists of a partition key, sequence number, and data blob (up to 1 MB).

- <mark style="background: #ADCCFFA6;">Transient data store – default retention of 24 hours but can be configured for up to 7 days.</mark>  
![[Pasted image 20240213142438.png]]

There are four types of Kinesis service, and these are detailed below.

![](https://i.imgur.com/BlBZihR.png)

![[AWS Solutions Architect Skillbuilder#^24ea13]]

![[AWS Solutions Architect Skillbuilder#^fc2c6b]]

![[Serverless Skillbuider#Data Processing with Amazon Kinesis]]


## Kinesis Video Streams

**Kinesis Video Streams** <mark style="background: #ABF7F7A6;">makes it easy to securely stream video from connected devices to AWS for analytics, machine learning (ML), and other processing.</mark>

- Durably stores, encrypts, and indexes video data streams, and allows access to data through easy-to-use APIs.
- Producers provide data streams.
- <mark style="background: #FFB86CA6;">Stores data for 24 hours by default, up to 7 days.</mark>
- Stores data in shards – 5 transaction per second for reads, up to a max read rate of 2MB per second and 1000 records per second for writes up to a max of 1MB per second.
- Consumers receive and process data.
- Can have multiple shards in a stream.
- Supports encryption at rest with server-side encryption (KMS) with a customer master key.

>Kinesis Video Streams does not appear much on AWS exams.

## Kinesis Data Streams

<mark style="background: #BBFABBA6;">Kinesis Data Streams enables you to build custom applications that process or analyze streaming data for specialized needs.</mark>
- <mark style="background: #FFB86CA6;">Kinesis Data Streams enables real-time processing of streaming big data.</mark>
- <mark style="background: #FF5582A6;">Kinesis Data Streams is useful for rapidly moving data off data producers and then continuously processing the data.</mark>
- Kinesis Data Streams **stores data** <mark style="background: #FFF3A3A6;">for later processing by applications</mark> (<mark style="background: #CACFD9A6;">key difference with Firehose which delivers data directly to AWS services</mark>).  
![[Pasted image 20240213142837.png]]

![[Pasted image 20240213142941.png]]  
![[Pasted image 20240213143014.png]]  
![[Pasted image 20240213143040.png]]

Common use cases include:
- <mark style="background: #BBFABBA6;">Accelerated log and data feed intake.</mark>
- <mark style="background: #BBFABBA6;">Real-time metrics and reporting.</mark>
- <mark style="background: #BBFABBA6;">Real-time data analytics.</mark>
- <mark style="background: #BBFABBA6;">Complex stream processing.</mark>

The diagram below illustrates the high-level architecture of Kinesis Data Streams.
- <mark style="background: #ABF7F7A6;">Producers continually push data to Kinesis Data Streams.</mark>
- <mark style="background: #CACFD9A6;">Consumers process the data in real time.</mark>
- <mark style="background: #FFB8EBA6;">Consumers can store their results using an AWS service such as Amazon DynamoDB, Amazon Redshift, or Amazon S3.</mark>
- **Kinesis Streams applications are consumers that run on EC2 instances.**
- <mark style="background: #FFB86CA6;">Shards are uniquely identified groups or data records in a stream.</mark>
- <mark style="background: #FFF3A3A6;">Records are the data units stored in a Kinesis Stream.</mark>

![](https://i.imgur.com/Tkzvsbn.png)

- A producer creates the data that makes up the stream.  
_Producers_ can be used through the following:
- Kinesis Streams API.
- Kinesis Producer Library (KPL).
- Kinesis Agent.

- <mark style="background: #FFF3A3A6;">A record is the unit of data stored in a Amazon Kinesis data stream.</mark>
- <mark style="background: #ABF7F7A6;">A record is composed of a sequence number, partition key, and data blob.</mark>

<mark style="background: #083CA4A6;">By default, records of a stream are accessible for up to 24 hours from the time they are added to the stream (can be raised to 7 days by enabling extended data retention).</mark>

A **data blob** <mark style="background: #FFF3A3A6;">is the data of interest your data producer adds to a data stream</mark>.  
<mark style="background: #CACFD9A6;">The maximum size of a data blob (the data payload before Base64-encoding) within one record is 1 megabyte (MB).</mark>

A **shard** is the <mark style="background: #FF5582A6;">base throughput unit of an Amazon Kinesis data stream</mark>.  
<mark style="background: #D2B3FFA6;">One shard provides a capacity of 1MB/sec data input and 2MB/sec data output.</mark>  
Each shard can support up to 1000 PUT records per second.

<mark style="background: #FFB86CA6;">A stream is composed of one or more shards.</mark>

<mark style="background: #FF5582A6;">The total capacity of the stream is the sum of the capacities of its shards.</mark>

<mark style="background: #ADCCFFA6;">Kinesis Data Streams supports resharding, which lets you adjust the number of shards in your stream to adapt to changes in the rate of data flow through the stream.</mark>

There are two types of resharding operations: _shard split_ and _shard merge_.
- <mark style="background: #083CA4A6;">In a shard split, you divide a single shard into two shards.</mark>
- In a <mark style="background: #083CA4A6;">shard merge, you combine two shards into a single shard.</mark>

![](https://i.imgur.com/5xbjd1p.png)

<mark style="background: #CACFD9A6;">Splitting increases the number of shards in your stream and therefore increases the data capacity of the stream.</mark>  
Splitting increases the cost of your stream (you pay per-shard).

<mark style="background: #CACFD9A6;">Merging reduces the number of shards in your stream and therefore decreases the data capacity—and cost—of the stream.</mark>

<mark style="background: #ADCCFFA6;">Consumers are the EC2 instances that analyze the data received from a stream.</mark>  
<mark style="background: #D2B3FFA6;">Consumers are known as Amazon Kinesis Streams Applications.</mark>

<mark style="background: #FFB8EBA6;">When the data rate increases, add more shards to increase the size of the stream. </mark>  
Remove shards when the data rate decreases.

<mark style="background: #FFF3A3A6;">Partition keys are used to group data by shard within a stream.</mark>

<mark style="background: #D2B3FFA6;">Kinesis Streams uses KMS master keys for encryption.  
To read from or write to an encrypted stream the producer and consumer applications must have permission to access the master key.</mark>  

<mark style="background: #BBFABBA6;">Kinesis Data Streams replicates synchronously across three AZs.</mark>

## Kinesis Data Firehose
<mark style="background: #D2B3FFA6;">Kinesis Data Firehose is the easiest way to load streaming data into data stores and analytics tools.</mark>  
![[Pasted image 20240213143456.png]]
- <mark style="background: #FFB86CA6;">Captures, transforms, and loads streaming data.</mark>
- Enables <mark style="background: #ABF7F7A6;">near real-time analytics</mark> with existing business intelligence tools and dashboards.
- <mark style="background: #BBFABBA6;">Kinesis Data Streams can be used as the source(s) to Kinesis Data Firehose.</mark>
- <mark style="background: #083CA4A6;">You can configure Kinesis Data Firehose to transform your data before delivering it.</mark>
- <mark style="background: #ADCCFFA6;">With Kinesis Data Firehose you don’t need to write an application or manage resources.</mark>
- <mark style="background: #FFF3A3A6;">Firehose can batch, compress, and encrypt data before loading it.</mark>
- <mark style="background: #FFB8EBA6;">Firehose synchronously replicates data across three AZs as it is transported to destinations.</mark>
- Each delivery stream stores data records for up to 24 hours.
	- A _source_ is where your streaming data is continuously generated and captured.
	- A _delivery stream_ is the underlying entity of Amazon Kinesis Data Firehose.
	- A _record_ is ==the data of interest your data producer sends to a delivery stream.==
	- The maximum size of a record (before Base64-encoding) is 1000 KB.
	- A _destination_ is the data store where your data will be delivered.  
	  

<mark style="background: #FFB86CA6;">Firehose Destinations</mark> include:
- **Amazon S3.**
- _Amazon Redshift._
- _Amazon Elasticsearch Service_.
- _Splunk_.  
  
![[Pasted image 20240213143726.png]]
- Producers provide data streams.
- <mark style="background: #BBFABBA6;">No shards, totally automated.</mark>
- <mark style="background: #CACFD9A6;">Can encrypt data with an existing AWS Key Management Service (KMS) key.</mark>
- <mark style="background: #FF5582A6;">Server-side-encryption can be used if Kinesis Streams is used as the data source.</mark>

- <mark style="background: #083CA4A6;">Firehose can invoke an AWS Lambda function to transform incoming data before delivering it to a destination.</mark>

- _For Amazon S3 destinations_, <mark style="background: #FFF3A3A6;">streaming data is delivered to your S3 bucket. If data transformation is enabled, you can optionally back up source data to another Amazon S3 bucket: </mark>  
![](https://i.imgur.com/Ucr28LZ.png)  

- For Amazon Redshift destinations, <mark style="background: #ADCCFFA6;">streaming data is delivered to your S3 bucket first</mark>.  
	**Kinesis Data Firehose** <mark style="background: #CACFD9A6;">then issues an Amazon Redshift</mark> **COPY** <mark style="background: #ADCCFFA6;">command to load data from your S3 bucket to your Amazon Redshift cluster.</mark>  

If data transformation is enabled, you can optionally back up source data to another Amazon S3 bucket:  
![](https://i.imgur.com/Xi8dsIA.png)  


For **Amazon ElasticSearch** destinations, <mark style="background: #FFF3A3A6;">streaming data is delivered to your Amazon ES cluster, and it can optionally be backed up to your S3 bucket concurrently</mark>:  
![](https://i.imgur.com/4dZZo7a.png)


_For Splunk destinations_, streaming data is delivered to Splunk, and it can optionally be backed up to your S3 bucket concurrently:  
![](https://i.imgur.com/6UKQc1z.png)


![](https://i.imgur.com/sCfzuNz.png)

## Kinesis Data Analytics
**Amazon Kinesis Data Analytics** is the <mark style="background: #FFF3A3A6;">easiest way to process and analyze real-time, streaming data</mark>.
- Can use standard SQL queries to process Kinesis data streams.
- Provides real-time analysis.

Use cases:
- <mark style="background: #FFB8EBA6;">Generate time-series analytics</mark>.
- <mark style="background: #FFB8EBA6;">Feed real-time dashboards</mark>.
- <mark style="background: #FFB8EBA6;">Create real-time alerts and notifications</mark>.

<mark style="background: #ADCCFFA6;">Quickly author and run powerful SQL code against streaming sources.</mark>

><mark style="background: #BBFABBA6;">Can ingest data from Kinesis Streams and Kinesis Firehose.</mark>

> <mark style="background: #D2B3FFA6;">Output to S3, RedShift, Elasticsearch and Kinesis Data Streams</mark>.

<mark style="background: #CACFD9A6;">Sits over Kinesis Data Streams and Kinesis Data Firehose</mark>.

<mark style="background: #FFB86CA6;">A Kinesis Data Analytics application consists of three components</mark>:
- **Input** – <mark style="background: #BBFABBA6;">the streaming source for your application</mark>.
- **Application code** – <mark style="background: #BBFABBA6;">a series of SQL statements that process input and produce output</mark>.
- **Output** – one or more in-application streams to hold intermediate results.

<mark style="background: #ADCCFFA6;">Kinesis Data Analytics supports two types of inputs</mark>: **streaming data sources** and **reference data sources**:

- <mark style="background: #FFF3A3A6;">A streaming data source is continuously generated data that is read into your application for processing</mark>.
- <mark style="background: #FF5582A6;">A reference data source is static data that your application uses to enrich data coming in from streaming sources.</mark>

Can configure destinations to persist the results.

<mark style="background: #FF5582A6;">Supports Kinesis Streams and Kinesis Firehose (S3, RedShift, Elasticsearch) as destinations.</mark>

IAM can be used to provide Kinesis Analytics with permissions to read records from sources and write to destinations.  
![](https://i.imgur.com/YhmwpHZ.png)  
![](https://i.imgur.com/SCC27wE.png)  
![](https://i.imgur.com/ZGqwIzd.png)

## Kinesis Client Library
**Kinesis Client Library** is a Java library that helps read records from a Kinesis Stream with distributed applications sharing the read workload.

The KCL is different from the Kinesis Data Streams API that is available in the AWS SDKs.

- The Kinesis Data Streams API helps you <mark style="background: #CACFD9A6;">manage many aspects of Kinesis Data Streams (including</mark> <mark style="background: #BBFABBA6;">creating streams, resharding, and putting and getting records</mark>).
- The KCL <mark style="background: #CACFD9A6;">provides a layer of abstraction specifically for processing data in a consumer role</mark>.  
![](https://i.imgur.com/12QGHzC.png)  

The KCL <mark style="background: #FFB86CA6;">acts as an intermediary between your record processing logic and Kinesis Data Streams.</mark>

When you start a KCL application, it calls the KCL to instantiate a worker. The KCL performs the following tasks:
- Connects to the stream.
- <mark style="background: #CACFD9A6;">Enumerates the shards</mark>.
- Coordinates shard associations with other workers (if any).
- Instantiates a record processor for every shard it manages.
- <mark style="background: #CACFD9A6;">Pulls data records from the stream</mark>.
- Pushes the records to the corresponding record processor.
- Checkpoints processed records.
- Balances shard-worker associations when the worker instance count changes.
- Balances shard-worker associations when shards are split or merged.

The KCL ensures that for every shard there is a record processor.

Manages the number of record processors relative to the number of shards & consumers.

If you have only one consumer, the KCL will create all the record processors on a single consumer.

Each shard is processed by exactly one KCL worker and has exactly one corresponding record processor, so you never need multiple instances to process one shard.

However, one worker can process any number of shards, so it’s fine if the number of shards exceeds the number of instances.  
![](https://i.imgur.com/MhLKLyj.png)  
If you have two consumers it will load balance and create half the processors on one instance and half on another.

Scaling out consumers:

- With KCL, generally you should ensure that the number of instances does not exceed the number of shards (except for failure or standby purposes).
- Each shard can be read by only one KCL instance.
- You never need multiple instances to handle the processing of one shard.

However, one worker can process multiple shards.

Example:

- 4 shards = max 4 KCL instances.
- 6 shards = max 6 KCL instances.

Progress is checkpointed into DynamoDB (IAM access required).

KCL can run on EC2, Elastic Beanstalk, and on-premises servers.

Records are read in order at the shard level.
## Security

Control access / authorization using IAM policies.

Encryption in flight using HTTPS endpoints.

Encryption at rest using KMS.

Possible to encrypt / decrypt data on the client side.

VPC endpoints available for Kinesis to access within a VPC.

## SQS Vs SNS Vs Kinesis

SQS:
- Consumers pull data.
- <mark style="background: #CACFD9A6;">Data is deleted after being consumed</mark>.
- Can have as many workers (consumers) as you need.
- <mark style="background: #CACFD9A6;">No need to provision throughput.</mark>
- <mark style="background: #CACFD9A6;">No ordering guarantee (except with FIFO queues)</mark>.
- Individual message delay.

SNS:
- <mark style="background: #CACFD9A6;">Push data to many subscribers</mark>.
- Up to 12,500,000 subscribers.
- Data is not persisted (lost if not deleted).
- Pub/sub.
- <mark style="background: #FFB8EBA6;">Up to 10,000,000 topics.</mark>
- No need to provision throughput.
- Integrates with SQS for fan-out architecture pattern.

Kinesis:
- <mark style="background: #CACFD9A6;">Consumers pull data.</mark>
- <mark style="background: #FFF3A3A6;">As many consumers as you need.</mark>
- Possible to replay data.
- <mark style="background: #CACFD9A6;">Meant for real-time big data, analytics, and ETL.</mark>
- <mark style="background: #BBFABBA6;">Ordering at the shard level.</mark>
- Data expires after X days.
- Must provision throughput.  
![[Pasted image 20240214002938.png]]

![[Pasted image 20240214002309.png]]  
![[Pasted image 20240214002712.png]]  
![[Pasted image 20240214002756.png]]
