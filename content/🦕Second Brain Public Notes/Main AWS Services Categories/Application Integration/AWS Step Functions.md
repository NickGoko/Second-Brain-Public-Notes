---
tags:
  - cloud/aws
---


![[Pasted image 20240214143734.png]]

![[Pasted image 20240214144034.png]]

---
- [[Serverless Skillbuider#Workflow Orchestration with AWS Step Functions|Workflow Orchestration with AWS Step Functions]]

---
- [Introduction to Step Functions(opens in a new tab)](https://explore.skillbuilder.aws/pages/55/learner-dashboard?ctl231=se-%22Introduction%20to%20Step%20Functions%22)
- [How AWS Step Functions Work(opens in a new tab)](https://explore.skillbuilder.aws/pages/55/learner-dashboard?ctl231=se-%22How%20AWS%20Step%20Functions%20Work%22)
- [Observability for AWS Step Functions(opens in a new tab)](https://explore.skillbuilder.aws/pages/55/learner-dashboard?ctl231=se-%22Observability%20for%20AWS%20Step%20Functions%22)
- [Developer Tooling for AWS Step Functions(opens in a new tab)](https://explore.skillbuilder.aws/pages/55/learner-dashboard?ctl231=se-%22Developer%20Tooling%20for%20AWS%20Step%20Functions%22)
- [Design Patterns for AWS Step Functions(opens in a new tab)](https://explore.skillbuilder.aws/pages/55/learner-dashboard?ctl231=se-%22Design%20Patterns%20for%20AWS%20Step%20Functions%22)
- [AWS Step Functions Developer Guide(opens in a new tab)](https://docs.aws.amazon.com/step-functions/latest/dg/welcome.html)
- [AWS Step Functions Overview(opens in a new tab)](https://aws.amazon.com/step-functions/)
- [AWS Step Functions Quotas(opens in a new tab)](https://docs.aws.amazon.com/step-functions/latest/dg/limits.html)
- [Supported AWS Service Integrations for Step Functions(opens in a new tab)](https://docs.aws.amazon.com/step-functions/latest/dg/connect-supported-services.html)
- [Introduction to AWS Step Functions(opens in a new tab)](https://youtu.be/Dh7h3lkpeP4)
- [Build on Serverless: Breaking the Monolith with Step Functions(opens in a new tab)](https://youtu.be/CFelZoLjF50)
- ☞[The AWS Step Functions Workshop(opens in a new tab)](https://catalog.workshops.aws/stepfunctions/en-US)
- [Tutorial: Create a Serverless Workflow(opens in a new tab)](https://aws.amazon.com/getting-started/tutorials/create-a-serverless-workflow-step-functions-lambda/)
- [Builder Session: Create a State Machine that Implements the Saga Pattern](https://github.com/aws-samples/aws-step-functions-long-lived-transactions)

---
# FAQ
## Overview

## Q: What is AWS Step Functions?

[AWS Step Functions](https://aws.amazon.com/step-functions/) is <mark style="background: #FFF3A3A6;">a fully managed service that makes it easier to coordinate the components of distributed applications and microservices using visual workflows</mark>. Building applications from individual components that each perform a discrete function helps you scale more easily and change applications more quickly.  

Step Functions is a reliable way to coordinate components and step through the functions of your application.  
Step Functions provides a graphical console to arrange and visualize the components of your application as a series of steps. This makes it easier to build and run multi-step applications.  

Step Functions automatically triggers and tracks each step and retries when there are errors, so your application executes in order and as expected. Step Functions logs the state of each step, so when things do go wrong, you can [diagnose and debug problems more quickly](https://aws.amazon.com/step-functions/features/).  
You can change and add steps without even writing code, so you can more easily evolve your application and innovate faster.  

## Q: What Are the Benefits of Designing My Application Using Orchestration?

Breaking an application into service components (or steps) <mark style="background: #ADCCFFA6;">ensures that the failure of one component does not bring the whole system down</mark>.  
 Each component scales independently and that component may be updated without requiring the entire system to be redeployed after each change.  

The [coordination of service components](https://docs.aws.amazon.com/lambda/latest/dg/lambda-stepfunctions.html) involves <mark style="background: #FF5582A6;">managing execution dependencies and scheduling, and concurrency in accordance with the logical flow of the application</mark>. In such an application, you can use service orchestration to do this and to handle failures.  

## Q: What Are Some Common Step Functions Use Cases?

Step Functions helps with any computational problem or business process that can be subdivided into a series of steps.  
It’s also useful for creating end-to-end workflows to manage jobs with interdependencies. 

Common use cases include:
- Data processing: <mark style="background: #BBFABBA6;">consolidate data from multiple databases into unified reports, refine and reduce large data sets into useful formats</mark>, iterate and process millions of files in an Amazon Simple Storage Service (S3) bucket with high concurrency workflows, or coordinate multi-step analytics and machine learning workflows
	  
- <mark style="background: #ADCCFFA6;">Building serverless generative AI applications</mark>: leverage Step Functions for orchestrating interactions with [Amazon Bedrock’s](https://aws.amazon.com/bedrock/) Foundation Models, prompt chaining, fine-tuning, and enriching with capabilities from over 220 AWS services
	  
- <mark style="background: #CACFD9A6;">DevOps and IT automation</mark>: <mark style="background: #BBFABBA6;">build tools for continuous integration and continuous deployment, or create event-driven applications that automatically respond to changes in infrastructure</mark>
	  
- E-commerce: <mark style="background: #BBFABBA6;">automate mission-critical business processes, such as order fulfillment and inventory tracking</mark>
	  
- Web applications: <mark style="background: #BBFABBA6;">implement robust user registration processes and sign-on authentication </mark> 
    
## Q: How Does AWS Step Functions Work?

When you use Step Functions, you define state machines that describe your workflow as a series of steps, their relationships, and their inputs and outputs. State machines contain a number of states, each of which represents a step in a workflow diagram.  

States can perform work, make choices, pass parameters, initiate parallel execution, manage timeouts, or terminate your workflow with a success or failure.  

The visual console automatically graphs each state in the order of execution, making it easier to design multi-step applications. The console highlights the real-time status of each step and provides a detailed history of every execution.  

For more information, see **[How Step Functions Works](https://docs.aws.amazon.com/step-functions/latest/dg/how-step-functions-works.html)** in the Step Functions [**developer guide**](https://docs.aws.amazon.com/step-functions/latest/dg/how-step-functions-works.html).  

## Q: How Does Step Functions Connect to My Resources?

You can orchestrate any AWS service using [service integrations](https://docs.aws.amazon.com/step-functions/latest/dg/concepts-connectors.html) or any self-managed application component using [Activity Tasks](https://docs.aws.amazon.com/step-functions/latest/dg/concepts-activities.html).

[Service integrations](https://docs.aws.amazon.com/step-functions/latest/dg/concepts-connectors.html) help you construct calls to AWS services and include the response in your workflow. [AWS–SDK service integrations](https://aws.amazon.com/about-aws/whats-new/2021/09/aws-step-functions-200-aws-sdk-integration/) help you invoke one of over 9,000 AWS API actions from over 200 services directly from your workflow.  

Optimized service integrations further simplify use of common services such as [AWS Lambda](https://aws.amazon.com/lambda/), [Amazon Elastic Container Service (ECS)](https://aws.amazon.com/ecs/), [AWS Glue](https://aws.amazon.com/glue/), or [Amazon EMR](https://aws.amazon.com/emr/) with capabilities including IAM policy generation and the RunAJob pattern that will automatically wait for completion of asynchronous jobs.

[Activity Tasks](https://docs.aws.amazon.com/step-functions/latest/dg/concepts-activities.html) incorporate integration with activity works that you run in a location of your choice, including in [Amazon Elastic Compute Cloud (EC2)](https://aws.amazon.com/ec2/), in Amazon ECS, on a mobile device, or on an on-premises server. The activity worker polls Step Functions for work, takes any inputs from Step Functions, performs the work using your code, and returns results. Since activity workers request work, it is easier to use workers that are deployed behind a firewall.  

A Step Functions state machine can contain combinations of [service integrations](https://docs.aws.amazon.com/step-functions/latest/dg/concepts-connectors.html) and [Activity Tasks](https://docs.aws.amazon.com/step-functions/latest/dg/concepts-activities.html). Step Functions applications can also combine activity workers running in a data center with service tasks that run in the cloud. The workers in the data center continue to run as usual, along with any cloud-based service tasks.  

## Q: How Do I Get Started with Step Functions?

There are a number of ways you can get started with Step Functions:

- Explore [sample projects](https://console.aws.amazon.com/states/home?#/sampleProjects) in the Step Functions console
- Read through the [Step Functions Developer Guide](http://docs.aws.amazon.com/step-functions/latest/dg/welcome.html)
- Try our [10-minute tutorials](https://aws.amazon.com/step-functions/getting-started/#Tutorials)

## Q: What Language Does Step Functions Use?

AWS Step Functions state machines are defined in [JSON](https://aws.amazon.com/documentdb/what-is-json/) using the declarative [Amazon States Language](https://states-language.net/spec.html).  

To create an [activity worker](https://docs.aws.amazon.com/step-functions/latest/dg/concepts-activities.html), you may use any programming language, as long as you can communicate with Step Functions using [web service APIs](https://aws.amazon.com/what-is/api/).  

For convenience, you may use an AWS SDK in the language of your choosing. Lambda supports code written in [Node.js (JavaScript)](https://aws.amazon.com/developer/language/javascript/), [Python](https://aws.amazon.com/developer/language/python/), [Golang (Go)](https://aws.amazon.com/developer/language/go/), and C# (using the .NET Core runtime and other languages). For more information on the Lambda programming model, see the [Lambda Developer Guide](https://docs.aws.amazon.com/lambda/latest/dg/programming-model-v2.html).  

## Q: My Workflow Has Some of the Properties of Standard Workflows and Some Properties of Express Workflows. How Do I Get the Best of Both?

You can compose the two workflow types:  

- **By running Express Workflows as a child workflow of Standard Workflows**: The Express Workflow is invoked from a Task state in the parent orchestration workflow and succeeds or fails as a whole from the parent's perspective. It is subject to the parent's retry policy for that Task.  
    
- **By calling Express Workflows from within an Express Workflow, so long as all workflows do not exceed the duration limit of the parent**: You might choose to factor your workflows this way if your use case has a combination of long-running or exactly-once, and short-lived high-rate steps.  
    

## Q: How Does Step Functions Support Parallelism?

Step Functions includes a Map state for dynamic parallelism. The Map state has two operating modes, Inline and Distributed, and both modes execute the same set of steps for a collection of items. A Map in Inline mode can support concurrency of 40 parallel branches and execution history limits of 25,000 events or approximately 6,500 state transitions in a workflow. With the Distributed mode, you can run at concurrency of up to 10,000 parallel branches. The Distributed Map has been optimized for Amazon S3, helping you more easily iterate over objects in an S3 bucket. See the **[FAQ](https://aws.amazon.com/step-functions/faqs/#Integration)** in the integration section. The iterations of a Distributed Map are split into parallel executions to help you overcome payload and execution history limits. You can also choose whether each iteration is performed by a Standard Workflow, which is idempotent, or Express Workflow, which is a higher speed and lower cost, but not idempotent. Learn more about the **[Map state](https://docs.aws.amazon.com/step-functions/latest/dg/amazon-states-language-map-state.html)**.

## Comparisons

## Q: When Should I Use Step Functions vs. Amazon Simple Queue Service (SQS)?

You should use AWS Step Functions when you need to coordinate service components in the development of highly scalable and auditable applications. Amazon Simple Queue Service (Amazon SQS), is used for when you need a reliable, highly scalable, hosted queue for sending, storing, and receiving messages between services.

- Step Functions keeps track of all tasks and events in an application, SQS requires you to implement your own application-level tracking, especially if your application uses multiple queues.  
    
- The Step Functions console and visibility APIs provide an application-centric view that lets you search for executions, drill-down into an execution's detail, and administer executions. SQS would require implementing additional functionality.  
    
- Step Functions offers several features that facilitate application development, such as passing data between tasks and flexibility in distributing tasks, whereas SQS would require you to implement application-level functionality.  
    
- Step Functions has out-of-the-box capabilities to build workflows to coordinate your distributed application. SQS allows you to build basic workflows, but has limited functionality.  
    

## When Should I Use Step Functions vs. Amazon Simple Workflow Service (SWF)?

You should consider using Step Functions for all your new applications, since it provides a more productive and agile approach to coordinating application components using visual workflows. If you require external signals to intervene in your processes or you would like to launch child processes that return a result to a parent, then you should consider **[Amazon Simple Workflow Service (Amazon SWF).](https://aws.amazon.com/swf/)**  

With SWF, instead of writing state machines in declarative JSON, you can write a decider program to separate activity steps from decision steps. This provides you complete control over your orchestration logic, but increases the complexity of developing applications. You may write decider programs in the programming language of your choice, or you may use the Flow framework to use programming constructs that structure asynchronous interactions for you.  

## How Does Step Functions’ HTTPS Endpoints Integration Relate to Amazon EventBridge’s API Destinations?

Amazon EventBridge is a serverless service that uses events to connect application components together making it easier for developers to build scalable event-driven applications. API Destinations is a feature of EventBridge that enables you to create rules to forward events to third-party endpoints to decouple event producers and consumers.

AWS Step Functions’ HTTPS endpoints integration will enable you to invoke HTTPS-based services and receive a response that can be used to control the flow of your execution based on your business logic. Amazon EventBridge focuses on routing events, whereas Step Functions focuses on the orchestration of workflows and management of state. EventBridge API Destinations and Step Functions' HTTPS endpoints integration can support a connection for authentication, so you can reuse authentication credentials across services. Both services can be used together to build highly scalable and robust distributed applications.  

## Integration

## Q: How Does Step Functions Connect and Coordinate other AWS Services?

Workflows that you create with Step Functions can connect and coordinate over 200 AWS services using [**service integrations**](https://docs.aws.amazon.com/step-functions/latest/dg/concepts-connectors.html). For example, you can:

- Invoke an AWS Lambda function
- Run an ECS or AWS Fargate task
- Get an existing item from an Amazon DynamoDB table or put a new item into a DynamoDB table
- Submit an AWS Batch job and wait for it to complete
- Invoke Amazon Bedrock Foundation Model
- Publish a message to an SNS topic
- Send a message to an Amazon SQS queue
- Start an AWS Glue job run
- Create an Amazon SageMaker job to train a machine learning model or batch transform a data set

To learn more about using Step Functions to connect to other AWS services, see the **[Step Functions developer guide](https://docs.aws.amazon.com/step-functions/latest/dg/welcome.html)**. You can also create tasks in your state machines that run applications, see the FAQ in the [**Overview**](https://aws.amazon.com/step-functions/faqs//#Overview) section, _How does Step Functions connect to my resources?_

[For the most common use-cases of Step Functions, visit the use cases page, where there is detailed cases, alongside their architecture visualizations.](https://aws.amazon.com/step-functions/use-cases/)

## Q: How Does Step Functions Integrate with Third-party Applications?

Using AWS Step Functions’ HTTPS endpoints integration you can directly integrate with HTTP-based services, including SaaS applications. Using a visual interface, you can build and orchestrate distributed applications composed of AWS services and SaaS applications.  

## Q: How Can I Test, Analyze, or Debug My Executions?

You can use the TestState API to test a single step of your workflow, enabling faster feedback cycles to accelerate development. The TestState enables you to call services and endpoints directly, modify the input to mimic different scenarios, and review the response. You can access the TestState through Workflow Studio, making it easy to test as you build without the need to deploy your workflow. TestState accepts a single state definition and input, then synchronously returns the state output along with intermediate data transformations. After you run your workflow, you can analyze and debug executions through Amazon CloudWatch Logs, AWS X-Ray, and directly in the Step functions console through a visual operator experience that helps you quickly identify problem areas.   

## Q: How Can Step Functions Help Me Process a Large Dataset in Amazon S3?

You can create workflows using a Map state in Distributed mode to perform large-scale processing of data such as logs, media files, sales transactions, or IoT sensor data. Step Functions will iterate through the items and start up parallel workflow executions instantly allowing you to build on-demand data processing at scale. The Distributed Map state has been optimized to work with S3. You can specify an S3 bucket with filter criteria, a S3 manifest file, JSON collection or CSV file stored in S3 as inputs for your workflow. You can also specify a S3 bucket for the execution outputs of a Distributed Map.

## How Does Step Functions Work with Amazon API Gateway?

You can associate your Step Functions APIs with [Amazon API Gateway](https://aws.amazon.com/api-gateway/) so that these APIs invoke your state machines when an HTTPS request is sent to an API method that you define.  

You can use an API Gateway API to start Step Functions state machines that coordinate the components of a distributed backend application, and **[integrate human activity tasks](https://aws.amazon.com/blogs/compute/implementing-serverless-manual-approval-steps-in-aws-step-functions-and-amazon-api-gateway/)** into the steps of your application such as approval requests and responses.  

You can also make serverless asynchronous calls to the APIs of services that your application uses. For more information, try our tutorial, **[Creating a Step Functions API Using API Gateway](https://docs.aws.amazon.com/step-functions/latest/dg/tutorial-api-gateway.html)**.  

## Q: How Does AWS Step Functions Work with Amazon EventBridge?

Choregraphy and orchestration are two different models for how distributed services can communicate with one another. In orchestration, communication is more tightly controlled and Step Functions, an orchestration service, coordinates the interaction and order in which services are invoked.  

Choreography achieves communication without tight control. With [Amazon EventBridge](https://aws.amazon.com/eventbridge/) events flow between services without centralized coordination. Many applications use both choreography and orchestration for different use cases.   

Examples of how you may use Step Functions and EventBridge together could include sending an event or creating a schedule with [EventBridge Scheduler](https://aws.amazon.com/eventbridge/scheduler/) to trigger an AWS Step Functions workflow, followed by emitting events at different steps of your workflow.  

## What is AWS Step Functions vs. AWS Lambda

AWS Lambda is a serverless, event-driven compute service that lets you run code for virtually any type of application or backend service without provisioning or managing servers. Step Functions is a serverless orchestration service that lets you easily coordinate multiple Lambda functions into flexible workflows that are easy to debug and change. Step Functions will keep your Lambda functions free of additional logic by triggering and tracking each step of your application for you.  

## Is AWS Step Functions Serverless?

Yes, Step Functions is a serverless orchestration service. Step Functions automatically scales the operations and underlying compute to run the steps of your application for you in response to changing workloads. Step Functions has built-in fault tolerance and maintains service capacity across multiple Availability Zones in each region to protect applications against individual machine or data center failures. This helps ensure high availability for both the service itself and for the application workflow it operates.  

Step Functions offers pay-for-use billing model to increase agility and optimize costs. Learn more about [Step Functions Pricing](https://aws.amazon.com/step-functions/pricing/).

## Q: How Does Logging and Monitoring Work for Step Functions?

AWS Step Functions sends metrics to [Amazon CloudWatch](https://aws.amazon.com/cloudwatch/) and [AWS CloudTrail](https://aws.amazon.com/cloudtrail/) for application monitoring. CloudWatch collects and track metrics, sets alarms, and automatically reacts to changes in AWS Step Functions.  

CloudTrail captures all API calls for Step Functions as events, including calls from the Step Functions console and from code calls to the Step Functions APIs. Step Functions also supports CloudWatch Events **[managed rules](https://docs.aws.amazon.com/AmazonCloudWatch/latest/events/CloudWatch-Events-Managed-Rules.html)** for each integrated service in your workflow, and will create and manage CloudWatch Events rules in your AWS account as needed.  

For more information, see [**monitoring and logging**](https://docs.aws.amazon.com/step-functions/latest/dg/monitoring-logging.html) in the Step Functions developer guide.  

## Q: What Happens if My Express Workflow Fails due to Exhausted Retries or an Unmanaged Exception?

By default, Express Workflows report all outcomes to CloudWatch Logs including workflow input, output, and completed steps. You may select different levels of logging to only log errors, and you can choose to not log input and output. Workflows that exhaust retries or have an unmanaged exception should be re-run from the start.

## Q: How Does Step Functions Help You Build Generative AI Applications?

Step Functions has an optimized integration with [Amazon Bedrock](https://aws.amazon.com/bedrock/). You can invoke Bedrock’s Foundation Models directly from your Step Functions’ workflow using natural language. This gives you the ability to:   

- Enrich your data processed by Step Functions with generative AI capabilities to reduce the complexity of handling your data, such as text summarization, image generation, or personalization.
- Retrieve information from databases such as your latest product pricing and user personalization data and use Step Functions intrinsic functions to inject it into the prompt, making sure the LLM uses the most current data to improve the accuracy of the response.
- Generate embeddings by having Step Functions go through docs, extract data, chunk the documents, and then transform the data from digital text to embedding as a multi-step process. This can be scheduled as a recurring process.
- Use Step Function workflows for prompt chaining. You can orchestrate multiple LLM calls and choose the best model for each stage of the chain, forming a customized chain of processing stages, curating more contextually-aware and accurate responses from the foundational model.
- Build Human-in-the-loop (HITL) interactions with your generative AI workflow to moderate answers to avoid hallucination or build in logic to handle responses that are not supported by the foundational model.

## Security

## Q: Can I Access Step Functions from Resources behind My Amazon VPC without Connecting to the Internet?

Step Functions also supports VPC Endpoints (VPCE) using [AWS PrivateLink](https://docs.aws.amazon.com/whitepapers/latest/aws-vpc-connectivity-options/aws-privatelink.html). You can access Step Functions from VPC-enabled [AWS Lambda](https://aws.amazon.com/lambda/) functions and other AWS services without traversing the public internet.  

For more information, refer to the [Amazon VPC Endpoints for Step Functions in the Step Functions developer guide.](https://docs.aws.amazon.com/step-functions/latest/dg/vpc-endpoints.html)  

## Compliance

## Q: What Are the compliance Standards Supported by Step Functions?

Step Functions conforms to HIPAA, FedRAMP, SOC, GDPR, and other common compliance standards. See the **[AWS Cloud Security](https://aws.amazon.com/compliance/services-in-scope/)** site to get a detailed list of supported compliance standards.



# Tutorial: Learn to Use the AWS Step Functions Workflow StudioDeveloper Guide

In this tutorial, you will learn the basics of working with Workflow Studio for AWS Step Functions. In [Design mode](https://docs.aws.amazon.com/step-functions/latest/dg/workflow-studio-components.html#wfs-interface-design-mode) of Workflow Studio, you'll create a state machine containing multiple states, including `Pass`, `Choice`, `Fail`, `Wait`, and `Parallel`. You'll use the drag and drop feature to search for, select, and configure these states. Then, you'll view the auto-generated [Amazon States Language](https://docs.aws.amazon.com/step-functions/latest/dg/concepts-amazon-states-language.html) (ASL) definition of your workflow. You'll also use the [Code mode](https://docs.aws.amazon.com/step-functions/latest/dg/workflow-studio-components.html#wfs-interface-code-mode) of Workflow Studio to edit the workflow definition. Then, you'll exit Workflow Studio, run the state machine, and review the execution details.

In this tutorial, you'll also learn how to update the state machine and view the changes in the execution output. Finally, you'll perform a clean-up step and delete your state machine.

After you complete this tutorial, you'll know how to use Workflow Studio to create and configure a workflow using both the **Design** and **Code** modes. You'll also know how to update, run, and delete your state machine.

###### Topics

- [Step 1: Navigate to Workflow Studio](https://docs.aws.amazon.com/step-functions/latest/dg/tutorial-workflow-studio-using.html#tutorial-open-wf-studio)
- [Step 2: Create a state machine](https://docs.aws.amazon.com/step-functions/latest/dg/tutorial-workflow-studio-using.html#tutorial-workflow-studio-using-create)
- [Step 3: Review the auto-generated Amazon States Language definition](https://docs.aws.amazon.com/step-functions/latest/dg/tutorial-workflow-studio-using.html#tutorial-wf-studio-review-asl-def)
- [Step 4: Edit the workflow definition in Code mode](https://docs.aws.amazon.com/step-functions/latest/dg/tutorial-workflow-studio-using.html#tutorial-wf-studio-edit-asl-code)
- [Step 5: Save the state machine](https://docs.aws.amazon.com/step-functions/latest/dg/tutorial-workflow-studio-using.html#tutorial-wf-studio-save-wflow)
- [Step 6: Run the state machine](https://docs.aws.amazon.com/step-functions/latest/dg/tutorial-workflow-studio-using.html#tutorial-workflow-studio-using-start)
- [Step 7: Update your state machine](https://docs.aws.amazon.com/step-functions/latest/dg/tutorial-workflow-studio-using.html#tutorial-workflow-studio-using-update)
- [Step 8: Clean up](https://docs.aws.amazon.com/step-functions/latest/dg/tutorial-workflow-studio-using.html#tutorial-workflow-studio-using-cleanup)

## Step 1: Navigate to Workflow Studio

1. Open the [Step Functions console](https://console.aws.amazon.com/states/home) and choose **Create state machine**.
    
2. In the **Choose a template** dialog box, select **Blank**.
    
3. Choose **Select**. This opens Workflow Studio in [Design mode](https://docs.aws.amazon.com/step-functions/latest/dg/workflow-studio-components.html#wfs-interface-design-mode).
    

## Step 2: Create a State Machine

In Workflow Studio, a state machine is a graphical representation of your workflow. With Workflow Studio, you can define, configure, and examine the individual steps of your workflow. In the following steps, you use the [Design mode](https://docs.aws.amazon.com/step-functions/latest/dg/workflow-studio-components.html#wfs-interface-design-mode) of Workflow Studio to create your state machine.

###### To Create a State Machine

1. Make sure you're in the **Design** mode of Workflow Studio.
    
2. From the [States browser](https://docs.aws.amazon.com/step-functions/latest/dg/workflow-studio-components.html#workflow-studio-components-states) on the left, choose the **Flow** tab. Then, drag a **Pass** state to the empty state labelled **Drag first state here**.
    
3. Drag a **Choice** state from the **Flow** tab and drop it below the **Pass** state.
    
4. For **State name**, replace the default name of **Choice**. For this tutorial, use the name `IsHelloWorldExample`.
    
5. Drag another **Pass** state and drop it to one branch of the **IsHelloWorldExample** state. Then, drag a **Fail** state and drop it below the other branch of the **IsHelloWorldExample** state.
    
6. Choose the **Pass (1)** state, and rename it to `Yes`. Rename the **Fail** state as `No`.
    
7. Specify the **IsHelloWorldExample** state's branching logic using the boolean variable `IsHelloWorldExample`.
    
    If `IsHelloWorldExample` is `False`, the workflow will enter the **No** state. Otherwise, the workflow will continue its execution flow in the **Yes** state.
    
    To define the branching logic, do the following:
    
    1. Choose the **IsHelloWorldExample** state on the [Canvas](https://docs.aws.amazon.com/step-functions/latest/dg/workflow-studio-components.html#workflow-studio-components-grapheditor), and then under **Choice Rules,** choose the edit icon in the **Rule #1** box to define the first choice rule.
        
    2. Choose **Add conditions**.
        
    3. In the **Conditions for rule #1** dialog box, enter `$.IsHelloWorldExample` under **Variable**.
        
    4. Choose **is equal to** under **Operator**.
        
    5. Choose **Boolean constant** under **Value**, and then choose **true** from the dropdown list.
        
    6. Choose **Save conditions**.
        
    7. Make sure the **Then next state is:** dropdown list has **Yes** selected.
        
    8. Choose **Add new choice rule**, then choose **Add conditions**.
        
    9. In the **Rule #2** box, define the second choice rule when the `IsHelloWorldExample` variable's value is false by repeating substeps 7.c through 7.f. For step 7.e, choose **false** instead of **true**.
        
    10. In the **Rule #2** box, choose **No** from the **Then next state is:** dropdown list.
        
    11. In the **Default rule** box, choose the edit icon to define the default choice rule, and then choose **Yes** from the dropdown list.
        
8. Add a **Wait** state after the **Yes** state, and name it `Wait 3 sec`. Then, configure the wait time to be three seconds by doing the following steps:
    
    1. Under **Options**, keep the default selection of **Wait for a fixed interval**.
        
    2. Under **Seconds**, make sure **Enter seconds** is selected, and then enter `3` in the box.
        
9. After the **Wait 3 sec** state, add a **Parallel** state. Add two **Pass** states in its two branches. Name the first **Pass** state `Hello`. Name the second **Pass** state `World`.
    
    The completed workflow will look like this:
    
    ![  
    The completed workflow for the IsHelloWorldExample state  
    machine.  
    ](https://docs.aws.amazon.com/images/step-functions/latest/dg/images/wfs_tutorial_result_01.png)
    

## Step 3: Review the Auto-generated Amazon States Language Definition

As you drag and drop states from the **Flow** tab onto the canvas, Workflow Studio automatically composes the [Amazon States Language](https://docs.aws.amazon.com/step-functions/latest/dg/concepts-amazon-states-language.html) (ASL) definition of your workflow in real-time. In the [Inspector](https://docs.aws.amazon.com/step-functions/latest/dg/workflow-studio-components.html#workflow-studio-components-formdefinition) panel, choose the **Definition** toggle button to view this definition or switch to the [Code mode](https://docs.aws.amazon.com/step-functions/latest/dg/workflow-studio-components.html#wfs-interface-code-mode) to edit this definition as required. For information about editing the workflow definition, see [Step 4](https://docs.aws.amazon.com/step-functions/latest/dg/tutorial-workflow-studio-using.html#tutorial-wf-studio-edit-asl-code) of this tutorial.

- (Optional) Choose **Definition** on the **Inspector** panel and view the state machine's workflow.
    
    The following example code shows the auto-generated Amazon States Language definition for the `IsHelloWorldExample` state machine. The `Choice` state that you added in Workflow Studio is used to determine the execution flow based on [the branching logic you defined in Step 2](https://docs.aws.amazon.com/step-functions/latest/dg/tutorial-workflow-studio-using.html#tutorial-workflow-studio-using-create).
    
    ```
    <span>{</span>
      <span>"Comment"</span>: <span>"A Hello World example of the Amazon States Language using Pass states"</span>,
      <span>"StartAt"</span>: <span>"Pass"</span>,
      <span>"States"</span>: <span>{</span>
        <span>"Pass"</span>: <span>{</span>
          <span>"Type"</span>: <span>"Pass"</span>,
          <span>"Next"</span>: <span>"IsHelloWorldExample"</span>,
          <span>"Comment"</span>: <span>"A Pass state passes its input to its output, without performing work. Pass states are useful when constructing and debugging state machines."</span>
        },
        <span>"IsHelloWorldExample"</span>: <span>{</span>
          <span>"Type"</span>: <span>"Choice"</span>,
          <span>"Comment"</span>: <span>"A Choice state adds branching logic to a state machine. Choice rules can implement 16 different comparison operators, and can be combined using And, Or, and Not\""</span>,
          <span>"Choices"</span>: [
            <span>{</span>
              <span>"Variable"</span>: <span>"$.IsHelloWorldExample"</span>,
              <span>"BooleanEquals"</span>: <span>false</span>,
              <span>"Next"</span>: <span>"No"</span>
            },
            <span>{</span>
              <span>"Variable"</span>: <span>"$.IsHelloWorldExample"</span>,
              <span>"BooleanEquals"</span>: <span>true</span>,
              <span>"Next"</span>: <span>"Yes"</span>
            }
          ],
          <span>"Default"</span>: <span>"Yes"</span>
        },
        <span>"No"</span>: <span>{</span>
          <span>"Type"</span>: <span>"Fail"</span>,
          <span>"Cause"</span>: <span>"Not Hello World"</span>
        },
        <span>"Yes"</span>: <span>{</span>
          <span>"Type"</span>: <span>"Pass"</span>,
          <span>"Next"</span>: <span>"Wait 3 sec"</span>
        },
        <span>"Wait 3 sec"</span>: <span>{</span>
          <span>"Type"</span>: <span>"Wait"</span>,
          <span>"Seconds"</span>: <span>3</span>,
          <span>"Next"</span>: <span>"Parallel"</span>
        },
        <span>"Parallel"</span>: <span>{</span>
          <span>"Type"</span>: <span>"Parallel"</span>,
          <span>"End"</span>: <span>true</span>,
          <span>"Branches"</span>: [
            <span>{</span>
              <span>"StartAt"</span>: <span>"Hello"</span>,
              <span>"States"</span>: <span>{</span>
                <span>"Hello"</span>: <span>{</span>
                  <span>"Type"</span>: <span>"Pass"</span>,
                  <span>"End"</span>: <span>true</span>
                }
              }
            },
            <span>{</span>
              <span>"StartAt"</span>: <span>"World"</span>,
              <span>"States"</span>: <span>{</span>
                <span>"World"</span>: <span>{</span>
                  <span>"Type"</span>: <span>"Pass"</span>,
                  <span>"End"</span>: <span>true</span>
                }
              }
            }
          ]
        }
      }
    }
    ```
    

## Step 4: Edit the Workflow Definition in Code Mode

The **Code** mode of Workflow Studio provides an integrated code editor to view and edit the ASL definition of your workflows.

1. Choose **Code** to switch to the **Code** mode.
    
2. After the **Parallel** state's definition, place the cursor and press `Enter`.
    
3. Press `Ctrl+space` to see the list of states that you can add after the **Parallel** state.
    
4. Choose **Pass State** from the list of options. The code editor adds boilerplate code for the **Pass State**.
    
5. The addition of this state results in errors in your workflow definition. In the **Parallel** state's definition, replace `"End": true` with `` `"Next": "PassState"` ``.
    
6. In the **Pass State** definition you added, make the following changes:
    
    1. Remove the **Result** node.
        
    2. Remove `"ResultPath": "$.result",` and `"Next": "NextState"`.
        
    3. After `"Type": "Pass",`, enter `` `"End": true` ``.
        
    4. Add a `,` after the **Pass State** definition.
        

Your workflow definition should now look similar to the following definition.

```
<span>{</span>
  <span>"Comment"</span>: <span>"A description of my state machine"</span>,
  <span>"StartAt"</span>: <span>"Pass"</span>,
  <span>"States"</span>: <span>{</span>
    <span>"Pass"</span>: <span>{</span>
      <span>"Type"</span>: <span>"Pass"</span>,
      <span>"Next"</span>: <span>"IsHelloWorldExample"</span>
    },
    <span>"IsHelloWorldExample"</span>: <span>{</span>
      <span>"Type"</span>: <span>"Choice"</span>,
      <span>"Choices"</span>: [
        <span>{</span>
          <span>"Variable"</span>: <span>"$.IsHelloWorldExample"</span>,
          <span>"BooleanEquals"</span>: <span>true</span>,
          <span>"Next"</span>: <span>"Yes"</span>
        },
        <span>{</span>
          <span>"Variable"</span>: <span>"$.IsHelloWorldExample"</span>,
          <span>"BooleanEquals"</span>: <span>false</span>,
          <span>"Next"</span>: <span>"No"</span>
        }
      ],
      <span>"Default"</span>: <span>"Yes"</span>
    },
    <span>"Yes"</span>: <span>{</span>
      <span>"Type"</span>: <span>"Pass"</span>,
      <span>"Next"</span>: <span>"Wait 3 seconds"</span>
    },
    <span>"Wait 3 seconds"</span>: <span>{</span>
      <span>"Type"</span>: <span>"Wait"</span>,
      <span>"Seconds"</span>: <span>3</span>,
      <span>"Next"</span>: <span>"Parallel"</span>
    },
    <span>"Parallel"</span>: <span>{</span>
      <span>"Type"</span>: <span>"Parallel"</span>,
      <span>"Branches"</span>: [
        <span>{</span>
          <span>"StartAt"</span>: <span>"Hello"</span>,
          <span>"States"</span>: <span>{</span>
            <span>"Hello"</span>: <span>{</span>
              <span>"Type"</span>: <span>"Pass"</span>,
              <span>"End"</span>: <span>true</span>
            }
          }
        },
        <span>{</span>
          <span>"StartAt"</span>: <span>"World"</span>,
          <span>"States"</span>: <span>{</span>
            <span>"World"</span>: <span>{</span>
              <span>"Type"</span>: <span>"Pass"</span>,
              <span>"End"</span>: <span>true</span>
            }
          }
        }
      ],
      <span>"Next"</span>: <span>"PassState"</span>
    },
    <span>"PassState"</span>: <span>{</span>
      <span>"Type"</span>: <span>"Pass"</span>,
      <span>"End"</span>: <span>true</span>
    },
    <span>"No"</span>: <span>{</span>
      <span>"Type"</span>: <span>"Fail"</span>
    }
  }
}
```

## Step 5: Save the State Machine

1. Choose the **Config** more or choose the edit icon next to the default state machine name of **MyStateMachine**. In **State machine configuration**, specify a name. For example, enter `HelloWorld`.
    
2. (Optional) Specify other workflow settings, such as state machine type and its execution role. For this tutorial, keep all the default selections in **State machine configuration**.
    
3. Choose **Create**.
    
4. In the **Confirm role creation** dialog box, choose **Confirm** to continue.
    
    You can also choose **View role configuration** to go back to the **Config** mode.
    

For more information about the **Config** mode, see [Config mode of Workflow Studio](https://docs.aws.amazon.com/step-functions/latest/dg/workflow-studio-components.html#wfs-interface-config-mode).

## Step 6: Run the State Machine

State machine executions are instances where you run your workflow to perform tasks.

1. On the **State machines** page, choose the **HelloWorld** state machine.
    
2. On the **HelloWorld** page, choose **Start execution**.
    
3. (Optional) To identify your execution, you can specify a name for it in the **Name** box. By default, Step Functions generates a unique execution name automatically.
    
###### Note
    
    Step Functions allows you to create names for state machines, executions, and activities, rate controls, and labels that contain non-ASCII characters. These non-ASCII names don't work with Amazon CloudWatch. To ensure that you can track CloudWatch metrics, choose a name that uses only ASCII characters.
    
4. In the **Input** box, enter input values for your execution in JSON format. Based on your input, the `IsHelloWorldExample` variable determines which state machine flow will be executed. For now, use the following input value:
    
    ```
    <span>{</span>
       <span>"IsHelloWorldExample"</span>: <span>true</span>
    }
    ```
    
###### Note
    
    While specifying an execution input is optional, in this tutorial, it is mandatory to specify an execution input similar to the above example input. This input value is referenced in the `Choice` state when you run the state machine.
    
5. Choose **Start execution**.
    
1. The Step Functions console directs you to a page that's titled with your execution ID. This page is known as the _Execution Details_ page. On this page, you can review the execution results as the execution progresses or after it's complete.
    
    To review the execution results, choose individual states on the **Graph view**, and then choose the individual tabs on the [Step details](https://docs.aws.amazon.com/step-functions/latest/dg/exec-details-interface-overview.html#exec-details-intf-step-details) pane to view each state's details including input, output, and definition respectively. For details about the execution information you can view on the _Execution Details_ page, see [Execution Details page – Interface overview](https://docs.aws.amazon.com/step-functions/latest/dg/exec-details-interface-overview.html).
    
    For this tutorial, if you entered an input value of `"IsHelloWorldExample": true`, you should see the following output:
    
    ```
    <span>{</span>
       <span>"IsHelloWorldExample"</span>: <span>true</span>
    },
    <span>{</span>
       <span>"IsHelloWorldExample"</span>: <span>true</span>
    }
    ```
    

## Step 7: Update Your State Machine

When you update a state machine, your updates are _eventually consistent_. After a short amount of time, all newly started executions will reflect your state machine's updated definition. All currently running executions will run to completion under the previous definition.

In this step, you'll update your state machine in the [Design mode](https://docs.aws.amazon.com/step-functions/latest/dg/workflow-studio-components.html#wfs-interface-design-mode) mode of Workflow Studio. You'll add a `Result` field in the **Pass** state named **World**.

1. On the page titled with your execution ID, choose **Edit state machine**.
    
2. Make sure you're in the **Design** mode.
    
3. Choose the **Pass** state named **World** on the canvas, and then choose **Output**.
    
4. In the **Result** box, enter `"World has been updated!"`.
    
5. Choose **Save**.
    
6. (Optional) In the **Definition** area, view the updated Amazon States Language definition of your workflow.
    
    ```
    <span>{</span>
          <span>"Type"</span>: <span>"Parallel"</span>,
          <span>"End"</span>: <span>true</span>,
          <span>"Branches"</span>: [
            <span>{</span>
              <span>"StartAt"</span>: <span>"Hello"</span>,
              <span>"States"</span>: <span>{</span>
                <span>"Hello"</span>: <span>{</span>
                  <span>"Type"</span>: <span>"Pass"</span>,
                  <span>"End"</span>: <span>true</span>
                }
              }
            },
            <span>{</span>
              <span>"StartAt"</span>: <span>"World"</span>,
              <span>"States"</span>: <span>{</span>
                <span>"World"</span>: <span>{</span>
                  <span>"Type"</span>: <span>"Pass"</span>,
                  <span>"Result"</span>: <span>"World has been updated!"</span>,
                  <span>"End"</span>: <span>true</span>
                }
              }
            }
          ],
          <span>"Next"</span>: <span>"PassState"</span>
        }
    ```
    
7. Choose **Execute**.
    
8. In the **Start execution** dialog box that opens in a new tab, provide the following execution input.
    
    ```
    <span>{</span>
       <span>"IsHelloWorldExample"</span>: <span>true</span>
    }
    ```
    
9. Choose **Start Execution**.
    
10. (Optional) In the **Graph view**, choose the **World** step, and then choose **Output**. The output is **World has been updated!**
    

## Step 8: Clean up

###### To Delete Your State Machine

1. From the navigation menu, choose **State machines**.
    
2. On the **State machines** page, select **HelloWorld**, and then choose **Delete**.
    
3. In the **Delete state machine** dialog box, type `delete` to confirm deletion.
    
4. Choose **Delete**.
    
    If deletion is successful, a green status bar appears at the top of your screen. The green status bar tells you that your state machine is marked for deletion. Your state machine will be deleted when all of its in-progress executions stop running.
    

###### To Delete Your Execution Role

1. Open the [Roles page](https://console.aws.amazon.com/iam/home?#/roles) for IAM.
    
2. Choose the IAM role that Step Functions created for you. For example, **StepFunctions-HelloWorld-role-EXAMPLE**.
    
3. Choose **Delete role**.
    
4. Choose **Yes, delete**.