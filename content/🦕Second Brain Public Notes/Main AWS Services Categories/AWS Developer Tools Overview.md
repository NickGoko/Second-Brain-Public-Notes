---
tags:
  - cloud/aws
---
With the AWS Developer Tools you can host your code, build, test, and deploy your application quickly and effectively. AWS provides a suite of tools including software development kits (SDKs), code editors, and continuous integration and delivery (CI/CD) services for DevOps software development.

## AWS CodeArtifact

AWS CodeArtifact is a fully managed artifact repository service.

You can use AWS CodeArtifact to securely store, publish, and share software packages.

CodeArtifact can be configured to automatically fetch software packages and dependencies from public artifact repositories.

CodeArtifact works with commonly used package managers and build tools like Maven, Gradle, npm, yarn, twine, pip, and NuGet making it easy to integrate into existing development workflows.

## AWS CodeCommit

AWS CodeCommit is a fully managed [**source control**](https://aws.amazon.com/devops/source-control/) service that hosts secure Git-based repositories.

Git is an Open Source distributed source control system:

- Centralized repository for all of your code, binaries, images, and libraries.
- Tracks and manages code changes.
- Maintains version history.
- Manages updates from multiple sources.
- Enables collaboration.

It makes it easy for teams to collaborate on code in a secure and highly scalable ecosystem.

CodeCommit eliminates the need to operate your own source control system or worry about scaling its infrastructure.

You can use CodeCommit to securely store anything from source code to binaries, and it works seamlessly with your existing Git tools.

Provides version control for version changes that happen over time.

You can easily commit, branch, and merge your code.

CodeCommit repositories are private.

CodeCommit scales seamlessly.

CodeCommit is integrated with Jenkins, CodeBuild and other CI tools.

CodeCommit is one of the AWS continuous integration tools (CodeBuild compiles and test code):

![AWS CodeCommit](https://digitalcloud.training/wp-content/uploads/2022/02/Screen-Shot-2022-02-03-at-3.56.49-PM-1024x495.png)

### Encryption

You can transfer your files to and from AWS CodeCommit using HTTPS or SSH.

Repositories are automatically encrypted at rest through AWS Key Management Service (AWS KMS) using customer-specific keys.

### Authentication and Access Control

AWS CodeCommit uses AWS Identity and Access Management to control and monitor who can access data as well as how, when, and where they can access it.

CodeCommit also helps monitor your repositories via AWS CloudTrail and AWS CloudWatch.

Authentication

You need to configure your Git client to communicate with CodeCommit repositories.

As part of this configuration, you provide IAM credentials that CodeCommit can use to authenticate you.

IAM supports CodeCommit with three types of credentials:

- Git credentials, an IAM -generated user name and password pair you can use to communicate with CodeCommit repositories over HTTPS.
- SSH keys, a locally generated public-private key pair that you can associate with your IAM user to communicate with CodeCommit repositories over SSH.
- [**AWS access keys**](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html), which you can use with the credential helper included with the AWS CLI to communicate with CodeCommit repositories over HTTPS.

### Authorization

IAM policies for authorizing access for users/roles to repositories.

CodeCommit only supports identity-based policies, not resource-based policies.

You can attach tags to CodeCommit resources or pass tags in a request to CodeCommit.

To control access based on tags, you provide tag information in the [**condition element**](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_elements_condition.html) of a policy using the codecommit:ResourceTag/key-name, aws:RequestTag/key-name, or aws:TagKeys condition keys.

### Notifications

You can trigger notifications in CodeCommit using AWS SNS or AWS Lambda or AWS CloudWatch Event rules.

Notifications are in relation to pull request and comment events – triggers are related to pushing to a branch or creating / deleting a branch.

Use cases for notifications SNS / AWS Lambda:

- Deletion of branches.
- Trigger for pushes that happen in the master branch.
- Notify external build system.
- Trigger AWS Lambda function to perform codebase analysis.

Use cases for CloudWatch Event Rules:

- Trigger for pull request updates (created / updated / deleted / commented).
- Commit comment events.
- CloudWatch Event Rules go into an SNS Topic.

## AWS CodeBuild

AWS CodeBuild is a fully managed continuous integration (CI) service that compiles source code, runs tests, and produces software packages that are ready to deploy.

With CodeBuild, you don’t need to provision, manage, and scale your own build servers.

CodeBuild scales continuously and processes multiple builds concurrently, so your builds are not left waiting in a queue.

CodeBuild is an alternative to other build tools such as Jenkins.

CodeBuild scales continuously and processes multiple builds concurrently.

You pay based on the time it takes to complete the builds.

AWS CodeBuild runs your builds in preconfigured build environments that contain the operating system, programming language runtime, and build tools (e.g., Apache Maven, Gradle, npm) required to complete the task.

It is possible to extend capabilities by leveraging your own Docker images.

CodeBuild is integrated with KMS for encryption of build artifacts, IAM for build permissions, VPC for network security, and CloudTrail for logging API calls.

CodeBuild takes source code from GitHub, CodeCommit, CodePipleine, S3 etc.

Build instructions can be defined in the code (buildspec.yml).

Output logs can be sent to Amazon S3 & AWS CloudWatch Logs.

There are metrics to monitor CodeBuild statistics.

You can use CloudWatch alarms to detect failed builds and trigger SNS notifications.

Builds can be defined within CodePipeline or CodeBuild itself.

### Benefits of CodeBuild

Fully managed by AWS.

On-demand and scales seamlessly.

Pre-configured environments for many programming languages.

### CodeBuild Concepts

**Build project** – defines how CodeBuild will run a build defines settings including:

- Location of the source code.
- The build environment to use.
- The build commands to run.
- Where to store the output of the build.

**Build environment** – the operating system, language runtime, and tools that CodeBuild uses for the build.

**Build Specification** – a YAML file that describes the collection of commands and settings for CodeBuild to run a build.

### Preconfigured Build Environments

AWS CodeBuild provides build environments for Java, Python, Node.js, Ruby, Go, Android, .NET Core for Linux, and Docker.

### Customized Build Environments

You can bring your own build environments to use with AWS CodeBuild, such as for the Microsoft .NET Framework.

You can package the runtime and tools for your build into a Docker image and upload it to a public [**Docker**](https://aws.amazon.com/docker/) Hub repository or [**Amazon EC2 Container Registry**](https://aws.amazon.com/ecr/) (Amazon ECR).

When you create a new build project, you can specify the location of your Docker image, and CodeBuild will pull the image and use it as the build project configuration.

### Specifying Build Commands

You can define the specific commands that you want AWS CodeBuild to perform, such as installing build tool packages, running unit tests, and packaging your code.

The build specification is a YAML file that lets you choose the commands to run at each phase of the build and other settings.

You can override the default buildspec file name and location.

CodeBuild helps you get started quickly with sample build specification files for common scenarios, such as builds using Apache Maven, Gradle, or npm.

The code sample shows the contents of a buildspec.yml file that is being used to build a Docker image and push it to Amazon Elastic Container Registry (ECR):

version: 0.2

phases:

install:

runtime-versions:

docker: 18

pre_build:

commands:

- echo Logging in to Amazon ECR...

- $(aws ecr get-login --no-include-email --region $AWS_DEFAULT_REGION)

build:

commands:

- echo Build started on `date`

- echo Building the Docker image...

- docker build -t $IMAGE_REPO_NAME:$IMAGE_TAG .

- docker tag $IMAGE_REPO_NAME:$IMAGE_TAG $AWS_ACCOUNT_ID.dkr.ecr.$AWS_DEFAULT_REGION.amazonaws.com/$IMAGE_REPO_NAME:$IMAGE_TAG

post_build:

commands:

- echo Build completed on `date`

- echo Pushing the Docker image...

- docker push $AWS_ACCOUNT_ID.dkr.ecr.$AWS_DEFAULT_REGION.amazonaws.com/$IMAGE_REPO_NAME:$IMAGE_TAG

**_Exam tip:_** _You must have a buildspec.yml file at the root of your source code._

You can define environment variables:

- Plaintext variables.
- Secure secrets using the SSM Parameter store.

Phases:

- Install: install dependencies you may need for the build.
- Pre-build: final commands to execute before build.
- Build: actual build commands.
- Post build: finishing touches (e.g. zip file output).

Artifacts: these get uploaded to S3 (encrypted with KMS).

Cache: files to cache (usually dependencies) to S3 for future builds.

### CodeBuild Local Build

In case you need to do deep troubleshooting beyond analyzing log files.

Can run CodeBuild locally on your computer using Docker.

Leverages the CodeBuild agent.

## AWS CodeDeploy

CodeDeploy is a deployment service that automates application deployments to Amazon EC2 instances, on-premises instances, serverless Lambda functions, or Amazon ECS services.

You can deploy a nearly unlimited variety of application content, including:

- Serverless AWS Lambda functions.
- Web and configuration files.
- Executables.
- Packages.
- Scripts.
- Multimedia files.

CodeDeploy can deploy application content that runs on a server and is stored in Amazon S3 buckets, GitHub repositories, or Bitbucket repositories.

CodeDeploy can also deploy a serverless Lambda function.

You do not need to make changes to your existing code before you can use CodeDeploy.

Can be used to automatically deploy applications to many EC2 instances.

Similar open source tools include Ansible, Terraform, Chef, Puppet etc.

Integrates with various CI/CD tools including Jenkins, GitHub, Atlassian, AWS CodePipeline as well as config management tools like Ansible, Puppet and Chef.

CodeDeploy is a fully managed service.

There’s lots of flexibility to define any kind of deployment.

CodeDeploy can be connected to CodePipeline and use artifacts from there.

CodeDeploy can use re-use existing setup tools, works with any application, auto scaling integration.

### CodeDeploy Application

An AWS CodeDeploy application contains information about what to deploy and how to deploy it.

Need to choose the compute platform:

- EC2/On-premises.
- AWS Lambda.
- Amazon ECS.

EC2/On-Premises:

- Amazon EC2 cloud instances, on-premises servers, or both.
- Deployments that use the EC2/On-Premises compute platform manage the way in which traffic is directed to instances by using an in-place or blue/green deployment type.

![CodeDeploy EC2 on-premises](https://digitalcloud.training/wp-content/uploads/2022/02/Screen-Shot-2022-02-03-at-4.00.02-PM-300x117.png)

AWS Lambda:

- Used to deploy applications that consist of an updated version of a Lambda function.
- You can manage the way in which traffic is shifted to the updated Lambda function versions during a deployment by choosing a canary, linear, or all-at-once configuration.

![CodeDeploy traffic shifting lambda](https://digitalcloud.training/wp-content/uploads/2022/02/Screen-Shot-2022-02-03-at-4.01.34-PM-300x129.png)

Amazon ECS:

- Used to deploy an Amazon ECS containerized application as a task set.
- CodeDeploy performs a blue/green deployment by installing an updated version of the application as a new replacement task set.
- CodeDeploy reroutes production traffic from the original application task set to the replacement task set.
- The original task set is terminated after a successful deployment.
- You can manage the way in which traffic is shifted to the updated task set during a deployment by choosing a canary, linear, or all-at-once configuration.

![CodeDeploy ECS](https://digitalcloud.training/wp-content/uploads/2022/02/Screen-Shot-2022-02-03-at-4.02.33-PM-300x176.png)

Deployment Group

Each deployment group belongs to one application and specifies:

- A deployment configuration – a set of deployment rules as well as success / failure conditions used during a deployment.
- Notifications configuration for deployment events.
- Amazon CloudWatch alarms to monitor a deployment.
- Deployment rollback configuration.

Deployment Type

CodeDeploy provides two deployment type options – in-place and blue/green.

![CodeDeploy deployment type](https://digitalcloud.training/wp-content/uploads/2022/02/Screen-Shot-2022-02-03-at-4.03.51-PM-300x92.png)

In-place deployment:

- The application on each instance in the deployment group is stopped, the latest application revision is installed, and the new version of the application is started and validated.
- You can use a load balancer so that each instance is deregistered during its deployment and then restored to service after the deployment is complete.
- Only deployments that use the EC2/On-Premises compute platform can use in-place deployments.

**_Exam tip:_** _AWS Lambda and Amazon ECS deployments cannot use an in-place deployment type._

Blue/green on an EC2/On-Premises compute platform:

- The instances in a deployment group (the original environment) are replaced by a different set of instances (the replacement environment) using these steps:
    - Instances are provisioned for the replacement environment.
    - The latest application revision is installed on the replacement instances.
    - An optional wait time occurs for activities such as application testing and system verification.
    - Instances in the replacement environment are registered with an Elastic Load Balancing load balancer, causing traffic to be rerouted to them.
    - Instances in the original environment are deregistered and can be terminated or kept running for other uses.

**_Note:_** _If you use an EC2/On-Premises compute platform, be aware that blue/green deployments work with Amazon EC2 instances only._

Blue/green on an AWS Lambda compute platform:

- Traffic is shifted from your current serverless environment to one with your updated Lambda function versions.
- You can specify Lambda functions that perform validation tests and choose the way in which the traffic shifting occurs.
- All AWS Lambda compute platform deployments are blue/green deployments.
- For this reason, you do not need to specify a deployment type.

Blue/green on an Amazon ECS compute platform:

- Traffic is shifted from the task set with the original version of an application in an Amazon ECS service to a replacement task set in the same service.
- You can set the traffic shifting to linear or canary through the deployment configuration.
- The protocol and port of a specified load balancer listener is used to reroute production traffic.
- During a deployment, a test listener can be used to serve traffic to the replacement task set while validation tests are run.

Deployment on Amazon EC2:

EC2 instances are identified by CodeDeploy by using tags or an Auto Scaling Group name.

![Auto Scaling Tags](https://digitalcloud.training/wp-content/uploads/2022/02/Screen-Shot-2022-02-03-at-4.04.53-PM-300x181.png)

Each Amazon EC2 instance must have the correct IAM instance profile attached.

The CodeDeploy agent must be installed and running on each instance.

The agent continuously polls for work to do.

CodeDeploy sends the appspec.yml file (which must be at the root of your source code).

The application code is pulled from GitHub or S3.

EC2 will run the deployment instructions.

CodeDeploy agent will report of success / failure of deployment on the instance.

EC2 instances are grouped by deployment group (e.g. dev, test, prod).

**Note:** CodeDeploy does not provision the resources – it deploys applications not EC2 instances.

### AppSpec File

The application specification file (AppSpec file) is a [**YAML**](http://www.yaml.org/)-formatted, or JSON-formatted file used by CodeDeploy to manage a deployment.

The AppSpec file defines the deployment actions you want AWS CodeDeploy to execute.

The name of the AppSpec file for an EC2/On-Premises deployment must be appspec.yml. The name of the AppSpec file for an Amazon ECS or AWS Lambda deployment must be appspec.yaml or appspec.yml.

The following code sample shows the format of an appspec.yml file for an Amazon EC2 instance with WordPress:

version: 0.0

os: linux

files:

- source: /

destination: /var/www/html/WordPress

hooks 

BeforeInstall:

- location: scripts/install_dependencies.sh

timeout: 300

runas: root

AfterInstall:

- location: scripts/change_permissions.sh

timeout: 300

runas: root

ApplicationStart:

- location: scripts/start_server.sh

- location: scripts/create_test_db.sh

timeout: 300

runas: root

ApplicationStop:

- location: scripts/stop_server.sh

timeout: 300

runas: root

The _files_ section specifies how to source and copy from S3 / GitHub to the filesystem.

_hooks_ are a set of instructions to be run to deploy the new version (hooks have timeouts).

### AppSpec.yaml For ECS

The Amazon ECS task definition file must be specified with its ARN in the TaskDefinition instruction in the AppSpec file.

The container and port in your replacement task set where your Application Load Balancer or Network Load Balancer reroutes traffic during a deployment must be specified with the LoadBalancerInfo instruction in the AppSpec file.

Here is an example of an AppSpec file written in YAML for deploying an Amazon ECS service

version: 0.0

Resources:

- TargetService:

Type: AWS::ECS::Service

Properties:

TaskDefinition: "arn:aws:ecs:us-east-1:111222333444:task-definition/my-task-definition-family-name:1"

LoadBalancerInfo:

ContainerName: "SampleApplicationName"

ContainerPort: 80

# Optional Properties

PlatformVersion: "LATEST"

NetworkConfiguration:

AwsvpcConfiguration:

Subnets: ["subnet-1234abcd","subnet-5678abcd"]

SecurityGroups: ["sg-12345678"]

AssignPublicIp: "ENABLED"

Hooks:

- BeforeInstall: "LambdaFunctionToValidateBeforeInstall"

- AfterInstall: "LambdaFunctionToValidateAfterTraffic"

- AfterAllowTestTraffic: "LambdaFunctionToValidateAfterTestTrafficStarts"

- BeforeAllowTraffic: "LambdaFunctionToValidateBeforeAllowingProductionTraffic"

- AfterAllowTraffic: "LambdaFunctionToValidateAfterAllowingProductionTraffic"

**_Note:_** _The hooks are different for each type of compute platform and not all available hooks are shown. For more information on the available hooks for each compute platform please read the AWS documentation_ [**_here_**](https://docs.aws.amazon.com/codedeploy/latest/userguide/reference-appspec-file-structure-hooks.html)_._

### AppSpec.yaml For AWS Lambda

The format of the AppSpec.yaml file for use with AWS Lambda is as follows:

version: 0.0

Resources:

- myLambdaFunction:

Type: AWS::Lambda::Function

Properties:

Name: "myLambdaFunction"

Alias: "myLambdaFunctionAlias"

CurrentVersion: "1"

TargetVersion: "2"

Hooks:

- BeforeAllowTraffic: "LambdaFunctionToValidateBeforeTrafficShift"

- AfterAllowTraffic: "LambdaFunctionToValidateAfterTrafficShift"

The following hooks are available for use:

- BeforeAllowTraffic – used to specify the tasks or functions you want to run before traffic is routed to the newly deployed Lambda function.
- AfterAllowTraffic – used to specify the tasks or functions you want to run after the traffic has been routed to the newly deployed Lambda function.

### Revision

When updating to a new version a Revision includes everything needed to deploy the new version: AppSpec file, application files, executables, and config files.

### In-place Deployment (EC2 only)

Here’s how it works:

1. First, you create deployable content on your local development machine or similar environment, and then you add an application specification file (AppSpec file). The AppSpec file is unique to CodeDeploy. It defines the deployment actions you want CodeDeploy to execute. You bundle your deployable content and the AppSpec file into an archive file, and then upload it to an Amazon S3 bucket or a GitHub repository. This archive file is called an application revision (or simply a revision).
2. Next, you provide CodeDeploy with information about your deployment, such as which Amazon S3 bucket or GitHub repository to pull the revision from and to which set of Amazon EC2 instances to deploy its contents. CodeDeploy calls a set of Amazon EC2 instances a deployment group. A deployment group contains individually tagged Amazon EC2 instances, Amazon EC2 instances in Amazon EC2 Auto Scaling groups, or both.  
    Each time you successfully upload a new application revision that you want to deploy to the deployment group, that bundle is set as the target revision for the deployment group. In other words, the application revision that is currently targeted for deployment is the target revision. This is also the revision that is pulled for automatic deployments.
3. Next, the CodeDeploy agent on each instance polls CodeDeploy to determine what and when to pull from the specified Amazon S3 bucket or GitHub repository.
4. Finally, the CodeDeploy agent on each instance pulls the target revision from the Amazon S3 bucket or GitHub repository and, using the instructions in the AppSpec file, deploys the contents to the instance.

CodeDeploy keeps a record of your deployments so that you can get deployment status, deployment configuration parameters, instance health, and so on.

### Blue/green Deployments

A blue/green deployment is used to update your applications while minimizing interruptions caused by the changes of a new application version. CodeDeploy provisions your new application version alongside the old version before rerouting your production traffic.

**AWS Lambda:** Traffic is shifted from one version of a Lambda function to a new version of the same Lambda function.

**Amazon ECS:** Traffic is shifted from a task set in your Amazon ECS service to an updated, replacement task set in the same Amazon ECS service.

**EC2/On-Premises:** Traffic is shifted from one set of instances in the original environment to a replacement set of instances.

**_Note:_** _All AWS Lambda and Amazon ECS deployments are blue/green. An EC2/On-Premises deployment can be in-place or blue/green._

For Amazon ECS and AWS Lambda there are three ways traffic can be shifted during a deployment:

- Canary: Traffic is shifted in two increments. You can choose from predefined canary options that specify the percentage of traffic shifted to your updated Amazon ECS task set / Lambda function in the first increment and the interval, in minutes, before the remaining traffic is shifted in the second increment.
- Linear: Traffic is shifted in equal increments with an equal number of minutes between each increment. You can choose from predefined linear options that specify the percentage of traffic shifted in each increment and the number of minutes between each increment.
- All-at-once: All traffic is shifted from the original Amazon ECS task set /  Lambda function to the updated Amazon ECS task set / Lambda function all at once.

For Amazon EC2 you can choose how your replacement environment is specified:

**Copy an existing Amazon EC2 Auto Scaling group:**

- During the blue/green deployment, CodeDeploy creates the instances for your replacement environment during the deployment.
- With this option, CodeDeploy uses the Amazon EC2 Auto Scaling group you specify as a template for the replacement environment, including the same number of running instances and many other configuration options.

**Choose instances manually:**

- You can specify the instances to be counted as your replacement using Amazon EC2 instance tags, Amazon EC2 Auto Scaling group names, or both.
- If you choose this option, you do not need to specify the instances for the replacement environment until you create a deployment.

## AWS CodePipeline

AWS CodePipeline is a fully managed continuous delivery service that helps you automate your release pipelines for fast and reliable application and infrastructure updates.

CodePipeline automates the build, test, and deploy phases of your release process every time there is a code change, based on the release model you define.

CodePipeline enables you to deliver features and updates rapidly and reliably.

You can easily integrate AWS CodePipeline with third-party services such as GitHub or with your own custom plugin. With AWS CodePipeline, you only pay for what you use.

There are no upfront fees or long-term commitments.

Uses a user-defined software release process.

A fast and reliable way to quickly release new features and bug fixes.

CodePipeline provides tooling integrations for many AWS and third-party software at each stage of the pipeline including:

- Source stage – S3, CodeCommit, Github, ECR, Bitbucket Cloud (beta).
- Build – CodeBuild, Jenkins.
- Deploy stage – CloudFormation, CodeDeploy, ECS, Elastic Beanstalk, AWS Service Catalog, S3.

![aws codepipeline](https://digitalcloud.training/wp-content/uploads/2022/02/Screen-Shot-2022-02-03-at-4.06.33-PM-300x157.png)

### Key CodePipeline Concepts

Pipelines:

- A workflow that describes how software changes go through the release process.

Artifacts:

- Files or changes that will be worked on by the actions and stages in the pipeline.
- Each pipeline stage can create “artifacts”.
- Artifacts are passed, stored in Amazon S3, and then passed on to the next stage.

Stages:

- Pipelines are broken up into stages, e.g., build stage, deployment stage.
- Each stage can have sequential actions and or parallel actions.
- Stage examples would be build, test, deploy, load test etc.
- Manual approval can be defined at any stage.

Actions:

- Stages contain at least one action, these actions take some action on artifacts and will have artifacts as either an input, and output, or both.

Transitions:

- The progressing from one stage to another inside of a pipeline.

The diagram below shows a pipeline with a manual approval stage:

![aws codepipeline approval](https://digitalcloud.training/wp-content/uploads/2022/02/Screen-Shot-2022-02-03-at-4.07.35-PM-300x152.png)

Every code change pushed to your code repository automatically enters the workflow and triggers the set of actions defined for each stage of the pipeline.

CodePipeline state changes happen in AWS CloudWatch Events which can create SNS notifications.

Notifications may include failed pipelines or cancelled stages.

If CodePipeline fails a stage, your pipeline stops and you can get information in the console.

You can also audit API calls with AWS CloudTrail.

If CodePipeline cannot perform an action, check that the IAM service role attached to the pipeline has the correct permissions.

## AWS CodeStar

AWS CodeStar enables you to quickly develop, build, and deploy applications on AWS. AWS CodeStar provides a unified user interface, enabling you to easily manage your software development activities in one place.

With AWS CodeStar, you can set up your entire [**continuous delivery**](https://aws.amazon.com/devops/continuous-delivery/) toolchain in minutes, allowing you to start releasing code faster.

AWS CodeStar makes it easy for your whole team to work together securely, allowing you to easily manage access and add owners, contributors, and viewers to your projects.

Each AWS CodeStar project comes with a project management dashboard, including an integrated issue tracking capability powered by Atlassian JIRA Software.

With the AWS CodeStar project dashboard, you can easily track progress across your entire software development process, from your backlog of work items to teams’ recent code deployments.

**Exam tip:** If an exam scenario requires a unified development toolchain, and mentions collaboration between team members, synchronization, and centralized management of the CI/CD pipeline this will be CodeStar rather than CodePipeline or CodeCommit.

![aws codestar](https://digitalcloud.training/wp-content/uploads/2022/02/Screen-Shot-2022-02-03-at-4.08.39-PM-300x205.png)

### Benefits and Features

Project templates for various projects and programming languages:

- With AWS CodeStar project templates, you can easily develop a variety of applications including websites, web applications, web services, and Alexa skills.
- AWS CodeStar project templates include the code for getting started on supported programming languages including Java, JavaScript, PHP, Ruby, and Python.

Work across your team securely:

- AWS CodeStar enables you to collaborate across your team in a secure manner.
- AWS CodeStar simplifies the process of setting up project access for teams because it provides built-in role-based policies that follow AWS security best practices.
- You can easily manage access for project owners, contributors, and viewers without needing to manually configure your own policy for each service.

Support for multiple Integrated Development Environments (IDEs):

- Integrates natively with the AWS Cloud9 cloud-based IDE.
- Can also choose from a number of popular IDEs such as Microsoft Visual Studio and Eclipse.

CodeStar integrates with several other AWS services including:

- CodeCommit.
- CodeBuild.
- CodeDeploy.
- CodePipeline.
- CloudWatch.

### Pricing

There is no additional charge for AWS CodeStar.

You pay for AWS resources (e.g. EC2 instances, Lambda executions or S3 buckets) used to in your CodeStar projects.

You only pay for what you use, as you use it; there are no minimum fees and no upfront commitments.

## AWS Cloud9

AWS Cloud9 is a cloud-based integrated development environment (IDE) that lets you write, run, and debug your code with just a browser.

It includes a code editor, debugger, and terminal.

Cloud9 comes prepackaged with essential tools for popular programming languages, including JavaScript, Python, PHP, and more, so you don’t need to install files or configure your development machine to start new projects.

Since your Cloud9 IDE is cloud-based, you can work on your projects from your office, home, or anywhere using an internet-connected machine.

Cloud9 also provides a seamless experience for developing serverless applications enabling you to easily define resources, debug, and switch between local and remote execution of serverless applications.

With Cloud9, you can quickly share your development environment with your team, enabling you to pair program and track each other’s inputs in real time.

### Benefits and Features

Code with just a browser:

- AWS Cloud9 gives you the flexibility to run your development environment on a managed Amazon EC2 instance or any existing Linux server that supports SSH.
- This means that you can write, run, and debug applications with just a browser, without needing to install or maintain a local IDE.
- The Cloud9 code editor and integrated debugger include helpful, time-saving features such as code hinting, code completion, and step-through debugging.
- The Cloud9 terminal provides a browser-based shell experience enabling you to install additional software, do a git push, or enter commands.

Code together in real-time:

- AWS Cloud9 makes collaborating on code easy.
- You can share your development environment with your team in just a few clicks and pair program together.
- While collaborating, your team members can see each other type in real time, and instantly chat with one another from within the IDE.

Build serverless applications with ease:

- AWS Cloud9 makes it easy to write, run, and debug serverless applications.
- It preconfigures the development environment with all the SDKs, libraries, and plug-ins needed for serverless development.
- Cloud9 also provides an environment for locally testing and debugging AWS Lambda functions.
- This allows you to iterate on your code directly, saving you time and improving the quality of your code.

Direct terminal access to AWS:

- AWS Cloud9 comes with a terminal that includes sudo privileges to the managed Amazon EC2 instance that is hosting your development environment and a preauthenticated AWS Command Line Interface.
- This makes it easy for you to quickly run commands and directly access AWS services.

Start new projects quickly:

- AWS Cloud9 makes it easy for you to start new projects.
- Cloud9’s development environment comes prepackaged with tooling for over 40 programming languages, including Node.js, JavaScript, Python, PHP, Ruby, Go, and C++.
- This enables you to start writing code for popular application stacks within minutes by eliminating the need to install or configure files, SDKs, and plug-ins for your development machine.
- Because Cloud9 is cloud-based, you can easily maintain multiple development environments to isolate your project’s resources.

## Amazon CodeGuru

Amazon CodeGuru provides intelligent recommendations to improve code quality and identify an application’s most expensive lines of code.

You can integrate CodeGuru into existing software development workflows to automate code reviews.

CodeGuru continuously monitors an application’s performance in production.

Provides recommendations and on how to improve code quality, application performance, and reduce overall cost.

### Security Detection

CodeGuru can detect many security issues such as:

1. OWASP Top 10: checks for top web application security risks such as broken access control, injection, and data integrity failures
2. AWS API security best practices: check API security for Amazon Elastic Compute Cloud and AWS Key Management Service
3. AWS security best practices (AWS crypto is implemented to Amazon’s standards): apply Amazon’s internal security expertise to your code
4.  Java crypto library best practices: check if Javax.Crypto.Cipher is initialized and called correctly
5. Python crypto library best practices: check if correct versions of Python hashing and cryptography algorithms are used
6. Secure web applications: check app-related security issues, such as LDAP injections
7. Sensitive information leaks: check for any leakage of personal or sensitive information (example: logging AWS account credentials in plain text)
8. Input validation: checks for malformed or malicious data from untrusted sources

### Secrets Detection

CodeGuru provides secrets detection for detecting secrets that are hardcoded in cod repositories or configuration files.

Can detect API keys, passwords, SSH keys, access token, database connections strings and more.

### Code Quality

CodeGuru Reviewer identifies quality issues in your code.

Ensures best practices are followed such as correct use of AWS APIs.

Provides best practice detection for programming languages such as Java and Python.

## AWS X-Ray

AWS X-Ray helps developers analyze and debug production, distributed applications, such as those built using a microservices architecture.

With X-Ray, you can understand how your application and its underlying services are performing to identify and troubleshoot the root cause of performance issues and errors.

X-Ray provides an end-to-end view of requests as they travel through your application and shows a map of your application’s underlying components.

![aws x-ray](https://digitalcloud.training/wp-content/uploads/2022/02/Screen-Shot-2022-02-03-at-4.09.53-PM-300x205.png)

You can use X-Ray to analyze both applications in development and in production, from simple three-tier applications to complex microservices applications consisting of thousands of services.

AWS X-Ray supports applications running on:

- Amazon Elastic Compute Cloud (Amazon EC2).
- Amazon EC2 Container Service (Amazon ECS).
- AWS Lambda.
- AWS Elastic Beanstalk.

X-Ray on EC2 / On-premises:

- Linux system must run the X-Ray daemon.
- IAM instance role if EC2, other AWS credentials on on-premises instance.

X-Ray on Lambda:

- Make sure the X-Ray integration is ticked in the Lambda configuration (Lambda will run the daemon).
- IAM role is the Lambda role.

X-Ray on Elastic Beanstalk:

- Set configuration in the Elastic Beanstalk console.
- Or use the Beanstalk extension (.ebextensions/xray-daemon.config)

X-Ray on ECS/EKS/Fargate:

- Create a Docker image that runs the daemon or use the official X-Ray Docker image.
- Ensure port mappings and network settings are correct and IAM task roles are defined.

The X-Ray SDK captures metadata for requests made to MySQL and PostgreSQL databases (self-hosted, Amazon RDS, Amazon Aurora), and Amazon DynamoDB.

It also captures metadata for requests made to Amazon Simple Queue Service and Amazon Simple Notification Service.

The X-Ray SDK is installed in your application and forwards to the X-Ray daemon which forwards to the X-Ray API.

You can then visualize what is happening in the X-Ray console.

The X-Ray SDK provides:

- Interceptors to add your code to trace incoming HTTP requests.
- Client handlers to instrument AWS SDK client that your application uses to call other AWS services.
- An HTTP client to use to instrument calls to other internal and external HTTP web services.

![x-ray instrument](https://digitalcloud.training/wp-content/uploads/2022/02/Screen-Shot-2022-02-03-at-4.11.13-PM-300x190.png)

AWS X-Ray supports tracing for applications that are written in Node.js, Java, and .NET.

Code must be instrumented to use the AWS X-Ray SDK.

The IAM role must be correct to send traces to X-Ray.

The X-Ray daemon agent has a config to send traces cross account:

- Make sure the IAM permissions are correct – the agent will assume a role.
- This allows to have a central account for all your application tracing.

### Key X-Ray Terminology

Trace:

- An X-Ray trace is a set of data points that share the same trace ID.

Segments:

- An X-Ray segment encapsulates all the data points for a single component (for example, authorization service) of the distributed application.
- Segments include system-defined and user-defined data in the form of annotations and are composed of one or more sub-segments that represent remote calls made from the service.

Subsegments:

- Subsegments provide more granular timing information and details about downstream calls that your application made to fulfill the original request.
- A subsegment can contain additional details about a call to an AWS service, an external HTTP API, or an SQL database.
- You can even define arbitrary subsegments to instrument specific functions or lines of code in your application.
- For services that don’t send their own segments, like Amazon DynamoDB, X-Ray uses subsegments to generate inferred segments and downstream nodes on the service map.
- This lets you see all your downstream dependencies, even if they don’t support tracing, or are external.

Annotations:

- An X-Ray annotation is system-defined, or user-defined data associated with a segment.
- System-defined annotations include data added to the segment by AWS services, whereas user-defined annotations are metadata added to a segment by a developer.
- A segment can contain multiple annotations.
- These are key / value pairs used to index traces and use with filters.
- Use annotations to record information on segments or subsegments that you want indexed for search.

Sampling:

- To provide a performant and cost-effective experience, X-Ray does not collect data for every request that is sent to an application.
- Instead, it collects data for a statistically significant number of requests.
- X-Ray should not be used as an audit or compliance tool because it does not guarantee data completeness.

Metadata:

- Key / value pairs, not indexed and not used for searching.

**_Exam tip:_** _Remember that annotations can be used for adding system or user-defined data to segments and subsegments that you want to index for search. Metadata is not indexed and cannot be used for searching._

### Annotations and Filtering

AWS X-Ray lets you add annotations to data emitted from specific components or services in your application.

You can use this to append business-specific metadata that help you better diagnose issues.

You can also view and filter data for traces by properties such as annotation value, average latencies, HTTP response status, timestamp, database table used, and more.

### X-Ray SDK

The X-Ray SDK is installed in your application and forwards to the X-Ray daemon which forwards to the X-Ray API.

You can then visualize what is happening in the X-Ray console.

The X-Ray SDK provides:

- Interceptors to add your code to trace incoming HTTP requests.
- Client handlers to instrument AWS SDK client that your application uses to call other AWS services.
- An HTTP client to use to instrument calls to other internal and external HTTP web services.

Code must be instrumented to use the AWS X-Ray SDK.

The IAM role must be correct to send traces to X-Ray.

## AWS Fault Injection Simulator

AWS Fault Injection Simulator is a fully managed service for running fault injection experiments on AWS.

Makes it easier to improve an application’s performance, observability, and resiliency.

Fault injection experiments are used in chaos engineering, which is the practice of stressing an application in testing or production environments by creating disruptive events.

Fault injection experiment helps teams create the real-world conditions needed to uncover the hidden bugs, monitoring blind spots, and performance bottlenecks that are difficult to find in distributed systems.