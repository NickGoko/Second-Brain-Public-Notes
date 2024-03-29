---
tags:
  - cloud/aws
---


# FAQ
## General

Close all

### Q: What is AWS X-Ray?

AWS X-Ray helps developers analyze and debug production, distributed applications, such as those built using a microservices architecture. With X-Ray, you can understand how your application and its underlying services are performing to identify and troubleshoot the root cause of performance issues and errors. X-Ray provides an end-to-end view of requests as they travel through your application, and shows a map of your application’s underlying components. You can use X-Ray to analyze both applications in development and in production, from simple three-tier applications to complex microservices applications consisting of thousands of services.

### Q: Why Should I Use X-Ray?

Currently, if you build and run distributed applications, you have to rely on a per-service or per-resource process to track requests for your application as it travels across various components that make up your application. This problem is further complicated by the varying log formats and storage mediums across frameworks, services, and resources your application runs on or uses. This makes it difficult to correlate the various pieces of data and create an end-to-end picture of a request from the time it originates at the end-user or service to when a response is returned by your application. X-Ray provides a user-centric model, instead of service-centric or resource-centric model, for collecting data related to requests made to your application. This model enables you to create a user-centric picture of requests as they travel across services and resources. By correlating and aggregating data on your behalf, X-Ray enables you to focus on improving the experience for end-users of your application.

### Q: What Can I Do with X-Ray?

X-Ray makes it easy for you to:

- **Create a service map** – By tracking requests made to your applications, X-Ray can create a map of services used by your application. This provides you with a view of connections among services in your application, and enables you to create a dependency tree, detect latency or errors when working across AWS Availability Zones or Regions, zero in on services not operating as expected, and so on.
- **Identify errors and bugs** – X-Ray can automatically highlight bugs or errors in your application code by analyzing the response code for each request made to your application. This enables easy debugging of application code without requiring you to reproduce the bug or error.
- **Build your own analysis and visualization apps** – X-Ray provides a set of query APIs you can use to build your own analysis and visualizations apps that use the data that X-Ray records.

## Core Concepts

Close all

### Q: What is a Trace?

An X-Ray trace is a set of data points that share the same trace ID. For example, when a client makes a request to your application, it is assigned a unique trace ID. As the request makes its way through services in your application, the services relay information regarding the request back to X-Ray using this unique trace ID. The piece of information relayed by each service in your application to X-Ray is a segment, and a trace is a collection of segments.

### Q: What is a Segment?

An X-Ray segment encapsulates all the data points for a single component (for example, authorization service) of the distributed application. Segments include system-defined and user-defined data in the form of annotations and are composed of one or more sub-segments that represent remote calls made from the service. For example, when your application makes a call to a database in response to a request, it creates a segment for that request with a sub-segment representing the database call and its result. The sub-segment can contain data such as the query, table used, timestamp, and error status.

### Q: What is an Annotation?

An X-Ray annotation is system-defined or user-defined data associated with a segment. A segment can contain multiple annotations. System-defined annotations include data added to the segment by AWS services, whereas user-defined annotations are metadata added to a segment by a developer. For example, a segment created by your application can automatically be injected with region data for AWS service calls, whereas you might choose to add region data yourself for calls made to non-AWS services.

### Q: What Are Errors?

X-Ray errors are system annotations associated with a segment for a call that results in an error response. The error includes the error message, stack trace, and any additional information (for example, version or commit ID) to associate the error with a source file.

### Q: What is Sampling?

To provide a performant and cost-effective experience, X-Ray does not collect data for every request that is sent to an application. Instead, it collects data for a statistically significant number of requests. X-Ray should not be used as an audit or compliance tool because it does not guarantee data completeness.

### Q: What is the X-Ray Daemon?

The X-Ray daemon collects traces and sends them to the X-Ray service for aggregation, analysis, and storage. The daemon makes it easier for you to send data to the X-Ray service, instead of using the APIs directly.

## Using AWS X-Ray

Close all

### Q: How Do I Get Started with X-Ray?

You can get started with X-Ray by including the X-Ray language SDK in your application and installing the X-Ray daemon. For more information see the X-Ray [user guide](https://docs.aws.amazon.com/xray/latest/devguide/aws-xray.html).

### Q: What Types of Applications Can I Use with X-Ray?

X-Ray can be used with distributed applications of any size to trace and debug both synchronous requests and asynchronous events. For example, X-Ray can be used to trace web requests made to a web application or asynchronous events that utilize Amazon SQS queues.

### Q: Which AWS Services Can I Use with X-Ray?

You can use X-Ray with applications running on EC2, ECS, Lambda, Amazon SQS, Amazon SNS and Elastic Beanstalk. In addition, the X-Ray SDK automatically captures metadata for API calls made to AWS services using the AWS SDK. In addition, the X-Ray SDK provides add-ons for MySQL and PostgreSQL drivers.

### Q: What Code Changes Do I Need to Make to My Application to Use X-Ray?

If you’re using Elastic Beanstalk, you will need to include the language-specific X-Ray libraries in your application code. For applications running on other AWS services, such as EC2 or ECS, you will need to install the X-Ray daemon and instrument your application code.

### Q: Does X-Ray provide an API?

Yes, X-Ray provides a set of APIs for ingesting request data, querying traces, and configuring the service. You can use the X-Ray API to build analysis and visualization applications in addition to those provided by X-Ray.

## Regions

Close all

### Q: In Which Regions is X-Ray Available?

See Regional Products and Services for details.

### Q: Can I Use X-Ray to Track Requests from Applications or Services Spread across Multiple Regions?

Yes, you can use X-Ray to track requests flowing through applications or services across multiple regions. X-Ray data is stored locally to the processed region but with enough information to enable client applications to combine the data and provide a global view of traces. Region annotation for AWS services will be added automatically, however, customers will need to instrument custom services to add the regional annotation to make use of the cross-region support.

## Data Handling

Close all

### Q: How long Does it Take for Trace Data to Be Available in X-Ray?

Trace data sent to X-Ray is generally available for retrieval and filtering within 30 seconds of it being received by the service.

### Q: How far back Can I Query the Trace Data? How long Does X-Ray Store Trace Data For?

X-Ray stores trace data for the last 30 days. This enables you to query trace data going back 30 days.

### Q: Why Do I Sometimes See Partial Traces?

X-Ray makes the best effort to present complete trace information. However, in some situations (connectivity issues, delay in receiving segments, and so on) it is possible that trace information provided by the X-Ray APIs will be partial. In those situations, X-Ray tags traces as incomplete or partial.

### Q: My Application Components Run in Their Own AWS Accounts. Can I Use X-Ray to Collect Data across AWS Accounts?

Yes, the X-Ray daemon can assume a role to publish data into an account different from the one in which it is running. This enables you publish data from various components of your application into a central account.