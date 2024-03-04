---
tags:
  - cloud/aws
---

![](https://i.imgur.com/dtyFPbl.png)  
![](https://i.imgur.com/PTzrqfQ.png)

### Deployment Options for Elastic BeanStalk.
![](https://i.imgur.com/L9P2Xew.png)

![](https://i.imgur.com/wMdKjlw.png)
- All the instances are stopped so there is some downtime

![](https://i.imgur.com/Ig0PgiD.png)  
Some downtime is expected but only for some of the instance where the other run. However during that period capacity is reduced.  
![](https://i.imgur.com/aigju2m.png)


![](https://i.imgur.com/NpSEYnf.png)


![](https://i.imgur.com/CgP9Tw8.png)


<mark style="background: #BBFABBA6;">Summary</mark>  
![](https://i.imgur.com/xyikZlj.png)

AWS Elastic Beanstalk can be used to quickly deploy and manage applications in the AWS Cloud.

Developers upload applications and Elastic Beanstalk handles the deployment details of capacity provisioning, load balancing, auto-scaling, and application health monitoring.

You can use multiple availability zones to improve application reliability and availability.

Considered a Platform as a Service (PaaS) solution.

Supports the following platforms:
- [Docker](https://docs.aws.amazon.com/elasticbeanstalk/latest/platforms/platforms-supported.html#platforms-supported.docker)
- [Multicontainer Docker](https://docs.aws.amazon.com/elasticbeanstalk/latest/platforms/platforms-supported.html#platforms-supported.mcdocker)
- [Preconfigured Docker](https://docs.aws.amazon.com/elasticbeanstalk/latest/platforms/platforms-supported.html#platforms-supported.dockerpreconfig)
- [Go](https://docs.aws.amazon.com/elasticbeanstalk/latest/platforms/platforms-supported.html#platforms-supported.go)
- [Java SE](https://docs.aws.amazon.com/elasticbeanstalk/latest/platforms/platforms-supported.html#platforms-supported.javase)
- [Tomcat](https://docs.aws.amazon.com/elasticbeanstalk/latest/platforms/platforms-supported.html#platforms-supported.java)
- [.NET Core on Linux](https://docs.aws.amazon.com/elasticbeanstalk/latest/platforms/platforms-supported.html#platforms-supported.dotnetlinux)
- [.NET on Windows Server](https://docs.aws.amazon.com/elasticbeanstalk/latest/platforms/platforms-supported.html#platforms-supported.net)
- [Node.js](https://docs.aws.amazon.com/elasticbeanstalk/latest/platforms/platforms-supported.html#platforms-supported.nodejs)
- [PHP](https://docs.aws.amazon.com/elasticbeanstalk/latest/platforms/platforms-supported.html#platforms-supported.PHP)
- [Python](https://docs.aws.amazon.com/elasticbeanstalk/latest/platforms/platforms-supported.html#platforms-supported.python)
- [Ruby](https://docs.aws.amazon.com/elasticbeanstalk/latest/platforms/platforms-supported.html#platforms-supported.ruby)

- <mark style="background: #ABF7F7A6;">Developers can focus on writing code and don’t need to worry about deploying infrastructure.</mark>
- You pay only for the resources provisioned, not for Elastic Beanstalk itself.
- <mark style="background: #BBFABBA6;">Elastic Beanstalk automatically scales your application up and down.</mark>
- <mark style="background: #FFB86CA6;">You can select the EC2 instance type that is optimal for your application.</mark>
- Can retain full administrative control or have Elastic Beanstalk do it for you.
- The Managed Platform Updates feature automatically applies updates for your operating system and platform.
- <mark style="background: #ABF7F7A6;">Elastic Beanstalk monitors and manages application health and information is viewable via a dashboard.</mark>
- Integrated with CloudWatch and X-Ray for performance data and metrics.
- Integrates with Amazon VPC and AWS IAM.
- Can provision most database instances.
- <mark style="background: #FFB86CA6;">Stores your application files and, optionally, server log files in Amazon S3.</mark>  
  Application data can also be stored on S3.
- Multiple environments are supported to enable versioning.
- <mark style="background: #ABF7F7A6;">Changes from Git repositories are replicated.</mark>
- Linux and Windows AMI support.
- Code is deployed using a WAR file or Git repository.
- <mark style="background: #ABF7F7A6;">Can use the AWS toolkit for Visual Studio and the AWS toolkit for Eclipse to deploy Elastic Beanstalk.</mark>
- Fault tolerance within a single region.
- By default applications are publicly accessible.
- Can access logs without logging into application servers.
- Provides ISO, PCI, SOC 1, SOC 2, and SOC 3 compliance along with the criteria for HIPAA eligibility.
- Supports AWS Graviton arm64-based processors.

## Elastic Beanstalk Layers
There are several layers that make up Elastic Beanstalk and each layer is described below:

**Application**:
- Within Elastic Beanstalk, <mark style="background: #BBFABBA6;">an application is a collection of different elements, such as environments, environment configurations, and application versions.</mark>
- You can have multiple application versions held within an application.

**Application version**:
- An application version is a very specific reference to a section of deployable code.
- The application version will point typically to an Amazon s3 bucket containing the code.

**Environment**:
- An environment refers to an application version that has been deployed on AWS resources.
- The resources are configured and provisioned by AWS Elastic Beanstalk.
- The environment is comprised of all the resources created by Elastic Beanstalk and not just an EC2 instance with your uploaded code.

![Elastic Beanstalk Applications Environments and Versions](https://digitalcloud.training/wp-content/uploads/2022/01/elastic-beanstalk-applications-environments-and-ve.jpeg)

**Environment tier**:
- Determines how Elastic Beanstalk provisions resources based on what the application is designed to do.
- **Web servers** are standard applications that listen for and then process HTTP requests, typically over port 80.
- **Workers** are specialized applications that have a background processing task that listens for messages on an Amazon SQS queue.

**Environment configurations**:

- An environment configuration is a collection of parameters and settings that dictate how an environment will have its resources provisioned by Elastic Beanstalk and how these resources will behave.

**Configuration template**:

- This is a template that provides the baseline for creating a new, unique environment configuration.

## Deployment Options

AWS Elastic Beanstalk provides several options for how [**deployments**](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/using-features.deploy-existing-version.html) are processed, including deployment policies and options that let you configure batch size and health check behavior during deployments.

### Deployment Options
Single instance: great for development.  
High availability with load balancer: great for production.

### Deployment Policies
The deployment policies are: <mark style="background: #ABF7F7A6;">All at once, Rolling, Rolling with additional batch, and Immutable.</mark>

#### All at Once:
- Deploys the new version to all instances simultaneously.
- All your instances are out of service while the deployment takes place.
- Fastest deployment.
- Good for quick iterations in the development environment.
- You will experience an outage while the deployment is taking place – not ideal for mission-critical systems.
- If the update fails, you need to roll back the changes by re-deploying the original version to all your instances.
- No additional cost.

#### Rolling:

- Update a few instances at a time (batch), and then move onto the next batch once the first batch is healthy (downtime for 1 batch at a time).
- The application is running both versions simultaneously.
- Each batch of instances is taken out of service while the deployment takes place.
- Your environment capacity will be reduced by the number of instances in a batch while the deployment takes place.
- Not ideal for performance-sensitive systems.
- If the update fails, you need to perform an additional rolling update to roll back the changes.
- No additional cost.
- Long deployment time.

#### Rolling with Additional Batch:
- Like Rolling but launches new instances in a batch ensuring that there is full availability.
- The application is running at capacity.
- You can set the bucket size.
- The application is running both versions simultaneously.
- Small additional cost.
- Additional batch is removed at the end of the deployment.
- Longer deployment.
- Good for production environments.

#### Immutable:
- Launches new instances in a new ASG and deploys the version update to these instances before swapping traffic to these instances once healthy.
- Zero downtime.
- New code is deployed to new instances using an ASG.
- High cost as double the number of instances running during updates.
- Longest deployment.
- Quick rollback in case of failures.
- Great for production environments.

Additionally, Elastic Beanstalk supports blue/green deployment.

#### Blue / Green Deployment:

- <mark style="background: #BBFABBA6;">This is not a feature within Elastic Beanstalk</mark>
- <mark style="background: #D2B3FFA6;">You create a new “staging” environment and deploy updates there.</mark>
- <mark style="background: #ABF7F7A6;">The new environment (green) can be validated independently, and you can roll back if there are issues.</mark>
- <mark style="background: #ADCCFFA6;">Route 53 can be set up using weighted policies to redirect a percentage of traffic to the staging environment.</mark>
- <mark style="background: #CACFD9A6;">Using Elastic Beanstalk, you can “swap URLs” when done with the environment test.</mark>
- <mark style="background: #BBFABBA6;">Zero downtime.</mark>

## Golden AMIs

When deploying code to Amazon EC2 using Beanstalk, Elastic Beanstalk must resolve application dependencies which can take a long time.

<mark style="background: #D2B3FFA6;">A golden AMI is a method of reducing this time by packaging all dependencies, configuration, and software into the AMI before deploying</mark>.

## Elastic Beanstalk CLI

There is an additional CLI called “eb cli”.

The EB CLI is a command-line interface for AWS Elastic Beanstalk that provides interactive commands that simplify creating, updating, and monitoring environments from a local repository.

You can use the EB CLI as part of your everyday development and testing cycle as an alternative to the Elastic Beanstalk console.

## Lifecycle Policies

Elastic Beanstalk can store at most 1000 application versions.

To phase out old versions use a lifecycle policy:
- Time-based – specify max age.
- Count based – specify max number to retain.

Versions that are in use will not be deleted.

Option to not delete the source bundle in S3 to prevent data loss.

## Worker Environments

If an application performs tasks that take a long time to complete (long-running tasks), offload to a worker environment.

It allows you to decouple your application tiers.

Can define periodic tasks in the cron.yaml file.

![Elastic Beanstalk Worker Environment](https://digitalcloud.training/wp-content/uploads/2022/01/elastic-beanstalk-worker-environment.jpeg)

## Elastic Beanstalk Extensions

<mark style="background: #BBFABBA6;">You can add AWS Elastic Beanstalk configuration files</mark> **(.ebextensions)** <mark style="background: #BBFABBA6;">to your web application’s source code to configure your environment and customize the AWS resources that it contains.</mark>

<mark style="background: #FF5582A6;">Customization includes defining packages to install, create Linux users and groups, running shell commands, specifying services to enable, configuring a load balancer, etc.</mark>

<mark style="background: #BBFABBA6;">Configuration files are YAMLor JSON-formatted documents with a </mark>**.config** <mark style="background: #BBFABBA6;">file extension that you place in a folder named</mark> **.ebextensions** <mark style="background: #BBFABBA6;">and deploy in your application source bundle.</mark>

<mark style="background: #FFB86CA6;">The .ebextensions folder must be included in the top-level directory of your application source code bundle.</mark>

All the parameters set in the UI can be configured in the code.

Requirements:
- Must be in the .ebextensions/ directory of the source code.
- YAML or JSON format.
- .config extensions can be included (e.g. logging.config).
- You can modify some default settings using “option_settings”.
- You can add resources such as RDS, ElastiCache, and DynamoDB.

Resources managed by .ebextensions get deleted if the environment is terminated.

## Elastic Beanstalk with Amazon Relational Database Service (RDS)

You can deploy Amazon RDS within an Elastic Beanstalk environment as in the diagram below:

![Elastic Beanstalk Environment with RDS](https://digitalcloud.training/wp-content/uploads/2022/01/elastic-beanstalk-environment-with-rds.jpeg)  
<mark style="background: #CACFD9A6;">However, if you terminate your Elastic Beanstalk environment you also lose the database.  
The use case is only for development environments, typically not suitable for production.  
</mark>


For production, it is preferable to create the Amazon RDS database outside of Elastic Beanstalk as in the diagram below:  
![Elastic Beanstalk and Amazon RDS](https://digitalcloud.training/wp-content/uploads/2022/01/elastic-beanstalk-and-amazon-rds.jpeg)

<mark style="background: #ABF7F7A6;">Steps to migrate from RDS within a Beanstalk environment to standalone RDS:</mark>

- Take a snapshot of the RDS DB.
- Enable deletion protection on the RDS DB.
- Create a new environment without an RDS DB and point applications to the existing RDS DB.
- Perform a blue/green deployment and swap the new and old environments.
- Terminate the old environment (RDS will not be deleted due to termination protection).
- Delete the CloudFormation stack (will be in the DELETE_FAILED state).

### Connecting to an Amazon RDS Database

When the environment update is complete, the DB instance’s hostname and other connection information are available to your application through the following environment properties:

- RDS_HOSTNAME – The hostname of the DB instance.
- RDS_PORT – The port on which the DB instance accepts connections. The default value varies among DB engines.
- RDS_DB_NAME – The database name, ebdb.
- RDS_USERNAME – The user name that you configured for your database.
- RDS_PASSWORD – The password that you configured for your database.

## Custom Domain Names

<mark style="background: #D2B3FFA6;">If you’re using AWS Elastic Beanstalk to deploy and manage applications in the AWS Cloud, you can use Amazon Route 53 to route DNS traffic for your domain, such as example.com, to a new or an existing Elastic Beanstalk environment.</mark>

You create either a _CNAME record_ or an _alias record_, depending on whether the domain name for the environment includes the Region, such as **us-east-2**, in which you deployed the environment. New environments include the Region in the domain name; environments that were created before early 2016 do not.

If the domain name does NOT include the Region: create a CNAME record.

If the domain name DOES include the Region: create an Alias record.

## Security

Elastic Beanstalk works with HTTPS:

- Load the SSL certificate onto the load balancer.
- Can be performed from the console or in code (.ebextensions/securelistener-alb.config).
- SSL certificate can be provisioned using ACM or CLI.

For redirecting HTTP to HTTPS:

- Configure in the application.
- Configure the ALB with a rule.
- Ensure health checks are not redirected.

## Monitoring and Reporting

Elastic Beanstalk automatically uses [**Amazon CloudWatch**](https://digitalcloud.training/amazon-cloudwatch/) to help you monitor your application and environment status.

You can navigate to the Amazon CloudWatch console to see your dashboard and get an overview of all your resources as well as your alarms.

You can also choose to view more metrics or add custom metrics.

## Logging and Auditing

With CloudWatch Logs, you can monitor and archive your Elastic Beanstalk application, system, and custom log files from Amazon EC2 instances of your environments.

You can also configure alarms that make it easier for you to react to specific log stream events that your metric filters extract.

The CloudWatch Logs agent installed on each Amazon EC2 instance in your environment publishes metric data points to the CloudWatch service for each log group you configure.

Each log group applies its own filter patterns to determine what log stream events to send to CloudWatch as data points.

Log streams that belong to the same log group share the same retention, monitoring, and access control settings.

In addition to instance logs, if you enable [**enhanced health**](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/health-enhanced.html) for your environment, you can configure the environment to stream health information to CloudWatch Logs.

## Authorization and Access Control

AWS Elastic Beanstalk supports [**identity-based**](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/AWSHowTo.iam.html) policies.

AWS Elastic Beanstalk does not support [**resource-based**](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_identity-vs-resource.html) policies.

AWS Elastic Beanstalk has partial support for [**resource-level**](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_aws-services-that-work-with-iam.html) permissions.

When you create an environment, AWS Elastic Beanstalk prompts you to provide two AWS Identity and Access Management (IAM) roles: a service role and an instance profile.

The [**service role**](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/concepts-roles-service.html) is assumed by Elastic Beanstalk to use other AWS services on your behalf.

The [**instance profile**](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/concepts-roles-instance.html) is applied to the instances in your environment and allows them to retrieve [**application versions**](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/concepts.html#concepts-version) from Amazon Simple Storage Service (Amazon S3), upload logs to Amazon S3, and perform other tasks that vary depending on the environment type and platform.

You can also create [**user policies**](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/concepts-roles-user.html) and apply them to IAM users and groups in your account to allow users to create and manage Elastic Beanstalk applications and environments. Elastic Beanstalk provides managed policies for full access and read-only access.


![[Module 10 - Automatic Your Architecture#AWS Elastic Beanstalk]]

## General

[Q: What is AWS Elastic Beanstalk? >>](https://aws.amazon.com/elasticbeanstalk/faqs//#)

**Q: What is AWS Elastic Beanstalk?**

AWS Elastic Beanstalk makes it even easier for developers to quickly deploy and manage applications in the AWS Cloud. Developers simply upload their application, and Elastic Beanstalk automatically handles the deployment details of capacity provisioning, load balancing, auto-scaling, and application health monitoring.

[Show less](https://aws.amazon.com/elasticbeanstalk/faqs//#)

[Q: Who should use AWS Elastic Beanstalk? >>](https://aws.amazon.com/elasticbeanstalk/faqs//#)

**Q: Who should use AWS Elastic Beanstalk?**

Those who want to deploy and manage their applications within minutes in the AWS Cloud. You don’t need experience with [cloud computing](https://aws.amazon.com/what-is-cloud-computing/) to get started. AWS Elastic Beanstalk supports Java, .NET, PHP, Node.js, Python, Ruby, Go, and Docker web applications.  

[Show less](https://aws.amazon.com/elasticbeanstalk/faqs//#)

[Q: Which languages and development stacks does AWS Elastic Beanstalk support? >>](https://aws.amazon.com/elasticbeanstalk/faqs//#)

**Q: Which languages and development stacks does AWS Elastic Beanstalk support?**

AWS Elastic Beanstalk supports the following languages and development stacks:

Apache Tomcat for Java applications

Apache HTTP Server for PHP applications

Apache HTTP Server for Python applications

Nginx or Apache HTTP Server for Node.js applications

Passenger or Puma for Ruby applications

Microsoft IIS 7.5, 8.0, and 8.5 for .NET applications

Java SE

Docker

Go

See Supported Platforms for a complete, up-to-date list of supported language and development stacks.  

[Show less](https://aws.amazon.com/elasticbeanstalk/faqs//#)

[Q: Will AWS Elastic Beanstalk support other languages? >>](https://aws.amazon.com/elasticbeanstalk/faqs//#)

**Q: Will AWS Elastic Beanstalk support other languages?**

Yes. AWS Elastic Beanstalk is designed so that it can be extended to support multiple development stacks and programming languages in the future. AWS is working with solution providers on the APIs and capabilities needed to create additional Elastic Beanstalk offerings.  

[Show less](https://aws.amazon.com/elasticbeanstalk/faqs//#)

[Q: What can developers now do with AWS Elastic Beanstalk that they could not before? >>](https://aws.amazon.com/elasticbeanstalk/faqs//#)

**Q: What can developers now do with AWS Elastic Beanstalk that they could not before?**

AWS Elastic Beanstalk automates the details of capacity provisioning, load balancing, auto scaling, and application deployment, creating an environment that runs a version of your application. You can simply upload your deployable code (e.g., WAR file), and AWS Elastic Beanstalk does the rest. The AWS Toolkit for Visual Studio and the AWS Toolkit for Eclipse allow you to deploy your application to AWS Elastic Beanstalk and manage it without leaving your IDE. Once your application is running, Elastic Beanstalk automates management tasks–such as monitoring, application version deployment, a basic health check–and facilitates log file access. By using Elastic Beanstalk, developers can focus on developing their application and are freed from deployment-oriented tasks, such as provisioning servers, setting up load balancing, or managing scaling.  

[Show less](https://aws.amazon.com/elasticbeanstalk/faqs//#)

[Q: How is AWS Elastic Beanstalk different from existing application containers or platform-as-a-service solutions? >>](https://aws.amazon.com/elasticbeanstalk/faqs//#)

**Q: How is AWS Elastic Beanstalk different from existing application containers or platform-as-a-service solutions?**

Most existing application containers or platform-as-a-service solutions, while reducing the amount of programming required, significantly diminish developers’ flexibility and control. Developers are forced to live with all the decisions predetermined by the vendor–with little to no opportunity to take back control over various parts of their application’s infrastructure. However, with AWS Elastic Beanstalk, developers retain full control over the AWS resources powering their application. If developers decide they want to manage some (or all) of the elements of their infrastructure, they can do so seamlessly by using Elastic Beanstalk’s management capabilities.  

[Show less](https://aws.amazon.com/elasticbeanstalk/faqs//#)

[Q: What elements of my application can I control when using AWS Elastic Beanstalk? >>](https://aws.amazon.com/elasticbeanstalk/faqs//#)

**Q: What elements of my application can I control when using AWS Elastic Beanstalk?**

With AWS Elastic Beanstalk, you can:

Select the operating system that matches your application requirements (e.g., Amazon Linux or Windows Server 2016)

Choose from several Amazon EC2 instances including On-Demand, Reserved instances, and Spot instances 

Choose from several available database and storage options

Enable login access to Amazon EC2 instances for immediate and direct troubleshooting

Quickly improve application reliability by running in more than one Availability Zone

Enhance application security by enabling HTTPS protocol on the load balancer

Access built-in Amazon CloudWatch monitoring and getting notifications on application health and other important events

Adjust application server settings (e.g., JVM settings) and pass environment variables

Run other application components, such as a memory caching service, side-by-side in Amazon EC2

Access log files without logging in to the application servers  

[Show less](https://aws.amazon.com/elasticbeanstalk/faqs//#)

[Q: What are the Cloud resources powering my AWS Elastic Beanstalk application? >>](https://aws.amazon.com/elasticbeanstalk/faqs//#)

**Q: What are the Cloud resources powering my AWS Elastic Beanstalk application?**

AWS Elastic Beanstalk uses proven AWS features and services, such as Amazon EC2, Amazon RDS, Elastic Load Balancing, Auto Scaling, Amazon S3, and Amazon SNS, to create an environment that runs your application. The current version of AWS Elastic Beanstalk uses the Amazon Linux AMI or the Windows Server 2019.  

[Show less](https://aws.amazon.com/elasticbeanstalk/faqs//#)

[Q: What kinds of applications are supported by AWS Elastic Beanstalk? >>](https://aws.amazon.com/elasticbeanstalk/faqs//#)

**Q: What kinds of applications are supported by AWS Elastic Beanstalk?**

AWS Elastic Beanstalk supports Java, .NET, PHP, Node.js, Python, Ruby, Go, and Docker, and is ideal for web applications. However, due to Elastic Beanstalk’s open architecture, non-web applications can also be deployed using Elastic Beanstalk. We expect to support additional application types and programming languages in the future. See [Supported Platforms](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/concepts.platforms.html) to learn more.  

[Show less](https://aws.amazon.com/elasticbeanstalk/faqs//#)

[Q: Which operating systems does AWS Elastic Beanstalk use? >>](https://aws.amazon.com/elasticbeanstalk/faqs//#)

**Q: Which operating systems does AWS Elastic Beanstalk use?**

AWS Elastic Beanstalk runs on the Amazon Linux AMI and the Windows Server AMI. Both AMIs are supported and maintained by Amazon Web Services and are designed to provide a stable, secure, and high-performance execution environment for Amazon EC2 Cloud computing.  

[Show less](https://aws.amazon.com/elasticbeanstalk/faqs//#)

## Getting Started

[Q: How do I sign up for AWS Elastic Beanstalk? >>](https://aws.amazon.com/elasticbeanstalk/faqs//#)

**Q: How do I sign up for AWS Elastic Beanstalk?**

To sign up for AWS Elastic Beanstalk, choose the Sign Up Now button on the Elastic Beanstalk detail page. You must have an Amazon Web Services account to access this service; if you do not already have one, you will be prompted to create one when you begin the Elastic Beanstalk process. After signing up, please refer to the AWS Elastic Beanstalk Getting Started Guide.  

[Show less](https://aws.amazon.com/elasticbeanstalk/faqs//#)

[Q: Why am I asked to verify my phone number when signing up for AWS Elastic Beanstalk? >>](https://aws.amazon.com/elasticbeanstalk/faqs//#)

**Q: Why am I asked to verify my phone number when signing up for AWS Elastic Beanstalk?**

AWS Elastic Beanstalk registration requires you to have a valid phone number and email address on file with AWS in case we ever need to contact you. Verifying your phone number takes only a few minutes and involves receiving an automated phone call during the registration process and entering a PIN number using the phone key pad.  

[Show less](https://aws.amazon.com/elasticbeanstalk/faqs//#)

[Q: How do I get started after I have signed up? >>](https://aws.amazon.com/elasticbeanstalk/faqs//#)

**Q: How do I get started after I have signed up?**

The best way to get started with AWS Elastic Beanstalk is to work through the AWS Elastic Beanstalk Getting Started Guide, part of our technical documentation. Within a few minutes, you will be able to deploy and use a sample application or upload your own application.  

[Show less](https://aws.amazon.com/elasticbeanstalk/faqs//#)

[Q: Is there a sample application that I can use to check out AWS Elastic Beanstalk? >>](https://aws.amazon.com/elasticbeanstalk/faqs//#)

**Q: Is there a sample application that I can use to check out AWS Elastic Beanstalk?**

Yes. AWS Elastic Beanstalk includes a sample application that you can use to test drive the offering and explore its functionality.  

[Show less](https://aws.amazon.com/elasticbeanstalk/faqs//#)

## Databases and Storage

[Q: Does AWS Elastic Beanstalk store anything in Amazon S3? >>](https://aws.amazon.com/elasticbeanstalk/faqs//#)

**Q: Does AWS Elastic Beanstalk store anything in Amazon S3?**

Yes. AWS Elastic Beanstalk stores your application files and, optionally, server log files in Amazon S3. If you are using the AWS Management Console, the AWS Toolkit for Visual Studio, or AWS Toolkit for Eclipse, an Amazon S3 bucket will be created in your account for you and the files you upload will be automatically copied from your local client to Amazon S3. Optionally, you may configure Elastic Beanstalk to copy your server log files every hour to Amazon S3. You do this by editing the environment configuration settings.  

[Show less](https://aws.amazon.com/elasticbeanstalk/faqs//#)

[Q: Can I use Amazon S3 to store application data, like images? >>](https://aws.amazon.com/elasticbeanstalk/faqs//#)

**Q: Can I use Amazon S3 to store application data, like images?**

Yes. You can use Amazon S3 for application storage. The easiest way to do this is by including the AWS SDK as part of your application’s deployable file. For example, you can include the AWS SDK for Java as part of your application's WAR file.  

[Show less](https://aws.amazon.com/elasticbeanstalk/faqs//#)

[Q: What database solutions can I use with AWS Elastic Beanstalk? >>](https://aws.amazon.com/elasticbeanstalk/faqs//#)

**Q: What database solutions can I use with AWS Elastic Beanstalk?**

AWS Elastic Beanstalk does not restrict you to any specific data persistence technology. You can choose to use Amazon Relational Database Service (Amazon RDS) or Amazon DynamoDB, or use Microsoft SQL Server, Oracle, or other relational databases running on Amazon EC2.  

[Show less](https://aws.amazon.com/elasticbeanstalk/faqs//#)

[Q: How do I set up a database for use with AWS Elastic Beanstalk? >>](https://aws.amazon.com/elasticbeanstalk/faqs//#)

**Q: How do I set up a database for use with AWS Elastic Beanstalk?**

Elastic Beanstalk can automatically provision an Amazon RDS DB instance. The information about connectivity to the DB instance is exposed to your application by environment variables. To learn more about how to configure RDS DB instances for your environment, see the Elastic Beanstalk Developer Guide.

  

[Show less](https://aws.amazon.com/elasticbeanstalk/faqs//#)

[Q: Does this mean I need to modify the application code when moving from test to production? >>](https://aws.amazon.com/elasticbeanstalk/faqs//#)

**Q: Does this mean I need to modify the application code when moving from test to production?**

Not with AWS Elastic Beanstalk. With Elastic Beanstalk, you can specify the connection information in the environment configuration. By extracting the connection string from the application code, you can easily configure different Elastic Beanstalk environments to use different databases.  

[Show less](https://aws.amazon.com/elasticbeanstalk/faqs//#)

## Security

[Q: How do I make my application private? >>](https://aws.amazon.com/elasticbeanstalk/faqs//#)

**Q: How do I make my application private?**

By default, your application is available publicly at myapp.elasticbeanstalk.com for anyone to access. You can use Amazon VPC to provision a private, isolated section of your application in a virtual network that you define. This virtual network can be made private through specific security group rules, network ACLs, and custom route tables. You can also easily control what other incoming traffic, such as SSH, is delivered or not to your application servers by changing the EC2 security group settings.  

[Show less](https://aws.amazon.com/elasticbeanstalk/faqs//#)

[Q: Can I run my application inside a Virtual Private Cloud (VPC)? >>](https://aws.amazon.com/elasticbeanstalk/faqs//#)

**Q: Can I run my application inside a Virtual Private Cloud (VPC)?**

Yes, you can run your applications in a VPC. For more details, see the AWS Elastic Beanstalk Developer Guide.  

[Show less](https://aws.amazon.com/elasticbeanstalk/faqs//#)

[Q: Where can I find more information about security and running applications on AWS? >>](https://aws.amazon.com/elasticbeanstalk/faqs//#)

**Q: Where can I find more information about security and running applications on AWS?**

For more information about security on AWS, please refer to our Amazon Web Services: Overview of Security Processes document and visit our Security Center.  

[Show less](https://aws.amazon.com/elasticbeanstalk/faqs//#)

[Q: Is it possible to use Identity & Access Management (IAM) with AWS Elastic Beanstalk? >>](https://aws.amazon.com/elasticbeanstalk/faqs//#)

**Q: Is it possible to use Identity & Access Management (IAM) with AWS Elastic Beanstalk?**

Yes. IAM users with the appropriate permissions can now interact with AWS Elastic Beanstalk.  

[Show less](https://aws.amazon.com/elasticbeanstalk/faqs//#)

[Q: Why should I use IAM with AWS Elastic Beanstalk? >>](https://aws.amazon.com/elasticbeanstalk/faqs//#)

**Q: Why should I use IAM with AWS Elastic Beanstalk?**

IAM allows you to manage users and groups in a centralized manner. You can control which IAM users have access to AWS Elastic Beanstalk, and limit permissions to read-only access to Elastic Beanstalk for operators who should not be able to perform actions against Elastic Beanstalk resources. All user activity within your account will be aggregated under a single AWS bill.  

[Show less](https://aws.amazon.com/elasticbeanstalk/faqs//#)

[Q: How do I create IAM users? >>](https://aws.amazon.com/elasticbeanstalk/faqs//#)

**Q: How do I create IAM users?**

You can use the IAM console, IAM command line interface (CLI), or IAM API to provision IAM users. By default, IAM users have no access to AWS services until permissions are granted.  

[Show less](https://aws.amazon.com/elasticbeanstalk/faqs//#)

[Q: How do I grant an IAM user access to AWS Elastic Beanstalk? >>](https://aws.amazon.com/elasticbeanstalk/faqs//#)

**Q: How do I grant an IAM user access to AWS Elastic Beanstalk?**

You can grant IAM users access to services by using policies. To simplify the process of granting access to AWS Elastic Beanstalk, you can use one of the policy templates in the IAM console to help you get started. Elastic Beanstalk offers two templates: a read-only access template and a full-access template. The read-only template grants read access to Elastic Beanstalk resources. The full-access template grants full access to all Elastic Beanstalk operations, as well as permissions to manage dependent resources, such as Elastic Load Balancing, Auto Scaling, and Amazon S3. You can also use the AWS Policy Generator to create custom policies. For more details, see the AWS Elastic Beanstalk Developer Guide.  

[Show less](https://aws.amazon.com/elasticbeanstalk/faqs//#)

[Q: Can I restrict access to specific AWS Elastic Beanstalk resources? >>](https://aws.amazon.com/elasticbeanstalk/faqs//#)

**Q: Can I restrict access to specific AWS Elastic Beanstalk resources?**

Yes. You can allow or deny permissions to specific AWS Elastic Beanstalk resources, such as applications, application versions, and environments.  

[Show less](https://aws.amazon.com/elasticbeanstalk/faqs//#)

[Q: Who gets billed for the AWS resources that an IAM user creates? >>](https://aws.amazon.com/elasticbeanstalk/faqs//#)

**Q: Who gets billed for the AWS resources that an IAM user creates?**

All resources created by IAM users under a root account are owned and billed to the root account.  

[Show less](https://aws.amazon.com/elasticbeanstalk/faqs//#)

[Q: Who has access to an AWS Elastic Beanstalk environment launched by an IAM user? >>](https://aws.amazon.com/elasticbeanstalk/faqs//#)

**Q: Who has access to an AWS Elastic Beanstalk environment launched by an IAM user?**

The root account has full access to all AWS Elastic Beanstalk environments launched by any IAM user under that account. If you use the Elastic Beanstalk template to grant read-only access to an IAM user, that user will be able to view all applications, application versions, environments, and any associated resources in that account. If you use the Elastic Beanstalk template to grant full access to an IAM user, that user will be able to create, modify, and terminate any Elastic Beanstalk resources under that account.  

[Show less](https://aws.amazon.com/elasticbeanstalk/faqs//#)

[Q: Can an IAM user access the AWS Elastic Beanstalk console? >>](https://aws.amazon.com/elasticbeanstalk/faqs//#)

**Q: Can an IAM user access the AWS Elastic Beanstalk console?**

Yes. An IAM user can access the AWS Elastic Beanstalk console using their username and password.  

[Show less](https://aws.amazon.com/elasticbeanstalk/faqs//#)

[Q: Can an IAM user call the AWS Elastic Beanstalk API? >>](https://aws.amazon.com/elasticbeanstalk/faqs//#)

**Q: Can an IAM user call the AWS Elastic Beanstalk API?**

Yes. An IAM user can use their access key and secret key to perform operations using the Elastic Beanstalk API.  

[Show less](https://aws.amazon.com/elasticbeanstalk/faqs//#)

[Q: Can an IAM user use the AWS Elastic Beanstalk command line interface? >>](https://aws.amazon.com/elasticbeanstalk/faqs//#)

**Q: Can an IAM user use the AWS Elastic Beanstalk command line interface?**

Yes. An IAM user can use their access key and secret key to perform operations using the AWS Elastic Beanstalk command line interface (CLI).  

[Show less](https://aws.amazon.com/elasticbeanstalk/faqs//#)

## Managed Platform Updates

[Q: How can I keep the underlying platform of the environment running my application automatically up-to-date? >>](https://aws.amazon.com/elasticbeanstalk/faqs//#)

**Q: How can I keep the underlying platform of the environment running my application automatically up-to-date?**

You can opt-in to having your AWS Elastic Beanstalk environments automatically updated to the latest version of the underlying platform running your application during a specified maintenance window. Elastic Beanstalk regularly releases new versions of supported platforms (Java, PHP, Ruby, Node.js, Python, .NET, Go, and Docker) with operating system, web and application server, and language and framework updates.  

[Show less](https://aws.amazon.com/elasticbeanstalk/faqs//#)

[Q: How can I get started with managed platform updates? >>](https://aws.amazon.com/elasticbeanstalk/faqs//#)

**Q: How can I get started with managed platform updates?**

To let Elastic Beanstalk automatically manage your platform updates, you must enable managed platform updates in the Configuration tab of the Elastic Beanstalk console or use the EB CLI or API. After you have enabled the feature, you can configure which types of updates to allow and when updates can occur.  

[Show less](https://aws.amazon.com/elasticbeanstalk/faqs//#)

[Q: What kinds of platform version updates will managed platform updates apply? >>](https://aws.amazon.com/elasticbeanstalk/faqs//#)

**Q: What kinds of platform version updates will managed platform updates apply?**

AWS Elastic Beanstalk can automatically perform platform updates for new patch and minor platform versions. Elastic Beanstalk will not automatically perform major platform version updates (e.g., Java 7 Tomcat 7 to Java 8 Tomcat 8) because they include backwards incompatible changes and require additional testing. In these cases, you must manually initiate the update.  

[Show less](https://aws.amazon.com/elasticbeanstalk/faqs//#)

[Q: How does AWS Elastic Beanstalk distinguish between “major,” “minor,” and “patch” version releases? >>](https://aws.amazon.com/elasticbeanstalk/faqs//#)

**Q: How does AWS Elastic Beanstalk distinguish between “major,” “minor,” and “patch” version releases?**

AWS Elastic Beanstalk platforms are versioned using this pattern: MAJOR.MINOR.PATCH (e.g., 2.0.0). Each portion is incremented as follows:

MAJOR version when there are incompatible changes.

MINOR version when there is additional functionality added in a backward-compatible manner.

PATCH version when there are backward-compatible bug fixes.  

[Show less](https://aws.amazon.com/elasticbeanstalk/faqs//#)

[Q: When and how can I perform major version updates? >>](https://aws.amazon.com/elasticbeanstalk/faqs//#)

**Q: When and how can I perform major version updates?**

You can perform major version updates at any time using the AWS Elastic Beanstalk management console, API, or CLI. You have the following options to perform a major version update:

Apply the update in-place on an existing environment. See Updating Your Elastic Beanstalk Environment's Platform Version.

Create a clone of an existing environment with the new platform version. See Clone an Environment to learn more.  

[Show less](https://aws.amazon.com/elasticbeanstalk/faqs//#)

[Q: How does Elastic Beanstalk apply managed platform updates? >>](https://aws.amazon.com/elasticbeanstalk/faqs//#)

**Q: How does Elastic Beanstalk apply managed platform updates?**

The updates are applied using an immutable deployment mechanism that ensures that no changes are made to the existing environment until a parallel fleet of Amazon EC2 instances, with the updates installed, is ready to be swapped with the existing instances, which are then terminated. In addition, if the Elastic Beanstalk health system detects any issues during the update, traffic is redirected to the existing fleet of instances, ensuring minimal impact to end users of your application.  

[Show less](https://aws.amazon.com/elasticbeanstalk/faqs//#)

[Q: Will my application be available during the maintenance windows? >>](https://aws.amazon.com/elasticbeanstalk/faqs//#)

**Q: Will my application be available during the maintenance windows?**

Since managed platform updates use an immutable deployment mechanism to perform the updates, your application will be available during the maintenance window and consumers of your application will not be impacted by the update.  

[Show less](https://aws.amazon.com/elasticbeanstalk/faqs//#)

[Q: What does it cost to use managed platform updates? >>](https://aws.amazon.com/elasticbeanstalk/faqs//#)

**Q: What does it cost to use managed platform updates?**

There is no additional charge for the managed platform updates feature. You simply pay for the additional EC2 instances necessary to perform the update for the duration of the update.  

[Show less](https://aws.amazon.com/elasticbeanstalk/faqs//#)

[Q: What is a maintenance window? >>](https://aws.amazon.com/elasticbeanstalk/faqs//#)

**Q: What is a maintenance window?**

A maintenance window is a weekly two-hour-long time slot during which AWS Elastic Beanstalk will initiate platform updates if managed platform updates is enabled and a new version of the platform is available. For example, if you select a maintenance window that begins every Sunday at 2 AM, AWS Elastic Beanstalk will initiate the platform update sometime between 2-4 AM every Sunday. It is important to note that, depending on the configuration of your applications, updates could complete outside of the maintenance window.

The maintenance window is set on a per-environment basis, providing you the option to set different maintenance windows for your various application components or applications. This allows environment updates to be staggered if you do not want multiple pieces of your application to be updated at the same time. If you enable managed platform updates but do not specify a maintenance window, a default weekly 2-hour window will be assigned for your environment. If you want to change when maintenance is performed on your behalf, you can do so by modifying the managed update configuration in the AWS Management Console or by using the UpdateEnvironment API.  

[Show less](https://aws.amazon.com/elasticbeanstalk/faqs//#)

[Q: How will I be notified of the availability of new platform versions? >>](https://aws.amazon.com/elasticbeanstalk/faqs//#)

**Q: How will I be notified of the availability of new platform versions?**

You will be notified about the availability of new platform versions through the AWS Management Console, forum announcements, and release notes.  

[Show less](https://aws.amazon.com/elasticbeanstalk/faqs//#)

[Q: Where can I find details of changes between platform versions? >>](https://aws.amazon.com/elasticbeanstalk/faqs//#)

**Q: Where can I find details of changes between platform versions?**

Details on changes between platform versions can be found on the AWS Elastic Beanstalk Release Notes page.  

[Show less](https://aws.amazon.com/elasticbeanstalk/faqs//#)

[Q: What operations can I perform on the environment while a managed update is in progress? >>](https://aws.amazon.com/elasticbeanstalk/faqs//#)

**Q: What operations can I perform on the environment while a managed update is in progress?**

The only action available to you while a managed platform update is in-progress is ‘abort’. This will allow you to stop the update immediately and roll back to the previous version.  

[Show less](https://aws.amazon.com/elasticbeanstalk/faqs//#)

[Q: Which platform version will my environment be updated to if there are multiple new versions released in between maintenance windows? >>](https://aws.amazon.com/elasticbeanstalk/faqs//#)

**Q: Which platform version will my environment be updated to if there are multiple new versions released in between maintenance windows?**

Your environment will always be updated to the latest version available based on the level (minor plus patch or patch only) you have selected.  

[Show less](https://aws.amazon.com/elasticbeanstalk/faqs//#)

[Q: Where can I find details of all the managed platform updates that have been performed on my environment? >>](https://aws.amazon.com/elasticbeanstalk/faqs//#)

**Q: Where can I find details of all the managed platform updates that have been performed on my environment?**

Details for every managed platform update are available on the events page and are tagged with an event type of “MAINTENANCE.”  

[Show less](https://aws.amazon.com/elasticbeanstalk/faqs//#)

[Q: How often are platform version updates released? >>](https://aws.amazon.com/elasticbeanstalk/faqs//#)

**Q: How often are platform version updates released?**

The number of version releases in a given year varies based on the frequency and content of releases and patches from the language/framework’s vendor or core team, and the outcome of a thorough vetting of these releases and patches by our platform engineering team.  

[Show less](https://aws.amazon.com/elasticbeanstalk/faqs//#)

## AWS Graviton Support

[Q: How do I deploy a new workload with the Graviton processor from the Elastic Beanstalk console? >>](https://aws.amazon.com/elasticbeanstalk/faqs//#)

**Q: How do I deploy a new workload with the Graviton processor from the Elastic Beanstalk console?**  

To deploy your application with arm64-based processors on the Elastic Beanstalk console, you can select processor architecture and instance type from capacity tab in Configure more options settings.  

[Show less](https://aws.amazon.com/elasticbeanstalk/faqs//#)

[Q: How do I deploy a new workload with the Graviton processor from the AWS CLI, Elastic Beanstalk CLI, or infrastructure as code services? >>](https://aws.amazon.com/elasticbeanstalk/faqs//#)

**Q: How do I deploy a new workload with the Graviton processor from the AWS CLI, Elastic Beanstalk CLI, or infrastructure as code services?**  

To deploy your application using the Elastic Beanstalk CLI, AWS CLI, CFN, or AWS CDK, refer to [Elastic Beanstalk Developer Guide.](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/using-features.managing.ec2.html)  

[Show less](https://aws.amazon.com/elasticbeanstalk/faqs//#)

[Q: Do I need to recompile my workload before migrating to Graviton? >>](https://aws.amazon.com/elasticbeanstalk/faqs//#)

**Q: Do I need to recompile my workload before migrating to Graviton?**  

If your workload is on an interpreted programming language such as Node.js, Python, Tomcat, PHP, or Ruby, you do not need to recompile your workload to use Graviton. If you are using Go or .Net Core for your workload, you need to update the build command for the arm64 instance type. You also need to recompile binary dependencies or use an arm64 compatible release of binary dependencies. If you are using Docker, your Docker image must be multi-architecture and support deploying to both x86 and arm64.  

[Show less](https://aws.amazon.com/elasticbeanstalk/faqs//#)

[Q: Which platform branches are supported by Graviton on Elastic Beanstalk? >>](https://aws.amazon.com/elasticbeanstalk/faqs//#)

**Q: Which platform branches are supported by Graviton on Elastic Beanstalk?**  

Elastic Beanstalk supports Graviton on 64bit Amazon Linux 2 for a variety of platform and branches. See the [documentation](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/Welcome.html) for a full list.  

[Show less](https://aws.amazon.com/elasticbeanstalk/faqs//#)

[Q: What are the use cases where I can use the Graviton processor? >>](https://aws.amazon.com/elasticbeanstalk/faqs//#)

**Q: What are the use cases where I can use the Graviton processor?**  

You can easily transition your workload to Graviton and take advantage of performance and cost benefits in the following use cases: Linux-based workloads built primarily on open-source technologies; containerized and microservices-based applications such as Docker and MC Docker; applications written in portable programming languages such as Java, Python, .NET Core, node.js, and PHP; Compiled C/C++, Rust, or Go applications; .NET Core (v3.1+) workloads running on Linux; multi-threaded workloads;non-uniform memory access (NUMA) sensitive workloads; and arm64-native software development and testing.  

[Show less](https://aws.amazon.com/elasticbeanstalk/faqs//#)

## Billing

[Q: How much does AWS Elastic Beanstalk cost? >>](https://aws.amazon.com/elasticbeanstalk/faqs//#)

**Q: How much does AWS Elastic Beanstalk cost?**

There is no additional charge for AWS Elastic Beanstalk–you pay only for the AWS resources actually used to store and run your application.  

[Show less](https://aws.amazon.com/elasticbeanstalk/faqs//#)

[Q: How much do the AWS resources powering my application on AWS Elastic Beanstalk cost? >>](https://aws.amazon.com/elasticbeanstalk/faqs//#)

**Q: How much do the AWS resources powering my application on AWS Elastic Beanstalk cost?**

You pay only for what you use, and there is no minimum fee for the use of any AWS resources. For Amazon EC2 pricing information, please visit the pricing section on the EC2 detail page. For Amazon S3 pricing information, please visit the pricing section on the S3 detail page. You can use the AWS simple calculator to estimate your bill for different application sizes.  

[Show less](https://aws.amazon.com/elasticbeanstalk/faqs//#)

[Q: How do I check how many AWS resources have been used by my application and access my bill? >>](https://aws.amazon.com/elasticbeanstalk/faqs//#)

**Q: How do I check how many AWS resources have been used by my application and access my bill?**

You can view your charges for the current billing period at any time on the Amazon Web Services web site by logging into your Amazon Web Services account and choosing Account Activity under Your Web Services Account.  

[Show less](https://aws.amazon.com/elasticbeanstalk/faqs//#)

## Support

[Q: Does AWS Support cover AWS Elastic Beanstalk? >>](https://aws.amazon.com/elasticbeanstalk/faqs//#)

**Q: Does AWS Support cover AWS Elastic Beanstalk?**

Yes. AWS Support covers issues related to your use of AWS Elastic Beanstalk. For further details and pricing, see the AWS Support page.  

[Show less](https://aws.amazon.com/elasticbeanstalk/faqs//#)

[Q: What other support options are available? >>](https://aws.amazon.com/elasticbeanstalk/faqs//#)

**Q: What other support options are available?**

You can tap into the breadth of existing AWS community knowledge to help you with your development through the AWS Elastic Beanstalk discussion forum.