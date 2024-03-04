---
tags:
  - cloud/aws
---
**AWS Lambda** <mark style="background: #FFB86CA6;">lets you run code as functions without provisioning or managing servers.</mark>  
![[Pasted image 20240214115704.png]]
- Lambda-based applications are <mark style="background: #ABF7F7A6;">composed of functions triggered by events.</mark>
- With serverless computing, your application still runs on servers, but all the server management is done by AWS.
- <mark style="background: #FFF3A3A6;">You cannot log in to the compute instances that run Lambda functions or customize the operating system or language runtime.</mark>  
![[Pasted image 20240214120046.png]]  
![](https://i.imgur.com/UfeZ1zi.png)

**Lambda functions**:
- Consist of code and any associated dependencies.
- Configuration information is associated with the function.
- You specify the configuration information when you create the function.
- API provided for updating configuration data.

You specify the amount of memory you need allocated to your Lambda functions.  
<mark style="background: #FFF3A3A6;">AWS Lambda allocates CPU power proportional to the memory you specify using the same ratio as a general purpose EC2 instance type.</mark>

Functions can access:
- AWS services or non-AWS services.
- AWS services running in VPCs (e.g. RedShift, Elasticache, RDS instances).
- Non-AWS services running on EC2 instances in an AWS VPC.

<mark style="background: #CACFD9A6;">To enable your Lambda function to access resources inside your private VPC</mark>, <mark style="background: #BBFABBA6;">you must provide additional VPC-specific configuration information that includes VPC subnet IDs and security group IDs.</mark>

<mark style="background: #ADCCFFA6;">AWS Lambda uses this information to set up elastic network interfaces (ENIs) that enable your function.</mark>

<mark style="background: #FFB8EBA6;">You can request additional memory in 1 MB increments from 128 MB to 10240 MB.</mark>

There is a maximum execution timeout.
- Max is 15 minutes (900 seconds), default is 3 seconds.
- You pay for the time it runs.
- Lambda terminates the function at the timeout.  
![[Pasted image 20240214115804.png]]

![](https://i.imgur.com/8X6LpHU.png)  
![](https://i.imgur.com/q6qt8lr.png)


Code is invoked using API calls made using AWS SDKs.

- Lambda assumes an IAM role when it executes the function.

AWS Lambda stores code in Amazon S3 and encrypts it at rest.

Lambda provides continuous scaling – scales out not up.

Lambda scales concurrently executing functions up to your default limit (1000).

Lambda can scale up to tens of thousands of concurrent executions.

Lambda functions are serverless and independent, 1 event = 1 function.

Functions can trigger other functions so 1 event can trigger multiple functions.

Use cases fall within the following categories:

- Using Lambda functions with AWS services as event sources.
- On-demand Lambda function invocation over HTTPS using Amazon API Gateway (custom REST API and endpoint).
- On-demand Lambda function invocation using custom applications (mobile, web apps, clients) and AWS SDKs, AWS Mobile SDKs, and the AWS Mobile SDK for Android.
- Scheduled events can be configured to run code on a scheduled basis through the AWS Lambda Console.

## Invoking Lambda Functions

You can invoke Lambda functions directly with the Lambda console, the Lambda API, the AWS SDK, the AWS CLI, and AWS toolkits.

You can also configure other AWS services to invoke your function, or you can configure Lambda to read from a stream or queue and invoke your function.

When you invoke a function, you can choose to invoke it synchronously or asynchronously.

Other AWS services and resources invoke your function directly.

For example, you can configure CloudWatch Events to invoke your function on a timer, or you can configure Amazon S3 to invoke your function when an object is created.

Each service varies in the method it uses to invoke your function, the structure of the event, and how you configure it.

### Synchronous Invocation

You wait for the function to process the event and return a response.

When you invoke a function synchronously, Lambda runs the function and waits for a response.

When the function execution ends, Lambda returns the response from the function’s code with additional data, such as the version of the function that was executed. To invoke a function synchronously with the AWS CLI, use the invoke command.

$ aws lambda invoke –function-name my-function –payload ‘{ “key”: “value” }’ response.json { “ExecutedVersion”: “$LATEST”, “StatusCode”: 200 }

### Asynchronous Invocation

When you invoke a function asynchronously, you don’t wait for a response from the function code.

For asynchronous invocation, Lambda handles retries and can send invocation records to a destination.

For asynchronous invocation, Lambda places the event in a queue and returns a success response without additional information. A separate process reads events from the queue and sends them to your function. To invoke a function asynchronously, set the invocation type parameter to Event.

$ aws lambda invoke --function-name my-function --invocation-type Event --payload '{ "key": "value" }' response.json { "StatusCode": 202 }

The output file (response.json) doesn’t contain any information but is still created when you run this command. If Lambda can’t add the event to the queue, the error message appears in the command output.

## Event Source Mappings

Lambda is an event-driven compute service where AWS Lambda runs code in response to events such as changes to data in an S3 bucket or a DynamoDB table.

An event source is an AWS service or developer-created application that produces events that trigger an AWS Lambda function to run.

You can use event source mappings to process items from a stream or queue in services that don’t invoke Lambda functions directly.

Supported AWS event sources include:

- [**Amazon S3**](https://docs.aws.amazon.com/lambda/latest/dg/invoking-lambda-function.html#supported-event-source-s3).
- [**Amazon DynamoDB**](https://docs.aws.amazon.com/lambda/latest/dg/invoking-lambda-function.html#supported-event-source-dynamo-db).
- [**Amazon Kinesis Data Streams**](https://docs.aws.amazon.com/lambda/latest/dg/invoking-lambda-function.html#supported-event-source-kinesis-streams).
- [**Amazon Simple Notification Service**](https://docs.aws.amazon.com/lambda/latest/dg/invoking-lambda-function.html#supported-event-source-sns).
- [**Amazon Simple Email Service**](https://docs.aws.amazon.com/lambda/latest/dg/invoking-lambda-function.html#supported-event-source-ses).
- [**Amazon Simple Queue Service**](https://docs.aws.amazon.com/lambda/latest/dg/invoking-lambda-function.html#supported-event-source-sqs).
- [**Amazon Cognito**](https://docs.aws.amazon.com/lambda/latest/dg/invoking-lambda-function.html#supported-event-source-cognito).
- [**AWS CloudFormation**](https://docs.aws.amazon.com/lambda/latest/dg/invoking-lambda-function.html#supported-event-source-cloudformation).
- [**Amazon CloudWatch Logs**](https://docs.aws.amazon.com/lambda/latest/dg/invoking-lambda-function.html#supported-event-source-cloudwatch-logs).
- [**Amazon CloudWatch Events**](https://docs.aws.amazon.com/lambda/latest/dg/invoking-lambda-function.html#supported-event-source-cloudwatch-events).
- [**AWS CodeCommit**](https://docs.aws.amazon.com/lambda/latest/dg/invoking-lambda-function.html#supported-event-source-codecommit).
- [**AWS Config**](https://docs.aws.amazon.com/lambda/latest/dg/invoking-lambda-function.html#supported-event-source-config).
- [**Amazon Alexa**](https://docs.aws.amazon.com/lambda/latest/dg/invoking-lambda-function.html#supported-event-source-echo).
- [**Amazon Lex**](https://docs.aws.amazon.com/lambda/latest/dg/invoking-lambda-function.html#supported-event-source-lex).
- [**Amazon API Gateway**](https://docs.aws.amazon.com/lambda/latest/dg/invoking-lambda-function.html#supported-event-source-api-gateway).
- [**AWS IoT Button**](https://docs.aws.amazon.com/lambda/latest/dg/invoking-lambda-function.html#supported-event-source-iot-button).
- [**Amazon CloudFront**](https://docs.aws.amazon.com/lambda/latest/dg/invoking-lambda-function.html#supported-event-source-cloudfront).
- [**Amazon Kinesis Data Firehose**](https://docs.aws.amazon.com/lambda/latest/dg/invoking-lambda-function.html#supported-event-source-kinesis-firehose).
- [**Other Event Sources: Invoking a Lambda Function On Demand**](https://docs.aws.amazon.com/lambda/latest/dg/invoking-lambda-function.html#api-gateway-with-lambda).

Other event sources can invoke Lambda functions on-demand.

Applications need permissions to invoke Lambda functions.

Lambda can run code in response to HTTP requests using Amazon API gateway or API calls made using the AWS SDKs.

Services that Lambda reads events from:

- [**Amazon Kinesis**](https://docs.aws.amazon.com/lambda/latest/dg/with-kinesis.html)
- [**Amazon DynamoDB**](https://docs.aws.amazon.com/lambda/latest/dg/with-ddb.html)
- [**Amazon Simple Queue Service**](https://docs.aws.amazon.com/lambda/latest/dg/with-sqs.html)

An event source mapping uses permissions in the function’s [**execution role**](https://docs.aws.amazon.com/lambda/latest/dg/lambda-intro-execution-role.html) to read and manage items in the event source.

Permissions, event structure, settings, and polling behavior vary by event source.

To process items from a stream or queue, you can create an event source mapping.

Each event that your function processes can contain hundreds or thousands of items.

The configuration of the event source mapping for stream-based services (DynamoDB, Kinesis), and Amazon SQS, is made on the Lambda side.

**_Note:_** _for other services such as Amazon S3 and SNS, the function is invoked asynchronously, and the configuration is made on the source (S3/SNS) rather than Lambda._

## Lambda Versions

Versioning means you can have multiple versions of your function.

You can use versions to manage the deployment of your AWS Lambda functions.  For example, you can publish a new version of a function for beta testing without affecting users of the stable production version.

The function version includes the following information:

- The function code and all associated dependencies.
- The Lambda runtime that executes the function.
- All the function settings, including the environment variables.
- A unique Amazon Resource Name (ARN) to identify this version of the function.

You work on $LATEST which is the latest version of the code – this is mutable (changeable).

When you’re ready to publish a Lambda function you create a version (these are numbered).

Numbered versions are assigned a number starting with 1 and subsequent versions are incremented by 1.

Versions are immutable (code cannot be edited).

Each version has its own ARN.

Because different versions have unique ARNs this allows you to effectively manage them for different environments like Production, Staging or Development.

A qualified ARN has a version suffix.

An unqualified ARN does not have a version suffix.

You cannot create an alias from an unqualified ARN.

## Lambda Aliases

- Lambda aliases are pointers to a specific Lambda version.
- Using an alias you can invoke a function without having to know which version of the function is being referenced.
- Aliases are mutable.
- Aliases enable stable configuration of event triggers / destinations.
- Aliases also have static ARNs but can point to any version of the same function.
- Aliases can also be used to split traffic between Lambda versions (blue/green).

Aliases enable blue / green deployment by assigning weights to Lambda version (doesn’t work for $LATEST, you need to create an alias for $LATEST).

## Traffic Shifting

With the introduction of alias traffic shifting, it is now possible to trivially implement canary deployments of Lambda functions.

By updating additional version weights on an alias, invocation traffic is routed to the new function versions based on the weight specified.

Detailed CloudWatch metrics for the alias and version can be analyzed during the deployment, or other health checks performed, to ensure that the new version is healthy before proceeding.

The following example AWS CLI command points an alias to a new version, weighted at 5% (original version at 95% of traffic):

aws lambda update-alias --function-name myfunction --name myalias --routing-config '{"AdditionalVersionWeights" : {"2" : 0.05} }'

## Lambda Handler

A handler is a function which Lambda will invoke to execute your code – it is an entry point.

When you create a Lambda function, you specify a handler that AWS Lambda can invoke when the service executes the function on your behalf.

You define a Lambda function handler as an instance or static method in a class.

## Function Dependencies
If your Lambda function depends on external libraries such as AWS X-Ray SDK, database clients etc. you need to install the packages with the code and zip it all up.

- For Node.js use npm & “node modules” directory.
- For Python use pip — target options.
- For Java include the relevant .jar files.

Upload the zip file straight to Lambda if it’s less than 50MB, otherwise upload to S3.

Native libraries work they need to be compiled on Amazon Linux.

AWS SDK comes with every Lambda function by default.

## Concurrent Executions

### Managing Concurrency

The first time you invoke your function, AWS Lambda creates an instance of the function and runs its handler method to process the event. When the function returns a response, it stays active and waits to process additional events.  
If you invoke the function again while the first event is being processed, Lambda initializes another instance, and the function processes the two events concurrently.

![](https://i.imgur.com/FuvEn77.png)

Your functions’ concurrency is the number of instances that serve requests at a given time. For an initial burst of traffic, your functions’ cumulative concurrency in a Region can reach an initial level of between 500 and 3000, which varies per Region.

Burst Concurrency Limits:
- 3000 – US West (Oregon), US East (N. Virginia), Europe (Ireland).
- 1000 – Asia Pacific (Tokyo), Europe (Frankfurt).
- 500 – Other Regions.

After the initial burst, your functions’ concurrency can scale by an additional 500 instances each minute. This continues until there are enough instances to serve all requests, or until a concurrency limit is reached.

The default account limit is up to 1000 executions per second, per region (can be increased).

This is a safety feature to limit the number of concurrent executions across all functions in each region per account.

Each invocation over the concurrency limit will trigger a throttle.

TooManyRequestsExeception may be experienced if the concurrent execution limit is exceeded.

You may receive a HTTP status code: 429 and the message is “Request throughput limit exceeded”.

Throttle behavior:

- For synchronous invocations returns throttle error 429.
- For asynchronous invocations retries automatically (twice) then goes to a Dead Letter Queue (DLQ).

A DLQ can be an SNS topic or SQS queue.

The original event payload is sent to the DLQ.

The Lambda function needs an IAM role with permissions to SNS / SQS.

Lambda also integrates with X-Ray for debugging.

- Can trace Lambda with X-Ray.
- Need to enable in the Lambda configuration and it will run the X-Ray daemon.
- Use AWS SDK in your code.

### Reserved Concurrency

You can set a reserved concurrency at the function level to guarantee a set number of concurrent executions will be available for a critical function.

You can reserve up to the **Unreserved account concurrency** value that is shown in the console, minus 100 for functions that don’t have reserved concurrency.

To throttle a function, set the reserved concurrency to zero. This stops any events from being processed until you remove the limit.

**To reserve concurrency for a function**

1. Open the Lambda console [**Functions page**](https://console.aws.amazon.com/lambda/home#/functions).
2. Choose a function.
3. Under **Concurrency**, choose **Reserve concurrency**.
4. Enter the amount of concurrency to reserve for the function.
5. Choose **Save**.

### Provisioned Concurrency

When provisioned concurrency is allocated, the function scales with the same burst behavior as standard concurrency.

After it’s allocated, provisioned concurrency serves incoming requests with very low latency.

When all provisioned concurrency is in use, the function scales up normally to handle any additional requests.

Application Auto Scaling takes this a step further by providing autoscaling for provisioned concurrency.

With Application Auto Scaling, you can create a target tracking scaling policy that adjusts provisioned concurrency levels automatically, based on the utilization metric that Lambda emits.

[**Use the Application Auto Scaling API**](https://docs.aws.amazon.com/lambda/latest/dg/configuration-concurrency.html#configuration-concurrency-api) to register an alias as a scalable target and create a scaling policy.

Provisioned concurrency runs continually and is billed in addition to standard invocation costs.

Success and Failure Destinations

Lambda asynchronous invocations can put an event or message on Amazon Simple Notification Service (SNS), Amazon Simple Queue Service (SQS), or Amazon EventBridge for further processing.

With Destinations, you can route asynchronous function results as an execution record to a destination resource without writing additional code.

An execution record contains details about the request and response in JSON format including version, timestamp, request context, request payload, response context, and response payload.

For each execution status such as Success or Failure you can choose one of four destinations: another Lambda function, SNS, SQS, or EventBridge. Lambda can also be configured to route different execution results to different destinations.

On-Success:

- When a function is invoked successfully, Lambda routes the record to the destination resource for every successful invocation.
- You can use this to monitor the health of your serverless applications via execution status or build workflows based on the invocation result.

On-Failure:

- Destinations gives you the ability to handle the Failure of function invocations along with their Success.
- When a function invocation fails, such as when retries are exhausted or the event age has been exceeded (hitting its TTL),
- Destinations routes the record to the destination resource for every failed invocation for further investigation or processing.
- Destinations provide more useful capabilities than Dead Letter Queues (DLQs) by passing additional function execution information, including code exception stack traces, to more destination services.
- Destinations and DLQs can be used together and at the same time although Destinations should be considered a more preferred solution.

### Dead Letter Queue (DLQ)

You can configure a dead letter queue (DLQ) on AWS Lambda to give you more control over message handling for all asynchronous invocations, including those delivered via AWS events (S3, SNS, IoT, etc)..

A dead-letter queue saves discarded events for further processing. A dead-letter queue acts the same as an on-failure destination in that it is used when an event fails all processing attempts or expires without being processed.

However, a dead-letter queue is part of a function’s version-specific configuration, so it is locked in when you publish a version. On-failure destinations also support additional targets and include details about the function’s response in the invocation record.

You can setup a DLQ by configuring the ‘DeadLetterConfig’ property when creating or updating your Lambda function.

You can provide an SQS queue or an SNS topic as the ‘TargetArn’ for your DLQ, and AWS Lambda will write the event object invoking the Lambda function to this endpoint after the standard retry policy (2 additional retries on failure) is exhausted.

## Lambda Layers

You can configure your Lambda function to pull in additional code and content in the form of layers.

A layer is a ZIP archive that contains libraries, a custom runtime, or other dependencies.

With layers, you can use libraries in your function without needing to include them in your deployment package.

A function can use up to 5 layers at a time.

Layers are extracted to the /opt directory in the function execution environment.

Each runtime looks for libraries in a different location under /opt, depending on the language.

## Lambda@Edge
![](https://i.imgur.com/Q2IfHiu.png)

**Lambda@Edge** <mark style="background: #BBFABBA6;">allows you to run code across AWS locations globally without provisioning or managing servers, responding to end users at the lowest network latency.</mark>

Lambda@Edge <mark style="background: #FFF3A3A6;">lets you run Node.js and Python Lambda functions to customize content that CloudFront delivers, executing the functions in AWS locations closer to the viewer.</mark>

The functions run in response to CloudFront events, without provisioning or managing servers.  
You can use Lambda functions to change CloudFront requests and responses at the following points:
- After CloudFront receives a request from a viewer (viewer request).
- Before CloudFront forwards the request to the origin (origin request).
- After CloudFront receives the response from the origin (origin response).
- Before CloudFront forwards the response to the viewer (viewer response).

<mark style="background: #CACFD9A6;">You just upload your Node.js code to AWS Lambda and configure your function to be triggered in response to an Amazon CloudFront request.</mark>

The code is then ready to execute across AWS locations globally when a request for content is received, and scales with the volume of CloudFront requests globally.  
![[Pasted image 20240214120726.png]]  
![](https://i.imgur.com/C5KdtJ7.png)
 
## Lambda and Amazon VPC

- You can connect a Lambda function to private subnets in a VPC.  
	Lambda needs the following VPC configuration information so that it can connect to the VPC:
	- Private subnet ID.
	- Security Group ID (with required access).  
Lambda uses this information to setup an Elastic Network Interface (ENI) using an available IP address from your private subnet.  
![](https://i.imgur.com/7yfi5zL.png)

<mark style="background: #CACFD9A6;">Lambda functions provide access only to a single VPC</mark>. If multiple subnets are specified, they must all be in the same VPC.

<mark style="background: #FFF3A3A6;">Lambda functions configured to access resources in a particular VPC will not have access to the Internet as a default configuration.</mark>

<mark style="background: #BBFABBA6;">If you need access to the internet, you will need to create a NAT in your VPC to forward this traffic and configure your security group to allow this outbound traffic.</mark>

<mark style="background: #ADCCFFA6;">Careful with DNS resolution of public hostnames as it could add to function running time (cost).</mark>

Cannot connect to a dedicated tenancy VPC.

**_Exam tip:_** _If a Lambda function needs to connect to a VPC and needs Internet access, make sure you connect to a private subnet that has a route to a NAT Gateway (the NAT Gateway will be in a public subnet)._

Lambda uses your function’s permissions to create and manage network interfaces. To connect to a VPC, your function’s execution role must have the following permissions:
- <mark style="background: #ABF7F7A6;">ec2:CreateNetworkInterface</mark>
- <mark style="background: #ABF7F7A6;">ec2:DescribeNetworkInterfaces</mark>
- <mark style="background: #ABF7F7A6;">ec2:DeleteNetworkInterface</mark>
	
These permissions are included in the **AWSLambdaVPCAccessExecutionRole** managed policy.

<mark style="background: #CACFD9A6;">Only connect to a VPC if you need to as it can slow down function execution</mark>.

## Building Lambda Apps

You can deploy and manage your serverless applications using the AWS Serverless Application Model (AWS SAM).

AWS SAM is a specification that prescribes the rules for expressing serverless applications on AWS.

This specification aligns with the syntax used by AWS CloudFormation today and is supported natively within AWS CloudFormation as a set of resource types (referred to as “serverless resources”).

You can automate your serverless application’s release process using AWS CodePipeline and AWS CodeDeploy.

You can enable your Lambda function for tracing with AWS X-Ray.

## Elastic Load Balancing

Application Load Balancers (ALBs) support AWS Lambda functions as targets.

You can register your Lambda functions as targets and configure a listener rule to forward requests to the target group for your Lambda function.

**Exam tip:** Functions can be registered to target groups using the API, AWS Management Console or the CLI.

When the load balancer forwards the request to a target group with a Lambda function as a target, it invokes your Lambda function and passes the content of the request to the Lambda function, in JSON format.

Limits:

- The Lambda function and target group must be in the same account and in the same Region.
- The maximum size of the request body that you can send to a Lambda function is 1 MB.
- The maximum size of the response JSON that the Lambda function can send is 1 MB.
- WebSockets are not supported. Upgrade requests are rejected with an HTTP 400 code.

By default, health checks are disabled for target groups of type lambda.

You can enable health checks to implement DNS failover with Amazon Route 53. The Lambda function can check the health of a downstream service before responding to the health check request.

If you create the target group and register the Lambda function using the AWS Management Console, the console adds the required permissions to your Lambda function policy on your behalf.

Otherwise, after you create the target group and register the function using the AWS CLI, you must use the add-permission command to grant Elastic Load Balancing permission to invoke your Lambda function.

## Lambda Limits

Memory – minimum 128 MB, maximum 10,240 MB in 1 MB increments.

Ephemeral disk capacity (/tmp space) per invocation – 512 MB.

Size of environment variables maximum 4 KB.

Number of file descriptors – 1024.

Number of processes and threads (combined) – 1024.

Maximum execution duration per request – 900 seconds.

Concurrent executions per account – 1000 (soft limit).

Function burst concurrency 500 -3000 (region dependent).

Invocation payload:

- Synchronous 6 MB.
- Asynchronous 256 KB

Lambda function deployment size is 50 MB (zipped), 250 MB unzipped.

## Operations and Monitoring

Lambda automatically monitors Lambda functions and reports metrics through CloudWatch.

Lambda tracks the number of requests, the latency per request, and the number of requests resulting in an error.

You can view the request rates and error rates using the AWS Lambda Console, the CloudWatch console, and other AWS resources.

You can use AWS X-Ray to visualize the components of your application, identify performance bottlenecks, and troubleshoot requests that resulted in an error.

Your Lambda functions send trace data to X-Ray, and X-Ray processes the data to generate a service map and searchable trace summaries.

The AWS X-Ray Daemon is a software application that gathers raw segment data and relays it to the AWS X-Ray service.

The daemon works in conjunction with the AWS X-Ray SDKs so that data sent by the SDKs can reach the X-Ray service.

When you trace your Lambda function, the X-Ray daemon automatically runs in the Lambda environment to gather trace data and send it to X-Ray.

Must have permissions to write to X-Ray in the execution role.

## Development Best Practices

Perform one-off time-consuming tasks outside of the function handler, e.g.:

- Connect to databases.
- Initialize the AWS SDK.
- Pull in dependencies or datasets.

Use environment variables for:

- Connection strings, S3 bucket etc.
- Passwords and other sensitive data (can be encrypted with KMS).

Minimize deployment packages size to runtime necessities.

- Break down the function if required.
- Remember the Lambda limits.

Avoid using recursive code, never have a Lambda function call itself.

Don’t put you Lambda function in a VPC unless you need to (can take longer to initialize).

## Charges

Priced based on:

- Number of requests.
- Duration of the request calculated from the time your code begins execution until it returns or terminates.
- The amount of memory allocated to the function.


![[Module 13 - Building Microservices and Serverless Architectures#Building Serverless Architectures with AWS Lambda]]


# FAQ
## General

Close all

### Q: What is AWS Lambda?

AWS Lambda lets you run code without provisioning or managing servers. You pay only for the compute time you consume - there is no charge when your code is not running. With Lambda, you can run code for virtually any type of application or backend service - all with zero administration. Just upload your code, and Lambda takes care of everything required to run and scale your code with high availability. You can set up your code to automatically trigger from other AWS services or call it directly from any web or mobile app.

### Q: What is Serverless Computing?

[Serverless computing](https://aws.amazon.com/serverless/) allows you to build and run applications and services without thinking about servers. With serverless computing, your application still runs on servers, but all the server management is done by AWS. At the core of serverless computing is AWS Lambda, which lets you run your code without provisioning or managing servers.

### Q: What Events Can Trigger an AWS Lambda Function?

Please see our [documentation](https://docs.aws.amazon.com/lambda/latest/dg/intro-core-components.html#intro-core-components-event-sources) for a complete list of event sources.

### Q: When Should I Use AWS Lambda versus Amazon EC2?

Amazon Web Services offers a set of compute services to meet a range of needs.

[Amazon EC2](https://aws.amazon.com/ec2/) offers flexibility, with a wide range of instance types and the option to customize the operating system, network and security settings, and the entire software stack, allowing you to easily move existing applications to the cloud. With Amazon EC2 you are responsible for provisioning capacity, monitoring fleet health and performance, and designing for fault tolerance and scalability. [AWS Elastic Beanstalk](https://aws.amazon.com/elasticbeanstalk/) offers an easy-to-use service for deploying and scaling web applications in which you retain ownership and full control over the underlying EC2 instances. [Amazon EC2 Container Service](https://aws.amazon.com/ecs/) is a scalable management service that supports Docker containers and allows you to easily run distributed applications on a managed cluster of Amazon EC2 instances.

AWS Lambda makes it easy to execute code in response to events, such as changes to Amazon S3 buckets, updates to an Amazon DynamoDB table, or custom events generated by your applications or devices. With Lambda, you do not have to provision your own instances; Lambda performs all the operational and administrative activities on your behalf, including capacity provisioning, monitoring fleet health, applying security patches to the underlying compute resources, deploying your code, running a web service front end, and monitoring and logging your code. AWS Lambda provides easy scaling and high availability to your code without additional effort on your part.

### Q: What Kind of Code Can Run on AWS Lambda?

AWS Lambda offers an easy way to accomplish many activities in the cloud. For example, you can use AWS Lambda to build mobile back-ends that retrieve and transform data from Amazon DynamoDB, handlers that compress or transform objects as they are uploaded to Amazon S3, auditing and reporting of API calls made to any Amazon Web Service, and server-less processing of streaming data using Amazon Kinesis.

### Q: What Languages Does AWS Lambda Support?

AWS Lambda natively supports Java, Go, PowerShell, Node.js, C#, Python, and Ruby code, and provides a Runtime API which allows you to use any additional programming languages to author your functions. Please read our documentation on using [Node.js](https://docs.aws.amazon.com/lambda/latest/dg/authoring-function-in-nodejs.html), [Python](http://docs.aws.amazon.com/lambda/latest/dg/python-lambda.html), [Java](http://docs.aws.amazon.com/lambda/latest/dg/java-lambda.html), [Ruby](https://docs.aws.amazon.com/lambda/latest/dg/lambda-runtimes.html), [C#](http://docs.aws.amazon.com/lambda/latest/dg/current-supported-versions.html), [Go](https://docs.aws.amazon.com/lambda/latest/dg/go-programming-model.html), and [PowerShell](https://docs.aws.amazon.com/lambda/latest/dg/powershell-programming-model.html).  
![[Pasted image 20240214115945.png]]
### Q: Can I Access the Infrastructure that AWS Lambda Runs On?

No. AWS Lambda operates the compute infrastructure on your behalf, allowing it to perform health checks, apply security patches, and do other routine maintenance.

### Q: How Does AWS Lambda Isolate My Code?

Each AWS Lambda function runs in its own isolated environment, with its own resources and file system view. AWS Lambda uses the same techniques as Amazon EC2 to provide security and separation at the infrastructure and execution levels.

### Q: How Does AWS Lambda Secure My Code?

AWS Lambda stores code in Amazon S3 and encrypts it at rest. AWS Lambda performs additional integrity checks while your code is in use.

### Q: What AWS Regions Are Available for AWS Lambda?

Please refer to the [AWS Global Infrastructure Region Table](https://aws.amazon.com/about-aws/global-infrastructure/regional-product-services/).

## AWS Lambda Functions

Close all

### Q: What is an AWS Lambda Function?

The code you run on AWS Lambda is uploaded as a “Lambda function”. Each function has associated configuration information, such as its name, description, entry point, and resource requirements. The code must be written in a “stateless” style i.e. it should assume there is no affinity to the underlying compute infrastructure. Local file system access, child processes, and similar artifacts may not extend beyond the lifetime of the request, and any persistent state should be stored in Amazon S3, Amazon DynamoDB, Amazon EFS, or another Internet-available storage service. Lambda functions can include libraries, even native ones.

### Q: Will AWS Lambda Reuse Function Instances?

To improve performance, AWS Lambda may choose to retain an instance of your function and reuse it to serve a subsequent request, rather than creating a new copy. To learn more about how Lambda reuses function instances, visit our [documentation](https://docs.aws.amazon.com/lambda/latest/dg/lambda-introduction.html). Your code should not assume that this will always happen.

### Q: What if I Need Scratch Space on Disk for My AWS Lambda Function?

You can configure each Lambda function with its own ephemeral storage between 512MB and 10,240MB, in 1MB increments. The ephemeral storage is available in each function’s /tmp directory.

Each function has access to 512MB of storage at no additional cost. When configuring your functions with more than 512MB of ephemeral storage, you will be charged based on the amount of storage you configure, and how long your function runs, metered in 1ms increments. For comparison, in the US East (Ohio) region, the AWS Fargate ephemeral storage price is $0.000111 per GB-hour, or $0.08 per GB-month. Amazon EBS gp3 storage volume pricing in US East (Ohio) is $0.08 per GB-month. AWS Lambda ephemeral storage pricing is $0.0000000309 per GB-second, or $0.000111 per GB-hour and $0.08 per GB-month. To learn more, see [AWS Lambda Pricing](https://aws.amazon.com/lambda/pricing/).

### Q: How Do I Configure My Application to Use AWS Lambda Ephemeral Storage?

You can configure each Lambda function with its own ephemeral storage between 512MB and 10,240MB, in 1MB increments by using the AWS Lambda console, AWS Lambda API, or AWS CloudFormation template during function creation or update.

### Q: Is AWS Lambda Ephemeral Storage Encrypted?

Yes. All data stored in ephemeral storage is encrypted at rest with a key managed by AWS.

### Q: What Metrics Can I Use to Monitor My AWS Lambda Ephemeral Storage Usage?

You can use AWS CloudWatch Lambda Insight metrics to monitor your ephemeral storage usage. To learn more, see the AWS CloudWatch Lambda Insights [documentation](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/Lambda-Insights-metrics.html).

### Q: When Should I Use Amazon S3, Amazon EFS, or AWS Lambda Ephemeral Storage for My Serverless Applications?

If your application needs durable, persistent storage, consider using Amazon S3 or Amazon EFS. If your application requires storing data needed by code in a single function invocation, consider using AWS Lambda ephemeral storage as a transient cache. To learn more, please see [Choosing between AWS Lambda data storage options in web apps](https://aws.amazon.com/blogs/compute/choosing-between-aws-lambda-data-storage-options-in-web-apps/).

### Q: Can I Use Ephemeral Storage while Provisioned Concurrency is Enabled for My Function?

Yes. However, if you application needs persistent storage, consider using Amazon EFS or Amazon S3. When you enable Provisioned Concurrency for your function, your function's [initialization code](https://docs.aws.amazon.com/lambda/latest/dg/foundation-progmodel.html) runs during allocation and every few hours, as running instances of your function are recycled. You can see the initialization time in logs and [traces](https://docs.aws.amazon.com/lambda/latest/dg/services-xray.html) after an instance processes a request. However, initialization is billed even if the instance never processes a request. This Provisioned Concurrency initialization behavior may affect how your function interacts with data you store in ephemeral storage, even when your function isn’t processing requests. To learn more about Provisioned Concurrency, please see the relevant [documentation](https://docs.aws.amazon.com/lambda/latest/dg/provisioned-concurrency.html).

### Q: How Do I Configure My Application to Use AWS Lambda Ephemeral Storage?

You can configure each Lambda function with its own ephemeral storage between 512MB and 10,240MB, in 1MB increments by using the AWS Lambda console, AWS Lambda API, or AWS CloudFormation template during function creation or update.

### Q: Is AWS Lambda Ephemeral Storage Encrypted?

Yes. All data stored in ephemeral storage is encrypted at rest with a key managed by AWS.

### Q: What Metrics Can I Use to Monitor My AWS Lambda Ephemeral Storage Usage?

You can use AWS CloudWatch Lambda Insight metrics to monitor your ephemeral storage usage. To learn more, see the AWS CloudWatch Lambda Insights [documentation](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/Lambda-Insights-metrics.html).

### Q: Why Must AWS Lambda Functions Be Stateless?

Keeping functions stateless enables AWS Lambda to rapidly launch as many copies of the function as needed to scale to the rate of incoming events. While AWS Lambda’s programming model is stateless, your code can access stateful data by calling other web services, such as Amazon S3 or Amazon DynamoDB.

### Q: Can I Use Threads and Processes in My AWS Lambda Function Code?

Yes. AWS Lambda allows you to use normal language and operating system features, such as creating additional threads and processes. Resources allocated to the Lambda function, including memory, execution time, disk, and network use, must be shared among all the threads/processes it uses. You can launch processes using any language supported by Amazon Linux.

### Q: What Restrictions Apply to AWS Lambda Function Code?

Lambda attempts to impose as few restrictions as possible on normal language and operating system activities, but there are a few activities that are disabled: Inbound network connections are blocked by AWS Lambda, and for outbound connections, only TCP/IP and UDP/IP sockets are supported, and ptrace (debugging) system calls are blocked. TCP port 25 traffic is also blocked as an anti-spam measure.

### Q: How Do I Create an AWS Lambda Function Using the Lambda Console?

If you are using Node.js or Python, you can author the code for your function using code editor in the AWS Lambda console, which lets you author and test your functions, and view the results of function executions in a robust, IDE-like environment. [Go to the console to get started](https://console.aws.amazon.com/lambda/home?region=us-east-1).

You can also package the code (and any dependent libraries) as a ZIP and upload it using the AWS Lambda console from your local environment or specify an Amazon S3 location where the ZIP file is located. Uploads must be no larger than 50MB (compressed). You can use the AWS Eclipse plugin to author and deploy Lambda functions in Java. You can use the Visual Studio plugin to author and deploy Lambda functions in C#, and Node.js.

### Q: How Do I Create an AWS Lambda Function Using the Lambda CLI?

You can package the code (and any dependent libraries) as a ZIP and upload it using the AWS CLI from your local environment, or specify an Amazon S3 location where the ZIP file is located. Uploads must be no larger than 50MB (compressed). Visit the [Lambda Getting Started guide](https://docs.aws.amazon.com/lambda/latest/dg/getting-started.html) to get started.

### Q: Does AWS Lambda Support Environment Variables?

Yes. You can easily create and modify environment variables from the AWS Lambda Console, CLI, or SDKs. To learn more about environment variables, see the [documentation](https://docs.aws.amazon.com/lambda/latest/dg/env_variables.html).

### Q: Can I Store Sensitive Information in Environment Variables?

For sensitive information, such as database passwords, we recommend you use client-side encryption using [AWS Key Management Service](https://docs.aws.amazon.com/kms/latest/developerguide/overview.html) and store the resulting values as ciphertext in your environment variable. You will need to include logic in your AWS Lambda function code to decrypt these values.

### Q: How Can I Manage My AWS Lambda Functions?

**Q: How can I manage my AWS Lambda functions?**

### Q: Can I Share Code across Functions?

Yes, you can package any code (frameworks, SDKs, libraries, and more) as a [Lambda Layer](https://docs.aws.amazon.com/lambda/latest/dg/configuration-layers.html) and manage and share them easily across multiple functions.

### Q: How Do I Monitor an AWS Lambda Function?

AWS Lambda automatically monitors Lambda functions on your behalf, reporting real-time metrics through Amazon CloudWatch, including total requests, account-level and function-level concurrency usage, latency, error rates, and throttled requests. You can view statistics for each of your Lambda functions via the Amazon CloudWatch console or through the AWS Lambda console. You can also call third-party monitoring APIs in your Lambda function.  
 

Visit [Troubleshooting CloudWatch metrics](https://docs.aws.amazon.com/lambda/latest/dg/monitoring-functions.html) to learn more. Standard charges for AWS Lambda apply to use Lambda’s built-in metrics.

### Q: How Do I Troubleshoot Failures in an AWS Lambda Function?

AWS Lambda automatically integrates with Amazon CloudWatch logs, creating a log group for each Lambda function and providing basic application lifecycle event log entries, including logging the resources consumed for each use of that function. You can easily insert additional logging statements into your code. You can also call third-party logging APIs in your Lambda function. Visit [Troubleshooting Lambda functions](https://docs.aws.amazon.com/lambda/latest/dg/monitoring-functions.html) to learn more. Amazon CloudWatch Logs rates will apply.

### Q: How Do I Scale an AWS Lambda Function?

You do not have to scale your Lambda functions – AWS Lambda scales them automatically on your behalf. Every time an event notification is received for your function, AWS Lambda quickly locates free capacity within its compute fleet and runs your code. Since your code is stateless, AWS Lambda can start as many copies of your function as needed without lengthy deployment and configuration delays. There are no fundamental limits to scaling a function. AWS Lambda will dynamically allocate capacity to match the rate of incoming events.

### Q: How Are Compute Resources Assigned to an AWS Lambda Function?

In the AWS Lambda resource model, you choose the amount of memory you want for your function, and are allocated proportional CPU power and other resources. For example, choosing 256MB of memory allocates approximately twice as much CPU power to your Lambda function as requesting 128MB of memory and half as much CPU power as choosing 512MB of memory. To learn more, see our [Function Configuration documentation](https://docs.aws.amazon.com/lambda/latest/dg/resource-model.html).  
  
You can set your memory from 128MB to 10,240MB.

### Q: When Should I Use AWS Lambda Functions with More than 3008 MB of Memory?

Customers running memory or compute-intensive workloads can now use more memory for their functions. Larger memory functions help multithreaded applications run faster, making them ideal for data and computationally intensive applications like machine learning, batch and ETL jobs, financial modeling, genomics, HPC, and media processing.

### Q: How long Can an AWS Lambda Function Execute?

AWS Lambda functions can be configured to run up to 15 minutes per execution. You can set the timeout to any value between 1 second and 15 minutes.

### Q: How Will I Be Charged for Using AWS Lambda Functions?

AWS Lambda is priced on a pay-per-use basis. Please see the [AWS Lambda pricing page](https://aws.amazon.com/lambda/pricing/) for details.

### Q: Can I save Money on AWS Lambda with a Compute Savings Plan?

Yes. In addition to saving money on Amazon EC2 and AWS Fargate, you can also use Compute Savings Plans to save money on AWS Lambda. Compute Savings Plans offer up to 17% discount on Duration, Provisioned Concurrency, and Duration (Provisioned Concurrency). Compute Savings Plans do not offer a discount on Requests in your Lambda bill. However, your Compute Savings Plans commitment can apply to Requests at regular rates.

### Q: Does AWS Lambda Support Versioning?

Yes. By default, each AWS Lambda function has a single, current version of the code. Clients of your Lambda function can call a specific version or get the latest implementation. Please read our documentation on [versioning Lambda functions](https://docs.aws.amazon.com/lambda/latest/dg/versioning-aliases.html).

### Q: How long after Uploading My Code Will My AWS Lambda Function Be Ready to Call?

Deployment times may vary with the size of your code, but AWS Lambda functions are typically ready to call within seconds of upload.

### Q: Can I Use My Own Version of a Supported Library?

Yes. You can include your own copy of a library (including the AWS SDK) in order to use a different version than the default one provided by AWS Lambda.

### Q: How Does Tiered Pricing Work?

AWS Lambda offers discounted pricing tiers for monthly on-demand function duration above certain thresholds. Tiered pricing is available for functions running on both x86 and Arm architectures. Lambda pricing tiers are applied to aggregate monthly on-demand duration of your functions running on the same architecture (x86 or Arm, respectively), in the same region, within the account. If you’re using consolidated billing in AWS Organizations, pricing tiers are applied to the aggregate monthly duration of your functions running on the same architecture, in the same region, across the accounts in the organization. For example, if you are running x86 Lambda functions in the US East (Ohio) region, you will pay $0.0000166667 for every GB-second for the first 6 billion GB-seconds per month, $0.0000150000 for every GB-second for the next 9 billion GB-seconds per month, and $0.0000133334 for every GB-second over 15 billion GB-seconds per month, in that region. Pricing for Requests, Provisioned Concurrency, and Provisioned Concurrency Duration remains unchanged. For more information, please see [AWS Lambda Pricing](https://aws.amazon.com/lambda/pricing/)

### Q: Can I Take Advantage of both Tiered Pricing, and Compute Savings Plans?

Yes. Lambda usage that is covered by your hourly savings plan commitment is billed at the [applicable CSP rate and discount](https://aws.amazon.com/savingsplans/compute-pricing/). The remaining usage that is not covered by this commitment will be billed at the rate corresponding to the tier your monthly aggregate function duration falls in.

## Using AWS Lambda to Process AWS Events

Close all

### Q: What is an Event Source?

An event source is an AWS service or developer-created application that produces events that trigger an AWS Lambda function to run. Some services publish these events to Lambda by invoking the cloud function directly (for example, Amazon S3). Lambda can also poll resources in other services that do not publish events to Lambda. For example, Lambda can pull records from an Amazon Kinesis stream or an Amazon SQS queue and execute a Lambda function for each fetched message.Many other services, such as AWS CloudTrail, can act as event sources simply by logging to Amazon S3 and using S3 bucket notifications to trigger AWS Lambda functions

### Q: What Event Sources Can Be Used with AWS Lambda?

Please see our [documentation](https://docs.aws.amazon.com/lambda/latest/dg/intro-core-components.html#intro-core-components-event-sources) for a complete list of event sources.

### Q: How Are Events Represented in AWS Lambda?

Events are passed to a Lambda function as an event input parameter. For event sources where events arrive in batches, such as Amazon SQS, Amazon Kinesis, and Amazon DynamoDB Streams, the event parameter may contain multiple events in a single call, based on the batch size you request. To learn more about Amazon S3 event notifications, visit [Configuring Notifications for Amazon S3 Events](https://docs.aws.amazon.com/AmazonS3/latest/dev/NotificationHowTo.html). To learn more about Amazon DynamoDB Streams, visit the [DynamoDB Stream Developers Guide](http://docs.aws.amazon.com/amazondynamodb/latest/developerguide/Streams.html). To learn more about invoking Lambda functions using Amazon SNS, visit the [Amazon SNS Developers Guide](http://docs.aws.amazon.com/sns/latest/dg/sns-lambda.html). For more information on Amazon Cognito events, visit [Amazon Cognito](https://aws.amazon.com/cognito/). For more information on AWS CloudTrail logs and auditing API calls across AWS services, see [AWS CloudTrail](https://aws.amazon.com/cloudtrail/).

### Q: How Do I Make an AWS Lambda Function Respond to Changes in an Amazon S3 Bucket?

From the AWS Lambda console, you can select a function and associate it with notifications from an Amazon S3 bucket. Alternatively, you can use the Amazon S3 console and configure the bucket’s notifications to send to your AWS Lambda function. This same functionality is also available through the AWS SDK and CLI.

### Q: How Do I Make an AWS Lambda Function Respond to Updates in an Amazon DynamoDB Table?

You can trigger a Lambda function on DynamoDB table updates by subscribing your Lambda function to the DynamoDB Stream associated with the table. You can associate a DynamoDB Stream with a Lambda function using the Amazon DynamoDB console, the AWS Lambda console, or Lambda’s registerEventSource API.

### Q: How Do I Use an AWS Lambda Function to Process Records in an Amazon Kinesis Stream?

From the AWS Lambda console, you can select a Lambda function and associate it with an Amazon Kinesis stream owned by the same account. This same functionality is also available through the AWS SDK and CLI.

### Q: How Does AWS Lambda Process Data from Amazon Kinesis Streams and Amazon DynamoDB Streams?

The Amazon Kinesis and DynamoDB Streams records sent to your AWS Lambda function are strictly serialized, per shard. This means that if you put two records in the same shard, Lambda guarantees that your Lambda function will be successfully invoked with the first record before it is invoked with the second record. If the invocation for one record times out, is throttled, or encounters any other error, Lambda will retry until it succeeds (or the record reaches its 24-hour expiration) before moving on to the next record. The ordering of records across different shards is not guaranteed, and processing of each shard happens in parallel.

### Q: How Should I Choose between AWS Lambda and Amazon Kinesis Data Analytics for My Analytics Needs?

AWS Lambda allows you to perform time-based aggregations (such as count, max, sum, average, etc.) over a short window of up to 15 minutes for your data in Amazon Kinesis or Amazon DynamoDB Streams over a single logical partition such as a shard. This gives you the option to easily set up simple analytics for your event-based application without adding architectural complexity, as your business and analytics logic can be located in the same function. Lambda allows aggregations over a maximum of a 15-minute tumbling window, based on the event timestamp. [Amazon Kinesis Data Analytics](https://aws.amazon.com/kinesis/data-analytics/) allows you to build more complex analytics applications that support flexible processing choices and robust fault-tolerance with exactly-once processing without duplicates, and analytics that can be performed over an entire data stream across multiple logical partitions. With KDA, you can analyze data over multiple types of aggregation windows (tumbling window, stagger window, sliding window, session window) using either the event time or the processing time.  
 

|   | AWS Lambda | Amazon KDA |
| --- | --- | --- |
| Tumbling Window | Yes | Yes |
| Stagger Window | No | Yes |
| Sliding Window | No | Yes |
| Session Window | No | Yes |
| Enrichment | No | Yes |
| Joint input and reference tables | No | Yes |
| Split input stream | No | Yes |
| Exactly-once processing | No | Yes |
| Maximum time window | 15 mins | No limit |
| Aggregation scope | Partition/shard | Stream |
| Time semantics | Event time | Event time, Processing time |

### Q: How Do I Use an AWS Lambda Function to Respond to Notifications Sent by Amazon Simple Notification Service (SNS)?

From the AWS Lambda console, you can select a Lambda function and associate it with an Amazon SNS topic. This same functionality is also available through the AWS SDK and CLI.

### Q: How Do I Use an AWS Lambda Function to Respond to Emails Sent by Amazon Simple Email Service (SES)?

From the Amazon SES Console, you can set up your receipt rule to have Amazon SES deliver your messages to an AWS Lambda function. The same functionality is available through the AWS SDK and CLI.

### Q: How Do I Use an AWS Lambda Function to Respond to Amazon CloudWatch Alarms?

First, configure the alarm to send Amazon SNS notifications. Then from the AWS Lambda console, select a Lambda function and associate it with that Amazon SNS topic. See the [Amazon CloudWatch Developer Guide](https://docs.aws.amazon.com/AmazonCloudWatch/latest/DeveloperGuide/WhatIsCloudWatch.html) for more on setting up Amazon CloudWatch alarms.

### Q: How Do I Use an AWS Lambda Function to Respond to Changes in User or Device Data Managed by Amazon Cognito?

From the AWS Lambda console, you can select a function to trigger when any datasets associated with an [Amazon Cognito](https://aws.amazon.com/cognito/) identity pool are synchronized. This same functionality is also available through the AWS SDK and CLI. Visit Amazon Cognito for more information on using Amazon Cognito to share and synchronize data across a user’s devices.

### Q: How Can My Application Trigger an AWS Lambda Function Directly?

You can invoke a Lambda function using a custom event through AWS Lambda’s invoke API. Only the function owner or another AWS account that the owner has granted permission can invoke the function. Visit the [Lambda Developers Guide](https://docs.aws.amazon.com/lambda/latest/dg/welcome.html) to learn more.

### Q: What is the Latency of Invoking an AWS Lambda Function in Response to an Event?

AWS Lambda is designed to process events within milliseconds. Latency will be higher immediately after a Lambda function is created, updated, or if it has not been used recently.

### Q: How Do I Create a Mobile Backend Using AWS Lambda?

You upload the code you want AWS Lambda to execute and then invoke it from your mobile app using the AWS Lambda SDK included in the AWS Mobile SDK. You can make both direct (synchronous) calls to retrieve or check data in real time, as well as asynchronous calls. You can also define a custom API using Amazon API Gateway and invoke your Lambda functions through any REST compatible client. To learn more about the AWS Mobile SDK, visit the [AWS Mobile SDK](https://aws.amazon.com/mobile/sdk/) page. To learn more about Amazon API Gateway, visit the [Amazon API Gateway](https://aws.amazon.com/api-gateway/) page.

### Q: How Do I Invoke an AWS Lambda Function over HTTPS?

You can invoke a Lambda function over HTTPS by defining a custom RESTful API using Amazon API Gateway. This gives you an endpoint for your function which can respond to REST calls like GET, PUT, and POST. Read more about using AWS Lambda with Amazon API Gateway.

### Q: How Can My AWS Lambda Function Customize Its Behavior to the Device and App Making the Request?

When called through the AWS Mobile SDK, AWS Lambda functions automatically gain insight into the device and application that made the call through the ‘context’ object.

### Q: How Can My AWS Lambda Function Personalize Its Behavior Based on the Identity of the End-user of an Application?

When your app uses the Amazon Cognito identity, end users can authenticate themselves using a variety of public login providers such as Amazon, Facebook, Google, and other OpenID Connect-compatible services. User identity is then automatically and secured presented to your Lambda function in the form of an Amazon Cognito id, allowing it to access user data from Amazon Cognito, or as a key to store and retrieve data in Amazon DynamoDB or other web services.

### Q: How Do I Create an Alexa Skill Using AWS Lambda?

AWS Lambda is integrated with the Alexa Skills Kit, a collection of self-service APIs, tools, documentation, and code samples that make it easy for you to create voice-driven capabilities (or “skills”) for Alexa. You simply upload the Lambda function code for the new Alexa skill you are creating, and AWS Lambda does the rest, executing the code in response to Alexa voice interactions and automatically managing the compute resources on your behalf. Read the Alexa Skills Kit documentation for more details.

### Q: What Happens if My Function Fails while Processing an Event?

For Amazon S3 bucket notifications and custom events, AWS Lambda will attempt execution of your function three times in the event of an error condition in your code or if you exceed a service or resource limit. For ordered event sources that AWS Lambda polls on your behalf, such as Amazon DynamoDB Streams and Amazon Kinesis streams, Lambda will continue attempting execution in the event of a developer code error until the data expires. You can monitor progress through the Amazon Kinesis and Amazon DynamoDB consoles and through the Amazon CloudWatch metrics that AWS Lambda generates for your function. You can also set Amazon CloudWatch alarms based on error or execution throttling rates.

## Using AWS Lambda to Build Applications

Close all

### Q: What is a Serverless Application?

Lambda-based applications (also referred to as serverless applications) are composed of functions triggered by events. A typical serverless application consists of one or more functions triggered by events such as object uploads to Amazon S3, Amazon SNS notifications, or API actions. These functions can stand alone or leverage other resources such as DynamoDB tables or Amazon S3 buckets. The most basic serverless application is simply a function.

### Q: How Do I Deploy and Manage a Serverless Application?

You can deploy and manage your serverless applications using the AWS Serverless Application Model (AWS SAM). AWS SAM is a specification that prescribes the rules for expressing serverless applications on AWS. This specification aligns with the syntax used by AWS CloudFormation today and is supported natively within AWS CloudFormation as a set of resource types (referred to as "serverless resources"). These resources make it easier for AWS customers to use CloudFormation to configure and deploy serverless applications using existing CloudFormation APIs.

### Q: How Can I Discover Existing Serverless Applications Developed by the AWS Community?

You can choose from a collection of serverless applications published by developers, companies, and partners in the AWS community with the [AWS Serverless Application Repository](https://aws.amazon.com/serverless/serverlessrepo/). After finding an application, you can configure and deploy it straight from the [Lambda console](https://console.aws.amazon.com/lambda/home?region=us-east-1).

### Q: How Do I Automate Deployment for a Serverless Application?

You can automate your serverless application release process using AWS CodePipeline and AWS CodeDeploy. CodePipeline is a continuous delivery service that enables you to model, visualize and automate the steps required to release your serverless application. CodeDeploy provides a deployment automation engine for your Lambda-based applications. CodeDeploy lets you orchestrate deployments according to established best-practice methodologies such as canary and linear deployments, and helps you establish the necessary guardrails to verify that newly-deployed code is safe, stable, and ready to be fully released to production.  
 

To learn more about serverless CI/CD, visit our [documentation](https://docs.aws.amazon.com/lambda/latest/dg/automating-deployment.html).

### Q: How Do I Get Started on Building a Serverless Application?

To get started, visit the AWS Lambda console and download one of our blueprints. The file you download will contain an AWS SAM file (which defines the AWS resources in your application) and a .ZIP file (which includes your function code). You can then use AWS CloudFormation commands to package and deploy the serverless application that you just downloaded. For more details, visit our [documentation](https://docs.aws.amazon.com/lambda/latest/dg/deploying-lambda-apps.html).

### Q: How Do I Coordinate Calls between Multiple AWS Lambda Functions?

You can use [AWS Step Functions](https://aws.amazon.com/step-functions/) to coordinate a series of AWS Lambda functions in a specific order. You can invoke multiple Lambda functions sequentially, passing the output of one to the other, and/or in parallel, and Step Functions will maintain state during executions for you.

### Q: How Do I Troubleshoot a Serverless Application?

You can enable your Lambda function for tracing with [AWS X-Ray](https://aws.amazon.com/xray/) by adding X-Ray permissions to your Lambda function execution role and changing your function “tracing mode” to “active. ” When X-Ray is enabled for your Lambda function, AWS Lambda will emit tracing information to X-Ray regarding the Lambda service overhead incurred when invoking your function. This will provide you with insights such as Lambda service overhead, function init time, and function execution time. In addition, you can include the X-Ray SDK in your Lambda deployment package to create your own trace segments, annotate your traces, or view trace segments for downstream calls made from your Lambda function. X-Ray SDKs are currently available for Node.js and Java. Visit [Troubleshooting Lambda-based applications](https://docs.aws.amazon.com/lambda/latest/dg/lambda-x-ray.html) to learn more. AWS X-Ray rates will apply.

### Q. Can I Build Serverless Applications that Connect to Relational Databases?
![](https://i.imgur.com/IeF6uWl.png)

Yes. You can build highly scalable, secure, Lambda-based serverless applications that connect to relational databases using [Amazon RDS Proxy](https://aws.amazon.com/rds/proxy/), a highly available database proxy that manages thousands of concurrent connections to relational databases. Currently, RDS Proxy supports MySQL and Aurora databases. You can begin using RDS Proxy through the Amazon RDS console or the AWS Lambda console. Serverless applications that use fully managed connection pools from RDS Proxy will be billed according to [RDS Proxy Pricing](https://aws.amazon.com/rds/proxy/pricing/).

### Q: How is AWS SAM Licensed?

The specification is open sourced under Apache 2.0, which allows you and others to adopt and incorporate AWS SAM into build, deployment, monitoring, and management tools with a commercial-friendly license. You can access the AWS SAM repository on GitHub [here](https://github.com/awslabs/serverless-application-specification).

## Container Image Support

Close all

### Q: What is Container Image Support for AWS Lambda?

AWS Lambda now enables you to package and deploy functions as container images. Customers can leverage the flexibility and familiarity of container tooling, and the agility and operational simplicity of AWS Lambda to build applications.

### Q: How Can I Use Container Image Support for AWS Lambda?

You can start with either an AWS provided base images for Lambda or by using one of your preferred community or private enterprise images. Then, simply use Docker CLI to build the image, upload it to Amazon ECR, and then create the function by using all familiar Lambda interfaces and tools, such as the AWS Management Console, the AWS CLI, the AWS SDK, AWS SAM, and AWS CloudFormation.

### Q: Which Container Image Types Are Supported?

You can deploy third-party Linux base images (e.g. Alpine or Debian) to Lambda in addition to the Lambda provided images. AWS Lambda will support all images based on the following image manifest formats: Docker Image Manifest V2 Schema 2 (used with Docker version 1.10 and newer) or Open Container Initiative (OCI) Spec (v1.0 and up). Lambda supports images with a size of up to 10GB.

### Q: What Base Images Can I Use?

AWS Lambda provides a variety of base images customers can extend, and customers can also use their preferred Linux-based images with a size of up to 10GB.

### Q: What Container Tools Can I Use to Package and Deploy Functions as Container Images?

You can use any container tooling as long as it supports one of the following container image manifest formats: Docker Image Manifest V2 Schema 2 (used with Docker version 1.10 and newer) or Open Container Initiative (OCI) Specifications (v1.0 and up). For example, you can use native container tools (i.e. docker run, docker compose, Buildah and Packer) to define your functions as a container image and deploy to Lambda.

### Q: What AWS Lambda Features Are Available to Functions Deployed as Container Images?

All existing AWS Lambda features, with the exception of Lambda layers and Code Signing, can be used with functions deployed as container images. Once deployed, AWS Lambda will treat an image as immutable. Customers can use container layers during their build process to include dependencies.

### Q: Will AWS Lambda Patch and Update My Deployed Container Image?

Not at this time. Your image, once deployed to AWS Lambda, will be immutable. The service will not patch or update the image. However, AWS Lambda will publish curated base images for all supported runtimes that are based on the Lambda managed environment. These published images will be patched and updated along with updates to the AWS Lambda managed runtimes. You can pull and use the latest base image from DockerHub or Amazon ECR Public, re-build your container image and deploy to AWS Lambda via Amazon ECR. This allows you to build and test the updated images and runtimes, prior to deploying the image to production

### Q: What Are the Differences between Functions Created Using ZIP Archives vs. Container Images?

There are three main differences between functions created using ZIP archives vs. container images:

1. Functions created using ZIP archives have a maximum code package size of 250 MB unzipped, and those created using container images have a maximum image size of 10 GB. 
2. Lambda uses Amazon ECR as the underlying code storage for functions defined as container images, so a function may not be invocable when the underlying image is deleted from ECR. 
3. ZIP functions are automatically patched for the latest runtime security and bug fixes. Functions defined as container images are immutable, and customers are responsible for the components packaged in their function. Customers can leverage the AWS provided base images which are regularly updated by AWS for security and bug fixes, using the most recent patches available.

### Q: Is there a Performance Difference between Functions Defined as Zip and Container Images?

No - AWS Lambda ensures that the performance profiles for functions packaged as container images are the same as for those packaged as ZIP archives, including typically sub-second start up times.

### Q: How Will I Be Charged for Deploying Lambda Functions as Container Images?

There is no additional charge for packaging and deploying functions as container images to AWS Lambda. When you invoke your function deployed as a container image, you pay the regular price for requests and execution duration. To learn more, visit [AWS Lambda pricing](https://aws.amazon.com/lambda/pricing/). You will be charged for storing your container images in Amazon ECR at the standard ECR prices. To learn more, visit [Amazon ECR pricing](https://aws.amazon.com/ecr/pricing/).

### Q: What is the Lambda Runtime Interface Emulator (RIE)?

The Lambda Runtime Interface Emulator is a proxy for the Lambda [Runtime API](https://docs.aws.amazon.com/lambda/latest/dg/runtimes-api.html),which allows customers to locally test their Lambda function packaged as a container image. It is a lightweight web server that converts HTTP requests to JSON events and emulates the Lambda Runtime API. It allows you to locally test your functions using familiar tools such as cURL and the Docker CLI (when testing functions packaged as container images). It also simplifies running your application on additional compute services. You can include the Lambda Runtime Interface Emulator in your container image to have it accept HTTP requests natively instead of the JSON events required for deployment to Lambda. This component does not emulate the Lambda orchestrator, or security and authentication configurations. The Runtime Interface Emulator is open sourced on GitHub. You can get started by downloading and installing it on your local machine.

### Q: Why Do I Need the Lambda Runtime Interface Emulator (RIE) during Local Testing?

The Lambda Runtime API in the running Lambda service accepts JSON events and returns responses. The Lambda Runtime Interface Emulator allows the function packaged as a container image to accept HTTP requests during local testing with tools like cURL, and surface them via the same interface locally to the function. It allows you to use the docker run or docker-compose up command to locally test your lambda application.

### Q: What Function Behaviors Can I Test Locally with the Emulator?

You can use the emulator to test if your function code is compatible with the Lambda environment, runs successfully, and provides the expected output. For example, you can mock test events from different event sources. You can also use it to test extensions and agents built into the container image against the Lambda Extensions API.

### Q: How Does the Runtime Interface Emulator (RIE) Help Me Run My Lambda Compatible Image on Additional Compute Services?

Customers can add the Runtime Interface Emulator as the entry point to the container image or package it as a sidecar to ensure the container image now accepts HTTP requests instead of JSON events. This simplifies the changes required to run their container image on additional compute services. Customers will be responsible for ensuring they follow all security, performance, and concurrency best practices for their chosen environment. RIE is pre-packaged into the AWS Lambda provided images, and is available by default in AWS SAM CLI. Base image providers can use the [documentation](https://docs.aws.amazon.com/lambda/latest/dg/welcome.html) to provide the same experience for their base images.

### Q: How Can I Deploy My Existing Containerized Application to AWS Lambda?

You can deploy a containerized application to AWS Lambda if it meets the below requirements:

1. The container image must implement the Lambda Runtime API. We have open-sourced a set of software packages, Runtime Interface Clients (RIC), that implement the Lambda Runtime API, allowing you to seamlessly extend your preferred base images to be Lambda compatible.
2. The container image must be able to run on a read-only filesystem. Your function code can access a writable /tmp directory storage of 512 MB. If you are using an image that requires a writable root directory, configure it to write to the /tmp directory.
3. The files required for the execution of function code can be read by the default Lambda user. Lambda defines a default Linux user with least-privileged permissions that follows security best practices. You need to verify that your application code does not rely on files that are restricted by other Linux users for execution.
4. It is a Linux based container image.

## AWS Lambda Snapstart

Close all

### Q. What is AWS Lambda SnapStart?

AWS Lambda SnapStart for Java delivers up to 10x faster function startup performance. For on-demand functions, the initialization phase (where AWS Lambda loads the function’s code and initializes external dependencies) is the largest contributor to start-up latency, and happens on the first invoke. With Lambda SnapStart, Lambda initializes the one-time initialization function code ahead of time when you publish a function version, instead of when you first invoke the function. Then, Lambda takes a snapshot and caches the memory and disk state of the initialized  [execution environment](https://docs.aws.amazon.com/lambda/latest/dg/lambda-runtime-environment.html). When you invoke the function—and as it scales up—Lambda resumes the function from the cached snapshot instead of initializing the function from scratch.

### Q. How Do I Configure My Lambda Function to Use Lambda SnapStart?

Lambda SnapStart is a simple function level configuration that can be configured for new and existing Java functions by using Lambda API, the AWS Management Console, AWS Command Line Interface (CLI), AWS SDK, AWS Cloud Development Kit (CDK), AWS CloudFormation, and the AWS Serverless Application Model (SAM). When you configure Lambda SnapStart, every function version that is published thereafter benefits from the improved startup performance offered by Lambda SnapStart. To learn more about Lambda SnapStart, see the [documentation](https://docs.aws.amazon.com/lambda/latest/dg/snapstart.html).

### Q. How Do I Choose between Lambda SnapStart and Provisioned Concurrency (PC)?

Lambda SnapStart is a performance optimization that helps your Java functions to achieve up to 10x faster start-up times by reducing the variable latency incurred during execution of one-time initialization code. Lambda SnapStart works broadly across all functions in your application or account at no additional cost. When a customer publishes a function version with Lambda SnapStart, the function’s code is initialized ahead of time, instead of being initialized on the first invoke. Lambda then takes a snapshot of the initialized execution environment and persists it in a tiered cache for low-latency access. When the function is first invoked and then scaled, Lambda resumes the function from the cached snapshot instead of initializing from scratch, driving a lower startup latency. While Lambda SnapStart reduces startup latency, it works as a best-effort optimization, and does not guarantee elimination of cold starts. If your application has strict latency requirements and requires double-digit millisecond startup times, we recommend you use PC.

### Q. Which Runtimes Does Lambda SnapStart Support?

Lambda SnapStart supports the Java 11 runtime. Future versions of Java will be supported after they are released. For all runtimes supported by Lambda, see the [Lambda runtimes documentation](https://docs.aws.amazon.com/lambda/latest/dg/lambda-runtimes.html).

### Q. Can I Enable both Lambda SnapStart and PC on the Same Function?

No. Lambda SnapStart and PC cannot be enabled at the same time, on the same function.

### Q. Can I Configure a Lambda SnapStart Function with a Virtual Private Cloud (VPC)?

Yes. You can configure a Lambda SnapStart function to access resources in a virtual private cloud (VPC). For more information on how to configure your function with a VPC, see the [Lambda documentation](https://docs.aws.amazon.com/lambda/latest/dg/configuration-vpc.html).

### Q. Can I Configure Lambda SnapStart on both X86 and Arm Architectures?

No. You can configure Lambda SnapStart only for functions running on x86 architecture at this time.

### Q. Can I Enable Lambda SnapStart with Amazon Elastic File System (EFS)?

No. You cannot enable Lambda SnapStart with Amazon EFS at this time.

### Q. Can I Enable Lambda SnapStart with Larger Ephemeral Storage (/tmp) beyond 512 MB?

No. You cannot enable Lambda SnapStart with larger ephemeral storage (/tmp) beyond 512 MB at this time.

### Q. Does the Process of Caching and Resuming from Snapshots Introduce Software Compatibility Considerations?

Yes. If your code assumes uniqueness of state, you need to evaluate your code’s resilience to snapshot operations (such as being cloned and resumed). To learn more on uniqueness considerations with Lambda SnapStart, see the [documentation](https://docs.aws.amazon.com/lambda/latest/dg/snapstart-uniqueness.html#snapstart-scanning) and [blog](https://aws.amazon.com/blogs/compute/starting-up-faster-with-aws-lambda-snapstart/) on understanding uniqueness in VM snapshots with Lambda SnapStart.

### Q. Can I Execute My Own Code before a Snapshot is Created or when the Function is Resumed from Snapshot?

Yes. You can implement your own software logic before creating (checkpointing) a snapshot and after restoring a snapshot using runtime hooks. To learn more, see the [Lambda SnapStart documentation](https://docs.aws.amazon.com/lambda/latest/dg/snapstart-runtime-hooks.html).

### Q. Will I Be Charged for Lambda SnapStart?

No. There's no additional cost for enabling Lambda SnapStart. You are charged based on the number of requests for your functions and the duration your code executes based on current [Lambda Pricing](https://aws.amazon.com/lambda/pricing/). Duration charges apply to code that runs in the handler of a function and runtime hooks, as well as initialization code that is declared outside of the handler. Please note that AWS Lambda may periodically recycle execution environments with security patches and rerun your initialization code. For more details, see the [Lambda Programming Model documentation](https://docs.aws.amazon.com/lambda/latest/dg/foundation-progmodel.html).

### Q. How long Do the Snapshots for the Published Function Version Stay Cached with Lambda SnapStart?

With Lambda SnapStart, Lambda keeps a snapshot of the initialized execution environment for the last three published function versions, as long as the published versions continue to receive invokes. The snapshot associated with a published function version expires if it remains inactive for more than 14 days.

### Q. How Can I Encrypt the Snapshots of Initialized Execution Environment Created by Lambda SnapStart?

Snapshots are encrypted be default with customer-unique AWS Key Management Service (KMS) keys owned and managed by the Lambda service. Customers can also encrypt snapshots using a [KMS key](https://docs.aws.amazon.com/kms/latest/developerguide/concepts.html#customer-cmk) owned and managed by the customer.

### Q. Is there a time Limit for how long My Code Initialization Can Run with Lambda SnapStart?

The maximum allowed initialization duration for Lambda SnapStart will match the execution timeout duration you have configured for your function. The maximum configurable execution timeout limit for a function is 15 minutes.

## Provisioned Concurrency

Close all

### Q: What is AWS Lambda Provisioned Concurrency?

Provisioned Concurrency gives you greater control over the performance of your serverless applications. When enabled, Provisioned Concurrency keeps functions initialized and hyper-ready to respond in double-digit milliseconds.

### Q: How Do I Set up and Manage Provisioned Concurrency?

You can configure concurrency on your function through the AWS Management Console, the Lambda API, the AWS CLI, and AWS CloudFormation. The simplest way to benefit from Provisioned Concurrency is by using AWS Auto Scaling. You can use Application Auto Scaling to configure schedules, or have Auto Scaling automatically adjust the level of Provisioned Concurrency in real time as demand changes. To learn more about Provisioned Concurrency, [see the documentation](https://docs.aws.amazon.com/lambda/latest/dg/configuration-concurrency.html).

### Q: Do I Need to Change My Code if I want to Use Provisioned Concurrency?

You don’t need to make any changes to your code to use Provisioned Concurrency. It works seamlessly with all existing functions and runtimes. There is no change to the invocation and execution model of Lambda when using Provisioned Concurrency.

### Q: How Will I Be Charged for Provisioned Concurrency?

Provisioned Concurrency adds a pricing dimension, of ‘Provisioned Concurrency’, for keeping functions initialized. When enabled, you pay for the amount of concurrency that you configure and for the period of time that you configure it. When your function executes while Provisioned Concurrency is configured on it, you also pay for Requests and execution Duration. To learn more about the pricing of Provisioned Concurrency, see [AWS Lambda Pricing](https://aws.amazon.com/lambda/pricing/).

### Q: When Should I Use Provisioned Concurrency?

Provisioned Concurrency is ideal for building latency-sensitive applications, such as web or mobile backends, synchronously invoked APIs, and interactive microservices. You can easily configure the appropriate amount of concurrency based on your application's unique demand. You can increase the amount of concurrency during times of high demand and lower it, or turn it off completely, when demand decreases.

### Q: What Happens if a Function Receives Invocations above the Configured Level of Provisioned Concurrency?

If the concurrency of a function reaches the configured level, subsequent invocations of the function have the latency and scale characteristics of regular Lambda functions. You can restrict your function to only scale up to the configured level. Doing so prevents the function from exceeding the configured level of Provisioned Concurrency. This is a mechanism to prevent undesired variability in your application when demand exceeds the anticipated amount.

## AWS Lambda Functions Powered by Graviton2 Processors

Close all

### Q: What Are AWS Lambda Functions Powered by Graviton2 Processors?

AWS Lambda allows you to run your functions on either x86-based or Arm-based processors. AWS Graviton2 processors are custom built by Amazon Web Services using 64-bit Arm Neoverse cores to deliver increased price performance for your cloud workloads. Customers get the same advantages of AWS Lambda, running code without provisioning or managing servers, automatic scaling, high availability, and only paying for the resources you consume.

### Q: Why Should I Use AWS Lambda Functions Powered by Graviton2 Processors?

AWS Lambda functions powered by Graviton2, using an Arm-based processor architecture designed by AWS, are designed to deliver up to 34% better price performance compared to functions running on x86 processors, for a variety of serverless workloads, such as web and mobile backends, data, and stream processing. With lower latency, up to 19% better performance, a 20% lower cost, and the highest power-efficiency currently available at AWS, Graviton2 functions can power mission critical serverless applications. Customers can configure both existing and new functions to target the Graviton2 processor. They can deploy functions running on Graviton2 as either zip files or container images.

### Q: How Do I Configure My Functions to Run on Graviton2 Processors?

You can configure functions to run on Graviton2 through the AWS Management Console, the AWS Lambda API, the AWS CLI, and AWS CloudFormation by setting the architecture flag to ‘arm64’ for your function.

### Q: How Do I Deploy My Application Built Using Functions Powered by Graviton2 Processors?

There is no change between x86-based and Arm-based functions. Simply upload your code via the AWS Management Console, zip file, or container image, and AWS Lambda automatically runs your code when triggered, without requiring you to provision or manage infrastructure.

### Q: Do I Need an Arm-based Development Machine to Create, Build, and Test Functions Powered by Graviton2 Processors Locally?

Interpreted languages like Python, Java, and Node generally do not require recompilation unless your code references libraries that use architecture specific components. In those cases, you would need to provide the libraries targeted to arm64. For more details, please see the [Getting started with AWS Graviton](https://github.com/aws/aws-graviton-getting-started) page. Non-interpreted languages will require compiling your code to target arm64. While more modern compilers will produce compiled code for arm64, you will need to deploy it into an arm-based environment to test. To learn more about using Lambda functions with Graviton2, please see the [documentation](https://docs.aws.amazon.com/lambda/latest/dg/foundation-arch.html).

### Q: Can an Application Use both Functions Powered by Graviton2 Processors and X86 Processors?

An application can contain functions running on both architectures. AWS Lambda allows you to change the architecture (‘x86\_64’ or ‘arm64’) of your function’s current version. Once you create a specific version of your function, the architecture cannot be changed.

### Q: Does AWS Lambda Support Multi-architecture Container Images?

No. Each function version can only use a single container image.

### Q: Can I Create AWS Lambda Layers that Target Functions Powered by AWS Graviton2 Processors?

Yes. Layers and extensions can be targeted to ‘x86\_64’ or ‘arm64’ compatible architectures. The default architecture for functions and layers is ‘x86\_64’.

### Q: What Languages and Runtimes Are Supported by Lambda Functions Running on Graviton2 Processors?

At launch, customers can use Python, Node.js, Java, Ruby, .Net Core, Custom Runtime (provided.al2), and OCI Base images. To learn more, please see the [AWS Lambda Runtimes](https://docs.aws.amazon.com/lambda/latest/dg/lambda-runtimes.html).

### Q: What is the Pricing of AWS Lambda Functions Powered by AWS Graviton2 Processors? Does the AWS Lambda Free Tier Apply to Functions Powered by Graviton2?

AWS Lambda functions powered by AWS Graviton2 processors are 20% cheaper compared to x86-based Lambda functions. The Lambda free tier applies to AWS Lambda functions powered by x86 and Arm-based architectures.

### Q: How Do I Choose between Running My Functions on Graviton2 Processors or X86 Processors?

Each workload is unique and we recommend customers test their functions to determine the price performance improvement they might see. To do that, we recommend using the [AWS Lambda Power Tuning](https://github.com/alexcasalboni/aws-lambda-power-tuning) tool. We recommend starting with web and mobile backends, data, and stream processing when testing your workloads for potential price performance improvements.

## Amazon EFS for AWS Lambda

Close all

### Q: What is Amazon EFS for AWS Lambda?

With Amazon Elastic File System (Amazon EFS) for AWS Lambda, customers can securely read, write and persist large volumes of data at virtually any scale using a fully managed elastic NFS file system that can scale on demand without the need for provisioning or capacity management. Previously, developers added code to their functions to download data from S3 or databases to local temporary storage, limited to 512MB. With EFS for Lambda, developers don't need to write code to download data to temporary storage in order to process it.

### Q: How Do I Set up Amazon EFS for Lambda?

Developers can easily connect an existing EFS file system to a Lambda function via an [EFS Access Point](https://docs.aws.amazon.com/efs/latest/ug/efs-access-points.html) by using the console, CLI, or SDK. When the function is first invoked, the file system is automatically mounted and made available to function code. You can learn more in the documentation.

### Q: Do I Need to Configure My Function with VPC Settings before I Can Use My Amazon EFS File System?

Yes. Mount targets for Amazon EFS are associated with a subnet in a VPC. The AWS Lambda function needs to be configured to access that VPC.

### Q: Who Should Use Amazon EFS for Lambda?

Using EFS for Lambda is ideal for building machine learning applications or loading large reference files or models, processing or backing up large amounts of data, hosting web content, or developing internal build systems. Customers can also use EFS for Lambda to keep state between invocations within a stateful microservice architecture, in a Step Functions workflow, or sharing files between serverless applications and instance or container-based applications.

### Q: Will My Data Be Encrypted in Transit?

Yes. Data encryption in transit uses industry-standard Transport Layer Security (TLS) 1.2 to encrypt data sent between AWS Lambda functions and the Amazon EFS file systems.

### Q: Is My Data Encrypted at Rest?

Customers can provision Amazon EFS to encrypt data at rest. Data encrypted at rest is transparently encrypted while being written, and transparently decrypted while being read, so you don’t have to modify your applications. Encryption keys are managed by the AWS Key Management Service (KMS), eliminating the need to build and maintain a secure key management infrastructure.

### Q: How Will I Be Charged for Amazon EFS for AWS Lambda?

There is no additional charge for using Amazon EFS for AWS Lambda. Customers pay the standard price for AWS Lambda and for Amazon EFS. When using Lambda and EFS in the same availability zone, customers are not charged for data transfer. However, if they use VPC peering for Cross-Account access, they will incur data transfer charges. To learn more, please see [Pricing](https://aws.amazon.com/lambda/pricing/).

### Q: Can I Associate More than One Amazon EFS File System with My AWS Lambda Function?

No. Each Lambda function will be able to access one EFS file system.

### Q: Can I Use the Same Amazon EFS File System across Multiple Functions, Containers, and Instances?

Yes. Amazon EFS supports Lambda functions, ECS and Fargate containers, and EC2 instances. You can share the same file system and use IAM policy and Access Points to control what each function, container, or instance has access to.  

## Lambda Functions URLs

Close all

### Q: Do AWS Lambda Functions Support HTTP(S) Endpoints?

Yes. Lambda functions can be configured with a function URL, a built-in HTTPS endpoint that can be invoked using the browser, curl, and any HTTP client. Function URLs are an easy way to get started building HTTPS accessible functions.

### Q: How Do I Configure a Lambda Function URL for My Function?

You can configure a function URL for your function through the AWS Management Console, the AWS Lambda API, the AWS CLI, AWS CloudFormation, and the AWS Serverless Application Model. Function URLs can be enabled on the $LATEST unqualified version of your function, or on any function alias. To learn more about configuring a function URL, [see the documentation](https://docs.aws.amazon.com/lambda/latest/dg/welcome.html).

### Q: How Do I Secure My Lambda Function URL?

Lambda function URLs are secured with IAM authorization by default. You can choose to disable IAM authorization to create a public endpoint or if you plan to implement custom authorization as part of the function’s business logic.

### Q: How Do I Invoke My Function with a Lambda Function URL?

You can easily invoke your function from your web browser by navigating to the Lambda URL, from your client application’s code using an HTTP library, or from the command line using curl.

### Q: Do Lambda Function URLs Work with Function Versions and Aliases?

Yes. Lambda function URLs can be enabled on a function or function alias. If no alias is specified, the URL will point to $LATEST by default. Function URLs cannot target an individual function version.

### Q: Can I Enable Custom Domains for My Lambda Function URL?

Custom domain names are not currently supported with function URLs. You can use a custom domain with your function URL by creating an Amazon CloudFront distribution and a CNAME to map your custom domain to your CloudFront distribution name. Then, map your CloudFront distribution domain name to be routed to your function URL as an origin.

### Q: Can Lambda Function URLs Be Used to Invoke a Function in a VPC?

Yes, function URLs can be used to invoke a Lambda function in a VPC.

### Q: What is the Pricing for Using Lambda Function URLs?

There is no additional charge for using function URLs. You pay the standard price for AWS Lambda. To learn more, please see [AWS Lambda Pricing](https://aws.amazon.com/lambda/pricing/).

## Lambda@Edge

Close all

### Q: What is Lambda@Edge?

[Lambda@Edge](https://aws.amazon.com/lambda/edge/) allows you to run code across AWS locations globally without provisioning or managing servers, responding to end-users at the lowest network latency. You just upload your Node.js or Python code to AWS Lambda and configure your function to be triggered in response to [Amazon CloudFront](https://aws.amazon.com/cloudfront/) requests (i.e., when a viewer request lands, when a request is forwarded to or received back from the origin, and right before responding back to the end-user). The code is then ready to execute across AWS locations globally when a request for content is received, and scales with the volume of CloudFront requests globally. Learn more in our [documentation](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/lambda-at-the-edge.html).

### Q: How Do I Use Lambda@Edge?

To use Lambda@Edge, you just upload your code to AWS Lambda and associate a function version to be triggered in response to Amazon CloudFront requests. Your code must satisfy the Lambda@Edge service limits. Lambda@Edge supports Node.js and Python for global invocation by CloudFront events at this time. Learn more in our [documentation](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/lambda-at-the-edge.html).

### Q: When Should I Use Lambda@Edge?

Lambda@Edge is optimized for latency-sensitive use cases where your end viewers are distributed globally. All the information you need to make a decision should be available at the CloudFront edge, within the function and the request. This means that use cases where you are looking to make decisions on how to serve content based on user characteristics (e.g., location, client device, etc.) can now be executed and served close to your users without having to be routed back to a centralized server.

### Q: Can I Deploy My Existing Lambda Functions for Global Invocation?

You can associate existing Lambda functions with CloudFront events for global invocation if the function satisfies the Lambda@Edge service requirements and limits. Read more [here](https://docs.aws.amazon.com/lambda/latest/dg/API_UpdateFunctionConfiguration.html) on how to update your function properties.

### Q: What Amazon CloudFront Events Can Be Used to Trigger My Functions?

Your functions will automatically trigger in response to the following Amazon CloudFront events:

- Viewer Request - This event occurs when an end-user or a device on the Internet makes an HTTP(S) request to CloudFront, and the request arrives at the edge location closest to that user.
- Viewer Response - This event occurs when the CloudFront server at the edge is ready to respond to the end user or the device that made the request.
- Origin Request - This event occurs when the CloudFront edge server does not already have the requested object in its cache, and the viewer request is ready to be sent to your backend origin web server (e.g. Amazon EC2, or Application Load Balancer, or Amazon S3).
- Origin Response - This event occurs when the CloudFront server at the edge receives a response from your backend origin web server.

### Q: How is AWS Lambda@Edge Different from Using AWS Lambda behind Amazon API Gateway?

The difference is that API Gateway and Lambda are regional services. Using [Lambda@Edge](https://aws.amazon.com/lambda/edge/) and [Amazon CloudFront](https://aws.amazon.com/cloudfront/) allows you to execute logic across multiple AWS locations based on where your end viewers are located.

## Scalability and Availability

Close all

### Q: How Available Are AWS Lambda Functions?

AWS Lambda is designed to use replication and redundancy to provide high availability for both the service itself and for the Lambda functions it operates. There are no maintenance windows or scheduled downtimes for either.

### Q: Do My AWS Lambda Functions Remain Available when I Change My Code or Its Configuration?

Yes. When you update a Lambda function, there will be a brief window of time, typically less than a minute, when requests could be served by either the old or the new version of your function.

### Q: Is there a Limit to the Number of AWS Lambda Functions I Can Execute at Once?

No. AWS Lambda is designed to run many instances of your functions in parallel. However, AWS Lambda has a default safety throttle, for the number of concurrent executions per account per region (visit [here](https://docs.aws.amazon.com/lambda/latest/dg/concurrent-executions.html#concurrent-execution-safety-limit) for info on default safety throttle limits). You can also control the maximum concurrent executions for individual AWS Lambda functions, which you can use to reserve a subset of your account concurrency limit for critical functions, or cap traffic rates to downstream resources.  
  
If you wish to submit a request to increase the concurrent execution limit, you can use [Service Quotas](https://docs.aws.amazon.com/servicequotas/latest/userguide/request-quota-increase.html) to request a limit increase request.

### Q: What Happens if My account Exceeds the Default Throttle Limit on Concurrent Executions?

On exceeding the maximum concurrent executions limit, AWS Lambda functions being invoked synchronously will return a throttling error (429 error code). Lambda functions being invoked asynchronously can absorb reasonable bursts of traffic for approximately 15-30 minutes, after which incoming events will be rejected as throttled. In case the Lambda function is being invoked in response to Amazon S3 events, events rejected by AWS Lambda may be retained and retried by S3 for 24 hours. Events from Amazon Kinesis streams and Amazon DynamoDB streams are retried until the Lambda function succeeds or the data expires. Amazon Kinesis and Amazon DynamoDB Streams retain data for 24 hours.

### Q: Are Default Maximum Concurrent Execution Limits Applied on a per Function Level?

The default maximum concurrent execution limit is applied at the account level. However, you can also set limits on individually functions as well (visit [here](https://docs.aws.amazon.com/lambda/latest/dg/configuration-concurrency.html) for info on Reserved Concurrency).

### Q. How Quickly Do My AWS Lambda Functions Scale?

Each synchronously invoked Lambda function can scale at a rate of up to 1000 concurrent executions every 10 seconds. While Lambda's scaling rate is suitable for most use cases, it is particularly ideal for those with predictable or unpredictable bursts of traffic. For example, SLA-bound data processing would require predictable yet rapid scaling to meet processing demand. Similarly, serving breaking news articles, or flash sales could drive unpredictable levels of traffic in a short period of time. Lambda's scaling rate can facilitate such use cases without additional configurations or tooling. Additionally, the concurrency scaling limit is a function-level limit, which means each function in your account scales independently of other functions.

### Q: What Happens if My Lambda Function Fails while Processing an Event?

On failure, Lambda functions being invoked synchronously will respond with an exception. Lambda functions being invoked asynchronously are retried at least 3 times. Events from Amazon Kinesis streams and Amazon DynamoDB streams are retried until the Lambda function succeeds or the data expires. Kinesis and DynamoDB Streams retain data for a minimum of 24 hours.

### Q: What Happens if My Lambda Function Invocations Exhaust the Available Policy?

On exceeding the retry policy for asynchronous invocations, you can configure a “dead letter queue” (DLQ) into which the event will be placed; in the absence of a configured DLQ the event may be rejected. On exceeding the retry policy for stream-based invocations, the data would have already expired and therefore rejected.

### Q: What Resources Can I Configure as a Dead Letter Queue for a Lambda Function?

You can configure an Amazon SQS queue or an Amazon SNS topic as your dead letter queue.

## Security and Access Control

Close all

### Q: How Do I Allow My AWS Lambda Function Access to other AWS Resources?

You grant permissions to your Lambda function to access other resources using an IAM role. AWS Lambda assumes the role while executing your Lambda function, so you always retain full, secure control of exactly which AWS resources it can use. Visit [Setting up AWS Lambda](https://docs.aws.amazon.com/lambda/latest/dg/setting-up.html) to learn more about roles.

### Q: How Do I Control Which Amazon S3 Buckets Can Call Which AWS Lambda Functions?

When you configure an Amazon S3 bucket to send messages to an AWS Lambda function, a resource policy rule will be created that grants access. Visit the [Lambda Developer Guide](https://docs.aws.amazon.com/lambda/latest/dg/welcome.html) to learn more about resource policies and access controls for Lambda functions.

### Q: How Do I Control Which Amazon DynamoDB Table or Amazon Kinesis Stream an AWS Lambda Function Can Poll?

Access controls are managed through the Lambda function role. The role you assign to your Lambda function also determines which resource(s) AWS Lambda can poll on its behalf. Visit the [Lambda Developer Guide](https://docs.aws.amazon.com/lambda/latest/dg/welcome.html) to learn more.

### Q: How Do I Control Which Amazon SQS Queue an AWS Lambda Function Can Poll?

Access controls can be managed by the Lambda function role or a resource policy setting on the queue itself. If both policies are present, the more restrictive of the two permissions will be applied.

### Q: How Do I Access Resources in Amazon VPC from My AWS Lambda Function?

You can enable Lambda functions to access resources in your VPC by specifying the subnet and security group as part of your function configuration. Lambda functions configured to access resources in a particular VPC will not have access to the internet as a default configuration. To grant internet to these functions, use [internet gateways](https://docs.aws.amazon.com/vpc/latest/userguide/extend-intro.html). By default, Lambda functions communicate with resources in a dual-stack VPC over IPv4. You can configure your functions to access resources in a dual-stack VPC over IPv6. For more details on Lambda functions configured with VPC, see [Lambda Private Networking with VPC](https://docs.aws.amazon.com/lambda/latest/dg/foundation-networking.html).

### Q: What is Code Signing for AWS Lambda?

Code Signing for AWS Lambda offers trust and integrity controls that enable you to verify that only unaltered code from approved developers is deployed in your Lambda functions. You can use [AWS Signer](https://docs.aws.amazon.com/signer/latest/developerguide/Welcome.html), a fully-managed code signing service, to digitally sign code artifacts and configure your Lambda functions to verify the signatures at deployment. Code Signing for AWS Lambda is currently only available for functions packaged as ZIP archives.

### Q: How Do I Create Digitally Signed Code Artifacts?

You can create digitally signed code artifacts using a [Signing Profile](https://docs.aws.amazon.com/signer/latest/api/API_SigningProfile.html) through the AWS Signer console, the Signer API, SAM CLI or AWS CLI. To learn more, please see the [documentation for AWS Signer](https://docs.aws.amazon.com/signer/latest/api/Welcome.html).

### Q: How Do I Configure My Lambda Functions to Enable Code Signing?

You can enable code signing by creating a Code Signing Configuration through the AWS Management Console, the Lambda API, the AWS CLI, AWS CloudFormation, and AWS SAM. Code Signing Configuration helps you specify the approved signing profiles and configure whether to warn or reject deployments if signature checks fail. Code Signing Configurations can be attached to individual Lambda functions to enable the code signing feature. Such functions now start verifying signatures at deployment.

### Q: What Signature Checks Does AWS Lambda Perform on Deployment?

AWS Lambda can perform the following signature checks at deployment:

• Corrupt signature - This occurs if the code artifact has been altered since signing.  
• Mismatched signature - This occurs if the code artifact is signed by a signing profile that is not approved.  
• Expired signature - This occurs if the signature is past the configured expiry date.  
• Revoked signature - This occurs if the signing profile owner revokes the signing jobs.

To learn more, please see the [AWS Lambda documentation](https://docs.aws.amazon.com/lambda/latest/dg/welcome.html).

### Q: Can I Enable Code Signing for Existing Functions?

Yes, you can enable code signing for existing functions by attaching a code signing configuration to the function. You can do this using the AWS Lambda console, the Lambda API, the AWS CLI, AWS CloudFormation, and AWS SAM.

### Q: Is there Any Additional Cost for Using Code Signing for AWS Lambda?

There is no additional cost when using Code Signing for AWS Lambda. You pay the standard price for AWS Lambda. To learn more, please see [Pricing](https://aws.amazon.com/lambda/pricing/).

## Advanced Logging Controls

Close all

### Q: What Advanced Logging Controls Are Supported on Lambda?

To provide you a simplified and enhanced logging experience by default, AWS Lambda offers advanced logging controls such as the ability to natively capture Lambda function logs in JSON structured format, control the log level filtering of Lambda function logs without making any code changes, and customize the Amazon CloudWatch log group Lambda sends logs to.

### Q: What Can I Use Advanced Logging Controls For?

You can capture Lambda function logs in JSON structured format without having to use your own logging libraries. JSON structured logs make it easier to search, filter, and analyze large volumes of log entries. You can control the log level filtering of Lambda function logs without making any code changes, which enables you to choose the required logging granularity level for Lambda functions without sifting through large volumes of logs when debugging and troubleshooting errors. You can also set which [Amazon CloudWatch](https://aws.amazon.com/cloudwatch/) log group Lambda sends logs to, making it easier to aggregate logs from multiple functions within an application in one place. You can then apply security, governance, and retention policies to logs at the application level rather than individually to every function.

### Q. How Do I Use Advanced Logging Controls?

You can specify advanced logging controls for your Lambda functions using AWS Lambda API, AWS Lambda console, AWS CLI, AWS Serverless Application Model (SAM), and AWS CloudFormation. To learn more, visit the [launch blog post](https://aws.amazon.com/blogs/compute/introducing-advanced-logging-controls-for-aws-lambda-functions/) for advanced logging controls or the [Lambda Developer Guide](https://docs.aws.amazon.com/lambda/latest/dg/monitoring-cloudwatchlogs.html#monitoring-cloudwatchlogs-advanced).

### Q. Can I Use My Own Logging Libraries to Generate JSON Structured Logs for My Lambda Function?

Yes, you can use your own logging libraries to generate Lambda logs in JSON structured format. To ensure your logging libraries work seamlessly with Lambda’s native JSON structured logging capability, Lambda will not double-encode any logs generated by your function that are already JSON encoded. You can also use [Powertools for AWS Lambda](https://github.com/aws-powertools/) library to capture Lambda logs in JSON structured format.

### Q. How Will I Be Charged for Using the Advanced Logging Controls?
There is no additional charge for using advanced logging controls on Lambda. You will continue to be charged for ingestion and storage of your Lambda logs by Amazon CloudWatch Logs. See [CloudWatch pricing page](https://aws.amazon.com/cloudwatch/pricing/) for log pricing details.