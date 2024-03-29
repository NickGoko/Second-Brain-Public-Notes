---
tags:
  - cloud/aws
---


# FAQ
## General

**Q: What is AWS CodePipeline?**

AWS CodePipeline is a continuous delivery service that enables you to model, visualize, and automate the steps required to release your software. With AWS CodePipeline, you model the full release process for building your code, deploying to pre-production environments, testing your application and releasing it to production. AWS CodePipeline then builds, tests, and deploys your application according to the defined workflow every time there is a code change. You can integrate partner tools and your own custom tools into any stage of the release process to form an end-to-end continuous delivery solution.

  
**Q: Why should I use AWS CodePipeline?**

By automating your build, test, and release processes, AWS CodePipeline enables you to increase the speed and quality of your software updates by running all new changes through a consistent set of quality checks.

**Q: What is continuous delivery?**

Continuous delivery is a software development practice where code changes are automatically built, tested, and prepared for a release to production. AWS CodePipeline is a service that helps you practice continuous delivery. Learn more about continuous delivery [here](https://aws.amazon.com/devops/continuous-delivery/).

## Concepts

The diagram below represents the concepts discussed in this section.

![](https://d1.awsstatic.com/product-marketing/CodePipeline/CodePipeline_Elements.1390531beabe7fd38b2414c39800136eed24e9c8.png)

**Q: What is a pipeline?**

A pipeline is a workflow construct that describes how software changes go through a release process. You define the workflow with a sequence of stages and actions.


![[Pasted image 20240229220702.png]]

![[Pasted image 20240229205033.png]]  
**Q: What is a revision?**

A revision is a change made to the source location defined for your pipeline. It can include source code, build output, configuration, or data. A pipeline can have multiple revisions flowing through it at the same time.

**Q: What is a stage?**

A stage is a group of one or more actions. A pipeline can have two or more stages.

**Q: What is an action?**

An action is a task performed on a revision. Pipeline actions occur in a specified order, in serial or in parallel, as determined in the configuration of the stage. For more information, see [Edit a Pipeline](http://docs.aws.amazon.com/codepipeline/latest/userguide/how-to-edit-pipelines.html) and [Action Structure Requirements in AWS CodePipeline](http://docs.aws.amazon.com/codepipeline/latest/userguide/pipeline-structure.html#action-requirements).

**Q: What is an artifact?**

When an action runs, it acts upon a file or set of files. These files are called artifacts. These artifacts can be worked upon by later actions in the pipeline. For example, a source action will output the latest version of the code as a source artifact, which the build action will read in. Following the compilation, the build action will upload the build output as another artifact, which will be read by the later deployment actions.

**Q: What is a transition?**

The stages in a pipeline are connected by transitions, and are represented by arrows in the AWS CodePipeline console. Revisions that successfully complete the actions in a stage will be automatically sent on to the next stage as indicated by the transition arrow. Transitions can be disabled or enabled between stages.

## Using AWS CodePipeline

**Q: How do I get started with AWS CodePipeline?**

You can sign in to the [AWS Management Console](https://console.aws.amazon.com/codepipeline/), create a pipeline, and start using the service. If you want an introduction to AWS CodePipeline, see [Getting Started](http://docs.aws.amazon.com/codepipeline/latest/userguide/getting-started.html), which includes step-by-step tutorials. 

**Q: How do I start a pipeline?**  
After you create a pipeline, it will automatically trigger a run to release the latest revision of your source code. From then on, every time you make a change to your source location, a new run is triggered. In addition, you can re-run the last revision through a pipeline using the [Release Change button in the pipeline console.](http://docs.aws.amazon.com/codepipeline/latest/userguide/how-to-manually-start.html)

**Q: How do I stop a pipeline?**  
To stop a pipeline, you can disable a transition from one stage to another. Once disabled, your pipeline will continue to run revisions through the actions, but it will not promote revisions through the disabled transition to later stages. For more details, see Disable or Enable Transitions in AWS CodePipeline.

**Q: Can I edit an existing pipeline?**  
Yes. You can use the AWS CodePipeline console or AWS CLI to add or remove stages in a pipeline as well as to add, edit, or remove actions in a stage.

**Q: Can I create a copy of an existing pipeline?**  
Yes. You can use the get-pipeline AWS CLI command to get the JSON structure of your existing pipeline. You can then use that JSON and the create-pipeline AWS CLI command to create a new pipeline with the same structure as the existing one.

**Q: Can actions run in parallel?**  
Yes. You can configure one or more actions to run in parallel for any given stage.

**Q: How can I practice continuous delivery for my serverless applications and AWS Lambda functions?**  
You can release updates to your serverless application by including the [AWS Serverless Application Model](http://docs.aws.amazon.com/lambda/latest/dg/deploying-lambda-apps.html) template and its corresponding files in your source code repository. You can use AWS CodeBuild in your pipeline to package your code for deployment. You can then use [AWS CloudFormation actions](http://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/continuous-delivery-codepipeline.html) to create a [change set](http://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/using-cfn-updating-stacks-changesets.html) and deploy your serverless application. You have the option to extend your workflow with additional steps such as manual approvals or automated tests. Learn more [here](http://docs.aws.amazon.com/lambda/latest/dg/automating-deployment.html).

**Q: How can I provision and manage my AWS resources through a release workflow process?**  
Using AWS CodePipeline and AWS CloudFormation, you can use continuous delivery to automatically build and test changes to your AWS CloudFormation stacks before promoting them to production stacks. This release process lets you rapidly and reliably make changes to your AWS infrastructure. You can extend your workflow with additional actions such as manual approvals, test actions, or invoke AWS Lambda actions. For more details, see [Continuous Delivery with AWS CloudFormation](http://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/continuous-delivery-codepipeline.html) page.

**Q: What product integrations are available with AWS CodePipeline?**  
AWS CodePipeline integrates with AWS services such as AWS CodeCommit, Amazon S3, AWS CodeBuild, AWS CodeDeploy, AWS Elastic Beanstalk, AWS CloudFormation, AWS OpsWorks, Amazon ECS, and AWS Lambda. In addition, AWS CodePipeline integrates with a number of partner tools. For details see the [product integrations](https://aws.amazon.com/codepipeline/product-integrations/) page. Finally, you can write your own custom actions and integrate any existing tool with CodePipeline. For more details on custom actions, see the [Create and Add a Custom Action in AWS CodePipeline page](http://docs.aws.amazon.com/codepipeline/latest/userguide/how-to-create-custom-action.html).

**Q: Can I get a history of AWS CodePipeline API calls?**  
Yes. To receive a history of AWS CodePipeline API calls made on your account for security analysis and operational troubleshooting purposes, you simply turn on AWS CloudTrail in the AWS Management Console. For more information, see [Logging AWS CodePipeline API calls by Using AWS CloudTrail](http://docs.aws.amazon.com/codepipeline/latest/userguide/integ-cloudtrail.html).

**Q: What are the service limits when using AWS CodePipeline?**  
For information on the service limits, see [Limits](http://docs.aws.amazon.com/codepipeline/latest/userguide/limits.html).

  
 

**Q: How do I receive notifications or alerts for any events in AWS CodePipeline?**  
You can create notifications for events impacting your pipelines. Notifications will come in the form of [Amazon SNS](https://aws.amazon.com/sns/) notifications. Each notification will include a status message as well as a link to the resources whose event generated that notification. Notifications has no additional cost; but, you may be charged for other AWS services utilized by notifications, such as Amazon SNS. To learn how to get started with notifications, see the [notifications user guide](https://docs.aws.amazon.com/codestar-notifications/latest/userguide/welcome.html). Additionally, customers using [AWS Chatbot](https://aws.amazon.com/chatbot/) can configure notifications to be sent to their Slack Channels or Amazon Chime chat rooms. For more details please check [here](https://docs.aws.amazon.com/codestar-notifications/latest/userguide/notifications-chatbot.html).  

## Partners

**Q: What do I need to do to integrate with AWS CodePipeline?**  
If you’re interested in becoming an AWS partner who integrates your developer service with AWS CodePipeline, please contact codepipeline-request@amazon.com.  

## Security

**Q: Can I use AWS Identity and Access Management (IAM) to manage access to AWS CodePipeline?**  
Yes. AWS CodePipeline supports [resource-level permissions](http://docs.aws.amazon.com/IAM/latest/UserGuide/PermissionsOverview.html). You can specify which user can perform what action on a pipeline. For example, you can provide a user read-only access to a pipeline, if you want them to see the pipeline status but not modify the pipeline. You can also set permissions for any stage or action within a pipeline. For more information on using IAM with AWS CodePipeline, see [Access Permissions Reference](http://docs.aws.amazon.com/codepipeline/latest/userguide/access-permissions.html).

**Q: Can I enable the pipeline in one AWS account to be accessed by an IAM user in another AWS account?**  
Yes. You can create an IAM role in the AWS account that owns the pipeline to delegate access to the pipeline and any related resources to an IAM user in another account. For a walkthrough on enabling such a cross account access, see [Walkthrough: Delegating Access Across AWS Accounts For Accounts You Own Using IAM Roles](http://docs.aws.amazon.com/IAM/latest/UserGuide/roles-walkthrough-crossacct.html) and [Configure Cross-Account Access to a Pipeline](http://docs.aws.amazon.com/codepipeline/latest/userguide/access-permissions.html#d0e7634).  

## Regions

**Q: Which regions does AWS CodePipeline support?**  
Please refer to [Regional Products and Services](https://aws.amazon.com/about-aws/global-infrastructure/regional-product-services/) for details of CodePipeline availability by region.  

## Billing

**Q: How much does AWS CodePipeline cost?**  
For details on AWS CodePipeline cost, see the [pricing page](https://aws.amazon.com/codepipeline/pricing/).