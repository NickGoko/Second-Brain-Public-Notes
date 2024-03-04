---
tags:
  - cloud/aws
---


![[Pasted image 20240215114208.png]]

![[Pasted image 20240215114305.png]]
<!--⚠️Imgur upload failed, check dev console-->

![[Pasted image 20240215120341.png]]

![[Pasted image 20240215120425.png]]

![[AWS Solutions Architect Skillbuilder#Database Migration]]

# FAQ
### General

**Q: What is AWS Database Migration Service?**  

AWS Database Migration Service (AWS DMS) is a managed migration and replication service that helps you move your databases and analytics workloads to AWS quickly and securely. The source database remains fully operational during the migration, minimizing downtime to applications that rely on the database.

The AWS Database Migration Service can assess, convert, and migrate your data to and from the most widely used commercial and open-source databases. AWS Database Migration Service supports homogeneous migrations such as Oracle to Oracle, as well as heterogeneous migrations between different databases, such as Oracle or Microsoft SQL Server to Amazon Aurora.

With AWS Database Migration Service, you can also continuously replicate data with low latency from a supported source to a supported target. For example, you can replicate from multiple sources to Amazon Simple Storage Service (Amazon S3) to build a highly available and scalable data lake solution.

You can also consolidate databases into a petabyte-scale data warehouse by streaming data to Amazon Redshift. Learn more about the supported source and target databases.

**Q: How do I get started with AWS Database Migration Service?**  

[Getting started with AWS Database Migration Service](https://aws.amazon.com/dms/getting-started/) is quick and simple. Most data replication tasks can be set up in less than 10 minutes.

Visit the AWS Database Migration Service section of the [AWS Management Console](https://aws.amazon.com/console/) and enter the Start Migration wizard. Specify your source and target endpoints, select an existing replication instance or create a new one, and accept the default schema mapping rules or define your own transformations. Data replication will start immediately after you complete the wizard.  

**Q: How much does AWS DMS cost?**  

AWS DMS is an affordable, low-cost option to migrate your databases and analytics workloads. You pay only for the replication instances and any additional log storage. Data transfer is free. You can find full pricing details on the [DMS pricing page](https://aws.amazon.com/dms/pricing/).  

**Q: How much does AWS DMS Schema Conversion cost?**  

AWS DMS Schema Conversion is free to use as a part of DMS. Pay only for the storage used.  

**Q. What are the database migration steps when using AWS Database Migration Service?**  

During a typical simple database migration, you will create a target database, migrate the database schema, set up the data replication process, initiate the full load and a subsequent change data capture and apply, and conclude with a switchover of your production environment to the new database once the target database is caught up with the source database.  

**Q. Is the database migration process using AWS DMS different for continuous data replication?**  

The only difference is in the last step (the production environment switchover), which is absent for continuous data replication. Your data replication task will run until you change or terminate it.  

**Q: Can I monitor the progress of a database migration task?**  

Yes. AWS Database Migration Service has a variety of metrics displayed in the AWS Management Console. It provides an end-to-end view of the data replication process, including diagnostic and performance data for each point in the replication pipeline.

AWS Database Migration Service also integrates with other AWS services such as [CloudTrail](https://aws.amazon.com/cloudtrail/) and [CloudWatch](https://aws.amazon.com/cloudwatch/) Logs. You can also leverage the [AWS Database Migration Service API](https://docs.aws.amazon.com/dms/latest/APIReference/Welcome.html) and [AWS Command Line Interface (AWS CLI)](https://aws.amazon.com/cli/) to integrate with your existing tools or build custom monitoring tools to suit your specific needs.  

**Q: How do I integrate AWS Database Migration Service with other applications?**  

AWS Database Migration Service provides a provisioning API that allows creating a replication task directly from your development environment, or scripting their creation at scheduled times during the day.

The service API and CLI allows developers and database administrators to automate the creation, restart, management and termination of replication tasks.  

### Supported Sources and Target Engines

**Q: What source databases and target databases does AWS Database Migration Service support?**  
AWS Database Migration Service (DMS) supports a range of homogeneous and heterogeneous data replications.

Either the source or the target database (or both) need to reside in RDS or on EC2. Replication between on-premises to on-premises databases is not supported.

- [Supported DMS sources](https://docs.aws.amazon.com/dms/latest/userguide/CHAP_Introduction.Sources.html)
- [Supported DMS targets](https://docs.aws.amazon.com/dms/latest/userguide/CHAP_Introduction.Targets.html)

**Q: What sources and targets engines does AWS DMS Serverless support?**  

AWS DMS Serverless supports popular databases and analytics services, such as Oracle, Microsoft SQL Server, PostgreSQL, MySQL, Amazon Redshift, Amazon RDS, Amazon Aurora, and more. See the full [list of supported engines](https://docs.aws.amazon.com/dms/latest/userguide/data-migrations.html).

**Q: What sources and targets does AWS DMS Schema Conversion support?**  

AWS DMS Schema Conversion supports a range of popular databases, which are listed  [here](https://docs.aws.amazon.com/dms/latest/userguide/CHAP_SchemaConversion.html#schema-conversion-data-providers).  

**Q: What sources and targets does AWS Schema Conversion Tool support?**  

AWS Schema Conversion Tool (AWS SCT) supports a range of database and data warehouse conversions, which are listed  [here](https://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/CHAP_Welcome.html).

**Q: What sources and targets does AWS DMS homogeneous data migrations support?**

[See the full list of supported engines](https://docs.aws.amazon.com/dms/latest/userguide/data-migrations.html) for AWS DMS homogeneous data migrations, including PostgreSQL and MySQL.  

### Schema Conversion

**Q. Will AWS Database Migration Service help me convert my Oracle PL/SQL and SQL Server T-SQL code to Amazon RDS for MySQL and Amazon RDS for PostgreSQL stored procedures?**  

Yes, part of the AWS Database Migration Service is [AWS DMS Schema Conversion (DMS SC)](https://docs.aws.amazon.com/dms/latest/userguide/CHAP_SchemaConversion.html) which automates the conversion of Oracle PL/SQL and SQL Server T-SQL code to equivalent code in the Amazon RDS for MySQL dialect of SQL or the equivalent PL/pgSQL code in PostgreSQL.  
  
When a code fragment cannot be automatically converted to the target language, DMS SC will clearly document the locations that require manual input from the application developer. A downloadable version, called [AWS Schema Conversion Tool (AWS SCT)](https://aws.amazon.com/dms/schema-conversion-tool/), is also available.

**Q: Does AWS Database Migration Service migrate the database schema for me?**

Yes, when you need to use a more customizable schema migration process (for example, when you are migrating your production database and need to move your stored procedures and secondary database objects), you can use the built-in Schema Conversion feature of AWS DMS for heterogeneous migrations. Alternative options include downloading AWS Schema Conversion Tool or using the schema export tools native to the source engine, if you are doing homogeneous migrations such as:

1. SQL Server Management Studio's Import and Export Wizard.
2. Oracle's SQL Developer Database Export tool or script the export using the dbms\_metadata package.
3. MySQL's Workbench Migration Wizard.  
    

**Q. How are AWS Database Migration Service (AWS DMS) and AWS Schema Conversion Tool (AWS SCT) related?**

AWS DMS and AWS SCT work in conjunction to both migrate databases and support ongoing replication for a variety of uses such as populating data lakes and warehouses, synchronizing systems, and so on. AWS SCT can copy database schemas for homogeneous migrations and convert them for heterogeneous migrations. The schemas can be between databases (for example, Oracle to PostgreSQL), or between data warehouses (for example, Netezza to Amazon Redshift).

Once a schema has been created on an empty target, depending on the volume of data and/or supported engines, either AWS DMS or AWS SCT are then used to move the data. AWS DMS traditionally moves smaller relational workloads (<10 TB), whereas AWS SCT is primarily used to migrate large data warehouse workloads. AWS DMS supports ongoing replication to keep the target in sync with the source; AWS SCT does not.  
  

### Data Replication

**Q: In addition to one-time data migration, can I use AWS Database Migration Service for continuous data replication?**  

Yes, you can use AWS Database Migration Service for one-time data migration into RDS and EC2-based databases as well as for continuous data replication. AWS Database Migration Service will capture changes on the source database and apply them in a transactionally consistent way to the target.

Continuous replication can be done from your data center to the databases in AWS or in the reverse, replicating to a database in your data center from a database in AWS. Ongoing continuous replication can also be done between homogeneous or heterogeneous databases. For ongoing replication, it would be preferable to use Multi-AZ for high availability.

**Q. Why should I use AWS Database Migration Service instead of my own self-managed replication solution?**  

AWS Database Migration Service is very simple to use. Replication tasks can be set up in minutes instead of hours or days, compared to the self-managed replication solutions that have to be installed and configured. AWS Database Migration Service monitors for replication tasks, network or host failures, and automatically provisions a host replacement in case of failures that can’t be repaired. Users of AWS Database Migration Service don’t have to overprovision capacity and invest in expensive hardware and replication software, as they typically have to do with self-managed solutions. 

With AWS Database Migration Service users can take advantage of on-demand pricing and scale their replication infrastructure up or down, depending on the load. AWS Database Migration Service data replication integrates tightly with the AWS Schema Conversion Tool, simplifying heterogeneous database migration projects.  

**Q: Can I replicate data from encrypted data sources?**  

Yes, AWS Database Migration Service can read and write from and to encrypted databases. AWS Database Migration Service connects to your database endpoints on the SQL interface layer. If you use the Transparent Data Encryption features of Oracle or SQL Server, AWS Database Migration Service will be able to extract decrypted data from such sources and replicate it to the target.

The same applies to storage-level encryption. As long as AWS Database Migration Service has the correct credentials to the database source, it will be able to connect to the source and propagate data (in decrypted form) to the target.

We recommend using encryption-at-rest on the target to maintain the confidentiality of your information. If you use application-level encryption, the data will be transmitted through AWS Database Migration Service as is, in encrypted format, and then inserted into the target database.  

### Serverless

**Q: What is AWS DMS Serverless?**

AWS Database Migration Service (AWS DMS) Serverless automatically provisions, monitors, and scales resources to make database and analytics migrations to AWS easier and more cost effective. With AWS DMS Serverless, you no longer have to overprovision migration resources or manually monitor and scale resources for continuous data replication. AWS DMS Serverless optimizes resources to meet demand, so you’re only paying for the resources used. This makes it helpful for popular use cases such as continuous data replication, as well as complex heterogeneous migrations between different source and target engines.

**Q: Can I use AWS DMS Serverless for continuous replication?**

Yes, AWS DMS Serverless can be used for continuous replication. DMS Serverless supports both Single-AZ and Multi-AZ deployment options.

**Q. Which DMS feature should I use for homogeneous database migrations?**

For homogeneous migrations, we recommend using DMS built-in native tooling for supported engines, due to its familiarity and seamless migration. You do not need to provision or monitor the migration, and you only pay for the hours used during the migration. To check supported engines, go to [DMS documentation page](https://docs.aws.amazon.com/dms/latest/userguide/data-migrations.html).

For heterogeneous migrations or continuous data replications with data fluctuations, we recommend using AWS DMS Serverless as it automatically monitors and scales resources to meet demand without manual intervention or over provisioning resources, saving you time and cost. On-demand instances, on the other hand, are good for predictable, stable data transfers, as they can be rightsized for performance and cost. See [AWS DMS Serverless documentation](https://docs.aws.amazon.com/dms/latest/userguide/CHAP_Serverless.html) for supported engines.

**Q. Is AWS DMS homogeneous data migration serverless?**

Yes, AWS DMS built-in native tooling for homogeneous data migration is serverless. It does not use replication instances and will automatically monitor and scale migration resources as needed to provide a seamless migration.

### Migration Planning

**Q: What is AWS DMS Fleet Advisor?  
**

[AWS DMS Fleet Advisor](https://aws.amazon.com/dms/fleet-advisor/) is a free, fully managed capability of AWS Database Migration Service (AWS DMS). It automates migration planning and helps you migrate database and analytics fleets to the cloud at scale with minimal effort. For discovery of on-premises databases, you can use a standalone AWS DMS Fleet Advisor collector or the database and analytics collection module of the [AWS Application Discovery Service (ADS) Agentless Collector.](https://docs.aws.amazon.com/application-discovery/latest/userguide/agentless-collector.htm)

**Q: When should I use AWS DMS Fleet Advisor versus AWS Application Discovery Service and Migration Evaluator?**  

[AWS DMS Fleet Advisor](https://aws.amazon.com/dms/fleet-advisor/) is intended for users looking to migrate a large number of database and analytics servers to AWS. When you are ready to migrate your database and analytics workloads to target services in AWS, you should [use AWS DMS Fleet Advisor to discover and analyze](https://docs.aws.amazon.com/dms/latest/userguide/CHAP_FleetAdvisor.html) your Online Transaction Processing (OLTP) and Online Analytical Processing (OLAP) database workloads. Fleet Advisor allows you to build a customized migration plan by determining the complexity of migrating your source databases to target services in AWS.

The [AWS Application Discovery Service](https://aws.amazon.com/application-discovery/) (ADS) and [Migration Evaluator](https://aws.amazon.com/migration-evaluator/) are targeted for broad-based compute and attached block storage discovery. The Migration Evaluator is used by customers starting their migration journey who are looking for a data-driven business case for AWS. ADS is used to feed the [AWS Migration Hub](https://aws.amazon.com/migration-hub/) to visualize server to server dependencies, create application groups, and track migration progress.  

**Q: When should I use the AWS DMS Fleet Advisor collector versus AWS Application Discovery Service?**

For most customers, we recommend using the [AWS Application Discovery Service (ADS) Agentless Collector](https://docs.aws.amazon.com/application-discovery/latest/userguide/agentless-collector.html) in [regions where available](https://aws.amazon.com/about-aws/global-infrastructure/regional-product-services/), as it supports server migration through AWS Migration Hub as well as allows you to discover on-premises databases. For all other regions, we recommend using the AWS DMS Fleet Advisor collector. Database metadata and utilization metrics collected from both the standalone AWS DMS Fleet Advisor collector and the AWS ADS Agentless Collector will be available in [AWS DMS Fleet Advisor.](https://aws.amazon.com/dms/fleet-advisor/)

Use the AWS ADS Agentless Collector if you have a [VMware vCenter Server environment,](https://docs.aws.amazon.com/application-discovery/latest/userguide/agentless-collector.html) otherwise the AWS DMS Fleet Advisor collector can be installed on a [Microsoft Windows Server 2012 or higher.](https://docs.aws.amazon.com/dms/latest/userguide/fa-data-collectors-install.html)  
 

### Lifecycle Policy

**Q: What is the AWS DMS support lifecycle policy?  
**

The AWS DMS support lifecycle policy specifies how long support will be available for each DMS version, from when a version is released to when it is no longer supported.  

**Q: What is the purpose of the support lifecycle policy?**  

The support lifecycle policy aims to provide predictable and consistent guidelines for support for each AWS DMS version release. The guidelines will benefit customers to strategically plan their migration and upgrades.  

**Q: What are the support timelines for AWS DMS releases?**

The end of support date for each DMS version release will start 18 months after its initial release. For the latest schedule of all existing DMS versions, please go to the new section "Support lifecycle policy" from your DMS console.   

**Q: How are the timelines communicated?**  

Support timelines for each AWS DMS version release will be included in the associated [DMS Release Notes](https://docs.aws.amazon.com/dms/latest/userguide/CHAP_ReleaseNotes.html), as well as in the new “Support lifecycle policy” section in your DMS console. If you are using any versions that will reach end of support within 90 days you will see an alert next to the Engine Version under "Replication Instance". In addition, AWS will send DMS instance owners a quarterly email reminder if they are running a release that will no longer be supported in the following quarter.

**Q: When did the AWS DMS release support lifecycle policy go into effect?** 

The policy went into effect on January 1st, 2023. All instances that have reached the end of support date of 18 months after release will be automatically upgraded to the latest preferred DMS version regardless of the automatic upgrade setting.

**Q: What is a preferred DMS version?**

The DMS service designates one of the newest releases of DMS as the preferred version. This preferred version is the version that will be used for automatic upgrades and is the default choice for customers creating a new DMS instance.

**Q: How do you define the latest preferred AWS DMS version?**

New DMS versions are only released after extensive testing. After the release of a new  version, the DMS service team closely monitors reliability metrics and customer feedback. Once we are confident that there are no significant issues with the new release, we will mark that release as the new preferred version which you can find when selecting the version upon creation of the replication instance.

**Q: Is the support policy term the same for major and minor version of DMS?**

AWS DMS does not differentiate between a major and minor version release, and does not plan to have a different support policy. 

**Q: Will AWS DMS automatically update my instance to latest preferred version?**

If you enable auto upgrade, your replication instance will be automatically updated to the latest preferred version as it becomes available. If you opt out of the auto-upgrade, AWS DMS will update your instances to the latest preferred version once the end-of-life date has been reached, which will be communicated via email and console notification prior to upgrade. You can learn more about how to upgrade the DMS engine version using the AWS Console or AWS CLI in this [DMS User Guide](https://docs.aws.amazon.com/dms/latest/userguide/CHAP_ReplicationInstance.EngineVersions.html).

**Q: How do I enable auto-upgrade?**

The auto upgrade setting in your replication instance is turned on by default. To check or make any modification to this setting using AWS CLI, DMS API, or console you can use  this [Modifying a Replication Instance guide](https://docs.aws.amazon.com/dms/latest/userguide/CHAP_ReplicationInstance.Modifying.html).

**Q: What happens to your task during the upgrade?** 

If the tables in the migration task are in the replicating ongoing changes phase (CDC), AWS DMS pauses the task while the patch is applied. The migration then continues from where it was left off when the patch was applied.

If AWS DMS is running a full load operation when the patch is applied, AWS DMS restarts the migration for the table. These upgrades will occur during the maintenance window specified for the replication instance. You can find more details on [Working with the AWS DMS Maintenance Window guide](https://docs.aws.amazon.com/dms/latest/userguide/CHAP_ReplicationInstance.MaintenanceWindow.html#CHAP_ReplicationInstance.MaintenanceWindow.Effect).

**Q: I have instances on a version that is not covered in support. How does this affect my existing instances and jobs? What do you recommend as next steps?**

After the end of life date for a DMS version has passed, AWS DMS may remove the release version from the console and upgrade your replication instance to the latest preferred version in order to continue providing support. We recommend you to upgrade to the latest AWS DMS release as soon as possible.