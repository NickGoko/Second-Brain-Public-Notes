---
tags:
  - cloud/aws
---


# FAQ
## General

**Q: What is AWS CodeBuild?**

AWS CodeBuild is a fully managed continuous integration service in the cloud. CodeBuild compiles source code, runs tests, and produces packages that are ready to deploy. CodeBuild eliminates the need to provision, manage, and scale your own build servers. CodeBuild automatically scales up and down and processes multiple builds concurrently, so your builds don’t have to wait in a queue. You can get started quickly by using CodeBuild prepackaged build environments, or you can use custom build environments to use your own build tools. With CodeBuild, you only pay by the minute.  

[Show less](https://aws.amazon.com/codebuild/faqs/#)

**Q: Why should I use CodeBuild?**

Instead of having to set up, patch, and maintain the build server software yourself, you can use CodeBuild’s fully managed experience. You submit your build jobs to CodeBuild, and it runs them in temporary compute containers that are created fresh on every build and then discarded when finished. You don’t need to manage build server hardware or software. CodeBuild also automatically scales to meet your build volume. It immediately processes each build you submit and can run separate builds concurrently, meaning your builds are never left waiting in a queue.  

[Show less](https://aws.amazon.com/codebuild/faqs/#)

**Q: Can I use CodeBuild to automate my release process?**

Yes. CodeBuild is integrated with AWS CodePipeline. You can add a build action and set up a continuous integration and continuous delivery process that runs in the cloud. You can learn how to set up and monitor your builds from the CodePipeline console [here](https://docs.aws.amazon.com/codebuild/latest/userguide/how-to-create-pipeline.html).  

[Show less](https://aws.amazon.com/codebuild/faqs/#)

## Using CodeBuild

**Q: What is a build project?**

A build project is used to define how CodeBuild will run a build. It includes information such as where to get the source code, which build environment to use, the build commands to run, and where to store the build output. A build environment is the combination of operating system, programming language runtime, and tools used by CodeBuild to run a build.  

[Show less](https://aws.amazon.com/codebuild/faqs/#)

**Q: How do I configure a build project?**

A build project can be configured through the console or the AWS CLI. You specify the source repository location, the runtime environment, the build commands, the IAM role assumed by the container, and the compute class required to run the build. Optionally, you can specify build commands in a buildspec.yml file.  

[Show less](https://aws.amazon.com/codebuild/faqs/#)

**Q: Which source repositories does CodeBuild support?**

CodeBuild can connect to AWS CodeCommit, S3, GitHub, and GitHub Enterprise and Bitbucket to pull source code for builds.  

[Show less](https://aws.amazon.com/codebuild/faqs/#)

**Q: Which programming frameworks does CodeBuild support?**

CodeBuild provides preconfigured environments for supported versions of Java, Ruby, Python, Go, Node.js, Android, .NET Core, PHP, and Docker. You can also customize your own environment by creating a Docker image and uploading it to the Amazon EC2 Container Registry or the Docker Hub registry. You can then reference this custom image in your build project.  

[Show less](https://aws.amazon.com/codebuild/faqs/#)

**Q: Which preconfigured Windows build runtimes does CodeBuild provide?**

CodeBuild provides a preconfigured Windows build environment for .NET Core 2.0. We would like to provide a preconfigured build environment for Microsoft .NET Framework customers, many of whom already have a license to use the Microsoft proprietary libraries. However, Microsoft has been unwilling to work with us in addressing these customer requests at this time. You can customize your environment yourself to support other build targets, such as .NET Framework, by creating a Docker image and uploading it to the Amazon EC2 Container Registry or the Docker Hub registry. You can then reference this custom image in your build project.  

[Show less](https://aws.amazon.com/codebuild/faqs/#)

**Q: What happens when a build is run?**

CodeBuild will create a temporary compute container of the class defined in the build project, load it with the specified runtime environment, download the source code, execute the commands configured in the project, upload the generated artifact to an S3 bucket, and then destroy the compute container. During the build, CodeBuild will stream the build output to the service console and Amazon CloudWatch.  

[Show less](https://aws.amazon.com/codebuild/faqs/#)

**Q: Can I use CodeBuild with Jenkins?**

Yes. The [CodeBuild Plugin for Jenkins](https://github.com/awslabs/aws-codebuild-jenkins-plugin) can be used to integrate CodeBuild into Jenkins jobs. The build jobs are sent to CodeBuild, eliminating the need for provisioning and managing the Jenkins worker nodes.  

[Show less](https://aws.amazon.com/codebuild/faqs/#)

**Q: How can I view past build results?**

You can access your past build results through the console, CloudWatch, or the API. The results include outcome (success or failure), build duration, output artifact location, and log location. With the CodeBuild dashboard, you can view metrics to understand build behavior over time. The dashboard displays number of builds attempted, succeeded, and failed, as well as build duration. You can also visit the CloudWatch console to view more detailed build metrics. To learn more about monitoring CodeBuild with CloudWatch, visit our documentation.  

[Show less](https://aws.amazon.com/codebuild/faqs/#)

**Q: How can I debug a past build failure?**

You can debug a build by inspecting the detailed logs generated during the build run or you can use [CodeBuild Local](https://aws.amazon.com/blogs/devops/announcing-local-build-support-for-aws-codebuild/) to locally test and debug your builds.  

[Show less](https://aws.amazon.com/codebuild/faqs/#)

**Q: Why is build.general1.small not supported for .NET Core for Windows build environments?**

The .NET Core for Windows build environment requires more memory and processing power than is available in the build.general1.small compute instance type due to the size of the Windows Docker base container and additional libraries. Due to this limitation, there is no free tier for the .NET Core for Windows build environment.  

[Show less](https://aws.amazon.com/codebuild/faqs/#)

**Q: How do I receive notifications or alerts for any events in AWS CodeBuild?**

You can create notifications for events impacting your build projects. Notifications will come in the form of [Amazon SNS](https://aws.amazon.com/sns/) notifications. Each notification will include a status message as well as a link to the resources whose event generated that notification. Notifications has no additional cost; but, you may be charged for other AWS services utilized by notifications, such as Amazon SNS. To learn how to get started with notifications, see the [notifications user guide](https://docs.aws.amazon.com/codestar-notifications/latest/userguide/welcome.html). Additionally, customers using [AWS Chatbot](https://aws.amazon.com/chatbot/) can configure notifications to be sent to their Slack Channels or Amazon Chime chat rooms. For more details please check [here](https://docs.aws.amazon.com/codestar-notifications/latest/userguide/notifications-chatbot.html).  

[Show less](https://aws.amazon.com/codebuild/faqs/#)

## Security

**Q: Can I encrypt the build artifacts stored by CodeBuild?**

Yes. You can specify a key stored in the AWS Key Management Service (AWS KMS) to encrypt your artifacts.  

[Show less](https://aws.amazon.com/codebuild/faqs/#)

**Q: How does CodeBuild isolate builds that belong to other customers?**

CodeBuild runs your build in fresh environments isolated from other users and discards each build environment upon completion. CodeBuild provides security and separation at the infrastructure and execution levels.  

[Show less](https://aws.amazon.com/codebuild/faqs/#)

**Q: Can I use AWS Identity and Access Management (IAM) to manage access to CodeBuild?**

Yes. You can control access to your build projects through resource-level permissions in IAM policies.  

[Show less](https://aws.amazon.com/codebuild/faqs/#)

## Regions