---
tags:
  - cloud/aws
---
AWS Disaster Recovery Whitepaper is one of the very important Whitepaper for both the Associate & Professional AWS Certification exam

## Disaster Recovery Overview

![[Pasted image 20240229215026.png]]
- AWS Disaster Recovery whitepaper highlights AWS services and features that can be leveraged for disaster recovery (DR) processes to significantly minimize the impact on data, system, and overall business operations.
- It outlines best practices to improve your DR processes, from minimal investments to full-scale availability and fault tolerance, and describes how AWS services can be used to reduce cost and ensure business continuity during a DR event
- Disaster recovery (DR) is about preparing for and recovering from a disaster. Any event that has a negative impact on a company’s business continuity or finances could be termed a disaster. One of the AWS best practice is to always design your systems for failures

## **Disaster Recovery Key AWS Services**

1. **Region**
    - AWS services are available in multiple regions around the globe, and the DR site location can be selected as appropriate, in addition to the primary site location
2. Storage
    - **Amazon S3**
        - provides a highly durable (99.999999999%) storage infrastructure designed for mission-critical and primary data storage.
        - stores Objects redundantly on multiple devices across multiple facilities within a region
    - **Amazon Glacier**
        - provides extremely low-cost storage for data archiving and backup.
        - Objects are optimized for infrequent access, for which retrieval times of several **(3-5) hours** are adequate.
    - **Amazon EBS**
        - provides the ability to create point-in-time snapshots of data volumes.
        - Snapshots can then be used to create volumes and attached to running instances
    - **Amazon Storage Gateway**
        - a service that provides seamless and highly secure integration between on-premises IT environment and the storage infrastructure of AWS.
    - **AWS Import/Export**
        - accelerates moving large amounts of data into and out of AWS by using portable storage devices for transport bypassing the Internet
        - transfers data directly onto and off of storage devices by means of the high-speed internal network of Amazon
3. Compute
    - **Amazon EC2**
        - provides resizable compute capacity in the cloud which can be easily created and scaled.
        - EC2 instance creation using Preconfigured AMIs
        - EC2 instances can be launched in multiple AZs, which are engineered to be insulated from failures in other AZs
4. Networking
    - **Amazon Route 53**
        - is a highly available and scalable DNS web service
        - includes a number of global load-balancing capabilities that can be effective when dealing with DR scenarios _for e.g. DNS endpoint health checks and the ability to failover between multiple endpoints_ 
    - **Elastic IP**
        - addresses enables masking of instance or Availability Zone failures by <mark style="background: #ADCCFFA6;">programmatically remapping</mark>
        - addresses are static IP addresses designed for dynamic cloud computing.
    - **Elastic Load Balancing (****ELB)**
        - <mark style="background: #ADCCFFA6;">performs health checks and automatically distributes incoming application traffic across multiple EC2 instances</mark>
    - **Amazon Virtual Private Cloud (Amazon VPC)**
        - allows provisioning of a private, isolated section of the AWS cloud where resources can be launched in a defined virtual network
    - **Amazon Direct Connect**
        - makes it easy to set up a dedicated network connection from on-premises environment to AWS
5. Databases
    - **RDS, DynamoDb, Redshift** provided as a fully managed RDBMS, NoSQL and data warehouse solutions which can scale up easily
    - DynamoDB offers cross region replication
    - RDS provides Multi-AZ and Read Replicas and also ability to snapshot data from one region to other
6. Deployment Orchestration
    - **CloudFormation**
        - gives developers and systems administrators an easy way to create a collection of related AWS resources and provision them in an orderly and predictable fashion
    - **Elastic Beanstalk**
        - is an easy-to-use service for deploying and scaling web applications and services
    - **OpsWorks**
        - is an application management service that makes it easy to deploy and operate applications of all types and sizes.
        - Environment can be defined as a series of layers, and each layer can be configured as a tier of the application.
        - has automatic host replacement, so in the event of an instance failure it will be automatically replaced.
        - can be used in the preparation phase to template the environment, and combined with AWS CloudFormation in the recovery phase.
        - Stacks can be quickly provisioned from the stored configuration to support the defined RTO.  

![](https://i.imgur.com/8MnvS25.png)


## **Key Factors for Disaster Planning**

![Disaster Recovery RTO RPO Defination](https://jayendrapatil.com/wp-content/uploads/2016/03/Screen-Shot-2016-05-30-at-8.01.45-AM-1024x283.png)

**Recovery Time Objective (RTO)** – The time it takes **after a disruption** to restore a business process to its service level, as defined by the operational level agreement (OLA) _for e.g. if the RTO is 1 hour and disaster occurs @ 12:00 p.m (noon), then the DR process should restore the systems to an acceptable service level within an hour i.e. by 1:00 p.m_

**Recovery Point Objective (RPO)** – The acceptable amount of data loss measured in time **before the disaster occurs**. _for e.g., if a disaster occurs at 12:00 p.m (noon) and the RPO is one hour, the system should recover all data that was in the system before 11:00 a.m._

## Disaster Recovery Scenarios

- Disaster Recovery scenarios can be implemented with the Primary infrastructure running in your data center in conjunction with the AWS
- Disaster Recovery Scenarios still apply if Primary site is running in AWS using AWS multi region feature.
- Combination and variation of the below is always possible.

## Disaster Recovery Scenarios Options

![[Pasted image 20240229214042.png]]
1. Backup & Restore (Data backed up and restored)
2. Pilot Light (Only Minimal critical functionalities)
3. Warm Standby (Fully Functional Scaled down version)
4. Multi-Site (Active-Active)

![](https://jayendrapatil.com/wp-content/uploads/2016/03/Disaster-Recovery.png)

For the DR scenarios options, RTO and RPO reduces with an increase in Cost as you move from Backup & Restore option (left) to Multi-Site option (right)

### Backup & Restore

AWS can be used to backup the data in a cost effective, durable and secure manner as well as recover the data quickly and reliably.

#### Backup Phase
![[Pasted image 20240215113416.png]]  
In most traditional environments, data is backed up to tape and sent off-site regularly taking longer time to restore the system in the event of a disruption or disaster![Backup Restore - Backup Phase](https://jayendrapatil.com/wp-content/uploads/2016/03/Screen-Shot-2016-05-30-at-8.15.13-AM.png)

1. Amazon S3 can be used to backup the data and perform a quick restore and is also available from any location
2. AWS Import/Export can be used to transfer large data sets by shipping storage devices directly to AWS bypassing the Internet
3. Amazon Glacier can be used for archiving data, where retrieval time of several hours are adequate and acceptable
4. AWS Storage Gateway enables snapshots (used to created EBS volumes) of the on-premises data volumes to be transparently copied into S3 for backup. It can be used either as a backup solution (Gateway-stored volumes) or as a primary data store (Gateway-cached volumes)
5. AWS Direct connect can be used to transfer data directly from On-Premise to Amazon consistently and at high speed
6. Snapshots of Amazon EBS volumes, Amazon RDS databases, and Amazon Redshift data warehouses can be stored in Amazon S3

#### **Restore phase**

Data backed up then can be used to quickly restore and create Compute and Database instances

![Backup Restore - Recovery Phase](https://jayendrapatil.com/wp-content/uploads/2016/03/Screen-Shot-2016-05-30-at-8.23.51-AM.png)Key steps for Backup and Restore:  
1\. Select an appropriate tool or method to back up the data into AWS.  
2\. Ensure an appropriate retention policy for this data.  
3\. Ensure appropriate security measures are in place for this data, including encryption and access policies.  
4\. Regularly test the recovery of this data and the restoration of the system.

### Pilot Light
![[Pasted image 20240215113523.png]]  
In a Pilot Light Disaster Recovery scenario option a minimal version of an environment is always running in the cloud, which basically host the critical functionalities of the application _for e.g. databases_

In this approach :-

1. Maintain a pilot light by configuring and running the most critical core elements of your system in AWS _for e.g. Databases_ where the data needs to be replicated and kept updated.
2. During recovery, a full-scale production environment, _for e.g. application and web servers,_ can be rapidly provisioned (using preconfigured AMIs and EBS volume snapshots) around the critical core
3. For Networking, either a ELB to distribute traffic to multiple instances and have DNS point to the load balancer or preallocated Elastic IP address with instances associated can be used

Preparation phase steps :

1. Set up Amazon EC2 instances or RDS instances to replicate or mirror data critical data
2. Ensure that all supporting custom software packages available in AWS.
3. Create and maintain AMIs of key servers where fast recovery is required.
4. Regularly run these servers, test them, and apply any software updates and configuration changes.
5. Consider automating the provisioning of AWS resources.

![Pilot Light Scenario - Preparation Phase](https://jayendrapatil.com/wp-content/uploads/2016/03/Preparation-Phase-Pilot-Light-Scenario.png)

Recovery Phase steps :

1. Start the application EC2 instances from your custom AMIs.
2. Resize existing database/data store instances to process the increased traffic _for e.g. If using RDS, it can be easily scaled vertically while EC2 instances can be easily scaled horizontally_
3. Add additional database/data store instances to give the DR site resilience in the data tier _for e.g. turn on Multi-AZ for RDS to improve resilience._
4. Change DNS to point at the Amazon EC2 servers.
5. Install and configure any non-AMI based systems, ideally in an automated way.

![Pilot Light Scenario - Recovery Phase](https://jayendrapatil.com/wp-content/uploads/2016/03/Recovery-Phase-Pilot-Light-Scenario.png)

### **Warm Standby**
![[Pasted image 20240215113619.png]]
- In a Warm standby DR scenario a scaled-down version of a fully functional environment identical to the business critical systems is always running in the cloud
- This setup can be used for testing, quality assurances or for internal use.
- In case of an disaster, the system can be easily scaled up or out to handle production load.

Preparation phase steps :

1. Set up Amazon EC2 instances to replicate or mirror data.
2. Create and maintain AMIs for faster provisioning
3. Run the application using a minimal footprint of EC2 instances or AWS infrastructure.
4. Patch and update software and configuration files in line with your live environment.

![Warm Standby - Preparation Phase](https://jayendrapatil.com/wp-content/uploads/2016/03/Preparation-Phase-Warm-Standby.png)Recovery phase Steps:

1. Increase the size of the Amazon EC2 fleets in service with the load balancer (**horizontal scaling**).
2. Start applications on larger Amazon EC2 instance types as needed (**vertical scaling**).
3. Either manually change the DNS records, or use Route 53 automated health checks to route all the traffic to the AWS environment.
4. Consider using Auto Scaling to right-size the fleet or accommodate the increased load.
5. Add resilience or scale up your database to guard against DR going down

![Warm Standby - Recovery Phase](https://jayendrapatil.com/wp-content/uploads/2016/03/Recovery-Phase-Warm-Standby.png)

### **Multi-Site**
![[Pasted image 20240215113833.png]]
- Multi-Site is an **active-active** configuration DR approach, <mark style="background: #BBFABBA6;">where in an identical solution runs on AWS as your on-site infrastructure.</mark>
- Traffic can be equally distributed to both the infrastructure as needed by using DNS service weighted routing approach.
- In case of a disaster the DNS can be tuned to send all the traffic to the AWS environment and the AWS infrastructure scaled accordingly.

Preparation phase steps :

1. Set up your AWS environment to duplicate the production environment.
2. Set up DNS weighting, or similar traffic routing technology, to distribute incoming requests to both sites.
3. Configure automated failover to re-route traffic away from the affected site. _for e.g. application to check if primary DB is available if not then redirect to the AWS DB_

![Multi-Site - Preparation Phase](https://jayendrapatil.com/wp-content/uploads/2016/03/Preparation-Phase-Multi-Site-Scenario.png)

Recovery phase steps :

1. Either manually or by using DNS failover, change the DNS weighting so that all requests are sent to the AWS site.
2. Have application logic for failover to use the local AWS database servers for all queries.
3. Consider using Auto Scaling to automatically right-size the AWS fleet.![Multi-Site - Recovery Phase](https://jayendrapatil.com/wp-content/uploads/2016/03/Recovery-Phase-Multi-Site-Scenario.png)

## **AWS Certification Exam Practice Questions**

> - Questions are collected from Internet and the answers are marked as per my knowledge and understanding (which might differ with yours).
> - AWS services are updated everyday and both the answers and questions might be outdated soon, so research accordingly.
> - AWS exam questions are not updated to keep up the pace with AWS updates, so even if the underlying feature has changed the question might not be updated
> - Open to further feedback, discussion and correction.

1. Which of these Disaster Recovery options costs the least?
    1. **Pilot Light** (most systems are down and brought up only after disaster)
    2. Fully Working Low capacity Warm standby
    3. Multi site Active-Active
2. Your company currently has a 2-tier web application running in an on-premises data center. You have experienced several infrastructure failures in the past two months resulting in significant financial losses. Your CIO is strongly agreeing to move the application to AWS. While working on achieving buy-in from the other company executives, he asks you to develop a disaster recovery plan to help improve Business continuity in the short term. He specifies a target Recovery Time Objective (RTO) of 4 hours and a Recovery Point Objective (RPO) of 1 hour or less. He also asks you to implement the solution within 2 weeks. Your database is 200GB in size and you have a 20Mbps Internet connection. How would you do this while minimizing costs?
    1. Create an EBS backed private AMI which includes a fresh install or your application. Setup a script in your data center to backup the local database every 1 hour and to encrypt and copy the resulting file to an S3 bucket using multi-part upload (while AMI is a right approach to keep cost down, Upload to S3 very Slow)
    2. Install your application on a compute-optimized EC2 instance capable of supporting the application’s average load synchronously replicate transactions from your on-premises database to a database instance in AWS across a secure Direct Connect connection. (EC2 running in Compute Optimized as well as Direct Connect is expensive to start with also Direct Connect cannot be implemented in 2 weeks)
    3. Deploy your application on EC2 instances within an Auto Scaling group across multiple availability zones asynchronously replicate transactions from your on-premises database to a database instance in AWS across a secure VPN connection. (While VPN can be setup quickly asynchronous replication using VPN would work, running instances in DR is expensive)
    4. **Create an EBS backed private AMI that includes a fresh install of your application. Develop a Cloud Formation template which includes your AMI and the required EC2. Auto-Scaling and ELB resources to support deploying the application across Multiple Availability Zones. Asynchronously replicate transactions from your on-premises database to a database instance in AWS across a secure VPN connection. (**Pilot Light approach with only DB running and replicate while you have preconfigured AMI and autoscaling config**)**
3. You are designing an architecture that can recover from a disaster very quickly with minimum down time to the end users. Which of the following approaches is best?
    1. Leverage Route 53 health checks to automatically fail over to backup site when the primary site becomes unreachable
    2. Implement the Pilot Light DR architecture so that traffic can be processed seamlessly in case the primary site becomes unreachable
    3. **Implement either Fully Working Low Capacity Standby or Multi-site Active-Active architecture so that the end users will not experience any delay even if the primary site becomes unreachable**
    4. Implement multi-region architecture to ensure high availability
4. Your customer wishes to deploy an enterprise application to AWS that will consist of several web servers, several application servers and a small (50GB) Oracle database. Information is stored, both in the database and the file systems of the various servers. The backup system must support database recovery, whole server and whole disk restores, and individual file restores with a recovery time of no more than two hours. They have chosen to use RDS Oracle as the database. Which backup architecture will meet these requirements?
    1. Backup RDS using automated daily DB backups. Backup the EC2 instances using AMIs and supplement with file-level backup to S3 using traditional enterprise backup software to provide file level restore (RDS automated backups with file-level backups can be used)
    2. Backup RDS using a Multi-AZ Deployment Backup the EC2 instances using AMIs, and supplement by copying file system data to S3 to provide file level restore (Multi-AZ is more of an Disaster recovery solution)
    3. Backup RDS using automated daily DB backups. Backup the EC2 instances using EBS snapshots and supplement with file-level backups to Amazon Glacier using traditional enterprise backup software to provide file level restore (Glacier not an option with the 2 hours RTO)
    4. Backup RDS database to S3 using Oracle RMAN. Backup the EC2 instances using AMIs, and supplement with EBS snapshots for individual volume restore. (Will use RMAN only if Database hosted on EC2 and not when using RDS)
5. Which statements are true about the Pilot Light Disaster recovery architecture pattern?
    1. Pilot Light is a hot standby (Cold Standby)
    2. **Enables replication of all critical data to AWS**
    3. **Very cost-effective DR pattern**
    4. **Can scale the system as needed to handle current production load**
6. An ERP application is deployed across multiple AZs in a single region. In the event of failure, the Recovery Time Objective (RTO) must be less than 3 hours, and the Recovery Point Objective (RPO) must be 15 minutes. The customer realizes that data corruption occurred roughly 1.5 hours ago. What DR strategy could be used to achieve this RTO and RPO in the event of this kind of failure?
    1. **Take hourly DB backups to S3, with transaction logs stored in S3 every 5 minutes**
    2. Use synchronous database master-slave replication between two availability zones. (Replication won’t help to backtrack and would be sync always)
    3. Take hourly DB backups to EC2 Instance store volumes with transaction logs stored In S3 every 5 minutes. (Instance store not a preferred storage)
    4. Take 15 minute DB backups stored in Glacier with transaction logs stored in S3 every 5 minutes. (Glacier does not meet the RTO)
7. Your company’s on-premises content management system has the following architecture:  
    – Application Tier – Java code on a JBoss application server  
    – Database Tier – Oracle database regularly backed up to Amazon Simple Storage Service (S3) using the Oracle RMAN backup utility  
    – Static Content – stored on a 512GB gateway stored Storage Gateway volume attached to the application server via the iSCSI interfaceWhich AWS based disaster recovery strategy will give you the best RTO?
    1. **Deploy the Oracle database and the JBoss app server on EC2. Restore the RMAN Oracle backups from Amazon S3. Generate an EBS volume of static content from the Storage Gateway and attach it to the JBoss EC2 server.**
    2. Deploy the Oracle database on RDS. Deploy the JBoss app server on EC2. Restore the RMAN Oracle backups from Amazon Glacier. Generate an EBS volume of static content from the Storage Gateway and attach it to the JBoss EC2 server. (Glacier does help to give best RTO)
    3. Deploy the Oracle database and the JBoss app server on EC2. Restore the RMAN Oracle backups from Amazon S3. Restore the static content by attaching an AWS Storage Gateway running on Amazon EC2 as an iSCSI volume to the JBoss EC2 server. (No need to attach the Storage Gateway as an iSCSI volume can just create a EBS volume)
    4. Deploy the Oracle database and the JBoss app server on EC2. Restore the RMAN Oracle backups from Amazon S3. Restore the static content from an AWS Storage Gateway-VTL running on Amazon EC2 (VTL is Virtual Tape library and doesn’t fit the RTO)

## References
- Whitepaper available @ [AWS Disaster Recovery whitepaper](https://d1.awsstatic.com/whitepapers/aws-disaster-recovery.pdf)

<iframe loading="lazy" title="AWS re: Invent STG 202: How to do Backup and Disaster Recovery in the Cloud" width="656" height="369" src="https://www.youtube.com/embed/Aj5SX_w26Tw?feature=oembed&amp;enablejsapi=1" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen="" id="yinote-youtube-iframe"></iframe>