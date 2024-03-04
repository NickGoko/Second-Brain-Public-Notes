---
tags:
  - cloud/aws
---
The Amazon Elastic Container Service (ECS) is <mark style="background: #BBFABBA6;">a highly scalable, high performance container management service that supports Docker containers.</mark>

- <mark style="background: #BBFABBA6;">Amazon ECS allows you to easily run applications on a managed cluster of Amazon EC2 instances.</mark>
- <mark style="background: #D2B3FFA6;">Amazon ECS eliminates the need for you to install, operate, and scale your own cluster management infrastructure.</mark>
- <mark style="background: #FF5582A6;">Using API calls you can launch and stop container-enabled applications, query the complete state of clusters, and access features like security groups, Elastic Load Balancing, EBS volumes and IAM roles.</mark>

- <mark style="background: #FFF3A3A6;">Amazon ECS can be used to schedule the placement of containers across clusters based on resource needs and availability requirements.</mark>

<mark style="background: #ADCCFFA6;">There is no additional charge for Amazon ECS</mark>. You pay for:
- Resources created with the EC2 Launch Type (e.g. EC2 instances and EBS volumes).
- <mark style="background: #FFB86CA6;">The number and configuration of tasks you run for the Fargate Launch Type</mark>.

>It is possible to use Elastic Beanstalk to handle the provisioning of an Amazon ECS cluster, load balancing, auto-scaling, monitoring, and placing your containers across your cluster.

Alternatively <mark style="background: #BBFABBA6;">use ECS directly for more fine-grained control for customer application architectures.</mark>

<mark style="background: #ADCCFFA6;">It is possible to associate a service on Amazon ECS to an Application Load Balancer (ALB) for the Elastic Load Balancing (ELB) service.</mark>  
<mark style="background: #CACFD9A6;">The ALB supports a target group that contains a set of instance ports.</mark> You can specify a dynamic port in the ECS task definition which gives the container an unused port when it is scheduled on the EC2 instance.

You can use any AMI that meets the Amazon ECS AMI specification. For example, please follow the link regarding [Amazon ECS-Optimized AMIs](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/ecs-optimized_AMI.htm).

## Amazon ECS Vs Amazon EKS

Amazon also provide the **Elastic Container Service for Kubernetes (Amazon EKS)** which can be <mark style="background: #BBFABBA6;">used to deploy, manage, and scale containerized applications using Kubernetes on AWS.</mark>

The table below describes some of the differences between these services to help you understand when you might choose one over the other:

|   |   |
|---|---|
|**Amazon ECS**|**Amazon EKS**|
|Managed, highly available, highly scalable container platform|Managed, highly available, highly scalable container platform|
|AWS-specific platform that supports Docker Containers|<mark style="background: #ADCCFFA6;">Compatible with upstream Kubernetes so it’s easy to lift and shift from other Kubernetes deployments</mark> |
|Considered simpler and easier to use|<mark style="background: #ADCCFFA6;">Considered more feature-rich and complex with a steep learning curve</mark> |
|<mark style="background: #FFB86CA6;">Leverages AWS services like Route 53, ALB, and CloudWatch</mark> |A hosted Kubernetes platform that <mark style="background: #ABF7F7A6;">handles many things internally</mark> |
|“<mark style="background: #D2B3FFA6;">Tasks” are instances of containers that are run on underlying compute but more of less isolated</mark> |<mark style="background: #FF5582A6;">“Pods” are containers collocated with one another and can have shared access to each other</mark> |
|Limited extensibility|Extensible via a wide variety of third-party and community add-ons.|

## Launch Types

- <mark style="background: #CACFD9A6;">An Amazon ECS launch type determines the type of infrastructure on which your tasks and services are hosted.</mark>  
There are two launch types, and the table below describes some of the differences between the two launch types:

|   |   |
|---|---|
|**Amazon EC2**|**Amazon Fargate**|
|<mark style="background: #BBFABBA6;">You can explicitly provision EC2 instances</mark> |<mark style="background: #BBFABBA6;">The control plan asks for resources and Fargate automatically provisions</mark> |
|<mark style="background: #FFF3A3A6;">You’re responsible for upgrading, patching, care of EC2 pool</mark> |<mark style="background: #FFF3A3A6;">Fargate provisions compute as needed</mark> |
|You must handle cluster optimization|Fargate handles customer optimizations|
|More granular control over infrastructure|Limited control, as infrastructure is automated|

### Fargate Launch Type
- The Fargate launch type <mark style="background: #BBFABBA6;">allows you to run your containerized applications without the need to provision and manage the backend infrastructure.</mark>  
  Just <mark style="background: #ADCCFFA6;">register your task definition and Fargate launches the container for you.</mark>
- <mark style="background: #CACFD9A6;">Fargate Launch Type is a serverless infrastructure managed by AWS.</mark>
- <mark style="background: #ADCCFFA6;">Fargate only supports container images hosted on Elastic Container Registry (ECR) or Docker Hub.</mark>  
![[Pasted image 20240214102132.png]]
### EC2 Launch Type
- <mark style="background: #FFF3A3A6;">The EC2 launch type allows you to run your containerized applications on a cluster of Amazon EC2 instances that you manage.</mark>
- Private repositories are only supported by the EC2 Launch Type.  
![[Pasted image 20240214101929.png]]  
The following diagram shows the two launch types and summarizes some key differences:

![Amazon ECS EC2 vs Fargate](https://digitalcloud.training/wp-content/uploads/2022/01/amazon-ecs-ec2-vs-fargate-1.jpeg)

## ECS Terminology
The following table provides an overview of some of the terminology used with Amazon ECS:

|   |   |
|---|---|
|**Amazon ECS Term**|**Definition**|
|Cluster|Logical Grouping of EC2 Instances|
|Container Instance|<mark style="background: #FFF3A3A6;">EC2 instance running the ECS agent</mark> |
|Task Definition|<mark style="background: #ADCCFFA6;">Blueprint that describes how a docker container should launch</mark> |
|Task|<mark style="background: #D2B3FFA6;">A running container using settings in a Task Definition</mark> |
|Service|<mark style="background: #FF5582A6;">Defines long running tasks – can control task count with Auto Scaling and attach an ELB</mark> |

![](https://i.imgur.com/cDtHWDe.png)

![[Pasted image 20240214102431.png]]  
![[Pasted image 20240214102559.png]]
## Images
<mark style="background: #FFF3A3A6;">Containers are created from a read-only template called an image which has the instructions for creating a Docker container.</mark>
- Images are built from a Dockerfile.
- Only Docker containers are currently supported.  
<mark style="background: #ABF7F7A6;">An image contains the instructions for creating a Docker container.</mark>
- Images are stored in a registry such as DockerHub or AWS Elastic Container Registry (ECR).
- ECR is a managed AWS Docker registry service that is secure, scalable, and reliable.  
	ECR supports private Docker repositories with resource-based permissions using AWS IAM to access repositories and images.

- Developers can use the Docker CLI to push, pull and manage images.

## Tasks and Task Definitions

- <mark style="background: #CACFD9A6;">To prepare your application to run on Amazon ECS, you </mark><mark style="background: #FF5582A6;">create a task definition</mark>.
- A **task definition** is required to run Docker containers in Amazon ECS.
- A **task definition** is <mark style="background: #FFF3A3A6;">a text file in JSON format that describes one or more containers, up to a maximum of 10. </mark>
  
<mark style="background: #ADCCFFA6;">Task definitions use Docker images to launch containers. </mark>  
<mark style="background: #FFB86CA6;">You specify the number of tasks to run (i.e. the number of containers).</mark>

_Some of the parameters you can specify in a task definition include_:
- <mark style="background: #FFF3A3A6;">Which Docker images to use with the containers in your task</mark>.
- <mark style="background: #CACFD9A6;">How much CPU and memory to use with each container.</mark>
- <mark style="background: #FFF3A3A6;">Whether containers are linked together in a task.</mark>
- <mark style="background: #CACFD9A6;">The Docker networking mode to use for the containers in your task.</mark>
- <mark style="background: #FFF3A3A6;">What (if any) ports from the container are mapped to the host container instances.</mark>
- Whether the task should continue if the container finished or fails.
- <mark style="background: #FFF3A3A6;">The commands the container should run when it is started.</mark>
- <mark style="background: #CACFD9A6;">Environment variables that should be passed to the container when it starts.</mark>
- <mark style="background: #FFF3A3A6;">Data volumes that should be used with the containers in the task.</mark>
- IAM role the task should use for permissions.

You can use Amazon ECS Run task to run one or more tasks once.

## ECS Clusters
- ECS Clusters are a <mark style="background: #BBFABBA6;">logical grouping of container instances that you can place tasks on.</mark>
- A default cluster is created but you can then create multiple clusters to separate resources.
- <mark style="background: #FFF3A3A6;">ECS allows the definition of a specified number (desired count) of tasks to run in the cluster</mark>.
  
- <mark style="background: #ADCCFFA6;">Clusters can contain tasks using the Fargate and EC2 launch type.</mark>
- <mark style="background: #083CA4A6;">For clusters with the EC2 launch type clusters can contain different container instance types.</mark>
- <mark style="background: #ADCCFFA6;">Each container instance may only be part of one cluster at a time.</mark>
  
- “<mark style="background: #FFB86CA6;">Services” provide auto-scaling functions for ECS.</mark>
  
- <mark style="background: #CACFD9A6;">Clusters are region specific.</mark>
  
- <mark style="background: #ADCCFFA6;">You can create IAM policies for your clusters to allow or restrict users’ access to specific clusters.</mark>

## Services
<mark style="background: #BBFABBA6;">Amazon ECS allows you to run and maintain a specified number of instances of a task definition simultaneously in an Amazon ECS cluster. </mark>  

<mark style="background: #083CA4A6;">This is called a service.</mark>  

><mark style="background: #FF5582A6;">If any of your tasks should fail or stop for any reason, the Amazon ECS service scheduler launches another instance of your task definition to replace it and maintain the desired count of tasks in the service depending on the scheduling strategy used.</mark>

<mark style="background: #ADCCFFA6;">In addition to maintaining the desired count of tasks in your service, you can optionally run your service behind a load balancer. </mark>  
<mark style="background: #CACFD9A6;">The load balancer distributes traffic across the tasks that are associated with the service.</mark>

There are <mark style="background: #FFF3A3A6;">two service scheduler strategies </mark>available:
- REPLICA:
    - <mark style="background: #ADCCFFA6;">The replica scheduling strategy places and maintains the desired number of tasks across your cluster</mark>. <mark style="background: #FFB86CA6;">By default, the service scheduler spreads tasks across Availability Zones</mark>. You can use task placement strategies and constraints to customize task placement decisions. For more information, see [Replica](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/ecs_services.html#service_scheduler_replica).
- DAEMON:
    - <mark style="background: #ADCCFFA6;">The daemon scheduling strategy deploys exactly one task on each active container instance that meets all of the task placement constraints that you specify in your cluster.</mark> The service scheduler evaluates the task placement constraints for running tasks and will stop tasks that do not meet the placement constraints. When using this strategy, there is no need to specify a desired number of tasks, a task placement strategy, or use Service Auto Scaling policies. For more information, see [Daemon](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/ecs_services.html#service_scheduler_daemon).

## Service Scheduler
- You can schedule ECS using **Service Scheduler** and **Custom Scheduler**.
- <mark style="background: #CACFD9A6;">Ensures that the specified number of tasks are constantly running and reschedules tasks when a task fails.</mark>
- <mark style="background: #CACFD9A6;">Can ensure tasks are registered against an ELB.</mark>

## Custom Scheduler
- You can <mark style="background: #CACFD9A6;">create your own schedulers to meet business needs.</mark>
- Leverage third party schedulers such as Blox.
- The Amazon ECS schedulers leverage the same cluster state information provided by the Amazon ECS API to make appropriate placement decisions.

## Service Discovery
<mark style="background: #CACFD9A6;">Because containers are immutable by nature, they can churn regularly and be replaced with newer versions of the service.</mark> This means that <mark style="background: #FFF3A3A6;">there is a need to register the new and deregister the old/unhealthy services</mark>. To do this on your own is challenging, hence the need for service discovery.

**AWS Cloud Map** is a cloud resource discovery service. <mark style="background: #ABF7F7A6;">With Cloud Map, you can define custom names for your application resources, and it maintains the updated location of these dynamically changing resources.</mark> This increases your application availability because your web service always discovers the most up-to-date locations of its resources.

<mark style="background: #CACFD9A6;">Cloud Map natively integrates with ECS, and as we build services</mark> in the workshop, will see this firsthand. For more information on service discovery with ECS, please see [here](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/service-discovery.html).

[![cloudmap](https://ecsworkshop.com/images/cloudmapproduct.png)](https://ecsworkshop.com/images/cloudmapproduct.png)
## ECS Container Agent

The **ECS container agent** <mark style="background: #FFF3A3A6;">allows container instances to connect to the cluster.</mark>

The container agent runs on each infrastructure resource on an ECS cluster.

The ECS container agent is included in the Amazon ECS optimized AMI and can also be installed on any EC2 instance that supports the ECS specification (only supported on EC2 instances).

Linux and Windows based.

For non-AWS Linux instances to be used on AWS you must manually install the ECS container agent.

## Auto Scaling
![[Pasted image 20240214111016.png]]
### Service Auto Scaling
Amazon ECS service can optionally be configured to use **Service Auto Scaling** <mark style="background: #BBFABBA6;">to adjust the desired task count up or down automatically</mark>.

<mark style="background: #CACFD9A6;">Service Auto Scaling leverages the Application Auto Scaling service to provide this functionality</mark>.

Amazon ECS Service Auto Scaling supports the following types of scaling policies:
- [Target Tracking Scaling Policies](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/service-autoscaling-targettracking.html)—<mark style="background: #FFF3A3A6;">Increase or decrease the number of tasks that your service runs based on a target value for a specific CloudWatch metric.</mark> This is similar to the way that your thermostat maintains the temperature of your home. You select temperature and the thermostat does the rest.
- [Step Scaling Policies](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/service-autoscaling-stepscaling.html)—<mark style="background: #FFF3A3A6;">Increase or decrease the number of tasks that your service runs in response to CloudWatch alarms</mark>.  
	  Step scaling is based on a set of scaling adjustments, known as <mark style="background: #FF5582A6;">step adjustments</mark>, which vary based on the size of the alarm breach.
- [Scheduled Scaling](https://docs.aws.amazon.com/autoscaling/application/userguide/application-auto-scaling-scheduled-scaling.html)—Increase or decrease the number of tasks that your service runs based on the date and time.

![Amazon ECS Service Auto Scaling](https://digitalcloud.training/wp-content/uploads/2022/01/amazon-ecs-service-auto-scaling-1.jpeg)

### Cluster Auto Scaling
![[Pasted image 20240214111109.png]]  
<mark style="background: #CACFD9A6;">Uses an Amazon ECS resource type called</mark> a **Capacity Provider**.

A Capacity Provider can be associated with an EC2 Auto Scaling Group (ASG).

<mark style="background: #BBFABBA6;">When you associate an ECS Capacity Provider with an ASG and add the Capacity Provider to an ECS cluster, the cluster can now scale your ASG automatically</mark> by using two new features of ECS:

1. **Managed scaling**, with an automatically created scaling policy on your ASG, and a new scaling metric (Capacity Provider Reservation) that the scaling policy uses; and
2. **Managed instance termination protection**, which enables container-aware termination of instances in the ASG when scale-in happens.

![](https://digitalcloud.training/wp-content/uploads/2022/01/word-image-1.png)

![[Pasted image 20240214111157.png]]
## Security/SLA
![[Pasted image 20240214102328.png]]
- EC2 instances use an IAM role to access ECS.
- IAM can be used to control access at the container level using IAM roles.  
<mark style="background: #ADCCFFA6;">The container agent makes calls to the ECS API on your behalf through the applied IAM roles and policies</mark>.

<mark style="background: #FFB8EBA6;">You need to apply IAM roles to container instances before they are launched </mark>(_EC2 launch type_).

Assign extra permissions to tasks through separate IAM roles (**IAM Roles for Tasks**).

<mark style="background: #BBFABBA6;">ECS tasks use an IAM role to access services and resources.</mark>

Security groups attach at the instance or container level.

You have root level access to the operating system of the EC2 instances.

The Compute SLA guarantees a Monthly Uptime Percentage of at least 99.99% for Amazon ECS.

## ECS with X-Ray

There are two ways to run X-Ray:

As a daemon: X-Ray agent runs in a daemon container.

As a “sidecar”: X-Ray runs alongside each container.

For Fargate the X-Ray daemon only runs as a sidecar.

![Amazon ECS with AWS X-Ray Daemon](https://digitalcloud.training/wp-content/uploads/2022/01/amazon-ecs-with-aws-x-ray-daemon-1.jpeg)

Task definition:

- X-Ray runs on port 2000 UDP.
- Must specify the daemon address.
- Must link the containers together.

X-Ray provides a Docker container image that you can deploy alongside your application:

- Command: _docker pull amazon/aws-xray-daemon_

## ECS with Elastic Beanstalk

There are two options: Single and MultiDocker container mode.

### Single Container Docker

The single container platform can be used to deploy a Docker image (described in a Dockerfile or Dockerrun.aws.json definition) and source code to EC2 instances running in an Elastic Beanstalk environment.

Use the single container platform when you only need to run one container per instance.

### Multicontainer Docker

The other basic platform, Multicontainer Docker, uses the Amazon Elastic Container Service to coordinate the deployment of multiple Docker containers to an Amazon ECS cluster in an Elastic Beanstalk environment.

The instances in the environment each run the same set of containers, which are defined in a Dockerrun.aws.json file.

Use the multicontainer platform when you need to deploy multiple Docker containers to each instance.

ElasticBeanstalk creates the following resources:

- ECS cluster.
- EC2 container instances.
- Load balancers (for high availability mode).
- Task definitions and execution.

Requires a config file Dockerrun.aws.json at the root of the source code.

Your Docker images must be pre-built (can be stored in ECR).

## ECSEventBridge
![[Pasted image 20240214111436.png]]  
![[Pasted image 20240214111542.png]]

## ECS tasksSQS
![[Pasted image 20240214111701.png]]




## Using an Amazon Elastic Load Balancer with ECS

<mark style="background: #CACFD9A6;">It is possible to associate a service on Amazon ECS to an Amazon Elastic Load Balancer (ELB).  
</mark>  
The ALB supports a target group that contains a set of instance ports.

You can specify a dynamic port in the ECS task definition which gives the container an unused port when it is scheduled on the EC2 instance (this is specific to ALB only).

![Amazon ECS with Application Load Balancer (ALB)](https://digitalcloud.training/wp-content/uploads/2022/01/amazon-ecs-with-application-load-balancer-alb-1.jpeg)

![[Module 13 - Building Microservices and Serverless Architectures#Amazon ECS]]