---
tags:
  - cloud/aws
---

![[Pasted image 20240214112005.png]]  
**Amazon Elastic Container Registry (ECR)** is a fully managed Docker container registry that makes it easy for developers to store, manage, and deploy Docker container images.

Amazon ECR is integrated with Amazon Elastic Container Service (ECS).

<mark style="background: #FFF3A3A6;">Amazon ECR hosts your images in a highly available and scalable architecture, allowing you to reliably deploy containers for your applications.</mark>

Integration with AWS Identity and Access Management (IAM) provides resource-level control of each repository.

![Amazon Elastic Container Registry (ECR)](https://digitalcloud.training/wp-content/uploads/2022/01/amazon-elastic-container-registry-ecr-1.jpeg)

### Pushing and Pulling Images to ECR

You must first authenticate.

To authenticate Docker to an Amazon ECR registry with get-login-password, run the **aws ecr get-login-password** command:

- ``AWS ecr get-login-password –region us-east-1 | docker login –username AWS –password-stdin aws_account_id.dkr.ecr.us-east-1.amazonaws.com``

Tag your image:

-`` docker tag e9ae3c220b23 aws_account_id.dkr.ecr.region.amazonaws.com/my-web-app``

Push the image using the **docker push** command:

- ``docker push aws_account_id.dkr.ecr.region.amazonaws.com/my-web-app``

Pull the image using the **docker pull** command. The image name format should be registry/repository[:tag] to pull by tag, or registry/repository[@digest] to pull by digest.

- ``docker pull aws_account_id.dkr.ecr.region.amazonaws.com/my-web-app:e9ae3c220b23``

[FAQs](https://aws.amazon.com/ecr/faqs/)  
**Q: How do I get started using Amazon ECR?**  
The best way to get started with Amazon ECR is to use the Docker CLI to push and pull your first image. Visit our [Getting Started](https://aws.amazon.com/ecr/getting-started/) page for more information.

**Q: Can I access Amazon ECR inside a VPC?**  
Yes. You can set up [AWS PrivateLink endpoints](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/vpc-endpoints.html) to <mark style="background: #FFF3A3A6;">allow your instances to pull images from your private repositories without traversing through the public internet</mark>.  

**Q: What’s the best way to manage my repositories and images?**  
Amazon ECR provides a [command line interface and APIs](http://aws.amazon.com/documentation/ecr/) to create, monitor, and delete repositories and set repository permissions. You can perform the same actions in the Amazon ECR console, which can be accessed via the “Repositories” section of the Amazon ECR console. Amazon ECR also integrates with the Docker CLI, allowing you to push, pull, and tag images on your development machine.

**Q: How do I publicly share an image using Amazon ECR?**

You publish an image to the Amazon ECR public gallery by signing into your AWS account and pushing to a public repository you create. You are assigned a unique alias per account to use in image URLs that identifies all public images that you publish.

**Q: Can I use a custom alias for my public images?**

Yes. You can request a custom alias such as your organization or project name, unless it’s a reserved alias. Names that identify AWS services are reserved. Names that identify AWS Marketplace sellers may also be reserved. We will review and approve your custom alias request within a few days unless your alias request violates the AWS Acceptable Use Policy or other AWS policies.  

**Q: How do I pull a public image from Amazon ECR?**

You pull using the familiar ‘docker pull’ command with the URL of the image. You can easily search for this URL by finding images using a publisher alias, image name, or image description using the Amazon ECR public gallery. Image URLs are in the format `public.ecr.aws/<alias>/<image>:<tag>`, for example public.ecr.aws/eks/aws-alb-ingress-controller:v1.1.5  

**Q: Does Amazon ECR replicate images across AWS Regions?**

Yes. Amazon ECR is designed to give you flexibility in where you store and how you deploy your images. <mark style="background: #CACFD9A6;">You can create deployment pipelines that build images, push them to Amazon ECR in one Region, and Amazon ECR can automatically replicate them to other Regions and accounts for deployment to multi-Region clusters</mark>.

**Q: Can I use Amazon ECR within local and on-premises environments?**  
Yes. You can access Amazon ECR anywhere that Docker runs such as desktops and on-premises environments.

**Q: Does the Amazon ECR public gallery provide AWS-published images?**  
Yes. Services such as Amazon EKS, Amazon SageMaker and AWS Lambda publish their official public use container images and artifacts to Amazon ECR.  

**Q: Does Amazon ECR work with Amazon ECS?**  
Yes. Amazon ECR is integrated with Amazon ECS, allowing you to easily store, run, and manage container images for applications running on Amazon ECS. All you need to do is specify the Amazon ECR repository in your task definition and Amazon ECS will retrieve the appropriate images for your applications.

**Q: Does Amazon ECR work with AWS Elastic Beanstalk?**  
Yes. AWS Elastic Beanstalk supports Amazon ECR for both [single and multi-container Docker environments](http://docs.aws.amazon.com/elasticbeanstalk/latest/dg/create_deploy_docker.container.console.html), allowing you to easily deploy container images stored in Amazon ECR with AWS Elastic Beanstalk. All you need to do is specify the Amazon ECR repository in your Dockerrun.aws.json configuration and attach the AmazonEC2ContainerRegistryReadOnly policy to your container instance role.

**Q: What version of Docker Engine does Amazon ECR support?**  
Amazon ECR currently supports Docker Engine 1.7.0 and up.

**Q: What version of the Docker Registry API does Amazon ECR support?**  
Amazon ECR supports the Docker Registry V2 API specification.

**Q: Will Amazon ECR automatically build images from a Dockerfile?**  
No. However, Amazon ECR integrates with a number of popular CI/CD solutions to provide this capability. See the [Amazon ECR Partners page](https://aws.amazon.com/what-are-containers/partners/) for more information.

**Q: Does Amazon ECR support federated access?**  
Yes. Amazon ECR is integrated with AWS Identity and Access Management (IAM), which supports [identity federation for delegated access](https://aws.amazon.com/identity/federation/) to the AWS Management Console or AWS APIs.

**Q: What version of the Docker Image Manifest specification does Amazon ECR support?**  
Amazon ECR supports the Docker Image Manifest V2, Schema 2 format. In order to maintain backwards compatibility with Schema 1 images, Amazon ECR will continue to accept images uploaded in the Schema 1 format. Additionally, Amazon ECR can down-translate from a Schema 2 to a Schema 1 image when pulling with an older version of Docker Engine (1.9 and below).

**Q: Does Amazon ECR support the Open Container Initiative (OCI) format?**  
Yes. Amazon ECR is compatible with the Open Container Initiative (OCI) image specification, letting you push and pull OCI images and artifacts. Amazon ECR can also translate between Docker Image Manifest V2, Schema 2 images and OCI images on pull.


[[Module 13 - Building Microservices and Serverless Architectures]]