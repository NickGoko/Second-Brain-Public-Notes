---
tags:
  - cloud/aws
---


https://aws.amazon.com/app-mesh/

# FAQ
**Q: What is AWS App Mesh?**

A: AWS App Mesh makes it easy to monitor, control, and debug the communications between services. App Mesh uses Envoy, an open source service mesh proxy which is deployed alongside your microservice containers. App Mesh is integrated with AWS services for monitoring and tracing, and it works with many popular third-party tools. App Mesh can be used with microservice containers managed by Amazon ECS, Amazon EKS, AWS Fargate, Kubernetes running on AWS, and services running on Amazon EC2.

**Q: Why should I use App Mesh?**

A: App Mesh makes it easier to get visibility, security, and control over the communications between your services without writing new code or running additional AWS infrastructure. Using App Mesh, you can standardize how services communicate, implement rules for communications between services, and capture metrics, logs, and traces directly into AWS services and third-party tools of your choice.

**Q: How does App Mesh work?**

A: App Mesh sets up and manages a service mesh for your services. To do this, you run the open source Envoy proxy alongside each service, and App Mesh configures the proxy to handle all communications into and out of each container. App Mesh collects metrics, such as error rates, and connections per second, which can be exported to Amazon CloudWatch using a statsd collector. Using App Mesh APIs, you can route traffic based on path or weights to specific service versions.

**Q: What is a service mesh?**

A: A service mesh is a new software layer that handles all of the communications between services. It provides new features to connect and manage connections between services and is independent of each service’s code, allowing it to work across network boundaries and with multiple service management systems.

## Integrations

**Q: How does App Mesh work with Amazon Elastic Container Services (ECS) and AWS Fargate?**

A: App Mesh provides new communication, observation, and management capabilities to applications managed by Amazon ECS and AWS Fargate. You add the Envoy proxy image to the task definition. App Mesh manages Envoy configuration to provide service mesh capabilities. App Mesh exports metrics, logs, and traces to the endpoints specified in the Envoy bootstrap configuration provided. App Mesh provides an API to configure traffic routes and other controls between microservices that are mesh-enabled.

**Q: How does App Mesh work with Amazon Elastic Container Service for Kubernetes (EKS)?**

A: Use the open source AWS App Mesh controller and mutating webhook admission controller. These controllers connect your Kubernetes services to App Mesh and ensure that the Envoy proxy is injected into your pods. App Mesh exports metrics, logs, and traces to the endpoints specified in the Envoy bootstrap configuration provided. App Mesh provides an API to configure traffic routes and other controls between microservices that are mesh-enabled.

**Q: How does App Mesh work with services running on Amazon EC2?**

A: Run the Envoy proxy as a container or process on your EC2 instance. Use the AWS-provided container proxy init container, or run your own script, to redirect network traffic on the instance through the proxy. App Mesh manages Envoy configuration to provide service mesh capabilities. App Mesh exports metrics, logs, and traces to the endpoints specified in the Envoy bootstrap configuration provided. App Mesh provides an API to configure traffic routes and other controls between microservices that are mesh-enabled.

**Q: Why should I use App Mesh instead of AWS Elastic Load Balancers?**

A: We recommend using AWS Elastic Load Balancing to handle all internet traffic and traffic from clients that are not within your trust boundary. For internal services that connect to other services within an AWS region, App Mesh provides flexibility, consistency, and a greater degree of control and monitoring for services communications.  

## Monitoring, Logging, and Tracing

**Q: What type of monitoring capabilities does App Mesh provide?**

A: With App Mesh, you get consistent metrics and logs for every hop between services. These logs and metrics include metadata such as service-names and request identifiers. With these, you can aggregate, filter, a see graphical dashboards of service-to-service communications using tools like Amazon CloudWatch. Common dashboards might include error rates and error codes between your service and dependent services. App Mesh automatically collects traces for each service and makes it easy to visualize a service map with details of all service API calls. These capabilities make it easier to debug and identify the root cause of communication issues between your microservices.

**Q: Can I use non-AWS tools for monitoring, logging, or tracing with App Mesh? Yes.**

A: Yes. App Mesh supports any third-party tool that works with Envoy. This includes Splunk, Prometheus, Jaeger, Flagger, and Grafana, as well as open-tracing solutions like Zipkin and LightStep.  

## Traffic Control

**Q: What type of traffic controls does App Mesh provide?**

A: App Mesh gives you a set of client-side controls for traffic routing. App Mesh provides APIs to route traffic between applications based on service names and versions. These capabilities make it easier to deploy new versions of your microservices.  

## Service-to-Service Authentication

**Q: How does App Mesh support application identity?**

Mutual TLS (mTLS) provides a way to enforce application identity at transport layer and allow or deny client connections based on the certificate they present. AWS App Mesh has support for enforcing client application identity with X.509 certificates, called mutual transport layer security, or mTLS. In order to configure mTLS, you need to set up the client to provide a certificate to the server service during request initiation, as part of the TLS session negotiation. This certificate is used by the server to identify and authenticate the client, checking the certificate is valid and was issued by a trusted certificate authority (CA), and identifying who the client is by using the Subject Alternative Name (SAN) on the certificate.

**Q: Why should I use mTLS with AWS App Mesh?**

Microservices also have particular security needs, including end-to-end traffic encryption and flexible service access control, which can be addressed with a service mesh. The AWS App Mesh mTLS implementation enables your client applications to verify the servers and provides traffic encryption, and mutual TLS offers peer authentication that is used for service-to-service authentication. It adds a layer of security over TLS that allows your services to verify the client making the connection. Breaking down a monolithic application into microservices and running them in a service mesh offers various benefits, including better visibility and smart traffic routing.