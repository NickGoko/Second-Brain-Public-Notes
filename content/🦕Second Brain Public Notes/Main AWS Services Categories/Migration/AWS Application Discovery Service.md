---
tags:
  - cloud/aws
---

![](https://i.imgur.com/CNtR5ZP.png)
 
# FAQ
## General

[Q: What is the AWS Application Discovery Service? >>](https://aws.amazon.com/application-discovery/faqs//#)

**Q: What is AWS Application Discovery Service?**

AWS Application Discovery Service collects and presents data to enable enterprise customers to understand the configuration, usage, and behavior of servers in their IT environments. Server data is retained in the Application Discovery Service where it can be tagged and grouped into applications to help organize AWS migration planning. Collected data can be exported for analysis in Excel or other cloud migration analysis tools.  

[Show less](https://aws.amazon.com/application-discovery/faqs//#)

[Q: How does the Application Discovery Service help enterprises migrate to AWS? >>](https://aws.amazon.com/application-discovery/faqs//#)

**Q: How does the Application Discovery Service help enterprises migrate to AWS?**

Application Discovery Service helps enterprises obtain a snapshot of the current state of their data center servers by collecting server specification information, hardware configuration, performance data, and details of running processes and network connections. Once the data is collected, you can use it to perform a Total Cost of Ownership (TCO) analysis and then create a cost optimized migration plan based on your unique business requirements.  

[Show less](https://aws.amazon.com/application-discovery/faqs//#)

[Q: How does Application Discovery Service work? >>](https://aws.amazon.com/application-discovery/faqs//#)

**Q: How does Application Discovery Service work?**

Application Discovery Service supports both agent and agentless-based on-premises tooling, in addition to file-based import. With agentless discovery, customers deploy the tooling on centralized servers which then leverage public APIs within the on-premises environment to discover resources and monitor utilization. This process allows one install to monitor many servers. For customers that need higher resolution data, including information about running processes, the collection tooling is deployed on each server (physical or virtual) within the on-premises environment.  

[Show less](https://aws.amazon.com/application-discovery/faqs//#)

[Q: How can I get started using Application Discovery Service? >>](https://aws.amazon.com/application-discovery/faqs//#)

**Q: How can I get started using Application Discovery Service?**

To get started with Application Discovery Service, simply visit the [AWS Migration Hub console](https://console.aws.amazon.com/migrationhub/dashboard).  

[Show less](https://aws.amazon.com/application-discovery/faqs//#)

[Q: Where is Application Discovery Service available? >>](https://aws.amazon.com/application-discovery/faqs//#)

**Q: Where is Application Discovery Service available?**

Application Discovery Service is available worldwide. This means you can perform discovery on resources regardless of their location. To see which regions the service is hosted in, please refer to the [AWS Region Table](https://aws.amazon.com/about-aws/global-infrastructure/regional-product-services/).  

[Show less](https://aws.amazon.com/application-discovery/faqs//#)

[Q: What is the Migration Hub home region? >>](https://aws.amazon.com/application-discovery/faqs//#)

**Q: What is the Migration Hub home region?**

Before using the Migration Hub and Application Discovery Service, you need to select a Migration Hub home region from the [Migration Hub Settings](https://console.aws.amazon.com/migrationhub/settings) page or using the [Migration Hub Config API](https://docs.aws.amazon.com/migrationhub-home-region/latest/APIReference/Welcome.html). Application Discovery Service uses the Migration Hub home region as the only AWS region to store your discovery and planning data. The data stored in the Migration Hub home region provides a single repository of discovery and migration planning information for your entire portfolio and a single view of migrations into multiple AWS regions. See [the docs](https://docs.aws.amazon.com/migrationhub/latest/ug/home-region.html) to learn more about the Migration Hub home region.

Note: Once set, the Migration Hub home region cannot be changed.  

[Show less](https://aws.amazon.com/application-discovery/faqs//#)

[Q: Which on-premises discovery tool should I use? >>](https://aws.amazon.com/application-discovery/faqs//#)

**Q: Which on-premises discovery tool should I use?  
**

Customers looking for process-level dependency data are advised to use the AWS Application Discovery Service Discovery Agent. The data collected may be used in both Migration Hub and Amazon Athena.

Customers exclusively looking for metadata about on-premises VMware infrastructure should use the AWS Application Discovery Service Agentless Collector. The data discovered may be used in Migration Hub. Both agent-based and agentless Application Discovery may be run simultaneously.

Customers looking for a guided migration assessment or agentless server dependency mapping should request an assessment via Migration Evaluator. This service offers a dedicated solutions architect to assist with data discovery and provide migration expertise. The Migration Evaluator Agentless Collector monitors VMware, Hyper-V, SQL Server, Windows, and Linux workloads. The data collected may be used in both Migration Hub and Migration Evaluator.  

[Show less](https://aws.amazon.com/application-discovery/faqs//#)

## Agent-based Discovery

[Q: What data does the AWS Application Discovery Service Discovery Agent capture? >>](https://aws.amazon.com/application-discovery/faqs//#)

**Q: What data does the AWS Application Discovery Service Discovery Agent capture?**

The Discovery Agent captures system configuration, system performance, running processes, and details of the network connections between systems.  

[Show less](https://aws.amazon.com/application-discovery/faqs//#)

[Q: What operating systems does Application Discovery Service provide agents for? >>](https://aws.amazon.com/application-discovery/faqs//#)

**Q: What operating systems does Application Discovery Service provide agents for?**

Application Discovery Service launched a new 2.0 version of the Discovery Agent that offers better operating system support. 2.0 version of the Discovery Agent supports Microsoft Windows Server 2008 R1 SP2, 2008 R2 SP1, 2012 R1, 2012 R2, 2016, 2019, Amazon Linux 2012.03, 2015.03, Amazon Linux 2 (9/25/2018 update and later), Ubuntu 12.04, 14.04, 16.04, 18.04, 20.04, Red Hat Enterprise Linux 5.11, 6.10, 7.3, 7.7, 8.1, CentOS 5.11, 6.9, 7.3 and SUSE 11 SP4, 12 SP5.

[Show less](https://aws.amazon.com/application-discovery/faqs//#)

[Q: How is the data protected while in transit to AWS? >>](https://aws.amazon.com/application-discovery/faqs//#)

**Q: How is the data protected while in transit to AWS?**

The Discovery Agent uses HTTPS/TLS to transmit data to Application Discovery Service. The Discovery Agent can be operated in an offline test mode that writes data to a local file so customers can review collected data before enabling online mode.  

[Show less](https://aws.amazon.com/application-discovery/faqs//#)

[Q: How do I install the Discovery Agent in my data center? >>](https://aws.amazon.com/application-discovery/faqs//#)

**Q: How do I install the Discovery Agent in my data center?**

Please refer to the [documentation](https://aws.amazon.com/documentation/application-discovery/) for details on how to install the Discovery Agent.  

[Show less](https://aws.amazon.com/application-discovery/faqs//#)

[Q: Will the Discovery Agent grant AWS remote access to my data center server? >>](https://aws.amazon.com/application-discovery/faqs//#)

**Q: Will the Discovery Agent grant AWS remote access to my data center server?**

No, the Discovery Agent deployed on your data center server will not grant AWS remote access. However, the Discovery Agent does need to establish an outbound SSL connection to transfer the collected data to AWS.  

[Show less](https://aws.amazon.com/application-discovery/faqs//#)

[Q: Can I run agents in my EC2 instances? >>](https://aws.amazon.com/application-discovery/faqs//#)

**Q: Can I run agents in my EC2 instances?**

Yes. You can install the Discovery Agents on your EC2 instances to perform discovery and report upon performance information, network connections, and running processes, just as for any other server.  

[Show less](https://aws.amazon.com/application-discovery/faqs//#)

## Agentless Discovery

[Q: What does ‘agentless’ Application Discovery mean? >>](https://aws.amazon.com/application-discovery/faqs//#)

**Q: What does ‘agentless’ Application Discovery mean?**

‘Agentless’ means that software does not need to be installed on each host to use Application Discovery. Simply install the Agentless Collector as an OVA on the VMware vCenter.  

[Show less](https://aws.amazon.com/application-discovery/faqs//#)

[Q: What data does the Agentless Collector capture? >>](https://aws.amazon.com/application-discovery/faqs//#)

**Q: What data does the Agentless Collector capture?**

The Agentless Collector is delivered as an Open Virtual Appliance (OVA) package that can be deployed to a VMware host. The type of data collected will depend on the capabilities that you configure. If the credentials are provided to connect to vCenter, the Agentless Collector will collect VM inventory, configuration, and performance history data such as CPU, memory, and disk usage. If credentials are provided to connect to databases such as Oracle, SQL Server, MySQL, or PostgreSQL, the Agentless Collector will collect version, edition, and schema data. Server and database information is uploaded to the Application Discovery Service data store. Database information can be sent to AWS DMS Fleet Advisor for analysis.  

[Show less](https://aws.amazon.com/application-discovery/faqs//#)

[Q: What operating systems does the agentless discovery support? >>](https://aws.amazon.com/application-discovery/faqs//#)

**Q: What operating systems does the agentless discovery support?**

Agentless discovery is OS agnostic. It collects information about VMware virtual machines regardless of the VM operating system.  

[Show less](https://aws.amazon.com/application-discovery/faqs//#)

[Q: How is the data protected while in transit to AWS? >>](https://aws.amazon.com/application-discovery/faqs//#)

**Q: How is the data protected while in transit to AWS?**

The Agentless Collector uses HTTPS/TLS to transmit data to the Application Discovery Service.  

[Show less](https://aws.amazon.com/application-discovery/faqs//#)

[Q: How do I install the Agentless Collector in my data center? >>](https://aws.amazon.com/application-discovery/faqs//#)

**Q: How do I install the Agentless Collector in my data center?**

Please refer to the [documentation](https://docs.aws.amazon.com/application-discovery/latest/userguide/agentless-collector.html) for details on how to install the Agentless Collector.  

[Show less](https://aws.amazon.com/application-discovery/faqs//#)

[Q: How can I start the data collection? >>](https://aws.amazon.com/application-discovery/faqs//#)

**Q: How can I start the data collection?**

Data collection is controlled from the local Agentless Collector UI. You will need access to the on-premises environment to start or stop collection.  

[Show less](https://aws.amazon.com/application-discovery/faqs//#)

[Q: Will the Agentless Collector grant AWS remote access to my data center servers? >>](https://aws.amazon.com/application-discovery/faqs//#)

**Q: Will the Agentless Collector grant AWS remote access to my data center servers?**

No, the Agentless Collector deployed on your VMware environment will not grant AWS remote access to your data center servers. However, the tool requires VMware credentials in order to collect data. These credentials reside locally and are never shared with AWS. The Agentless Collector establishes outbound SSL connection to transfer only the collected data.  

[Show less](https://aws.amazon.com/application-discovery/faqs//#)

[Q: Can I run agentless discovery in my EC2 instances? >>](https://aws.amazon.com/application-discovery/faqs//#)

**Q: Can I run agentless discovery in my EC2 instances?**

No. The Agentless Collector installs on VMware and collects information only from the VMware vCenter.  

[Show less](https://aws.amazon.com/application-discovery/faqs//#)

## Discovered Data

[Q: What kind of information is captured by Application Discovery Service? >>](https://aws.amazon.com/application-discovery/faqs//#)

**Q: What kind of information is captured by Application Discovery Service?**

Application Discovery Service is designed to capture a variety of data including static configuration such as server hostnames, IP addresses, MAC addresses, CPU allocation, network throughput, memory allocation, disk resource allocations, and DNS servers. It also captures resource utilization metrics such as CPU usage and memory usage. Application Discovery Service offers two collectors. In addition to the information above, the Discovery Agent can help identify server workloads by collecting active Transport Control Protocol (TCP) connections and process information. The Agentless Collector can additionally discover engine, version, and edition information for databases.  

[Show less](https://aws.amazon.com/application-discovery/faqs//#)

[Q: Does this service capture any storage metrics? >>](https://aws.amazon.com/application-discovery/faqs//#)

**Q: Does this service capture any storage metrics?**

Yes, disk metrics, such as read and write volume, throughput, allocated/provisioned and utilized capacity, are captured by this service.  

[Show less](https://aws.amazon.com/application-discovery/faqs//#)

[Q: How often is the information within Application Discovery Service updated? >>](https://aws.amazon.com/application-discovery/faqs//#)

**Q: How often is the information within Application Discovery Service updated?**

Information is gathered only when the Discovery Agent or the Agentless Collector is online.  

[Show less](https://aws.amazon.com/application-discovery/faqs//#)

## Using the AWS Application Discovery Service Data

[Q: Can I ingest data into Application Discovery Service from my existing configuration management database (CMDB)? >>](https://aws.amazon.com/application-discovery/faqs//#)

**Q: Can I ingest data into Application Discovery Service from my existing configuration management database (CMDB)?**

Yes, you can import information about your on-premises servers and applications into the Migration Hub so you can track the status of application migrations. To import your data, you can download and populate the import CSV template and then upload it using the Migration Hub import console or by invoking the Application Discovery Service APIs.  

[Show less](https://aws.amazon.com/application-discovery/faqs//#)

[Q: How do I access the data from this service? >>](https://aws.amazon.com/application-discovery/faqs//#)

**Q: How do I access the data from this service?**

Summary data can be viewed in the AWS console. You can export detailed data collected by Application Discovery Service using the AWS Console or a public API. The service exports data in CSV format.  

[Show less](https://aws.amazon.com/application-discovery/faqs//#)

## Data Exploration in Amazon Athena

[Q. What is the Data Exploration feature? >>](https://aws.amazon.com/application-discovery/faqs//#)

**Q. What is the Data Exploration feature?**

The Data Exploration feature allows customers to analyze the data collected from their on-premises servers by Application Discovery Service agents in one single place. Once a customer enables this feature, data collected by agents is automatically stored in an Amazon S3 bucket created in their account. Customers can query the collected data in Amazon Athena and visualize the query output in Amazon QuickSight to perform migration planning.

[Show less](https://aws.amazon.com/application-discovery/faqs//#)

[Q. What can I see inside Amazon Athena with Data Exploration turned on? >>](https://aws.amazon.com/application-discovery/faqs//#)

**Q. What can I see inside Amazon Athena with Data Exploration turned on?**

If the Data Exploration feature is turned on when you get to Amazon Athena, you can see a database called “application\_discovery\_service\_database”. Inside the database, a list of tables is created by default for you. These tables include:

- os\_info\_agent
- network\_interface\_agent
- sys\_performance\_agent
- processes\_agent
- inbound\_connection\_agent
- outbound\_connection\_agent
- id\_mapping\_agent  
    

[Show less](https://aws.amazon.com/application-discovery/faqs//#)

[Q. Is there cost associated with using Application Discovery Service’s Data Exploration feature? >>](https://aws.amazon.com/application-discovery/faqs//#)

**Q. Is there cost associated with using Application Discovery Service’s Data Exploration feature?**

The Application Discovery Service discovery tools are available at no charge. However, additional charges may apply for streaming agent data via Amazon Kinesis Data Firehose, for storing the agent data in a S3 bucket and for querying the agent data in Amazon Athena. The cost of using each of these AWS resources will vary based on the actual time period you collect data via agents, the number of agents you have deployed, the network activity on each server where the agent is deployed, and the number of queries that are run on the collected data.

**Q. Can I enable Data Exploration for some agents only?**

No, the Data Exploration feature is a global setting for all agents. The global setting ensures that data collected by all agents is for the same time period.

**Q. Do I need to create a special S3 bucket to use this feature?**

No, you don’t have to create an S3 bucket on your own. When you turn on this new feature for the first time, a S3 bucket with the name “aws-application-discovery-service-” is created automatically on your behalf. By default, this bucket and the discovery data saved to this bucket are private. Only the users in your account with permission to Application Discovery Service and Migration Hub can access the bucket and the data it contains.

**Q. Will the S3 bucket storing my discovery data be secure?**

Yes, the data stored in the designed S3 bucket is encrypted using the [customer master key](https://docs.aws.amazon.com/kms/latest/developerguide/concepts.html#master_keys). You can also further control access to your S3 resources by using a combination of [bucket ACLs](https://docs.aws.amazon.com/AmazonS3/latest/dev/acl-overview.html) and [IAM and bucket policies](https://docs.aws.amazon.com/AmazonS3/latest/dev/using-iam-policies.html).