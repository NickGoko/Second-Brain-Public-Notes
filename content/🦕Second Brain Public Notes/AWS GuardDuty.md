---
tags:
  - cloud/aws
---

![](https://i.imgur.com/fxH1pwE.png)  
![](https://i.imgur.com/RknPZfK.png)

<mark style="background: #FFB86CA6;">Intelligent threat detection service.</mark>

<mark style="background: #FFF3A3A6;">Continuously monitors for malicious activity and delivers detailed security findings for visibility and remediation.</mark>

<mark style="background: #CACFD9A6;">Monitors AWS accounts, workloads, and data in Amazon S3.</mark>

<mark style="background: #BBFABBA6;">Detects account compromise, instance compromise, malicious reconnaissance, and bucket compromise</mark>.

Amazon GuardDuty gives you access to built-in detection techniques developed and optimized for the cloud.

AWS Security continuously maintains and improves these detection algorithms.

The primary detection categories include:

- **Reconnaissance:** Activity suggesting reconnaissance by an attacker such as:
    - Unusual API activity.
    - Intra-VPC port scanning.
    - Unusual, failed login request patterns.
    - Unblocked port probing from a known bad IP.
- **Instance compromise:** Activity indicating an instance compromise, such as:
    - Cryptocurrency mining
    - Backdoor command and control (C&C) activity.
    - Malware using domain generation algorithms (DGA).
    - Outbound denial of service activity.
    - Unusually high network traffic volume.
    - Unusual network protocols.
    - Outbound instance communication with a known malicious IP.
    - Temporary Amazon EC2 credentials used by an external IP address.
    - Data exfiltration using DNS.
- **Account compromise:** Common patterns indicative of account compromise include:
    - API calls from an unusual geolocation or anonymizing proxy.
    - Attempts to disable AWS CloudTrail logging.
    - Changes that weaken the account password policy.
    - Unusual instance or infrastructure launches.
    - Infrastructure deployments in an unusual region.
    - API calls from known malicious IP addresses.
- **Bucket compromise:** Activity indicating a bucket compromise, such as:
    - Suspicious data access patterns indicating credential misuse.
    - Unusual Amazon S3 API activity from a remote host.
    - Unauthorized S3 access from known malicious IP addresses.
    - API calls to retrieve data in S3 buckets from a user with no prior history of accessing the bucket or invoked from an unusual location.


# FAQ
## Service Overview

Close all

### What is Amazon GuardDuty?

GuardDuty is <mark style="background: #FFB86CA6;">an intelligent threat detection service that continuously monitors your AWS accounts, workloads, and data for malicious activity.</mark> If potential malicious activity, such as anomalous behavior, credential exfiltration, or command and control infrastructure (C2) communication is detected, GuardDuty generates detailed security findings that can be used for security visibility and assisting in remediation.

### What Are the Key Benefits of GuardDuty?

GuardDuty makes it easier to continuously monitor your AWS accounts, workloads, and. GuardDuty is designed to operate completely independently from your resources and have no performance or availability impact to your workloads. The service is fully managed with integrated threat intelligence, machine learning (ML) anomaly detection, and malware scanning. GuardDuty delivers detailed and actionable alerts that are designed to be integrated with existing event management and workflow systems. There are no upfront costs and you pay only for the events analyzed, with no additional software to deploy or threat intelligence feed subscriptions required.

### How much Does GuardDuty Cost?

GuardDuty is a pay-as-you-go service, and you only pay for the usage you incur. GuardDuty prices are based on the volume of analyzed service logs, [virtual CPUs](https://aws.amazon.com/rds/instance-types/) (vCPUs) or Aurora Serverless v2 instance [Aurora capacity units](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/aurora-serverless-v2.how-it-works.html) (ACUs) for Amazon RDS event analysis, the number and size of Amazon Elastic Kubernetes Service (Amazon EKS) or Amazon Elastic Container Service (Amazon ECS) workloads being monitored at runtime, and the volume of data scanned for malware.

Analyzed service logs are filtered for cost optimization and directly integrated with GuardDuty, which means you don’t have to activate or pay for them separately. If EKS Runtime Monitoring is enabled for your account, you will not be charged for analysis of VPC Flow Logs from instances where the GuardDuty agent is deployed and active. The runtime security agent provides us with similar (and more contextual) network telemetry data. Hence, to avoid double charging customers, we will not charge for VPC Flow Logs from Amazon Elastic Compute Cloud (Amazon EC2) instances where the agent is installed.

See [Amazon GuardDuty pricing](https://aws.amazon.com/guardduty/pricing/) for additional details and pricing examples.

### Does the Estimated Cost in the GuardDuty Payer account Show the Total Aggregated Costs for Linked Accounts, or just that Individual Payer Account?

The estimated cost represents the cost for the individual payer account, and you will see the billed usage and average daily cost for each member account in the [GuardDuty administrator account](https://docs.aws.amazon.com/guardduty/latest/ug/guardduty_accounts.html). You must go to the individual account if you want to see the detailed usage info.

### Is there a Free Trial of GuardDuty?

Yes, any new account to GuardDuty can try the service for 30 days at no cost. You have access to the full feature set and detections during the free trial. During the trial period, you can view the post-trial [costs estimate on the GuardDuty console](https://docs.aws.amazon.com/guardduty/latest/ug/monitoring_costs.html) usage page. If you are a GuardDuty administrator, you will see the estimated costs for your member accounts. After 30 days, you can view actual costs of this feature in the AWS Billing console.

### What Are the Differences between GuardDuty and Amazon Macie?

GuardDuty provides broad security monitoring of your AWS accounts, workloads, and data to help identify threats, such as attacker reconnaissance; instance, account, bucket, or Amazon EKS cluster compromises; and malware. [Macie](https://aws.amazon.com/macie/) is a fully managed sensitive data discovery service that uses ML and pattern matching to discover your sensitive data in Amazon Simple Storage Service (Amazon S3).

### Is GuardDuty a Regional or Global Service?

GuardDuty is a regional service. Even when multiple accounts are enabled and multiple AWS Regions are used, the GuardDuty security findings remain in the same Regions where the underlying data was generated. This ensures all data analyzed is regionally based and doesn’t cross AWS regional boundaries. However, you can choose to aggregate security findings produced by GuardDuty across Regions using Amazon EventBridge or pushing findings to your data store (like Amazon S3) and then aggregating findings as you see fit. You can also send GuardDuty findings to AWS Security Hub and use its [cross-Region aggregation](https://docs.aws.amazon.com/securityhub/latest/userguide/finding-aggregation.html) capability.

### Which Regions Does GuardDuty Support?

GuardDuty regional availability is listed in the [AWS Regional Services List](https://aws.amazon.com/about-aws/global-infrastructure/regional-product-services/).

### Which Partners Work with GuardDuty?

Many technology partners have integrated and built on GuardDuty. There are also consulting, system integrator, and managed security service providers with expertise about GuardDuty. For details, see the [Amazon GuardDuty Partners](https://aws.amazon.com/guardduty/resources/partners/) page.

### Does GuardDuty Help Address Payment Card Industry Security Standard (PCI DSS) Requirements?

Foregenix published a [white paper](https://d1.awsstatic.com/certifications/foregenix_amazon_guardduty_security_review_07-2020.pdf) providing a detailed assessment of GuardDuty effectiveness for assisting in meeting requirements, like PCI DSS requirement 11.4, which requires intrusion detection techniques at critical points in the network.

## Enabling GuardDuty

Close all

### How Do I Enable GuardDuty?

You can set up and deploy GuardDuty in a few steps in the AWS Management Console. Once enabled, GuardDuty immediately starts analyzing continuous streams of account and network activity in near real time and at scale. There are no additional security software, sensors, or network appliances to deploy or manage. Threat intelligence is pre-integrated into the service and is continuously updated and maintained.

### Can I Manage Multiple Accounts with GuardDuty?

Yes, GuardDuty has a multiple account management feature, allowing you to associate and manage multiple AWS accounts from a single administrator account. When used, all security findings are aggregated to the administrator account for review and remediation. EventBridge events are also aggregated to the GuardDuty administrator account when using this configuration. Additionally, GuardDuty is integrated with [AWS Organizations](https://aws.amazon.com/organizations/), allowing you to delegate an administrator account for GuardDuty for your organization. This delegated administrator (DA) account is a centralized account that consolidates all findings and can configure all member accounts.

### Which Data Sources Does GuardDuty Analyze?

The [foundational data sources](https://docs.aws.amazon.com/guardduty/latest/ug/guardduty_data-sources.html) that GuardDuty analyzes include: AWS CloudTrail management event logs, CloudTrail management events, and Amazon EC2 VPC Flow Logs and DNS query logs. GuardDuty protection plans monitor other resource types, including CloudTrail S3 data events (S3 Protection), Amazon EKS audit logs and runtime activity for Amazon EKS (EKS Protection), Amazon ECS runtime activity (ECS Runtime Monitoring), Amazon EC2 runtime activity (EC2 Runtime Monitoring), Amazon EBS volume data (Malware Protection), Amazon Aurora login events (RDS Protection), and network activity logs (Lambda Protection). The service is optimized to consume large data volumes for near real-time processing of security detections. GuardDuty gives you access to built-in detection techniques developed and optimized for the cloud, which are maintained and continuously improved upon by GuardDuty engineering.

### How Quickly Does GuardDuty Start Working?

Once enabled, GuardDuty starts analyzing for malicious or unauthorized activity. The timeframe to begin receiving findings depends on the activity level in your account. GuardDuty does not look at historical data, only activity that starts after it is enabled. If GuardDuty identifies any potential threats, you will receive a finding in the GuardDuty console.

### Do I Have to Enable CloudTrail, VPC Flow Logs, DNS Query Logs, or Amazon EKS Audit Logs for GuardDuty to Work?

No, GuardDuty pulls independent data streams directly from CloudTrail, VPC Flow Logs, DNS query logs, and Amazon EKS. You don’t have to manage Amazon S3 bucket policies or modify the way you collect and store logs. GuardDuty permissions are managed as service-linked roles. You can disable GuardDuty at any time, which will remove all GuardDuty permissions. This makes it easier for you to enable the service, as it avoids complex configuration. The service-linked roles also remove the chance that an AWS Identity and Access Management (IAM) permission misconfiguration or Amazon S3 bucket policy change will affect service operation. Lastly, the service-linked roles make GuardDuty extremely efficient at consuming high volumes of data in near real time with minimal to no impact on the performance and availability of your account or workloads.

### Is there Any Performance or Availability Impact to Enabling GuardDuty on My Account?

When you enable GuardDuty for the first time, it operates completely independent of your AWS resources. If you configure GuardDuty Runtime Monitoring to automatically deploy the GuardDuty security agent, this could result in additional resource utilization, and will also create VPC endpoints in VPCs used to run the monitored workloads.

### Does GuardDuty Manage or Keep My Logs?

No, GuardDuty does not manage or retain your logs. All data that GuardDuty consumes is analyzed in near real time and discarded thereafter. This allows GuardDuty to be highly efficient and cost effective, and to reduce the risk of data remanence. For log delivery and retention, you should use AWS logging and monitoring services directly, which provide full-featured delivery and retention options.

### How Can I Prevent GuardDuty from Looking at My Logs and Data Sources?

You can prevent GuardDuty from analyzing your data sources at any time in the general settings by choosing to suspend the service. This will immediately stop the service from analyzing data, but it will not delete your existing findings or configurations. You can also choose to disable the service in the general settings. This will delete all remaining data, including your existing findings and configurations, before relinquishing the service permissions and resetting the service. You can also selectively disable capabilities like GuardDuty S3 Protection or GuardDuty EKS Protection through the Management Console or via the AWS CLI.

## Activating GuardDuty

Close all

### What Can GuardDuty Detect?

GuardDuty gives you access to built-in detection techniques developed and optimized for the cloud. The detection algorithms are maintained and continually improved upon by GuardDuty Engineers. The primary detection categories include the following:

- **Reconnaissance:** Activity suggesting reconnaissance by an attacker, such as unusual API activity, intra-VPC port scanning, unusual patterns of failed login requests, or unblocked port probing from a known bad IP.
- **Instance compromise:** Activity indicating an instance compromise, such as cryptocurrency mining, malware using domain generation algorithms (DGAs), outbound denial of service activity, an unusually high volume of network traffic, unusual network protocols, outbound instance communication with a known malicious IP, temporary Amazon EC2 credentials used by an external IP address, and data exfiltration using DNS.
- **Account compromise:** Common patterns indicative of account compromise, including API calls from an unusual geolocation or anonymizing proxy, attempts to deactivate CloudTrail logging, unusual instance or infrastructure launches, infrastructure deployments in an unusual region, the exfiltration of credentials, suspicious database login activity, and API calls from known malicious IP addresses.
- **Bucket compromise:** Activity indicating a bucket compromise, such as suspicious data access patterns indicating credential misuse, unusual Amazon S3 API activity from a remote host, unauthorized Amazon S3 access from known malicious IP addresses, and API calls to retrieve data in Amazon S3 buckets from a user that had no prior history of accessing the bucket or invoked from an unusual location. GuardDuty continuously monitors and analyzes CloudTrail S3 data events (like GetObject, ListObjects, and DeleteObject) to detect suspicious activity across all of your Amazon S3 buckets.
- **Malware detection:** GuardDuty begins a malware detection scan when it identifies suspicious behavior indicative of malicious software in Amazon EC2 instance or container workloads. GuardDuty generates temporary replicas of Amazon EBS volumes attached to such Amazon EC2 instance or container workloads and scans the volume replicas for trojans, worms, crypto miners, rootkits, bots, and more, that might be used to compromise the workloads, repurpose resources for malicious use, and gain unauthorized access to data. GuardDuty Malware Protection generates contextualized findings that can validate the source of the suspicious behavior. These findings can be routed to the proper administrators and initiate automated remediation.
- **Container compromise:** Activity identifying possible malicious or suspicious behavior in container workloads is detected by continuously monitoring and profiling [Amazon EKS](https://aws.amazon.com/eks/) clusters by analyzing its [Amazon EKS audit logs](https://docs.aws.amazon.com/eks/latest/userguide/control-plane-logs.html) and container runtime activity in Amazon EKS or Amazon ECS.

### What is GuardDuty Threat Intelligence?

GuardDuty threat intelligence is made up of IP addresses and domains known to be used by attackers. GuardDuty threat intelligence is provided by AWS and third-party providers, such as Proofpoint and CrowdStrike. These threat intelligence feeds are pre-integrated and continuously updated in GuardDuty at no additional cost.

### Can I Supply My Own Threat Intelligence?

Yes, GuardDuty allows you to upload your own threat intelligence or [trusted IP address list](https://aws.amazon.com/premiumsupport/knowledge-center/guardduty-trusted-ip-list/). When this feature is used, these lists are only applied to your account and not shared with other customers.

### How Are Security Findings Delivered?

When a potential threat is detected, GuardDuty delivers a detailed security finding to the GuardDuty console and EventBridge. This makes alerts more actionable and more easily integrated into existing event management or workflow systems. The findings include the category, resource affected, and metadata associated with the resource, such as a severity level.

### What is the Format of GuardDuty Findings?

GuardDuty findings come in a common JSON format, which is also used by Macie and Amazon Inspector. This makes it easier for customers and partners to consume security findings from all three services and incorporate them into broader event management, workflow, or security solutions.

### How long Are Security Findings Made Available in GuardDuty?

Security findings are retained and made available through the GuardDuty console and APIs for 90 days. After 90 days, the findings are discarded. To retain findings for longer than 90 days, you can enable EventBridge to automatically push findings to an Amazon S3 bucket in your account or another data store for long-term retention.

### Can I Aggregate GuardDuty Findings?

Yes, you can choose to aggregate security findings produced by GuardDuty across regions using EventBridge or by pushing findings to your data store (like Amazon S3) and then aggregating findings as you see fit. You can also send GuardDuty findings to Security Hub and use its [cross-Region aggregation](https://docs.aws.amazon.com/securityhub/latest/userguide/finding-aggregation.html) capability.

### Can I Take Automated Preventative Actions Using GuardDuty?

With GuardDuty, EventBridge, and AWS Lambda, you have the flexibility to set up automated remediation actions based on a security finding. For example, you can create a Lambda function to modify your AWS security group rules based on security findings. If you receive a GuardDuty finding indicating one of your Amazon EC2 instances is being probed by a known malicious IP, you can address it through an EventBridge rule, initiating a Lambda function to automatically modify your security group rules and restrict access on that port.

### How Are GuardDuty Detections Developed and Managed?

GuardDuty has a team focused on detection engineering, management, and iteration. This produces a steady cadence of new detections in the service, as well as continual iteration on existing detections. Several feedback mechanisms are built into the service, such as the thumbs-up and thumbs-down in each security finding found in the GuardDuty user interface (UI). This allows you to provide feedback that might be incorporated into future iterations of GuardDuty detections.

### Can I Write Custom Detections in Amazon GuardDuty?

No, GuardDuty removes the heavy lifting and complexity of developing and maintaining your own custom rule sets. New detections are continually added based on customer feedback, along with research from AWS security engineers and the GuardDuty engineering team. However, customer-configured customizations include adding your own [threat lists and trusted IP address list](https://docs.aws.amazon.com/guardduty/latest/ug/guardduty_upload-lists.html).

## GuardDuty S3 Protection

Close all

### How Can I Get Started with S3 Protection if I Am Currently Using GuardDuty?

For current GuardDuty accounts, S3 Protection can be activated in the console on the S3 Protection page, or through the API. This will start a 30-day no-cost trial of the GuardDuty S3 Protection feature.

### Is there a Free Trial of GuardDuty S3 Protection?

Yes, there is a 30-day free trial. Each account in each Region gets a 30-day no-cost trial of the GuardDuty that includes the S3 Protection feature. Accounts that already have GuardDuty enabled will also get a 30-day free trial of the S3 Protection feature when they first activate it.

### If I Am a New User to GuardDuty, is S3 Protection Enabled by Default for My Accounts?

Yes. Any new accounts that enable GuardDuty through the console or API will also have S3 Protection turned on by default. New GuardDuty accounts created using the AWS Organizations auto-enable feature will not have S3 Protection turned on unless the Auto-enable for S3 option is turned on.

### Can I Use GuardDuty S3 Protection without Enabling the Full GuardDuty Service (including the Analysis of VPC Flow Logs, DNS Query Logs, and CloudTrail Management events)?

No, the GuardDuty service must be enabled in order to use S3 Protection. Current GuardDuty accounts have the option to enable S3 Protection, and new GuardDuty accounts will have the feature by default once the GuardDuty service is enabled.

### Does GuardDuty Monitor All Buckets in My account to Help Protect My Amazon S3 Deployment?

Yes, S3 Protection monitors all Amazon S3 buckets in your environment by default.

### Do I Need to Turn on CloudTrail S3 Data Event Logging for S3 Protection?

No, GuardDuty has direct access to CloudTrail S3 data event logs. You are not required to enable S3 data event logging in CloudTrail, and therefore will not incur the associated costs. Note that GuardDuty does not store the logs and only uses them for its analysis.

## GuardDuty EKS Protection

Close all

### How Does GuardDuty EKS Protection Work?

GuardDuty EKS Protection is a GuardDuty feature that monitors Amazon EKS cluster control plane activity by analyzing [Amazon EKS audit logs](https://docs.aws.amazon.com/eks/latest/userguide/control-plane-logs.html). GuardDuty is integrated with Amazon EKS, giving it direct access to Amazon EKS audit logs without requiring you to turn on or store these logs. These audit logs are security-relevant chronological records documenting the sequence of actions performed on the Amazon EKS control plane. These Amazon EKS audit logs give GuardDuty the visibility needed to conduct continuous monitoring of Amazon EKS API activity and apply proven threat intelligence and anomaly detection to identify malicious activity or configuration changes that might expose your Amazon EKS cluster to unauthorized access. When threats are identified, GuardDuty generates security findings that include the threat type, a severity level, and container-level detail (such as pod ID, container image ID, and associated tags).

### What Types of Threats Can GuardDuty EKS Protection Detect on My Amazon EKS Workloads?

GuardDuty EKS Protection can detect threats related to user and application activity captured in Amazon EKS audit logs. Amazon EKS threat detections include Amazon EKS clusters that are accessed by known malicious actors or from Tor nodes, API operations performed by anonymous users that might indicate a misconfiguration, and misconfigurations that can result in unauthorized access to Amazon EKS clusters. Also, using ML models, GuardDuty can identify patterns consistent with privilege-escalation techniques, such as a suspicious launch of a container with root-level access to the underlying Amazon EC2 host. See [Amazon GuardDuty Finding types](https://docs.aws.amazon.com/guardduty/latest/ug/guardduty_finding-types-active.html) for a complete list of all new detections.

### Do I Need to Turn on a Amazon EKS Audit Logs

No, GuardDuty has direct access to Amazon EKS audit logs. Note that GuardDuty only uses these logs for analysis; it doesn’t store them, nor do you need to enable or pay for these Amazon EKS audit logs to be shared with GuardDuty. To optimize for costs, GuardDuty applies intelligent filters to only consume a subset of the audit logs that are relevant for security threat detection.

### Is there a Free Trial of GuardDuty EKS Protection?

Yes, there is a 30-day free trial. Each new GuardDuty account in each Region receives a 30-day free trial of GuardDuty, including the GuardDuty EKS Protection feature. Existing GuardDuty accounts receive a 30-day trial of GuardDuty EKS Protection at no additional charge. During the trial period, you can view the post-trial [costs estimate on the GuardDuty console](https://docs.aws.amazon.com/guardduty/latest/ug/monitoring_costs.html) usage page. If you are a GuardDuty administrator, you will see the estimated costs for your member accounts. After 30 days, you can view actual costs of this feature in the AWS Billing console.

### How Can I Get Started with GuardDuty EKS Protection if I Am Currently Using GuardDuty?

GuardDuty EKS Protection must be turned on for each individual account. You can activate the feature for your accounts with a single action in the GuardDuty console from the GuardDuty EKS Protection console page. If you are operating in a GuardDuty multi-account configuration, you can activate GuardDuty EKS Protection across your entire organization from the GuardDuty administrator account GuardDuty EKS Protection page. This will activate continuous monitoring for Amazon EKS in all individual member accounts. For GuardDuty accounts created using the AWS Organizations auto-activate feature, you must explicitly turn on Auto-activate for Amazon EKS. Once activated for an account, all existing and future Amazon EKS clusters in the account will be monitored for threats without any configuration on your Amazon EKS clusters.

### Is GuardDuty EKS Protection Enabled by Default for My Accounts if I Am a New GuardDuty User?

Yes, any new account that turns on GuardDuty through the console or API will also have GuardDuty EKS Protection turned on by default. For new GuardDuty accounts created using the AWS Organizations auto-enable feature, you need to explicitly enable the auto-enable for EKS Protection option. 

### How Do I Disable GuardDuty EKS Protection?

You can disable the feature in the console or by using the API. In the GuardDuty console, you can disable GuardDuty EKS Protection for your accounts on the GuardDuty EKS Protection console page. If you have a GuardDuty administrator account, you can also disable this feature for your member accounts.

### If I Disable GuardDuty EKS Protection, how Do I Enable it Again?

If you previously disabled GuardDuty EKS Protection, you can re-enable the feature in the console or by using the API. In the GuardDuty console, you can enable GuardDuty EKS Protection for your accounts on the GuardDuty EKS Protection console page.

### Do I Have to Enable GuardDuty EKS Protection on Each AWS account and Amazon EKS Cluster Individually?

GuardDuty EKS Protection must be enabled for each individual account. If you are operating in a GuardDuty multi-account configuration, you can enable threat detection for Amazon EKS across your entire organization with a single click on the GuardDuty administrator account GuardDuty EKS Protection console page. This will enable threat detection for Amazon EKS in all individual member accounts. Once enabled for an account, all existing and future Amazon EKS clusters in the account will be monitored for threats, and no manual configuration is required on your Amazon EKS clusters.

### Will I Be Charged if I don’t Use Amazon EKS and I Enable GuardDuty EKS Protection in GuardDuty?

You will not incur any GuardDuty EKS Protection charges if you aren’t using Amazon EKS and you have GuardDuty EKS Protection enabled. However, when you start using Amazon EKS, GuardDuty will automatically monitor your clusters and generate findings for identified issues, and you will be charged for this monitoring.

### Can I Enable GuardDuty EKS Protection without Enabling the Full GuardDuty Service (including the Analysis of VPC Flow Logs, DNS Query Logs, and CloudTrail Management events)?

No, the GuardDuty service must be enabled for GuardDuty EKS Protection to be available.

### Does GuardDuty EKS Protection Monitor Amazon EKS Audit Logs for Amazon EKS Deployments on AWS Fargate?

Yes, GuardDuty EKS Protection monitors Amazon EKS audit logs from both Amazon EKS clusters deployed on Amazon EC2 instances and Amazon EKS clusters deployed on Fargate.

### Does GuardDuty Monitor Non-managed Amazon EKS on Amazon EC2 or Amazon EKS Anywhere?

Currently, this capability only supports Amazon EKS deployments running on Amazon EC2 instances in your account or on Fargate.

### Will Using GuardDuty EKS Protection Impact the Performance or Cost of Running Containers on Amazon EKS?

No, GuardDuty EKS Protection is designed to not have any performance, availability, or cost implications to Amazon EKS workload deployments.

### Do I Have to Enable GuardDuty EKS Protection in Each AWS Region Individually?

Yes, GuardDuty is a regional service, and thus GuardDuty EKS Protection must be enabled in each AWS Region separately.

## GuardDuty EKS Runtime Monitoring

Close all

### How Does GuardDuty EKS Runtime Monitoring Work?

GuardDuty EKS Runtime Monitoring uses a fully-managed Amazon EKS add-on that adds visibility into the runtime activity of individual Kubernetes containers running on Amazon EKS, such as ﬁle access, process execution, and network connections. The add-on can be activated automatically, directly from GuardDuty, for all existing and new Amazon EKS clusters in an account, or manually from Amazon EKS for an individual cluster. The add-on automatically deploys a GuardDuty security agent as a Daemon set that collects runtime events from all pods running on the node and delivers them to GuardDuty for security analytics processing. This allows GuardDuty to identify specific containers within your Amazon EKS clusters that are potentially compromised, and detect attempts to escalate privileges from an individual container to the underlying Amazon EC2 host and the broader AWS environment. When GuardDuty detects a potential threat, a security finding is generated that includes metadata context that includes container, Kubernetes pod, and process details.

### How Can I Get Started with EKS Runtime Monitoring if I Am Currently Using GuardDuty?

For current GuardDuty accounts, the feature can be activated from the GuardDuty console on the [EKS Runtime Monitoring](https://docs.aws.amazon.com/guardduty/latest/ug/guardduty-eks-runtime-monitoring.html) page, or through the API. Learn more about GuardDuty EKS Runtime Monitoring.

### If I Am a New User to GuardDuty, is EKS Runtime Monitoring Turned on by Default for My Accounts?

No. GuardDuty EKS Runtime Monitoring is the only protection plan that is not enabled by default when you turn on GuardDuty for the first time. The feature can be activated from the GuardDuty console on the EKS Runtime Monitoring page, or through the API. New GuardDuty accounts created using the AWS Organizations auto-enable feature will not have EKS Runtime Monitoring turned on unless the auto-enable for Amazon EKS option is turned on.

### Can I Use GuardDuty EKS Runtime Monitoring without Activating the Full GuardDuty Service?

No, the GuardDuty service must be enabled in order to use GuardDuty EKS Runtime Monitoring.

### Is GuardDuty EKS Runtime Monitoring Available in All Regions where GuardDuty is Currently Available?

For a full list of Regions where EKS Runtime Monitoring is available, visit [Region-specific feature availability.](https://docs.aws.amazon.com/guardduty/latest/ug/guardduty_regions.html#gd-regional-feature-availability)

### Do I Have to Activate GuardDuty EKS Runtime Monitoring on Each AWS account and Amazon EKS Cluster Individually?

GuardDuty EKS Runtime Monitoring must be enabled for each individual account. If you are operating in a GuardDuty multi-account configuration, you can turn on threat detection for Amazon EKS across your entire organization with a single click on the GuardDuty administrator account GuardDuty EKS Runtime Monitoring console page. This will activate runtime monitoring for Amazon EKS in all individual member accounts. Once activated for an account, all existing and future Amazon EKS clusters in the account will be monitored for runtime threats, and no manual configuration is required on your Amazon EKS clusters.

### Can I Modify how I Monitor Specific Clusters in Amazon EKS?

GuardDuty EKS Runtime Monitoring allows you to [selectively configure](https://docs.aws.amazon.com/guardduty/latest/ug/eks-protection-configuration-key-concepts.html) which Amazon EKS clusters are to be monitored for threat detection. With cluster-level configurability, you can selectively monitor EKS clusters for threat detection or continue using account-level configurability to monitor all EKS clusters in a given account and Region.

### Will Using GuardDuty EKS Runtime Monitoring Impact the Performance or Cost of Running Containers on Amazon EKS?

If you configure GuardDuty EKS Runtime Monitoring to automatically deploy the GuardDuty security agent, this could result in additional resource utilization, and will also create VPC endpoints in VPCs used to run Amazon EKS clusters. [Learn more about EKS add ons](https://docs.aws.amazon.com/eks/latest/userguide/eks-add-ons.html).

### Will I Be Charged if I don’t Use Amazon EKS and I Turn on GuardDuty EKS Runtime Monitoring in GuardDuty?

You will not incur any GuardDuty EKS Runtime Monitoring charges if you aren’t using Amazon EKS and you have GuardDuty EKS Runtime Monitoring turned on. However, when you start using Amazon EKS, GuardDuty will automatically monitor your clusters and generate findings for identified issues, and you will be charged for this monitoring.

## GuardDuty ECS Runtime Monitoring

Close all

### How Does GuardDuty ECS Runtime Monitoring Work?

GuardDuty ECS Runtime Monitoring can be enabled in a few steps in the GuardDuty console, using AWS Organizations for multi-account management and Amazon ECS for automated resource discovery and agent deployment. This allows security teams to centrally enable, configure, and manage runtime threat detection coverage for all accounts and workloads across the organization and maintain full security coverage. Coverage status across all Amazon ECS clusters can be viewed in the GuardDuty console, and notification of changes in coverage can be automated using EventBridge. Once the GuardDuty agent is deployed, it begins collecting and analyzing runtime event activity for potential threats. When GuardDuty identifies threats, it issues actionable security findings to the GuardDuty console, Security Hub, and EventBridge, allowing customers to use existing integration with security event management or workflow systems, such as Splunk, Jira, and ServiceNow. GuardDuty is also integrated with Amazon Detective, allowing security practitioners to investigate and run to ground ECS related security events and proactively hunt threats across their organization. GuardDuty findings can also be used to invoke automated and semi-automated responses through EventBridge and Lambda, such as temporary invalidating credentials or isolating a workload for further investigation.

### How Do I Enable or Disable GuardDuty ECS Runtime Monitoring?

The simplest way to enable and ensure complete coverage is through the GuardDuty service console. You can enable ECS Runtime Monitoring for an AWS account or organization on the Runtime Monitoring page. You can opt in to having AWS manage the deployment of the agent on your behalf for all clusters in the Region, providing a "zero touch" experience for Amazon ECS operators. Alternatively, you can choose to manually deploy the agent per cluster from the Amazon ECS console. GuardDuty ECS Runtime Monitoring can be disabled for an AWS account or organization on the GuardDuty console Container Protection page. If the security agent was deployed automatically by GuardDuty, then GuardDuty will also remove the security agent when the feature is disabled; however, if the agent was deployed manually, then it needs to be manually removed through the Amazon ECS console.

### Which Operating Models and Workloads Does GuardDuty ECS Runtime Monitoring Support?

GuardDuty ECS Runtime Monitoring supports ECS workloads that use ECS agent version 1.x and above. Supported operating system distributions include Amazon Linux 2 (AL2), Amazon Linux 2023 (AL2023), Bottlerocket, and popular Ubuntu releases. Supported CPU Architectures include 64-bit x86 architecture for x86-based processors, and 64-bit ARM architecture for the AWS Graviton2 processor. GuardDuty ECS Runtime Monitoring supports Fargate platform versions for Linux (1.4.0 or latest). GuardDuty ECS Runtime Monitoring is configured for all Amazon ECS tasks and services, whether they run on Amazon EC2 instances in your account or on Fargate.  

### How Does GuardDuty Update New Agent Versions?

AWS publishes GuardDuty agent updates on a regular basis. For Amazon ECS on Amazon EC2, you can update to the latest agent version by updating to the latest ECS optimized AMI or ECS agent. For Amazon ECS on Fargate, the Fargate agent pulls the latest GuardDuty agent version automatically.

If you choose to manually deploy the agent per cluster, then you will be responsible to also update the agent when GuardDuty publicizes the release of a new version. New agent versions are carefully tested and monitored before, during, and after release. GuardDuty maintains a subset of previous agent versions so that you can roll back an update in the case where your application has a unique conflict with the agent; you can find detailed rollback procedure documented in the [GuardDuty User Guide](https://docs.aws.amazon.com/guardduty/latest/ug/what-is-guardduty.html). For CVE patches and other urgent updates, follow AWS update guidelines included in your PHD notices.

### How Does GuardDuty ECS Runtime Monitoring Affect Amazon ECS Resource Utilization and Cost?

Like all security, observability, and other use cases requiring an on-host agent, the GuardDuty security agent introduces resource utilization overhead. The GuardDuty security agent is designed to be lightweight, and it is carefully monitored by GuardDuty and Amazon ECS to minimize utilization and cost impact to covered workloads. The exact resource utilization metrics will be made available for application and security teams to monitor in AWS CloudWatch.

## GuardDuty Malware Protection

Close all

### How Does Amazon GuardDuty Malware Protection Work?

GuardDuty begins a malware detection scan when it identifies suspicious behavior indicative of malicious software in Amazon EC2 instance, or container workloads. It scans a replica Amazon EBS volume that GuardDuty generates based on the snapshot of your Amazon EBS volume for trojans, worms, crypto miners, rootkits, bots, and more. GuardDuty Malware Protection generates contextualized findings that can help validate the source of the suspicious behavior. These findings can also be routed to the proper administrators and can initiate automated remediation.

### Which GuardDuty Finding Types for Amazon EC2 Will Initiate a Malware Scan?

GuardDuty findings for Amazon EC2 that will initiate a malware scan are listed [here](https://docs.aws.amazon.com/guardduty/latest/ug/gd-findings-initiate-malware-protection-scan.html).

### Which Resources and File Types Can GuardDuty Malware Protection Scan?

Malware Protection supports detection of malicious files by scanning Amazon EBS attached to Amazon EC2 instances. It can scan any file present on the volume, and the supported file system types can be found [here](https://docs.aws.amazon.com/guardduty/latest/ug/malware-protection-limitations.html).

### Which Types of Threats Can GuardDuty Malware Protection Detect?

Malware Protection scans for threats such as trojans, worms, crypto miners, rootkits, and bots, that might be used to compromise workloads, repurpose resources for malicious use, and gain unauthorized access to data.

### Do I Need to Turn on Logging for GuardDuty Malware Protection to Work?

Service logging does not need to be enabled for GuardDuty or the Malware Protection feature to work. The Malware Protection feature is part of GuardDuty, which is an AWS service that uses intelligence from integrated internal and external sources.

### How Does GuardDuty Malware Protection Accomplish Scanning without Agents?

Instead of using security agents, GuardDuty Malware Protection will create and scan a replica based on the snapshot of Amazon EBS volumes attached to the potentially infected Amazon EC2 instance or container workload in your account. The permissions you granted to GuardDuty via a service-linked role allows the service to create an encrypted volume replica in GuardDuty’s service account from that snapshot that remains in your account. GuardDuty Malware Protection will then scan the volume replica for malware.

### Is there a Free Trial of GuardDuty Malware Protection?

Yes, each new GuardDuty account in each Region receives a 30-day free trial of GuardDuty, including the Malware Protection feature. Existing GuardDuty accounts receive a 30-day trial of Malware Protection at no additional charge the first time it is enabled in an account. During the trial period, you can view the post-trial [costs estimate on the GuardDuty console](https://docs.aws.amazon.com/guardduty/latest/ug/monitoring_costs.html) usage page. If you are a GuardDuty administrator, you will see the estimated costs for your member accounts. After 30 days, you can view actual costs of this feature in the AWS Billing console.

### If I Am Currently Using GuardDuty, how Can I Get Started with GuardDuty Malware Protection?

You can enable Malware Protection in the GuardDuty console by going to the Malware Protection page or using the API. If you are operating in a GuardDuty multi-account configuration, you can enable the feature across your entire organization in the GuardDuty administrator account’s Malware Protection console page. This will enable monitoring for malware in all individual member accounts. For GuardDuty accounts created using the [AWS Organizations](https://aws.amazon.com/organizations/) auto-enable feature, you need to explicitly enable the auto-enable for the Malware Protection option.

### If I Am a New User to GuardDuty, is Malware Protection Enabled by Default for My Accounts?

Yes, any new account that enables GuardDuty using the console or API will also have GuardDuty Malware Protection enabled by default. For new GuardDuty accounts created using the AWS Organizations auto-enable feature, you need to explicitly enable the auto-enable for Malware Protection option. 

### How Do I Disable GuardDuty Malware Protection?

You can disable the feature in the console or using the API. You will see an option to disable Malware Protection for your accounts in the GuardDuty console, on the Malware Protection console page. If you have a GuardDuty administrator account, you can also disable Malware Protection for your member accounts.

### If I Disable GuardDuty Malware Protection, how Do I Enable it Again?

If Malware Protection was disabled, you can enable the feature in the console or using the API. You can enable Malware Protection for your accounts in the GuardDuty console, on to the Malware Protection console page.

### If no GuardDuty Malware Scans Are Performed during a Billing Period, Will there Be Any Charges?

No, there will be no charges for Malware Protection if there are no scans for malware during a billing period. You can view costs of this feature in the AWS Billing console.

### Does GuardDuty Malware Protection Support Multi-account Management?

Yes, GuardDuty has a multiple account management feature, allowing you to associate and manage multiple AWS accounts from a single administrator account. GuardDuty has multi-account management through AWS Organizations integration. This integration helps security and compliance teams ensure full coverage of GuardDuty, including Malware Protection, across all accounts in an organization.

### Do I Need to Make Any Configuration Changes, Deploy Any Software, or Modify My AWS Deployments?

No. Once the feature is enabled, GuardDuty Malware Protection will initiate a malware scan in response to [relevant Amazon EC2 findings](https://docs.aws.amazon.com/guardduty/latest/ug/what-is-guardduty.html). You don’t have to deploy any agents, there are no log sources to enable, and there are no other configuration changes to make.

### Will Using GuardDuty Malware Protection Impact the Performance of Running My Workloads?

GuardDuty Malware Protection is designed to not affect the performance of your workloads. For example, Amazon EBS volume snapshots created for malware analysis can only be generated once in a 24-hour period, and GuardDuty Malware Protection retains the encrypted replicas and snapshots for a few minutes after it completes a scan. Further, GuardDuty Malware Protection uses GuardDuty compute resources for malware scanning instead of customer compute resources.

### Do I Have to Enable GuardDuty Malware Protection in Each AWS Region Individually?

Yes, GuardDuty is a regional service, and Malware Protection has to be enabled in each AWS Region separately.

### How Does GuardDuty Malware Protection Use Encryption?

GuardDuty Malware Protection scans a replica based on the snapshot of Amazon EBS volumes attached to the potentially infected Amazon EC2 instance or container workload in your account. If your Amazon EBS volumes are encrypted with a customer managed key, you have the option to share your [AWS Key Management Service (KMS) key with GuardDuty and the service](https://docs.aws.amazon.com/guardduty/latest/ug/data-protection.html) uses the same key to encrypt the replica Amazon EBS volume. For unencrypted Amazon EBS volumes, GuardDuty uses its own key to encrypt the replica Amazon EBS volume.

### Will the Amazon EBS Volume Replica Be Analyzed in Same Region as the Original Volume?

Yes, all replica Amazon EBS volume data (and the snapshot the replica volume is based on) stays in the same Region as the original Amazon EBS volume.

### How Can I Estimate and Control Spend on GuardDuty Malware Protection?

Each new GuardDuty account, in each Region, receives a 30-day free trial of GuardDuty, including the Malware Protection feature. Existing GuardDuty accounts receive a 30-day trial of Malware Protection at no additional charge the first time it is enabled in an account. During the trial period, you can estimate the post-trial [costs estimate on the GuardDuty console](https://docs.aws.amazon.com/guardduty/latest/ug/monitoring_costs.html) usage page. If you are a GuardDuty administrator, you will see the estimated costs for your member accounts. After 30 days, you can view actual costs of this feature in the AWS Billing console.

Pricing for this feature is based on the GB of data scanned in a volume. You can apply customizations using [scan options](https://docs.aws.amazon.com/guardduty/latest/ug/what-is-guardduty.html) from the console to mark some Amazon EC2 instances, [using tags](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/Using_Tags.html), to be included or excluded from scanning, thus controlling the cost. In addition, GuardDuty will only scan an Amazon EC2 instance once every 24 hours. If GuardDuty generates multiple Amazon EC2 findings for an Amazon EC2 instance within 24 hours, a scan will only occur for the first relevant Amazon EC2 finding. If Amazon EC2 findings continue, for an instance, 24 hours after the last malware scan, a new malware scan will be initiated for that instance.

### Can I Keep the Snapshots Taken by GuardDuty Malware Protection?

Yes, there is a setting where you can enable snapshot retention when Malware Protection scan detects malware. You can enable this setting from the GuardDuty console, on the Settings page. By default, snapshots are deleted a few minutes after it completes a scan and after 24 hours if the scan did not complete.

### By Default, what is the Maximum Length of time a Replica Amazon EBS Volume Will Be Retained?

GuardDuty Malware Protection will retain each replica Amazon EBS volume it generates and scans for up to 24 hours. By default, replica Amazon EBS volumes are deleted a few minutes after GuardDuty Malware Protection completes a scan. In some instances, however, GuardDuty Malware Protection may need to retain a replica Amazon EBS volume for longer than 24 hours if a service outage or connection problem interferes with its malware scan. When this occurs, GuardDuty Malware Protection will retain the replica Amazon EBS volume for up to seven days to give the service time to triage and address the outage or connection problem. GuardDuty Malware Protection will delete the replica Amazon EBS volume after the outage or failure is addressed or once the extended retention period lapses.

### Will Multiple GuardDuty Findings for a Single Amazon EC2 Instance or Container Workload that Indicate Possible Malware Initiate Multiple Malware Scans?

No, GuardDuty only scans a replica based on the snapshot of Amazon EBS volumes attached to the potentially infected Amazon EC2 instance or container workload once every 24 hours. Even if GuardDuty generates multiple findings that qualify to initiate a malware scan, it will not initiate additional scans if it has been less than 24 hours since a prior scan. If GuardDuty generates a qualified finding after 24 hours from the last malware scan, GuardDuty Malware Protection will initiate a new malware scan for that workload.

### If I Disable GuardDuty, Do I also Have to Disable the Malware Protection Feature?

No, disabling the GuardDuty service also disables the Malware Protection feature.

## GuardDuty RDS Protection

Close all

### How Does GuardDuty RDS Protection Work?

GuardDuty RDS Protection can be turned on with a single action in the GuardDuty console, with no agents to manually deploy, no data sources to activate, and no permissions to configure. Using tailored ML models, GuardDuty RDS Protection begins by analyzing and profiling login attempts to existing and new Amazon Aurora databases. When suspicious behaviors or attempts by known malicious actors are identified, GuardDuty issues actionable security findings to the GuardDuty and Amazon Relational Database Service (RDS) consoles, Security Hub, and Amazon EventBridge, allowing for integration with existing security event management or workflow systems. Learn more about [how GuardDuty RDS Protection uses RDS login activity monitoring](https://docs.aws.amazon.com/guardduty/latest/ug/rds-protection.html#understanding-how-rds-pro-works).

### How Can I Get Started with Threat Detection for Aurora Databases if I Am Currently Using GuardDuty?

For current GuardDuty accounts, the feature can be activated from the GuardDuty console on the RDS Protection page, or through the API. Learn more about [GuardDuty RDS Protection](https://docs.aws.amazon.com/guardduty/latest/ug/rds-protection.html).

### If I Am a New User to GuardDuty, is Threat Detection for Aurora Databases Enabled by Default for My Accounts?

Yes. Any new accounts that activate GuardDuty through the console or API will also have RDS Protection turned on by default. New GuardDuty accounts created using the AWS Organizations auto-enable feature will not have RDS Protection turned on unless the auto-enable for RDS option is turned on.

### Can I Use GuardDuty RDS Protection without Activating the Full GuardDuty Service (including the Analysis of Amazon Virtual Private Cloud (Amazon VPC) Flow Logs, DNS Query Logs, and AWS CloudTrail Management events)?

No, the GuardDuty service must be enabled in order to use GuardDuty RDS Protection.

### Is GuardDuty RDS Protection Available in All Regions where GuardDuty is Currently Available?

For a full list of Regions where RDS Protection is available, visit [Region-specific feature availability](https://docs.aws.amazon.com/guardduty/latest/ug/guardduty_regions.html#gd-regional-feature-availability).

### What Amazon Aurora version(s) Does GuardDuty RDS Protection Support?

Please see the list of [supported Amazon Aurora database versions](https://docs.aws.amazon.com/guardduty/latest/ug/rds-protection.html#rds-pro-supported-db).

### Will Using GuardDuty RDS Protection Impact the Performance or Cost of Running Aurora Databases?

No, GuardDuty threat detection for Aurora databases is designed to not have performance, availability, or cost implications to your Amazon Aurora databases.

## GuardDuty Lambda Protection

Close all

### How Does Amazon GuardDuty Lambda Protection Work?

GuardDuty Lambda Protection continuously monitors network activity, starting with VPC Flow Logs, from your serverless workloads to detect threats such as Lambda functions maliciously repurposed for unauthorized cryptocurrency mining, or compromised Lambda functions that are communicating with known threat actor servers. GuardDuty Lambda Protection can be enabled with a few steps in the GuardDuty console, and using AWS Organizations, can be centrally enabled for all existing and new accounts in an organization. Once enabled, it automatically starts monitoring network activity data from all existing and new Lambda functions in an account.

### How Can I Get Started with GuardDuty Lambda Protection if I Am Currently Using GuardDuty?

For current GuardDuty accounts, the feature can be activated from the GuardDuty console on the Lambda Protection page, or through the API. [Learn more about GuardDuty Lambda Protection](https://docs.aws.amazon.com/guardduty/latest/ug/lambda-protection.html).

### If I Am a New User to GuardDuty, is GuardDuty Lambda Protection Enabled by Default for My Accounts?

Yes. Any new accounts that activate GuardDuty through the console or API will also have Lambda Protection turned on by default. New GuardDuty accounts created using the AWS Organizations auto-enable feature will not have Lambda Protection turned on unless the auto-enable for Lambda option is turned on.

### Is GuardDuty Lambda Protection Available in All Regions where GuardDuty is Currently Available?

For a full list of Regions where Lambda Protection is available, visit [Region-specific feature availability](https://docs.aws.amazon.com/guardduty/latest/ug/guardduty_regions.html#gd-regional-feature-availability).

### Will Using GuardDuty Lambda Protection Impact the Performance or Cost of Running Lambda Workloads?

No, GuardDuty Lambda Protection is designed to not have performance, availability, or cost implications to your Lambda workloads.