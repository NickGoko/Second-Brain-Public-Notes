---
tags:
  - cloud/aws
---
**AWS CloudTrail** is a web service that records activity made on your account and delivers log files to an Amazon S3 bucket.
- <mark style="background: #BBFABBA6;">CloudTrail is for auditing (CloudWatch is for performance monitoring).</mark>

<mark style="background: #ADCCFFA6;">CloudTrail is about logging and saves a history of API calls for your AWS account.</mark>

Provides visibility into user activity by recording actions taken on your account.  
![](https://i.imgur.com/RmLoNB4.png)

API history enables security analysis, resource change tracking, and compliance auditing.  
![](https://i.imgur.com/UVoiysH.png)

- Logs API calls made via:
	- AWS Management Console.
	- AWS SDKs.
	- Command line tools.
	- Higher-level AWS services (such as CloudFormation).

- CloudTrail records account activity and service events from most AWS services and logs the following records:
	- The identity of the API caller.
	- The time of the API call.
	- The source IP address of the API caller.
	- The request parameters.
	- The response elements returned by the AWS service.

- CloudTrail is enabled by default.

CloudTrail is per AWS account.  
![](https://i.imgur.com/FlDDqE9.png)  
![](https://i.imgur.com/hYEFaCV.png)  
![](https://i.imgur.com/byF9l5p.png)  
![](https://i.imgur.com/JoNVaxw.png)

<mark style="background: #FFB8EBA6;">You can consolidate logs from multiple accounts using an S3 bucket</mark>:
1. Turn on CloudTrail in the paying account.
2. Create a bucket policy that allows cross-account access.
3. Turn on CloudTrail in the other accounts and use the bucket in the paying account.

<mark style="background: #FFF3A3A6;">You can integrate CloudTrail with CloudWatch Logs to deliver data events captured by CloudTrail to a CloudWatch Logs log stream.</mark>

- CloudTrail log file integrity validation feature allows you to determine whether a CloudTrail log file was unchanged, deleted, or modified since CloudTrail delivered it to the specified Amazon S3 bucket.  

# FAQ
## General

Close all

### What is AWS CloudTrail?

CloudTrail enables auditing, security monitoring, and operational troubleshooting by tracking user activity and API usage. CloudTrail logs, continuously monitors, and retains account activity related to actions across your AWS infrastructure, giving you control over storage, analysis, and remediation actions.

### What Are the Benefits of CloudTrail?

CloudTrail helps you prove compliance, improve security posture, and consolidate activity records across Regions and accounts. CloudTrail provides visibility into user activity by recording actions taken on your account. CloudTrail records important information about each action, including who made the request, the services used, the actions performed, parameters for the actions, and the response elements returned by the AWS service. This information helps you track changes made to your AWS resources and troubleshoot operational issues. CloudTrail makes it easier to ensure compliance with internal policies and regulatory standards. For more details, refer to the AWS compliance whitepaper [Security at Scale: Logging in AWS](https://d1.awsstatic.com/whitepapers/compliance/AWS_Security_at_Scale_Logging_in_AWS_Whitepaper.pdf) . 

### Who Should Use CloudTrail?

Use CloudTrail if you need to audit activity, monitor security, or troubleshoot operational issues.

## Getting Started

### If I Am a New AWS Customer or Existing AWS Customer and don’t Have CloudTrail Set Up, Do I Need to Enable or Set up Anything to view My account Activity?

No, nothing is required to begin viewing your account activity. You can visit the [AWS CloudTrail console](https://console.aws.amazon.com/cloudtrail/) or AWS CLI and begin viewing up to the past 90 days of account activity.

### Does the CloudTrail Event History Show All account Activity within My Account?

AWS CloudTrail will only show the results of the CloudTrail Event history for the current Region you are viewing for the last 90 days, and supports a range of [AWS services](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/view-cloudtrail-events-supported-services.html) . These events are limited to management events that create, modify, and delete API calls and account activity. For a complete record of account activity, including all management events, data events, and read-only activity, you must configure a CloudTrail trail.

### What search Filters Can I Use to view My account Activity?

You can specify Time range and one of the following attributes: event name, user name, resource name, event source, event ID, and resource type.

### Can I Use the Lookup-events CLI Command even if I don’t Have a Trail Configured?

Yes, you can visit the [CloudTrail console](https://console.aws.amazon.com/cloudtrail/) or use the CloudTrail API/CLI and begin viewing the past 90 days of account activity.

### What Additional CloudTrail Features Are Available after Creating a Trail?

Set up a CloudTrail trail to deliver your CloudTrail events to Amazon Simple Storage Service (Amazon S3), Amazon CloudWatch Logs, and Amazon CloudWatch Events. This helps you use features to archive, analyze, and respond to changes in your AWS resources.

### Can I Restrict User Access from Viewing the CloudTrail Event History?

Yes, CloudTrail integrates with [AWS Identity and Access Management](https://aws.amazon.com/iam/) (IAM), which helps you control access to CloudTrail and to other AWS resources that CloudTrail requires. This includes the ability to restrict permissions to view and search account activity. Remove the "cloudtrail:LookupEvents" from the Users IAM policy to prevent that IAM user from viewing account activity.

### Is there Any Cost Associated with CloudTrail Event History Being Enabled on My account upon Creation?

There is no cost for viewing or searching account activity with CloudTrail Event History. 

### Can I Turn off CloudTrail Event History for My Account?

For any CloudTrail trails created, you can stop logging or delete the trails. This will also stop account activity delivery to the Amazon S3 bucket you designated as part of your trail configuration and delivery to CloudWatch Logs if configured. Account activity for the past 90 days will still be collected and visible within the CloudTrail console and through the AWS Command Line Interface (AWS CLI). 

## Services and Region Support

Close all

### What Services Are Supported by CloudTrail?

CloudTrail records account activity and service events from most AWS services. For the list of supported services, see [CloudTrail Supported Services](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-supported-services.html) in the CloudTrail User Guide.

### Are API Calls Made from the AWS Management Console Recorded?

Yes. CloudTrail records API calls made from any client. The AWS Management Console, AWS SDKs, command line tools, and higher-level AWS services call AWS API operations, so these calls are recorded.

### Where Are My Log Files Stored and Processed before They Are Delivered to My S3 Bucket?

Activity information for services with Regional endpoints (such as Amazon Elastic Compute Cloud \[Amazon EC2\] or Amazon Relational Database Service \[Amazon RDS\]) is captured and processed in the same Region as the action is made. It is then delivered to the Region associated with your S3 bucket. Activity information for services with single endpoints such as IAM and AWS Security Token Service (AWS STS) is captured in the Region where the endpoint is located. It is then processed in the Region where the CloudTrail trail is configured and delivered to the Region associated with your S3 bucket.

## Applying a Trail to All Regions

Close all

### What Does it Mean to Apply a Trail to All AWS Regions?

Applying a trail to all AWS Regions refers to creating a trail that will record AWS account activity across all Regions in which your data is stored. This setting also applies to any new Regions added. For more details on Regions and partitions, refer to the [Amazon Resource Names and AWS Service Namespaces page](https://docs.aws.amazon.com/general/latest/gr/aws-arns-and-namespaces.html) .

### What Are the Benefits of Applying a Trail to All Regions?

You can create and manage a trail across all Regions in the partition in one API call or a few selections. You will receive a record of account activity made in your AWS account across all Regions to one S3 bucket or CloudWatch Logs group. When AWS launches a new Region, you will receive the log files containing event history for the new Region without taking any action.

### How Do I Apply a Trail to All Regions?

In the CloudTrail console, you select yes to apply to all Regions in the trail configuration page. If you are using the SDKs or AWS CLI, you set the IsMultiRegionTrail to true. 

### What Happens when I Apply a Trail to All Regions?

Once you apply a trail in all Regions, CloudTrail will create a new trail by replicating the trail configuration. CloudTrail will record and process the log files in each Region and deliver log files containing account activity across all Regions to a single S3 bucket and a single CloudWatch Logs log group. If you specified an optional Amazon Simple Notification Service (Amazon SNS) topic, CloudTrail will deliver Amazon SNS notifications for all log files delivered to a single SNS topic.

### Can I Apply an Existing Trail to All Regions?

Yes. You can apply an existing trail to all Regions. When you apply an existing trail to all Regions, CloudTrail will create a new trail for you in all Regions. If you previously created trails in other Regions, you can view, edit, and delete those trails from the [CloudTrail console](https://console.aws.amazon.com/cloudtrail/home) . 

### How long Will it Take for CloudTrail to Replicate the Trail Configuration to All Regions?

Typically, it will take less than 30 seconds to replicate the trail configuration to all Regions.

## Multiple Trails

Close all

### How Many Trails Can I Create in a Region?

You can create up to five trails in a Region. A trail that applies to all Regions exists in each Region and is counted as one trail in each Region.

### What is the Benefit of Creating Multiple Trails in a Region?

With multiple trails, different stakeholders such as security administrators, software developers, and IT auditors can create and manage their own trails. For example, a security administrator can create a trail that applies to all Regions and configure encryption using one Amazon Key Management Service (Amazon KMS) key. A developer can create a trail that applies to one Region for troubleshooting operational issues.

### Does CloudTrail Support Resource-level Permissions?

Yes. Using resource-level permissions, you can write granular access control policies to allow or deny access to specific users for a particular trail. For more details, go to CloudTrail [documentation](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/grant-custom-permissions-for-cloudtrail-users.html) . 

## Security and Expiration

Close all

### How Can I Secure My CloudTrail Log Files?

By default, CloudTrail log files are encrypted using S3 server-side encryption (SSE) and placed into your S3 bucket. You can control access to log files by applying IAM or S3 bucket policies. You can add an additional layer of security by enabling S3 [multi-factor authentication (MFA) Delete](https://docs.aws.amazon.com/AmazonS3/latest/dev/MultiFactorAuthenticationDelete.html) on your S3 bucket. For more details on creating and updating a trail, see the [CloudTrail documentation](http://docs.aws.amazon.com/awscloudtrail/latest/userguide/setupyourtrail.html) .

### Where Can I Download a Sample S3 Bucket Policy and an SNS Topic Policy?

You can download a sample [S3 bucket policy](https://awscloudtrail.s3.amazonaws.com/policy/S3/AWSCloudTrail-S3BucketPolicy-2013-11-01.json) and an [SNS topic policy](https://awscloudtrail.s3.amazonaws.com/policy/SNS/AWSCloudTrail-SnsTopicPolicy-2013-11-01.json) from the CloudTrail S3 bucket. You must update the sample policies with your information before you apply them to your S3 bucket or SNS topic.

### How long Can I Store My Activity Log Files?

You control the retention policies for your CloudTrail log files. By default, log files are stored indefinitely. You can use [S3 Object lifecycle management rules](https://docs.aws.amazon.com/AmazonS3/latest/dev/object-lifecycle-mgmt.html) to define your own retention policy. For example, you might want to delete old log files or archive them to Amazon Simple Storage Service Glacier (Amazon S3 Glacier).

## Event Message, Timeliness, and Delivery Frequency

Close all

### What Information is Available in an Event?

An event contains information about the associated activity: who made the request, the services used, the actions performed, the parameters for the action, and the response elements returned by the AWS service. For more details, see the [CloudTrail Event Reference](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/eventreference.html) section of the user guide. 

### How long Does it Take CloudTrail to Deliver an Event for an API Call?

Typically, CloudTrail delivers an event within 5 minutes of the API call. For more information on how CloudTrail works, see [here](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/how-cloudtrail-works.html) .   

### How Often Will CloudTrail Deliver Log Files to My S3 Bucket?

CloudTrail delivers log files to your S3 bucket approximately every five minutes. CloudTrail does not deliver log files if no API calls are made on your account. 

### Can I Be Notified when New Log Files Are Delivered to My S3 Bucket?

Yes. You can turn on Amazon SNS notifications to take immediate action on delivery of new log files. 

### I Believe One of My Log Files Has Multiple Duplicate Events. How Do I Know Which Events Are Unique?

Although uncommon, you may receive log files that contain one or more duplicate events. Duplicate events will have the same eventID. For more information about the eventID field, see [CloudTrail record contents](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-event-reference-record-contents.html) . 

### What Happens if CloudTrail is Turned on for My account but My S3 Bucket is not Configured with the Correct Policy?

CloudTrail log files are delivered in accordance with the S3 bucket policies that you have in place. If the bucket policies are misconfigured, CloudTrail will not be able to deliver log files. 

### Is it Possible to Receive Duplicate Events?

CloudTrail is designed to support at least one delivery of subscribed events to customer S3 buckets. In some situations, it is possible that CloudTrail could deliver the same event more than once. As a result, customers may notice duplicated events. 

## Data Events

Close all

### What Are Data Events?

Data events provide insights into the resource (data plane) operations performed on or within the resource itself. Data events are often high-volume activities and include operations such as S3 object level API operations and AWS Lambda function invoke API. Data events are deactivated by default when you configure a trail. To record CloudTrail data events, you must explicitly add the supported resources or resource types you want to collect activity on. Unlike management events, data events incur additional costs. For more information, see [CloudTrail pricing](https://aws.amazon.com/cloudtrail/pricing/) . 

### How Can I Consume Data Events?

Data events that are recorded by CloudTrail are delivered to S3, similar to management events. Once enabled, these events are also available in Amazon CloudWatch Events. 

### What Are S3 Data Events? How Do I Record Them?

S3 data events represent API activity on S3 Objects. To get CloudTrail to record these actions, you specify a S3 bucket in the data events section when creating a new trail or modifying an existing one. Any API actions on the Objects within the specified S3 bucket are recorded by CloudTrail. 

### What Are Lambda Data Events? How Do I Record Them?

Lambda data events record runtime activity of your Lambda functions. With Lambda data events, you can get details on Lambda function runtime. Examples of Lambda function runtime include which IAM user or service made the Invoke API call, when the call was made, and which function was applied. All Lambda data events are delivered to an S3 bucket and CloudWatch Events. You can turn on logging for Lambda data events using the CLI or CloudTrail console and select which Lambda functions get logged by creating a new trail or editing an existing trail. 

## Delegated Administrator

Close all

### Can I Add a Delegated Administrator to My Organization?

Yes, CloudTrail now supports adding up to three delegated administrators per organization.

### Who is the Owner of an Organization Trail or Event Data Store at the Organizational Level Created by a Delegated Admin?

The management account will remain the owner of any organization trails or event datastores created at organization level, regardless of whether it was created by a delegated admin account or by a management account.

### In Which Regions is Delegated Administrator Support Available?

Currently, delegated administrator support for CloudTrail is available in all Regions where AWS CloudTrail is available. For more information, see the [AWS Regions](https://aws.amazon.com/about-aws/global-infrastructure/regional-product-services/) table.

## CloudTrail Insights

Close all

### What Are CloudTrail Insights Events?

CloudTrail Insights events help you identify unusual activity in your AWS accounts such as spikes in resource provisioning, bursts of AWS Identity and Access Management (IAM) actions, or gaps in periodic maintenance activity. CloudTrail Insights uses machine learning (ML) models that continually monitor CloudTrail write management events for abnormal activity.

When abnormal activity is detected, CloudTrail Insights events are shown in the console, and delivered to CloudWatch Events, your S3 bucket, and optionally to the CloudWatch Logs group. This makes it easier to create alerts and integrate with existing event management and workflow systems.

### What Type of Activity Does CloudTrail Insights Help Identify?

CloudTrail Insights detects unusual activity by analyzing CloudTrail write management events within an AWS account and a Region. An unusual or abnormal event is defined as the volume of AWS API calls that deviates from what is expected from a previously established operating pattern or baseline. CloudTrail Insights adapts to changes in your normal operating patterns by considering time-based trends in your API calls and applying adaptive baselines as workloads change.

CloudTrail Insights can help you detect misbehaving scripts or applications. Sometimes a developer changes a script or application that begins a repeating loop or makes a large number of calls to unintended resources such as databases, data stores, or other functions. Often this behavior isn't noticed until the month-end billing cycle when costs have increased unexpectedly or an actual outage or disruption occurs. CloudTrail Insights events can make you aware of these changes in your AWS account so that you can take corrective action quickly.

### How Does CloudTrail Insights Work with other AWS Services that Use Anomaly Detection?

CloudTrail Insights identifies unusual operational activity in your AWS accounts that helps you address operational issues, minimizing operational and business impact. Amazon GuardDuty focuses on improving security in your account, providing threat detection by monitoring account activity. Amazon Macie is designed to improve data protection in your account by discovering, classifying, and protecting sensitive data. These services provide complementary protections against different types of problems that could arise in your account.

### Do I Need to Have CloudTrail Set up in order for CloudTrail Insights to Work?

Yes. CloudTrail Insights events are configured on individual trails, so you must have at least one trail set up. When you turn on CloudTrail Insights events for a trail, CloudTrail starts monitoring the write management events captured by that trail for unusual patterns. If CloudTrail Insights detects unusual activity, a CloudTrail Insights event is logged to the delivery destination specified in the trail definition.

### What Kinds of Events Does CloudTrail Insights Monitor?

CloudTrail Insights tracks unusual activity for write management API operations.

### How Do I Get Started?

You can enable CloudTrail Insights events on individual trails in your account by using the console, the CLI, or the SDK. You can also enable CloudTrail Insights events across your organization by using an Organizational trail configured in your AWS Organizations management account. You can turn on CloudTrail Insights events by choosing the radio button in your trail definition. 

## CloudTrail Lake

Close all

### Why Should I Use CloudTrail Lake?

CloudTrail Lake helps you examine incidents by querying all actions logged by CloudTrail, configuration items recorded by AWS Config, evidence from Audit Manager, or events from non-AWS sources. It simplifies incident logging by helping to remove operational dependencies and provides tools that can help reduce your reliance on complex data process pipelines that span across teams. CloudTrail Lake does not require you to move and ingest CloudTrail logs elsewhere, which helps maintain data fidelity and decreases dealing with low-rate limits that throttle your logs. It also provides near real-time latencies as it is fine-tuned to process high-volume structured logs, making them available for incident investigation. Lastly, CloudTrail Lake provides a familiar, multi-attribute query experience with SQL and is capable of scheduling and handling multiple concurrent queries.

### How Does This Feature Relate to and Work with other AWS Services?

CloudTrail is the canonical source of logs for user activity and API usage across AWS services. You can use CloudTrail Lake to examine activity across AWS services once the logs are available in CloudTrail. You can query and analyze user activity and impacted resources, and use that data to address issues such as identifying bad actors and baselining permissions.

### How Can I Ingest Events from Sources outside of AWS, such as Custom Applications, Third-party Applications, or other Public Clouds?

You can find and add partner integrations to start receiving activity events from these applications in a few steps using the CloudTrail console, without having to build and maintain custom integrations. For sources other than the available partner integrations, you can use the new CloudTrail Lake APIs to set up your own integrations and push events to CloudTrail Lake. To get started, see [Working with CloudTrail Lake in the CloudTrail User Guide](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-lake.html) .

### When Do You Recommend Using AWS Config Advanced Query instead of CloudTrail Lake for Querying Configuration Items from AWS Config?

AWS Config advanced query is recommended for customers who want to aggregate and query on current state AWS Config configuration items (CI). This helps customers with inventory management, security and operational intelligence, cost optimization, and compliance data. AWS Config advanced query is free if you are an AWS Config customer. 

CloudTrail Lake supports query coverage for AWS Config configuration items, including resource configuration and compliance history. Analyzing configuration and compliance history for resources with related CloudTrail events helps infer who, when, and what changed on those resources. This helps with root-cause analysis of incidents related to security exposure or non-compliance. CloudTrail Lake is recommended if you must aggregate and query data across CloudTrail events and historical configuration items.  

### If I Enable Ingestion of Configuration Items from AWS Config Today into CloudTrail Lake, Will CloudTrail Lake Ingest My Historical Configuration Items (generated before the Creation of CloudTrail Lake) or Collect only the Newly Recorded Configuration Items?

CloudTrail Lake will not ingest AWS Config configuration items that were generated before CloudTrail Lake was configured. Newly recorded configuration items from AWS Config, at an account level or organization level, will be delivered to the specified CloudTrail Lake event data store. These configuration items will be available in the lake for query for the specified retention period, and can be used for historical data analysis. 

### Can I Always Know Which User Made a Particular Configuration Change by Querying CloudTrail Lake?

If multiple configuration changes are attempted on a single resource by multiple users in quick succession, only one configuration item may be created that would map to the end state configuration of the resource. In this and similar scenarios, it may not be possible to provide 100% correlation on which user made what configuration changes by querying CloudTrail and configuration items for a specific time-range and resource-id.

### If I've Used Trails Before, Can I Bring Existing CloudTrail Logs into My Existing or New CloudTrail Lake Event Data Store?

Yes. The CloudTrail Lake import capability supports copying CloudTrail logs from an S3 bucket that stores logs from across multiple accounts (from an organization trail) and multiple AWS Regions. You can also import logs from individual accounts and single-region trails. The import capability also lets you specify an import date range, so that you import only the subset of logs that are needed for long-term storage and analysis in CloudTrail Lake. After you've consolidated your logs, you can run queries on your logs, from the most recent events collected after you enabled CloudTrail Lake, to historic events brought over from your trails.

### Does This Import Capability Impact the Original Trail in S3?

The import capability copies the log information from S3 to CloudTrail Lake and keeps the original copy in S3 as is.

### What CloudTrail Events Can I Query after Enabling the CloudTrail Lake Feature?

You can enable CloudTrail Lake for any of the event categories collected by CloudTrail, depending on your internal troubleshooting needs. Event categories include management events that capture control plane activities such as CreateBucket and TerminateInstances, and data events that capture data plane activities such as GetObject and PutObject. You do not need a separate trail subscription for any of these events. For CloudTrail Lake, you will need to choose between the one-year extendable retention and seven-year retention pricing options, which will impact your cost, as well as your event retention duration. You can query the data anytime. Within CloudTrail Lake dashboards, we support querying CloudTrail events.

### After I Enable the CloudTrail Lake Feature, how long Do I Need to Wait to Begin Writing Queries?

You can begin querying the activities that occur after enabling the feature almost immediately.

### What Are Some of the Common Security and Operational Use Cases that I Can Solve Using CloudTrail Lake?

Common use cases include investigating security incidents, like unauthorized access or compromised user credentials, and enhancing your security posture by performing audits to regularly baseline user permissions. You can perform necessary audits to make sure the right set of users are making changes to your resources (such as security groups), and track any changes not adhering to your organization’s best practices. Additionally, you can track actions taken on your resources and assess modifications or deletions, and get deeper insights on your AWS services bills including the IAM users subscribing to services.

### How Do I Get Started with CloudTrail Lake?

If you are a current or new CloudTrail customer, you can immediately begin using the CloudTrail Lake capability to run queries by enabling the feature through the API or the CloudTrail console. Select the CloudTrail Lake tab on the left panel of the CloudTrail console, and select the Create Event Data Store button. When you create an event data store, you choose the pricing option you want to use for the event data store. The pricing option determines the cost for ingesting events and the maximum and default retention period for the event data store. Then, make event selections from all event categories logged by CloudTrail (Management and Data events) to get started.

Additionally, to help you visualize your top CloudTrail Lake events, you can start using CloudTrail Lake dashboards. CloudTrail Lake dashboards are prebuilt dashboards that provide out-of-the-box visibility and top insights from your audit and security data directly within the CloudTrail console.

### I Created an Event Data Store with Seven-year Retention Pricing. Will I Be Able to Migrate the Same Event Data Store to the One-year Extendable Retention Pricing Option? What Happens to My Existing Data in the Event Data Store that Was Ingested Based on Seven-year Retention Pricing?

Yes. You can update the pricing option from seven-year retention pricing to one-year extendable retention pricing as part of the event data store configuration. Your existing data will remain available in the event data store for the configured retention period. This data will not incur any extended retention charges. However, any newly ingested data will follow the one-year extendable retention pricing charges for both ingestion and extended retention. 

### I Created an Event Data Store with One-year Extendable Retention Pricing. Will I Be Able to Migrate the Same Event Data Store to the Seven-year Retention Pricing Option?

No. We currently do not support migration of an event data store from one-year extendable retention pricing to seven-year retention pricing. However, you will be able to turn-off logging for the current event data store, while creating a new event data store with seven-year retention pricing for newly ingested data. You will still be able to retain and analyze the data in both event data stores with the respective pricing option and configured retention period.

### Why is the Retention Period for CloudTrail Lake Calculated Based on Event-time and not Based on Ingestion-time to CloudTrail Lake?

CloudTrail Lake is an audit lake that helps customers meet their use case needs around compliance and auditing. Based on their compliance program mandates, customers need to retain audit logs for a specified duration from when the logs were generated, irrespective of when they were ingested into CloudTrail Lake.

### If I Ingest a Historical CloudTrail Event from S3 to CloudTrail Lake, and I Have the Event Data Store Retention Period Configured to 1 Year, Will This Event Always Be Stored in CloudTrail Lake for 1 Year from the time of Ingestion?

No. Since this was a historical event with an event-time in the past, this event will be retained in CloudTrail Lake for a retention period of 1 year starting from event-time. So the duration for which that event will be stored in CloudTrail Lake will be less than 1 year. 

### What Type of Events from CloudTrail Lake Can I Visualize on Dashboards Today?

Today, CloudTrail Lake dashboards support CloudTrail management and data events.

### Are Dashboards Enabled at an account Level or Event Data Store Level?

Dashboards are enabled at an account level today, and will apply to all event data stores active in that account that have CloudTrail management or data events enabled.

### What Charges Are Incurred when I Enable CloudTrail Lake Dashboards?

CloudTrail Lake dashboards are powered by CloudTrail Lake queries. When you enable CloudTrail Lake dashboards, you will be charged for the data scanned. See [pricing page](https://aws.amazon.com/cloudtrail/pricing/) for more details.

### Can I Create Custom Dashboards Today?

No. Today, all CloudTrail Lake dashboards are curated and pre-defined, and cannot be customized.

### What Use Cases Do CloudTrail Lake Dashboards Support?

Auditing and compliance engineers can use the CloudTrail Lake dashboards to track progress of compliance mandates such as migration to TLS 1.2 and beyond. CloudTrail Lake dashboards will help security engineers closely track sensitive user activities such as deletion of trails or repeated access denied errors. Cloud operation engineers can get visibility to issues such as top service throttling errors from the curated dashboard.

## Log File Aggregation

Close all

### I Have Multiple AWS Accounts. I Would like Log Files for All the Accounts to Be Delivered to a Single S3 Bucket. Can I Do That?

Yes. You can configure one S3 bucket as the destination for multiple accounts. For detailed instructions, refer to [aggregating log files to a single S3 bucket section](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/aggregatinglogs.html) of the CloudTrail user guide.

## Integration with CloudWatch Logs

Close all

### What is CloudTrail Integration with CloudWatch Logs?

CloudTrail integration with CloudWatch Logs delivers management and data events captured by CloudTrail to a CloudWatch Logs log stream in the CloudWatch Logs log group you specify.

### What Are the Benefits of CloudTrail Integration with CloudWatch Logs?

This integration helps you receive SNS notifications of account activity captured by CloudTrail. For example, you can create CloudWatch alarms to monitor API calls that create, modify, and delete Security Groups and Network access control lists (ACLs).

### How Do I Turn on CloudTrail Integration with CloudWatch Logs?

You can turn on CloudTrail integration with CloudWatch Logs from the CloudTrail console by specifying a CloudWatch Logs log group and an IAM role. You can also use the AWS SDKs or the AWS CLI to turn on this integration.

### What Happens when I Turn on CloudTrail Integration with CloudWatch Logs?

After you turn on the integration, CloudTrail continually delivers account activity to a CloudWatch Logs log stream in the CloudWatch Logs log group you specified. CloudTrail also continues to deliver logs to your S3 bucket as before.

### In Which AWS Regions is CloudTrail Integration with CloudWatch Logs Supported?

This integration is supported in the Regions where CloudWatch Logs is supported. For more information, see [Regions and endpoints](https://docs.aws.amazon.com/general/latest/gr/rande.html) in the AWS General Reference.

### How Does CloudTrail Deliver Events Containing account Activity to My CloudWatch Logs?

CloudTrail assumes the IAM role you specify to deliver account activity to CloudWatch Logs. You limit the IAM role to only the permissions it requires to deliver events to your CloudWatch Logs log stream. To review IAM role policy, go to the [user guide](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cw_role_policy.html) of the CloudTrail documentation.

### What Charges Do I Incur once I Turn on CloudTrail Integration with CloudWatch Logs?

After you turn on CloudTrail integration with CloudWatch Logs, you incur standard CloudWatch Logs and CloudWatch charges. For details, go to the CloudWatch [pricing page](https://aws.amazon.com/cloudwatch/pricing/) . 

## CloudTrail Log File Encryption Using AWS KMS

Close all

### What is the Benefit of CloudTrail Log File Encryption Using Server-side Encryption with AWS KMS?

CloudTrail log file encryption using [SSE-KMS](https://docs.aws.amazon.com/AmazonS3/latest/dev/UsingKMSEncryption.html) helps you add an additional layer of security to CloudTrail log files delivered to an S3 bucket by encrypting the log files with a KMS key. By default, CloudTrail will encrypt log files delivered to your S3 bucket using S3 server-side encryption.

### I Have an Application that Ingests and Processes CloudTrail Log Files. Do I Need to Make Any Changes to My Application?

With SSE-KMS, S3 will automatically decrypt the log files so that you do not need to make any changes to your application. As always, you must make sure that your application has appropriate permissions such as S3 GetObject and AWS KMS Decrypt permissions.

### How Do I Configure CloudTrail Log File Encryption?

You can use the AWS Management Console, or AWS CLI or the AWS SDKs to configure log file encryption. For detailed instructions, refer to the [documentation](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/encrypting-cloudtrail-log-files-with-aws-kms.html) .

### What Charges Do I Incur once I Configure Encryption Using SSE-KMS?

Once you configure encryption using SSE-KMS, you will incur standard AWS KMS charges. For details, go to AWS KMS [pricing page](https://aws.amazon.com/kms/pricing/) .

## CloudTrail Log File Integrity Validation

Close all

### What is CloudTrail Log File Integrity Validation?

The CloudTrail log file integrity validation feature helps you determine whether a CloudTrail log file was unchanged, deleted, or modified since CloudTrail delivered it to the specified S3 bucket.

### What is the Benefit of the CloudTrail Log File Integrity Validation?

You can use the log file integrity validation as an aid in your IT security and auditing processes.

### How Do I Enable CloudTrail Log File Integrity Validation?

You can enable the CloudTrail log file integrity validation feature from the console, AWS CLI or AWS SDKs.

### What Happens once I Turn on the Log File Integrity Validation Feature?

Once you turn on the log file integrity validation feature, CloudTrail will deliver digest files on an hourly basis. The digest files contain information about the log files that were delivered to your S3 bucket and hash values for those log files. They also contain digital signatures for the previous digest file and the digital signature for the current digest file in the S3 metadata section. For more information about digest files, digital signatures, and hash values, go to [CloudTrail documentation](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-log-file-validation-intro.html) .

### Where Are the Digest Files Delivered To?

The digest files are delivered to the same S3 bucket where your log files are delivered. However, they are delivered to a different folder so that you can enforce granular access control policies. For details, refer to the digest file structure section of the [CloudTrail documentation](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-log-file-validation-digest-file-structure.html) .

### How Can I Validate the Integrity of a Log File or Digest File Delivered by CloudTrail?

You can use the AWS CLI to validate the integrity of a log file or digest file. You can also build your own tools to do the validation. For more details on using the AWS CLI for validating the integrity of a log file, refer to the [CloudTrail documentation](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-log-file-validation-cli.html) .

### I Aggregate All My Log Files across All Regions and Multiple Accounts into One Single S3 Bucket. Will the Digest Files Be Delivered to the Same S3 Bucket?

Yes. CloudTrail will deliver the digest files across all Regions and multiple accounts into the same S3 bucket.

## CloudTrail Processing Library

Close all

### What is the CloudTrail Processing Library?

The CloudTrail Processing Library is a Java library that makes it easier to build an application that reads and processes CloudTrail log files. You can download the CloudTrail Processing Library from [GitHub](https://github.com/aws/aws-cloudtrail-processing-library) .

### What Functionality Does CloudTrail Processing Library Provide?

CloudTrail Processing Library provides functionality to handle tasks such as continually polling an SQS queue and reading and parsing Amazon Simple Queue Service (Amazon SQS) messages It can also download log files stored in S3, and parse and serialize log file events in a fault-tolerant manner. For more information, go to the [user guide](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/using_processing_lib.html) in the CloudTrail documentation. 

### What Software Do I Need to Start Using the CloudTrail Processing Library?

You need aws-java-sdk version 1.9.3 and Java 1.7 or higher.

## Pricing

Close all

### How Do I Get Charged for CloudTrail Trails?

CloudTrail helps you view, search, and download the last 90 days of your account’s management events for free. You can deliver one copy of your ongoing management events to S3 for free by creating a trail. Once a CloudTrail trail is set up, S3 charges apply based on your usage.

You can deliver additional copies of events, including data events, using trails. You will be charged for data events or additional copies of management events. Learn more on the [pricing page](https://aws.amazon.com/cloudtrail/pricing/) .

### If I Have only One Trail with Management Events, and Apply it to All Regions, Will I Incur Charges?

No. The first copy of management events is delivered free of charge in each Region.

### If I Enable Data Events on an Existing Trail with Free Management Events, Will I Get Charged?

Yes. You will be charged for only the data events. The first copy of management events is delivered free of charge. 

### How Do I Get Charged for CloudTrail Lake?

When you use CloudTrail Lake, you pay for ingestion and storage together, where the billing is based on the amount of uncompressed data ingested and the amount of compressed data stored. When you create an event data store, you choose the pricing option you want to use for the event data store. The pricing option determines the cost for ingesting events and the maximum and default retention period for the event data store. Querying charges are based on the compressed data you choose to analyze. Learn more on the [pricing page](https://aws.amazon.com/cloudtrail/pricing/) .

### Can I Calculate My Estimated CloudTrail Lake Ingestion Usage if I Know My Historical CloudTrail Usage in Trails?

Yes. Each CloudTrail event, on average, is around 1500 bytes. Using this mapping, you will be able to estimate the CloudTrail Lake ingestion based on past month’s CloudTrail usage in trails by number of events.

## Partners

Close all

### How Do the AWS Partner Solutions Help Me Analyze the Events Recorded by CloudTrail?

Multiple partners offer integrated solutions to analyze CloudTrail log files. These solutions include features like change tracking, troubleshooting, and security analysis. For more information, see the [CloudTrail partners section](https://aws.amazon.com/cloudtrail/partners/) .

### How Can I Onboard an Integration to CloudTrail Lake as an Available Source?

To get started with your integration you can review the [Partner Onboarding Guide](https://docs.aws.amazon.com/awscloudtrail/latest/partner-onboarding/cloudtrail-lake-partner-onboarding.html) . Engage with your partner development team or partner solutions architect to connect you with the CloudTrail Lake team for a deeper dive or further questions.

## Other

Close all

### Will Turning on CloudTrail Impact the Performance of My AWS Resources or Increase API Call Latency?

No. Turning on CloudTrail has no impact on performance for your AWS resources or API call latency.