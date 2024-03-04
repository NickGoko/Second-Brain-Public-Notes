---
tags:
  - cloud/aws
---
## I. What is AWS SAM?

The **AWS Serverless Application Model (AWS SAM)** is <mark style="background: #D2B3FFA6;">**an open-source framework designed to streamline the building and deployment of serverless applications on AWS**.</mark>  
By simplifying the process of creating and managing resources, it significantly reduces the complexity usually associated with traditional architectures.

### A. SAM Templates
<mark style="background: #BBFABBA6;">These are configuration files, written in YAML or JSON, that specify the resources used in your AWS serverless application.</mark>  
<mark style="background: #FF5582A6;">They are an extension of AWS CloudFormation templates, providing a simplified syntax for defining serverless resources such as Lambda functions, API Gateway APIs, and DynamoDB tables.</mark>

### B. SAM Command Line Interface (CLI)

The SAM CLI is a vital tool for local development and testing of serverless applications. It provides commands for all phases of the development lifecycle, from debugging your application locally to deploying your code in the AWS cloud.

Beyond its basic function, AWS SAM offers a shorthand syntax to express functions, APIs, databases, and event source mappings. This feature empowers developers to define and model their applications using just a few lines per resource in YAML format.

During deployment, SAM seamlessly transforms and expands this syntax into AWS CloudFormation syntax, facilitating faster and more efficient construction of serverless applications. Additionally, AWS SAM supports all AWS CloudFormation template items such as Outputs, Mappings, Parameters, providing developers with the comprehensive tooling needed to build robust and scalable serverless applications.

![AWS Serverless Application Model SAM](https://digitalcloud.training/wp-content/uploads/2022/02/aws-serverless-application-model-sam.jpeg)

## II. Key Benefits of AWS SAM

### A. Integration with Development Tools

AWS SAM not only works seamlessly with popular integrated development environments (IDEs) like PyCharm, IntelliJ, and VS Code, enhancing productivity and simplifying the development process, but it also integrates with a comprehensive suite of AWS serverless tools.

This integration allows you to discover new applications in the [AWS Serverless Application Repository](https://serverlessrepo.aws.amazon.com/applications) and utilize the [AWS Cloud9 IDE](https://aws.amazon.com/cloud9/) to author, test, and debug SAM-based serverless applications.

Moreover, you can leverage [AWS CodeBuild](https://aws.amazon.com/codebuild/), [AWS CodeDeploy](https://aws.amazon.com/codedeploy/), and [AWS CodePipeline](https://aws.amazon.com/codepipeline/) to construct an efficient and reliable deployment pipeline for your serverless applications.

### B. Local Testing and Debugging

With SAM CLI, you can locally build, test, and debug applications defined by SAM templates. This accelerates the development cycle by providing immediate feedback. The SAM CLI provides a Lambda-like execution environment that lets developers locally build, test, and debug applications defined by SAM templates.

![AWS SAM Build Locally](https://digitalcloud.training/wp-content/uploads/2022/02/aws-sam-build-locally.jpeg)

Moreover, the SAM CLI can also be used to deploy these applications to AWS, making it an all-encompassing tool for managing the lifecycle of serverless applications.

### C. Built on AWS CloudFormation

AWS SAM is an extension of [AWS CloudFormation](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/Welcome.html), which means you can use all the powerful, flexible features of CloudFormation in addition to serverless-specific capabilities.

### D. Built-in Best Practices

AWS SAM templates are designed with best practices in mind, incorporating built-in application lifecycle management features such as safe deployments and rollback capabilities. This effortless integration allows developers to adopt industry-standard methodologies without significant overhead.

Further enhancing this approach, AWS SAM enables you to deploy your infrastructure as configuration. This practice facilitates the implementation of additional best practices such as code reviews, which contribute to higher code quality and fewer deployment issues.

Moreover, AWS SAM’s versatility extends to allowing gradual deployments and tracing. With just a few lines of SAM configuration, you can enable gradual deployments through AWS CodeDeploy and introduce tracing using [AWS X-Ray](https://aws.amazon.com/xray/)

## III. Disadvantages of AWS SAM

### A. The API Gateway Configuration

AWS SAM can be restrictive when it comes to API Gateway configuration. While it simplifies many aspects, it doesn’t offer the same level of flexibility as manual or Serverless Framework configurations.

### B. Poor Community of Plugin Creators

Compared to the Serverless Framework, AWS SAM has fewer plugins available. This is due in part to its narrower focus and the fact that it is relatively new.

## IV. Building a Serverless Application with AWS SAM

### A. Installing the SAM CLI

The SAM CLI is easily installed through various package managers such as Homebrew for macOS, or pip for Python.

### B. Downloading a Sample AWS SAM Application

AWS provides numerous sample SAM applications that you can use as a starting point. You can [download these samples directly from GitHub](https://github.com/serverless-projects/aws-sam-examples).

### C. Building the Application

Once you’ve created your SAM template and written your code, use the **_sam build_** command to build your application.

### D. Deployment Details

A SAM template file is a YAML configuration that represents the architecture of a serverless application.

You use the template to declare all of the AWS resources that comprise your serverless application in one place.

AWS SAM templates are an extension of AWS CloudFormation templates, so any resource that you can declare in an AWS CloudFormation template can also be declared in an AWS SAM template.

All configuration code is in YAML.

The “Transform” header indicates it’s a SAM template: Transform: ‘AWS::Serverless-2016-10-31’

There are several resource types:

- AWS::Serverless::Function (AWS Lambda)
- AWS::Serverless::Api (API Gateway)
- AWS::Serverless::SimpleTable (DynamoDB)
- AWS::Serverless::Application (AWS Serverless Application Repository)
- AWS::Serverless::HttpApi (API Gateway HTTP API)
- AWS::Serverless::LayerVersion (Lambda layers)

Only two commands are required to package and deploy to AWS.

Use either:

`sam package`

`sam deploy`

Or use:

`AWS cloudformation package`

`AWS cloudformation deploy`

SAM Policy Templates are a list of templates to apply permissions to your Lambda functions.

Examples:
- S3ReadPolicy.
- SQSPollerPolicy.
- DynamoDBCrudPolicy.

### E. Testing the Application

Test your application locally using the sam local command. For testing in the AWS environment, you can invoke your Lambda function manually or create test events in the Lambda console.

## V. Serverless Application Repository

The **AWS Serverless Application Repository** <mark style="background: #FFF3A3A6;">acts as a centralized hub for serverless applications, providing a managed repository that fosters collaboration among teams, organizations, and individual developers.</mark>  
This platform not only allows users to store and share reusable applications but also empowers them to assemble and deploy serverless architectures in innovative and efficient ways.

Leveraging the Serverless Application Repository eliminates the need for conventional deployment steps such as cloning, building, packaging, or publishing source code to AWS. Instead, users can readily incorporate pre-built applications from the repository into their serverless architectures. This practice significantly streamlines the development process, mitigates duplicated efforts, promotes adherence to organizational best practices, and accelerates time-to-market.

Further enhancing the Repository’s usability and security, integration with AWS Identity and Access Management (IAM) offers granular resource-level control over each application. This feature facilitates flexible sharing options, allowing users to publicly share applications with the broader community or privately share them with specific AWS accounts.

Explore the diverse range of applications available in the Serverless Application Repository by [CLICKING HERE](https://serverlessrepo.aws.amazon.com/applications).

## VI. AWS SAM vs. Serverless Framework

While **both AWS SAM and the Serverless Framework offer a simplified way to define and deploy serverless applications**, they each have their strengths and weaknesses.  
The Serverless Framework is provider-agnostic, meaning it can be used with multiple cloud providers, not just AWS.

On the other hand, AWS SAM is an AWS-specific service with deep integration and support for AWS services.  
The choice between the two often depends on the specific needs and context of your project.

![AWS SAM vs. Serverless Framework](https://digitalcloud.training/wp-content/uploads/2023/05/AWS-SAM-Cheat-Sheet-1024x736.png)