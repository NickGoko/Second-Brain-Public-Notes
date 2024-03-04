---
tags:
  - cloud/aws
---


![[Pasted image 20240214112409.png]]  
![[Pasted image 20240214114516.png]]  
![[Pasted image 20240214114620.png]]  
![[Pasted image 20240214114635.png]]  
The **Amazon Elastic Kubernetes Service (Amazon EKS)** is <mark style="background: #BBFABBA6;">a managed service for running Kubernetes on AWS and on-premises</mark>.

- <mark style="background: #FFF3A3A6;">Amazon EKS can run on Amazon EC2 or AWS Fargate</mark>.
- <mark style="background: #CACFD9A6;">Integrates with Application Load Balancers, AWS IAM for RBA and Amazon VPC.</mark>

**Amazon EKS** <mark style="background: #ADCCFFA6;">provides a scalable and highly available Kubernetes</mark> _control plane_ <mark style="background: #ADCCFFA6;">running across multiple AWS Availability Zones (AZs)</mark>.

Amazon EKS <mark style="background: #BBFABBA6;">automatically manages availability and scalability of Kubernetes API servers and etcd persistence layer.</mark>

**Amazon EKS** <mark style="background: #FFB86CA6;">runs the Kubernetes control plane across three AZs to ensure high availability, and automatically detects and replaces unhealthy control plane nodes.</mark>

**_Exam tip:_** _The principle use case is when organizations need a consistent control plane for managing containers across hybrid clouds and multicloud environments._

# FAQ
**Q: What is Amazon Elastic Kubernetes Service (Amazon EKS)?**  
A: Amazon EKS is <mark style="background: #D2B3FFA6;">a managed service that makes it easy for you to run Kubernetes on AWS without installing and operating your own Kubernetes control plane or worker nodes. </mark>

**Q: What is Kubernetes?**  
A: **Kubernetes** is <mark style="background: #ADCCFFA6;">an open-source container orchestration system allowing you to deploy and manage containerized applications at scale</mark>.  
Kubernetes arranges containers into logical groupings for management and discoverability, then launches them onto clusters of Amazon Elastic Compute Cloud (Amazon EC2) instances.  
Using Kubernetes, you can run containerized applications including microservices, batch processing workers, and platforms as a service (PaaS) using the same toolset on premises and in the cloud.

**Q: Why should I use Amazon EKS?**

A: <mark style="background: #BBFABBA6;">Amazon EKS provisions and scales the Kubernetes control plane, including the application programming interface (API) servers and backend persistence layer, across multiple AWS Availability Zones (AZs) for high availability and fault tolerance. </mark>  
<mark style="background: #FFB86CA6;">Amazon EKS automatically detects and replaces unhealthy control plane nodes and patches the control plane. </mark>You can run EKS using AWS Fargate, which provides serverless compute for containers. Fargate removes the need to provision and manage servers, lets you specify and pay for resources per application, and improves security through application isolation by design.

Amazon EKS is integrated with many AWS services to provide scalability and security for your applications. These services include Elastic Load Balancing for load distribution, AWS Identity and Access Management (IAM) for authentication, Amazon Virtual Private Cloud (VPC) for isolation, and AWS CloudTrail for logging.  

**Q: How does Amazon EKS work?**

A: Amazon EKS works by provisioning (starting) and managing the Kubernetes control plane and worker nodes for you. At a high level, Kubernetes consists of two major components: a cluster of 'worker nodes' running your containers, and the control plane managing when and where containers are started on your cluster while monitoring their status.

Without Amazon EKS, you have to run both the Kubernetes control plane and the cluster of worker nodes yourself. With Amazon EKS, you provision your worker nodes using a single command in the EKS console, command-line interface (CLI), or API. AWS handles provisioning, scaling, and managing the Kubernetes control plane in a highly available and secure configuration. This removes a significant operational burden and allows you to focus on building applications instead of managing AWS infrastructure.

**Q: Which operating systems does Amazon EKS support?**

A: Amazon EKS supports Kubernetes-compatible Linux x86, ARM, and Windows Server operating system distributions. Amazon EKS provides optimized AMIs for Amazon Linux 2, Bottlerocket, and Windows Server 2019. At this time, there is no Amazon EKS optimized AMI for AL2023. EKSoptimized AMIs for other Linux distributions, such as Ubuntu, are available from their respective vendors.

**Q: I have a feature request, who do I tell?**

A: Please let us know what we can add or do better by opening a feature request on the [AWS Container Services Public Roadmap](https://github.com/aws/containers-roadmap)