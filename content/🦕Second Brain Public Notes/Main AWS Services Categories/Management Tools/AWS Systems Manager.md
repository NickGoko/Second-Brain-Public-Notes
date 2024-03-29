---
tags:
  - cloud/aws
review-frequency: high
reviewed: 2023-12-16
---
![](https://i.imgur.com/OI03kF9.png)  

![](https://i.imgur.com/DG7y0SZ.png)

![](https://i.imgur.com/qunFfEP.png) 

![](https://i.imgur.com/S6NmETv.png)


<mark style="background: #BBFABBA6;">AWS Systems Manager is an AWS service that provides visibility and control of infrastructure on AWS.</mark>

AWS Systems Manager provides a unified interface through which you can view operational data from multiple AWS services.

<mark style="background: #FFB86CA6;">AWS Systems Manager allows you to automate operational tasks across your AWS resources.</mark>

<mark style="background: #D2B3FFA6;">Formally known as SSM, AWS Systems Manager is a central hub to control and view your entire AWS infrastructure.  
</mark>  
It can aid with security within your account and helps automate remedial tasks to ensure your environment is as compliant as possible.

<mark style="background: #BBFABBA6;">AWS Systems manager is a powerful service which allows you to have a holistic view of all of the services you are using to view and control your infrastructure on AWS.  
</mark>  
AWS Systems Manager provides a unified interface through which you can view operational data from multiple AWS services.

<mark style="background: #D2B3FFA6;">With AWS Systems Manager, you can group resources, like Amazon EC2 instances, Amazon S3 buckets, or Amazon RDS instances, by application, view operational data for monitoring and troubleshooting, and take action on your groups of resources.</mark>

With AWS Systems Manager, you can select a resource group and view its recent API activity, resource configuration changes, related notifications, operational alerts, software inventory, and patch compliance status.

<mark style="background: #D2B3FFA6;">You can also take action on each resource group depending on your operational needs.</mark>

**AWS Systems Manager**<mark style="background: #BBFABBA6;"> simplifies resource and application management, shortens the time to detect and resolve operational problems, and makes it easy to operate and manage your infrastructure securely at scale.</mark>

## Systems Manager Components

**AWS Systems Manager Inventory Manager** <mark style="background: #D2B3FFA6;">Automates the process of collecting software inventory from managed instances.</mark>

<mark style="background: #BBFABBA6;">You can simply specify the types of metadata to be collected, the instances from which the metadata should be gathered, and the schedule for collecting metadata.</mark>

AWS Systems Manager collects information about your instances and the software installed on them, helping you to understand your system configurations and installed applications.

The gathered data enables you to manage application assets, track licenses, monitor file integrity, discover applications not installed by a traditional installer, and more.

#### Configuration Compliance

**AWS Systems Manager**<mark style="background: #D2B3FFA6;"> lets you scan your managed instances for patch compliance and configuration inconsistencies.  
</mark>  
You can collect and aggregate data from multiple AWS accounts and Regions, and then drill down into specific resources that aren’t compliant.

<mark style="background: #ABF7F7A6;">By default, AWS Systems Manager displays data about patching and associations.</mark> You can also customize the service and create your own compliance types based on your requirements.

#### AWS Systems Manager Automation

<mark style="background: #BBFABBA6;">AWS Systems Manager allows you to safely automate common and repetitive IT operations and management tasks across AWS resources.</mark>

With Systems Manager, <mark style="background: #ADCCFFA6;">you can create JSON/YAML documents that specify a specific list of tasks or use community published documents.</mark>

<mark style="background: #FFB86CA6;">These documents can be executed directly through the AWS Management Console, CLIs, and SDKs, scheduled in a maintenance window, or triggered based on changes to AWS resources through Amazon CloudWatch Events.</mark>

You can track the execution of each step in the documents as well as require approvals for each step.

You can also incrementally roll out changes and automatically halt when errors occur.

#### AWS Systems Manager Run Command

By using Run Command, you can automate common administrative tasks and make one-time configuration changes in bulk, and at enterprise scale.

This essentially prevents you from having to jump into every one of your instances and run the same command hundreds of times.

It is all actively managed within the console and there is an easy to use console in which to administer your commands, as well as a CLI or through the AWS SDK.

Example tasks include: stopping, restarting, terminating, and resizing instances. Attaching and detaching EBS volumes, creating snapshots and you can install or bootstrap an application, build a deployment pipeline etc.

Commands can be applied to a group of systems based on AWS instance tags or manual selection.

The commands and parameters are defined in an AWS Systems Manager document.

Commands can be issued using the AWS Console, AWS CLI, AWS Tools for Windows PowerShell, the AWS Systems Manager API, or Amazon SDKs.

#### AWS Systems Manager Session Manager

<mark style="background: #D2B3FFA6;">AWS Systems Manager provides safe; secure and remote management of your instances at scale without logging into your servers, replacing the need for bastion hosts, SSH, or remote PowerShell.</mark>

It provides a simple way of <mark style="background: #ABF7F7A6;">automating common administrative tasks across groups of instances</mark> such as **registry edits**, **user management**, and **software and patch installations**.

Session Manager provides a command terminal for Linux instances and Windows PowerShell terminal for Windows instances.

Session Manager not only provides a fully auditable terminal environment, but you can administer access to SSH sessions without having to open any ports, strongly enhancing your security posture. You can simply enable the least privileged IAM permissions to the Session Manager console and allow your developers to maximize their efficiency and effectiveness.

<mark style="background: #083CA4A6;">All actions taken with AWS Systems Manager are recorded by AWS CloudTrail, allowing you to audit changes throughout your environment.</mark>

CloudTrail can intercept StartSession events using Session Manager.

Compared to SSH:

• Do not need to open port 22.

• Do not need bastion hosts for management.

• All commands are logged to S3 / CloudWatch.

• Secure shell access is authenticated using IAM user accounts, not key pairs.

#### Incident Manager

You can automate solutions in the **Incident Manager** console to help bring the appropriate internal resources to your attention.

AWS Chatbot links designated chat channels to AWS Incident Manager, and Automation runbooks are executed for AWS Systems Manager using the Incident Manager.

Responders are engaged via SMS and phone calls in predefined response plans.

By suggesting action items based on Amazon’s post-incident analysis template, Incident Manager helps you improve service reliability. For example, you can automate a runbook step or add a new alarm after an incident.

#### Systems Manager Patch Manager

Patch Manager enables the automated patching your EC2 instances. It includes security patches, as well as other patches for both your applications and your operating systems.

Patch Manager uses what are known as patch baselines, which involve the definition of rules for auto-approving patches, as well as declined patches. By scheduling patching as a maintenance window task in Systems Manager, you can easily install patches on a regular basis.

Understanding the state of your servers that are part of your Systems Manager fleet is paramount to enabling a compliant and secure workload of your applications and your servers.

The process from end-to-end consists of obtaining metadata about your managed Systems Manager nodes (on-premise, EC2 etc.) Regardless of if you are using Systems Manager in the cloud or Systems Manager on-premise you store this metadata in a centralized repository (an S3 Bucket). You can from there query the metadata using native tools to gain insights into trends across your nodes in a number of different categories.

This aggregation of metadata can include multiple regions and multiple accounts, all in one place, and permissions to this sub-service can be granularly assigned using IAM as well as Service Control Policies for AWS Organizations.

#### AWS Systems Manager Parameter Store

AWS Systems Manager provides a centralized store to manage your configuration data, whether plain-text data such as database strings or secrets such as passwords.

This allows you to separate your secrets and configuration data from your code. Parameters can be tagged and organized into hierarchies, helping you manage parameters more easily.

For example, you can use the same parameter name, “db-string”, with a different hierarchical path, “dev/db-string” or “prod/db-string”, to store different values.

AWS Systems Manager is integrated with AWS Key Management Service (KMS), allowing you to automatically encrypt the data you store.

You are able to store these secrets in a way in which you don’t have to manage any servers, making the entire process much easier.

If your data is also kept separate from your code, you will be in a much better position security wise, as you are enabling separation.

You can also control user and resource access to parameters using AWS Identity and Access Management (IAM).

Parameters can be referenced through other AWS services, such as Amazon Elastic Container Service, AWS Lambda, and AWS CloudFormation.

#### AWS Systems Manager Distributor

Distributor is an AWS Systems Manager feature that enables you to securely store and distribute software packages in your organization.

You can use Distributor with existing Systems Manager features like Run Command and State Manager to control the lifecycle of the packages running on your instances.

#### AWS Systems Manager State Manager

If you need to manage the state of your AWS EC2 resources, AWS Systems Manager State Manager enables you to maintain your instances in whichever state you like.

There are three steps in using Systems Manager State Manager:

1. Decide which state to apply to your resources

2. You may be able to create the desired state for your AWS resources with a pre-configured SSM document – you need to figure this out.

3. You then create an association between your instance and the state you have defined.

You can query AWS Systems Manager at any time to view the status of your instance configurations, giving you on-demand visibility into your compliance status.

#### AWS Systems Manager OpsCenter

If you have any operational issues related to your AWS Resources – you can use OpsCenter to provide a central location where operations engineers and IT professionals can view, investigate, and resolve operational work items (OpsItems) related to AWS resources

#### AWS Systems Manager Maintenance Windows

AWS Systems Manager lets you schedule windows of time to run administrative and maintenance tasks across your instances.

This ensures that you can select a convenient and safe time to install patches and updates or make other configuration changes, improving the availability and reliability of your services and applications.

#### AWS Systems Manager Resource Groups

You can use resource groups to organize your AWS resources. Resource groups make it easier to manage, monitor, and automate tasks on large numbers of resources at one time.

AWS Resource Groups provides two general methods for defining a resource group. Both methods involve using a query to identify the members for a group.

The first method relies on tags applied to AWS resources to add resources to a group. Using this method, you apply the same key/value pair tags to resources of various types in your account and then use the AWS Resource Groups service to create a group based on that tag pair.

The second method is based on resources available in an individual AWS CloudFormation stack. Using this method, you choose an AWS CloudFormation stack, and then choose resource types in the stack that you want to be in the group.

AWS Systems Manager Resource Groups allows the creation of logical groups of resources that you can perform actions on (such as patching).

Resource groups are regional in scope.

#### Systems Manager Document

An AWS Systems Manager document (SSM document) defines the actions that Systems Manager performs on your managed instances.

Systems Manager includes more than a dozen pre-configured documents that you can use by specifying parameters at runtime.

Documents use JavaScript Object Notation (JSON) or YAML, and they include steps and parameters that you specify.

## Monitoring and Reporting

#### Insights Dashboard

AWS Systems Manager automatically aggregates and displays operational data for each resource group through a dashboard.

Systems Manager eliminates the need for you to navigate across multiple AWS consoles to view your operational data.

With Systems Manager you can view API call logs from AWS CloudTrail, resource configuration changes from AWS Config, software inventory, and patch compliance status by resource group.

You can also easily integrate your AWS CloudWatch Dashboards, AWS Trusted Advisor notifications, and AWS Personal Health Dashboard performance and availability alerts into your Systems Manager dashboard.

Systems Manager centralizes all relevant operational data, so you can have a clear view of your infrastructure compliance and performance.

#### Amazon CloudWatch

You can configure and use the Amazon CloudWatch agent to collect metrics and logs from your instances instead of using SSM Agent for these tasks. The CloudWatch agent enables you to gather more metrics on EC2 instances than are available using SSM Agent. In addition, you can gather metrics from on-premises servers using the CloudWatch agent.

#### Logging and Auditing

Systems Manager is integrated with AWS CloudTrail, a service that provides a record of actions taken by a user, role, or an AWS service in Systems Manager. CloudTrail captures all API calls for Systems Manager as events, including calls from the Systems Manager console and from code calls to the Systems Manager APIs.

SSM Agent writes information about executions, commands, scheduled actions, errors, and health statuses to log files on each instance. You can view log files by manually connecting to an instance, or you can automatically send logs to Amazon CloudWatch Logs.

## Authorization and Access Control

AWS Systems Manager supports identity-based policies.

AWS Systems Manager does not support resource-based policies.

You can attach tags to Systems Manager resources or pass tags in a request to Systems Manager.

To control access based on tags, you provide tag information in the condition element of a policy using the ssm:resourceTag/key-name, aws:ResourceTag/key-name, aws:RequestTag/key-name, or aws:TagKeys condition keys.

## AWS Systems Manager Pricing

There is no charge for most components in Systems Manager, and you only pay for the resources that are managed as part of the systems manager service.

There are some exceptions however – OpsCenter and Parameter store cost a small amount of money.

The OpsCenter pricing is as follows:

|   |   |
|---|---|
|**OpsCenter Details**|**Pricing**|
|Number of OpsItems|$2.97 per 1,000 OpsItems|
|Get, Describe, Update, and GetOpsSummary API requests|$0.039 per 1,000 requests|
|||

The Parameter store pricing is also as follows:

|   |   |
|---|---|
|**Parameter type**|**Pricing**|
|Standard|No additional charge|
|Advanced|$0.05 per advanced parameter per month (prorated hourly if the parameter is stored less than a month)|

## AWS Systems Manager FAQ

• Who should use Systems Manager?

If you are using many different services across many different accounts, and you want to gain keen operational insight into your AWS Resources, you can use Systems Manager. If you are a SysOps administrator you can gain great benefits from using Systems Manager.

• Which operating system can Systems Manager support?

You can use Systems Manager with both Linux and Windows operating systems.

• Which Regions can i use Systems Manager in?

There is a Systems Manager Region table, linked here which you can use to check your region.

• How can i use Systems Manager?

You can use AWS Systems Manager with the CLI, SDK and the AWS Console.

Thanks for reading our breakdown of Systems Manager, and exploring how useful it is as a service.

- What is a managed instance?

A managed instance is any on-premises server or any Amazon EC2 instance that can be managed using AWS Systems Manager.

## General

**Q: What is AWS Systems Manager?**  
AWS Systems Manager allows you to centralize operational data from multiple AWS services and automate tasks across your resources on AWS and in multicloud and hybrid environments. You can create logical groups of resources such as applications, different layers of an application stack, or production versus development environments. With Systems Manager, you can select a resource group and view its recent API activity, resource configuration changes, related notifications, operational alerts, software inventory, and patch compliance status. You can also take action on each resource group depending on your operational needs. Systems Manager provides a central place to view and manage your resources on AWS and in multicloud and hybrid environments, so you can have complete visibility and control over your operations.  

**Q: Who should use AWS Systems Manager?**  
If you use multiple AWS services, AWS Systems Manager provides you with a centralized and consistent way to gather operational insights and carry out routine management tasks. You can use AWS Systems Manager to perform routine operations, track your development, test, and production environments, and proactively act on events or other operational incidents. AWS Systems Manager provides an operations complement to the more developer-focused tools you use, such as code editors and integrated development environments (IDEs). Similar to an IDE, AWS Systems Manager integrates a broad range of operations tools.  

**Q: How do I get started?**  
Getting started with AWS Systems Manager is easy. Using the AWS Management Console, navigate to the AWS Systems Manager console. You can create a resource group by using a simple tag query, then begin exploring the integrated set of operational tools that AWS Systems Manager provides.  

**Q: Which operating systems does AWS Systems Manager support?**  
AWS Systems Manager is optimized to manage both Windows and Linux platforms from a single unified experience. Refer to the [documentation](http://docs.aws.amazon.com/systems-manager/latest/userguide/systems-manager-managedinstances.html) for more details on managing on-premises systems.

**Q: Does AWS Systems Manager manage instances running on premises?**  
Yes, AWS Systems Manager supports managing instances that are running in an on-premises data center, in hybrid and other cloud environments, and at the edge. Refer to [AWS Systems Manager prerequisites](http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/systems-manager-prereqs.html) for more details.  

**Q: How can I manage AWS IoT Greengrass devices using AWS Systems Manager?**  
Systems Manager enables you to manage AWS IoT Greengrass devices alongside Amazon Elastic Compute Cloud (EC2) instances and on-premises servers. To get started, see [Setting up AWS Systems Manager for edge devices](https://docs.aws.amazon.com/systems-manager/latest/userguide/systems-manager-setting-up-edge-devices.html).  

**Q: How does AWS Systems Manager help manage Amazon EC2 instances and on-premises servers?**  
AWS Systems Manager offers an agent to perform actions inside instances or servers. The agent is completely open source and available on [GitHub](https://github.com/aws/amazon-ssm-agent).  

**Q: Can I privately access AWS Systems Manager APIs from my VPC without using public IP addresses?**  
Yes, you can privately access AWS Systems Manager APIs from your VPC (created using Amazon Virtual Private Cloud) by creating VPC Endpoints. With [VPC Endpoints](http://docs.aws.amazon.com/systems-manager/latest/userguide/sysman-setting-up-vpc.html), the routing between the VPC and AWS Systems Manager is handled by the AWS network without the need for an internet gateway, NAT gateway, or virtual private network (VPN) connection. The latest generation of VPC Endpoints used by AWS Systems Manager is powered by AWS PrivateLink, a technology that enables private connectivity between AWS services using Elastic Network Interfaces (ENIs) with private IP addresses in your VPCs. To learn more about PrivateLink, visit the [PrivateLink documentation](https://docs.aws.amazon.com/vpc/latest/userguide/endpoint-services-overview.html).  

**Q: In what Regions is AWS Systems Manager available?**  
See the [AWS Regions Table](https://aws.amazon.com/about-aws/global-infrastructure/regional-product-services/) for AWS Systems Manager Region availability.  

**Q: What sorts of insights can I gather through AWS Systems Manager?**  
AWS Systems Manager overlays information from multiple AWS services. These cross-service insights are surfaced through multiple native dashboards. AWS Systems Manager also embeds [Amazon CloudWatch](https://aws.amazon.com/cloudwatch/) dashboards and lets you reuse your existing dashboards or build new ones.  

**Q: What are built-in insights?**  
AWS Systems Manager’s built-in insights are dashboards that include recent API calls through [AWS CloudTrail](https://aws.amazon.com/cloudtrail/), recent configuration changes through [AWS Config](https://aws.amazon.com/config/), instance software inventory listings, instance patch compliance views, and instance configuration compliance views. You can filter these account-level insights to reflect the members of a particular resource group. These dashboards also show recent event logs through [AWS Personal Health Dashboard](https://aws.amazon.com/premiumsupport/phd/) and optimization recommendations through [AWS Trusted Advisor](https://aws.amazon.com/premiumsupport/trustedadvisor/).  

**Q: What is a managed instance?**  
A managed instance is any on-premises server or Amazon EC2 instance that can be managed using AWS Systems Manager. A managed instance can be a physical server or virtual machine in your on-premises data center or even another cloud provider.

**Q: How do I set up a managed instance?**  
You can set up an EC2 instance as a managed instance by installing the Systems Manager agent and attaching an [AWS Identity and Access Management (IAM)](https://aws.amazon.com/iam/) instance profile to the instance, which gives Systems Manager permission to perform actions on your instance. To register servers or virtual machines outside of Amazon EC2, you can create an activation.

**Q: Do some operating systems already include the Systems Manager agent?**  
The Systems Manager agent is installed by default on the AWS Windows AMIs, on the Amazon Linux AMI, and available on the Amazon Linux repo. You can also install the agent on other supported operating systems.  

**Q: What are AWS Systems Manager activations?**  
AWS Systems Manager activations enable hybrid and cross-cloud management. Using AWS Systems Manager activations, you can easily register any server, whether physical or virtual, to be managed by AWS Systems Manager.

**Q: How do I register an instance using AWS Systems Manager activation?**  
You can create an AWS Systems Manager activation from the AWS Systems Manager console or API, which gives you an activation code and ID. Using this activation code and ID, you can run a command on your servers to register them to Systems Manager.

**Q: What is an AWS Systems Manager document?**  
An AWS Systems Manager document enables configuration as code to manage resources at scale. An AWS Systems Manager document defines a series of actions that allows you to remotely manage instances, ensure desired state, and automate operations. An AWS Systems Manager document is cross-platform and can be used for Windows and Linux instances.

**Q: Where can I use AWS Systems Manager documents?**  
You can use Systems Manager documents with run command, state manager, or automation features.

**Q: Are there pre-defined AWS Systems Manager documents?**  
Yes. You can choose from a variety of pre-defined AWS Systems Manager documents that automate common tasks including collecting inventory, installing applications, joining instances to a domain, instance operations, collecting metrics, and more.  

**Q: How do I create my own AWS Systems Manager document?**  
You can author AWS Systems Manager documents in JSON or YAML to match the defined document schema, from the AWS Systems Manager console or the APIs.

**Q: What does the AWS Systems Manager SLA guarantee?**  
Our AWS Systems Manager SLA guarantees a Monthly Uptime Percentage of at least 99.9% for AWS Systems Manager priced features.  

**Q: How do I know if I qualify for an SLA Service Credit?**  
You are eligible for an SLA credit for AWS Systems Manager under the AWS Systems Manager SLA if an AWS Systems Manager priced feature has a Monthly Uptime Percentage of less than 99.9% during any monthly billing cycle.

For full details on all of the terms and conditions of the SLA, as well as details on how to submit a claim, please see the [AWS Systems Manager SLA details page](https://aws.amazon.com/systems-manager/sla/).  

**Q: Can I connect my ServiceNow and Jira Service Desk instances to AWS Systems Manager?  
**Yes. The AWS Service Management Connector for ServiceNow and Jira Service Desk (formerly the AWS Service Catalog Connector) allows ServiceNow and Jira Service Desk end-users to manage and operate your resources on AWS and in multicloud and hybrid environments natively via ServiceNow. ServiceNow and Jira Service Desk users can execute automation runbooks using AWS Systems Manager seamlessly on ServiceNow and Jira Service Desk with the AWS Service Management Connector. This simplifies AWS product request actions for ServiceNow and Jira Service Desk users and provides governance and oversight over AWS products.

The AWS Service Management Connector for ServiceNow is available at no charge in the [ServiceNow Store](https://store.servicenow.com/sn_appstore_store.do#!/store/application/f0b117a3db32320093a7d7a0cf961912/). This new feature is generally available in all [AWS Regions](https://aws.amazon.com/about-aws/global-infrastructure/regional-product-services/) where AWS Service Catalog is available. For more information, please visit the [documentation](https://docs.aws.amazon.com/servicecatalog/latest/adminguide/integrations-servicenow.html).

The AWS Service Management Connector for Jira Service Desk is available at no charge in the [Atlassian Marketplace](https://marketplace.atlassian.com/1221283). This new feature is generally available in all [AWS Regions](https://aws.amazon.com/about-aws/global-infrastructure/regional-product-services/) where AWS Service Catalog is available. For more information, please visit the [documentation](https://docs.aws.amazon.com/servicecatalog/latest/adminguide/integrations-jiraservicedesk.html).  

**Q: How can I manage Windows Instances graphically in AWS?**  
AWS Systems Manager provides a new console-based management experience for Windows. You can use a full graphical interface via Remote Desktop Protocol (RDP) to easily set up connections to and manage Windows instances through Systems Manager Fleet Manager. RDP connects into your Windows servers through a few simple steps in the Fleet Manager console, providing access to your server or server-based application. You don’t need to install additional software, set up additional servers, or open direct inbound access to ports on the instance. The Fleet Manager console allows you to view, interact with, and switch between multiple servers side by side within a single browser window directly, without the need to switch back and forth between tabs. Like other Fleet Manager features, console-based management for Windows is available for Managed Instances in EC2 and in other environments, such as on-premises and other clouds. In addition to standard credential-based access to RDP, you also have the option to use [AWS IAM Identity Center](https://aws.amazon.com/iam/identity-center/) and supported identity providers such as Okta, Ping, and OneLogin for a one-click login experience allowing connections without the need to join a domain.  

**Q: How do I access console-based management for Windows?**  
Use Fleet Manager to access console-based management experience for Windows in AWS Systems Manager. There is an option for console-based RDP under the Instance Actions drop-down button, in addition to the existing Session Manager option.  

**Q: Does AWS Systems Manager manage instances running on premises, in hybrid environments,other cloud environments, and at the edge?**  
Yes, AWS Systems Manager supports managing instances that are running in an onpremises datacenter, in hybrid and other cloud environments, and at the edge. Refer to AWS Systems Managerprerequisites for more details.  

## Explorer

**Q: What is AWS Systems Manager Explorer?**  
AWS Systems Manager Explorer is a customizable operations dashboard for your resources on AWS and in multicloud and hybrid environments. Explorer displays an aggregated view of operations data from across your AWS accounts and Regions. Explorer provides context into how operational issues are distributed across your business units or applications, how they trend over time, and how they vary by category.  

**Q: What is OpsData?**  
OpsData is operations data displayed by the Explorer dashboard. OpsData comes from a variety of sources including EC2, OpsCenter, and Patch Manager. You can view and manage OpsData sources from the Explorer settings page.  

**Q: How does Explorer relate to OpsCenter?**  
One type of data displayed by Explorer are OpsItems from OpsCenter. OpsItems help you manage, investigate, and remediate operational issues. Explorer provides an aggregated view of your OpsItems alongside other relevant operations data across accounts and Regions. OpsItems can still be managed and remediated through OpsCenter.  

**Q: How do I view my OpsData across accounts and Regions?**  
You can view your OpsData across accounts and Regions by setting up a resource data sync from the Explorer settings page. The resource data sync collects all OpsData from the accounts and Regions you have specified and aggregates them into a single view.  

**Q: When do I use AWS Systems Manager and AWS Security Hub?  
**AWS Systems Manager is the operations hub for AWS that enables you to manage your Cloud and hybrid infrastructure with ease. Using Systems Manager, you can diagnose and resolve operational issues related to your resources on AWS and in multicloud and hybrid environments in a central location (using Systems Manager OpsCenter) and see a dashboard of your operations data across your AWS accounts and Regions (using Systems Manager Explorer). AWS Security Hub is used by security and compliance professionals and by DevOps engineers to continuously monitor and improve the security posture of their AWS accounts and resources. Most customers segregate their security issues (e.g., Amazon S3 buckets publicly accessible or crypto-mining detected on Amazon EC2 instances) and operational issues (e.g., under-utilized Amazon Redshift instances or over-utilized Amazon EC2 instances) because security issues are sensitive and typically have different access requirements. As a result, they use Security Hub to understand, manage, and remediate their security issues, and they use Systems Manager to understand, manage, and remediate their operational issues. We also recommend that you use Security Hub for more specialized views into your security posture.

When the same engineers work on both security and operational issues, it can help to consolidate them in a single location. You can do that by opting in for findings to be sent to Systems Manager OpsCenter and Explorer, where engineers can investigate and remediate security issues alongside operational issues, using Systems Manager Automation runbooks.  

## OpsCenter

**Q: What is AWS Systems Manager OpsCenter?  
**OpsCenter is a Systems Manager capability that provides a central location where operations engineers, IT professionals, and others can view, investigate, and resolve operational issues related to their environment. OpsCenter is designed to reduce mean time to resolution (MTTR) for impacted AWS and hybrid cloud resources. OpsCenter aggregates and standardizes operational issues, referred to as OpsItems, while providing contextually relevant data that helps with diagnosis and remediation. Information includes Config changes, AWS CloudTrail logs, resource description, AWS CloudWatch alarms, related OpsItems, and related resources. You can use our public APIs to create OpsItems from any source or use OpsItems integrated with Amazon CloudWatch Events. This means you can configure CloudWatch to automatically create OpsItems for any AWS service that publishes events to CloudWatch Events.

You can create the following types of OpsItems leveraging manual or automated configurations:  

- Resource failures, such as an Amazon EC2 Auto Scaling group failure to launch an instance or a Systems Manager Automation execution failure  
      
    
- Resource performance issues, such as a throttling event for Amazon DynamoDB or degraded Amazon EBS volume performance  
      
    
- Health alerts from various AWS services, such as scheduled maintenance for an Amazon Relational Database Service (RDS) instance or EC2 instance  
      
    
- AWS Security Hub security alerts  
      
    
- Resource state changes, such as an Amazon EC2 instance state change from running to stopped  
      
    
- Any other work item that needs someone’s attention

**Q: What is an OpsItem?  
**An OpsItem is an AWS resource-related operational event that needs a user’s attention, and potentially an investigation and resolution. It could be a resource-related failure, a maintenance notification, security alert, or a performance issue. An OpsItem includes relevant information that aids with investigation and resolution of the underlying event, such as impacted resources, similar past events, and recommended runbooks. High EC2 instance CPU utilization, AWS CodeDeploy Deployment Failed, or EC2 Automation Execution failed are some examples of common OpsItems.

**Q: What are the benefits of using OpsCenter?  
**OpsCenter enables users to reduce their MTTR for operational issues, in some cases by over 50%. OpsCenter enables standardization and aggregation of operational issues (OpsItems) across various resources in a single place. Additionally, it brings together contextual information and operational tooling required to investigate and remediate issues. This reduces the time it takes engineers to navigate different tools to get relevant information. Working from a single location also minimizes the chances of manual errors, and reduces training time for newly hired engineers.

**Q: Who should use OpsCenter?  
**Medium to large enterprises that use multiple AWS services for their infrastructure needs can leverage OpsCenter to manage their day-to-day operations. Additionally, Managed Service Provider (MSP) partners can also leverage OpsCenter as they manage infrastructure on behalf of other AWS customers. MSP customers can have a read-only role for better transparency into the MSP’s day-to-day operations.

Primary users of the service will be operations engineers, such as DevOps engineers and IT service desk professionals. 

**Q: How is OpsCenter different from a Case Management system?  
**OpsCenter is designed to complement your existing case management systems. You can integrate OpsCenter into your existing case management system by using public API actions. You can also maintain manual lifecycle workflows in your current systems and use OpsCenter as an investigation and remediation hub.

**Q: How much does OpsCenter cost?  
**OpsCenter pricing can be found on the AWS Systems Manager [pricing page](https://aws.amazon.com/systems-manager/pricing/).

**Q: How do I get started with OpsCenter?  
**You can use the AWS Systems Manager [console](https://console.aws.amazon.com/systems-manager/) to turn on OpsCenter in just a few clicks.

**Q: Does OpsCenter require the use of the AWS Systems Manager Agent?  
**Getting started with OpsCenter doesn’t require the use of the Systems Manager Agent. 

## Incident Manager

**Q: What is Incident Manager?  
**Incident Manager helps you prepare for incidents with automated response plans. Response plans execute runbook actions, track incident updates, and enable chat-based collaboration while automatically notifying the appropriate people to respond.

**Q: What is a response plan?  
**A response plan describes the contacts to notify – such as an on-call application team – and a set of procedures to follow to investigate and mitigate in response to an alarm (or set of alarms). The steps in the procedure, which can be manual or automated, are represented as a Systems Manager Automation document.

**Q: What is an incident?  
**An incident is any unplanned interruption or reduction in quality of services. Response plans control how incidents are automatically started based on Amazon CloudWatch alarms or Amazon EventBridge events. You can also start incidents manually in Incident Manager.

**Q: What is an analysis?  
**An analysis is the post-incident document of record tied to the incident (or set of incidents). An analysis consists of several sections: a textual summary, the timeline of key events and metrics, a set of questions to guide authors through the post-incident analysis process, and a list of operational action items for improvement.

**Q: How does Incident Manager deliver messages about an incident?  
**Incident Manager uses the configured response plan to notify the desired contacts in order (escalating to the next contact as needed). A contact can represent a device – such as a shared phone number – or a person with a list of devices in order. Incident Manager supports SMS, voice calls, email, and Slack notifications (via AWS Chatbot).

**Q: How does Incident Manager work with other AWS services?  
**With Incident Manager, you can automatically take action when a critical issue is detected by an Amazon CloudWatch alarm or Amazon EventBridge event. Incident Manager immediately executes pre-configured response plans to engage responders via SMS and phone calls, links designated chat channels using AWS Chatbot, and executes AWS Systems Manager Automation runbooks. The Incident Manager console integrates with AWS Systems Manager OpsCenter to help you track incidents and post-incident action items from a central place that also synchronizes with popular third-party incident management tools such as [Jira Service Desk](https://aws.amazon.com/about-aws/whats-new/2020/10/customers-can-now-use-jira-service-desk-to-track-operational-items-related-to-aws-resources/) and [ServiceNow](https://aws.amazon.com/about-aws/whats-new/2021/04/customers-can-now-use-servicenow-to-track-operational-items-related-to-aws-resources/).

**Q: How do I get started with Incident Manager?  
**To get started, select Incident Manager from the AWS Console or navigate to AWS Systems Manager to find it in the left navigation pane under Operations Management.

**Q: Can I use Incident Manager across accounts and AWS Regions?  
**Yes. Incident Manager uses [Resource Access Manager](https://aws.amazon.com/ram/) to share incidents, response plans, and contacts across member accounts. Member accounts can be individually selected or identified using AWS Organizations. Incident Manager also provides cross-region replication of incidents to achieve higher availability.

## CloudWatch Dashboards

**Q: What are Amazon CloudWatch Dashboards?**  
With [Amazon CloudWatch Dashboards](https://aws.amazon.com/cloudwatch/), you can create reusable dashboards that allow you to monitor your your resources on AWS and in multicloud and hybrid environments in one location. Metric data is kept for a period of fifteen months, enabling you to view up-to-the-minute data and also historical data.  

**Q: How are Amazon CloudWatch Dashboards integrated with AWS Systems Manager?**  
Your existing [CloudWatch Dashboards](https://aws.amazon.com/cloudwatch/) are now available directly through AWS Systems Manager. You can also create new CloudWatch Dashboards directly from Systems Manager. Using CloudWatch Dashboards, you can build your own custom operational dashboards to reflect the health of an application component, an application tier, or general areas of operational ownership.  

## Application Manager

**Q: What is AWS Systems Manager Application Manager?  
**AWS Systems Manager Application Manager helps DevOps engineers investigate and remediate issues with their resources on AWS and in multicloud and hybrid environments in the context of their applications.  

**Q: How do I get started using Application Manager?  
**To get started with AWS Systems Manager Application Manager, go to the AWS Systems Manager console and navigate to the Application Management category in the left navigation pane. Choose the Application Manager link to get started.

**Q: How does Application Manager work with other AWS services?  
**AWS Systems Manager Application Manager is integrated with multiple AWS services, including Amazon CloudWatch for monitoring, AWS CloudTrail for auditing, AWS Config for tracking infrastructure configuration changes, AWS CloudFormation to provision CloudFormation stacks, and other AWS Systems Manager features such as runbook automation.

**Q: What is an application in Application Manager?  
**In AWS Systems Manager Application Manager, an application represents a logical group of resources that operate as a unit. A logical group may be a business application, ownership boundaries for operators, or a developer environment such as staging or production.

**Q: How does Application Manager discover applications?  
**You can use existing mechanisms such as tagging, resource groups, and AWS CloudFormation stack definitions to discover an application in AWS Systems Manager Application Manager.

**Q: Can I perform operational tasks in Application Manager or just view data?  
**In AWS Systems Manager Application Manager, you can perform operational tasks and view data. In addition to viewing operational data, you can initiate runbooks to help you remediate operational issues with application resources. You can also manage your AWS CloudFormation templates and provision them into CloudFormation stacks.

**Q: Does Application Manager handle applications that are distributed across different accounts and AWS Regions?  
**Today, you can use AWS Systems Manager Application Manager for applications within a single AWS account and Region.

**Q: Can I edit my application in Application Manager?  
**You can edit your application within AWS Systems Manager Application Manager. After an application is onboarded, you can add or delete new resource groups or CloudFormation stacks from the application. Additionally, Application Manager automatically reflects any changes made to an application in its respective service console.

**Q: How is Application Manager different from Resource Groups in the AWS Systems Manager console?  
**AWS Systems Manager Application Manager builds on the existing resource group functionality in the AWS Systems Manager console to provide contextual and operational information such as alarms, OpsItems, and runbook logs for a given application. To onboard an application, Application Manager can use resource groups as one of the source constructs, in addition to other constructs like Launch Wizard and CloudFormation stacks.

**Q: I use an AWS CloudFormation stack to provision infrastructure for each application. Does Application Manager integrate with CloudFormation stacks?  
**AWS Systems Manager Application Manager integrates with CloudFormation stacks. To get started from the Application Manager console, choose a stack that represents your application and start managing it. You can view the stack details—such as events, parameters, and resources—and gain centralized visibility into all operational data that Application Manager provides in the context of your stack. Moreover, you can author, store, version, validate, share, and provision the CloudFormation templates for your application from within the Application Manager console. You can provision a template into new or existing CloudFormation stacks, and track which version of your template is currently used by a given stack.

**Q: I currently use a tagging solution to manage application resources. Why should I use Application Manager?  
**When you onboard your application with AWS Systems Manager Application Manager, you can use your tags as the criteria to group resources into an application. With Application Manager, you can view all your resources within a hierarchy of groups and subgroups, then view operational data and perform operational actions at the group and subgroup levels.

**Q: Does Application Manager integrate with Amazon Elastic Kubernetes Service (Amazon EKS) and Amazon Elastic Container Service (Amazon ECS)?  
**AWS Systems Manager Application Manager integrates with Amazon EKS and Amazon ECS to provide information about the health of your container clusters, as well as a component runtime view of your resources in a cluster. You can create and view OpsItems for resources in a cluster and quickly remediate issues with resources by using runbooks. 

## AppConfig

**Q: What is AWS AppConfig?**  
AWS AppConfig is a feature of AWS Systems Manager that allows you to quickly validate and roll out configurations across an application of any size, whether hosted on Amazon EC2 instances, containers, AWS Lambda functions, mobile apps, or IoT devices, in a controlled and monitored way. AWS AppConfig enables you to validate configuration data to make sure it is syntactically and semantically correct according to your definitions before deploying it to your application. AWS AppConfig allows you to follow deployment best practices by rolling out configuration at a pace that you define while monitoring for errors. In case of errors, AWS AppConfig can roll back the changes to minimize impact to the application’s users.  

**Q: Who should use AWS AppConfig?**  
AWS AppConfig is designed for System administrators, DevOps teams, and developers who want to roll out configuration changes across their applications in a managed and monitored way, similar to the way they manage code, but without the need for deploying code when a configuration value changes, thus helping to mitigate the risk of outages. AWS AppConfig is for any size or type of company or organization that has targets (hosts, servers, AWS Lambda functions, containers, mobile devices, IoT devices, etc.) for configurations.  

**Q: What is a configuration?**  
A configuration is a collection of one or more application settings that your application uses to modify its behavior at runtime. You can store your configurations as AWS Systems Manager Documents or Parameters.  

**Q: What is a validator?**  
A validator is either a schema or a pointer to an AWS Lambda function that AWS AppConfig uses to enable you to test that your configuration is syntactically or semantically correct according to your definitions.  

**Q: What is a deployment strategy?**  
A deployment strategy is a plan for how configuration data propagates to an application. A deployment strategy includes controls for defining the speed at which a configuration rolls out, the percentage of application instances that should receive updated configuration at various intervals, and the amount of time AWS AppConfig should monitor the overall application to help you ensure the configuration changes did not introduce an adverse effect.  

**Q: How is AWS AppConfig different from AWS CodeDeploy?**  
An application configuration is data that influences the behavior of an application and does not require compilation; configuration is an abstraction that can change at runtime. For example, we can control a feature release by populating a configuration value to a specific date and time. If the value needs to change, say to a new date and time, an administrator can change the configuration value, with no compiling required, and the application applies the new configuration at runtime. Both application configuration and code should include safety mechanisms to prevent errors in a production environment. We recommend that you use AWS AppConfig to apply safety mechanisms when deploying new configurations and AWS CodeDeploy when deploying new code.  

**Q: When should I use AWS Systems Manager parameter store and when should I use AWS AppConfig?**  
AWS Systems Manager parameter store is a feature that offers the ability to store, retrieve, and manage a secret or plain-text configuration value. Common use cases for parameter store include storing database strings and license codes as parameter values. If you need to store and retrieve values in a self-managed way, you should use parameter store. AWS AppConfig is an application configuration management service that allows you to safely release updated configuration to applications at runtime and allows you to store configurations as Parameters. If you need to model a complex set of application configurations that you can validate and deploy safely in a controlled environment, with the ability to roll back changes under certain conditions, you should use AWS AppConfig.  

**Q: How is AWS AppConfig different from AWS Config?**  
AWS Config enables you to assess, audit, and evaluate the configurations of your AWS resources while AWS AppConfig lets you manage application configuration. You should use AWS Config to get a detailed view of the configuration of AWS resources in your account and identify how the resources were configured in the past and how the configurations change over time. AWS AppConfig is meant for your applications running on AWS resources or on-premises servers. With AWS AppConfig, you can validate changes in application configuration and set deployment strategies to safely deploy updated configurations to applications at run-time.  

## Parameter Store

**Q: What is AWS Systems Manager parameter store?**  
AWS Systems Manager provides a centralized store to manage your configuration data, whether plain-text data such as database strings or secrets such as passwords. This allows you to separate your secrets and configuration data from your code. Parameters can be tagged and organized into hierarchies, helping you manage parameters more easily. For example, you can use the same parameter name, "db-string", with a different hierarchical path, "dev/db-string” or “prod/db-string", to store different values. Systems Manager is integrated with [AWS Key Management Service (KMS)](https://aws.amazon.com/kms/), allowing you to automatically encrypt the data you store. You can also control user and resource access to parameters using [AWS Identity and Access Management (IAM)](https://aws.amazon.com/iam/). Parameters can be referenced through other AWS services, such as [Amazon Elastic Container Service (ECS)](https://aws.amazon.com/ecs/), [AWS Lambda](https://aws.amazon.com/lambda/), and [AWS CloudFormation](https://aws.amazon.com/cloudformation/).  

**Q: Why should I use AWS Systems Manager parameter store?**  
It is a best practice to store configuration data and secrets separately from your code. You can use AWS Systems Manager parameter store to quickly store and reference configuration and sensitive information. Rather than storing data in config files or referencing them in plain text, you can store and obtain this information in your applications or scripts. Additionally, you control who has access to parameters so that only the right set of users has access to the appropriate information.  

**Q: How do you store sensitive data?**  
A secure string is any sensitive data that needs to be stored and referenced in a secure manner. If you have data that you do not want users to reference in clear text or have access to data that can be tampered with or misused, you should use secure strings in AWS Systems Manager parameter store. You can encrypt your sensitive data using your own AWS KMS key or your user account default key provided by AWS KMS.  

**Q: In what services can I reference my parameters?**  
You can easily reference your parameters across AWS services such as Amazon ECS, AWS Lambda, and AWS Systems Manager, or any service through which you can use the AWS Systems Manager parameter store APIs.  

**Q: Can I track usage and provide access control to specific parameters?**  
Yes. You can provide granular access control through customized permissions to users and resources (such as instances) for parameters access using AWS IAM. This means you can control who can access which parameter on what resource. You can also set up Amazon CloudWatch Events rules based on parameter change events. Additionally, you can also track and audit parameter API calls using AWS CloudTrail.  

**Q: Can I track changes to parameters?**  
Yes, you can see a history of parameter changes. You can also use versions that are automatically implemented upon change to look up specific parameter value bases on its version.  

**Q: Can I store hierarchical data as parameters?**  
Yes, you can use a hierarchical structure to store parameters. You can also control and audit access at every level of the hierarchy.  

**Q: Can I receive notifications upon changes to parameter values?**  
Yes, you can set up Amazon CloudWatch and [Amazon Simple Notification Service (SNS)](https://aws.amazon.com/sns/) notifications for individual parameter values, and receive notifications upon change.  

**Q: What is the difference between Secrets Manager and Parameter Store?**  
[AWS Secrets Manage](https://aws.amazon.com/secrets-manager/)r is a service to manage the lifecycle for the secrets used in your organization centrally including rotation, audit, and access control. Secrets Manager helps you meet your security and compliance requirements by enabling you to rotate secrets automatically. Secrets Manager offers built-in integration for MySQL, PostgreSQL, and Amazon Aurora on Amazon RDS that's extensible to other types of secrets by customizing Lambda functions.

AWS Systems Manager Parameter Store provides secure, hierarchical storage for configuration data management, which can include secrets. Data such as database connection strings, passwords, and license codes can be stored as parameter values and can be audited and access controlled. Values stored can be either plain text or encrypted data. You can then reference values by using the unique name of the parameter. You can reference Systems Manager parameters to build generic configuration and automation scripts for use across AWS services such as Amazon ECS and AWS CloudFormation.  

**Q: Should I use Parameter Store or Secrets Manager?**  
If you want a single store for configuration and secrets, you can use Parameter Store. If you want a dedicated secrets store with lifecycle management, use Secrets Manager. Parameter Store is available at no additional charge with limit of 10,000 parameters. Refer to the [Secrets Manager pricing page](https://aws.amazon.com/secrets-manager/pricing/) for details.  

**Q: Is there a difference in the security model of Parameter Store and Secrets Manager?**  
No. Both Secrets Manager and Parameter Store are equally secure. Both services support encryption at rest using customer-owned KMS keys. For more information on how Parameter Store uses KMS, please see the [KMS Developer Guide](https://docs.aws.amazon.com/kms/latest/developerguide/services-parameter-store.html) on how Parameter Store uses AWS KMS.  

**Q: Can I use Secrets Manager with Parameter Store?**  
Yes. You can reference a Secrets Manager secret with Parameter Store.  

**Q: What are advanced parameters?**  
Advanced parameters provide enhanced capabilities such as the ability to store more than 10,000 parameters, larger parameter value size (up to 8 KB) and parameter policies such as expiration and no-change notifications. The expiration policy provides the ability to specify an expiration date and time. The no-change notification policy helps you track parameters that have not changed for a specified period of time. Advanced parameters are priced for storage per month and per API interaction. See the [pricing page](https://aws.amazon.com/systems-manager/pricing/) for details.

**Q: Can I convert between standard and advanced parameter types?**  
A standard parameter may be converted into an advanced parameter at any time. Advanced parameters cannot be converted into standard parameters. If an advanced parameter’s enhanced capabilities are no longer required or you no longer want to incur charges for that parameter, you must delete the advanced parameter and then create a new parameter as a standard parameter.

**Q: Can I increase the API throughput for Parameter Store?**  
Yes, API throughput can be raised to a higher limit through the Parameter Store settings tab. API throughput limits apply per Region per account. Increased throughput limit incurs charges. See the [pricing page](https://aws.amazon.com/systems-manager/pricing/) for details. If you no longer need increased throughput, you may reset the limit at any time from the Settings tab.

## Change Manager

**Q: What is AWS Systems Manager Change Manager?  
**AWS Systems Manager Change Manager is a change management capability. With Change Manager, you can request, approve, implement, and report on operational changes to your application configuration and infrastructure. Change Manager streamlines change processes with pre-approved change workflows and automated approvals. It integrates with AWS Systems Manager Automation to make changes, tying the implementation directly to the change request. Change Manager integrates with both AWS Systems Manager Change Calendar to block changes during specified periods and Amazon CloudWatch to automatically roll back changes based on alarms. From Change Manager, you can review changes made across your organization, helping you to identify which changes are pending approval and to audit the results of completed changes.

**Q: What are the benefits of using Change Manager?  
**With AWS Systems Manager Change Manager, you can improve the safety and governance of changes to application configuration and infrastructure, reducing the risk of service disruption. Change Manager helps to make operational changes safer by tracking required approvals and implementing only approved changes. Finally, Change Manager provides a consistent way to record and audit changes made across your organization, the intent of the changes, and who approved and implemented those changes, helping you to increase accountability.

**Q: What is a change request?  
**You can create a change request for each operational change to be made using AWS Systems Manager Change Manager. A change request can include information about the change such as the intent, the runbook to be used, and any specified rollback procedures. A change request also maintains a timeline of its lifecycle events such as submission, approval, implementation, and completion.

**Q: What is a change template?  
**Each change request is created from a specified change template that defines the approval workflow that the change request is required to go through. You can create change templates through the console or with an API. You can also require that any change template be reviewed and approved before it can be used to create change requests. You can use templates to model general change types such as standard, major, minor, and emergency, or more specific change types such as patching or rotating certificates.

**Q: How much does Change Manager cost?  
**AWS Systems Manager Change Manager pricing can be found on the AWS Systems Manager [pricing page](https://aws.amazon.com/systems-manager/pricing/).

**Q: How do I get started with Change Manager?  
**You can use the AWS Systems Manager [console](https://console.aws.amazon.com/systems-manager/) to turn on AWS Systems Manager Change Manager in just a few clicks.

**Q: Can I use Change Manager across accounts and AWS Regions?  
**With AWS Systems Manager Change Manager, you can manage operational changes across AWS accounts and Regions using AWS Organizations. You can designate an account in your organization as a delegated administrator. From that delegated account, you can request, approve, implement, and review changes across your AWS accounts and Regions. See the [user guide](https://docs.aws.amazon.com/systems-manager/latest/userguide/change-manager.html) to learn more.

**Q: Can I use my single sign-on identities to approve change requests?  
**AWS Systems Manager Change Manager integrates with AWS IAM Identity Center to make it easy for you to manage operational changes using your existing identity source. 

## Automation

**Q: What is AWS Systems Manager Automation?**  
Automation, a capability of AWS Systems Manager, simplifies common maintenance, deployment, and remediation tasks for AWS services like Amazon EC2, Amazon RDS, Amazon Redshift, Amazon S3, and many more by allowing you to codify your operations using runbooks. With Systems Manager Automation’s low-code visual designer, you can create custom runbooks that specify a specific list of tasks or use predefined runbooks created by AWS. These runbooks can be executed directly  through the [AWS Management Console](https://aws.amazon.com/console/), [CLIs](https://aws.amazon.com/cli/), and [SDKs](https://aws.amazon.com/tools/), scheduled in a maintenance  window, or triggered based on changes to your resources on AWS and in multicloud and  hybrid environments through [Amazon CloudWatch](https://aws.amazon.com/cloudwatch/) Events. You can track the execution of  each step in the runbooks as well as require approvals for each step. You can also  incrementally roll out changes and automatically halt when errors occur.

**Q: What tasks can I automate?**  
You can automate any task that involves interaction with AWS and on-premises resources. Built-in action types let you easily interact with Amazon EC2 instances, AWS CloudFormation stacks, and more. Action types are available to invoke AWS Systems Manager run command, Python and PowerShell scripts, and AWS Lambda functions.

**Q: Are there predefined AWS Systems Manager automation runbooks?**  
There are over 370 predefined AWS Systems Manager runbooks that you can execute to accomplish a wide range of tasks such as baking golden AMIs, patching Amazon EC2 instances, managing instance states, and more.  

**Q: Can I create my own AWS Systems Manager automation runbooks?**  
You can create your own custom runbooks using Automation’s low-code visual designer from the console. With the visual designer, you can focus on defining the business logic of your runbooks using a simple drag and drop interface and without having to worry about domain specific language syntax. However, if you prefer to code your runbooks, the visual designer also has a code editor which supports JSON or YAML. You can also use AWS Systems Manager automation runbooks shared by another account and share your runbooks with others.  

**Q: Can AWS Systems Manager Automation help with the approval process?**  
Yes. Built-in approval action types can be included in your AWS Systems Manager Automation runbooks. The approver can be one or more AWS IAM users. Runbook execution will wait until the minimum number of required approvals are received or denied and proceed appropriately.  

**Q: Can I execute AWS Systems Manager Automation runbooks against an entire resource group?  
**Yes. You can target resource groups and execute AWS Systems Manager Automation runbooks against specific resource types. You can also specify safety controls to indicate the number of resources in the group that should be simultaneously executed against, and you can add error thresholds that will stop runbook execution.

**Q: Can I execute AWS Systems Manager Automation runbook steps one at a time?**  
Yes. You can choose to execute the entire AWS Systems Manager automation runbook at once or choose the manual execution mode to execute one step at a time.  

**Q: Can I trigger AWS Systems Manager Automation runbook execution on a schedule or based on other events?**  
Yes. You can schedule AWS Systems Manager Automation runbook execution to be triggered as an Amazon CloudWatch Events target, or you can use AWS Systems Manager Maintenance Windows or AWS Systems Manager State Manager to trigger runbook execution on a schedule. You can also trigger runbook execution based on changes to your resources on AWS and in multicloud and hybrid environments through Amazon CloudWatch Events.  

**Q: How does a user specify a script in an Automation runbook?**  
There are two methods by which you can execute a script in Automation. You can include a script inline as a step in a runbook. Alternately, you can add scripts as attachments to a runbook and execute them by reference from a runbook step.  

**Q: Do Automation runbooks support multiple scripts?**  
Yes. You can attach multiple scripts to an Automation runbook and reference a script from a step. Scripts can be uploaded to a runbook as files or folder. Script dependencies, i.e. scripts calling other scripts, are also supported as long as the scripts are all part of the same runbook. Other artifacts required for the scripts to run such as CloudFormation or Serverless Application Model (SAM) templates can be attached to the runbooks.  

**Q: What script languages are supported by Automation for the script step?**  
Automation supports PowerShell Core and Python3. Environments preloaded are Python with Boto (preloaded with AWS APIs). You can perform security scans on Python scripts when using the visual designer for authoring runbooks. Security scans identify security vulnerabilities in your code and suggest remediations to improve the security of your code. Security scans are powered by [Amazon CodeGuru Security](https://docs.aws.amazon.com/codeguru/latest/security-ug/what-is-codeguru-security.html). Automation support for CodeGuru Security scans is currently in preview.  

**Q: What are the requirements of the script for a script step?**  
Automation supports inputs to be specified for a runbook. The parameters required by the scripts can be collected as Automation runbook input parameters, output from a previous step, or collected during runtime from other sources such as databases. Script output is available for consumption by the subsequent steps as a JSON object. Existing Automation features like referencing step output, Automation variables, and Systems Manager Parameter Store parameters can be used to pass outputs for consumption in the runbook.  

## Maintenance Windows

**Q: What is an AWS Systems Manager maintenance window?**  
AWS Systems Manager lets you schedule windows of time to run administrative and maintenance tasks across your instances. This ensures that you can select a convenient and safe time to install patches and updates or make other configuration changes, improving the availability and reliability of your services and applications.

**Q: Why should I use AWS Systems Manager maintenance windows?**  
AWS Systems Manager maintenance windows help improve availability and reliability of your workloads by automatically performing tasks in a well-defined window of time, significantly reducing the impact of any operational or infrastructure failures.  

**Q: What tasks can I perform using an AWS Systems Manager maintenance window?**  
You can perform tasks like the following:

- Installing applications, updating patches, installing or updating AWS Systems Manager agents, or executing PowerShell commands and Linux shell scripts.  
    
- Building Amazon Machine Images (AMIs), boot-strapping software, and configuring instances.  
    
- Executing AWS Lambda functions that trigger additional actions such as scanning your instances for patch updates.  
    
- Running [AWS StepFunctions](https://aws.amazon.com/step-functions/) state machines to perform tasks such as removing an instance from an Elastic Load Balancing (ELB) environment, patching the instance, and then adding the instance back to the ELB environment.  
      
    

**Q: What types of tasks can I schedule in an AWS Systems Manager maintenance window?**  
You can create and schedule any AWS Systems Manager run command execution, AWS Systems Manager automation document execution, AWS Step Functions, or AWS Lambda functions as tasks.  

**Q: What are the types of schedules I can choose for my AWS Systems Manager maintenance windows?**  
AWS Systems Manager maintenance windows can be scheduled for a recurring date (e.g., weekly on Tuesdays at 22:00:00 or the first Sunday of every month at 22:00:00). You can define your schedule using cron or rate expression.

## Fleet Manager

**Q: What is AWS Systems Manager Fleet Manager?  
**With AWS Systems Manager Fleet Manager, you can streamline your remote server management process. Fleet Manager helps you to easily manage and troubleshoot your fleet of servers running on AWS and on premises. You can drill down to individual servers to perform a variety of system administration tasks, including disk and file exploration, log management, Windows Registry operations, and user management, without needing to remotely connect to your virtual machines.

**Q: Why should I use Fleet Manager?  
**AWS Systems Manager Fleet Manager streamlines your remote server management process in the following ways:

- With Fleet Manager’s centralized graphical user interface (GUI), you can easily manage your fleet of servers running on AWS and on premises.
- Fleet Manager is operating system (OS) agnostic. You can use Fleet Manager to perform common OS operations on Windows, Linux, and Mac-based servers. 
- With Fleet Manager, you can run these OS operations seamlessly through the Systems Manager console, by choosing pre-built automation runbooks or bringing your own automation runbooks.

**Q: What features does Fleet Manager provide?  
**AWS Systems Manager Fleet Manager provides the following capabilities to manage your servers remotely:

- File system and log exploration: Use the Systems Manager console to browse through disks, folders, and files, including file-based logs, on servers. 
- Performance counter monitoring: Monitor common server performance metrics, such as CPU utilization, network traffic, disk usage, and memory utilization.
- Windows Event management: View and troubleshoot Windows Events logs without the need to install additional agents. 
- User and group administration: View a list of users and/or groups with access to a server and change their permissions.
- Registry operations: View and modify registry values on your Windows servers.

**Q: What types of environments can I manage using Fleet Manager?  
**Use AWS Systems Manager Fleet Manager across your AWS and on-premises environments to manage Windows, Linux, and Mac-based virtual machines.

**Q: How do I get started with Fleet Manager?  
**The quickest way to get started with AWS Systems Manager Fleet Manager is to use the AWS Management Console. You can turn on Fleet Manager in a few clicks. For additional details, see the [Getting Started](https://docs.aws.amazon.com/systems-manager/latest/userguide/fleet.html) documentation.

**Q: What is the cost of using Fleet Manager?  
**AWS Systems Manager Fleet Manager is available at no additional charge for servers running on AWS. For on-premises instance management using an AWS Systems Manager agent, you are charged based on the [public pricing](https://aws.amazon.com/systems-manager/pricing/#On-Premises_Instance_Management).

## Compliance

**Q: What is AWS Systems Manager configuration compliance?**  
AWS Systems Manager lets you scan your managed instances for patch compliance and configuration inconsistencies. You can collect and aggregate data from multiple AWS accounts and Regions, and then drill down into specific resources that aren’t compliant. By default, AWS Systems Manager displays data about patching and [associations](http://docs.aws.amazon.com/systems-manager/latest/userguide/sysman-state-about.html#sysman-state-assoc). You can also customize the service and create your own compliance types based on your requirements. 

**Q: Can I track changes to my configuration over time?**  
Using an integration with [AWS Config](https://aws.amazon.com/config/), you can monitor an instance's compliance with a desired configuration through AWS Config rules. This capability allows security experts and compliance auditors to have a complete audit trail of instance configuration changes, as well as receive proactive notifications in the event of non-compliance.  

**Q: How do I view the compliance levels of my instances?**  
With AWS Systems Manager you can view patch compliance information, which tells you the detailed results of the patching process. You can easily get aggregate compliance details per instance. In addition, you can drill in further and for each instance you can determine which patches are installed, missing, not applicable, and which failed to install.  

**Q: Can I create my own compliance checks?**  
Yes. You can create your own compliance types that can be recorded through the API. Based on your business requirements, you can create your own checks and then record the compliance through AWS Systems Manager to track non-compliant instances. You can also view this compliance information across accounts and Regions by creating a [resource data sync](http://docs.aws.amazon.com/systems-manager/latest/userguide/sysman-inventory-datasync.html).  

## Inventory

**Q: What is AWS Systems Manager inventory?**  
AWS Systems Manager collects information about your instances and the software installed on them, helping you to understand your system configurations and installed applications. You can collect data about applications, files, network configurations, Windows services, registries, server roles, updates, and any other system properties. The gathered data enables you to manage application assets, track licenses, monitor file integrity, discover applications not installed by a traditional installer, and more.  

**Q: Can I collect customized information from an Amazon EC2 instance or an on-premises instance?**  
Yes, you can create [custom inventory](http://docs.aws.amazon.com/systems-manager/latest/userguide/sysman-inventory-about.html#sysman-inventory-custom) types to collect additional system properties, which can be gathered by the instance itself or recorded using the API. Some examples include JSON-formatted results from PowerShell or other applications, and information statically stored in JSON files such as rack-info.  

**Q: How can I track changes to my configuration over time?**  
Using AWS Config, you can monitor an instance's compliance with a desired configuration through AWS Config rules. This capability allows security experts and compliance auditors to have a complete audit trail of instance configuration changes, as well as receive proactive notifications in the event of non-compliance.

**Q: Can I view or query inventory data from across AWS accounts or Regions?**  
Yes, you can [sync inventory data](http://docs.aws.amazon.com/systems-manager/latest/userguide/sysman-inventory-datasync.html) from multiple accounts and Regions to the same [Amazon S3](https://aws.amazon.com/s3/) bucket. You can then use [Amazon Athena](https://aws.amazon.com/athena/), [Amazon QuickSight](https://aws.amazon.com/quicksight/), or your own business intelligence (BI) tools to query inventory data across accounts and Regions.  

**Q: Can I perform analytics and visualization on inventory data?**  
Yes, in addition to a built-in inventory dashboard, you can build advanced analytics and visualizations on inventory data with Amazon Athena and Amazon QuickSight.  

## Session Manager

**Q: What is Session Manager?**  
Session Manager is a fully managed service that provides you with an interactive browser-based shell and CLI experience. It helps provide secure and auditable instance management without the need to open inbound ports, maintain bastion hosts, and manage Secure Shell (SSH) keys. Session Manager helps to enable compliance with corporate policies that require controlled access to instances, increase security and auditability of instance access, while providing the simplicity and cross-platform instance access to end users.

**Q: What are the benefits of using Session Manager?**  
Session Manager improves your security posture by not requiring you to open inbound ports, or to maintain SSH keys or certificates on your instances. It also centralizes access to instances using AWS IAM. Once you enable Session Manager, you can connect to any Linux or Windows EC2 instance and track each user who started a session on each instance. You can audit which user accessed an instance and when using AWS CloudTrail, and log every command executed on an instance to Amazon S3 or Amazon CloudWatch Logs. Finally, with Session Manager you don’t need upfront investments to operate and maintain bastion hosts.

**Q: Who should use Session Manager?**  
Any AWS customer who wants to improve their security and audit posture, reduce operational overhead by centralizing access control on instances, and reduce inbound instance access will benefit from Session Manager. Information Security experts who want to monitor and track instance access and activity, and close down inbound ports on instances, or enable connecting to instances without a public IP will benefit from Session Manager. Administrators who want to grant and revoke access from a single place and want to provide one solution for Windows and Linux instances to users will benefit as well. Finally, operators can get started quickly by using the browser to click to start a session and then selecting an instance, or use the CLI, without having to provide SSH keys.

**Q: What features are offered by Session Manager?**  
You can start a session to a Linux or Windows EC2 instance from the AWS Management Console, AWS CLI, or any other AWS SDKs. You can grant and revoke user access to instances using tag-based permissions from AWS IAM, and then you can audit who started or ended a session using AWS CloudTrail. All actions performed on an instance can be logged to Amazon S3 or Amazon CloudWatch Logs for later analysis.

**Q: How much does Session Manager cost?**  
Session Manager is available at no additional cost to manage Amazon EC2 instances.

**Q: How do I get started?**  
The quickest way to get started with Session Manager is to use the AWS Management Console. You can turn on Session Manager in a few clicks. For additional details, see the [Getting Started](https://docs.aws.amazon.com/systems-manager/latest/userguide/session-manager.html) documentation.  

**Q: Does Session Manager require the use of the AWS Systems Manager Agent?**  
Yes. Getting started with Session Manager requires the use of the latest version of the SSM Agent. The SSM Agent is open-sourced and on [GitHub](https://github.com/aws/amazon-ssm-agent).  

**Q: Can I turn on logging across an account?**  
Yes. You can enforce logging across an account by setting up Session Manager preferences.

## Run Command

**Q: What is AWS Systems Manager run command?**  
AWS Systems Manager provides you safe, secure remote management of your instances at scale without logging into your servers, replacing the need for bastion hosts, SSH, or remote PowerShell. It provides a simple way of automating common administrative tasks across groups of instances such as registry edits, user management, and software and patch installations. Through integration with AWS IAM, you can apply granular permissions to control the actions users can perform on instances. All actions taken with Systems Manager are recorded by AWS CloudTrail, allowing you to audit changes throughout your environment.  

**Q: Does AWS provide any predefined commands?**  
Yes. There are predefined commands available which are designed to help with commonly used administrative tasks. For Windows you can run a PowerShell or Shell command or script, configure Windows Update settings, and deploy an MSI application and more. For Linux you run any Shell command or script, and remotely update an installed agent. You can also create custom commands to perform common tasks required for your environment.  

**Q: Can I make bulk changes across my environments?**  
Yes. You can act against large groups of instances by targeting using tag based queries. You can propagate changes safely across your environments by setting up rate control, which allows you to specify simultaneous execution batches with error thresholds.

**Q: Can I control who can execute a command?**  
Yes. Using the published AWS IAM permissions and policies, you can use tag-based permissions to control who has access to execute commands or documents on specific instances. For example, you can specify an IAM user who can run PowerShell commands, but not join an instance to a domain. Another IAM user can only be given access to run a very specific command, like restarting services, giving you the flexibility to specify how much access any given user can have.  

## State Manager

**Q: What is AWS Systems Manager state manager?**  
AWS Systems Manager provides configuration management, which helps you maintain consistent configuration of your Amazon EC2 or on-premises instances. With Systems Manager, you can control configuration details such as server configurations, anti-virus definitions, firewall settings, and more. You can define configuration policies for your servers through the [AWS Management Console](https://aws.amazon.com/console/) or use existing scripts, PowerShell modules, or Ansible runbooks directly from GitHub or Amazon S3 buckets. Systems Manager automatically applies your configurations across your instances at a time and frequency that you define. You can query Systems Manager at any time to view the status of your instance configurations, giving you on-demand visibility into your compliance status.

**Q: Why should I use AWS Systems Manager state manager?**  
Ensuring that the infrastructure that is powering your applications is consistent is a challenge. AWS Systems Manager allows you to create policies, reapply these policies to prevent configuration drift, and monitor the status of your intended state.  

**Q: How do I create my policies?**  
Policies can be easily created through AWS Systems Manager documents. In addition, you also have predefined configurations that you can use for installing applications, joining instances to domain and so on.  

**Q: What are the targets that can be configured?**  
You have the flexibility to target instances or tags. This means you have the flexibility to have specific configurations for groups of instances such as web servers.  

**Q: Can I use my existing configuration management tools with AWS Systems Manager state manager?**  
Yes. AWS provides pre-defined AWS Systems Manager documents to run Ansible runbooks or Salt States, and you can use PowerShell DSC on your instances using AWS Systems Manager state manager to mitigate configuration drift. In addition, you can also directly run any configuration scripts from your public or private GitHub repository.  

## Patch Manager

**Q: What is AWS Systems Manager patch manager?**  
AWS Systems Manager helps you select and deploy operating system and software patches automatically across large groups of Amazon EC2 or on-premises instances. Through patch baselines, you can set rules to auto-approve select categories of patches to be installed, such as operating system or high severity patches, and you can specify a list of patches that override these rules and are automatically approved or rejected. You can also schedule maintenance windows for your patches so that they are only applied during preset times. Systems Manager helps ensure that your software is up-to-date and meets your compliance policies.

**Q: How do I specify when I want to patch an instance?**  
You can use an AWS Systems Manager maintenance window to define when patching occurs. AWS Systems Manager provides you the ability to define one or more recurring windows of time during which it is acceptable for your own maintenance to occur. By defining these windows and associating your instances with them, it is easier for you to ensure that any maintenance activities you perform on your instances that may affect the availability of a workload are done during a well-defined window of time.  

**Q: How do I customize the patching process?**  
AWS Systems Manager provides a fully automated patching process. You can easily customize the patching process by writing your own AWS Systems Manager command or automation document.

**Q: What types of patches can I install?**  
AWS Systems Manager supports the patching of Windowsand Linux-based instances. Please visit our [documentation](http://docs.aws.amazon.com/systems-manager/latest/userguide/systems-manager-patch.html) to see the versions currently supported.  

**Q: How do I pick the patches I want to install?**  
Patch baselines define the set of patches you have approved or blocked for deployment to your instances. In a patch baseline, you can select patches by the products (e.g., Windows Server 2008, Windows Server 2012, etc.), categories (e.g., critical updates, security updates, etc.), and severities for which you want to review patches for deployment. For each category selected, you can then define a schedule on which the contained patches will be automatically approved for deployment. In addition to the rules, you can also specify a whitelist and blacklist of patches that indicate patches that are to be installed or blocked respectively. At the time of patching, AWS Systems Manager will assess targeted instances for only the patches that have been approved prior to that point in time.  

**Q: How do I view the compliance levels of my instances?**  
You can view patch compliance information, which tells you the detailed results of the patching process. From the AWS Systems Manger console or APIs, you can easily get aggregate compliance details per instance. In addition, you drill in further and for each instance you can determine which patches are installed, missing, or not applicable, and which failed to install.  

## Distributor

**Q: What is AWS Systems Manager Distributor?**  
Distributor is an AWS Systems Manager feature that enables you to securely store and distribute software packages in your organization. You can use Distributor with existing Systems Manager features like Run Command and State Manager to control the lifecycle of the packages running on your instances.  

**Q: What are the benefits of using Distributor?**  
Distributor helps you scale software package rollouts by enabling standardization of package distribution. By using Distributor with AWS Systems Manager Run Command and State Manager, you eliminate the need to build and maintain your own package distribution and installation tooling. Distributor also simplifies software package management by using a centralized repository for all of your packages. Distributor supports the use of IAM policies, providing full control over who can create and update packages. Distributor also helps enable secure software package distribution because your packages are encrypted in storage and all communication between Distributor and your instance is signed and encrypted.  

**Q: Who should use Distributor?**  
Any AWS customer who regularly distributes software packages and wants a secure way to scale package management, a centralized repository for packages, or to eliminate the need for self-maintained distribution tooling should use Distributor. IT professionals who want to control who can create or update software packages and which versions are distributed to each AWS account will benefit from Distributor.  

**Q: How much does Distributor cost?**  
Distributor pricing can be found on the Systems Manager [Pricing page](https://aws.amazon.com/systems-manager/pricing/).  

**Q: How do I get started?**  
You can use the AWS Management Console to turn on Distributor in just a few clicks. For more information, see the [Getting Started](https://docs.aws.amazon.com/systems-manager/latest/userguide/distributor-getting-started.html) documentation.  

**Q: Does Distributor require the use of the SSM Agent?**  
Yes. Getting started with Distributor requires the use of the latest version of the SSM Agent. The SSM Agent is open-sourced and available on [GitHub](https://github.com/aws/amazon-ssm-agent). The SSM Agent is also installed by default on Amazon Linux, Amazon Linux 2, Windows, and Ubuntu AMIs.

![[Module 10 - Automatic Your Architecture#AWS System Manager]]