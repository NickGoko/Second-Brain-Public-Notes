---
tags:
  - cloud/aws
---

![[Module 13 - Building Microservices and Serverless Architectures#AWS Fargate]]

---
---

![[Developer Learning Plan#Introduction to AWS Fargate]]

# FAQ
## General

Open all

### What is AWS Fargate?

AWS Fargate is a serverless compute engine for containers that works with both [Amazon Elastic Container Service](https://aws.amazon.com/ecs/) (ECS) and [Amazon Elastic Kubernetes Service](https://aws.amazon.com/eks/) (EKS). AWS Fargate makes it easy to focus on building your applications by eliminating the need to provision and manage servers, lets you specify and pay for resources per application, and improves security through application isolation by design.

### Why Should I Use AWS Fargate?

AWS Fargate is a serverless, pay-as-you-go compute engine that lets you focus on building applications without managing servers. AWS Fargate is compatible with both Amazon ECS and Amazon EKS. AWS Fargate makes it easy to scale and manage cloud applications by shifting as much management of the underlying infrastructure resources to AWS so development teams can focus on writing code that solve business problems. Shifting tasks such as server management, resource allocation, and scaling to AWS does not only improve your operational posture, but also accelerates the process of going from idea to production on the cloud and lowers the total cost of ownership (TCO). With multiple CPU architectures and operating systems supported, you can enjoy the serverless benefits of cost, agility and scale across a wide variety of applications.

### How Does AWS Fargate Work with Amazon ECS and Amazon EKS?

Amazon ECS is a highly scalable, high performance container management service and Amazon EKS is a fully managed Kubernetes service. Both services can schedule containers onto AWS Fargate to automatically scale, load balance, and optimize container availability through managed scheduling, providing an easier way to build and operate containerized applications.

### Where Does My Workload Run on AWS Fargate?

With AWS Fargate each workload runs on its own single use, single tenant compute instance. Each workload is isolated by a virtualization boundary, with each Amazon ECS Task or Kubernetes pod running on a newly provisioned instance. Please see the [AWS Fargate Security Whitepaper](https://d1.awsstatic.com/whitepapers/AWS_Fargate_Security_Overview_Whitepaper.pdf) for more detail on the AWS Fargate architecture.

### How Should I Choose when to Use AWS Fargate?

Choose AWS Fargate for its isolation model and security. You should also select Fargate if you want to launch containers without having to provision or manage [Amazon Elastic Compute Cloud](https://aws.amazon.com/ec2/) (EC2) instances. AWS Fargate has built-in integrations with AWS services and third-party tools that allows you to monitor your applications and gather metrics and logs. And, with AWS Fargate, you pay only for compute resources used, with no upfront expenses. If you require greater control of your Amazon EC2 instances or broader customization options, then use Amazon ECS or Amazon EKS without AWS Fargate. Use Amazon EC2 for GPU workloads, which are not supported on AWS Fargate today.

### Can I Run My Arm-based Applications on AWS Fargate?

Yes. When using Amazon ECS, AWS Fargate allows you to run your Arm-based applications by using Arm-compatible container images or multi-architecture container images in [Amazon Elastic Container Registry](https://aws.amazon.com/ecr/) (Amazon ECR). You can simply specify the CPU Architecture as Arm64 in your Amazon ECS Task Definition to target AWS Fargate powered by Arm-based [AWS Graviton Processors](https://aws.amazon.com/ec2/graviton/). Use Amazon EC2 to run Arm workloads on Amazon EKS, which are not supported on AWS Fargate today.

### Can I Run My Amazon ECS Windows Containers on AWS Fargate?

Yes. AWS Fargate offers a serverless approach for running your Windows containers. It removes the need to provision and manage servers and lets you specify and pay for resources per application. AWS Fargate provides task-level isolation and handles the necessary patching and updating to help provide a secure compute environment. Please see the [Windows platform versions](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/platform-windows-fargate.html) documentation page for supported versions of Windows Server.

### Can I Use My Existing Microsoft Windows License with AWS Fargate?

Since AWS Fargate is a serverless compute engine, customers do not need to manage the underlying compute instances running in AWS Fargate. Therefore, AWS Fargate will manage the Windows OS licenses for you and the cost of doing so is built into the AWS Fargate pricing. 

### What Are the Service Quotas for AWS Fargate?

[Service quotas in AWS Fargate](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/service-quotas.html#service-quotas-fargate) are based on the number of vCPU cores used in a given region in a given account. New AWS accounts might have initial lower quotas that can increase over time, and request to raise these soft limits through the [standard AWS service quota increase process](https://docs.aws.amazon.com/servicequotas/latest/userguide/request-quota-increase.html). For workloads that will require significant scale (10,000s of cores) AWS recommends a multi-account strategy.

### What Does the AWS Fargate SLA Guarantee?

Our Compute SLA guarantees a Monthly Uptime Percentage of at least 99.99% for AWS Fargate. AWS makes two SLA commitments for the Included Containers Services: (1) a Multi-AZ Included Container Service SLA that governs Included Container Services deployed across multiple AZs; and (2) a Single Task/Pod SLA that governs Included Container Service tasks and pods individually. Please see the [AWS Fargate and Amazon Elastic Container Service SLA](https://aws.amazon.com/ecs/sla/) page.

### How Do I Know if I Qualify for an SLA Service Credit?

You are eligible for an AWS Fargate SLA credit under the Compute SLA if more than one Availability Zone in which you are running a task, within the same region, has a Monthly Uptime Percentage of less than 99.99% during any monthly billing cycle. For full details on all of the terms and conditions of the SLA, as well as details on how to submit a claim, please see the [Compute SLA details page](https://aws.amazon.com/compute/sla/).

## Using AWS Fargate

Close all

### How Can I Improve the Startup time of My Container Tasks Running on AWS Fargate?

- Seekable OCI (SOCI) can help reduce the launch time of Amazon ECS tasks on AWS Fargate. SOCI is a technology open sourced by AWS that enables containers to launch faster by lazily loading the container image. To learn how to get started with SOCI, please visit the [documentation](https://docs.aws.amazon.com/AmazonECS/latest/userguide/container-considerations.html#fargate-tasks-soci-images) and the [blog post](https://aws.amazon.com/blogs/aws/aws-fargate-enables-faster-container-startup-using-seekable-oci/).
- Reducing AWS Fargate startup times with zstd compressed container images. The layers of a container image are compressed for efficiency, by default using the [gzip](https://en.wikipedia.org/wiki/Gzip) format. However, containerd supports an alternative format known as “[zstd](https://en.wikipedia.org/wiki/Zstd)” that has been shown to decompress more quickly, resulting in faster task launch times when using AWS Fargate. [Please see this blogpost](https://aws.amazon.com/blogs/containers/reducing-aws-fargate-startup-times-with-zstd-compressed-container-images/) for more details on how to build container images with zstd.

### How Do I Size Workloads for AWS Fargate?

It is recommended to load test applications locally, or in development environments, to understand the requirements of the application to size the request appropriately. [AWS Compute Optimizer](https://docs.aws.amazon.com/compute-optimizer/latest/ug/view-ecs-recommendations.html) can be used to provide recommendations if a workload is under or over sized.

### How Do I Get Network Traffic in and out of My Workload on AWS Fargate?

On AWS Fargate, each ECS Task or Kubernetes Pod is given a dedicated [elastic network interface (ENI)](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-eni.html) attached into your [virtual private cloud (VPC)](https://docs.aws.amazon.com/vpc/latest/userguide/what-is-amazon-vpc.html). All traffic in and out of the containerized workload goes through this ENI. Therefore [VPC Security Groups](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-security-groups.html) and [VPC network ACLs](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-network-acls.html) can be used to secure the ENI, and [VPC Flow Logs](https://docs.aws.amazon.com/vpc/latest/userguide/flow-logs.html) can be used to monitor traffic flows.

### Can I Run Stateful Workloads on AWS Fargate?

Each workload that runs on AWS Fargate is given full access to [20 GiB of ephemeral storage](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/fargate-task-storage.html) to use as temporary storage while the workload is running. Once the workload has stopped, any data stored in this 20 GiB volume is erased. This ephemeral storage volume can be expanded up to 200GiB on Amazon ECS and 175 GiB on Amazon EKS. [Amazon Elastic File System](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/efs-volumes.html) (EFS) an be used to provide persistent storage to workloads running on AWS Fargate.

### Can I Build Container Images within AWS Fargate?

Common approaches to building containers from within containers often require privileged mode (such as with Docker in Docker), which is unavailable in AWS Fargate's security model, or mounting of the docker socket into a container, which is unavailable due to AWS Fargate utilizing containerd as of [Platform Version 1.4](https://aws.amazon.com/blogs/containers/aws-fargate-launches-platform-version-1-4/). Alternatively, rootless image build project such as [Kaniko](https://github.com/GoogleContainerTools/kaniko) can be deployed within AWS Fargate's security model and are a viable option for building container images.

## Security and Compliance

Close all

### Can AWS Fargate Be Used in Solutions that Must Conform to a Specific compliance Programs?

AWS Fargate meets the standards for a wide array of compliance programs, including PCI DSS, SOC, FIPS 140-2, FedRAMP, and HIPAA. For more information and a complete list of programs, please see the [AWS Cloud Security Services in Scope documentation](https://aws.amazon.com/compliance/services-in-scope/). 

### Can I Use AWS Fargate for Protected Health Information (PHI) and other HIPAA Regulated Workloads?

Yes. AWS Fargate is HIPAA-eligible. If you have an executed Business Associate Addendum (BAA) with AWS, you can process encrypted Protected Health Information (PHI) using containers deployed onto AWS Fargate. For more information, please visit [our page on HIPAA compliance](https://aws.amazon.com/compliance/hipaa-compliance/). If you plan to process, store, or transmit PHI and do not have an executed BAA from AWS, please contact us for more information. 

### Can I Use AWS Fargate for US Government-regulated Workloads or for Processing Sensitive Controlled Unclassified Information (CUI)?

Yes. AWS Fargate is available in [AWS GovCloud (US)](https://aws.amazon.com/govcloud-us/?) Regions. AWS GovCloud (US) is Amazon's isolated cloud infrastructure and services designed to address specific regulatory and compliance requirements of US Government agencies, as well as contractors, educational institutions, and other US customers that run sensitive workloads in the cloud. For a full list of AWS Regions where AWS Fargate is available, please visit our [Region table](https://aws.amazon.com/about-aws/global-infrastructure/regional-product-services/) or [documentation](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/AWS_Fargate-Regions.html). 

## Integration

Close all

### How Can AWS Fargate Be Extended through Integrations with other Systems?

AWS Fargate offers a flexible integration model inclusive of both first party AWS services and third party [Amazon Partner Network](https://aws.amazon.com/ecs/partners/) (APN) solutions. The common integration mechanism is to run a sidecar container within a AWS Fargate task that can interact with the primary application container, for example a runtime security agent or log router that interacts with the primary application and then ships data to a centralized system for analysis and review.

### What Options Do I Have for Monitoring AWS Fargate Workloads?

AWS provides several tools for monitoring and responding to various facets of your AWS Fargate resources, including [Amazon CloudWatch](https://aws.amazon.com/cloudwatch/) Alarms, Amazon CloudWatch Logs, Amazon CloudWatch Events, [AWS CloudTrail](https://aws.amazon.com/cloudtrail/) Logs, [AWS Trusted Advisor](https://docs.aws.amazon.com/awssupport/latest/user/trusted-advisor.html), and [AWS Compute Optimizer](https://aws.amazon.com/compute-optimizer/). A popular approach is to utilize [CloudWatch Container Insights](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/ContainerInsights.html) to collect and analyze logs and view operational dashboards. Application logging has built-in log drivers for CloudWatch and Splunk, but FireLens for Amazon ECS can be used via task definition parameters to route logs to an AWS service or AWS Partner Network (APN) destination.

## Pricing and Cost Optimization

Close all

### What is the Pricing of AWS Fargate?

With AWS Fargate, you pay only for the amount of vCPU, memory, and storage resources provisioned by your containerized applications. vCPU and memory resources are calculated from the time your container images are pulled until the Amazon ECS task or EKS pod terminates, rounded up to the nearest second. A minimum charge of 1 minute applies. 20 GB of ephemeral storage is available for all AWS Fargate Tasks and Pods by default—you only pay for any additional storage that you configure. AWS Fargate supports Spot and Compute Savings Plan pricing options just like with Amazon EC2 instances. You can find additional details on the [pricing page](https://aws.amazon.com/fargate/pricing/).

### How Do I Optimize My Spend on AWS Fargate?

- AWS offers Spot instances for AWS Fargate tasks, which utilizes spare compute capacity that is available at a lower price than on-demand instances. By using spot instances you can run interruption tolerant Amazon ECS Tasks at up to a 70 percent discount off the AWS Fargate price. 
- AWS introduced AWS Fargate Savings Plans, a discount model that provides you with the same discounts as Reserved Instances, in exchange for a commitment to use a specific amount (measured in dollars per hour) of compute power over a oneor three-year period. 
- AWS Graviton processors are designed by AWS to deliver the best price performance for your cloud workloads running in Amazon EC2, AWS managed containers, and other managed services. AWS Graviton provides up to 40 percent better price performance over comparable x86-based instances. AWS Graviton processors are more energy efficient and use up to 60 percent less energy for the same performance than comparable EC2 instances. 
- AWS Fargate is included in the AWS Compute Optimizer, which allows you to easily identify and remediate inefficient configurations.

### Why Should I Use AWS Fargate Powered by Graviton Processors?

AWS Graviton processors are custom built by Amazon Web Services cores to deliver the best price performance for your cloud workloads. AWS Fargate powered by AWS Graviton processors delivers up to 40% improved price/performance at 20% lower cost over comparable Intel x86-based Fargate for a variety of workloads such as application servers, web services, high-performance computing, and media processing. You get the same serverless benefits of AWS Fargate while optimizing performance and cost for running your containerized workloads.