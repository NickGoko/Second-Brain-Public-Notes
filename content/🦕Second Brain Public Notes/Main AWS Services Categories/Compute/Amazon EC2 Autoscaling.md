---
tags:
  - cloud/aws
---
AWS Auto Scaling monitors your applications and automatically adjusts capacity to maintain steady, predictable performance at the lowest possible cost.

AWS Auto Scaling refers to a collection of Auto Scaling capabilities across several AWS services.

The services within the AWS Auto Scaling family include:

- Amazon EC2 (known as Amazon EC2 Auto Scaling).
- Amazon ECS.
- Amazon DynamoDB.
- Amazon Aurora.

This page is specifically for Amazon EC2 Auto Scaling – Auto Scaling will also be discussed for the other services on their respective pages.

## Amazon EC2 Auto Scaling Features

Amazon EC2 Auto Scaling helps you ensure that you have the correct number of Amazon EC2 instances available to handle the load for your application.

You create collections of EC2 instances, called Auto Scaling groups.

Automatically provides horizontal scaling (scale-out) for your instances.

Triggered by an event of scaling action to either launch or terminate instances.

Availability, cost, and system metrics can all factor into scaling.

Auto Scaling is a region-specific service.

Auto Scaling can span multiple AZs within the same AWS region.

Auto Scaling can be configured from the Console, CLI, SDKs and APIs.

There is no additional cost for Auto Scaling, you just pay for the resources (EC2 instances) provisioned.

Auto Scaling works with ELB, CloudWatch and CloudTrail.

You can determine which subnets Auto Scaling will launch new instances into.

Auto Scaling will try to distribute EC2 instances evenly across AZs.

Launch configuration is the template used to create new EC2 instances and includes parameters such as instance family, instance type, AMI, key pair, and security groups.

You cannot edit a launch configuration once defined.

A launch configuration:

- Can be created from the AWS console or CLI.
- You can create a new launch configuration, or.
- You can use an existing running EC2 instance to create the launch configuration.
    - The AMI must exist on EC2.
    - EC2 instance tags and any additional block store volumes created after the instance launch will not be considered.
- If you want to change your launch configurations you have to create a new one, make the required changes, and use that with your auto scaling groups.

You can use a launch configuration with multiple Auto Scaling Groups (ASG).

Launch templates are similar to launch configurations and offer more options (more below).

An Auto Scaling Group (ASG) is a logical grouping of EC2 instances managed by an Auto Scaling Policy.

An ASG can be edited once defined.

You can attach one or more classic ELBs to your existing ASG.

You can attach one or more Target Groups to your ASG to include instances behind an ALB.

The ELBs must be in the same region.

Once you do this any EC2 instance existing or added by the ASG will be automatically registered with the ASG defined ELBs.

If adding an instance to an ASG would result in exceeding the maximum capacity of the ASG the request will fail.

You can add a running instance to an ASG if the following conditions are met:

- The instance is in a running state.
- The AMI used to launch the instance still exists.
- The instance is not part of another ASG.
- The instance is in the same AZs for the ASG.

## Scaling Options

The scaling options define the triggers and when instances should be provisioned/de-provisioned.

There are four scaling options:

- Maintain – keep a specific or minimum number of instances running.
- Manual – use maximum, minimum, or a specific number of instances.
- Scheduled – increase or decrease the number of instances based on a schedule.
- Dynamic – scale based on real-time system metrics (e.g. CloudWatch metrics).
- Predictive – machine learning to schedule the right number of EC2 instances in anticipation of approaching traffic changes.

The following table describes the scaling options available and when to use them:

|   |   |   |
|---|---|---|
|**Scaling**|**Description**|**When to use**|
|Maintain|Ensures the required number of instances are running|Use when you always need a known number of instances running at all times|
|Manual|Manually change desired capacity|Use when your needs change rarely enough that you’re ok the make manual changes|
|Scheduled|Adjust min/max on specific dates/times or recurring time periods|Use when you know when your busy and quiet times are. Useful for ensuring enough instances are available before very busy times|
|Dynamic|Scale in response to system load or other triggers using metrics|Useful for changing capacity based on system utilization, e.g. CPU hits 80%.|
|Predictive|predict capacity required ahead of time using ML|Useful for when capacity, and number of instances is unknown.|

### Scheduled Scaling

Scaling based on a schedule allows you to scale your application ahead of predictable load changes.

For example, you may know that traffic to your application is highest between 9am and 12pm Monday-Friday.

### Dynamic Scaling

Amazon EC2 Auto Scaling enables you to follow the demand curve for your applications closely, reducing the need to manually provision Amazon EC2 capacity in advance.

For example, you can track the CPU utilization of your EC2 instances or the “Request Count Per Target” to track the number of requests coming through an Application Load Balancer.

Amazon EC2 Auto Scaling will then automatically adjust the number of EC2 instances as needed to maintain your target.

### Predictive Scaling

Predictive Scaling uses machine learning to schedule the optimum number of EC2 instances in anticipation of upcoming traffic changes.

Predictive Scaling predicts future traffic, including regularly occurring spikes, and provisions the right number of EC2 instances in advance.

Predictive Scaling uses machine learning algorithms to detect changes in daily and weekly patterns and then automatically adjust forecasts.

You can configure the scaling options through Scaling Policies which determine when, if, and how the ASG scales out and in.

The following table describes the scaling policy types available for dynamic scaling policies and when to use them (more detail further down the page):

|   |   |   |
|---|---|---|
|**Scaling Policy**|**What it is**|**When to use**|
|Target Tracking Policy|Adds or removes capacity as required to keep the metric at or close to the specific target value.|You want to keep the CPU usage of your ASG at 70%|
|Simple Scaling Policy|Waits for the health check and cool down periods to expire before re-evaluating|Useful when load is erratic. AWS recommends step scaling instead of simple in most cases.|
|Step Scaling Policy|Increases or decreases the configured capacity of the Auto Scaling group based on a set of scaling adjustments, known as step adjustments.|You want to vary adjustments based on the size of the alarm breach|

The diagram below depicts an Auto Scaling group with a Scaling policy set to a minimum size of 1 instance, a desired capacity of 2 instances, and a maximum size of 4 instances:

![Auto Scaling Group Policy](https://digitalcloud.training/wp-content/uploads/2022/01/auto-scaling-group-policy.jpeg)

### Scaling Based on Amazon SQS

Can also scale based on an Amazon Simple Queue Service (SQS) queue.

This comes up as an exam question for SAA-C02.

Uses a custom metric that’s sent to Amazon CloudWatch that measures the number of messages in the queue per EC2 instance in the Auto Scaling group.

A target tracking policy configures your Auto Scaling group to scale based on the custom metric and a set target value. CloudWatch alarms invoke the scaling policy.

A custom “backlog per instance” metric is used to track the number of messages in the queue and also the number available for retrieval.

Can base the adjustments off the SQS Metric “ApproximateNumberOfMessages”.

## Launch Templates Vs Launch Configurations

Launch templates are like [launch configuration](https://docs.aws.amazon.com/autoscaling/ec2/userguide/LaunchConfiguration.html)s in that they specify the instance configuration information.

Information includes the ID of the Amazon Machine Image (AMI), the instance type, a key pair, security groups, and the other parameters that you use to launch EC2 instances.

Launch templates include additional features such as supporting multiple versions of a template.

With versioning, you can create a subset of the full set of parameters and then reuse it to create other templates or template versions.

## EC2 Auto Scaling Lifecycle Hooks

Lifecycle pause EC2 instances as an Auto Scaling group launches or terminates them so you can perform custom actions.

Paused instances remain in a wait state either until you complete the lifecycle action using the complete-lifecycle-action command or the CompleteLifecycleAction operation, or until the timeout period ends (one hour by default).

Lifecycle hooks provide greater control over how instances launch and terminate.

You can send notifications when an instance enters a wait state using Amazon EventBridge, Amazon SNS, or Amazon SQS to receive the notifications.

## High Availability

Amazon EC2 Auto Scaling offers high availability (HA) when instances are launched into at least two Availability Zones.

You can use an Amazon Elastic Load Balancer or Amazon Route 53 to direct incoming connections to your EC2 instances.

EC2 Auto Scaling cannot provide HA across multiple AWS Regions as it is a regional service.

## Monitoring and Reporting

When Auto Scaling group metrics are enabled the Auto Scaling group sends sampled data to [CloudWatch](https://digitalcloud.training/amazon-cloudwatch/) every minute (no charge).

You can enable and disable Auto Scaling group metrics using the AWS Management Console, AWS CLI, or AWS SDKs.

The AWS/AutoScaling namespace includes the following metrics which are sent to CloudWatch every 1 minute:

- GroupMinSize
- GroupMaxSize
- GroupDesiredCapacity
- GroupInServiceInstances
- GroupPendingInstances
- GroupStandbyInstances
- GroupTerminatingInstances
- GroupTotalInstances

Metrics are also sent from the Amazon EC2 instances to Amazon CloudWatch:

- Basic monitoring sends EC2 metrics to CloudWatch about ASG instances every 5 minutes.
- Detailed monitoring can be enabled and sends metrics every 1 minute (chargeable).
- If the launch configuration is created from the console basic monitoring of EC2 instances is enabled by default.
- If the launch configuration is created from the CLI detailed monitoring of EC2 instances is enabled by default.

EC2 Auto Scaling uses health checks to check if instances are healthy and available.

- By default Auto Scaling uses EC2 status checks.
- Auto Scaling supports ELB health checks and custom health checks in addition to the EC2 status checks.
- If any of the configured health checks returns an unhealthy status the instance will be terminated.
- With ELB health checks enabled an instance is marked as unhealthy if the ELB reports it as OutOfService.
- A healthy instance enters the InService state.
- If an EC2 instance is marked as unhealthy it will be scheduled for replacement.
- If connection draining is enabled, EC2 Auto Scaling will wait for any in-flight requests to complete or timeout before terminating instances.
- The health check grace period is a period of time in which a new instance is allowed to warm up before health check are performed (300 seconds by default).

**_Note:_** _When using Elastic Load Balancers it is an AWS best practice to enable the ELB health checks. If you don’t, EC2 status checks may show an instance as being healthy that the ELB has determined is unhealthy. In this case the instance will be removed from service by the ELB but will not be terminated by Auto Scaling._

## Logging and Auditing

[AWS CloudTrail](https://docs.aws.amazon.com/autoscaling/plans/APIReference/logging-using-cloudtrail.html) captures all API calls for AWS Auto Scaling as events.

The API calls that are captured include calls from the Amazon EC2 Auto Scaling console and code calls to the AWS Auto Scaling API.

If you create a trail, you can enable continuous delivery of CloudTrail events to an Amazon S3 bucket, including events for AWS Auto Scaling.

If you don’t configure a trail, you can still view the most recent (up to 90 days) events in the CloudTrail console in the **Event history**.

CloudTrail events include the calls made to AWS Auto Scaling, the IP address from which the requests were made, who made the requests, when they were made, and additional details.

## Authorization and Access Control

EC2 Auto Scaling support [identity-based IAM policies](https://docs.aws.amazon.com/autoscaling/ec2/userguide/control-access-using-iam.html).

Amazon EC2 Auto Scaling does not support resource-based policies.

Amazon EC2 Auto Scaling uses [service-linked roles](https://docs.aws.amazon.com/autoscaling/ec2/userguide/autoscaling-service-linked-role.html) for the permissions that it requires to call other AWS services on your behalf.

A service-linked role is a unique type of IAM role that is linked directly to an AWS service.

There is a default service-linked role for your account, named **AWSServiceRoleForAutoScaling**.

This role is automatically assigned to your Auto Scaling groups unless you specify a different service-linked role.

Amazon EC2 Auto Scaling also does not support Access Control Lists (ACLs).

You can apply tag-based, resource-level permissions in the identity-based policies that you create for Amazon EC2 Auto Scaling.

This offers better control over which resources a user can create, modify, use, or delete.

## ASG Behavior and Configuration

EC2 Auto Scaling – Termination Policy:

- Termination policies control the instances which are terminated first when a scale-in event occurs.
- There is a default termination policy configured and you can create your own customized termination policies.
- The default termination policy helps to ensure that EC2 instances span Availability Zones evenly for high availability.
- The default policy is fairly generic and flexible to cover a range of scenarios.

You can enable Instance Protection which prevents Auto Scaling from scaling in and terminating the EC2 instances.

If Auto Scaling fails to launch instances in a specific AZ it will try other AZs until successful.

The default health check grace period is 300 seconds.

“Scaling out” is the process in which EC2 instances are launched by the scaling policy.

“Scaling in” is the process in which EC2 instances are terminated by the scaling policy.

It is recommended to create a scale-in event for every configured scale-out event.

An imbalance may occur due to:

- Manually removing AZs/subnets from the configuration.
- Manually terminating EC2 instances.
- EC2 capacity issues.
- Spot price is reached.

All Elastic IPs and EBS volumes are detached from terminated EC2 instances and will need to be manually reattached.

Using custom health checks a CLI command can be issued to set the instance’s status to unhealthy, e.g.:

**_aws autoscaling set–instance-health –instance-id i-123abc45d –health-status Unhealthy_**

Once an EC2 instance enters the terminating state it cannot be put back into service again.

However, there is a short period of time in which an AWS CLI command can be run to change an instance to healthy.

Termination of unhealthy instances happens first, then Auto Scaling attempts to launch new instances to replace terminated instances. This is different to AZ rebalancing.

You can use the AWS Console or AWS CLI to manually remove (detach) instances from an ASG.

When detaching an EC2 instance you can optionally decrement the ASG’s desired capacity (to prevent it from launching another instance).

An instance can only be attached to one Auto Scaling group at a time.

You can suspend and then resume one or more of the scaling processes for your ASG at any time.

This can be useful when if want to investigate an issue with an application and make changes without invoking the scaling processes.

You can manually move an instance from an ASG and put it in the standby state.

Instances in the standby state are still managed by Auto Scaling, are charged as normal, and do not count towards available EC2 instance for workload/application use.

Auto scaling does not perform any health checks on EC2 instances in the standby state.

Standby state can be used for performing updates/changes/troubleshooting etc. without health checks being performed or replacement instances being launched.

When you delete an Auto Scaling group all EC2 instances will be terminated.

You can select to use Spot instances in launch configurations.

The ASG treats spot instances the same as on-demand instances.

You can mix Spot instances with on-demand (when using launch templates).

The ASG can be configured to send an Amazon SNS notification when:

- An instance is launched.
- An instance is terminated.
- An instance fails to launch.
- An instance fails to terminate.

Merging ASGs.

- Can merge multiple single AZ Auto Scaling Groups into a single multi-AZ ASG.
- Merging can only be performed by using the CLI.
- The process is to rezone one of the groups to cover/span the other AZs for the other ASGs and then delete the other ASGs.
- This can be performed on ASGs with or without ELBs attached to them.

Cooldown Period:

- The cooldown period is a setting you can configure for your Auto Scaling group that helps to ensure that it doesn’t launch or terminate additional instances before the previous scaling activity takes effect.
- A default cooldown period of 300 seconds is applied when you create your Auto Scaling group.
- You can configure the cooldown period when you create the Auto Scaling group.
- You can override the default cooldown via scaling-specific cooldown.

The warm-up period is the period in which a newly launched EC2 instance in an ASG that uses step scaling is not considered toward the ASG metrics.

![[Module 9 - Implementing Elasticity, High Availability, and Monitoring#Scaling]]


# FAQs
## General

**Q: What is Amazon EC2 Auto Scaling?**

Amazon EC2 Auto Scaling is a fully managed service designed to launch or terminate Amazon EC2 instances automatically to help ensure you have the correct number of Amazon EC2 instances available to handle the load for your application. Amazon EC2 Auto Scaling helps you maintain application availability through fleet management for EC2 instances, which detects and replaces unhealthy instances, and by scaling your Amazon EC2 capacity up or down automatically according to conditions you define. You can use Amazon EC2 Auto Scaling to automatically increase the number of Amazon EC2 instances during demand spikes to maintain performance and decrease capacity during lulls to reduce costs.  

**Q. When should I use Amazon EC2 Auto Scaling vs. AWS Auto Scaling?**

You should use AWS Auto Scaling to manage scaling for multiple resources across multiple services. AWS Auto Scaling lets you define dynamic scaling policies for multiple EC2 Auto Scaling groups or other resources using predefined scaling strategies. Using AWS Auto Scaling to configure scaling policies for all of the scalable resources in your application is faster than managing scaling policies for each resource via its individual service console. It’s also easier, as AWS Auto Scaling includes predefined scaling strategies that simplify the setup of scaling policies. 

You should use EC2 Auto Scaling if you only need to scale Amazon EC2 Auto Scaling groups, or if you are only interested in maintaining the health of your EC2 fleet. You should also use EC2 Auto Scaling if you need to create or configure Amazon EC2 Auto Scaling groups, or if you need to set up scheduled or step scaling policies (as AWS Auto Scaling supports only target tracking scaling policies).

EC2 Auto Scaling groups must be created and configured outside of AWS Auto Scaling, such as through the EC2 console, Auto Scaling API or via CloudFormation. AWS Auto Scaling can help you configure dynamic scaling policies for your existing EC2 Auto Scaling groups.  

**Q: How is Predictive Scaling Policy different from Predictive Scaling of AWS Auto Scaling plan?**

Predictive Scaling Policy brings the similar prediction algorithm offered through AWS Auto Scaling plan as a native scaling policy in EC2 Auto Scaling. You can use predictive scaling directly through AWS Command Line Interface (CLI), EC2 Auto Scaling Management Console, and AWS SDKs similar to how you use other scaling policies, such as Simple Scaling or Target Tracking etc.  You don’t have to create an AWS Auto Scaling plan just for using predictive scaling.    

**Q: What are the benefits of using Amazon EC2 Auto Scaling?**

Amazon EC2 Auto Scaling helps to maintain your Amazon EC2 instance availability. Whether you are running one Amazon EC2 instance or thousands, you can use Amazon EC2 Auto Scaling to detect impaired Amazon EC2 instances, and replace the instances without intervention. This ensures that your application has the compute capacity that you expect. You can use Amazon EC2 Auto Scaling to automatically scale your Amazon EC2 fleet by following the demand curve for your applications, reducing the need to manually provision Amazon EC2 capacity in advance. For example, you can set a condition to add new Amazon EC2 instances in increments to the ASG when the average utilization of your Amazon EC2 fleet is high; and similarly, you can set a condition to remove instances in increments when CPU utilization is low. You can also use Amazon CloudWatch to send alarms to trigger scaling activities and Elastic Load Balancing (ELB) to distribute traffic to your instances within the ASG. If you have predictable load changes, you can use Predictive Scaling policy to proactively increase capacity ahead of upcoming demand. Amazon EC2 Auto Scaling enables you to run your Amazon EC2 fleet at optimal utilization.  

**Q: What is fleet management and how is it different from dynamic scaling?**

If your application runs on Amazon EC2 instances, then you have what’s referred to as a ‘fleet’. _Fleet management_ refers to the functionality that automatically replaces unhealthy instances and maintains your fleet at the desired capacity. Amazon EC2 Auto Scaling fleet management ensures that your application is able to receive traffic and that the instances themselves are working properly. When Auto Scaling detects a failed [health check](http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/monitoring-system-instance-status-check.html), it can replace the instance automatically.

The _dynamic scaling_ capabilities of Amazon EC2 Auto Scaling refers to the functionality that automatically increases or decreases capacity based on load or other metrics. For example, if your CPU spikes above 80% (and you have an alarm setup) Amazon EC2 Auto Scaling can add a new instance dynamically.

**Q: What is target tracking?**

Target tracking is a new type of scaling policy that you can use to set up dynamic scaling for your application in just a few simple steps. With target tracking, you select a load metric for your application, such as CPU utilization or request count, set the target value, and Amazon EC2 Auto Scaling adjusts the number of EC2 instances in your ASG as needed to maintain that target. It acts like a home thermostat, automatically adjusting the system to keep the environment at your desired temperature. For example, you can configure target tracking to keep CPU utilization for your fleet of web servers at 50%. From there, Amazon EC2 Auto Scaling launches or terminates EC2 instances as required to keep the average CPU utilization at 50%.  

**Q: What is an EC2 Auto Scaling group (ASG)?**

An Amazon EC2 Auto Scaling group (ASG) contains a collection of EC2 instances that share similar characteristics and are treated as a logical grouping for the purposes of fleet management and dynamic scaling. For example, if a single application operates across multiple instances, you might want to increase the number of instances in that group to improve the performance of the application, or decrease the number of instances to reduce costs when demand is low. Amazon EC2 Auto Scaling will automatically adjust the number of instances in the group to maintain a fixed number of instances even if a instance becomes unhealthy, or based on criteria that you specify. You can find more information about ASG in the [Amazon EC2 Auto Scaling User Guide](http://docs.aws.amazon.com/autoscaling/latest/userguide/AutoScalingGroup.html).  

**Q: What happens to my Amazon EC2 instances if I delete my ASG?**

If you have an EC2 Auto Scaling group (ASG) with running instances and you choose to delete the ASG, the instances will be terminated and the ASG will be deleted.

**Q: How do I know when EC2 Auto Scaling is launching or terminating the EC2 instances in an EC2 Auto Scaling group?**

When you use Amazon EC2 Auto Scaling to scale your applications automatically, it is useful to know when EC2 Auto Scaling is launching or terminating the EC2 instances in your EC2 Auto Scaling group. [Amazon SNS](https://aws.amazon.com/sns/) coordinates and manages the delivery or sending of notifications to subscribing clients or endpoints. You can configure EC2 Auto Scaling to send an SNS notification whenever your EC2 Auto Scaling group scales. Amazon SNS can deliver notifications as HTTP or HTTPS POST, email (SMTP, either plain-text or in JSON format), or as a message posted to an Amazon SQS queue. For example, if you configure your EC2 Auto Scaling group to use the autoscaling: EC2\_INSTANCE\_TERMINATE notification type, and your EC2 Auto Scaling group terminates an instance, it sends an email notification. This email contains the details of the terminated instance, such as the instance ID and the reason that the instance was terminated.

For more information read [Getting SNS Notifications when your EC2 Auto Scaling Group Scales](http://docs.aws.amazon.com/autoscaling/latest/userguide/ASGettingNotifications.html).

**Q: What is a launch configuration?**

A launch configuration is a template that an EC2 Auto Scaling group uses to launch EC2 instances. When you create a launch configuration, you specify information for the instances such as the ID of the Amazon Machine Image (AMI), the instance type, a key pair, one or more security groups, and a block device mapping. If you've launched an EC2 instance before, you specified the same information in order to launch the instance. When you create an EC2 Auto Scaling group, you must specify a launch configuration. You can specify your launch configuration with multiple EC2 Auto Scaling groups. However, you can only specify one launch configuration for an EC2 Auto Scaling group at a time, and you can't modify a launch configuration after you've created it. Therefore, if you want to change the launch configuration for your EC2 Auto Scaling group, you must create a launch configuration and then update your EC2 Auto Scaling group with the new launch configuration. When you change the launch configuration for your EC2 Auto Scaling group, any new instances are launched using the new configuration parameters, but existing instances are not affected. You can see the [launch configurations](https://docs.aws.amazon.com/autoscaling/ec2/userguide/LaunchConfiguration.html) section of the EC2 Auto Scaling User Guide for more details.  

**Q: How many instances can an EC2 Auto Scaling group have?**

You can have as many instances in your EC2 Auto Scaling group as your EC2 quota allows.  

**Q: What happens if a scaling activity causes me to reach my Amazon EC2 limit of instances?**

Amazon EC2 Auto Scaling cannot scale past the Amazon EC2 limit of instances that you can run. If you need more Amazon EC2 instances, complete the [Amazon EC2 instance request form](https://aws.amazon.com/contact-us/ec2-request/).  

**Q: Can EC2 Auto Scaling groups span multiple AWS regions?**

EC2 Auto Scaling groups are regional constructs. They can span Availability Zones, but not AWS regions.  

**Q: How can I implement changes across multiple instances in an EC2 Auto Scaling group?**

You can use AWS CodeDeploy or CloudFormation to orchestrate code changes to multiple instances in your EC2 Auto Scaling group.

**Q: If I have data installed in an EC2 Auto Scaling group, and a new instance is dynamically created later, is the data copied over to the new instances?**

Data is not automatically copied from existing instances to new instances. You can use [lifecycle hooks](http://docs.aws.amazon.com/autoscaling/latest/userguide/lifecycle-hooks.html) to copy the data, or an [Amazon RDS](https://aws.amazon.com/rds/) database including replicas.  

**Q: When I create an EC2 Auto Scaling group from an existing instance, does it create a new AMI (Amazon Machine Image)?**  

When you create an Auto Scaling group from an existing instance, it does not create a new AMI. For more information see [Creating an Auto Scaling Group Using an EC2 Instance](http://docs.aws.amazon.com/autoscaling/latest/userguide/create-asg-from-instance.html).  

**Q: How does Amazon EC2 Auto Scaling balance capacity?**  

Balancing resources across [Availability Zones](http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-regions-availability-zones.html) is a best practice for well-architected applications, as this greatly increases aggregate system availability. Amazon EC2 Auto Scaling automatically balances EC2 instances across zones when you [configure multiple zones](http://docs.aws.amazon.com/autoscaling/latest/userguide/as-add-availability-zone.html) in your EC2 Auto Scaling group settings. Amazon EC2 Auto Scaling always launches new instances such that they are balanced between zones as evenly as possible across the entire fleet. What’s more, Amazon EC2 Auto Scaling only launches into Availability Zones in which there is available capacity for the requested instance type.  

**Q: What are lifecycle hooks?**  

Lifecycle hooks let you take action before an instance goes into service or before it gets terminated. This can be especially useful if you are not baking your software environment into an Amazon Machine Image (AMI). For example, launch hooks can perform software configuration on an instance to ensure that it’s fully prepared to handle traffic before Amazon EC2 Auto Scaling proceeds to connect it to your load balancer. One way to do this is by connecting the launch hook to an AWS Lambda function that invokes RunCommand on the instance. Terminate hooks can be useful for collecting important data from an instance before it goes away. For example, you could use a terminate hook to preserve your fleet’s log files by copying them to an Amazon S3 bucket when instances go out of service.

Visit [lifecycle hooks](https://docs.aws.amazon.com/autoscaling/ec2/userguide/lifecycle-hooks.html) in our Amazon EC2 Auto Scaling User Guide for more information.  

**Q: What are the characteristics of an “unhealthy” instance?**  

An unhealthy instance is one where the hardware has become impaired for some reason (bad disk, etc.), or it is not passing a user-configured ELB health check. Amazon EC2 Auto Scaling performs [health checks](http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/monitoring-system-instance-status-check.html) on each individual EC2 instance at regular intervals, and if the instance is connected to an Elastic Load Balancing load balancer, it can also perform [ELB health checks](http://docs.aws.amazon.com/elasticloadbalancing/latest/classic/elb-healthchecks.html).  

**Q: Can I customize a health check?**  

Yes, there is an API called _SetInstanceHealth_ that allows you to change an instance's state to UNHEALTHY, which will then result in a termination and replacement.  

**Q: Can I suspend health checks (for example, to evaluate unhealthy instances)?**  

Yes, you can temporarily suspend Amazon EC2 Auto Scaling health checks by using the SuspendProcesses API. You can use the ResumeProcesses API to resume automatic health checks.  

**Q: Which health check type should I select?**  

If you are using Elastic Load Balancing (ELB) with your group, you should select an ELB health check. If you’re not using ELB with your group, you should select the EC2 health check.  

**Q: Can I use Amazon EC2 Auto Scaling for health checks and to replace unhealthy instances if I’m not using Elastic Load Balancing (ELB)?**  

You don't have to use ELB to use Auto Scaling. You can use the EC2 health check to identify and replace unhealthy instances.  

**Q: Do the Elastic Load Balancing (ELB) health checks work with Application Load Balancers and Network Load Balancers? Will an instance be marked as unhealthy if any target group associated with it becomes unhealthy?**  

Yes, Amazon EC2 Auto Scaling works with Application Load Balancers and Network Load Balancers including their health check feature.  

**Q: Is there any way to use Amazon EC2 Auto Scaling to only add a volume without adding an instance?**  

A volume is attached to a new instance when it is added. Amazon EC2 Auto Scaling doesn't automatically add a volume when the existing one is approaching capacity. You can use the EC2 API to add a volume to an existing instance.  

**Q: What does the term “stateful instances” refer to?**  

When we refer to a stateful instance, we mean an instance that has data on it, which exists only on that instance. In general, terminating a stateful instance means that the data (or state information) on the instance is lost. You may want to consider using lifecycle hooks to copy the data off of a stateful instance before it’s terminated, or enable instance protection to prevent Amazon EC2 Auto Scaling from terminating it.

## Replacing Impaired Instances

**Q: How does Amazon EC2 Auto Scaling replace an impaired instance?**

When an impaired instance fails a health check, Amazon EC2 Auto Scaling automatically terminates it and replaces it with a new one. If you’re using an Elastic Load Balancing load balancer, Amazon EC2 Auto Scaling gracefully detaches the impaired instance from the load balancer before provisioning a new one and attaching it to the load balancer. This is all done automatically, so you don’t need to respond manually when an instance needs replacing.  

**Q: How do I control which instances Amazon EC2 Auto Scaling terminates when scaling in, and how do I protect data on an instance?**

With each Amazon EC2 Auto Scaling group, you control when Amazon EC2 Auto Scaling adds instances (referred to as scaling out) or remove instances (referred to as scaling in) from your group. You can scale the size of your group manually by attaching and detaching instances, or you can automate the process through the use of a scaling policy. When you have Amazon EC2 Auto Scaling automatically scale in, you must decide which instances Amazon EC2 Auto Scaling should terminate first. You can configure this through the use of a termination policy. You can also use instance protection to prevent Amazon EC2 Auto Scaling from selecting specific instances for termination when scaling in. If you have data on an instance, and you need that data to be persistent even if your instance is scaled in, then you can use a service like S3, RDS, or DynamoDB, to make sure that it is stored off the instance.  

**Q: How long is the turn-around time for Amazon EC2 Auto Scaling to spin up a new instance at inService state after detecting an unhealthy server?**

The turnaround time is within minutes. The majority of replacements happen within less than 5 minutes, and on average it is significantly less than 5 minutes. It depends on a variety of factors, including how long it takes to boot up the AMI of your instance.  

**Q: If Elastic Load Balancing (ELB) determines that an instance is unhealthy, and moved offline, will the previous requests sent to the failed instance be queued and rerouted to other instances within the group?**

When ELB notices that the instance is unhealthy, it will stop routing requests to it. However, prior to discovering that the instance is unhealthy, some requests to that instance will fail.  

**Q: If you don’t use Elastic Load Balancing (ELB) how would users be directed to the other servers in a group if there was a failure?**

You can integrate with Route53 (which Amazon EC2 Auto Scaling does not currently support out of the box, but many customers use). You can also use your own reverse proxy, or for internal microservices, can use service discovery solutions.  

## Security

**Q: How do I control access to Amazon EC2 Auto Scaling resources?**

Amazon EC2 Auto Scaling integrates with [AWS Identity and Access Management](https://aws.amazon.com/iam/) (IAM), a service that enables you to do the following:

- Create users and groups under your organization's AWS account
- Assign unique security credentials to each user under your AWS account
- Control each user's permissions to perform tasks using AWS resources
- Allow the users in another AWS account to share your AWS resources
- Create roles for your AWS account and define the users or services that can assume them
- Use existing identities for your enterprise to grant permissions to perform tasks using AWS resources  
    

For example, you could create an IAM policy that grants the Managers group permission to use only the _DescribeAutoScalingGroups_, _DescribeLaunchConfigurations_, _DescribeScalingActivities_, and _DescribePolicies_ API operations. Users in the Managers group could then use those operations with any Amazon EC2 Auto Scaling groups and launch configurations. With Amazon EC2 Auto Scaling resource-level permissions, you can restrict access to a particular EC2 Auto Scaling group or launch configuration.

For more information, see the [Controlling Access to Your Auto Scaling Resources](http://docs.aws.amazon.com/autoscaling/latest/userguide/control-access-using-iam.html) section of the Amazon EC2 Auto Scaling user guide.  

**Q: Can you define a default admin password on Windows instances with Amazon EC2 Auto Scaling?**

You can use the Key Name parameter to CreateLaunchConfiguration to associate a key pair with your instance. You can then use the _GetPasswordData_ API in EC2. This is also possible through the AWS Management Console.  

**Q: Are CloudWatch agents automatically installed on EC2 instances when you create an Amazon EC2 Auto Scaling group?**

If your AMI contains a CloudWatch agent, it’s automatically installed on EC2 instances when you create an EC2 Auto Scaling group. With the stock Amazon Linux AMI, you need to install it (recommended, via yum).  

## Cost Optimization

**Q: Can I create a single ASG to scale instances across different purchase options?**

Yes. You can provision and automatically scale EC2 capacity across different EC2 instance types, Availability Zones, and On-Demand, RIs and Spot purchase options in a single Auto Scaling Group. You have the option to define the desired split between On-Demand and Spot capacity, select which instance types work for your application, and specify preference for how EC2 Auto Scaling should distribute the ASG capacity within each purchasing model.  

**Q: Can I use ASGs to launch and manage just Spot Instances or just On-Demand instances and RIs?  
**

Yes. You can configure your ASG specifying all capacity to be only Spot instances or all capacity to be only On-Demand instances and RIs.

**Q: Can I have a base capacity with On-Demand instances and RIs, and scale my ASG out on Spot instances?  
**

Yes. When setting up an ASG to combine purchasing models, you can specify the base capacity of the group to be fulfilled by On-Demand instances. As the ASG scales in or scale out, EC2 Auto Scaling ensures the base capacity be fulfilled with On-Demand instances and anything beyond that be fulfilled with either only Spot instances or a specified percentage mix of On-Demand or Spot instances.

**Q: Can I modify the configuration of an ASG to update the different properties pertaining to combining purchasing models and specifying multiple instance types?  
**

Yes. Similar to other ASG parameters, customers can update an existing ASG to modify one or all parameters pertaining to combining purchasing models and specifying multiple instance types, including instance types, prioritization order for On-Demand instances, percentage split between On-Demand and Spot instances, and allocation strategy.

**Q: Can I use RI discounts with On-Demand Instances in an ASG?  
**

Yes. For example, if you have RIs for C4 instances and EC2 Auto Scaling launches a C4 you will receive your RI pricing for On-Demand Instances.

**Q: Can I specify instances of different sizes (CPU cores, memory) in my Auto Scaling group?  
**

Yes. You can specify any instance type available in a region. Additionally, you can specify an optional weight for each instance type, which defines the capacity units that each instance would contribute to your application’s performance.  

**Q: What if the instance types I like are not available in an Availability Zone?  
**

If none of the specified instance types are available in an Availability Zone, Auto Scaling will retarget the launches in other Availability Zones associated with the Auto Scaling group. Auto Scaling will always prefer keeping your compute balanced across Availability Zones and retarget if all instance types are not available in an Availability Zone.

## Pricing

**Q: What are the costs for using Amazon EC2 Auto Scaling?**

Amazon EC2 Auto Scaling fleet management for EC2 instances carries no additional fees. The dynamic scaling capabilities of Amazon EC2 Auto Scaling are enabled by Amazon CloudWatch and also carry no additional fees. Amazon EC2 and Amazon CloudWatch service fees apply and are billed separately.