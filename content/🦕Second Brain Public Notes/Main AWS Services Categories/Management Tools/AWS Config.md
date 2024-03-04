---
tags:
  - cloud/aws
---
**AWS Config** is a fully managed service that provides you with an AWS resource inventory, configuration history, and configuration change notifications to enable security and governance.  
![](https://i.imgur.com/gmR9U8J.png)  
![](https://i.imgur.com/D5EvOq0.png)  
![](https://i.imgur.com/OujqBNV.png)  
 ![](https://i.imgur.com/vJXDfM8.png)

With AWS Config you can discover existing AWS resources, export a complete inventory of your AWS resources with all configuration details, and determine how a resource was configured at any point in time.

These capabilities enable compliance auditing, security analysis, resource change tracking, and troubleshooting.

<mark style="background: #BBFABBA6;">Allow you to assess, audit and evaluate configurations of your AWS resources.</mark>

Very useful for Configuration Management as part of an ITIL program.

Creates a baseline of various configuration settings and files and can then track variations against that baseline.

## AWS Config Vs CloudTrail

[**AWS CloudTrail**](https://digitalcloud.training/aws-cloudtrail/) <mark style="background: #ADCCFFA6;">records user API activity on your account and allows you to access information about this activity.</mark>

<mark style="background: #D2B3FFA6;">AWS Config records point-in-time configuration details for your AWS resources as Configuration Items (CIs).</mark>

<mark style="background: #FFB86CA6;">You can use an AWS Config CI to answer, “What did my AWS resource look like?” at a point in time.</mark>

<mark style="background: #FFF3A3A6;">You can use AWS CloudTrail to answer, “Who made an API call to modify this resource?”.</mark>  
![](https://i.imgur.com/6AhbPca.png)  
![](https://i.imgur.com/wRcSTVr.png)

## AWS Config Rules
![](https://i.imgur.com/rknjMtu.png)

A Config Rule represents desired configurations for a resource and is evaluated against configuration changes on the relevant resources, as recorded by AWS Config.

[**AWS Config Rules**](https://docs.aws.amazon.com/config/latest/developerguide/evaluate-config.html) can check resources for certain desired conditions and if violations are found the resources are flagged as “noncompliant”.

Examples of Config Rules:

- Is backup enabled on [**Amazon RDS**](https://digitalcloud.training/amazon-rds/)?
- Is CloudTrail enabled on the AWS account?
- Are [**Amazon EBS**](https://digitalcloud.training/amazon-ebs/) volumes encrypted.

## Configuration Items

A [**Configuration Item (CI)**](https://docs.aws.amazon.com/config/latest/developerguide/config-item-table.html) is the configuration of a resource at a given point-in-time. A CI consists of 5 sections:

1. Basic information about the resource that is common across different resource types (e.g., Amazon Resource Names, tags).
2. Configuration data specific to the resource (e.g., [**Amazon EC2**](https://digitalcloud.training/amazon-ec2/) instance type).
3. Map of relationships with other resources (e.g., EC2::Volume vol-3434df43 is “attached to instance” EC2 Instance i-3432ee3a).
4. AWS CloudTrail event IDs that are related to this state.
5. Metadata that helps you identify information about the CI, such as the version of this CI, and when this CI was captured.

## Charges

With AWS Config, you are charged based on the number configuration items (CIs) recorded for supported resources in your AWS account.

AWS Config creates a configuration item whenever it detects a change to a resource type that it is recording.

 [AWS Config](https://docs.aws.amazon.com/config/latest/developerguide/WhatIsConfig.html)  
AWS Config provides a detailed view of the configuration of AWS resources in your AWS account. This includes how the resources are related to one another and how they were configured in the past so that you can see how the configurations and relationships change over time.

An AWS _resource_ is an entity you can work with in AWS, such as an Amazon Elastic Compute Cloud (EC2) instance, an Amazon Elastic Block Store (EBS) volume, a security group, or an Amazon Virtual Private Cloud (VPC)




An aggregator is an AWS Config resource type that collects AWS Config configuration and compliance data from the following:
- Multiple accounts and multiple regions.
- Single account and multiple regions. 
- An organization in AWS Organizations and all the accounts in that organization which have AWS Config enabled.  
Use an aggregator to view the resource configuration and compliance data recorded in AWS Config. The following image displays how an aggregator collects AWS Config data from multiple accounts and regions.  
![](https://i.imgur.com/ZZIoOG4.png)


# FAQ
## General
### What is AWS Config?

AWS Config is a fully managed service that provides you with resource inventory, configuration history, and configuration change notifications to use security and governance. With AWS Config, you can discover existing AWS resources, record configurations for third-party resources, export a complete inventory of your resources with all configuration details, and determine how a resource was configured at any point in time. These capabilities use compliance auditing, security analysis, resource change tracking, and troubleshooting.

### What is an AWS Config Rule?

An <mark style="background: #ADCCFFA6;">AWS Config rule represents desired configurations for a resource and is evaluated against configuration changes on the relevant resources, as recorded by AWS Config</mark>. The results of evaluating a rule against the configuration of a resource are available on a dashboard. Using AWS Config rules, you can assess your overall compliance and risk status from a configuration perspective, view compliance trends over time, and pinpoint which configuration change caused a resource to drift out of compliance with a rule.

### What is a Conformance Pack?

A conformance pack is a collection of AWS Config rules and remediation actions that is built using a common framework and packaging model on AWS Config. By packaging the preceding AWS Config artifacts, you can simplify the deployment and reporting aspects of governance policies and configuration compliance across multiple accounts and Regions and reduce the time that a resource is kept in a non-compliant state.

### What Are the Benefits of AWS Config?

<mark style="background: #FFF3A3A6;">AWS Config makes it easier to track your resource’s configuration without the need for upfront investments and avoiding the complexity of installing and updating agents for data collection or maintaining large databases.</mark> Once you enable AWS Config, you can view continuously updated details of all configuration attributes associated with AWS resources. You are notified through Amazon Simple Notification Service (SNS) of every configuration change.

### How Can AWS Config Help with Audits?

AWS Config gives you access to resource configuration history. You can relate configuration changes with AWS CloudTrail events that possibly contributed to the change in configuration. This information provides you full visibility, right from details, such as, “Who made the change?” and “From what IP address?”, to the effect of this change on AWS resources and related resources. You can use this information to generate reports to aid auditing and assessing compliance over a period.

### Who Should Use AWS Config and AWS Config Rules?

Any AWS customer looking to improve their security and governance posture on AWS by continuously evaluating the configuration of their resources would benefit from this capability. Administrators within larger organizations who recommend best practices for configuring resources can codify these rules as AWS Config rules, and instill self-governance among users. Information security experts who monitor usage activity and configurations to detect vulnerabilities can benefit from AWS Config rules. If you have a workload that must comply to specific standards (e.g. [PCI-DSS or HIPAA](https://aws.amazon.com/compliance/) ) can use this capability to assess compliance of their AWS infrastructure configurations, and generate reports for their auditors. Operators who manage large AWS infrastructure or components that change frequently can also benefit from AWS Config rules for troubleshooting. If you want to track changes to resources configuration, answer questions about resource configurations, demonstrate compliance, troubleshoot, or perform security analysis, you should turn on AWS Config.

### Who Should Use AWS Config Conformance Packs?

If you are looking for a framework to build and deploy compliance packages for your AWS resource configurations across several accounts, then you should use conformance packs. This framework can be used to build customized packs for security, DevOps and other personas, and you can quickly get started using one of the sample conformance pack templates.

### Does the Service Guarantee that My Configurations Are Never out of Compliance?

AWS Config rules and conformance packs provide information about whether your resources are compliant with configuration rules you specify. They will evaluate resource configurations against the AWS Config rules either periodically or upon detecting configuration changes, or both, depending upon how you have configured the rule. They do not guarantee that resources will be compliant or prevent users from taking non-compliant actions. They can be used, however, to bring a non-compliant resource back into compliance by configuring appropriate remediation actions for each AWS Config rule.

### Does the Service Prevent Users from Taking Non-compliant Actions?

AWS Config rules do not directly affect how end users consume AWS. AWS Config rules evaluate resource configurations only after a configuration change has been completed and recorded by AWS Config. AWS Config rules do not prevent the user from making changes that could be non-compliant. To control what you can provision on AWS and configuration parameters used during provisioning, use [AWS Identity and Access Management](https://aws.amazon.com/iam/) (IAM) Policies and [AWS Service Catalog](https://aws.amazon.com/servicecatalog/) respectively.

### Can Rules Be Evaluated before Provisioning a Resource?

Yes, AWS Config rules can be set to proactive only, detective only, or both proactive and detective modes. For a full list of these rules, [see documentation](https://docs.aws.amazon.com/config/latest/developerguide/evaluate-config-rules.html) .

### I Already Use AWS Config Rules for My Resources Post-provisioning. How Do I Run Those Same Rules in Proactive Mode?

You can use the existing PutConfigRule API or the AWS Config console to enable proactive mode on an AWS Config rule in your account.

### Can AWS Config Record the Configurations of Resources on Premises or on other Clouds?

AWS Config helps you record configurations for third-party resources or custom resource types such as on-premises servers, software as a service (SaaS) monitoring tools, and version control systems. To do this, you must create a resource provider schema that conforms to and validates the configuration of the resource type. You must register the custom resource using [AWS CloudFormation](https://docs.aws.amazon.com/cloudformation-cli/latest/userguide/resource-type-register.html) or your infrastructure as code (IaC) tool.

If you have configured AWS Config to record all resource types, then third-party resources that are managed (created, updated, or deleted) through AWS CloudFormation are automatically tracked in AWS Config as configuration items. To dive deeper into the steps required for this and understand in which AWS Regions this is available, see the AWS Config Developer Guide: [Record Configurations for Third-Party Resources](https://docs.aws.amazon.com/config/latest/developerguide/customresources.html) .

### How Does AWS Config Work with AWS CloudTrail?

AWS CloudTrail records user API activity on your account and helps you access information about this activity. You get full details about API actions, such as identity of the caller, the time of the API call, the request parameters, and the response elements returned by the AWS service. AWS Config records point-in-time configuration details for your AWS resources as  [Configuration Items](https://docs.aws.amazon.com/config/latest/developerguide/resource-config-reference.html) (CIs). You can use a CI to answer, “What did my AWS resource look like?” at a point in time. You can use CloudTrail to answer “Who made an API call to modify this resource?” For example, you can use the AWS Management Console for AWS Config to detect security group “Production-DB” was incorrectly configured in the past. Using the integrated CloudTrail information, you can pinpoint which user misconfigured “Production-DB” security group.

### Can I Monitor compliance Information of Multiple Accounts and Regions through a Central Account?

AWS Config makes it easier to monitor compliance status across multiple accounts and Regions using the [multi-account, multi-Region data aggregation](https://docs.aws.amazon.com/config/latest/developerguide/config-concepts.html) capability. You can create a configuration aggregator in any account and aggregate the compliance details from other accounts. This capability is also leveraged on AWS Organizations, so you can aggregate data from all accounts within your organization.

### Can I Connect My ServiceNow and Jira Service Desk Instances to AWS Config?

Yes. The AWS Service Management Connector for ServiceNow and Jira Service Desk helps ServiceNow and Jira Service Desk end users to provision, manage, and operate AWS resources natively using ServiceNow and Jira Service Desk. ServiceNow users can track resources in a configuration item view, powered by AWS Config, seamlessly on ServiceNow with the AWS Service Management Connector. Jira Service Desk users can track resources within the issue request, with the AWS Service Management Connector. This simplifies AWS product request actions for ServiceNow and Jira Service Desk users and provides ServiceNow and Jira Service Desk administrators governance and oversight over AWS products.

The AWS Service Management Connector for ServiceNow is available at no charge in the [ServiceNow Store](https://store.servicenow.com/sn_appstore_store.do) . This new feature is generally available in all [AWS Regions](https://aws.amazon.com/about-aws/global-infrastructure/regional-product-services/) where AWS Service Catalog is available. For more information, visit the [documentation](https://docs.aws.amazon.com/servicecatalog/latest/adminguide/integrations-servicenow.html) .

The AWS Service Management Connector for Jira Service Desk is available at no charge in the [Atlassian Marketplace](https://marketplace.atlassian.com/1221283) . This new feature is generally available in all [AWS Regions](https://aws.amazon.com/about-aws/global-infrastructure/regional-product-services/)  where AWS Service Catalog is available. For more information, visit the [documentation](https://docs.aws.amazon.com/servicecatalog/latest/adminguide/integrations-jiraservicedesk.html) .

## Getting Started

### How Do I Get Started with This Service?

The quickest way to get started with AWS Config is to use the AWS Management Console. You can turn on AWS Config in a few selections. For additional details, see the [Getting Started](https://docs.aws.amazon.com/config/latest/developerguide/gs-console.html) documentation.

### How Do I Access My resources’ Configuration?

You can look up current and historical resource configuration using the AWS Management Console, AWS Command Line Interface or SDKs.

For additional details, refer to [AWS Config documentation](https://aws.amazon.com/documentation/config/) .

### Do I Turn on AWS Config Regionally or Globally?

You turn on AWS Config on a per-Region basis for your account.

### Can AWS Config Aggregate Data across Different AWS Accounts?

Yes, you can set up AWS Config to deliver configuration updates from different accounts to one Amazon Simple Storage Service (S3) bucket, once the appropriate IAM policies are applied to the Amazon S3 bucket. You can also publish notifications to the one SNS Topic, within the same Region, once appropriate IAM policies are applied to the SNS Topic.

### Is API Activity on AWS Config Itself Logged by CloudTrail?

Yes. All AWS Config API activity, including use of AWS Config API operations to read configuration data, is logged by CloudTrail.

### What time and time Zones Are Displayed in the Timeline view of a Resource? What about Daylight Savings?

AWS Config displays the time at which Configuration Items (CIs) were recorded for a resource on a timeline. All times are captured in Coordinated Universal Time (UTC). When the timeline is visualized on the management console, the service uses the current time zone (adjusted for daylight savings, if relevant) to display all times in the timeline view.

## Resource Configuration

### What is a Configuration Item?

A Configuration Item (CI) is the configuration of a resource at a given point-in-time. A CI consists of five sections:

Basic information about the resource that is common across different resource types (such as Amazon Resource Names, tags),

Configuration data specific to the resource (such as EC2 instance type),

Map of relationships with other resources (such as EC2::Volume vol-3434df43 is “attached to instance” EC2 Instance i-3432ee3a),

CloudTrail event IDs that are related to this state (only for AWS resources)

Metadata that helps you identify information about the CI, such as the version of this CI, and when this CI was captured.

[Learn more about configuration items.](https://docs.aws.amazon.com/config/latest/developerguide/resource-config-reference.html)

### What is a Custom Configuration Item?

A custom Configuration Item (CI) is the CI for a third-party or custom resource. Examples include on-premises databases, Active Directory servers, version control systems like GitHub and third-party monitoring tools such as Datadog.

### What Are AWS Config Relationships and how Are They Used?

AWS Config takes the relationships among resources into account when recording changes. For example, if a new EC2 Security Group is associated with an EC2 Instance, AWS Config records the updated configurations of both the primary resource, the EC2 Security Group, and related resources, if these resources changed.

### Does AWS Config Record Every State that a Resource Has Been In?

AWS Config detects change to a resource's configuration and records the configuration state that resulted from that change. In cases where several configuration changes are made to a resource in quick succession, AWS Config will record only the latest configuration of that resource that represents the cumulative impact of the set of changes. In these situations, AWS Config will list only the latest change in the relatedEvents field of the Configuration Item. This helps users and programs to continue to change infrastructure configurations without having to wait for AWS Config to record intermediate transient states.

### How Can I Choose how Often AWS Config Records Configuration Changes?

Periodic recording allows you to decide how often to record changes in your environment, reducing configuration items from resources which change frequently. Instead of receiving updates continuously, you may be able to use periodic recording to receive configuration changes every 24 hours to meet your use cases. 

### When Should I Use Periodic Recording instead of Continuous Recording?

Periodic recording gives you the option to decide how often to receive updates on your resource configurations. When enabled, AWS Config will only deliver the latest configuration of a resource at the end of a 24-hour period if it has changed, reducing the frequency of configuration data and making the cost of gathering this data more predictable for use cases such as operational planning and audit. If your security and compliance needs require ongoing monitoring of your resources, then continuous recording should be used.

### Does AWS Config Record Configuration Changes that Did not Result from API Activity on that Resource?

Yes, AWS Config will regularly scan the configuration of resources for changes that haven’t yet been recorded and record these changes. CIs recorded from these scans will not have a relatedEvent field in the message, and only the latest state that is different from state already recorded is selected.

### Does AWS Config Record Configuration Changes to Software within EC2 Instances?

Yes. AWS Config helps you record configuration changes to software within EC2 instances in your AWS account and also virtual machines (VMs) or servers in your on-premises environment. The configuration information recorded by AWS Config includes Operating System updates, network configuration, and installed applications. You can evaluate whether your instances, VMs, and servers are in compliance with your guidelines using AWS Config rules. The deep visibility and continuous monitoring capabilities provided by AWS Config help you assess compliance and troubleshoot operational issues.

### Does AWS Config Continue to Send Notifications if a Resource that Was Previously Non-compliant is Still Non-compliant after a Periodic Rule Evaluation?

AWS Config sends notifications only when the compliance status changes. If a resource was previously non-compliant and is still non-compliant, AWS Config will not send a new notification. If the compliance status changes to “compliant,” you will receive a notification for the change in status.

### Can I Flag, Exempt, or Exclude Resources from Being Evaluated by AWS Config Rules?

Yes, you can exclude resources by navigating to the AWS Config 'recorder settings' page in the console and selecting the 'Exclude Resource Types' option and specifying the desired exclusions. Alternatively, you can utilize the [PutConfigurationRecorder](https://docs.aws.amazon.com/config/latest/APIReference/API_PutConfigurationRecorder.html) API to access this feature. This API will disable the configuration recording for that resource type. Also, when you configure AWS Config rules, you can specify whether your rule runs evaluations against specified resource types or resources with a specific tag.

## AWS Config Rules

### What is a resource’s Configuration?

Configuration of a resource is defined by the data included in the Configuration Item (CI) of AWS Config. The initial release of AWS Config rules makes the CI for a resource available to relevant rules. AWS Config rules can use this information along with any other relevant information such as other attached resources and business hours to evaluate compliance of a resource’s configuration.

### What is a Rule?

A rule represents desired Configuration Item (CI) attribute values for resources and is evaluated by comparing those attribute values with CIs recorded by AWS Config. There are two types of rules:

AWS–managed rules: AWS–managed rules are pre-built and managed by AWS. You can choose the rule you want to enable, then supply a few configuration parameters to get started. [Learn more »](https://docs.aws.amazon.com/config/latest/developerguide/evaluate-config_use-managed-rules.html)

Customer managed rules: Customer managed rules are custom rules, defined, and built by you. You can create a function on AWS Lambda that can be invoked as part of a custom rule and these functions apply in your account. [Learn more »](http://docs.aws.amazon.com/config/latest/developerguide/evaluate-config_develop-rules.html)

The quickest way to get started with AWS Config is to use the AWS Management Console. You can turn on AWS Config in a few selections. For additional details, see the [Getting Started](http://docs.aws.amazon.com/config/latest/developerguide/gs-console.html) documentation.

### How Are Rules Created?

Rules are typically set up by the AWS account administrator. They can be created by leveraging AWS–managed rules (a predefined set of rules provided by AWS) or through customer managed rules. With AWS–managed rules, updates to the rule are automatically applied to any account using that rule. In the customer-managed model, customers have a full copy of the rule and apply the rule within their own account. These rules are maintained by the customers.

### How Many Rules Can I Create?

You can create up to 150 rules in your AWS account by default. Additionally, you can request an increase for the limit on the number of rules in your account by visiting the [AWS Service Limits](https://docs.aws.amazon.com/general/latest/gr/aws_service_limits.html) page.

### How Are Rules Evaluated?

Any rule can be set up as a change-triggered rule or as a periodic rule. A change-triggered rule is applied when AWS Config records a configuration change for any of the resources specified. Additionally, one of the following must be specified:

Tag Key:(optional Value): A tag key:value implies any configuration changes recorded for resources with the specified tag key:value will initiate an evaluation of the rule.

Resource type(s): Any configuration changes recorded for any resource within the specified resource type(s) will initiate an evaluation of the rule.

Resource ID: Any changes recorded to the resource specified by the resource type and resource ID will initiate an evaluation of the rule.

A periodic rule is initiated at a specified frequency. Available frequencies are 1 hr, 3 hr, 6 hr, 12 hr, or 24 hrs. A periodic rule has a full snapshot of current Configuration Items (CIs) for all resources available to the rule.

### What is an Evaluation?

Evaluation of a rule determines whether a rule is compliant with a resource at a particular point in time. It is the result of evaluating a rule against the configuration of a resource. AWS Config rules will capture and store the result of each evaluation. This result will include the resource, rule, time of evaluation, and a link to the Configuration Item (CI) that caused non-compliance.

### What Does compliance Mean?

A resource is compliant if it observes all rules that apply to it; otherwise it is noncompliant. Similarly, a rule is compliant if all resources evaluated by the rule comply with the rule; otherwise it is noncompliant. In some cases, such as when inadequate permissions are available to the rule, an evaluation cannot exist for the resource, leading to a state of insufficient data. This state is excluded from determining the compliance status of a resource or rule.

### What Information Does the AWS Config Rules Dashboard Provide?

The AWS Config rules dashboard gives you an overview of resources tracked by AWS Config, and a summary of current compliance by resource and by rule. When you view compliance by resource, you can determine if any rule that applies to the resource is currently not compliant. You can view compliance by rule, which tells you if any resource under the purview of the rule is currently non-compliant. Using these summary views, you can explore further the AWS Config timeline view of resources, to determine which configuration parameters changed. Using this dashboard, you can start with an overview and drill into fine-grained views that give you full information about changes in compliance status, and which changes caused non-compliance.

## Conformance Packs

### When Should I Use AWS Config Rules versus Conformance Packs?

You can use individual AWS Config rules to evaluate resource configuration compliance in one or more accounts. Conformance packs provide the additional benefit of packaging rules along with remediation actions into a single entity that can be deployed across an entire organization with a single selection. Conformance packs are intended to simplify compliance management and reporting at scale when you are managing several accounts. Conformance packs are designed to provide aggregated compliance reporting at the pack level and immutability. This helps the managed AWS Config rules and remediation documents within the conformance pack to not be modified or deleted by the individual member accounts of an organization.

### How Are AWS Config and AWS Config Rules Related to AWS Security Hub?

AWS Security Hub is a security and compliance service that provides security and compliance posture management as a service. It uses AWS Config and AWS Config rules as its primary mechanism to evaluate the configuration of AWS resources. AWS Config rules can also be used to evaluate resource configuration directly. AWS Config rules are also used by other AWS services, such as AWS Control Tower and AWS Firewall Manager.

### When Do I Use AWS Security Hub and AWS Config Conformance Packs?

If a compliance standard, such as PCI DSS, is already present in Security Hub, then the fully managed Security Hub service is an easier way to operationalize it. You can investigate findings through Security Hub’s integration with Amazon Detective, and you can build automated or semiautomated remediation actions using the Security Hub integration with Amazon EventBridge. However, if you want to assemble your own compliance or security standard, which can include security, operational, or cost optimization checks, AWS Config conformance packs are the way to go. AWS Config conformance packs simplify management of AWS Config rules by packaging a group of AWS Config rules and associated remediation actions into a single entity. This packaging simplifies deployment of rules and remediation actions across an organization. It also enables aggregated reporting, as compliance summaries can be reported at the pack level. You can start with the AWS Config conformance pack samples we provide and customize as you see fit.

### Do both Security Hub and AWS Config Conformance Packs Support Continuous compliance Monitoring?

Yes, both Security Hub and AWS Config conformance packs support continuous compliance monitoring, given their reliance on AWS Config and AWS Config rules. The underlying AWS Config rules can be triggered either periodically or upon detecting changes to the configuration of resources. This helps you continuously audit and assess the overall compliance of your AWS resource configurations with your organization’s policies and guidelines.

### How Do I Get Started with Conformance Packs?

The quickest way to get started is by creating a conformance pack using one of our sample templates through the CLI or the AWS Config console. Some of the sample templates include S3 Operational Best Practices, Amazon DynamoDB Operational Best Practices, and Operational Best Practices for PCI. These templates are written in YAML. You can download these templates from our documentation site and modify them to suit your environment using your favorite text editor. You can even add custom AWS Config rules that you could have previously written into the pack.

### Is there Any Cost Associated with Using This Feature on AWS Config?

Conformance packs will be charged using a tiered pricing model. For more details, visit the [AWS Config Pricing page](https://aws.amazon.com/config/pricing/) .

## Multi-account, multi-Region Data Aggregation

### What is Multi-account, multi-Region Data Aggregation?

Data aggregation on AWS Config helps you aggregate AWS Config data from multiple accounts and Regions into a single account and a single Region. Multi-account data aggregation is useful for central IT administrators to monitor compliance for multiple AWS accounts in the enterprise.

### Can I Use the Data Aggregation Capability to Centrally Provision AWS Config Rules across Multiple Accounts?

The data aggregation capability cannot be used for provisioning rules across multiple accounts. It is purely a reporting capability that provides visibility into your compliance. You can use [AWS CloudFormation StackSets](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/stacksets-concepts.html) to provision rules across accounts and Regions. Learn more in this [blog link](https://aws.amazon.com/blogs/aws/use-cloudformation-stacksets-to-provision-resources-across-multiple-aws-accounts-and-regions/) .

### How Do I Enable Data Aggregation in My Account?

Once AWS Config and AWS Config rules are enabled in your account, and the accounts being aggregated, you can enable data aggregation by creating an aggregator in your account. [Learn more](https://docs.aws.amazon.com/config/latest/developerguide/setup-aggregator-console.html) .

### What is an Aggregator?

An aggregator is an AWS Config resource type that collects AWS Config data from multiple accounts and Regions. Use an aggregator to view the resource configuration and compliance data recorded on AWS Config for multiple accounts and Regions.

### What Information Does the Aggregated view Provide?

The aggregated view displays the total count of non-compliant rules across the organization, the top five non-compliant rules by number of resources, and the top five AWS accounts that have the highest number of non-compliant rules. You can then drill down to view more details about the resources that are violating the rule and the list of rules that are being violated by an account.

### I Am not an AWS Organizations Customer. Can I Still Use the Data Aggregation Capability?

You can specify the accounts to aggregate the AWS Config data from by uploading a file or by individually entering accounts. Note that since these accounts are not part of any AWS organization, you will need each account to explicitly authorize the aggregator account. [Learn more](https://docs.aws.amazon.com/config/latest/developerguide/authorize-aggregator-account-console.html) .

### I Have only a Single Account, Can I Still Take Advantage of the Data Aggregation Capability?

The data aggregation capability is useful for multi-Region aggregation as well. Thus, you can aggregate the AWS Config data for your account across multiple Regions using this capability.

### In what Regions is the Multi-account, multi-Region Data Aggregation Capability Available?

For details on the Regions where multi-account, multi-Region data aggregation is available, visit the AWS Config Developer Guide: [Multi-Account Multi-Region Data Aggregation](https://docs.aws.amazon.com/config/latest/developerguide/aggregate-data.html) .

### What if I Have an account that Includes a Region not Supported by This Feature?

When you create an aggregator, you specify the Regions from where you can aggregate data. This [list](https://docs.aws.amazon.com/config/latest/developerguide/aggregate-data) shows only Regions where this feature is available. You can also select “all Regions,” in which case as soon as support is added in other Regions, it will automatically aggregate the data.

## Services and Region Support

### What AWS Resources Types Are Covered by AWS Config?

Review our [documentation](https://docs.aws.amazon.com/config/latest/developerguide/resource-config-reference.html) for a complete list of supported resource types.

### What Regions is AWS Config Available In?

For more information about the AWS Regions where AWS Config is available, see the [AWS Region](https://aws.amazon.com/about-aws/global-infrastructure/regional-product-services/) table.

## Pricing
### How Will I Be Charged for AWS Config?

With AWS Config, you are charged based on the number of configuration items recorded, the number of active AWS Config rule evaluations, and the number of conformance pack evaluations in your account. A configuration item is a record of the configuration state of a resource in your AWS account. There are two frequencies at which AWS Config can deliver configuration items: continuous and periodic. Continuous recording records and delivers configuration changes whenever a change occurs. Periodic recording delivers configuration data once every 24 hours, only if a change has occurred. An AWS Config rule evaluation is a compliance state evaluation of a resource by an AWS Config rule in your AWS account. A conformance pack evaluation is the evaluation of a resource by an AWS Config rule within the conformance pack. For more detail and examples, visit [https://aws.amazon.com/config/pricing/](https://aws.amazon.com/config/pricing/) .

### Does the Pricing for AWS Config Rules Include the Costs for Lambda Functions?

You can choose from a set of managed rules provided by AWS or you can author your own rules, written as Lambda functions. Managed rules are fully maintained by AWS and you do not pay any additional Lambda charges to run them. You can enable managed rules, provide any required parameters, and pay a single rate for each active AWS Config rule in a given month. Custom rules give you full control as they are applied as Lambda functions in your account. In addition to monthly charges for an active rule, standard [Lambda free tier](https://aws.amazon.com/free/) \* and function application rates apply to custom AWS Config rules.

\*AWS Free Tier is not available in the AWS China (Beijing) Region or the AWS China (Ningxia) Region.

### I want to Change the Lambda Function for My Custom AWS Config Rule. What is the Recommended Approach?

Charges are incurred whenever a new rule is created and it becomes active. If you must update or replace the Lambda function associated with a rule, the recommended approach is to update the rule instead of deleting it and creating a new rule.

## Partner Solutions

### What AWS Partner Solutions Are Available for AWS Config?

APN Partner solutions such as Splunk, ServiceNow, Evident.io, CloudCheckr, Redseal, and Red Hat CloudForms provide offerings that are fully integrated with data from AWS Config. Managed service providers, such as 2nd Watch and Cloudnexa have also announced integrations with AWS Config. Additionally, with AWS Config Rules, partners such as CloudHealth Technologies, Alert Logic, and Trend Micro are providing integrated offerings that can be used. These solutions include capabilities such as change management and security analysis and help you visualize, monitor, and manage AWS resource configurations.