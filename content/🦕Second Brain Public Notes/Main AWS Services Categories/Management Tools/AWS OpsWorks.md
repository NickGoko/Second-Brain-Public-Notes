---
tags:
  - cloud/aws
---
AWS OpsWorks is <mark style="background: #BBFABBA6;">a configuration management service that provides managed instances</mark> of these two open-source tools (Chef and Puppet).

<mark style="background: #BBFABBA6;">With OpsWorks AWS manage and automate how your infrastructure configured, deployed, and managed.</mark>

The difference between AWS OpsWorks for Chef and Puppet is that <mark style="background: #FFB86CA6;">Chef works with AWS OpsWorks Chef cookbooks and recipes</mark>, while <mark style="background: #ADCCFFA6;">AWS OpsWorks for Puppet Enterprise works with manifests and modules.</mark>

<mark style="background: #ADCCFFA6;">Recipes and manifests, as a rule, describe single concepts</mark>, <mark style="background: #FFB86CA6;">while cookbooks and recipes describe more general concepts.</mark>

AWS OpsWorks monitoring consists of a direct integration between AWS OpsWorks and CloudWatch.

AWS OpsWorks Logs for use and access of the service are natively and securely shipped to AWS CloudTrail.  
![[Module 14 - Planning for Disaster#^91ecc8]]

## AWS OpsWorks Stacks

AWS OpsWorks Stacks is a configuration management service within the wider OpsWorks AWS tooling that enables you to automate any tasks within your environment.

AWS OpsWorks Auto Healing for OpsWorks Stacks also allows your environments to be automatically healed to ensure your environments are proactively healthy.

A good example of these tasks may be things like scaling up and down, setting up of your database clusters, and installing packages and dependencies within your virtual machines.

Linux and Windows workloads are supported by OpsWorks stacks, and it uses Chef Recipes to configure the sorts of tasks which are best suited to being automated.

Every OpsWorks stack is built of multiple layers – each representing a different stack component, such as an individual load balancer, a database, or a set of EC2 instances.

There are number of features of AWS OpsWorks Stacks:

- EC2 instances can be deployed using template configurations, including EBS volumes.
- The software on your instances can be configured on-demand or automatically based on events that occur over time, from bootstrapping a base OS image into a running server to modifying running services to reflect changes.
- Stacks can be automatically healed by the AWS OpsWorks service. OpsWorks Stacks can replace a failed instance in your stack with a new one, ensuring maximum uptime and availability
- AWS OpsWorks Stacks integrates perfectly with Amazon CloudTrail and send logs to the CloudTrail console without having to configure this yourself.

## AWS OpsWorks for Chef Automate

**Chef Automate** is an enterprise level-platform that provides actionable insights with enterprise scale and performance across your cloud architecture.

AWS OpsWorks for Chef Automate is a managed way of launching a Chef Automate server in OpsWorks AWS.

Within AWS, you can run a Chef Automate server without having to worry about provisioning any hardware.

AWS OpsWorks Auto Healing for Chef Automate also allows your environments to be automatically healed to ensure your environments are proactively healthy.

Chef Automate handles its own operations, backups, restorations, and software upgrades also.

You can connect any on-premises computer or any EC2 instance that is running a supported operating system ([list here](http://man.hubwiz.com/docset/Chef.docset/Contents/Resources/Documents/docs.chef.io/platforms.html)) which has network access to an AWS OpsWorks for Chef Automate server.

You can configure automatic backups natively, and the backups are stored in S3.

Adding new nodes to your Chef server is as simple as inserting the user-data code provided by OpsWorks for Chef Automate into your Auto Scaling groups.

All Chef communication is encrypted using SSL to ensure that the server will communicate safely and securely with other aspects of your architecture.

You receive the full Chef Automate platform which includes premium features that you can use with Chef server, like Chef Workflow, Chef Visibility, and Chef Compliance, all within the same service.

OpsWorks for Chef Automate can also install updates automatically during a weekly maintenance window, one which you define.

You can launch a Chef Automate server through the console, using CloudFormation, or using the CLI or the SDK.

## AWS OpsWorks for Puppet Enterprise

OpsWorks for Puppet Enterprise is another subset of OpsWorks which lets you launch a Puppet Enterprise master in minutes, compared to hours.

You can configure automatic backups natively, and the backups are stored in S3.

Adding new nodes to your Puppet Enterprise server is as simple as inserting the user-data code provided by AWS OpsWorks for Puppet Enterprise into your Auto Scaling groups.

Puppet Enterprise communication is encrypted using SSL to ensure that the server will communicate safely and securely with other aspects of your architecture.

Deleting a Puppet Enterprise server will also delete everything associated with it, including backups and all other supporting resources.

AWS OpsWorks for Puppet Enterprise can also install updates automatically during a weekly maintenance window, one which you define.

You can launch a Puppet Enterprise server through the console, using CloudFormation, or using the CLI or the SDK.

## AWS OpsWorks Pricing

For OpsWorks Stacks, there is no additional charge. You pay for any resources you launch as part of the service, but nothing for OpsWorks Stacks.

On-premises deployments of OpsWorks stacks cost $0.02 per hour and with both deployments there are no minimum fees and no upfront commitments.

AWS OpsWorks for Chef Automate and for Puppet Enterprise are charged separately.

You are charged based on the number of nodes connected to your Chef Automate instance the times they are running for and the EC2 instance which is running.

The final price considers the number of nodes per month, and the number of node hours.

For both OpsWorks Puppet Enterprise and Chef Automate you benefit from 7,500 node hours free per month with the AWS Free Tier.

## OpsWorks AWS Endpoints and Quotas

OpsWorks for Chef Automate and AWS OpsWorks for Puppet Enterprise isn’t currently available in all Regions – and only exists in nine regions currently ([list here](https://docs.aws.amazon.com/general/latest/gr/opsworks-service.html).)

OpsWorks Stacks exists in fifteen regions instead, and any resources cannot be managed from other regions.

Please see the table below for information on the service quotas for AWS OpsWorks stacks.

|   |   |   |   |
|---|---|---|---|
|**Name**|**Description**|**Default Limit (Per Region)**|**Hard / Soft Limit**|
|Stacks|Number of Stacks|40|Soft|
|Layers per Stack|Multiple different stack components, such as an individual load balancer, a database, or a set of EC2 instances.|40|Soft|
|Instances per Stack|The maximum number of instances that you can have in an OpsWorks stack.|40|Soft|
|Apps per Stack|The maximum number of apps that you can have in an OpsWorks stack.|40|Soft|

Please see the table below for information on the service quotas for OpsWorks for Chef Automate and AWS OpsWorks for Puppet Enterprise.

|   |   |   |
|---|---|---|
|**Name**|**Default Limit (Per Region)**|**Hard / Soft Limit**|
|Manual backups per server|10|Soft|
|Number of scheduled (automated) backups per server|10|Soft|
|Number of servers|5|Soft|


![[Module 10 - Automatic Your Architecture#AWS OpsWorks]]

# FAQ
## General

**Q: What is AWS OpsWorks for Chef Automate?  
**

AWS OpsWorks for Chef Automate provides a fully managed Chef server and suite of automation tools that give you workflow automation for continuous deployment, automated testing for compliance and security, and a user interface that gives you visibility into your nodes and their status. The Chef server gives you full stack automation by handling operational tasks such as software and operating system configurations, package installations, database setups, and more. The Chef server centrally stores your configuration tasks and provides them to each node in your compute environment at any scale, from a few nodes to thousands of nodes. OpsWorks for Chef Automate is completely compatible with tooling and cookbooks from the Chef community and automatically registers new nodes with your Chef server.  

**Q: How is OpsWorks for Chef Automate different from OpsWorks Stacks?  
**

OpsWorks for Chef Automate is a configuration management service that helps you instantly provision a Chef server and lets the service operate it, including performing backups and software upgrades. The service offers full compatibility with Chef’s Supermarket cookbooks and recipes. It supports native Chef tools such as TestKitchen and Knife. The OpsWorks Stacks service helps you model, provision, and manage your applications on AWS using the embedded Chef solo client that is installed on Amazon EC2 instances on your behalf. To learn more, see [OpsWorks Stacks](https://aws.amazon.com/opsworks/stacks/).  

**Q: Who should use OpsWorks for Chef Automate?  
**

Customers who are looking for a configuration management experience that is fully compatible with Chef, including all community scripts and tooling, but without operational overhead should adopt OpsWorks for Chef Automate.  

**Q: How can I access OpsWorks for Chef Automate?  
**

The OpsWorks for Chef Automate service is available through the AWS Management Console, AWS SDKs, and the AWS Command Line Interface (CLI). After the Chef server has been set up, it can also be managed by Chef-compatible tools such as Knife.  

**Q: In which regions is OpsWorks for Chef Automate available?**

See [Regional Products and Services](https://aws.amazon.com/about-aws/global-infrastructure/regional-product-services/) for details.  

**Q: Are there any limits to OpsWorks for Chef Automate?  
**

The default service limits are:

- Configuration management servers per region: 5
- Automated backups per configuration management server: 30
- Manual backups per configuration management server: 10

If you would like to change these limits, contact AWS Support.  

**Q: What network requirements must my servers meet to work with OpsWorks for Chef Automate?  
**

Your servers must be able to connect to AWS public endpoints. See the [documentation](https://docs.aws.amazon.com/general/latest/gr/rande.html#opsworks_region) for details.  

**Q: What is Chef and how does OpsWorks for Chef Automate use it?  
**

Chef Automate is a software bundle by [Chef Software, Inc.](https://www.chef.io/automate/) that automates how applications are configured, deployed, and managed through the use of code. OpsWorks for Chef Automate uses Chef recipes to deploy and configure software components on Amazon EC2 instances and on-premises servers. Chef has a rich ecosystem with hundreds of cookbooks that can be used in AWS, such as cookbooks for managing PostgreSQL, Nginx, Solr, and many more.  

**Q: What is Chef Automate?  
**

Chef Automate gives you a full-stack, continuous deployment pipeline, automated testing for compliance and security, and visibility into everything that's happening along the way. It builds on Chef for infrastructure automation, InSpec for compliance automation, and Habitat for application automation. You can transform your company into a highly collaborative, software-driven organization with Chef Automate as the engine. To learn more, see the [Chef Automate product details page](https://www.chef.io/automate/).  

**Q: How do I use the Chef Automate console?  
**

Chef Automate includes its own console. The Chef Automate Console can be accessed through the OpsWorks link on the the AWS Management Console. After you click the link, you will be prompted for the credentials that you were assigned when you set up the Chef Automate server.  

**Q: I am an AWS OpsWorks Stacks customer. Should I migrate to OpsWorks for Chef Automate?  
**

OpsWorks Stacks customers who are looking for full Chef server compatibility are encouraged to use OpsWorks for Chef Automate. To learn more about OpsWorks Stacks, see the [OpsWorks Stacks product details page](https://aws.amazon.com/opsworks/stacks/).  

**Q: How can I migrate from OpsWorks Stacks to OpsWorks for Chef Automate?  
**

Before you migrate, you first have to adapt your OpsWorks cookbooks to work on a Chef server. Some may work without alterations, however. If you are using OpsWorks instance scaling (either time-based or load-based), you’ll need to use an EC2 Auto Scaling group and OpsWork Chef’s node registration feature instead. You will later be able to work with your Chef server and nodes by using Chef’s Visibility console or Knife.  

**Q: Which versions of Chef are supported?  
**

The OpsWorks for Chef Automate service will regularly upgrade your Chef server to the latest recommended version. Please see our [documentation](https://docs.aws.amazon.com/opsworks/latest/userguide/welcome_opscm.html) for the latest supported version. We recommend running the most current, stable [chef-client version](https://downloads.chef.io/chef/stable) on nodes associated with an AWS OpsWorks for Chef Automate server.  

**Q: Which cloud resources power my AWS OpsWorks for Chef Automate server?  
**

AWS OpsWorks for Chef Automate uses proven AWS features and services, such as Amazon EC2, Amazon EBS, Amazon S3, and Amazon CloudWatch to create the components that make up your managed Chef server. OpsWorks for Chef Automate uses the Amazon Linux Amazon Machine Image (AMI).  

**Q: How can I back up my Chef server?  
**

You can define a daily or weekly recurring Chef server backup. The service stores the backups in Amazon S3 on your behalf. Alternatively, you can choose to create manual backups on demand.  

**Q: How many backups can I keep for every Chef server?  
**

Backups are stored in Amazon S3 and incur additional fees. You can define a backup retention period of up to 30 generations. You can submit a service request to change that limit by using AWS Support channels.  

**Q: How can I restore my Chef server to an earlier point in time?  
**

After browsing through your available backups, you can choose a point in time from which to restore your Chef server. Server backups contain only Chef software persistent data such as cookbooks and registered nodes.  

**Q: Which resources can I connect to my Chef server?  
**

You can connect any EC2 instance or on-premises server that is running a supported operating system and has Internet access to an OpsWorks for Chef Automate server. You are charged an hourly fee for every connected resource.  

**Q: How do I register nodes with the Chef server?  
**

You’ll get user-data code snippets through the console. You can put these code snippets in an EC2 Auto Scaling group. These code snippets ensure that your instances are registered to your Chef server as Chef nodes, and that they run the corresponding Chef recipes. On-premises servers require that you install the Chef client agent software and register the server with your Chef server.  

**Q: How can I obtain Chef related training?  
**

You can choose your preferred Chef Automate training method from Chef’s [website](https://training.chef.io/).

- In Person Training - Chef offers in person classes that will meet your needs regardless of your skill level.
- Online Instructor-Led Training - No need to leave your home or office for Chef training.
- Self-Paced Training - Learn new skills whenever you have time.
- Private Training - Chef training delivered when and where you need it.  
    

## Maintenance Window

**Q: How can I keep the underlying Chef server running and up-to-date?  
**

Your managed configuration management server is updated to the latest version of Chef Automate during the maintenance window that you configure. OpsWorks for Chef Automate also regularly runs security updates and operating system package updates for you.  

**Q: What is an OpsWorks for Chef Automate maintenance window?  
**

A maintenance window is a daily or weekly one-hour time slot during which OpsWorks for Chef Automate initiates Chef version updates without breaking changes, security updates, and operating system package updates. For example, if you select a maintenance window that begins every Sunday at 2:00 A.M., OpsWorks for Chef Automate initiates the platform update between 2:00 and 3:00 A.M. every Sunday.

The maintenance window is set on a per-Chef-server basis, so you can set different maintenance times for different Chef servers. If you want to change when maintenance is performed, you can use the OpsWorks for Chef Automate console, the AWS CLI or APIs.  

**Q: How do I set up a maintenance window?  
**

The maintenance window is enabled by default and can be set during the Chef server setup phase. You can change settings later by using the AWS Management Console, CLI, or APIs.  

**Q: What kinds of version updates will be performed by OpsWorks for Chef Automate?  
**

OpsWorks for Chef Automate performs version updates automatically as long as the updates include backward-compatible changes. When new versions of Chef software become available, system maintenance is designed to update the version of Chef Automate and Chef Server on the server automatically, as soon as the version update passes AWS testing. AWS performs extensive testing to verify that Chef upgrades are production-ready and do not disrupt existing customer environments, so there can be lags between Chef software releases and their availability for application to existing OpsWorks for Chef Automate servers.  

**Q: When and how can I perform major version updates?  
**

You can perform major version updates at any time by using the AWS OpsWorks for Chef Automate console, API, or CLI.  

**Q: How does AWS OpsWorks for Chef Automate apply updates?  
**

The updates are applied directly to the managed EC2 instance on which the Chef server is running. If the OpsWorks for Chef Automate health system detects any issues during the update, OpsWorks for Chef Automate will roll back changes and try again during the next maintenance window.  

**Q: Will my Chef server be available during the maintenance window?  
**

Your Chef server is not available when maintenance updates are being applied. Your connected nodes enter a pending-server state until maintenance is complete. The connected nodes will continue to operate normally.  

**Q: How will I be notified of the availability of new OpsWorks for Chef Automate versions?  
**

You are notified about new Chef versions through the OpsWorks for Chef Automate console. The service console informs you if your Chef server was updated during the maintenance window.  

**Q: Where can I find details about changes between platform versions?  
**

Details about changes between Chef Automate versions are on the [Chef Automate Release Notes](https://docs.chef.io/release_notes_automate/) page.  

**Q: How often are platform version updates released?  
**

The number of version releases each year varies based on the frequency of Chef Automate patch releases from Chef and acceptance testing performed by AWS.  

## Getting Started

**Q: How do I get started with OpsWorks for Chef Automate?  
**

The best way to get started with OpsWorks for Chef Automate is to review the AWS OpsWorks for Chef Automate Getting Started chapter of the technical [documentation](http://docs.aws.amazon.com/opsworks/latest/userguide/gettingstarted-opscm.html).  

## Configuration and Management

**Q: How do I create Chef cookbooks and recipes?  
**

The easiest way to get started is to use existing Chef recipes. Many public repositories contain Chef cookbooks with recipes that can run with little to no modification. The OpsWorks for Chef Automate Starter Kit also includes an example Chef recipe and describes how it works.  

**Q: Can I use community cookbooks from the Chef Supermarket?  
**

Yes. OpsWorks for Chef Automate provides configuration management experience that is fully compatible with Chef Automate. You can use [community-authored cookbooks](https://supermarket.chef.io/) with no AWS-specific modifications.  

**Q: How do I upgrade my Chef nodes to a newer release version?  
**

Chef node upgrades can be done at your convenience by using the [Chef omnibus recipe](https://github.com/hw-cookbooks/omnibus_updater). Although OpsWorks regularly performs Chef server version upgrades on your behalf, your Chef nodes continue to operate even if they remain on the earlier version.  

**Q: Does my OpsWorks for Chef Automate server support community tools like Knife and Test Kitchen?  
**

Yes. OpsWorks for Chef Automate provides configuration management experience that is fully compatible with Chef Automate. You can use the same ecosystem of tools as an on-premises Chef Automate server.  

**Q: Is there a sample cookbook that I can use to check out OpsWorks for Chef Automate?  
**

Yes. The OpsWorks for Chef Automate Starter Kit includes a sample cookbook that you can use to test drive the offering and explore its functionality.  

## Security

**Q: Is it possible to use AWS Identity and Access Management (IAM) with OpsWorks for Chef Automate?  
**

Yes. IAM users with the appropriate permissions can work with AWS OpsWorks for Chef Automate. The Chef users are not managed by IAM and must be provisioned from within Chef Automate.  

**Q: How do I create IAM users?  
**

You can use the [IAM console](https://console.aws.amazon.com/iam/), IAM command line interface (CLI), or IAM API to provision IAM users. By default, IAM users have no access to AWS services until permissions are granted.  

**Q: Do I have root access to my OpsWorks for Chef Automate server EC2 instance?  
**

Yes. You can provide an SSH key pair to enable root access to the OpsWorks for Chef Automate server EC2 instance. OpsWorks for Chef Automate provides you with tooling to perform common operational tasks, and so we recommend that you disable SSH access.  

**Q: Where can I find more information about security and running applications on AWS?  
**

See Amazon Web Services: Overview of Security Processes and the [AWS Security Center](https://aws.amazon.com/security/).  

**Q: Can I get a history of OpsWorks for Chef Automate API calls made on my account for security analysis and troubleshooting purposes?  
**

Yes. To get a history of OpsWorks for Chef Automate API calls made on your account, you simply turn on AWS CloudTrail in the AWS Management Console.  

## Billing

**Q: How much do the AWS resources powering my application on OpsWorks for Chef Automate server cost?  
**

The OpsWorks for Chef Automate server is configured on your behalf and powered by Amazon EC2, Amazon EBS, Amazon S3, and Amazon CloudWatch. For EC2 pricing information, see the [EC2 pricing page](https://aws.amazon.com/ec2/pricing/). For S3 pricing information, see the [S3 pricing page](https://aws.amazon.com/s3/pricing/). For CloudWatch pricing information, see the [CloudWatch pricing page](https://aws.amazon.com/cloudwatch/pricing/). There are three EC2 instance types to choose from for running the Chef server: m4.large, r4.xlarge, r4.2xlarge. The hourly rate depends on the instance type used.  

**Q: Am I billed for EC2 instances and on-premises servers that are connected to my OpsWorks for Chef Automate server?  
**

You pay an hourly fee for each EC2 instance and on-premises server that is connected to an AWS OpsWorks for Chef Automate server. There are no minimum fees and no upfront commitments. For more information, see our [pricing page](https://aws.amazon.com/opsworks/chefautomate/pricing/).  

**Q: How do I view the cost of AWS resources that have been used by my OpsWorks for Chef Automate server?  
**

OpsWorks for Chef Automate automatically tags all Chef server resources with the name of your Chef server. You can use these tags with Cost Allocation Reports to organize and track your AWS costs. See [AWS Account Billing](https://console.aws.amazon.com/billing/home) for details.  

## Support

**Q: Does AWS Support cover OpsWorks for Chef Automate?  
**

Yes. [AWS Support](https://aws.amazon.com/premiumsupport/) covers issues related to your use of OpsWorks for Chef Automate. See the [Compare AWS Support Plans page](https://aws.amazon.com/premiumsupport/compare-plans/) for details.  

**Q: What other support options are available?  
**

You can tap into the breadth of existing AWS community knowledge to help you with your development by using the AWS OpsWorks discussion forum. See the [AWS OpsWorks Forums page](https://forums.aws.amazon.com/forum.jspa?forumID=153) for details.