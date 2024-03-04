---
tags:
  - cloud/labs
Status: 
Area:
---

Here is a linkedIn Post that my replace the CI/CD lab by understanding what its trying to say:  
[How to develop a secure CI/CD Pipeline in AWS](https://www.linkedin.com/feed/update/urn:li:activity:7125774983171072002/)  
Continuous integration and continuous delivery (CI/CD) pipelines are essential for modern software development. They automate the build, test, and deployment process, making it faster and more efficient to release new features and updates. However, CI/CD pipelines can also be a security risk if not properly implemented.  
  
Here are some tips for developing a secure CI/CD pipeline in AWS:  
1️⃣ Use a private source code repository. This will prevent unauthorized users from accessing your code. **AWS CodeCommit** is a good option for a private source code repository.  
2️⃣ Use least privilege permissions. Only grant the CI/CD pipeline the permissions it needs to function. This will help to reduce the attack surface of your pipeline.  
3️⃣ Use secrets management. Store sensitive information, such as passwords and API keys, in a **secrets manager.** This will prevent them from being exposed in the pipeline code or in plain text.  
4️⃣ Use security scanning tools. Use security scanning tools to scan your code for vulnerabilities before it is deployed. This will help to identify and fix security risks early on.  
5️⃣ Monitor your pipeline. Monitor your pipeline for suspicious activity. This will help you to detect and respond to security incidents quickly.  
  
Here are some additional tips for securing your CI/CD pipeline in AWS:  
📌 Use **AWS CodePipeline** to create your pipeline. AWS CodePipeline is a fully managed continuous delivery service that provides a secure and scalable way to build, test, and deploy your applications.  
📌 Use AWS CodeBuild to build your applications. AWS CodeBuild is a fully managed build service that provides a secure and scalable way to build your applications.  
📌 Use AWS CodeDeploy to deploy your applications. AWS CodeDeploy is a fully managed deployment service that provides a secure and scalable way to deploy your applications to Amazon Elastic Compute Cloud (Amazon EC2), Amazon Elastic Kubernetes Service (Amazon EKS), and AWS Lambda.  
📌 Use AWS Identity and Access Management (IAM) to control access to your pipeline. IAM allows you to create and manage users and groups, and to assign them permissions to your AWS resources.  
📌 Use AWS CloudTrail to audit your pipeline. CloudTrail is a fully managed auditing service that provides a record of all activity in your AWS account.  
Description: October Free Lab.  
This lab demonstrates how to build a fully managed continuous integration and continuous delivery (CI/CD) pipeline for applications that run on Amazon Elastic Container Service (Amazon ECS).  
You use [AWS CodePipeline] to model, orchestrate, and visualize a three-stage pipeline that deploys a containerized application using a [blue/green deployment strategy]. This strategy launches a new version of the application that runs alongside the old version and then slowly shifts traffic to the new version. Blue/green deployments are commonly employed when performing in-place application upgrades. Administrators can use these to validate new code while simultaneously running the old application version. If errors are detected in the new code, the deployment can be rolled back quickly and reliably.

When complete, your pipeline automatically builds a new container image whenever new code is pushed to your source repository and then uses [AWS CodeDeploy] and [Amazon ECS] to manage its deployment and shift traffic to it.



![](https://i.imgur.com/inBZCFt.jpg)



[Start Lab Here](#)  
In this lab, you use the following technology stack:

- AWS Cloud9
- AWS CodeBuild
- AWS CodeCommit
- AWS CodeDeploy
- AWS CodePipeline
- Amazon Elastic Container Registry (Amazon ECR)
- Amazon ECS

By the end of this lab, you will be able to do the following:
- Objective 1: Configure [**CodeCommit**] as a source control repository for an application.
- Objective 2: Create a [**CodeBuild**] project that uses a buildspec file to build a new Docker image and save it to **Amazon ECR** using an auditable and secure methodology.
- Objective 3: Create appspec.yaml and taskdef.json files that contain dynamic fields for use in blue/green deployments.
- Objective 4: Perform an in-place application upgrade using a blue/green deployment strategy configured in [**CodeDeploy**] and [**Amazon ECS**.]

>[!Missing]- Lab Expired  
>Missing Completion information. Because the lab stopped working

