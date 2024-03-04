---
tags:
  - cloud/aws
---
![[Pasted image 20240214151804.png]]  
![](https://i.imgur.com/HtIMl0X.png)

![](https://i.imgur.com/ySIfIbP.png)

![](https://i.imgur.com/G5nLP2N.png)

![](https://i.imgur.com/KZobRHK.png)

![](https://i.imgur.com/hdtU2cL.png)

![](https://i.imgur.com/GmwC3ZG.png)

![](https://i.imgur.com/ZtuBwBK.png)

![](https://i.imgur.com/ysTtCyU.jpeg)

![[Pasted image 20240229211338.png]]








![[Module 11 - Caching Content#Amazon ElastiCache]]


![[AWS Solutions Architect Skillbuilder#Use Case 2]]

# FAQ
## General

[The basics](https://aws.amazon.com/elasticache/faqs//#The_Basics) | [Serverless](https://aws.amazon.com/elasticache/faqs//#Serverless) | [Reserved Nodes](https://aws.amazon.com/elasticache/faqs//#Reserved_Nodes) | [Security](https://aws.amazon.com/elasticache/faqs//#Security) | [Compliance](https://aws.amazon.com/elasticache/faqs//#Compliance) | [Parameter groups](https://aws.amazon.com/elasticache/faqs//#Parameter_Groups)

### The Basics

**Q: What is Amazon ElastiCache?**  
Amazon ElastiCache is <mark style="background: #ADCCFFA6;">a web service that streamlines deployment and running of Memcached or Redis protocol-compliant caches</mark> in [the cloud](https://aws.amazon.com/what-is-cloud-computing/).  
ElastiCache improves application performance by allowing you to retrieve information from a fast, managed, in-memory system instead of relying on slower disk-based systems.  
<mark style="background: #FFF3A3A6;">The service simplifies and offloads the management, monitoring, and operation of in-memory environments, enabling your engineering resources to focus on developing applications.</mark>  
Using ElastiCache, you can not only improve load and response times to user actions and queries but also reduce the cost associated with scaling web applications.

ElastiCache automates common administrative tasks required to operate a distributed in-memory key-value environment. Using ElastiCache, you can add a caching or in-memory layer to your application architecture in a matter of minutes with a few steps in the AWS Management Console. E<mark style="background: #ADCCFFA6;">lastiCache is designed to automatically maintain high availability, and provides a 99.99% availability Service Level Agreement (SLA).</mark>  
ElastiCache is protocol compliant with Memcached and Redis, so code, applications, and popular tools that you use today with your existing Memcached or Redis environments will seamlessly work with the service. There are no up-front investments required, and you pay only for the resources you use.

**Q: What is in-memory caching and how does it help my applications?**  
<mark style="background: #083CA4A6;">The in-memory caching provided by ElastiCache can be used to significantly improve latency and throughput for many read-heavy application workloads (such as social networking, gaming, media sharing, and Q&A portals) or compute-intensive workloads (such as a recommendation engine).</mark>  
In-memory caching improves application performance by storing critical pieces of data in memory for low-latency access. Cached information can include the results of I/O-intensive database queries or the results of computationally intensive calculations.  
  
**Q: What does ElastiCache manage on my behalf?**  
- <mark style="background: #FFF3A3A6;">ElastiCache manages the work involved in setting up a distributed in-memory environment, from provisioning the resources you request to installing the software.</mark> 
- When using Amazon ElastiCache Serverless, there is no infrastructure that you need to configure and manage. 
- When designing your own ElastiCache cluster, the service automates common administrative tasks such as software patching and failure detection and recovery. 
- ElastiCache provides detailed monitoring metrics associated with your resources, allowing you to quickly diagnose and react to issues. For example, you can set up thresholds and receive alarms if one of your caches is overloaded with requests.

**Q: Which engines does ElastiCache support?**  
ElastiCache offers fully managed <mark style="background: #FFF3A3A6;">Redis and Memcached</mark> for your most demanding applications that require submillisecond response times.

**Q: How do I get started with ElastiCache?**  
If you are not already signed up for ElastiCache, you can select Get started on the [ElastiCache page](https://aws.amazon.com/elasticache/) and complete the sign-up process. You must have an AWS account; if you do not already have one, you will be prompted to create one when you begin the ElastiCache sign-up process. After you are signed up for ElastiCache, please refer to the [ElastiCache documentation](https://aws.amazon.com/documentation/elasticache/), which includes the Getting Started Guides for [Amazon ElastiCache for Redis](https://docs.aws.amazon.com/AmazonElastiCache/latest/red-ug/GettingStarted.html) or [Amazon ElastiCache for Memcached](https://docs.aws.amazon.com/AmazonElastiCache/latest/mem-ug/GettingStarted.html).

Once you have familiarized yourself with ElastiCache, you can create a cache within minutes by using the [console](http://console.aws.amazon.com/elasticache/home) or ElastiCache APIs.

**Q: How do I create a cache?**  
Caches are simple to create, using the [console](http://console.aws.amazon.com/elasticache/home), ElastiCache APIs, or command line tools. When using ElastiCache Serverless, you can create a cache using the default recommended settings and begin using it in under a minute.

### Serverless

**Q: What is ElastiCache Serverless?**  
<mark style="background: #FFF3A3A6;">ElastiCache Serverless is a serverless option that lets you get started with a cache in under a minute without infrastructure provisioning or capacity planning</mark>.  
<mark style="background: #ADCCFFA6;">ElastiCache Serverless removes the need for time-consuming capacity planning by continuously monitoring a cache’s compute, memory, and network utilization, so it can instantly scale to meet demand without downtime or performance degradation. </mark>  
ElastiCache Serverless automatically replicates data across multiple Availability Zones (AZs) and provides customers with a 99.99% availability service level agreement (SLA) for each cache.  
With ElastiCache Serverless, you only pay for the data you store and the compute resources your application uses. To get started, create an ElastiCache Serverless cache in just a few steps by specifying a cache name using the [console](http://console.aws.amazon.com/elasticache/home), ElastiCache Development Kit (SDK), or AWS Command Line Interface (AWS CLI).

**Q: How do I migrate an existing ElastiCache workload to ElastiCache Serverless?**  
<mark style="background: #FFF3A3A6;">You can move an existing ElastiCache workload by changing the Redis or Memcached endpoint to your new ElastiCache Serverless cache endpoint in your application</mark>. You can migrate existing ElastiCache data to ElastiCache Serverless by specifying the Amazon Simple Storage Service (Amazon S3) location of a backup file. Visit our ElastiCache Serverless documentation to learn more about migrating your workloads.

**Q: Which versions of Redis and Memcached does ElastiCache Serverless support?**  
ElastiCache Serverless supports ElastiCache for Redis version 7.1 and ElastiCache for Memcached version 1.6.21 and above.

**Q: How does ElastiCache Serverless scale?**  
ElastiCache Serverless continuously monitors your cache’s memory, compute, and network utilization to instantly scale. ElastiCache Serverless scales without downtime or performance degradation to the application by allowing the cache to scale up and initiating scale-out in parallel, to meet application requirements just in time. Visit our ElastiCache Serverless documentation to learn more about scaling.

**Q: What is the ElastiCache Serverless availability Service Level Agreement (SLA)?**  
ElastiCache Serverless automatically stores data redundantly across multiple AZs and provides a 99.99% availability [Service Level Agreement (SLA)](https://aws.amazon.com/elasticache/sla/) for all workloads.

**Q: What is ElastiCache Serverless pricing?**  
With ElastiCache Serverless, you only pay for the data you store and the compute your application uses. Visit the [ElastiCache pricing page](https://aws.amazon.com/elasticache/pricing) to learn more.

### Reserved Nodes

**Q: What are ElastiCache Reserved Nodes?**  
Reserved Nodes or Reserved Instances (RIs) provide you with a significant discount over on-demand usage when you commit to a one-year or three-year term.  
With Reserved Nodes, you can make a one-time, up-front payment to create a one or three-year reservation to run your cache in a specific Region and receive a significant discount off the ongoing hourly usage charge.  
There are three _Reserved Node types_ – <mark style="background: #FFB86CA6;">All Upfront</mark>, <mark style="background: #FFB86CA6;">No Upfront</mark>, and <mark style="background: #FFB86CA6;">Partial Upfront</mark> – that allow you to balance the amount you pay upfront with your effective hourly price.

**Q: Do Reserved Nodes apply to ElastiCache Serverless?**  
Reserved Nodes provide a discount that applies to ElastiCache on-demand usage. <mark style="background: #ADCCFFA6;">ElastiCache Serverless is not compatible with Reserved Nodes.</mark>

**Q: How many Reserved Nodes can I purchase?**  
You can purchase up to 300 Reserved Nodes. If you wish to run more than 300 nodes, please complete the [ElastiCache node request form](http://aws.amazon.com/contact-us/elasticache-node-limit-request/).

**Q: What if I have an existing node that I’d like to convert to a Reserved Node?**  
Purchase a node reservation with the same node class within the same Region as the node you are currently running and would like to reserve. If the reservation purchase is successful, ElastiCache will automatically apply your new hourly usage charge to your existing node.

**Q: If I sign up for a Reserved Node, when does the term begin? What happens to my node when the term ends?**  
Pricing changes associated with a Reserved Node are activated once your request is received and while the payment authorization is processed. You can follow the status of your reservation on the AWS Account Activity page or by using the DescribeReservedCacheNodes API. If the one-time payment cannot be successfully authorized by the next billing period, the discounted price will not take effect.

When your reservation term expires, your Reserved Node will revert to the appropriate On-Demand hourly usage rate for your node class and Region.

**Q: How do I control which nodes are billed at the Reserved Node rate?**  
The ElastiCache APIs to create, modify, and delete nodes do not distinguish between On-Demand and Reserved Nodes, so that you can seamlessly use both. When computing your bill, our system will automatically apply your reservations, such that all eligible nodes are charged at the lower hourly Reserved Cache Node rate.

**Q: Can I move a Reserved Node from one Region or AZ to another?**  
Each Reserved Node is associated with a specific Region, which is fixed for the lifetime of the reservation and cannot be changed. Each reservation can, however, be used in any of the available AZs within the associated Region.

**Q: Can I cancel a reservation?**  
No. You cannot cancel your node reservation, and the one-time payment (if applicable) is not refundable. You will continue to pay for every hour during your Reserved Node term regardless of your usage.

**Q: How do the payment options impact my bill?**  
When you purchase a Reserved Node under the All Upfront payment option, you pay for the entire term of the Reserved Node in one upfront payment. You can choose to pay nothing upfront by choosing the No Upfront option. The entire value of the No Upfront Reserved Node is spread across every hour in the term and you will be billed for every hour in the term, regardless of usage. The Partial Upfront payment option is a hybrid of the All Upfront and No Upfront options. You make a small upfront payment, and you are billed a low hourly rate for every hour in the term regardless of usage.

### Security

**Q: What security controls exist for ElastiCache?**  
<mark style="background: #FFB86CA6;">ElastiCache allows you to configure encryption of data at rest using AWS Key Management Service (AWS KMS)</mark>, <mark style="background: #FFF3A3A6;">encryption of data in transit using Transport Layer Security (TLS)</mark>, <mark style="background: #FFB8EBA6;">authentication using AWS Identity and Access Management (IAM)</mark>, and <mark style="background: #ABF7F7A6;">network access control with Amazon Elastic Compute Cloud (Amazon EC2) security groups.</mark>

**Q: How do I control access to ElastiCache?**  
When not using [Amazon Virtual Private Cloud](http://docs.amazonwebservices.com/AmazonVPC/latest/UserGuide/VPC_Introduction.html) (Amazon VPC), ElastiCache allows you to control access to your caches through network security groups.  
A security group acts like a firewall, controlling network access to your cache. By default, network access is turned off to your caches.  
If you want your applications to access your cache, you must explicitly enable access from hosts in specific [Amazon EC2 security groups](http://docs.amazonwebservices.com/AWSEC2/latest/UserGuide/using-network-security.html).

You can also control access to your ElastiCache resources using IAM authentication. For more information, see the [authenticating with IAM documentation](https://docs.aws.amazon.com/AmazonElastiCache/latest/red-ug/auth-iam.html).

### Compliance

**Q: Which compliance programs does ElastiCache support?**  
ElastiCache supports compliance programs such as SOC 1, SOC 2, SOC 3, ISO, MTCS, C5, PCI DSS, HIPAA, and FedRAMP. See [AWS Services in Scope by Compliance Program](https://aws.amazon.com/compliance/services-in-scope/) for a current list of supported compliance programs.

**Q: Is ElastiCache PCI DSS compliant?**  
Yes, the AWS PCI compliance program includes ElastiCache as a PCI-compliant service. To learn more, see the following resources:

- [ElastiCache for Redis Compliance  
    ](https://docs.aws.amazon.com/AmazonElastiCache/latest/red-ug/elasticache-compliance.html)
- [AWS PCI Compliance page](https://aws.amazon.com/compliance/pci-dss-level-1-faqs/)

To see the current list of compliance programs that ElastiCache is in scope for, see [AWS Services in Scope by Compliance Program](https://aws.amazon.com/compliance/services-in-scope/).

**Q: Is ElastiCache HIPAA eligible?**  
Yes, ElastiCache is a [HIPAA-eligible service](https://aws.amazon.com/compliance/hipaa-eligible-services-reference/) and is covered under the [AWS Business Associate Addendum (BAA)](https://aws.amazon.com/compliance/hipaa-compliance/). This means you can use ElastiCache to help you process, maintain, and store protected health information (PHI) and power healthcare applications.

**Q: What do I have to do to use HIPAA-eligible ElastiCache?**  
If you have an executed [Business Associate Agreement (BAA)](https://aws.amazon.com/compliance/hipaa-compliance/) with AWS, you can use ElastiCache to build applications that store and process HI under HIPAA. If you do not have a BAA, or have other questions about using AWS for your applications, [contact us](https://aws.amazon.com/contact-us/) for more information. 

**Q: Is ElastiCache FedRAMP authorized?**  
The AWS FedRAMP compliance program includes ElastiCache Redis as a FedRAMP-authorized service. U.S. government customers and their partners can now use the latest version of ElastiCache to process and store their FedRAMP systems, data, and mission-critical, high-impact workloads in the AWS GovCloud (US-East) and AWS GovCloud (US-West) Regions, and at moderate-level impact in the US East (Ohio), US East (N. Virginia), US West (N. California), and US West (Oregon) Regions.

To learn more, see the following resources:

- [ElastiCache for Redis Compliance](https://docs.aws.amazon.com/AmazonElastiCache/latest/red-ug/elasticache-compliance.html)
- [AWS FedRAMP Compliance](https://aws.amazon.com/compliance/fedramp/)

To see the current list of compliance programs that ElastiCache is in scope for, see [AWS Services in Scope by Compliance Program](https://aws.amazon.com/compliance/services-in-scope/).

**Q: Does it cost extra to use compliance features?**  
No, there is no additional cost for using compliance features.

### Parameter Groups

**Q: What are parameter groups? How are they helpful?**  
A parameter group acts as a container for engine configuration values that can be applied to one or more clusters. If you create a cluster without specifying a parameter group, a default parameter group is used. This default group contains engine defaults and ElastiCache system defaults optimized for the cluster you are running. However, if you want your cache to run with your custom-specified engine configuration values, you can create a new parameter group, modify the desired parameters, and modify the cluster to use the new parameter group. Once associated, all clusters that use a particular parameter group get all the parameter updates to that parameter group. For more information on configuring parameter groups, please refer to the [ElastiCache for Redis](https://docs.aws.amazon.com/AmazonElastiCache/latest/red-ug/ParameterGroups.Modifying.html) or [ElastiCache for Memcached](https://docs.aws.amazon.com/AmazonElastiCache/latest/mem-ug/ParameterGroups.Modifying.html) User Guide.

**Q: How do I choose the right configuration parameters for my caches?**  
ElastiCache by default chooses the optimal configuration parameters for your cache, taking into account the node type's memory and compute resource capacity. However, if you want to change them, you can do so using our configuration management APIs. Please note that changing configuration parameters from recommended values can have unintended effects, ranging from degraded performance to system crashes, and should only be attempted by advanced users who wish to assume these risks. For more information on changing parameters, please refer to the [ElastiCache User Guide](https://docs.aws.amazon.com/AmazonElastiCache/latest/mem-ug/ParameterGroups.Modifying.html).

**Q: How do I see the current setting for my parameters for a given parameter group?**  
You can use the [console](https://console.aws.amazon.com/), ElastiCache APIs, or command line tools to see information about your parameter groups and their corresponding parameter settings.

## Redis

[Redis features](https://aws.amazon.com/elasticache/faqs/#Redis_features) | [Performance](https://aws.amazon.com/elasticache/faqs/#Performance) | [Read replica](https://aws.amazon.com/elasticache/faqs/#Read_replica) | [Multi-AZ](https://aws.amazon.com/elasticache/faqs/#Multi-AZ) | [Backup and restore](https://aws.amazon.com/elasticache/faqs/#Backup_and_restore) | [Enhanced engine](https://aws.amazon.com/elasticache/faqs/#Enhanced_Engine) | [Encryption](https://aws.amazon.com/elasticache/faqs/#Encryption) | [Global Datastore](https://aws.amazon.com/elasticache/faqs/#Global_Datastore) | [Data tiering](https://aws.amazon.com/elasticache/faqs/#Data_tiering)[](https://aws.amazon.com/elasticache/faqs/#Multi-AZ)

### Redis Features

**Q: What is ElastiCache for Redis?**  
ElastiCache for Redis is a web service that streamlines deployment and running of Redis protocol-compliant caches in the cloud. The service enables the management, monitoring, and operation of Redis nodes; creation, deletion, and modification of the nodes can be carried out through the ElastiCache console, the AWS CLI, or the web service APIs. ElastiCache for Redis supports high-availability configurations, including Redis cluster mode enabled and cluster mode disabled with auto-failover from primary to replica.

**Q: Is ElastiCache for Redis protocol compliant with open source Redis?**  
Yes, ElastiCache for Redis is designed to be protocol compliant with open source Redis. Code, applications, drivers, and tools you use today with your existing standalone Redis data store will continue to work with ElastiCache for Redis and no code changes will be required for existing Redis deployments migrating to ElastiCache for Redis unless noted.

**Q: How much does ElastiCache for Redis cost?**  
Please see our [pricing](https://aws.amazon.com/elasticache/pricing/) for current pricing information.

**Q: Does ElastiCache for Redis support Multi-AZ operation?**  
Yes. With ElastiCache for Redis you can create a read replica in another AWS AZ. When using ElastiCache Serverless for Redis, data is automatically stored redundantly across multiple AZs for high availability. When designing your own ElastiCache for Redis cache, upon failure of a node, we will provision a new node. In scenarios where the primary node fails, ElastiCache for Redis will automatically promote an existing read replica to the primary role. For more details on how to handle node failures, visit [understanding Redis replication](https://docs.aws.amazon.com/AmazonElastiCache/latest/red-ug/Replication.Redis.Groups.html).

**Q: How do I upgrade to a newer engine version?**  
You can quickly upgrade to a newer engine version by using the ElastiCache APIs and specifying your preferred engine version. In the ElastiCache console, you can select a cache and select Modify. The engine upgrade process is designed to retain your existing data. For more details, see [caching strategies and best practices](https://docs.aws.amazon.com/AmazonElastiCache/latest/red-ug/BestPractices.html).

**Q: Can I downgrade to an earlier engine version?**  
No, downgrading to an earlier engine version is not supported.

**Q: Can I have cross-Region replicas with ElastiCache for Redis?**  
Yes. You can create cross-Region replicas using the [Global Datastore](https://docs.aws.amazon.com/AmazonElastiCache/latest/red-ug/Redis-Global-Datastore.html) feature in ElastiCache for Redis. Global Datastore provides fully managed, fast, reliable, and security-focused cross-Region replication. It allows you to write to your ElastiCache for Redis cluster in one Region and have the data available to be read from up to two other cross-Region replica clusters, thereby enabling low-latency reads and disaster recovery across Regions.

### Performance

**Q: What are the performance benefits of ElastiCache for Redis?**  
ElastiCache for Redis provides enhanced I/O threads that deliver significant improvements to throughput and latency at scale through multiplexing, presentation layer offloading, and more. Enhanced I/O threads improve performance by using more cores for processing I/O and dynamically adjusting to the workload. ElastiCache for Redis improves the throughput of TLS-enabled clusters by offloading encryption to the same enhanced I/O threads. ElastiCache for Redis version 7.0 introduced enhanced I/O multiplexing, that combines many client requests into a single channel and improves the main Redis thread efficiency.

In [ElastiCache for Redis version 7.1](https://aws.amazon.com/blogs/database/achieve-over-500-million-requests-per-second-per-cluster-with-amazon-elasticache-for-redis-7-1/) and above, we extended the enhanced I/O threads functionality to also handle the presentation layer logic. Enhanced I/O threads not only read client input, but also parses the input into a Redis binary command format, which is then forwarded to the main thread for execution, to provide performance gains. With ElastiCache for Redis version 7.1, you can achieve up to 100% more throughput and 50% lower P99 latency, compared to ElastiCache for Redis version 7.0. On r7g.4xlarge or larger, you can achieve over 1 million requests per second (RPS) per node.

**Q: How do I monitor Redis CPU utilization?**  
ElastiCache provides two different sets of metrics to measure the CPU utilization of your cache depending on your cache deployment choice. When using ElastiCache Serverless, you can monitor the CPU utilization with the ElastiCache Processing Units (ECPU) metric. The number of ECPUs consumed by your requests depends on the vCPU time taken and the amount of data transferred. Each read and write, like the Redis GET and SET commands or the Memcached get and set commands, requires 1 ECPU for each kilobyte (KB) of data transferred. Some Redis commands that operate on in-memory data structures can consume more vCPU time than a GET or SET command. ElastiCache calculates the number of ECPUs consumed based on the vCPU time taken by the command compared to a baseline of the vCPU time taken by a Redis SET or GET command. If your command takes additional vCPU time and transfers more data than the baseline of 1 ECPU, then ElastiCache calculates the ECPUs required based on the higher of the two dimensions.

When designing your own cluster, you can monitor EngineCPUUtilization and CPUUtilization. The CPUUtilization metric measures the CPU utilization for the instance (node), and the EngineCPUUtilization metric measures the utilization at the Redis process level. You need the EngineCPUUtilization metric in addition to the CPUUtilization metric, as the main Redis process is single threaded and uses just one CPU of the multiple CPU cores available on an instance. Therefore, the CPUUtilization metric does not provide precise visibility into the CPU utilization rates at the Redis process level. We recommend that you use both the CPUUtilization and EngineCPUUtilization metrics together to get a detailed understanding of CPU utilization for your Redis clusters.

Both sets of metrics are available in all AWS Regions, and you can access these metrics using Amazon CloudWatch or in the [console](https://console.aws.amazon.com/elasticache/). Additionally, we recommend that you visit [the documentation](https://docs.aws.amazon.com/AmazonElastiCache/latest/red-ug/CacheMetrics.WhichShouldIMonitor.html) to learn about useful metrics for performance monitoring.

**Q: How do I optimize Redis client performance?**  
Redis is one of the most popular NoSQL key-value stores and is known for its great performance. In order to optimize the usage of Redis, you also need a performant client.

### Read Replica

**Q: What does it mean to run a Redis node as a read replica?**  
Read replicas serve two purposes in Redis:

- Failure handling
- Read scaling

When you run a cache with a read replica, the primary serves both writes and reads. The replica serves exclusively read traffic and is also available as a warm standby in the event that the primary becomes impaired.

**Q: When would I want to consider using a Redis read replica?**  
With ElastiCache Serverless, read replicas are automatically maintained by the service. When designing your own cache, there are a variety of scenarios where deploying one or more read replicas for a given primary node might make sense. Common reasons for deploying a read replica include:

- Scaling beyond the compute or I/O capacity of a single primary node for read-heavy workloads: This excess read traffic can be directed to one or more read replicas.
- Serving read traffic while the primary is unavailable: If your primary node cannot take I/O requests (for example, due to I/O suspension for backups or scheduled maintenance), you can direct read traffic to your read replicas. For this use case, keep in mind that the data on the read replica might be stale, since the primary instance is unavailable. The read replica can also be used warmed up to restart a failed primary.
- Data protection scenarios: In the unlikely event of primary node failure or that the AZ in which your primary node resides becomes unavailable, you can promote a read replica in a different AZ to become the new primary. 

**Q: How do I connect to my read replicas?**

You can connect to a read replica just as you would connect to a primary cache node. If you have multiple read replicas, it is up to your application to determine how read traffic will be distributed amongst them. Here are more details:

- Redis (cluster mode disabled) clusters, use the individual node endpoints for read operations. (In the API/CLI these are referred to as read endpoints.)
- Redis (cluster mode enabled) clusters, use the cluster's configuration endpoint for all operations. You must use a client that supports Redis Cluster (Redis 3.2). You can still read from individual node endpoints. (In the API and CLI these are referred to as read endpoints.)

**Q: How many read replicas can I create for a given primary node?**  
ElastiCache allows you to create up to five (5) read replicas for a given primary cache node.

**Q: What happens to read replicas if failover occurs?**  
In the event of a failover, any associated and available read replicas should automatically resume replication once failover has completed (acquiring updates from the newly promoted read replica).

**Q: How does ElastiCache keep my read replica up-to-date with its primary node?**  
Updates to a primary cache node will automatically be replicated to any associated read replicas. However, with Redis’ asynchronous replication technology, a read replica can fall behind its primary cache node for a variety of reasons. Typical reasons include:

- Write I/O volume to the primary cache node exceeds the rate at which changes can be applied to the read replica.
- Network partitions or latency between the primary cache node and a read replica.

Read replicas are subject to the strengths and weaknesses of Redis replication. If you are using read replicas, you should be aware of the potential for lag between a read replica and its primary cache node or “inconsistency.” ElastiCache [emits a metric](https://docs.aws.amazon.com/AmazonElastiCache/latest/red-ug/CacheMetrics.Redis.html) to help you understand the inconsistency.

**Q: How much do read replicas cost? When does billing begin and end?**  
A read replica is billed as a standard cache node and at the same rates. Just like a standard cache node, the rate per cache node hour for a read replica is determined by the cache node class of the read replica: visit the [ElastiCache pricing page](https://aws.amazon.com/elasticache/pricing/) for up-to-date pricing. You are not charged for the data transfer incurred in replicating data between your primary cache node and read replica. Billing for a read replica begins as soon as the read replica has been successfully created (when the status is listed as active). The read replica will continue being billed at standard ElastiCache cache node hour rates until you issue a command to delete it.

**Q: What happens during failover and how long does it take?**  
Initiated failover is supported by ElastiCache so that you can resume cache operations as quickly as possible. When failing over, ElastiCache flips the DNS record for your cache node to point at the read replica, which is in turn promoted to become the new primary. We encourage you to follow best practices and implement cache node connection retry at the application layer. Typically, start to finish, steps one to five below complete within six minutes.

These are the automatic failover events, listed in order of occurrence:

1. Replication group message: Test Failover API called for node group `<node-group-id>`
2. Cache cluster message: Failover from primary node `<primary-node-id>` to replica node `<node-id>` completed
3. Replication group message: Failover from primary node `<primary-node-id>` to replica node `<node-id>` completed
4. Cache cluster message: Recovering cache nodes `<node-id>`
5. Cache cluster message: Finished recovery for cache nodes `<node-id>`

**Q: Can I create a read replica in another Region as my primary?**  
No, your read replica can only be provisioned in the same or different AZ of the same Region as your cache node primary. You can, however, use the [Global Datastore for Redis](https://docs.aws.amazon.com/AmazonElastiCache/latest/red-ug/Redis-Global-Datastore.html) to work with fully managed, fast, reliable, and security-focused replication across AWS Regions. Using this feature, you can create cross-Region read replica clusters for ElastiCache for Redis to enable low-latency reads and disaster recovery across AWS Regions.

**Q: Can I see which AZ my primary is currently located in?**  
Yes. You can gain visibility into the location of the current primary by using the console or DescribeCacheClusters API.

**Q: Can I add and remove read replica nodes for my Redis Cluster environment?**  
Yes. You can add or remove a read replica across one or more shards in a Redis Cluster environment. The cluster continues to stay online and serve incoming I/O during this operation.

### Multi-AZ

**Q: What is Multi-AZ for ElastiCache for Redis?**  
Multi-AZ is a feature that allows you to run in a more highly available configuration when designing your own ElastiCache for Redis cache.  
All ElastiCache Serverless caches are automatically run in a Multi-AZ configuration.  
An ElastiCache for Redis replication group consists of a primary and up to five read replicas. If Multi-AZ is enabled, then at least one replica is required per primary.  
During certain types of planned maintenance, or in the unlikely event of an ElastiCache node failure or AZ failure, ElastiCache will automatically detect the failure of a primary, select a read replica, and promote it to become the new primary. ElastiCache also propagates the DNS changes of the promoted read replica, so if your application is writing to the primary node endpoint, no endpoint change will be needed.

**Q: What are the benefits of using Multi-AZ and when should I use it?**  
The main benefits of running your ElastiCache for Redis in Multi-AZ mode are enhanced availability and a smaller need for administration. When running ElastiCache in a Multi-AZ configuration, your caches are eligible for the 99.99% availability SLA.  
If an ElastiCache for Redis primary node failure occurs, the impact on your ability to read and write to the primary is limited to the time it takes for automatic failover to complete. When Multi-AZ is enabled, ElastiCache node failover is automatic and requires no administration. You no longer need to monitor your Redis nodes and manually initiate a recovery in the event of a primary node disruption.

**Q: How does Multi-AZ work?**  
You can use Multi-AZ if you are using ElastiCache for Redis and have a replication group consisting of a primary node and one or more read replicas. If the primary node fails, ElastiCache will automatically detect the failure, select one from the available read replicas, and promote it to become the new primary. ElastiCache will propagate the DNS changes of the promoted replica so that your application can keep writing to the primary endpoint. ElastiCache will also spin up a new node to replace the promoted read replica in the same AZ of the failed primary. In case the primary failed due to temporary AZ disruption, the new replica will be launched once that AZ has recovered.

**Q: Can I have replicas in the same AZ as the primary?**  
Yes. Note that placing both the primary and the replicas in the same AZ will not make your ElastiCache for Redis replication group resilient to an AZ disruption. Additionally, having replicas in the same AZ as the primary will not be allowed if Multi-AZ is turned on.

**Q: What events would cause ElastiCache to fail over to a read replica?**  
ElastiCache will fail over to a read replica in the event of any of the following:

- Loss of availability in primary’s AZ  
    
- Loss of network connectivity to primary
- Compute unit failure on primary

**Q: Which read replica will be promoted in case of a primary node failure?**  
If there are more than one read replicas, the read replica with the smaller asynchronous replication lag to the primary will be promoted.

**Q: Will I be alerted when automatic failover occurs?**  
Yes, ElastiCache will create an event to inform you that automatic failover occurred. You can use the [DescribeEvents API](http://docs.aws.amazon.com/AmazonElastiCache/latest/APIReference/API_DescribeEvents.html) to return information about events related to your ElastiCache node, or select the Events section in the ElastiCache Management Console.

**Q: After failover, my primary is now located in a different AZ than my other AWS resources (for example, Amazon EC2 instances). Should I be concerned about latency?**  
AZs are engineered to provide low latency network connectivity to other AZs in the same Region. You should consider architecting your application and other AWS resources with redundancy across multiple AZs so your application will be resilient in the event of an AZ disruption.

**Q: Where can I get more information about Multi-AZ?**  
For more information about Multi-AZ, see ElastiCache [documentation](http://docs.aws.amazon.com/AmazonElastiCache/latest/UserGuide/RedisMultiAZ.html).

### Backup and Restore

**Q: What is Backup and Restore?**  
Backup and Restore is a feature that allows you to create snapshots of your ElastiCache for Redis caches. ElastiCache stores the snapshots, allowing users to subsequently use them to restore Redis caches.

**Q: Why would I need snapshots?**  
Creating snapshots can be useful in case of data loss caused by node failure, as well as the unlikely event of a hardware failure. Another common reason to use backups is for archiving purposes. Snapshots are stored in Amazon S3.

**Q: How does Backup and Restore work?**  
When a backup is initiated, ElastiCache will take a snapshot of a specified Redis cache that can later be used for recovery or archiving. You can initiate a backup any time you choose or set a recurring daily backup with retention period of up to 35 days. When you choose a snapshot to restore, a new ElastiCache for Redis cache will be created and populated with the snapshot’s data. ElastiCache for Redis snapshots are compatible with the open source Redis RDB file format.

**Q: How can I get started using Backup and Restore?**  
You can use the Backup and Restore feature through the console, ElastiCache APIs, and AWS CLI. You can deactivate and reactivate the feature any time you choose.

**Q: How do I specify which Redis cache and node to back up?**  
Backup and Restore creates snapshots on a per-cache basis. Users can specify which ElastiCache for Redis cache to back up through the console, AWS CLI, or the ElastiCache API. We recommend users enable backup on one of the cache’s read replicas, minimizing any potential impact on the primary. When using ElastiCache Serverless, backups are automatically conducted against read replicas.

**Q: Can I export ElastiCache for Redis snapshots to an Amazon S3 bucket owned by me?**  
Yes, you can export your ElastiCache for Redis snapshots to an authorized S3 bucket in the same Region as your cache.

**Q: I have multiple AWS accounts using ElastiCache for Redis. Can I use ElastiCache snapshots from one account to warm start an ElastiCache for Redis cluster in a different one?**  
Yes. You must first copy your snapshot into an authorized S3 bucket of your choice in the same Region and then grant cross-account bucket permissions to the other account.

**Q: How much does it cost to use Backup and Restore?**  
ElastiCache provides storage space for one snapshot free of charge for each active ElastiCache for Redis cache. Additional storage will be charged based on the space used by the snapshots with $0.085/GB every month (same price in all Regions). Data transfer for using the snapshots is free of charge.

**Q: What happens to my snapshots if I delete my ElastiCache for Redis cache?**  
When you delete an ElastiCache for Redis cache, your manual snapshots are retained. You will also have an option to create a final snapshot before the cache is deleted. Automatic cache snapshots are not retained.

### Enhanced Engine

**Q: How is the engine within ElastiCache for Redis different from open source Redis?**  
The engine within ElastiCache for Redis is fully compatible with open source Redis but also comes with enhancements that improve performance, robustness, and stability. Some of the enhancements include:

- More usable memory: You can now safely allocate more memory for your application without risking increased swap usage during syncs and snapshots.
- Improved synchronization: More robust synchronization under heavy load and when recovering from network disconnections. Additionally, syncs are faster as both the primary and replicas no longer use the disk for this operation.
- Smoother failovers: In the event of a failover, your shard now recovers faster as replicas no longer flush their data to do a full resync with the primary.
- TLS offload and IO multiplexing: ElastiCache is designed to better use available CPU resources by handling certain network-related processes on dedicated threads.

**Q: Do I need to change my application code to use the enhanced engine on ElastiCache?**  
No. The enhanced engine is fully compatible with open source Redis, thus you can enjoy its improved robustness and stability without the need to make any changes to your application code.

**Q: How much does it cost to use the enhanced engine?**  
There is no additional charge for using the enhanced engine.

### Encryption

**Q: What does encryption at rest for ElastiCache for Redis provide?**  
Encryption at rest provides mechanisms to guard against unauthorized access of your data. When enabled, it encrypts the following aspects:

- Disk during sync, backup, and swap operations
- Backups stored in Amazon S3

ElastiCache for Redis offers default (service-managed) encryption at rest, as well as the ability to use your own symmetric customer-managed AWS KMS keys in [AWS KMS](https://docs.aws.amazon.com/kms/latest/developerguide/overview.html). Visit [at-rest encryption](https://docs.aws.amazon.com/AmazonElastiCache/latest/red-ug/at-rest-encryption.html) to learn more.  
  
**Q: What does encryption in transit for ElastiCache for Redis provide?**  
The encryption in transit feature facilitates encryption of communications between clients and ElastiCache for Redis, as well as between the Redis servers (primary and read replicas). Read more about [ElastiCache in-transit encryption](https://docs.aws.amazon.com/AmazonElastiCache/latest/red-ug/in-transit-encryption.html).

**Q: How can I use encryption in transit, at rest, and Redis AUTH?**  
Encryption in transit, encryption at rest, Redis AUTH, and Role-Based Access Control (RBAC) are features you can select when creating your ElastiCache for Redis cache. If you enabled in-transit encryption, you can choose to use Redis AUTH or RBAC for additional security and access control.

**Q: Is there any action needed to renew TLS certificates?**  
No, ElastiCache manages certification expiration and renewal behind the scenes. No user action is necessary for ongoing certificate maintenance.

**Q: Are there additional costs for using encryption?**  
No, there are no additional costs for using encryption.

### Global Datastore

**Q: What is ElastiCache Global Datastore?**  
[Global Datastore is a feature of ElastiCache for Redis](https://docs.aws.amazon.com/AmazonElastiCache/latest/red-ug/Redis-Global-Datastore.html) that provides fully managed, fast, reliable and security-focused cross-Region replication. With Global Datastore, you can write to your ElastiCache for Redis cache in one Region and have the data available for read in up to two other cross-Region replica clusters, thereby enabling low-latency reads and disaster recovery across Regions.

Designed for real-time applications with a global footprint, Global Datastore typically replicates data across Regions in under one second, increasing the responsiveness of your applications by providing geolocal reads closer to end users. In the unlikely event of Regional degradation, one of the healthy cross-Region replica caches can be promoted to become the primary with full read and write capabilities. Once initiated, the promotion typically completes in less than a minute, allowing your applications to remain available.

**Q: How many AWS Regions can I replicate to?**  
You can replicate to up to two secondary Regions within a Global Datastore. The caches in secondary Regions can be used to serve low-latency local reads and for disaster recovery in the unlikely event of Regional degradation.

**Q: Which engine versions support Global Datastore?**  
Global Datastore is supported on ElastiCache for Redis 5.0.6 onward.

**Q: How can I create a Global Datastore?**  
You can set up a Global Datastore by using an existing cache or creating a new cache to be used as a primary. You can create a Global Datastore with just a few steps in the ElastiCache Management Console or by downloading the latest AWS SDK or AWS CLI. There is support for Global Datastore in AWS CloudFormation.

**Q: Does ElastiCache automatically fail over a Global Datastore to promote a secondary cluster in the event when a primary cluster (Region) is degraded?**  
No, ElastiCache doesn’t automatically promote a secondary cluster in the event when a primary cluster (Region) is degraded. You can manually initiate the failover by promoting a secondary cluster to become a primary. The fail over and promotion of a secondary cluster typically completes in less than one minute.

**Q: How is my data secured when using Global Datastore?**  
Global Datastore uses encryption in transit for cross-Region traffic to keep your data more secure. Additionally, you can also encrypt your primary and secondary caches using encryption at rest to keep your data better secured. Each primary and secondary cache can have a separate customer-managed AWS KMS key for encryption at rest.

**Q: What Recovery Point Objective (RPO) and Recovery Time Objective (RTO) can I expect with Global Datastore?**  
ElastiCache doesn’t provide an SLA for RPO and RTO. The RPO varies based on replication lag between Regions and depends on network latency between Regions and cross-Region network traffic congestion. The RPO of Global Datastore is typically under one second, so the data written in a primary Region is available in secondary Regions within one second. The RTO of Global Datastore for Redis is typically under a minute. Once a failover to a secondary cluster is initiated, ElastiCache typically promotes the secondary to full read and write capabilities in under a minute.

**Q: What is the pricing for Global Datastore?**  
ElastiCache does not charge any premium to use Global Datastore for Redis. You pay for the primary and secondary caches in your Global Datastore and for the [cross-Region data transfer traffic](https://aws.amazon.com/elasticache/pricing/).

### Data Tiering

**Q: What is data tiering for ElastiCache for Redis?**  
Data tiering provides a new price-performance option for Redis workloads by using lower-cost solid state drives (SSDs) in each cluster node in addition to storing data in memory. It is ideal for workloads that regularly access up to 20% of their overall dataset and for applications that can tolerate additional latency when accessing data on SSD. ElastiCache R6gd nodes with memory and SSDs have nearly 5x more total storage capacity and can help you achieve over 60% savings in price when running at maximum use compared to ElastiCache R6g nodes with memory only.

**Q: How does data tiering for ElastiCache for Redis work?**  
Data tiering works by automatically and transparently moving the least recently used items from memory to locally attached NVMe SSDs when available memory capacity is completely consumed. When an item that moves to SSD is subsequently accessed, ElastiCache moves it back to memory asynchronously before serving the request.

**Q: What performance can I expect when using clusters with data tiering?**  
Data tiering is designed to have minimal impact on application performance. Assuming 500-byte string values, you can expect an additional 300µs latency on average for requests to data stored on SSD compared to requests to data in memory.

**Q: Which engine versions support data tiering?**  
ElastiCache for Redis supports data tiering for Redis versions 6.2 and above.

**Q: Which node types support data tiering?**  
ElastiCache for Redis supports data tiering on Redis clusters using R6gd nodes.

**Q: Which ElastiCache features are supported for clusters using data tiering?**  
All Redis commands and most ElastiCache features are supported when using data tiering. For a list of features that are not supported on clusters using data tiering, see the [documentation](http://docs.aws.amazon.com/AmazonElastiCache/latest/red-ug/data-tiering.html).

**Q: What is the price for data tiering for ElastiCache for Redis?**  
There are no additional costs for using data tiering besides the node’s hourly cost. Nodes with data tiering are available with on-demand pricing and as reserved nodes. For pricing, see the [ElastiCache pricing page](https://aws.amazon.com/elasticache/pricing/).

## Memcached

[Memcached features](https://aws.amazon.com/elasticache/faqs/#Memcached_features) | [Configuration and scaling](https://aws.amazon.com/elasticache/faqs/#Configuration_and_scaling) | [Compatibility](https://aws.amazon.com/elasticache/faqs/#Compatibility) | [Auto Discovery](https://aws.amazon.com/elasticache/faqs/#Auto_Discovery) | [Engine version management](https://aws.amazon.com/elasticache/faqs/#Engine_version_management)

### Memcached Features

**Q: What can I cache using ElastiCache for Memcached?**  
You can cache a variety of objects using ElastiCache for Memcached. These objects include the content in persistent data stores (such as Amazon Relational Database Service (Amazon RDS), Amazon DynamoDB, or self-managed databases hosted on Amazon EC2), to dynamically generated web pages (with Nginx, for example), to transient session data that might not require a persistent backing store. You can also use it to implement high-frequency counters to deploy admission control in high-volume web applications.

**Q: Can I use ElastiCache for Memcached with an AWS persistent data store such as Amazon RDS or DynamoDB?**  
Yes. ElastiCache is an ideal front end for data stores like Amazon RDS or DynamoDB, providing a high-performance middle tier for applications with extremely high request rates or low latency requirements.

**Q: I currently use Memcached. How do I migrate to ElastiCache?**  
ElastiCache is protocol compliant with Memcached. Therefore, you can use standard Memcached operations like get, set, incr, and decr in exactly the same way as you would in your existing Memcached deployments. ElastiCache supports both the text and binary protocols. It also supports most of the standard stats results, which can also be viewed as graphs with CloudWatch. As a result, you can switch to using ElastiCache without recompiling or relinking your applications: The libraries you use will continue to work. To configure the cache servers your application accesses, update your application's Memcached config file to include the endpoints of the servers (nodes) we provision for you. You can use the Copy Node Endpoints option in the console or the DescribeCacheClusters API to get a list of the endpoints. As with any migration process, we recommend thorough testing of your new ElastiCache deployment before completing the cut-over from your current solution.

You can access ElastiCache clusters in an Amazon VPC from either the Amazon EC2 network or from your own data center. Please refer to [Amazon VPC access patterns](https://docs.aws.amazon.com/AmazonElastiCache/latest/mem-ug/elasticache-vpc-accessing.html) for more details. ElastiCache uses DNS entries to allow client applications to locate servers (nodes). The DNS name for a node remains constant, but the IP address of a node can change over time, for example, when nodes are autoreplaced after a failure on a non-VPC installation. See this FAQ for recommendations to deal with node failures.

### Configuration and Scaling

**Q: How do I select an appropriate node type for my application?**  
Though there is no precise answer for this question, with ElastiCache, you don't need to worry about getting the number of nodes exactly right, as you can quickly add or remove nodes later. You can also use ElastiCache Serverless to simplify running a highly available Memcached cache. The following two inter-related aspects can be considered for the choice of your initial configuration:

- The total memory required for your data to achieve your target cache-hit rate, and
- The number of nodes required to maintain acceptable application performance without overloading the database backend in the event of node failures.

The amount of memory required is dependent upon the size of your data set and the access patterns of your application. To improve fault tolerance, once you have a rough idea of the total memory required, divide that memory into enough nodes such that your application can survive the loss of one or two nodes. For example, if your memory requirement is 13 GB, you might want to use two cache.m4.large nodes instead of using one cache.m4.xlarge node. It is important that other systems such as databases will not be overloaded if the cache-hit rate is temporarily reduced during failure recovery of one or more nodes. Please refer to the [ElastiCache User Guide](http://docs.amazonwebservices.com/AmazonElastiCache/latest/mem-ug/ChooseACacheNodeType.html) for more details.

**Q: Can a cluster span multiple AZs?**  
Yes. When creating a cluster or adding nodes to an existing cluster, you can choose the AZs for the new nodes. You can either specify the requested number of nodes in each AZ or select Spread Nodes Across Zones. If the cluster is in Amazon VPC, nodes can only be placed in AZs that are part of the selected cache subnet group. For additional details, please see [ElastiCache VPC documentation](https://docs.aws.amazon.com/AmazonElastiCache/latest/red-ug/VPCs.CreatingCacheCluster.html).

**Q: How many nodes can I run per Region in ElastiCache Memcached?**  
You can run a maximum of 300 nodes per Region. If you need more nodes, please fill in the [ElastiCache Limit Increase Request form](http://aws.amazon.com/contact-us/elasticache-node-limit-request/).

**Q: How does ElastiCache respond to node failure?**  
The service will detect the node failure and react with the following automatic steps:

- ElastiCache will repair the node by acquiring new service resources and will then redirect the node's existing DNS name to point to the new service resources. For Amazon VPC installations, ElastiCache will ensure that both the DNS name and the IP address of the node remain the same when nodes are recovered in case of failure. For non–Amazon VPC installations, ElastiCache will ensure that the DNS name of a node is unchanged; however, the underlying IP address of the node can change.
- If you associated an SNS topic with your cluster, when the new node is configured and ready to be used, ElastiCache will send an SNS notification to let you know that node recovery occurred. This allows you to optionally arrange for your applications to force the Memcached client library to attempt to reconnect to the repaired nodes. This could be important, as some Memcached libraries will stop using a server (node) indefinitely if they encounter communication errors or timeouts with that server.

**Q: If I determine that I need more memory to support my application, how do I increase the total memory with ElastiCache?**  
You could add more nodes to your existing Memcached Cluster by using the Add Node option on the Nodes tab for your Cache Cluster in the console or calling the ModifyCacheCluster API.

### Compatibility

**Q: How does ElastiCache interact with other AWS services?**  
ElastiCache is ideally suited as a front end for AWS services like Amazon RDS and DynamoDB, providing extremely low latency for high-performance applications and offloading some of the request volume while these services provide long-lasting data durability. The service can also be used to improve application performance in conjunction with Amazon EC2 and Amazon EMR.

**Q: Is ElastiCache better suited to any specific programming language?**  
Memcached client libraries are available for many, if not all of the popular programming languages. If you encounter any issues with specific Memcached clients when using ElastiCache, please engage us in the [ElastiCache community forum](https://forums.aws.amazon.com/forum.jspa?forumID=127).

**Q: What popular Memcached libraries are compatible with ElastiCache?**  
ElastiCache does not require specific client libraries and works with existing Memcached client libraries without recompilation or application relinking (Memcached 1.4.5 and later). Examples include libMemcached (C) and libraries based on it (for instance, PHP, Perl, Python), spyMemcached (Java) and fauna (Ruby).

### Auto Discovery

**Q: What is Auto Discovery and what can I do with it?**  
Auto Discovery is a feature that saves developers time and effort, while reducing the complexity of their applications. Auto Discovery enables automatic discovery of cache nodes by clients when they are added to or removed from an ElastiCache cluster. Previously, to handle cluster membership changes, developers had to manually update the list of cache node endpoints. Depending on how the client application is architected, typically a client initialization (by shutting down the application and restarting it) is needed, resulting in downtime. Through Auto Discovery, ElastiCache removes this complexity. With Auto Discovery, in addition to being backwards protocol compliant with the Memcached protocol, ElastiCache provides clients with information on cache cluster membership. A client capable of processing the additional information reconfigures itself, without any initialization, to use the most current nodes of an ElastiCache cluster.

**Q: How does Auto Discovery work?**  
An ElastiCache cluster can be created with nodes that are addressable through named endpoints. With Auto Discovery the ElastiCache cluster is also given a unique configuration endpoint, which is a DNS Record that is valid for the lifetime of the cluster. This DNS Record contains the DNS Names of the nodes that belong to the cluster. ElastiCache will ensure that the configuration endpoint always points to at least one such target node. A query to the target node then returns endpoints for all the nodes of the cluster in question. After this, you can connect to the cluster nodes just as before and use the Memcached protocol commands such as get, set, incr, and decr. For more details, see [the documentation](https://docs.aws.amazon.com/AmazonElastiCache/latest/mem-ug/AutoDiscovery.Using.html). To use Auto Discovery, you will need a client capable of Auto Discovery. Auto Discovery clients for .Net , Java and PHP are available for download from the [ElastiCache console](https://console.aws.amazon.com/elasticache/). Upon initialization, the client will automatically determine the current members of the ElastiCache cluster using the configuration endpoint. When you make changes to your cache cluster by adding or removing nodes, or if a node is replaced upon failure, the Auto Discovery client automatically determines the changes, and you do not need to initialize your clients manually.

**Q: How can I get started using Auto Discovery?**  
To get started, download the ElastiCache Cluster Client by selecting the Download ElastiCache Cluster Client link on the [ElastiCache console](https://console.aws.amazon.com/elasticache/). Before you can download, you must have an ElastiCache account; if you do not already have one, you can sign up from the ElastiCache detail page. After you download the client, you can begin setting up and activating your ElastiCache cluster by visiting the [ElastiCache console](https://console.aws.amazon.com/elasticache/). More details can be found in the [documentation](http://docs.amazonwebservices.com/AmazonElastiCache/latest/mem-ug/AutoDiscovery.html).

**Q: If I continue to use my own Memcached clients with my ElastiCache cluster, will I be able to get this feature?**  
No, you will not get the Auto Discovery feature with the existing Memcached clients. To use the Auto Discovery feature a client must be able to use a configuration endpoint and determine the cluster node endpoints. You can either use the ElastiCache Cluster Client or extend your existing Memcached client to include the [Auto Discovery command set](https://docs.aws.amazon.com/AmazonElastiCache/latest/mem-ug/AutoDiscovery.AddingToYourClientLibrary.html).

**Q: What are the minimum hardware and software requirements for Auto Discovery?**  
To take advantage of Auto Discovery, a client capable of Auto Discovery must be used to connect to an ElastiCache Cluster. ElastiCache currently supports clients capable of Auto Discovery for .Net, Java, and PHP. These can be downloaded from the [ElastiCache console](https://console.aws.amazon.com/elasticache/). You can create clients for any other languages by building upon the popular Memcached clients available.

**Q: How do I modify or write my own Memcached client to support Auto Discovery?**  
You can take any Memcached Client Library and add support for Auto Discovery. If you would like to add or modify your own client to enable Auto Discovery, please refer to the [Auto Discovery command set documentation](https://docs.aws.amazon.com/AmazonElastiCache/latest/mem-ug/AutoDiscovery.AddingToYourClientLibrary.html).

**Q: Can I continue to work with my existing Memcached client if I don’t need Auto Discovery?**  
Yes, ElastiCache is still Memcached protocol compliant and does not require you to change your clients. However, to take advantage of the Auto Discovery feature, we enhanced the Memcached client capabilities. If you choose not to use the ElastiCache Cluster Client, you can continue to use your own clients or modify your own client library to understand the Auto Discovery command set.

**Q: Can I have heterogeneous clients when using Auto Discovery?**  
Yes, the same ElastiCache cluster can be connected through a client capable of Auto Discovery and the traditional Memcached client at the same time. ElastiCache remains 100% Memcached compliant.

**Q: Can I stop using Auto Discovery?**  
Yes, you can stop using Auto Discovery at any time. You can disable Auto Discovery by specifying the mode of operation during the ElastiCache Cluster client initialization. Also, since ElastiCache continues to support Memcached, you can use any Memcached protocol-compliant client as before.

### Engine Version Management

**Q: Can I control if and when the engine version powering ElastiCache Cluster is upgraded to new supported versions?**  
ElastiCache allows you to control if and when the Memcached protocol-compliant software powering your cluster is upgraded to new versions supported by ElastiCache. This provides you with the flexibility to maintain compatibility with specific Memcached versions, test new versions with your application before deploying in production, and perform version upgrades on your own terms and timelines. Version upgrades involve some compatibility risk; thus they will not occur automatically and must be initiated by you. This approach to software patching puts you in the driver's seat of version upgrades, but still offloads the work of patch application to ElastiCache. You can learn more about version management by reading the FAQs that follow. Alternatively, you can refer to the [ElastiCache User Guide](https://docs.aws.amazon.com/AmazonElastiCache/latest/mem-ug/VersionManagement.html). While Engine Version Management functionality is intended to give you as much control as possible over how patching occurs, we can patch your cluster on your behalf if we determine there is any security vulnerability in the system or cache software.

**Q: How do I specify which supported Memcached Version my cluster should run?**  
You can specify any currently supported version (minor or major) when creating a new cluster. If you wish to initiate an upgrade to a supported engine version release, you can do so using the Modify option for your cluster. Specify the version you wish to upgrade to in the Cache Engine Version field. The upgrade will then be applied on your behalf either immediately (if the Applied Immediately option is checked) or during the next scheduled maintenance window for your cluster.

**Q: Can I test my cluster against a new version before upgrading?**  
Yes. You can do so by creating a new cluster with the new engine version. You can point your development or staging application to this cluster, test it, and decide whether or not to upgrade your original cluster.

**Q: Does ElastiCache provide guidelines for supporting new Memcached version releases or deprecating versions that are currently supported?**  
We plan to support additional Memcached versions for ElastiCache, both major and minor. The number of new version releases supported in a given year will vary based on the frequency and content of the Memcached version releases and the outcome of a thorough vetting of the release by our engineering team.

**Q: What should I do to upgrade to the latest Memcached version?**  
You can upgrade your existing Memcached cluster by using the Modify process. When upgrading from an older version of Memcached to Memcached version 1.4.33 or newer, please ensure that your existing parameter max\_chunk\_size values satisfies conditions needed for slab\_chunk\_max parameter. Please review [upgrade prerequisites](https://docs.aws.amazon.com/AmazonElastiCache/latest/mem-ug/VersionManagement.html).