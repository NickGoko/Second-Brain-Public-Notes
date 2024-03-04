---
tags:
  - cloud/aws
---


![](https://i.imgur.com/NZhmSBa.png)  

![](https://i.imgur.com/URTv2kz.png)  

![](https://i.imgur.com/y3toFG8.png)

![](https://i.imgur.com/IOPYBwn.png)

**API Gateway** is <mark style="background: #ABF7F7A6;">a fully managed service that makes it easy for developers to publish, maintain, monitor, and secure APIs at any scale.</mark>

API Gateway supports the following:
- Creating, deploying, and managing a [**REST**](https://en.wikipedia.org/wiki/Representational_state_transfer) application programming interface (API) to expose backend HTTP endpoints, AWS Lambda functions, or other AWS services.
- Creating, deploying, and managing a [**WebSocket**](https://tools.ietf.org/html/rfc6455) API to expose AWS Lambda functions or other AWS services.
- Invoking exposed API methods through the frontend HTTP and WebSocket endpoints.

<mark style="background: #FFB86CA6;">Together with Lambda, API Gateway forms the app-facing part of the AWS serverless infrastructure.</mark>

Back-end services include Amazon EC2, AWS Lambda or any web application (public or private endpoints).

![Amazon API Gateway Overview](https://digitalcloud.training/wp-content/uploads/2022/01/amazon-api-gateway-overview.jpeg)

**API Gateway** <mark style="background: #ADCCFFA6;">handles all the tasks involved in accepting and processing up to hundreds of thousands of concurrent API calls.</mark>

- <mark style="background: #FFB8EBA6;">API calls include traffic management, authorization and access control, monitoring, and API version management.</mark>
- API Gateway provides a REST API that uses JSON.
- API Gateway exposes HTTPS endpoints to define a RESTful API.
- All the APIs created with Amazon API Gateway expose HTTPS endpoints only (does not support unencrypted endpoints).
- <mark style="background: #FFF3A3A6;">An API can present a certificate to be authenticated by the back end.</mark>
- <mark style="background: #FFB86CA6;">Can send each API endpoint to a different target.</mark>
- <mark style="background: #ABF7F7A6;">CloudFront is used as the public endpoint for API Gateway.</mark>  
	Using CloudFront behind the scenes, custom domains, and SNI are supported.
- Supports API keys and Usage Plans for user identification, throttling or quota management.
- Permissions to invoke a method are granted using IAM roles and policies or API Gateway custom authorizers.
- By default API Gateway assigns an internal domain that automatically uses the API Gateway certificates.  
When configuring your APIs to run under a custom domain name you can provide your own certificate.

## Amazon API Gateway Features

The following table describes some of the core features of Amazon API Gateway.

|   |   |
|---|---|
|**API Gateway Feature**|**Benefit**|
|Support for RESTful APIs and WebSocket APIs|With API Gateway, you can create RESTful APIs using either HTTP APIs or REST APIs|
|Private integrations with AWS ELB & AWS Cloud Map|With API Gateway, you can route requests to private resources in your VPC. Using HTTP APIs, you can build APIs for services behind private ALBs, private NLBs, and IP-based services registered in AWS Cloud Map, such as ECS tasks.|
|Metering|Define plans that meter and restrict third-party developer access to APIs.|
|Security|API Gateway provides multiple tools to authorize access to APIs and control service operation access.|
|Resiliency|Manage traffic with throttling so that backend operations can withstand traffic spikes.|
|Operations Monitoring|API Gateway provides a metrics dashboard to monitor calls to services.|
|Lifecycle Management|Operate multiple API versions and multiple stages for each version simultaneously so that existing applications can continue to call previous versions after new API versions are published.|
|AWS Authorization|Support for signature version 4 for REST APIs and WebSocket APIs, IAM access policies, and authorization with bearer tokens (e.g., JWT, SAML) using Lambda functions.|

## Endpoints
![](https://i.imgur.com/wuVzeqc.png)  


An [**API endpoint**](https://docs.aws.amazon.com/apigateway/latest/developerguide/api-gateway-basic-concept.html#apigateway-definition-api-endpoints) <mark style="background: #FFB86CA6;">type is a hostname for an API in API Gateway that is deployed to a specific region.</mark>

_The hostname is of the form_ <mark style="background: #D2B3FFA6;">{api-id}.execute-api.{region}.amazonaws.com.  
</mark>  
<mark style="background: #BBFABBA6;">The API endpoint type can be edge-optimized, regional, or private, depending on where most of your API traffic originates from.</mark>  
![](https://i.imgur.com/zF3YoNq.png)

### Edge-Optimized Endpoint

- <mark style="background: #FFB86CA6;">An edge-optimized API endpoint is best for geographically distributed clients. </mark>API requests are routed to the nearest CloudFront Point of Presence (POP). <mark style="background: #ADCCFFA6;">This is the default endpoint type for API Gateway REST APIs.</mark>
- Edge-optimized APIs capitalize the names of HTTP headers (for example, Cookie).
- CloudFront sorts HTTP cookies in natural order by cookie name before forwarding the request to your origin. For more information about the way CloudFront processes cookies, see Caching Content Based on Cookies.
- Any custom domain name that you use for an edge-optimized API applies across all regions.

### Regional Endpoint

- <mark style="background: #FFB86CA6;">A regional API endpoint is intended for clients in the same region.</mark>
- <mark style="background: #ADCCFFA6;">When a client running on an EC2 instance calls an API in the same region, or when an API is intended to serve a small number of clients with high demands, a regional API reduces connection overhead.</mark>
- For a regional API, any custom domain name that you use is specific to the region where the API is deployed.
- If you deploy a regional API in multiple regions, it can have the same custom domain name in all regions.
- <mark style="background: #FFB8EBA6;">You can use custom domains together with Amazon Route 53 to perform tasks such as latency-based routing.</mark>
- Regional API endpoints pass all header names through as-is.

### Private Endpoint

- <mark style="background: #FFB86CA6;">A private API endpoint is an API endpoint that can only be accessed from your Amazon Virtual Private Cloud (VPC) using an interface VPC endpoint, which is an </mark><mark style="background: #FF5582A6;">endpoint network interface (ENI)</mark> <mark style="background: #FFB86CA6;">that you create in your VPC.</mark>
- Private API endpoints pass all header names through as-is.

The following diagram depicts the three different Amazon API Gateway endpoint types:

![Amazon API Gateway Endpoint Types](https://digitalcloud.training/wp-content/uploads/2022/01/amazon-api-gateway-endpoint-types.jpeg)

## Amazon API Gateway API’s

### API Gateway REST API
- A collection of HTTP resources and methods that are integrated with backend HTTP endpoints, Lambda functions, or other AWS services.
- This collection can be deployed in one or more stages.
- <mark style="background: #ADCCFFA6;">Typically, API resources are organized in a resource tree according to the application logic.</mark>
- Each API resource can expose one or more API methods that have unique HTTP verbs supported by API Gateway.

The following diagram depicts the structure of an API:

![Amazon API Gateway API Structure](https://digitalcloud.training/wp-content/uploads/2022/01/amazon-api-gateway-api-structure.jpeg)

### API Gateway WebSocket API

- A collection of WebSocket routes and route keys that are integrated with backend HTTP endpoints, Lambda functions, or other AWS services.
- The collection can be deployed in one or more stages.
- API methods are invoked through frontend WebSocket connections that you can associate with a registered custom domain name.

## Methods

- API Gateway Methods are HTTP methods associated with an API Gateway resource.
- Each resource URL can have HTTP methods such as: GET, PUT, POST and DELETE.
- AWS also offers the “ANY” method as a catch-all.

## Deployments

Deployments are a snapshot of the APIs resources and methods.

Deployments must be created and associated with a stage for anyone to access the API.

## Stages and Stage Variables

A stage is a logical reference to a lifecycle state of your REST or WebSocket API (for example, ‘dev’, ‘prod’, ‘beta’, ‘v2’).

API stages are identified by API ID and stage name.

![Amazon API Gateway Stages](https://digitalcloud.training/wp-content/uploads/2022/01/amazon-api-gateway-stages.jpeg)

Stage variables are like environment variables for API Gateway.

Stage variables can be used in:
- Lambda function ARN.
- HTTP endpoint.
- Parameter mapping templates.

Use cases for stage variables:

- Configure HTTP endpoints your stages talk to (dev, test, prod etc.).
- Pass configuration parameters to AWS Lambda through mapping templates.

Stage variables are passed to the “context” object in Lambda.

Stage variables are used with Lambda aliases.

You can create a stage variable to indicate the corresponding Lambda alias.

You can create canary deployments for any stage – choose the % of traffic the canary channel receives.

## Mapping Templates

Mapping templates can be used to modify request / responses.  
Rename parameters.

Modify body content.

Add headers.

Map JSON to XML for sending to backend or back to client.

Uses Velocity Template Language (VTL).

Filter output results (remove unnecessary data).

## Caching

You can add caching to API calls by provisioning an Amazon API Gateway cache and specifying its size in gigabytes.

Caching allows you to cache the endpoint’s response.

Caching can reduce the number of calls to the backend and improve the latency of requests to the API.

API Gateway caches responses for a specific amount of time (time to live or TTL).

The default TTL is 300 seconds (min 0, max 3600).

Caches are defined per stage.

![Amazon API Gateway Cache](https://digitalcloud.training/wp-content/uploads/2022/01/amazon-api-gateway-cache.jpeg)

You can encrypt caches.

The cache capacity is between 0.5GB to 237GB.

It is possible to override cache settings for specific methods.

You can flush the entire cache (invalidate it) immediately if required.

Clients can invalidate the cache with the header: Cache-Control: max-age=0 .

## API Throttling

API Gateway sets a limit on a steady-state rate and a burst of request submissions against all APIs in your account.

Limits:

- By default API Gateway limits the steady-state request rate to 10,000 requests per second.
- The maximum concurrent requests is 5,000 requests across all APIs within an AWS account.
- If you go over 10,000 requests per second or 5,000 concurrent requests you will receive a 429 Too Many Requests error response.

Upon catching such exceptions, the client can resubmit the failed requests in a way that is rate-limiting, while complying with the API Gateway throttling limits.

Amazon API Gateway provides two basic types of throttling-related settings:

- **Server-side** throttling limits are applied across all clients. These limit settings exist to prevent your API—and your account—from being overwhelmed by too many requests.
- **Per-client** throttling limits are applied to clients that use API keys associated with your usage policy as a client identifier.

API Gateway throttling-related settings are applied in the following order:

1. Per-client per-method throttling limits that you set for an API stage in a usage plan.
2. Per-client throttling limits that you set in a usage plan.
3. Default per-method limits and individual per-method limits that you set in API stage settings.
4. Account-level throttling.

## Integrations and Method Requests / Responses

A method represents a client-facing interface by which the client calls the API to access back-end resources.

A Method resource is integrated with an Integration resource.

API methods are integrated with backend endpoints using API integrations.

Backend endpoints are known as “integration endpoints”.

### Integration Request

The internal interface of a WebSocket API route or REST API method in API Gateway, in which you map the body of a route request or the parameters and body of a method request to the formats required by the backend.

### Integration Response

The internal interface of a WebSocket API route or REST API method in API Gateway, in which you map the status codes, headers, and payload that are received from the backend to the response format that is returned to a client app.

### Method Request

The public interface of a REST API method in API Gateway that defines the parameters and body that an app developer must send in requests to access the backend through the API

### Method Response

The public interface of a REST API that defines the status codes, headers, and body models that an app developer should expect in responses from the API.

### Mapping Template

A script in [**Velocity Template Language (VTL)**](http://velocity.apache.org/engine/devel/vtl-reference.html) that transforms a request body from the frontend data format to the backend data format, or that transforms a response body from the backend data format to the frontend data format.

Mapping templates can be specified in the integration request or in the integration response. They can reference data made available at run time as context and stage variables.

The mapping can be as simple as an [**identity transform**](https://en.wikipedia.org/wiki/Identity_transform) that passes the headers or body through the integration as-is from the client to the backend for a request.

The same is true for a response, in which the payload is passed from the backend to the client.

## Integration Type

You choose an API integration type according to the types of integration endpoint you work with and how you want data to pass to and from the integration endpoint.

For a Lambda function, you can have the Lambda proxy integration, or the Lambda custom integration.

For an HTTP endpoint, you can have the HTTP proxy integration or the HTTP custom integration.

For an AWS service action, you have the AWS integration of the non-proxy type only. API Gateway also supports the mock integration, where API Gateway serves as an integration endpoint to respond to a method request.

The Lambda custom integration is a special case of the AWS integration, where the integration endpoint corresponds to the [**function-invoking action**](https://docs.aws.amazon.com/lambda/latest/dg/API_Invoke.html) of the Lambda service.

Programmatically, you choose an integration type by setting the [**type**](https://docs.aws.amazon.com/apigateway/api-reference/resource/integration/#type) property on the [**Integration**](https://docs.aws.amazon.com/apigateway/api-reference/resource/integration/) resource.

For the Lambda proxy integration, the value is AWS_PROXY.

For the Lambda custom integration and all other AWS integrations, it is AWS.

For the HTTP proxy integration and HTTP integration, the value is HTTP_PROXY and HTTP, respectively.

For the mock integration, the type value is MOCK.

The following list summarizes the supported integration types:

### AWS Integration

This type of integration lets an API expose AWS service actions.

In AWS integration, you must configure both the integration request and integration response and set up necessary data mappings from the method request to the integration request, and from the integration response to the method response.

![Amazon API Gateway Method AWS Lambda](https://digitalcloud.training/wp-content/uploads/2022/01/amazon-api-gateway-method-aws-lambda.jpeg)

### AWS_PROXY Integration

This type of integration lets an API method be integrated with the Lambda function invocation action with a flexible, versatile, and streamlined integration setup.

This integration relies on direct interactions between the client and the integrated Lambda function.

With this type of integration, also known as the Lambda proxy integration, you do not set the integration request or the integration response.

API Gateway passes the incoming request from the client as the input to the backend Lambda function.

The integrated Lambda function takes the [**input of this format**](https://docs.aws.amazon.com/apigateway/latest/developerguide/set-up-lambda-proxy-integrations.html#api-gateway-simple-proxy-for-lambda-input-format) and parses the input from all available sources, including request headers, URL path variables, query string parameters, and applicable body.

The function returns the result following this [**output format**](https://docs.aws.amazon.com/apigateway/latest/developerguide/set-up-lambda-proxy-integrations.html#api-gateway-simple-proxy-for-lambda-output-format).

This is the preferred integration type to call a Lambda function through API Gateway and is not applicable to any other AWS service actions, including Lambda actions other than the function-invoking action.

![Amazon API Gateway Integration Lambda Proxy](https://digitalcloud.training/wp-content/uploads/2022/01/amazon-api-gateway-integration-lambda-proxy.jpeg)

### HTTP Integration

This type of integration lets an API expose HTTP endpoints in the backend.

With the HTTP integration, also known as the HTTP custom integration, you must configure both the integration request and integration response.

You must set up necessary data mappings from the method request to the integration request, and from the integration response to the method response.

### HTTP_PROXY Integration

The HTTP proxy integration allows a client to access the backend HTTP endpoints with a streamlined integration setup on single API method.

You do not set the integration request or the integration response.

API Gateway passes the incoming request from the client to the HTTP endpoint and passes the outgoing response from the HTTP endpoint to the client.

### MOCK Integration

This type of integration lets API Gateway return a response without sending the request further to the backend.

This is useful for API testing because it can be used to test the integration set up without incurring charges for using the backend and to enable collaborative development of an API.

In collaborative development, a team can isolate their development effort by setting up simulations of API components owned by other teams by using the MOCK integrations.

It is also used to return CORS-related headers to ensure that the API method permits CORS access.

In fact, the API Gateway console integrates the OPTIONS method to support CORS with a mock integration.

[**Gateway responses**](https://docs.aws.amazon.com/apigateway/latest/developerguide/customize-gateway-responses.html) are other examples of mock integrations.

## Usage Plans and API Keys

A usage plan specifies who can access one or more deployed API stages and methods — and how much and how fast they can access them.

You can use a usage plan to configure throttling and quota limits, which are enforced on individual client API keys.

The plan uses API keys to identify API clients and meters access to the associated API stages for each key.

It also lets you configure throttling limits and quota limits that are enforced on individual client API keys.

API keys are alphanumeric string values that you distribute to app developer customers to grant access to your API.

You can use API keys together with [**usage plans**](https://docs.aws.amazon.com/apigateway/latest/developerguide/api-gateway-api-usage-plans.html) or [**Lambda authorizers**](https://docs.aws.amazon.com/apigateway/latest/developerguide/apigateway-use-lambda-authorizer.html) to control access to your APIs.

API Gateway can generate API keys on your behalf, or you can import them from a [**CSV file**](https://docs.aws.amazon.com/apigateway/latest/developerguide/api-key-file-format.html).

You can generate an API key in API Gateway or import it into API Gateway from an external source.

![Amazon API Gateway Usage Plans and API Keys](https://digitalcloud.training/wp-content/uploads/2022/01/amazon-api-gateway-usage-plans-and-api-keys.jpeg)

## Same Origin Policy

Used to prevent cross-site scripting attacks.

Web browser permits scripts in a first web page to access data in a second web page but only if the web pages have the same origin.

This is enforced by web browsers.

## Cross-origin Resource Sharing (CORS)

<mark style="background: #ADCCFFA6;">Can enable Cross Origin Resource Sharing (CORS) for multiple domain use with JavaScript/AJAX.</mark>

CORS is one way that the server at the other end (not the client code in the browser) can relax the same-origin policy.

CORS allows restricted resources (e.g. fonts) on a web page to be requested from another domain outside the domain from which the first resource was shared.

Using CORS:
- Can enable CORS on API Gateway if using JavaScript / AJAX.
- Can be used to enable requests from domains other than the APIs domain.
- Allows the sharing of resources between different domains.
- The method (GET, PUT, POST etc.) for which you will enable CORS must be available in the API Gateway API before you enable CORS.
- If CORS is not enabled and an API resource received requests from another domain the request will be blocked.
- Enable CORS on the API resources using the selected methods under the API Gateway.

## Identity and Access Management

There are several mechanisms for controlling and managing access to an API.

These mechanisms include:

- Resource-based policies.
- Standard IAM Roles and Policies (identity-based policies).
- IAM Tags.
- Endpoint policies for interface VPC endpoints.
- Lambda authorizers.
- Amazon Cognito user pools.

### IAM Resource-Based Policies

Amazon API Gateway resource policies are JSON policy documents that you attach to an API to control whether a specified principal (typically an IAM user or role) can invoke the API.

You can use API Gateway resource policies to allow your API to be securely invoked by:

- Users from a specified AWS account.
- Specified source IP address ranges or CIDR blocks.
- Specified virtual private clouds (VPCs) or VPC endpoints (in any account).
- You can use resource policies for all API endpoint types in API Gateway: private, edge-optimized, and Regional.

![Amazon API Gateway Resource-Based Policy](https://digitalcloud.training/wp-content/uploads/2022/01/amazon-api-gateway-resource-based-policy.jpeg)

### IAM Identity-Based Policies

You need to create IAM policies and attach to users / roles.

API Gateway verifies IAM permissions passed by the calling application.

Leverages sigv4 capability where IAM credentials are passed in headers.

Handles authentication and authorization.

Great for user / roles within your AWS account.

### Lambda Authorizer

Use AWS Lambda to validate the token in the header being passed.

Option to cache the result of the authentication.

Lambda must return an IAM policy for the user.

You pay per Lambda invocation.

Handles authentication and authorization.

Good for using OAuth, SAML or 3rd party authentication.

![Amazon API Gateway Lambda Authorizer](https://digitalcloud.training/wp-content/uploads/2022/01/amazon-api-gateway-lambda-authorizer.jpeg)

### Cognito User Pools

A user pool is a user directory in Amazon Cognito.

With a user pool, users can sign in to a web or mobile app through Amazon Cognito.

Users can also sign in through social identity providers like Google, Facebook, Amazon, or Apple, and through SAML identity providers.

Whether your users sign in directly or through a third party, all members of the user pool have a directory profile that you can access through a Software Development Kit (SDK).

![Amazon API Gateway Cognito User Pool](https://digitalcloud.training/wp-content/uploads/2022/01/amazon-api-gateway-cognito-user-pool.jpeg)

User pools provide:

- Sign-up and sign-in services.
- A built-in, customizable web UI to sign in users.
- Social sign-in with Facebook, Google, Login with Amazon, and Sign in with Apple, as well as sign-in with SAML identity providers from your user pool.
- User directory management and user profiles.
- Security features such as multi-factor authentication (MFA).

## Additional Features and Benefits

API Gateway provides several features that assist with creating and managing APIs:

- Metering – Define plans that meter and restrict third-party developer access to APIs.
- Security – API Gateway provides multiple tools to authorize access to APIs and control service operation access.
- Resiliency – Manage traffic with throttling so that backend operations can withstand traffic spikes.
- Operations Monitoring – API Gateway provides a metrics dashboard to monitor calls to services.
- Lifecycle Management – Operate multiple API versions and multiple stages for each version simultaneously so that existing applications can continue to call previous versions after new API versions are published.

API Gateway provides robust, secure, and scalable access to backend APIs and hosts multiple versions and release stages for your APIs.

You can create and distribute API Keys to developers.

Option to use AWS Sig-v4 to authorize access to APIs.

You can throttle and monitor requests to protect your backend.

API Gateway allows you to maintain a cache to store API responses.

SDK Generation for iOS, Android, and JavaScript.

Reduced latency and distributed denial of service protection using CloudFront.

Request/response data transformation and API mocking.

Resiliency through throttling rules based on the number of requests per second for each HTTP method (GET, PUT).

Throttling can be configured at multiple levels including Global and Service Call.

A cache can be created and specified in gigabytes (not enabled by default).

Caches are provisioned for a specific stage of your APIs.

Caching features include customizable keys and time-to-live (TTL) in seconds for your API data which enhances response times and reduces load on back-end services.

API Gateway can scale to any level of traffic received by an API.

## Logging and Monitoring

The Amazon API Gateway logs (near real time) back-end performance metrics such as API calls, latency, and error rates to CloudWatch.

You can monitor through the API Gateway dashboard (REST API) allowing you to visually monitor calls to the services.

API Gateway also meters utilization by third-party developers and the data is available in the API Gateway console and through APIs.

Amazon API Gateway is integrated with AWS CloudTrail to give a full auditable history of the changes to your REST APIs.

All API calls made to the Amazon API Gateway APIs to create, modify, delete, or deploy REST APIs are logged to CloudTrail.

Understanding the following metrics is useful for the exam:

- Monitor the IntegrationLatency metrics to measure the responsiveness of the backend.
- Monitor the Latency metrics to measure the overall responsiveness of your API calls.
- Monitor the CacheHitCount and CacheMissCount metrics to optimize cache capacities to achieve a desired performance.

![Amazon API Gateway Monitoring and Logging](https://digitalcloud.training/wp-content/uploads/2022/01/amazon-api-gateway-monitoring-and-logging.jpeg)

## Open API / Swagger

Can import existing Swagger / Open API 3.0 definitions (written in YAML or JSON) to API Gateway.

This is a common way of defining REST APIs using API definition as code.

Can also export current APIs as Swagger / Open API 3.0 definition.

Uses the API Gateway  Import API feature to import an API from an external definition.

With the import API you can either create a new API by submitting a POST request that includes a Swagger definition in the payload and endpoint configuration or you can update an existing API by using a PUT request that contains a Swagger definition or merge a definition with an existing API.

You specify the options using a mode query parameter in the request URL.

## Charges

With Amazon API Gateway, you only pay when your APIs are in use.

There are no minimum fees or upfront commitments.

You pay only for the API calls you receive, and the amount of data transferred out.

There are no data transfer out charges for Private APIs (however, AWS PrivateLink charges apply when using Private APIs in Amazon API Gateway).

Amazon API Gateway also provides optional data caching charged at an hourly rate that varies based on the cache size you select.

The API Gateway free tier includes one million API calls per month for up to 12 months.

![[Amazon API Gateway]]

# FAQ
## General

[Q: What is Amazon API Gateway? »](https://aws.amazon.com/api-gateway/faqs//#)

**Q: What is Amazon API Gateway?**  
Amazon API Gateway is a fully managed service that makes it easy for developers to publish, maintain, monitor, and secure APIs at any scale. With a few clicks in the AWS Management Console, you can create an API that acts as a “front door” for applications to access data, business logic, or functionality from your back-end services, such as applications running on Amazon Elastic Compute Cloud (Amazon EC2), Amazon Elastic Container Service (Amazon ECS) or AWS Elastic Beanstalk, code running on AWS Lambda, or any web application. Amazon API Gateway handles all of the tasks involved in accepting and processing up to hundreds of thousands of concurrent API calls, including traffic management, authorization and access control, monitoring, and API version management. Amazon API Gateway has no minimum fees or startup costs. For HTTP APIs and REST APIs, you pay only for the API calls you receive and the amount of data transferred out. For WebSocket APIs, you pay only for messages sent and received and for the time a user/device is connected to the WebSocket API.  

[Show less](https://aws.amazon.com/api-gateway/faqs//#)

[Q: Why use Amazon API Gateway? »](https://aws.amazon.com/api-gateway/faqs//#)

**Q: Why use Amazon API Gateway?**

Amazon API Gateway <mark style="background: #BBFABBA6;">provides developers with a simple, flexible, fully managed, pay-as-you-go service that handles all aspects of creating and operating robust APIs for application back ends</mark>. With API Gateway, you can launch new services faster and with reduced investment so you can focus on building your core business services. API Gateway was built to help you with several aspects of creating and managing APIs:

1. **Metering**. API Gateway helps you define plans that meter and restrict third-party developer access to your APIs. You can define a set of plans, configure throttling, and quota limits on a per API key basis. API Gateway automatically meters traffic to your APIs and lets you extract utilization data for each API key.

2. **Security**. A<mark style="background: #FFF3A3A6;">PI Gateway provides you with multiple tools to authorize access to your APIs and control service operation access</mark>. <mark style="background: #BBFABBA6;">API Gateway allows you to leverage AWS administration and security tools, such as AWS Identity and Access Management (IAM) and Amazon Cognito, to authorize access to your APIs</mark>.  
   **API Gateway** <mark style="background: #ADCCFFA6;">can verify signed API calls on your behalf using the same methodology AWS uses for its own APIs</mark>. <mark style="background: #FFB86CA6;">Using custom authorizers written as AWS Lambda functions</mark>, <mark style="background: #BBFABBA6;">API Gateway can also help you verify incoming bearer tokens, removing authorization concerns from your backend code.</mark>

3. **Resiliency**. <mark style="background: #BBFABBA6;">API Gateway helps you manage traffic with throttling so that backend operations can withstand traffic spikes</mark>.  
<mark style="background: #FFB86CA6;">API Gateway also helps you improve the performance of your APIs and the latency your end users experience by caching the output of API calls to avoid calling your backend every time.</mark>

4. **Operations Monitoring**. After an API is published and in use, API Gateway provides you with a metrics dashboard to monitor calls to your services. The <mark style="background: #FFF3A3A6;">API Gateway dashboard, through integration with Amazon CloudWatch, provides you with backend performance metrics covering API calls, latency data and error rates.</mark> <mark style="background: #CACFD9A6;">You can enable detailed metrics for each method in your APIs and also receive error, access or debug logs in CloudWatch Logs.</mark>

5. **Lifecycle Management**. A<mark style="background: #ADCCFFA6;">fter an API has been published, you often need to build and test new versions that enhance or add new functionality</mark>.  
   _API Gateway_ l<mark style="background: #BBFABBA6;">ets you operate multiple API versions and multiple stages for each version simultaneously so that existing applications can continue to call previous versions after new API versions are published</mark>.

6. **Designed for Developers**. API Gateway <mark style="background: #ADCCFFA6;">allows you to quickly create APIs and assign static content for their responses</mark> to reduce cross-team development effort and time-to-market for your applications. <mark style="background: #CACFD9A6;">Teams who depend on your APIs can begin development while you build your backend processes.</mark>

7. **Real-Time Two-Way Communication**. Build real-time two-way communication applications such as chat apps, streaming dashboards, and notifications without having to run or manage any servers. API Gateway maintains a persistent connection between connected users and enables message transfer between them.  

**Q: What API types are supported by Amazon API Gateway?  
**

Amazon API Gateway offers two options to create RESTful APIs, HTTP APIs and REST APIs, as well as an option to create WebSocket APIs.  

**HTTP API**: <mark style="background: #FF5582A6;">HTTP APIs</mark> are <mark style="background: #BBFABBA6;">optimized for building APIs that proxy to AWS Lambda functions or HTTP backends</mark>, <mark style="background: #ADCCFFA6;">making them ideal for serverless workloads</mark>. They do not currently offer API management functionality.

**REST API**: <mark style="background: #FF5582A6;">REST APIs</mark> <mark style="background: #BBFABBA6;">offer API proxy functionality and API management features in a single solution</mark>. REST APIs offer API management features such as usage plans, API keys, publishing, and monetizing APIs.

**WebSocket API:** <mark style="background: #FF5582A6;">WebSocket APIs</mark> <mark style="background: #BBFABBA6;">maintain a persistent connection between connected clients to enable real-time message communication</mark>. With WebSocket APIs in API Gateway, you can define backend integrations with AWS Lambda functions, Amazon Kinesis, or any HTTP endpoint to be invoked when messages are received from the connected clients.  


**Q: How do I get started with HTTP APIs in API Gateway?**

To get started with HTTP APIs, you can use the Amazon API Gateway console, the AWS CLI, AWS SDKs, or AWS CloudFormation. To learn more about getting started with HTTP APIs, visit our [documentation](https://docs.aws.amazon.com/apigateway/latest/developerguide/welcome.html).  

**Q. How do I get started with REST APIs in API Gateway?  
**

To get started with REST APIs, you can use the Amazon API Gateway console, the AWS CLI, or AWS SDKs. To learn more about getting started with REST APIs, visit our [documentation](https://docs.aws.amazon.com/apigateway/latest/developerguide/apigateway-rest-api.html).  

**Q. When creating RESTful APIs, when should I use HTTP APIs and when should I use REST APIs?  
**

You can build RESTful APIs using both HTTP APIs and REST APIs in Amazon API Gateway.  

HTTP APIs are optimized for building APIs that proxy to AWS Lambda functions or HTTP backends, making them ideal for serverless workloads. HTTP APIs are a cheaper and faster alternative to REST APIs, but they do not currently support API management functionality. REST APIs are intended for APIs that require API proxy functionality and API management features in a single solution.  

HTTP APIs are ideal for:

1. Building proxy APIs for AWS Lambda or any HTTP endpoint
2. Building modern APIs that are equipped with OIDC and OAuth 2 authorization 
3. Workloads that are likely to grow very large
4. APIs for latency sensitive workloads

REST APIs are ideal for:

1. Customers looking to pay a single price point for an all-inclusive set of features needed to build, manage, and publish their APIs. 


**Q. Which features come standard with HTTP APIs from API Gateway?**

HTTP APIs come standard with CORS support, OIDC and OAuth2 support for authentication and authorization, and automatic deployments on stages.  

**Q. Can I import an OpenAPI definition to create a HTTP API?**

Yes, you can import an API definition using OpenAPI 3. It will result in the creation of routes, integrations, and API models. For more information on importing OpenAPI definitions, see our [documentation](https://docs.aws.amazon.com/apigateway/latest/developerguide/http-api-import.html).  


**Q. How can I migrate from my current REST API to a HTTP API?**

To migrate from your current REST API to a HTTP API in Amazon API Gateway, do the following:

1. Check that all the features you need are available in HTTP. To see the complete feature list, visit our [documentation](https://docs.aws.amazon.com/apigateway/latest/developerguide/http-api-vs-rest.html). 
2. Go to your REST API and export the OpenAPI definition from your REST API
3. Go to your HTTP API and import the OpenAPI definition from the previous step
4. Test the API functions as expected
5. Update your clients with the new URL

While your API might work, you may notice some missing features. To identify any missing features, review the **Info**, **Warning**, and **Error** fields from the Import operation. For more information about migrating REST APIs to HTTP APIs, see our [documentation](https://docs.aws.amazon.com/apigateway/latest/developerguide/http-api-import.html).

[Show less](https://aws.amazon.com/api-gateway/faqs//#)

[Q: How do I know if my current REST API will work as a HTTP API? »](https://aws.amazon.com/api-gateway/faqs//#)

**Q. How do I know if my current REST API will work as a HTTP API?**

First, go to your REST and export the OpenAPI definition from your REST API. Then, go to your HTTP API and import the OpenAPI definition from the previous step. While your API might work, you may notice some missing features. To identify any missing features, review the **Info**, **Warning**, and **Error** fields from the Import operation. The AWS CLI will return information about your API within your info and warning fields. For more, read our [documentation](https://docs.aws.amazon.com/apigateway/latest/developerguide/http-api-import.html).  

[Show less](https://aws.amazon.com/api-gateway/faqs//#)

[Q: How do I get started with WebSocket APIs in Amazon API Gateway? »](https://aws.amazon.com/api-gateway/faqs//#)

**Q: How do I get started with WebSocket APIs in Amazon API Gateway?  
**

To get started, you can create a WebSocket API using the AWS Management Console, AWS CLI, or AWS SDKs. You can then set WebSocket routing to indicate the backend services such as AWS Lambda, Amazon Kinesis, or your HTTP endpoint to be invoked based on the message content. Refer to the [documentation](https://docs.aws.amazon.com/apigateway/latest/developerguide/apigateway-websocket-api.html) for getting started with WebSocket APIs in API Gateway.  

[Show less](https://aws.amazon.com/api-gateway/faqs//#)

[Q: Can I create HTTPS endpoints? »](https://aws.amazon.com/api-gateway/faqs//#)

**Q: Can I create HTTPS endpoints?  
**

Yes, all of the APIs created with Amazon API Gateway expose HTTPS endpoints only. Amazon API Gateway does not support unencrypted (HTTP) endpoints. By default, Amazon API Gateway assigns an internal domain to the API that automatically uses the Amazon API Gateway certificate. When configuring your APIs to run under a custom domain name, you can provide your own certificate for the domain.  

[Show less](https://aws.amazon.com/api-gateway/faqs//#)

[Q: What data types can I use with Amazon API Gateway? »](https://aws.amazon.com/api-gateway/faqs//#)

**Q: What data types can I use with Amazon API Gateway ?  
**

APIs built on Amazon API Gateway can accept any payloads sent over HTTPS for HTTP APIs, REST APIs, and WebSocket APIs. Typical data formats include JSON, XML, query string parameters, and request headers. You can declare any content type for your APIs responses, and then use the transform templates to change the back-end response into your desired format.  

[Show less](https://aws.amazon.com/api-gateway/faqs//#)

[Q: With what backends can Amazon API Gateway communicate? »](https://aws.amazon.com/api-gateway/faqs//#)

**Q: With what backends can Amazon API Gateway communicate?**

Amazon API Gateway can execute AWS Lambda functions in your account, start AWS Step Functions state machines, or call HTTP endpoints hosted on AWS Elastic Beanstalk, Amazon EC2, and also non-AWS hosted HTTP based operations that are accessible via the public Internet.API Gateway also allows you to specify a mapping template to generate static content to be returned, helping you mock your APIs before the backend is ready. You can also integrate API Gateway with other AWS services directly – for example, you could expose an API method in API Gateway that sends data directly to Amazon Kinesis.  

[Show less](https://aws.amazon.com/api-gateway/faqs//#)

[Q: For which client platforms can Amazon API Gateway generate SDKs? »](https://aws.amazon.com/api-gateway/faqs//#)

**Q: For which client platforms can Amazon API Gateway generate SDKs?**

API Gateway generates custom SDKs for mobile app development with Android and iOS (Swift and Objective-C), and for web app development with JavaScript. API Gateway also supports generating SDKs for Ruby and Java. Once an API and its models are defined in API Gateway, you can use the AWS console or the API Gateway APIs to generate and download a client SDK. Client SDKs are only generated for REST APIs in Amazon API Gateway.

[Show less](https://aws.amazon.com/api-gateway/faqs//#)

[Q: In which AWS regions is Amazon API Gateway available? »](https://aws.amazon.com/api-gateway/faqs//#)

**Q: In which AWS regions is Amazon API Gateway available?**

To see where HTTP APIs, REST APIs, WebSocket APIs are available, view the AWS region table [here](https://aws.amazon.com/about-aws/global-infrastructure/regional-product-services/).

[Show less](https://aws.amazon.com/api-gateway/faqs//#)

[Q: What can I manage through the Amazon API Gateway console? »](https://aws.amazon.com/api-gateway/faqs//#)

**Q: What can I manage through the Amazon API Gateway console?**

Through the Amazon API Gateway console, you can define the REST API and its associated resources and methods, manage the API lifecycle, generate client SDKs and view API metrics. You can also use the API Gateway console to define your APIs’ usage plans, manage developers’ API keys, and configure throttling and quota limits. All of the same actions are available through the API Gateway APIs.  

[Show less](https://aws.amazon.com/api-gateway/faqs//#)

[Q: What is a resource? »](https://aws.amazon.com/api-gateway/faqs//#)

**Q: What is a resource?**

A resource is a typed object that is part of your API’s domain. Each resource may have associated a data model, relationships to other resources, and can respond to different methods.You can also define resources as variables to intercept requests to multiple child resources.  

[Show less](https://aws.amazon.com/api-gateway/faqs//#)

[Q: What is a method? »](https://aws.amazon.com/api-gateway/faqs//#)

**Q: What is a method?**

Each resource within a REST API can support one or more of the standard HTTP methods. You define which verbs should be supported for each resource (GET, POST, PUT, PATCH, DELETE, HEAD, OPTIONS) and their implementation. For example, a GET to the cars resource should return a list of cars. To connect all methods within a resource to a single backend endpoint, API Gateway also supports a special “ANY” method.  

[Show less](https://aws.amazon.com/api-gateway/faqs//#)

[Q: What is a usage plan? »](https://aws.amazon.com/api-gateway/faqs//#)

**Q: What is a usage plan?**  
  
Usage plans help you declare plans for third-party developers that restrict access only to certain APIs, define throttling and request quota limits, and associate them with API keys. You can also extract utilization data on a per-API key basis to analyze API usage and generate billing documents. For example, you can create a basic, professional, and enterprise plans – you can configure the basic usage plan to only allow 1,000 requests per day and a maximum of 5 requests per second (RPS).  

[Show less](https://aws.amazon.com/api-gateway/faqs//#)

[Q: What is the Amazon API Gateway API lifecycle? »](https://aws.amazon.com/api-gateway/faqs//#)

**Q: What is the Amazon API Gateway API lifecycle?**

With Amazon API Gateway, each REST API can have multiple stages. Stages are meant to help with the development lifecycle of an API -- for example, after you’ve built your APIs and you deploy them to a development stage, or when you are ready for production, you can deploy them to a production stage.  

[Show less](https://aws.amazon.com/api-gateway/faqs//#)

[Q: What is a stage? »](https://aws.amazon.com/api-gateway/faqs//#)

**Q: What is a stage?**  

In Amazon API Gateway, stages are similar to tags. They define the path through which the deployment is accessible. For example, you can define a development stage and deploy your cars API to it. The resource will be accessible at https://www.myapi.com/dev/cars. You can also set up custom domain names to point directly to a stage, so that you don’t have to use the additional path parameter. For example, if you pointed myapi.com directly to the development stage, you could access your cars resource at https://www.myapi.com/cars. Stages can be configured using variables that can be accessed from your API configuration or mapping templates.  


**Q: What are stage variables?**

Stage variables let you define key/value pairs of configuration values associated with a stage. These values, similarly to environment variables, can be used in your API configuration. For example, you could define the HTTP endpoint for your method integration as a stage variable, and use the variable in your API configuration instead of hardcoding the endpoint – this allows you to use a different endpoint for each stage (e.g. dev, beta, prod) with the same API configuration. Stage variables are also accessible in the mapping templates and can be used to pass configuration parameters to your Lambda or HTTP backend.  

[Show less](https://aws.amazon.com/api-gateway/faqs//#)

[Q: What is a Resource Policy? »](https://aws.amazon.com/api-gateway/faqs//#)

**Q: What is a Resource Policy?**

A Resource Policy is a JSON policy document that you attach to an API to control whether a specified principal (typically an IAM user or role) can invoke the API. You can use a Resource Policy to enable users from a different AWS account to securely access your API or to allow the API to be invoked only from specified source IP address ranges or CIDR blocks. Resource Policies can be used with REST APIs in Amazon API Gateway.  

[Show less](https://aws.amazon.com/api-gateway/faqs//#)

[Q: What if I mistakenly deployed to a stage? »](https://aws.amazon.com/api-gateway/faqs//#)

**Q: What if I mistakenly deployed to a stage?**

Amazon API Gateway saves the history of your deployments. At any point, using the Amazon API Gateway APIs or the console, you can roll back a stage to a previous deployment.  

[Show less](https://aws.amazon.com/api-gateway/faqs//#)

[Q: Can I use my Swagger API definitions? »](https://aws.amazon.com/api-gateway/faqs//#)

**Q: Can I use my Swagger API definitions?**

Yes. You can use our open source [Swagger importer tool](https://github.com/awslabs/aws-apigateway-importer) to import your Swagger API definitions into Amazon API Gateway. With the Swagger importer tool you can create and deploy new APIs as well as update existing ones.  

**Q: How do I monetize my APIs on API Gateway?**

You can monetize your APIs on API Gateway by publishing them as products in AWS Marketplace. You will first need to [register as a seller](https://signin.aws.amazon.com/signin?redirect_uri=https%3A%2F%2Faws.amazon.com%2Fmarketplace%2Fmanagement%2Fregister%2F%3Fstate%3DhashArgs%2523%26isauthcode%3Dtrue&client_id=arn%3Aaws%3Aiam%3A%3A015428540659%3Auser%2Faws-mp-seller-management-portal&forceMobileApp=0) in AWS Marketplace, and submit your usage plans on API Gateway as products. [Read here](https://aws.amazon.com/blogs/compute/monetize-your-apis-in-aws-marketplace-using-api-gateway/) to learn more about API Monetization.  


**Q: How do I document my API on Amazon API Gateway?**

API Gateway offers the ability to create, update, and delete documentation associated with each portion of your API, such as methods and resources. You can access documentation-related APIs through the AWS SDKs, CLI, via RESTful calls, or by editing the documentation strings directly in the API Gateway console. Documentation can also be imported as a Swagger file, either as part of the API or separately, allowing you to add or update the documentation without disturbing the API definition. API Gateway conforms to the [Open API specification](https://swagger.io/specification/) for documentation imported from, or exported to, Swagger files. Documentation is supported for REST APIs in API Gateway.  

**Q: How can I avoid creating redundant copies of error messages and other documentation that recurs frequently in my API?**

In addition to offering standards-conformant API documentation support, API Gateway additionally supports documentation inheritance, making it simple to define a documentation string once and then use it in multiple places. Inheritance simplifies the process of defining API documentation, and can be converted to the standard representation when exporting the API as a Swagger file.  

**Q: Can I restrict access to private APIs to a specific Amazon VPC or VPC endpoint?**

Yes, you can apply a Resource Policy to an API to restrict access to a specific Amazon VPC or VPC endpoint. You can also give an Amazon VPC or VPC endpoint from a different account access to the Private API using a Resource Policy.

## Security and Authorization

[Q: How do I authorize access to my APIs? »](https://aws.amazon.com/api-gateway/faqs//#)

**Q: How do I authorize access to my APIs?**

With Amazon API Gateway, you can optionally set your API methods to require authorization. When setting up a method to require authorization you can leverage AWS Signature Version 4 or Lambda authorizers to support your own bearer token auth strategy.  

[Show less](https://aws.amazon.com/api-gateway/faqs//#)

[Q: How does AWS Signature Version 4 work? »](https://aws.amazon.com/api-gateway/faqs//#)

**Q: How does AWS Signature Version 4 work?**

You can use AWS credentials - access and secret keys - to sign requests to your service and authorize access like other AWS services. The signing of an Amazon API Gateway API request is managed by the custom API Gateway SDK generated for your service. You can retrieve temporary credentials associated with a role in your AWS account using Amazon Cognito.  

[Show less](https://aws.amazon.com/api-gateway/faqs//#)

[Q: What is a Lambda authorizer? »](https://aws.amazon.com/api-gateway/faqs//#)

**Q: What is a Lambda authorizer?**

Lambda authorizers are AWS Lambda functions. With custom request authorizers, you will be able to authorize access to APIs using a bearer token auth strategy such as OAuth. When an API is called, API Gateway checks if a Lambda authorizer is configured, API Gateway then calls the Lambda function with the incoming authorization token. You can use Lambda to implement various authorization strategies (e.g. JWT verification, OAuth provider callout) that return IAM policies which are used to authorize the request. If the policy returned by the authorizer is valid, API Gateway will cache the policy associated with the incoming token for up to 1 hour.  

[Show less](https://aws.amazon.com/api-gateway/faqs//#)

[Q: Can Amazon API Gateway generate API keys for distribution to third-party developers? »](https://aws.amazon.com/api-gateway/faqs//#)

**Q: Can Amazon API Gateway generate API keys for distribution to third-party developers?**

Yes. API Gateway can generate API keys and associate them with an usage plan. Calls received from each API key are monitored and included in the Amazon CloudWatch Logs you can enable for each stage. However, we do not recommend you use API keys for authorization. You should use API keys to monitor usage by third-party developers and leverage a stronger mechanism for authorization, such as signed API calls or OAuth.  

[Show less](https://aws.amazon.com/api-gateway/faqs//#)

[Q: How can I address or prevent API threats or abuse? »](https://aws.amazon.com/api-gateway/faqs//#)

**Q: How can I address or prevent API threats or abuse?**

API Gateway supports throttling settings for each method or route in your APIs. You can set a standard rate limit and a burst rate limit per second for each method in your REST APIs and each route in WebSocket APIs. Further, API Gateway automatically protects your backend systems from distributed denial-of-service (DDoS) attacks, whether attacked with counterfeit requests (Layer 7) or SYN floods (Layer 3).  

[Show less](https://aws.amazon.com/api-gateway/faqs//#)

[Q: Can I verify that it is API Gateway calling my backend? »](https://aws.amazon.com/api-gateway/faqs//#)

**Q: Can I verify that it is API Gateway calling my backend?**

Yes. Amazon API Gateway can generate a client-side SSL certificate and make the public key of that certificate available to you. Calls to your backend can be made with the generated certificate, and you can verify calls originating from Amazon API Gateway using the public key of the certificate.  

[Show less](https://aws.amazon.com/api-gateway/faqs//#)

[Q: Can I use AWS CloudTrail with Amazon API Gateway? »](https://aws.amazon.com/api-gateway/faqs//#)

**Q: Can I use AWS CloudTrail with Amazon API Gateway?**

Yes. Amazon API Gateway is integrated with [AWS CloudTrail](https://aws.amazon.com/cloudtrail/) to give you a full auditable history of the changes to your REST APIs. All API calls made to the Amazon API Gateway APIs to create, modify, delete, or deploy REST APIs are logged to CloudTrail in your AWS account.  

[Show less](https://aws.amazon.com/api-gateway/faqs//#)

[Q: How does Amazon API Gateway work with an Amazon Virtual Private Cloud (Amazon VPC)? »](https://aws.amazon.com/api-gateway/faqs//#)

**Q: How does Amazon API Gateway work with an Amazon Virtual Private Cloud (Amazon VPC)?** 

In Amazon API Gateway, you can proxy requests to backend HTTP/HTTPS resources running in your Amazon VPC by setting up [Private Integrations](https://docs.aws.amazon.com/apigateway/latest/developerguide/set-up-private-integration.html) using VPC Links. Client-side SSL certificates in Amazon API Gateway can be used to verify that requests to your backend systems were sent by API Gateway using the public key of the certificate. You can also create Private APIs in Amazon API Gateway which can only be accessible by resources within your Amazon VPC through Amazon VPC Endpoints.  

[Show less](https://aws.amazon.com/api-gateway/faqs//#)

[Q: Can I restrict access to private APIs to a specific Amazon VPC or VPC endpoint? »](https://aws.amazon.com/api-gateway/faqs//#)

**Q: Can I restrict access to private APIs to a specific Amazon VPC or VPC endpoint?**

Yes, you can apply a Resource Policy to an API to restrict access to a specific Amazon VPC or VPC endpoint. You can also give an Amazon VPC or VPC endpoint from a different account access to the Private API using a Resource Policy.  

[Show less](https://aws.amazon.com/api-gateway/faqs//#)

[Q: Can I configure my REST APIs in API Gateway to use TLS 1.1 or higher? »](https://aws.amazon.com/api-gateway/faqs//#)

**Q: Can I configure my REST APIs in API Gateway to use TLS 1.1 or higher ?**

If you’re using REST APIs, you can set up a CloudFront distribution with custom SSL certificate in your account and use it with [Regional APIs](https://docs.aws.amazon.com/apigateway/latest/developerguide/create-regional-api.html) in API Gateway. You can then configure the [Security Policy](https://aws.amazon.com/about-aws/whats-new/2017/09/amazon-cloudfront-now-lets-you-select-a-security-policy-with-minimum-tls-v1_1-1_2-and-security-ciphers-for-viewer-connections/) for the CloudFront distribution with TLS 1.1 or higher based on your security and compliance requirements.  

[Show less](https://aws.amazon.com/api-gateway/faqs//#)

## Management, Metrics, and Logging

[Q: How can I monitor my Amazon API Gateway APIs? »](https://aws.amazon.com/api-gateway/faqs//#)

**Q: How can I monitor my Amazon API Gateway APIs?**

Amazon API Gateway logs API calls, latency, and error rates to Amazon CloudWatch in your AWS account. The metrics are also available through the Amazon API Gateway console in a REST API dashboard. API Gateway also meters utilization by third-party developers, the data is available in the API Gateway console and through the APIs.  

[Show less](https://aws.amazon.com/api-gateway/faqs//#)

[Q: Can I set up alarms on the Amazon API Gateway metrics? »](https://aws.amazon.com/api-gateway/faqs//#)

**Q: Can I set up alarms on the Amazon API Gateway metrics?**

Yes, Amazon API Gateway sends logging information and metrics to Amazon CloudWatch. You can utilize the Amazon CloudWatch console to set up custom alarms.  

[Show less](https://aws.amazon.com/api-gateway/faqs//#)

[Q: How can I set up metrics for Amazon API Gateway? »](https://aws.amazon.com/api-gateway/faqs//#)

**Q: How can I set up metrics for Amazon API Gateway?**

By default, Amazon API Gateway monitors traffic at a REST API level. Optionally, you can enable detailed metrics for each method in your REST API from the deployment configuration APIs or console screen. Detailed metrics are also logged to Amazon CloudWatch and will be charged at the CloudWatch rates.  

[Show less](https://aws.amazon.com/api-gateway/faqs//#)

[Q: Can I determine which version of the API my customers are using? »](https://aws.amazon.com/api-gateway/faqs//#)

**Q: Can I determine which version of the API my customers are using?**

Yes. Metric details are specified by REST API and stage. Additionally, you can enable metrics for each method in your REST API.  

[Show less](https://aws.amazon.com/api-gateway/faqs//#)

[Q: Does Amazon API Gateway provide logging support? »](https://aws.amazon.com/api-gateway/faqs//#)

**Q: Does Amazon API Gateway provide logging support?**

Yes. Amazon API Gateway integrates with Amazon CloudWatch Logs. You can optionally enable logging for each stage in your API. For each method in your REST APIs, you can set the verbosity of the logging, and if full request and response data should be logged.  

[Show less](https://aws.amazon.com/api-gateway/faqs//#)

[Q: How quickly are logs available? »](https://aws.amazon.com/api-gateway/faqs//#)

**Q: How quickly are logs available?**

Logs, alarms, error rates and other metrics are stored in Amazon CloudWatch and are available near real time.  

[Show less](https://aws.amazon.com/api-gateway/faqs//#)

## Throttling and Caching

[Q: How can I protect my backend systems and applications from traffic spikes? »](https://aws.amazon.com/api-gateway/faqs//#)

**Q: How can I protect my backend systems and applications from traffic spikes?**

Amazon API Gateway provides throttling at multiple levels including global and by service call. Throttling limits can be set for standard rates and bursts. For example, API owners can set a rate limit of 1,000 requests per second for a specific method in their REST APIs, and also configure Amazon API Gateway to handle a burst of 2,000 requests per second for a few seconds. Amazon API Gateway tracks the number of requests per second. Any requests over the limit will receive a 429 HTTP response. The client SDKs (except Javascript) generated by Amazon API Gateway retry calls automatically when met with this response.  

[Show less](https://aws.amazon.com/api-gateway/faqs//#)

[Q: Can I throttle individual developers calling my APIs? »](https://aws.amazon.com/api-gateway/faqs//#)

**Q: Can I throttle individual developers calling my APIs?**

Yes. With usage plans you can set throttling limits for individual API keys.  

[Show less](https://aws.amazon.com/api-gateway/faqs//#)

[Q: How does throttling help me? »](https://aws.amazon.com/api-gateway/faqs//#)

**Q: How does throttling help me?**

Throttling ensures that API traffic is controlled to help your backend services maintain performance and availability.  

[Show less](https://aws.amazon.com/api-gateway/faqs//#)

[Q: At which levels can Amazon API Gateway throttle inbound API traffic? »](https://aws.amazon.com/api-gateway/faqs//#)

**Q: At which levels can Amazon API Gateway throttle inbound API traffic?**

Throttling rate limits can be set at the method level. You can edit the throttling limits in your method settings through the Amazon API Gateway APIs or in the Amazon API Gateway console.  

[Show less](https://aws.amazon.com/api-gateway/faqs//#)

[Q: How are throttling rules applied? »](https://aws.amazon.com/api-gateway/faqs//#)

**Q: How are throttling rules applied?**

API Gateway throttling related settings are applied in the following order: 1) per-client per-method throttling limits that you set for an API stage in a usage plan, 2) per-client throttling limits that you set in a usage plan, 3) default per-method limits and individual per-method limits that you set in API stage settings, 4) account-level throttling per region.  

[Show less](https://aws.amazon.com/api-gateway/faqs//#)

[Q: Does Amazon API Gateway provide API result caching? »](https://aws.amazon.com/api-gateway/faqs//#)

**Q: Does Amazon API Gateway provide API result caching?**

Yes. You can add caching to API calls by provisioning an API Gateway cache and specifying its size in gigabytes. The cache is provisioned for a specific stage of your APIs. This improves performance and reduces the traffic sent to your back end. Cache settings allow you to control the way the cache key is built and the time-to-live (TTL) of the data stored for each method. API Gateway also exposes management APIs that help you invalidate the cache for each stage. Caching is available for REST APIs in API Gateway.  

[Show less](https://aws.amazon.com/api-gateway/faqs//#)

[Q: What happens if a large number of end users try to invoke my API simultaneously? »](https://aws.amazon.com/api-gateway/faqs//#)

**Q: What happens if a large number of end users try to invoke my API simultaneously?**

If caching is not enabled and throttling limits have not been applied, then all requests will pass through to your backend service until the account level throttling limits are reached. If throttling limits are in place, then Amazon API Gateway will shed the necessary amount of requests and send only the defined limit to your back-end service. If a cache is configured, then Amazon API Gateway will return a cached response for duplicate requests for a customizable time, but only if under configured throttling limits. This balance between the backend and client ensures optimal performance of the APIs for the applications that it supports. Requests that are throttled will be automatically retried by the client-side SDKs generated by Amazon API Gateway. By default, Amazon API Gateway does not set any cache on your API methods.  

[Show less](https://aws.amazon.com/api-gateway/faqs//#)

[Q: How do APIs scale? »](https://aws.amazon.com/api-gateway/faqs//#)

**Q: How do APIs scale?**

Amazon API Gateway acts as a proxy to the backend operations that you have configured. Amazon API Gateway will automatically scale to handle the amount of traffic your API receives. Amazon API Gateway does not arbitrarily limit or throttle invocations to your backend operations and all requests that are not intercepted by throttling and caching settings in the Amazon API Gateway console are sent to your backend operations.  

[Show less](https://aws.amazon.com/api-gateway/faqs//#)

[back to top >>](https://aws.amazon.com/api-gateway/faqs//#)

## Billing

[Q: How am I charged for using Amazon API Gateway? »](https://aws.amazon.com/api-gateway/faqs//#)

**Q: How am I charged for using Amazon API Gateway?**

Amazon API Gateway bills per million API calls, plus the cost of data transfer out, in gigabytes. If you choose to provision a cache for your API, hourly rates apply. For WebSocket APIs, API Gateway bills based on messages sent and received and the number of minutes a client is connected to the API. Please see the API Gateway [pricing page](https://aws.amazon.com/api-gateway/pricing/) for details on API calls, data transfer, and caching costs per region.  

[Show less](https://aws.amazon.com/api-gateway/faqs//#)

[Q: Who pays for Amazon API Gateway API calls generated by third-party developers? »](https://aws.amazon.com/api-gateway/faqs//#)

**Q: Who pays for Amazon API Gateway API calls generated by third-party developers?**

The API owner is charged for the calls to their APIs on API Gateway.  

[Show less](https://aws.amazon.com/api-gateway/faqs//#)

[Q: If an API response is served by cached data, is it still considered an API call for billing purposes? »](https://aws.amazon.com/api-gateway/faqs//#)

**Q: If an API response is served by cached data, is it still considered an API call for billing purposes?**

Yes. API calls are counted equally for billing purposes whether the response is handled by your backend operations or the Amazon API Gateway caching operation.  

[Show less](https://aws.amazon.com/api-gateway/faqs//#)

[back to top >>](https://aws.amazon.com/api-gateway/faqs//#)

## WebSocket APIs

[Q: What is WebSocket routing in Amazon API Gateway? »](https://aws.amazon.com/api-gateway/faqs//#)

**Q: What is WebSocket routing in Amazon API Gateway?**

WebSocket routing in Amazon API Gateway is used to correctly route the messages to a specific integration. You specify a routing key and integration backend to invoke when defining your WebSocket API. The routing key is an attribute in the message body. A default integration can also be set for non-matching routing keys. Refer to [documentation](https://docs.aws.amazon.com/apigateway/latest/developerguide/apigateway-websocket-api-routes.htm) to learn more about routing.  

[Show less](https://aws.amazon.com/api-gateway/faqs//#)

[Q: How can I send messages to connected clients from the backend service? »](https://aws.amazon.com/api-gateway/faqs//#)

**Q:  How can I send messages to connected clients from the backend service?**

When a new client is connected to the WebSocket API, a unique URL, called the callback URL, is created for that client. You can use this callback URL to send messages to the client from the backend service.  

[Show less](https://aws.amazon.com/api-gateway/faqs//#)

[Q: How can I authorize access to my WebSocket API in Amazon API Gateway? »](https://aws.amazon.com/api-gateway/faqs//#)

**Q:  How can I authorize access to my WebSocket API in Amazon API Gateway?**

With Amazon API Gateway, you can either use IAM roles and policies or AWS Lambda Authorizers to authorize access to your WebSocket APIs.  

[Show less](https://aws.amazon.com/api-gateway/faqs//#)

[Q: How does my backend service know when a client is connected or disconnected from the WebSocket connection in Amazon API Gateway? »](https://aws.amazon.com/api-gateway/faqs//#)

**Q: How does my backend service know when a client is connected or disconnected from the WebSocket connection in Amazon API Gateway?**

When a client is connected or disconnected, a message will be sent from the Amazon API Gateway service to your backend AWS Lambda function or your HTTP endpoint using the $connect and $disconnect routes. You can take appropriate actions like adding or removing the client for the list of connected users.  

[Show less](https://aws.amazon.com/api-gateway/faqs//#)

[Q: How can my backend service identify if the client is still connected to the WebSocket connection? »](https://aws.amazon.com/api-gateway/faqs//#)

**Q: How can my backend service identify if the client is still connected to the WebSocket connection??**

You can use the callback URL GET method on the connection to identify if the client is connected to the WebSocket connection. Refer to documentation about using a callback URL.  

[Show less](https://aws.amazon.com/api-gateway/faqs//#)

[Q: Can I disconnect a client from my backend service? »](https://aws.amazon.com/api-gateway/faqs//#)

**Q: Can I disconnect a client from my backend service?**

Yes, you can disconnect the connected client from your backend service using the callback URL.  

[Show less](https://aws.amazon.com/api-gateway/faqs//#)

[Q: What is the maximum message size supported for WebSocket APIs? »](https://aws.amazon.com/api-gateway/faqs//#)

**Q: What is the maximum message size supported for WebSocket APIs?**

The maximum supported message size is 128 KB. Refer to the [documentation](https://docs.aws.amazon.com/apigateway/latest/developerguide/limits.html) for other limits around WebSocket APIs.  

[Show less](https://aws.amazon.com/api-gateway/faqs//#)

[Q: How am I charged for using WebSocket APIs on Amazon API Gateway? »](https://aws.amazon.com/api-gateway/faqs//#)

**Q: How am I charged for using WebSocket APIs on Amazon API Gateway?**

You will be charged based on 2 metrics: Connection minutes and messages.

**Connection minutes:** Total number of minutes the clients or devices are connected to the WebSocket connection (rounded to a minute).

**Messages:** Total number of messages sent to and received from connected clients. Messages are charged in increments of 32KB. Refer to the [pricing page](https://aws.amazon.com/api-gateway/pricing/) for details about WebSocket API pricing and examples.  

[Show less](https://aws.amazon.com/api-gateway/faqs//#)

[Q: If messages on the WebSocket connection fail authentication or authorization, do they still count toward my API usage bill? »](https://aws.amazon.com/api-gateway/faqs//#)

**Q: If messages on the WebSocket connection fail authentication or authorization, do they still count toward my API usage bill?**

No, if messages on the WebSocket connection fail authentication or authorization, they do not count toward your API usage bill.

[Show less](https://aws.amazon.com/api-gateway/faqs//#)