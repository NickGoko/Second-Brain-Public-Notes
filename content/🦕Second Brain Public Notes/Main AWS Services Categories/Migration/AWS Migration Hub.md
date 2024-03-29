---
tags:
  - cloud/aws
---

# FAQ
## General

**Q: What is AWS Migration Hub?**

AWS Migration Hub provides access to the tools you need to collect and inventory your existing IT assets based on actual usage, analyze application components and infrastructure dependencies, and group resources into applications. You can generate migration strategy and Amazon Elastic Compute Cloud (EC2) instance recommendations for business case and migration planning, track the progress of application migrations to AWS, and modernize applications already running on AWS.  

**Q: Why should I use AWS Migration Hub?**

AWS Migration Hub is the one destination for cloud migration and modernization, giving you the tools you need to accelerate and simplify your journey with AWS. If you’re making the case for cloud within your organization; planning, executing, and tracking a portfolio of applications migrating to AWS; or modernizing applications currently running on AWS, Migration Hub can help with your cloud transformation journey.  

**Q: What migration tools integrate with AWS Migration Hub?**

AWS Application Migration Service, AWS Server Migration Service, AWS Database Migration Service, and ATADATA ATAmotion are integrated with AWS Migration Hub and automatically report migration status to Migration Hub. See the [Migration Hub Documentation](http://docs.aws.amazon.com/migrationhub/latest/ug/) for more details about authorizing tools to send status to Migration Hub.  

**Q: How does AWS Migration Hub help me track the progress of my application migrations?**

AWS Migration Hub helps you by providing visibility into your migration progress. You use one of the integrated migration tools and then return to the hub to see the status of your migration. You can group servers into applications once the migration has started or, you can discover and group your servers before you start.  

**Q: How does AWS Migration Hub help me understand my IT environment?**

AWS Migration Hub helps you understand your IT environment by letting you explore information collected by AWS discovery tools and stored in the AWS Application Discovery Service’s repository. With the repository populated, you can view technical specifications and performance information about the discovered resources in Migration Hub. You can export data from the Application Discovery Service repository, analyze it, and import server groupings as an “application”. Once grouped, the application grouping is used to aggregate the migration status from each migration tool used to migrate the servers and databases in the application.  

**Q: How much does it cost to use AWS Migration Hub?**

AWS Migration Hub is available to all AWS customers at no additional charge. You pay only for the cost of the migration tools you use and any resources being consumed on AWS.

All Refactor Spaces orchestrated resources (for example, Transit Gateway) are provisioned in your AWS account. Therefore, you pay for usage of Refactor Spaces plus any costs associated with provisioned resources. For more information, see [AWS Migration Hub pricing](https://aws.amazon.com/migration-hub/pricing/) for more details.

### Service Level Agreement (SLA)

**Q: What does your AWS Migration Hub Refactor Spaces Service Level Agreement guarantee?**

Our SLA guarantees a Monthly Uptime Percentage of at least 99.9% for AWS Migration Hub Refactor Spaces within a Region.  

**Q: How do I know if I qualify for a SLA Service Credit?**

You are eligible for a SLA credit for AWS Migration Hub Refactor Spaces if the Region that you are operating in has an Monthly Uptime Percentage of less than 99.9% during any monthly billing cycle. For full details on all of the terms and conditions of the SLA, as well as details on how to submit a claim, please see [https://aws.amazon.com/migration-hub/sla/refactor-spaces/](https://aws.amazon.com/migration-hub/sla/refactor-spaces/).  

## Getting Started

**Q: How do I get started with AWS Migration Hub?**

Follow the [Getting Started Guide](http://docs.aws.amazon.com/migrationhub/latest/ug/getting-started.html#gs-the-two-ways) in our documentation to get started.  

**Q: What is the Migration Hub home Region?**

Before using most features in Migration Hub (except Refactor Spaces), you need to select a Migration Hub home Region from the [Migration Hub Settings](https://console.aws.amazon.com/migrationhub/settings) page or by using the [Migration Hub Config API](https://docs.aws.amazon.com/migrationhub-home-region/latest/APIReference/Welcome.html). 

The data stored in the Migration Hub home Region provides a single repository of discovery and migration planning information for your entire portfolio and a single view of migrations into multiple AWS Regions. You can migrate into any Region supported by your migration tools and the migration status will appear in your selected Migration Hub home Region. See [the documentation](https://docs.aws.amazon.com/migrationhub/latest/ug/home-region.html) to learn more about the Migration Hub home region.

Once set, the Migration Hub home Region cannot be changed.  

**Q: What Regions can I migrate to using AWS Migration Hub?**

AWS Migration Hub helps you track the status of your migrations in all AWS Regions, provided your migration tools are available in that Region. The migration tools that integrate with Migration Hub (for example, AWS Application Migration Service and AWS Database Migration Service) send migration status to your selected Migration Hub home Region. The home Region is used to store your discovery and migration tracking data and is set prior to first use of the service. Migration status is aggregated from all destination Regions and visible in the home Region. Note that integrated tools will not send status unless you have authorized (connected) them on the Tools page of the Migration Hub console.  

**Q: Where is AWS Migration Hub available?**

AWS Migration Hub is available worldwide for tracking the progress of application migrations, regardless of where the application currently resides. Refer to the AWS Region Table for availability of Migration Hub tools for inventory collection, planning and recommendation, and modernization capabilities.  

**Q: How is access granted to AWS Migration Hub?**

AWS Migration Hub requires an AWS account role, which will be added automatically the first time you access the console as an admin user. Integrated migration tools can be authorized on the Tools page of the Migration Hub console. Refer to the [Authentication and Access Control](http://docs.aws.amazon.com/migrationhub/latest/ug/auth-and-access-control.html) section of the AWS Migration Hub User Guide for more details.  

## Discovering Servers and Grouping Applications

**Q: How does AWS Migration Hub help me understand my IT environment?**  

AWS Migration Hub helps you understand your IT environment by letting you explore information collected by AWS discovery tools and stored in the AWS Application Discovery Service repository. With the repository populated, you can view technical specifications and performance information about the discovered resources in Migration Hub, analyze it, visualize and tag server and application dependencies, and group servers into applications. You can also export data and import groupings as an “application.” Once grouped, the application grouping is used to aggregate the migration status from each migration tool used to migrate the servers and databases in the application.  

**Q: How do I view my IT portfolio in AWS Migration Hub?**

To view your IT assets in AWS Migration Hub, first you perform discovery using an AWS discovery tool or by migrating with an integrated migration tool. Then you can explore your environment from within Migration Hub. You can learn more about any resource found by clicking on the server ID shown on the Servers page of the Migration Hub console. You then see the server details page. If you used an AWS discovery tool to discover your servers, you will see collected data, including technical specifications and average utilization.  

**Q: How do I add resources into the Discovery Repository?**

When you first visit AWS Migration Hub, you’re prompted to perform discovery or start migrating. If you decide to start migrating without performing discovery, your application servers and database servers will appear as resources in Migration Hub as you migrate them with integrated migration tools that you’ve authorized in the Migration Hub console.

For discovery, you have two data collection options. If you have a VMware environment and prefer not to install an agent, you can use the AWS Application Discovery Service agentless collector. If you need more detailed information, you can install agents on your servers that collect a wide variety of information, including details about resource utilization, processes running on the server, and the server’s network dependencies. Process and network dependency information is available for export and analysis outside AWS Migration Hub. See the [Application Discovery Service User Guide](http://docs.aws.amazon.com/application-discovery/latest/userguide/what-is-appdiscovery.html) for more details on the AWS Discovery Collectors.

**Q: How do I group servers into an application?**

Before grouping servers into an application, you need to populate AWS Migration Hub’s Servers list. Servers are added to the Servers list whenever you run AWS discovery tools or by using an integrated migration tool. Once your Servers list is populated, select one or more resources on the Servers page in the Migration Hub console and then choose “Group as Application.” If you’re discovering servers using the AWS Discovery agent, you can also group them into applications from the network visualization tool. Select one or more servers from the network graph and choose “Group as application.”  

**Q: How do I view applications?**

You can visit the Applications page in the Migrate section of the AWS Migration Hub console to see the list of applications and their current migration status. Only resources that are grouped to applications using the Discover section’s Servers page or AWS SDK/CLI will appear on the Applications page. Applications can have one of three migration statuses: “not started,” “in progress,” and “completed.”  

**Q: Can I see applications created by other users within the same account?**

Yes. Applications created by any IAM user within an account will be visible to any other IAM users within the same account that are granted access to AWS Migration Hub. Any changes made will be visible to all users with permission.  

**Q: Can I see applications that exist in other AWS accounts?**

You access AWS Migration Hub using an IAM User associated with an AWS account. This only allows you to see details from your AWS account; you do not have visibility into other accounts.  

## Importing Servers and Applications

**Q: How does the AWS Migration Hub import feature work?**

You can access the AWS Migration Hub import feature either from the Migration Hub [console](https://console.aws.amazon.com/migrationhub/discover/tools/options) or by invoking the Application Discovery Service [APIs](https://docs.aws.amazon.com/application-discovery/latest/APIReference/API_StartImportTask.html). The imported data is stored in the Application Discovery Service data repository in encrypted format.

**Q: What kind of data can I import using the import template?**

Migration Hub import allows you to import server details, including server specifications, utilization, tags and applications that are associated with your servers. You can import data from any source as long as the data is populated using the Migration Hub CSV [import template](https://s3-us-west-2.amazonaws.com/aws.migrationhub.import/latest/import_template.csv).

**Q: I imported an incorrect file. Can I overwrite or delete it?  
**

Yes. You can delete an incorrect file by visiting the Discover > Tools > Imports section and then selecting the “Delete imported data” option. To overwrite an existing imported file, delete the file and upload a new file with the corrected records.  

**Q: Is there a limit on the number of import files that I can upload?**

No. There is no limit on the number of import files that you can upload. However, we do restrict the number of records and servers that you can import. For details, refer to the Migration Hub import [limits](https://docs.aws.amazon.com/migrationhub/latest/ug/limits.html) section in the documentation.

**Q: Do I need to pay for importing data?  
**

No. There is no charge for importing your data.

**Q: I don't have data for all the fields in the import template. Can I still import my data?**

Yes. You can import data even if you don’t have data populated for all the fields in the import template. For each row, if you populate your own matching key (“ExternalId”), import will use it to uniquely identify and import the records. If you don’t specify the matching key, for each row, import will use the values specified for “IPAddress,” “HostName,” “MACAddress,” or a combination of “VMware.MoRefId” and “VMware.vCenterId” to determine the uniqueness of a given server. Rows that don’t contain a value for the matching key (“ExternalId”) or for any of the above fields will not be imported.  

**Q: What are the criteria for identifying an incorrect record?**

Import does a data validation check for all the imported fields that are part of the CSV import template. For example, if the value of “IPAddress” is invalid, the import feature will flag that record as incorrect. In addition, an import record will be considered invalid and won’t be imported if it doesn’t have at least one of these fields populated: “ExternalId,” “MACAddress,” “HostName,” “IPAddress,” or a combination of “VMware.VCenterId” and “VMware.MoRefId.”  

## Generating EC2 Instance Recommendations

**Q: What is the EC2 instance recommendations feature?**

EC2 instance recommendations is a feature of AWS Migration Hub that analyzes the data collected from each on-premises server, including server specification, CPU, and memory utilization, to recommend the least expensive EC2 instance required to run the on-premises workload. You can also fine-tune recommendations by specifying preferences for AWS purchasing option, AWS Region, EC2 instance type exclusions, and CPU/RAM utilization metric (average, peak, or percentile).  

**Q: Do I need to install the AWS Application Discovery Service Discovery Connector or Discovery Agent to use the EC2 instance recommendations feature?**  

No. To use the EC2 instance recommendations feature, you need to ensure that on-premises server details are available in AWS Migration Hub. You can import existing server inventory information from a source such as a content management database (CMDB), or use the AWS Application Discovery Service to collect data directly from your environment.  

**Q: How does the EC2 instance recommendations feature provide a match for a given server?**

The EC2 instance recommendations feature recommends the most cost-effective EC2 instance type that can satisfy the given CPU and RAM requirements while taking into account your selected instance type preferences such as AWS purchasing option, AWS Region, EC2 instance type exclusions, and CPU/RAM utilization metric (average, peak, or percentile).  

**Q: Does the EC2 instance recommendations feature provide recommendations for Burstable Performance Instances?**

Yes. The EC2 instance recommendations feature provides recommendations for [Burstable Performance Instances](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/burstable-performance-instances.html#burstable-performance-instances-limits). It uses “average” and “peak” CPU data points to compute an estimated number of consumed CPU credits and associated cost to more accurately compare the projected price with other instance families.

**Q: What happens if I have discovery data from multiple sources for the same server in AWS Migration Hub? Which data source is used to calculate the EC2 instance recommendation for that server?**

If discovery data is available from multiple sources for the same server, the EC2 instance recommendations feature will use the most recent and complete data to provide an instance recommendation. For example, if you upload the CPU/RAM specification for a given server using Migration Hub import, a recommendation will be generated based on the imported data. If you then install the AWS Application Discovery Service (ADS) Discovery Agent on this server, the ADS agent will also capture the server specification details. The next time you request EC2 instance recommendations for that server, the feature will use the ADS agent-collected specifications to generate the recommendation, since the agent's data is more recent and complete.  

**Q: When should I use the EC2 instance recommendations feature in AWS Migration Hub compared to a more detailed cost assessment with TSO Logic?**

Right-sizing your compute resources is one dimension of understanding your total cost of ownership (TCO). Use the EC2 instance recommendation feature of Migration Hub when you want an understanding of your projected EC2 costs. We also offer a more detailed assessment, including optimizations for Microsoft licensing and storage costs, using TSO Logic, an AWS Company. Contact [AWS Sales](https://aws.amazon.com/contact-us) or an [AWS Partner](https://aws.amazon.com/partners) to learn more about this detailed assessment.  

## Tracking Migration Status

**Q: What migration tools integrate with AWS Migration Hub?**

AWS Application Migration Service, AWS Server Migration Service, AWS Database Migration Service, and ATADATA ATAmotion are integrated with AWS Migration Hub and automatically report migration status to Migration Hub. See the [Migration Hub documentation](http://docs.aws.amazon.com/migrationhub/latest/ug/) for more details about authorizing tools to send status to Migration Hub.  

**Q: How do I use AWS Migration Hub when migrating applications?**

After you’ve created one or more application groupings from servers discovered using AWS discovery tools or by starting to migrate using an integrated migration tool, you can start or continue to migrate the server or database outside Migration Hub. Return to Migration Hub to view the migration status of each resource in the application. 

To do this, visit that application’s page in the Migration Hub console. There, you will see a diagram with all the resources that make up the application as well as a table with more migration status details. For each resource, the general and detailed status is shown as both a diagram and a table. For instance, for a server being migrated by AWS Server Migration Service, its status may be reported as “In progress / replication starting,” “In progress / replication complete,” or “Competed / AMI created.” 

When the migration completes, Migration Hub also shows details about the resources that have been created by the migration. For servers migrated by AWS Application Migration Service, AWS Server Migration Service, and ATADATA, Migration Hub provides links to the AMIs created or running EC2 instances (depending on the tool). For databases migrated by AWS Database Migration Service, Migration Hub provides the Target Endpoint ID, which can be used as a search filter on the Database Migration Service console.  

**Q: Does AWS Migration Hub automatically migrate my applications for me?**

No. AWS Migration Hub does not automate the steps of the migration. It provides a single place for you to track the progress of the applications you are migrating.  

**Q: What do I need to do in order for my application’s migration progress to appear in AWS Migration Hub?**

To view migration progress in AWS Migration Hub, two things must be true. The resources that you’re migrating must be in the AWS Discovery repository, and you must use supported tools to perform the migration. If you start migrating without performing discovery with AWS Discovery Collectors, the servers or databases reported by supported migration tools will be automatically added to your AWS Application Discovery Service repository. Once they’re added, you can group these servers as applications and track their status in a single grouping as the migration progresses.

If you’re using a supported tool but not seeing the status in an application, first check the Updates page to verify that the tool’s status is being received. If the status is not appearing on the Updates page, check the Tools page to verify that you’ve authorized the tool to send status to the Migration Hub. If it’s not authorized, click “Authorize” to add the appropriate IAM permissions.

If the migration status appears on the Updates page, it could be that the resource is not grouped into an application. Visit the Servers page and group the server to an application. Then view the application from the Migrate/Applications page to see the migration status.  

**Q: What is the experience if I don’t do a strict re-host migration, moving the resources exactly from on-premises to AWS?**

AWS Migration Hub will show the status of the resource migrations that are done with supported tools, provided that the resource is grouped in an application. It doesn’t need to be a strict rehost migration. For instance, if you move the contents of a database using AWS Database Migration Service, you will see updates in Migration Hub if the server corresponding to the database migration is grouped in an application.  

**Q: What if I’m using a tool that isn’t integrated with AWS Migration Hub?  
**

Tools that are not integrated with AWS Migration Hub will not report status in the Migration Hub Management Console. You can still see the status of other resources in the application and the application level status or you can update the status via your own automation using the CLI or APIs.  

**Q: How can other tools publish status to AWS Migration Hub?**

Migration tools can publish your status to AWS Migration Hub by writing to the [AWS Migration Hub API](http://docs.aws.amazon.com/migrationhub/latest/ug/api-reference.html). Partners interested in onboarding must have achieved the Migration Competency through the AWS Competency Program. Learn more about the Competency Program and apply for the Migration Competency [here](https://aws.amazon.com/migration/partner-solutions/).  

## Strategy Recommendations

**Q: What is Strategy Recommendations?**

AWS Migration Hub’s Strategy Recommendations helps you easily build a migration and modernization strategy for your applications running on premises or in AWS. Strategy Recommendations provides guidance on the strategy and tools that help you migrate and modernize at scale.  

**Q: Why should I use Strategy Recommendations?  
**

Strategy Recommendations helps you identify a tailored migration and modernization strategy at scale and provides the tools and services to help you run the strategy. It also helps you identify the incompatibilities (anti-patterns) in the source code that need to be resolved to implement these recommendations.  

**Q: What migration and modernization options does Strategy Recommendations support?**

Strategy Recommendations supports analysis for potential rehost (EC2) and replatform (managed environments such as RDS and Elastic BeanStalk, Containers, and OS upgrades) options for applications running on Windows Server 2003 or above or a wide variety of Linux distributions, including Ubuntu, RedHat, Oracle Linux, Debian, and Fedora. Strategy Recommendations offers additional refactor analysis for custom applications written in C# and Java, and licensed databases (such as Microsoft SQL Server and Oracle).  

**Q: How do I get started with Strategy Recommendations?** 

Follow the [Getting Started Guide](https://docs.aws.amazon.com/migrationhub-strategy/latest/userguide/what-is-mhub-strategy.html) in our documentation to get started.  

## Incremental App Refactor

**Q: What is application transformation?**  

Application transformation is the process of refactoring, rearchitecting, and rewriting applications to maximize the availability, scalability, business agility, and cost optimization benefits of running in the cloud.  

**Q: What is Refactor Spaces?**  

Refactor Spaces helps you accelerate application refactoring to take full advantage of computing in AWS and simplifies app transformation by making it easy to manage the refactor process while operating in production. By using Refactor Spaces, you focus on the refactor of your applications, not the creation and management of the underlying infrastructure that makes refactoring possible. Refactor Spaces helps reduce the business risk of evolving applications into microservices or extending legacy applications that can’t be modified with new features written in microservices.  

**Q: Why should I use Refactor Spaces?**  

Refactor Spaces addresses a common pair of practical problems when transforming applications: setting up an infrastructure for application refactoring and operating evolving applications at scale. Refactor Spaces helps you combine existing applications and microservices into a single application while allowing different approaches for architecture and technology, team alignment, and process between the parts. Using Refactor Spaces, you can transform legacy applications or extend them with microservices that run on any AWS compute target (such as EC2, Amazon Elastic Container Service, Amazon Elastic Kubernetes Service, AWS Fargate, and AWS Lambda). Refactor Spaces provides significant time savings by creating an infrastructure for application refactoring in minutes.  

**Q: What kind of applications can I refactor?**  

Any application targeted for refactor, rewrite, or rearchitecture is a candidate for using Refactor Spaces as long as its external interface is an HTTP-based protocol and running in AWS (or it can be rehosted with Application Migration Service or replatformed first). Refactor Spaces is commonly used to refactor older legacy and monolithic applications, but it also helps you navigate the refactoring and rearchitecture of modern services and applications.  

**Q: How does Refactor Spaces work with other AWS services?**  

Refactor Spaces orchestrates other AWS services to create refactoring environments and stitch together existing applications and microservices into Refactor Spaces applications that are easier to operate while the app is evolving. Application refactoring environments are built using Transit Gateway, Resource Access Manager, and API Gateway. Using these, Refactor Spaces helps keep existing applications separate from microservices through a multi-account structure that is bridged together with networking for easy cross-account communication.  

**Q: What is a Refactor Spaces Environment?**  

A Refactor Spaces Environment provides a unified view of networking, applications, and services across AWS accounts and is the container for your existing application and new microservices. The environment orchestrates Transit Gateway, Resource Access Manager, and VPCs to bridge networking across accounts to simplify communication between old and new services. The account where an environment is created is the environment owner. The owner can share the environment with other AWS accounts and manages applications, services, and routes added to the environment.  

**Q: What is a Refactor Spaces Application?**  

A Refactor Spaces Application provides configurable request routing to your existing application and new microservices. Applications include a proxy that simplifies strangler fig refactoring in AWS. When creating an application inside an environment, Refactor Spaces orchestrates API Gateway, Network Load Balancer (NLB), and AWS Lambda resource policies. The application’s proxy and routing are used to keep underlying architecture changes transparent to app consumers.  

**Q: What is a Refactor Spaces Service?**  

A Refactor Spaces Service represents the endpoint of an existing application or a new microservice. Services can have a VPC with either a URL endpoint or an AWS Lambda endpoint. Refactor Spaces automatically bridges service VPCs together within an environment using Transit Gateway, and traffic is permitted between any AWS resources in service VPCs across all accounts in the environment. When setting a route to a service, if the service has a Lambda endpoint, traffic is routed using API Gateway’s Lambda integration. For services with a URL endpoint, traffic is routed using an API Gateway VPC Link and NLB target group.  

**Q: How do I start incremental app refactoring with Refactor Spaces?**  

Refactor Spaces can be used through the AWS Management Console, AWS SDK/CLI, or CloudFormation (CFN). Usually, you’ll want to start with at least two accounts—one for your existing application and one to own the Refactor Spaces environment and manage traffic routing between services. Your AWS accounts can be new or existing accounts that are standalone, part of an AWS Organization, or provisioned by AWS Control Tower. 

First, install the Refactor Spaces Service-Linked Role (SLR) in each AWS account you plan to use for refactoring either by visiting the Refactor Spaces console in the account or by using IAM’s console or API to create the SLR Next, create a Refactor Spaces Environment in the account chosen to be the environment owner and share the environment with other accounts. Once the other accounts accept the environment sharing invitation, Refactor Spaces automatically shares AWS resources (such as Transit Gateway) contained in the environment with the other designated accounts. 

Next, create your first application. The Refactor Spaces Application provides configurable request routing (through API Gateway) to Refactor Spaces Services, regardless of which account a service is in. After creating the application, create one or more services in it. Initially, all traffic will flow to the existing app, so create a default route that sends all traffic to the service representing the existing app. Over time, you’ll add routes to cut traffic over to business capabilities being served by new microservices.  

**Q: Can I privately access AWS Migration Hub Refactor Spaces APIs from my VPC without using public IP addresses?**

Yes, you can privately access Refactor Spaces APIs from your VPC (created using Amazon Virtual Private Cloud) by creating VPC Endpoints. With VPC Endpoints, the routing between the VPC and Refactor Spaces is handled by the AWS network without the need for an internet gateway, NAT gateway, or virtual private network (VPN) connection. The latest generation of [VPC Endpoints](https://docs.aws.amazon.com/systems-manager/latest/userguide/sysman-setting-up-vpc.html) used by Refactor Spaces is powered by AWS PrivateLink, a technology that enables private connectivity between AWS services using Elastic Network Interfaces (ENIs) with private IP addresses in your VPCs. To learn more about PrivateLink support, visit the [Refactor Spaces PrivateLink documentation](https://docs.aws.amazon.com/migrationhub-refactor-spaces/latest/userguide/vpc-interface-endpoints.html).

## Orchestrator

**Q: What is migration orchestration?**

Migration orchestration is a process automation mechanism that uses templates, synchronizes multiple tasks into a workflow, and manages dependencies to achieve the desired goal of a migration project.

**Q: What is AWS Migration Hub Orchestrator?**

AWS Migration Hub Orchestrator is designed to automate and simplify the migration of applications to AWS. Orchestrator helps you reduce migration costs and time by removing many of the manual tasks involved in migrating large-scale enterprise applications, managing dependencies between different tools, and providing visibility into migration progress in one place. Use predefined and customizable workflow templates in Orchestrator that offer a prescribed set of migration tasks, migration tools, and automation opportunities to orchestrate complex workflows and interdependent tasks, simplifying the process of migrating to AWS.

**Q: What are the benefits of using AWS Migration Orchestrator?**

Orchestrator helps you accelerate migrations, simplify the migration process, and adapt the migration tools and process for your use cases.  

- **Accelerate migrations:** Accelerate your application migrations using proven predefined workflow templates based on thousands of applications with similar patterns that AWS has migrated.
- **Simplify with automation:** Automate pre-migration tasks, migration workflows, and migration tasks across multiple tools such as AWS Application Discovery Service, AWS Application Migration Service, and AWS Launch Wizard for the same migration workflow to minimize the manual work.
- **Adapt and streamline:** Customize and reuse workflow templates by building on top of baseline recommendations and modifying the steps and dependencies to address the needs of specific workloads and use cases.

**Q: Why should I use AWS Migration Hub Orchestrator?**

Orchestrator simplifies and accelerates the migration of applications to AWS.  

- **Migrate applications using a prescriptive methodology:** You can start migrations quickly by using predefined workflow templates that are based on thousands of applications with similar patterns that AWS has migrated.
- **Customize your migration workflow:** You can customize your workflow by adding your own steps, dependencies, and automations to address the needs of your specific use cases.
- **Orchestrate pre-migration tasks in the source environments:** You often need to check migration readiness, install agents, or remove unnecessary log files that you don’t want to migrate to AWS. Performing these tasks manually on each on-premises server is a tedious and error-prone process. With Orchestrator, you can automate these tasks to save time and cost while reducing errors.
- **Orchestrate the migration tasks in different migration tools:** Your optimal migration process might involve the use of multiple tools, such as AWS Application Discovery Service, AWS Application Migration Service, or AWS Launch Wizard for the same migration workflow. With Orchestrator, you can orchestrate your migration tasks by reusing the inventory metadata, configuration specification, and environment context to minimize the inputs you need to provide in each of these tools. By automating the manual migration tasks, managing dependencies between different tools, and providing visibility into migration progress in one place, Orchestrator helps you reduce migration costs and time.
- **Configure, validate, and launch the migrated applications:** In large migrations, checking the status of instances, databases, and network connectivity; installing and uninstalling applications on migrated servers; and shutting down the staging environment result in extended cutover period and downtime. With Orchestrator, you can automate these routine migration steps to reduce the cutover time by more than 50%.

**Q: How do I use Orchestrator?**

You can access Orchestrator from the AWS Migration Hub console or the AWS Command Line Interface (CLI). Use Orchestrator to complete the prerequisites of discovering or importing source servers, grouping the discovered servers into applications, and installing a plugin in the source environment. Next, pick one of the predefined workflow templates to create a workflow to orchestrate the application migration. If you wish, you can also specify custom steps to be automated or manually completed as part of the workflow. Once you define the workflow, you can run, pause, or delete it. You can also track the status of the workflow at step level and step group level in Orchestrator.

**Q: What is a workflow template in Orchestrator?**

A workflow template is a playbook with a prescribed set of migration tasks, dependencies, suitable migration tools, and recommended automation opportunities. For example, the predefined workflow template for migrating SAP NetWeaver–based applications with HANA databases includes step-by-step tasks for automated validation of connectivity between source servers and plugins, the ability to provision a new SAP environment using AWS Launch Wizard, automated validation of source and target environments, automated migration of HANA database and applications, and post-migration validation.

**Q: Which predefined workflow templates are provided in Orchestrator?**

Orchestrator currently supports five predefined workflow templates that you can use. The first template helps you migrate SAP NetWeaver–based applications with HANA databases using AWS Launch Wizard and HANA System Replication. The second template helps you accelerate the rehosting of any applications using AWS Application Migration Service (MGN). The third and fourth templates help you replat form your SQL Server databases to Amazon RDS and rehost your SQL Server databases to Amazon EC2 using native backup and restore. The fifth template helps you import your on-premises virtual machine (VM) images to AWS with a console-based experience for generating Amazon Machine Image (AMI) from your VM image that you have built to meet your IT security, configuration management, and compliance requirements. All of these templates include predefined automation of tasks with an option to add new steps and automation scripts.  
