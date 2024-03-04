---
tags:
  - cloud/aws
review-frequency: normal
reviewed: 2023-12-20
---
**AWS CloudFormation** is a service that <mark style="background: #BBFABBA6;">allows you to manage, configure and provision your AWS infrastructure as code.</mark>

AWS CloudFormation provides a common language for you to describe and provision all the infrastructure resources in your cloud environment.  

Resources are defined using a **CloudFormation template.**
- <mark style="background: #BBFABBA6;">CloudFormation interprets the template and makes the appropriate API calls to create the resources you have defined.</mark>
- **Supports YAML or JSON**.
- CloudFormation can be used to provision a broad range of AWS resources.
- Think of CloudFormation as deploying infrastructure as code.

CloudFormation has some similarities with AWS Elastic Beanstalk though they are also quite different as detailed in the table below:

|   |   |
|---|---|
|**CloudFormation**|**Elastic Beanstalk**|
|“Template-driven provisioning”|“Web apps made easy”|
|Deploys infrastructure using code|Deploys applications on EC2 (PaaS)|
|Can be used to deploy almost any AWS service|Deploys web applications based on Java, .NET, PHP, Node.js, Python, Ruby, Go, and Docker|
|Uses JSON or YAML template files|Uses ZIP or WAR files|
|Similar to Terraform|Similar to Google App Engine|

## Key Benefits

- <mark style="background: #ADCCFFA6;">Infrastructure is provisioned consistently, with fewer mistakes (human error).</mark>
- Less time and effort than configuring resources manually.
- <mark style="background: #ABF7F7A6;">You can use version control and peer review for your CloudFormation templates.</mark>
- Free to use (you’re only charged for the resources provisioned).
- It can be used to manage updates and dependencies.
- <mark style="background: #ADCCFFA6;">It can be used to rollback and delete the entire stack as well.</mark>

## Key Concepts

The following table describes the key concepts associated with AWS CloudFormation:

|   |   |
|---|---|
|**Component**|**Description**|
|Templates|The JSON or YAML text file that contains the instructions for building out the AWS environment|
|Stacks|The entire environment described by the template and created, updated, and deleted as a single unit|
|StackSets|AWS CloudFormation StackSets extends the functionality of stacks by enabling you to create, update, or delete stacks across multiple accounts and regions with a single operation|
|Change Sets|A summary of proposed changes to your stack that will allow you to see how those changes might impact your existing resources before implementing them|
|Templates|The JSON or YAML text file that contains the instructions for building out the AWS environment|

## Templates

**A template is a YAML or JSON template used to describe the end-state of the infrastructure you are either provisioning or changing.**

- After creating the template, you upload it to CloudFormation directly or using Amazon S3.
- CloudFormation reads the template and makes the API calls on your behalf.
- <mark style="background: #ADCCFFA6;">The resulting resources are called a </mark>“**Stack**”.
- _Logical IDs_ <mark style="background: #ADCCFFA6;">are used to reference resources within the template.</mark>
- Physical IDs identify resources outside of AWS CloudFormation templates, but only after the resources have been created.

### Template Elements
Mandatory:
- List of resources and associated configuration values.

Not mandatory:
- Template parameters (limited to 60).
- <mark style="background: #CACFD9A6;">Output values (limited to 60).</mark>
- List of data tables.

### Template Components

**Resources** – the _required_ Resources section declares the AWS resources that you want to include in the stack, such as an Amazon EC2 instance or an Amazon S3 bucket.
- Mandatory.
- Represent AWS components that will be created.
- Resources are declared and can reference each other.

The following example YAML code declares an EC2 instance as a resource:
```
Resources:  
  MyEC2Instance:  
    Type: "AWS::EC2::Instance"  
    Properties:  
      ImageId: "ami-0ff8a91507f77f867"
```

### Parameters
Use the _optional_ Parameters section to customize your templates. **Parameters enable you to input custom values to your template each time you create or update a stack.**
- <mark style="background: #ABF7F7A6;">Provide inputs to your CloudFormation template.</mark>
- <mark style="background: #ABF7F7A6;">Useful for template reuse.</mark>

The following example declares a parameter named _InstanceTypeParameter_.  
<mark style="background: #ABF7F7A6;">This parameter lets you specify the Amazon EC2 instance type for the stack to use when you create or update the stack.</mark>

**_Note:_** _the InstanceTypeParameter has a default value of t2.micro. This is the value that AWS CloudFormation uses to provision the stack unless another value is provided._
```
Parameters:  
  InstanceTypeParameter:  
    Type: String  
    Default: t2.micro  
    AllowedValues:  
      - t2.micro  
      - m1.small  
      - m1.large  
    Description: Enter t2.micro, m1.small, or m1.large. Default is t2.micro.
```

### Pseudo Parameters

**Pseudo parameters** are <mark style="background: #ADCCFFA6;">parameters that are predefined by AWS CloudFormation</mark>. You do not declare them in your template. Use them the same way as you would a parameter, as the argument for the Ref function.

Examples include:

- **AWS::AccountId** – <mark style="background: #CACFD9A6;">Returns the AWS account ID of the account in which the stack is being created.</mark>
- **AWS::NotificationARNs** – Returns the list of notification Amazon Resource Names (ARNs) for the current stack.
- **AWS::Region** – <mark style="background: #CACFD9A6;">Returns a string representing the AWS Region in which the encompassing resource is being created.</mark>
- AWS::StackId – Returns the ID of the stack as specified with the aws cloudformation create-stack command.

### Mappings

The _optional_ Mappings section matches a key to a corresponding set of named values.

- Fixed variables.
- Good for differentiating between regions, environments, AMIs etc.
- Need to know the values in advance.
- For user-specific values use parameters instead.

The following example has region keys that are mapped to two sets of values: one named HVM64 and the other HVMG2.
```
RegionMap:

    us-east-1:

      HVM64: ami-0ff8a91507f77f867

      HVMG2: ami-0a584ac55a7631c0c

    us-west-1:

      HVM64: ami-0bdb828fd58c52235

      HVMG2: ami-066ee5fd4a9ef77f1
```

**_Exam tip:_** _with mappings you can, for example, set values based on a region. You can create a mapping that uses the region name as a key and contains the values you want to specify for each specific region._

### Outputs

The _optional_ Outputs section<mark style="background: #ABF7F7A6;"> declares output values that you can import into other stacks </mark>(**to create cross-stack references**), <mark style="background: #ABF7F7A6;">return in response (to describe stack calls)</mark>, or v<mark style="background: #ABF7F7A6;">iew on the AWS CloudFormation console.</mark>

- <mark style="background: #BBFABBA6;">Outputs can be imported into other stacks.</mark>
- <mark style="background: #BBFABBA6;">Can view the outputs in the console or using the AWS CLI.</mark>
- <mark style="background: #ABF7F7A6;">Cannot delete a Stack if its outputs are being referenced by another CloudFormation Stack.</mark>

In the following example YAML code, the output named StackVPC returns the ID of a VPC, and then exports the value for cross-stack referencing with the name VPCID appended to the stack’s name
```
Outputs:
  StackVPC:
    Description: The ID of the VPC
    Value: !Ref MyVPC
    Export:
      Name: !Sub "${AWS::StackName}-VPCID"

```
### Conditions

The _optional_ Conditions section <mark style="background: #ABF7F7A6;">contains statements that define the circumstances under which entities are created or configured.</mark>
- <mark style="background: #BBFABBA6;">Control the creation of resources based on a condition.</mark>
- <mark style="background: #BBFABBA6;">Applied to resources and outputs.</mark>

In the sample YAML code below, resources are created only if the EnvType parameter is equal to prod:
```
Conditions:
  CreateProdResources: !Equals [ !Ref EnvType, prod ]
```


### Transform

The _optional_ Transform <mark style="background: #ABF7F7A6;">section specifies one or more macros that AWS CloudFormation uses to process your template.</mark>

The transform section can be used to reference additional code stored in S3, such as Lambda code or reusable snippets of CloudFormation code.

**The AWS::Serverless transform**, which is<mark style="background: #ADCCFFA6;"> a macro hosted by AWS CloudFormation, takes an entire template written in the AWS Serverless Application Model (AWS SAM) syntax and transforms and expands it into a compliant AWS CloudFormation template.</mark>

In the following example, the template uses AWS SAM syntax to simplify the declaration of a Lambda function and its execution role:
```
Transform: AWS::Serverless-2016-10-31

Resources:

  MyServerlessFunctionLogicalID:

    Type: AWS::Serverless::Function

    Properties:

      Handler: index.handler

      Runtime: nodejs8.10

      CodeUri: 's3://testBucket/mySourceCode.zip'
```


### Intrinsic Functions

AWS CloudFormation <mark style="background: #BBFABBA6;">provides several built-in functions that help you manage your stacks</mark>.  
**Use intrinsic functions in your templates to assign values to properties that are not available until runtime.**

**_EXAM TIP:_** _At a minimum, know the intrinsic functions listed below for the exam. The full list can be found at: https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/intrinsic-function-reference.html_

**Ref**
- Fn::Ref (or !Ref in YAML),
- <mark style="background: #D2B3FFA6;">The intrinsic function Ref returns the value of the specified parameter or resource.</mark>
- When you specify a parameter’s logical name, it returns the value of the parameter.
- When you specify a resource’s logical name, it returns a value that you can typically use to refer to that resource, such as a physical ID.

The following <mark style="background: #CACFD9A6;">resource declaration for an Elastic IP address</mark> <mark style="background: #ADCCFFA6;">needs the instance ID of an EC2 instance and uses the Ref function to specify the instance ID of the MyEC2Instance resource</mark>:
```
MyEIP:
  Type: "AWS::EC2::EIP"
  Properties:
    InstanceId: !Ref MyEC2Instance
```

**Fn::GetAtt**

- The Fn::GetAtt <mark style="background: #D2B3FFA6;">intrinsic function returns the value of an attribute from a resource in the template.</mark>
- Full syntax (YAML): Fn::GetAtt: [ logicalNameOfResource, attributeName ]
- Short form (YAML): !GetAtt logicalNameOfResource.attributeName

The following example template returns the _SourceSecurityGroup.OwnerAlias_ and _SourceSecurityGroup.GroupName_ of the load balancer with the logical name myELB.
```
AWSTemplateFormatVersion: 2010-09-09
Resources:
  myELB:
    Type: AWS::ElasticLoadBalancing::LoadBalancer
    Properties:
      AvailabilityZones:
        - eu-west-1a
      Listeners:
        - LoadBalancerPort: '80'
          InstancePort: '80'
          Protocol: HTTP

  myELBIngressGroup:
    Type: AWS::EC2::SecurityGroup
    Properties:
      GroupDescription: ELB ingress group
      SecurityGroupIngress:
        - IpProtocol: tcp
          FromPort: '80'
          ToPort: '80'
          SourceSecurityGroupOwnerId: !GetAtt myELB.SourceSecurityGroup.OwnerAlias
          SourceSecurityGroupName: !GetAtt myELB.SourceSecurityGroup.GroupName
```


**Fn::FindInMap**

- The intrinsic function Fn::FindInMap <mark style="background: #FFF3A3A6;">returns the value corresponding to keys in a two-level map that is declared in the Mappings section.</mark>
- Full syntax (YAML): Fn::FindInMap: [ MapName, TopLevelKey, SecondLevelKey ]
- Short form (YAML): !FindInMap [ MapName, TopLevelKey, SecondLevelKey ]

The following example shows how to use Fn::FindInMap for a template with a Mappings section that contains a single map, RegionMap, that associates AMIs with AWS regions:
```
Mappings:
  RegionMap:
    us-east-1:
      HVM64: "ami-0ff8a91507f77f867"
      HVMG2: "ami-0a584ac55a7631c0c"
    us-west-1:
      HVM64: "ami-0bdb828fd58c52235"
      HVMG2: "ami-066ee5fd4a9ef77f1"
Resources:
  myEC2Instance:
    Type: "AWS::EC2::Instance"
    Properties:
      ImageId: !FindInMap
        - RegionMap
        - !Ref 'AWS::Region'
        - HVM64
      InstanceType: m1.small
```

**Fn::ImportValue**
- The intrinsic function **Fn::ImportValue** <mark style="background: #D2B3FFA6;">returns the value of an output exported by another stack.</mark>
- <mark style="background: #ABF7F7A6;">You typically use this function to create cross-stack references.</mark>
```
Fn::ImportValue:
  !Sub "${NetworkStackName}-SecurityGroupID"
```


**Fn::Join**
- Full syntax (YAML): Fn::Join: [ delimiter, [ comma-delimited list of values ] ]
- Short form (YAML): !Join [ delimiter, [ comma-delimited list of values ] ]

The following example uses **Fn::Join** <mark style="background: #D2B3FFA6;">to construct a string value.</mark>  
It uses the Ref function with the Partition parameter and the AWS::AccountId pseudo parameter.
```
!Join
  - ''
  - - 'arn:'
    - !Ref Partition
    - ':s3:::elasticbeanstalk-*-'
    - !Ref 'AWS::AccountId'
```

**Fn::Sub**
- The intrinsic function **Fn::Sub** <mark style="background: #D2B3FFA6;">substitutes variables in an input string with values that you specify.</mark>
- <mark style="background: #BBFABBA6;">In your templates, you can use this function to construct commands or outputs that include values that aren’t available until you create or update a stack.</mark>

The following example uses a mapping to substitute the ${Domain} variable with the resulting value from the Ref function:
```
Name: !Sub
  - www.${Domain}
  - { Domain: !Ref RootDomainName }
```

## Stacks and Stack Sets
### Stacks

- <mark style="background: #ABF7F7A6;">Deployed resources based on templates.</mark>
- Create, update, and delete stacks using templates.
- Deployed through the Management Console, CLI or APIs.

Stack creation errors:
- <mark style="background: #BBFABBA6;">Automatic rollback on error is enabled by default.</mark>
- <mark style="background: #CACFD9A6;">You will be charged for resources provisioned even if there is an error.</mark>

Updating stacks:
- AWS CloudFormation<mark style="background: #BBFABBA6;"> provides two methods for updating stacks: direct update or creating and executing change sets.</mark>
- When you directly update a stack, you submit changes and AWS CloudFormation immediately deploys them.
- <mark style="background: #CACFD9A6;">Use direct updates when you want to quickly deploy your updates.</mark>
- <mark style="background: #ABF7F7A6;">With change sets, you can preview the changes</mark> AWS CloudFormation will make to your stack, and then decide whether to apply those changes.

### Stack Sets

**AWS CloudFormation StackSets** <mark style="background: #CACFD9A6;">extends the functionality of stacks</mark> by enabling you to <mark style="background: #ABF7F7A6;">create, update, or delete stacks across multiple accounts and regions with a single operation.</mark>

Using an administrator account, you define and manage an AWS CloudFormation template, and use the template as the basis for provisioning stacks into selected target accounts across specified regions.

An administrator account is the AWS account in which you create stack sets.  
A stack set is managed by signing in to the AWS administrator account in which it was created.  
A target account is the account into which you create, update, or delete one or more stacks in your stack set.

Before you can use a stack set to create stacks in a target account, you must set up a trust relationship between the administrator and target accounts.

### Nested Stacks

Nested stacks allow re-use of CloudFormation code for common use cases.

For example standard configuration for a load balancer, web server, application server etc.

Instead of copying out the code each time, create a standard template for each common use case and reference from within your CloudFormation template.

## Best Practices

AWS provides Python “helper scripts” which can help you install software and start services on your EC2 instances.

- Use CloudFormation to make changes to your landscape rather than going directly into the resources.
- Make use of Change Sets to identify potential trouble spots in your updates.
- Use Stack Policies to explicitly protect sensitive portions of your stack.
- <mark style="background: #ABF7F7A6;">Use a version control system such as CodeCommit or GitHub to track changes to templates.</mark>

## Serverless Application Model (SAM)

Use SAM for deploying serverless applications using CloudFormation.

SAM is an extension to CloudFormation used to define serverless applications.

Simplified syntax for defining serverless resources: APIs, Lambda Functions, DynamoDB Tables etc.

Use the SAM CLI to package your deployment code, upload it to S3 and deploy your serverless application.

## User Data with EC2

User data can be included in CloudFormation.  
The script is passed into Fn::Base64

The user data script logs are stored in /var/log/cloud-init-output.log

Binary is available on Amazon EC2 at /opt/aws/bin/cfn-init

## CloudFormation Helper Scripts

cfn-init:

- The cfn-init helper script reads template metadata from the AWS::CloudFormation::Init key and acts accordingly to:
- Fetch and parse metadata from AWS CloudFormation
- Install packages
- Write files to disk
- Enable/disable and start/stop services
- cfn-init does not require credentials, so you do not need to use the –access-key, –secret-key, –role, or –credential-file options.
- Logs go to /var/log/cfn-init.log

cfn-signal:

- The cfn-signal helper script signals AWS CloudFormation to indicate whether Amazon EC2 instances have been successfully created or updated.
- If you install and configure software applications on instances, you can signal AWS CloudFormation when those software applications are ready.
- You use the cfn-signal script in conjunction with a [**CreationPolicy**](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-attribute-creationpolicy.html) or an Auto Scaling group with a [**WaitOnResourceSignals**](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-attribute-updatepolicy.html) update policy.
- When AWS CloudFormation creates or updates resources with those policies, it suspends work on the stack until the resource receives the requisite number of signals or until the timeout period is exceeded.
- You can signal a creation policy ([**CreationPolicy**](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-attribute-creationpolicy.html)) or a wait condition handle ([**WaitOnResourceSignals**](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-attribute-updatepolicy.html)).

Troubleshooting errors:

- Make sure the AMI has the CloudFormation helper scripts included.
- Check that the cfn-init and cfn-signal commands have run successfully.
- Verify internet connectivity.

## Creation Policies and Wait Conditions

- CreationPolicy attribute:
- Use the CreationPolicy attribute when you want to wait on resource configuration actions before stack creation proceeds.
- You can associate the CreationPolicy attribute with a resource to prevent its status from reaching create complete until AWS CloudFormation receives a specified number of success signals, or the timeout period is exceeded.
- To signal a resource, you can use the [**cfn-signal**](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/cfn-signal.html) helper script or [**SignalResource**](https://docs.aws.amazon.com/AWSCloudFormation/latest/APIReference/API_SignalResource.html) API.
- AWS CloudFormation publishes valid signals to the stack events so that you track the number of signals sent.

The following CloudFormation resources support creation policies:

- [**AWS::AutoScaling::AutoScalingGroup**](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-as-group.html)
- [**AWS::EC2::Instance**](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-ec2-instance.html)
- [**AWS::CloudFormation::WaitCondition**](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-waitcondition.html)

DeletionPolicy attribute:

- With the DeletionPolicy attribute you can preserve or (in some cases) backup a resource when its stack is deleted.
- You specify a DeletionPolicy attribute for each resource that you want to control.
- If a resource has no DeletionPolicy attribute, AWS CloudFormation deletes the resource by default.

DependsOn attribute:

- With the DependsOn attribute you can specify that the creation of a specific resource follows another.
- When you add a DependsOn attribute to a resource, that resource is created only after the creation of the resource specified in the DependsOn attribute.

WaitCondition:

- Note: For Amazon EC2 and Auto Scaling resources, AWS recommends that you use a CreationPolicy attribute instead of wait conditions.
- You can use a wait condition for situations like the following:
- To coordinate stack resource creation with configuration actions that are external to the stack creation.
- To track the status of a configuration process.

UpdatePolicy Attribute (WaitOnResourceSignals)

Use the UpdatePolicy attribute to specify how AWS CloudFormation handles updates to the following resources:

- [**AWS::AutoScaling::AutoScalingGroup**](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-as-group.html),
- [**AWS::ElastiCache::ReplicationGroup**](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-elasticache-replicationgroup)
- [**AWS::Elasticsearch::Domain**](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-elasticsearch-domain.html)
- [**AWS::Lambda::Alias**](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-alias.html)

UpdateReplacePolicy attribute:

- Use the UpdateReplacePolicy attribute to retain or (in some cases) backup the existing physical instance of a resource when it is replaced during a stack update operation.

## Rollbacks and Creation Failures

[**Stack creation failures**](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/troubleshooting.html):

- By default everything will be deleted.
- You can optionally disable rollback (good for troubleshooting failures).

Stack update failures:

- The stack will automatically roll back to the previous known working state.
- The logs can assist with understanding what issue occurred.

## Monitoring and Reporting

You can monitor the progress of a stack update by viewing the stack’s events. The console’s **Events** tab displays each major step in the creation and update of the stack sorted by the time of each event with latest events on top.

For resources created by CloudFormation, use AWS monitoring and reporting tools applicable to the service.

## Authorization and Access Control

You can use IAM with AWS CloudFormation to control what users can do with AWS CloudFormation, such as whether they can view stack templates, create stacks, or delete stacks.

In addition to AWS CloudFormation actions, you can manage what AWS services and resources are available to each user.

That way, you can control which resources users can access when they use AWS CloudFormation.

For example, you can specify which users can create Amazon EC2 instances, terminate database instances, or update VPCs. Those same permissions are applied anytime they use AWS CloudFormation to do those actions.

## Charges

There is no additional charge for AWS CloudFormation.

You pay for AWS resources (such as Amazon EC2 instances, Elastic Load Balancing load balancers, etc.) created using AWS CloudFormation in the same manner as if you created them manually.

You only pay for what you use, as you use it; there are no minimum fees and no required upfront commitments.

## Snippets

[https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/CHAP_TemplateQuickRef.html](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/CHAP_TemplateQuickRef.html)

---

![[Module 10 - Automatic Your Architecture#Automating Your Infrastructure]]


---
![[Module 10 - Automatic Your Architecture#AWS Quick Starts]]


# FAQ

## General

Close all

### What is AWS CloudFormation?

AWS CloudFormation is a service that gives developers and businesses an easy way to create a collection of related AWS and third-party resources, and provision and manage them in an orderly and predictable fashion.

### What Can Developers Do with AWS CloudFormation?

Developers can deploy and update compute, database, and many other resources in a simple, declarative style that abstracts away the complexity of specific resource APIs. AWS CloudFormation is designed to allow resource lifecycles to be managed repeatably, predictable, and safely, while allowing for automatic rollbacks, automated state management, and management of resources across accounts and regions. Recent enhancements and options allow for multiple ways to create resources, including using AWS CDK for coding in higher-level languages, importing existing resources, detecting configuration drift, and a new Registry that makes it easier to create custom types that inherit many core CloudFormation benefits.

### How is CloudFormation Different from AWS Elastic Beanstalk?

These services are designed to complement each other. [AWS Elastic Beanstalk](https://aws.amazon.com/elasticbeanstalk/) provides an environment where you can easily deploy and run applications in the cloud. It is integrated with developer tools and provides a one-stop experience for managing application lifecycle. If your application workloads can be managed as Elastic Beanstalk workloads, you can enjoy a more turn-key experience in creating and updating applications. Behind the scenes, Elastic Beanstalk uses CloudFormation to create and maintain resources. If your application requirements dictate more custom control, the additional functionality of CloudFormation gives you more options to control your workloads.

AWS CloudFormation is a convenient provisioning mechanism for a broad range of [AWS](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/cfn-supported-resources.html) and third-party resources. It supports the infrastructure needs of many different types of applications such as existing enterprise applications, legacy applications, applications built using a variety of AWS resources, and container-based solutions (including those built using AWS Elastic Beanstalk).

AWS CloudFormation supports Elastic Beanstalk application environments as one of the AWS resource types. This allows you, for example, to create and manage an AWS Elastic Beanstalk–hosted application along with an RDS database to store the application data. Any other supported AWS resource can be added to the group as well.

### What New Concepts Does AWS CloudFormation Introduce?

CloudFormation introduces four concepts: A template is a JSON or YAML declarative code file that describes the intended state of all the resources you need to deploy your application. A stack implements and manages the group of resources outlined in your template, and allows the state and dependencies of those resources to be managed together. A change set is a preview of changes that will be executed by stack operations to create, update, or remove resources. A stack set is a group of stacks you manage together that can replicate a group.

### What Resources Does AWS CloudFormation Support?

To see a complete list of supported [AWS resources](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/cfn-supported-resources.html) and their features, visit the Supported AWS Services page in the Release History of the documentation.

The [AWS CloudFormation Registry](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/registry.html) and AWS CloudFormation [custom resources](http://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/crpg-walkthrough.html) enable management of additional AWS and third party resources.

### Can I Manage Individual AWS Resources that Are part of an AWS CloudFormation Stack?

Yes, you can. CloudFormation does not get in the way; you retain full control of all elements of your infrastructure, and can continue using all your existing AWS and third-party tools to manage your AWS resources. However, because CloudFormation can allow for additional rules, best practices, and compliance controls, we recommend that you allow CloudFormation to manage the changes to your resources. This predictable, controlled approach helps in managing hundreds or thousands of resources across your application portfolio.

### What Are the Elements of an AWS CloudFormation Template?

CloudFormation templates are JSON or YAML-formatted text files comprised of five types of elements:

1\. An optional list of template parameters (input values supplied at stack creation time)  
2\. An optional list of output values (e.g., the complete URL to a web application)  
3\. An optional list of data tables used to look up static configuration values (e.g., AMI names)  
4\. The list of AWS resources and their configuration values  
5\. A template file format version number

Template parameters are used to customize aspects of your template at run time, when the stack is built. For example, the Amazon RDS database size, Amazon EC2 instance types, database and web server port numbers can be passed to AWS CloudFormation when a stack is created. Each parameter can have a default value and description, and may be marked as “NoEcho” to hide the actual value you enter on the screen and in the AWS CloudFormation event logs. When you create an AWS CloudFormation stack, the AWS Management Console will automatically synthesize and present a pop-up dialog form for you to edit parameter values.

Output values are a convenient way to present a stack’s key resources (such as the address of an Elastic Load Balancing load balancer or Amazon RDS database) to the user via the AWS Management Console, or via the command line tools. You can use simple functions to concatenate string literals and the value of attributes associated with the actual AWS resources. A template can also leverage Registry resource types, your own custom private types, your own macros, and retrieving configuration parameters from AWS Secrets Manager and AWS System Manager Parameter Store.

### How Does AWS CloudFormation Choose Actual Resource Names?

You can assign logical names to AWS resources in a template. When a stack is created, AWS CloudFormation binds the logical name to the name of the corresponding actual AWS resource. Actual resource names are a combination of the stack and logical resource name. This allows multiple stacks to be created from a template without fear of name collisions between AWS resources.

### Why can’t I name All My Resources?

Although AWS CloudFormation allows you to name some resources (such as Amazon S3 buckets), CloudFormation doesn’t allow this for all resources. Naming resources restricts the reusability of templates and results in naming conflicts when an update causes a resource to be replaced. To minimize these issues, CloudFormation supports resource naming on a case by case basis.

### Can I Install Software at Stack Creation time Using AWS CloudFormation?

Yes. AWS CloudFormation provides a set of application bootstrapping scripts that enable you to install packages, files, and services on your EC2 instances simply by describing them in your CloudFormation template. For more details and a how-to, see [Bootstrapping Applications via AWS CloudFormation](https://s3.amazonaws.com/cloudformation-examples/BoostrappingApplicationsWithAWSCloudFormation.pdf).

CloudFormation can also be integrated with Systems Manager to drive and maintain software installations with Systems Manager Automation Documents.

### Can I Use AWS CloudFormation with Chef?

Yes. AWS CloudFormation can be used to bootstrap both the Chef Server and Chef Client software on your EC2 instances. For more details and a how-to, see [Integrating AWS CloudFormation with Chef](https://s3.amazonaws.com/cloudformation-examples/IntegratingAWSCloudFormationWithOpscodeChef.pdf).

### Can I Use AWS CloudFormation with Puppet?

Yes. AWS CloudFormation can be used to bootstrap both the Puppet Master and Puppet Client software on your EC2 instances. For more details and a how-to, see Integrating AWS CloudFormation with Puppet.

### Can I Use AWS CloudFormation with Terraform?

Yes. CloudFormation can bootstrap your Terraform engine on your EC2 instances, and you can use Terraform resource providers to create resources in stacks, leveraging stack state management, dependencies, stabilization and rollback.

### Does AWS CloudFormation Support Amazon EC2 Tagging?

Yes. Amazon EC2 resources that support the tagging feature can also be tagged in an AWS template. The tag values can refer to template parameters, other resource names, resource attribute values (e.g. addresses), or values computed by simple functions (e.g., a concatenated a list of strings). CloudFormation automatically tags Amazon EBS volumes and Amazon EC2 instances with the name of the CloudFormation stack they are part of.

### Do I Have Access to the Amazon EC2 Instance, or Auto Scaling Launch Configuration User-data Fields?

Yes. You can use simple functions to concatenate string literals and attribute values of the AWS resources and pass them to user-data fields in your template. Please refer to our sample templates to learn more about these easy to use functions.

### What Happens when One of the Resources in a Stack Cannot Be Created Successfully?

By default, the “automatic rollback on error” feature is enabled. This will direct CloudFormation to only create or update all resources in your stack if all individual operations succeed. If they do not, CloudFormation reverts the stack to the last known stable configuration. This is useful when, for example, you accidentally exceed your default limit of Elastic IP addresses, or you don’t have access to an EC2 AMI that you’re trying to run. This feature enables you to rely on the fact that stacks are created either fully or not at all, which simplifies system administration and layered solutions built on top of CloudFormation.

### Can Stack Creation Wait for My Application to Start Up?

Yes. One of the options CloudFormation provides is a _WaitCondition_ resource that acts as a barrier, blocking the creation of other resources until a completion signal is received from an external source such as your application or management system. Other options include creating custom logic with AWS Lambda functions.

### Can I save My Data when a Stack is Deleted?

Yes. CloudFormation allows you to define deletion policies for resources in the template. You can specify that snapshots be created for Amazon EBS volumes or Amazon RDS database instances before they are deleted. You can also specify that a resource should be preserved and not deleted when the stack is deleted. This is useful for preserving Amazon S3 buckets when the stack is deleted.

### Can I Create Stacks in a Virtual Private Cloud (VPC)?

Yes. CloudFormation supports creating VPCs, subnets, gateways, route tables and network ACLs as well as creating resources such as elastic IPs, Amazon EC2 Instances, EC2 security groups, auto scaling groups, elastic load balancers, Amazon RDS database instances and Amazon RDS security groups in a VPC.

### Can I Update My Stack after it Has Been Created?

Yes. You can use CloudFormation to modify and update the resources in your existing stacks in a controlled and predictable way. By using templates to manage your stack changes, you have the ability to apply version control to your AWS infrastructure just as you do with the software running on it.

### How Can I Participate in the CloudFormation Community?

Please join the [AWS CloudFormation GitHub community](https://github.com/aws-cloudformation).

### Can I Manage Resources Created outside of CloudFormation?

Yes! With Resource Import, you can bring an existing resource into AWS CloudFormation management using [resource import](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/resource-import.html).

## Getting Started

Close all

### How Do I Sign up for AWS CloudFormation?

To sign up for CloudFormation, click **Create Free Account** on the [CloudFormation product page](https://aws.amazon.com/cloudformation/). After signing up, please refer to the CloudFormation [documentation](https://docs.aws.amazon.com/cloudformation/), which includes our Getting Started Guide.

### Why Am I Asked to Verify My Phone Number when Signing up for AWS CloudFormation?

CloudFormation registration requires you to have a valid phone number and email address on file with AWS in case we ever need to contact you. Verifying your phone number takes only a few minutes and involves receiving an automated phone call during the registration process and entering a PIN number using the phone key pad.

### How Do I Get Started after I Have Signed Up?

The best way to get started with CloudFormation is to work through the Getting Started Guide, which is included in our technical documentation. Within a few minutes, you will be able to deploy and use one of our sample templates that illustrate how to create the infrastructure needed to run applications such as such as WordPress. There are various other sources of CloudFormation training, from thirdsparty curriculum providers to tutorials and articles on the web. For more information, check out the [CloudFormation Resources](https://aws.amazon.com/cloudformation/resources/).

### Are there Sample Templates that I Can Use to Check out AWS CloudFormation?

Yes, CloudFormation includes [sample templates](https://aws.amazon.com/cloudformation/resources/templates/) that you can use to test drive the offering and explore its functionality. Our sample templates illustrate how to interconnect and use multiple AWS resources in concert, following best practices for multiple Availability Zone redundancy, scale out, and alarming. To get started, all you need to do is go to the AWS Management Console, click Create Stack, and follow the steps to select and launch one of our samples. Once created, select your stack in the console and review the Template and Parameter tabs to look at the details of the template file used to create the respective stack. Sample templates are also available on GitHub.

## AWS CloudFormation Registry

Close all

### What is the AWS CloudFormation Registry?

The AWS CloudFormation Registry is a managed service that lets you register, use, and discover AWS and third-party resource types. Third-party resource types must be registered before they can be used to provision resources with AWS CloudFormation templates. Please see [Using the AWS CloudFormation registry](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/registry.html) in our in the documentation for details.

### What Are Resource Types in AWS CloudFormation?

A resource provider is a set of resource types with specifications and handlers that control the lifecycle of underlying resources via create, read, update, delete, and list operations. You can use resource providers to model and provision resources using CloudFormation. For example, AWS::EC2::Instance is a resource type from the Amazon EC2 provider. You can use this type to model and provision an Amazon EC2 instance using CloudFormation. Using the CloudFormation Registry, you can build and use resource providers to model and provision third-party resources such as SaaS monitoring, team productivity, or source code management resources.

### What is the Difference between AWS and Third Party Resource Providers?

The difference between AWS and third party resource providers is their origin. AWS resource providers are built and maintained by Amazon and AWS to manage AWS resources and services. For example, three AWS resource providers help you manage Amazon DynamoDB, AWS Lambda, and Amazon EC2 resources. These providers contain resource types such as AWS::DynamoDB::Table, AWS::Lambda::Function, and AWS::EC2::Instance. For a complete reference, go to our documentation.

Third party resource providers are built by another company, organization, or the developer community. They can help you manage both AWS and non-AWS resources such as AWS application resources and non-AWS SaaS software services such as monitoring, team productivity, incident management, or version control management tools.

### What is a Resource Schema?

A resource schema defines a resource type in a structured and consistent format. This schema is also used to validate the definition of a resource type. The schema includes all the supported parameters and attributes for a given resource type, as well as the required permissions to create the resource with the least privileges possible.

### How Do I Develop Resource Types?

Use the [AWS CloudFormation CLI](https://docs.aws.amazon.com/cloudformation-cli/latest/userguide/what-is-cloudformation-cli.html) to build resource providers. You start by defining a simple declarative schema for your resources, which includes permissions required and relationships to other resources. You then use the CloudFormation CLI to generate the scaffolding for resource lifecycle handlers (Create, Read, Update, Delete, and List), along with test stubs for unit and integration testing.

### How Do I Register a Resource Provider?

You can either use the open source [AWS CloudFormation CLI](https://docs.aws.amazon.com/cloudformation-cli/latest/userguide/what-is-cloudformation-cli.html) or directly call the RegisterType and related Registry APIs available via the AWS SDKs and AWS CLI. For more details, please see [Using the AWS CloudFormation registry](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/registry.html) in our in the documentation. AWS resource providers are available out of the box and do not require any additional registration steps before use.

## AWS CloudFormation Public Registry

Close all

### How Does CloudFormation Public Registry Relate to the CloudFormation Registry?

The CloudFormation Registry launched in November 2019 consisted of a private listing, allowing customers to extend CloudFormation for their own private use. The Public Registry extends the CloudFormation Registry and adds a public, searchable, central location for sharing, finding, consuming, and managing Resource Types and Modules <>, making it that much easier to configure and manage infrastructure and applications in a consistent manner for both AWS and third-party products.

### Is there a Cost for Using Third-party Resource Types Available on the CloudFormation Public Registry?

Yes. Refer to the [CloudFormation pricing page](https://aws.amazon.com/cloudformation/pricing/).

### Does AWS Verify Publishers of Third-party Extensions on the CloudFormation Public Registry?

Yes. In the CloudFormation Public Registry, you have access to curated content from verified publishers. First, we verify each publisher's identity using either AWS Marketplace or third-parties such as GitHub and Bitbucket.

### What is the AWS CloudFormation Public Registry

CloudFormation Public Registry is a new searchable and managed catalog of extensions that contains resource types (provisioning logic) and [modules](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/modules.html) published by AWS Partner Network (APN) Partners and the developer community. With CloudFormation Public Registry, anyone can now publish resource types and Modules on the Registry. Customers can easily discover and use these published resource types and modules, eliminating the need to build and maintain themselves.

### What is the Difference between a Resource and a Module?

A Resource Type is a code package containing provisioning logic, which allows you to manage the lifecycle of a resource like an Amazon EC2 Instance or an Amazon DynamoDB Table from creation to deletion, abstracting away complex API interactions. Resource Types contain a schema, which defines the shape and properties of a resource, and the necessary logic to provision, update, delete, and describe a resource. An example third-party Resource Type in the CloudFormation Public Registry is a Datadog monitor, MongoDB Atlas Project, or an Atlassian Opsgenie User among others.  
  
Modules are building blocks that can be reused across multiple CloudFormation templates and is used just like a native CloudFormation resource. These building blocks can be for a single resource, like best practices for defining an Amazon Elastic Compute Cloud (Amazon EC2) instance or they can be for multiple resources, to define common patterns of application architecture.

### How Do I Develop and Add My Own Resource or Module to the AWS CloudFormation Registry?

You can refer to this [link](https://docs.aws.amazon.com/cloudformation-cli/latest/userguide/resource-types.html) to develop and add your own resource or module to the AWS CloudFormation Registry. You can choose to publish it privately or to the Public Registry.

## Billing

Close all

### How much Does AWS CloudFormation Cost?

There is no additional charge for using AWS CloudFormation with resource providers in the following namespaces: AWS::\*, Alexa::\*, and Custom::\*. In this case, you pay for AWS resources (such as Amazon EC2 instances, Elastic Load Balancing load balancers, etc.) created using AWS CloudFormation just as if you had created them manually. You only pay for what you use, as you use it; there are no minimum fees and no required upfront commitments.

When you use resource providers with AWS CloudFormation outside the namespaces mentioned above, you incur charges per handler operation. Handler operations are create, update, delete, read, or list actions on a resource. For more information, please refer to our [pricing page](https://aws.amazon.com/cloudformation/pricing/).

### Will I Be Charged for Resources that Were Rolled back during a Failed Stack Creation Attempt?

Yes. Charges for AWS resources created during template instantiation apply irrespective of whether the stack as a whole could be created successfully.

## Limits and Restrictions

Close all

### Are there Limits to the Number of Templates or Stacks?

For more information on the maximum number of AWS CloudFormation stacks that you can create, see Stacks in [AWS CloudFormation quotas](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/cloudformation-limits.html?pg=fq&sec=lr). Complete our request for a higher limit [here](https://aws.amazon.com/contact-us/cloudformation-request/), and we will respond to your request within two business days.

### Are there Limits to the Size of Description Fields?

For more information, see Template Description in [AWS CloudFormation quotas](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/cloudformation-limits.html?pg=fq&sec=lr) and [Parameters](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/parameters-section-structure.html?pg=fq&sec=lr), [Resources](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/resources-section-structure.html?pg=fq&sec=lr) and [Outputs](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/outputs-section-structure.html?pg=fq&sec=lr) in the AWS documentation.

### Are there Limits to the Number of Parameters or Outputs in a Template?

For more information on the number of parameters and outputs you can specify in a template, see Parameters and Outputs sections in [AWS CloudFormation quotas](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/cloudformation-limits.html?pg=fq&sec=lr).

### Are there Limits to the Number of Resources that Can Be Created in a Stack?

For more information on the number of resources you can declare in a template, see Resources in [AWS CloudFormation quotas](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/cloudformation-limits.html?pg=fq&sec=lr). Creating smaller templates and stacks and modularizing your application across multiple stacks is a best practice to minimize blast radius for your resource changes, and to troubleshoot issues with multiple resource dependencies faster, since smaller groups of resources will have less complex dependencies than larger groups.

## Regions and Endpoints
### What Are the AWS CloudFormation Service Access Points in Each Region?

Endpoints for each region are available in [AWS CloudFormation endpoints](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/using-cfn-endpoints.html) in the technical [documentation](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/using-cfn-endpoints.html).


# [[Basics | CloudFormation Basics using AWS CLI]]
## AWS CLI
### Launching Latest Amazon Linux AMI in an AWS CloudFormation Stack

[AWS CloudFormation](https://aws.amazon.com/cloudformation/) also supports Parameter Store.  
For more information, see [Integrating AWS CloudFormation with AWS Systems Manager Parameter Store](https://aws.amazon.com/blogs/mt/integrating-aws-cloudformation-with-aws-systems-manager-parameter-store/). Here’s an example of how you would reference the latest Amazon Linux AMI in a CloudFormation template.
```YAML
# Use public Systems Manager Parameter 
Parameters: 
  LatestAmiId: 
    Type: 'AWS::SSM::Parameter::Value<AWS::EC2::Image::Id>'
    Default: '/aws/service/ami-amazon-linux-latest/amzn2-ami-hvm-x86_64-gp2' 
   Resources: 
    Instance:  
      Type: 'AWS::EC2::Instance' 
      Properties: 
        ImageId: !Ref LatestAmiId
```

