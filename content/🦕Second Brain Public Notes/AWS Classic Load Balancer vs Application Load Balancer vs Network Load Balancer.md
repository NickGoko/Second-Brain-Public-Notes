
- Elastic Load Balancing supports three types of load balancers:
    - Classic Load Balancer – CLB
    - Application Load Balancer – ALB
    - Network Load Balancer – NLB
- While there is some overlap in the features, AWS does not maintain feature parity between the different types of load balancers.

![CLB vs ALB vs NLB General](https://jayendrapatil.com/wp-content/uploads/2017/08/CLB-vs-ALB-vs-NLB-General.png)

## Usage Patterns

- [**Classic Load Balancer**](https://jayendrapatil.com/aws-elastic-load-balancing/)
    - provides basic load balancing across multiple EC2 instances and operates at both the request level and connection level.
    - is intended for applications that were built within the EC2-Classic network.
    - is ideal for simple load balancing of traffic across multiple EC2 instances.  
      ![](https://i.imgur.com/2E75uDZ.png)

- [**Application Load Balancer**](https://jayendrapatil.com/aws-elb-application-load-balancer/)
    - is ideal for microservices or container-based architectures where there is a need to route traffic to multiple services or load balance across multiple ports on the same EC2 instance.
    - operates at the request level (layer 7), routing traffic to targets – EC2 instances, containers, IP addresses, and Lambda functions based on the content of the request.
    - is ideal for advanced load balancing of HTTP and HTTPS traffic, and provides advanced request routing targeted at delivery of modern application architectures, including microservices and container-based applications.
    - simplifies and improves the security of the application, by ensuring that the latest SSL/TLS ciphers and protocols are used at all times.
    
- [**Network Load Balancer**](https://jayendrapatil.com/aws-elb-network-load-balancer/)
    - operates at the connection level (Layer 4), routing connections to targets – EC2 instances, microservices, and containers – within VPC based on IP protocol data.
    - is ideal for load balancing of both TCP and UDP traffic,
    - is capable of **handling millions of requests per second while maintaining ultra-low latencies**.
    - is **optimized to handle sudden and volatile traffic patterns** while using a **single static IP address per AZ**
    - is integrated with other popular AWS services such as Auto Scaling, ECS, CloudFormation, and AWS Certificate Manager (ACM).
- **AWS recommends using Application Load Balancer for Layer 7 and Network Load Balancer for Layer 4 when using VPC.**

## ![AWS ELB Classic Load Balancer Vs Application Load Balancer](https://jayendrapatil.com/wp-content/uploads/2017/08/AWS-ELB-Classic-Load-Balancer-vs-Application-Load-Balancer.png)
Supported Protocols

- Classic ELB operates at **layer 4** and supports HTTP, HTTPS, **TCP, SSL**
- ALB operates at **layer 7** and supports HTTP, HTTPS, **HTTP/2, WebSockets**
- NLB operates at the **connection level (Layer 4)**

## Load Balancing to Multiple Ports on the Same Instance

- Only ALB & NLB supports Load Balancing to multiple ports on the same instance

## Host-based Routing & Path-based Routing

- Host-based routing use host conditions to define rules that forward requests to different target groups based on the hostname in the host header. This enables ALB to support multiple domains using a single load balancer.
- Path-based routing use path conditions to define rules that forward requests to different target groups based on the URL in the request. Each path condition has one path pattern. If the URL in a request matches the path pattern in a listener rule exactly, the request is routed using that rule.
- Only ALB supports Host-based & Path-based routing.

![CLB vs ALB vs NLB Common configurations and Features](https://jayendrapatil.com/wp-content/uploads/2017/08/CLB-vs-ALB-vs-NLB-Common-configurations-and-Features.png)

## Slow Start

- By default, a target starts to receive its full share of requests as soon as it is registered with a target group and passes an initial health check.
- Using slow start mode gives targets time to warm up before the load balancer sends them a full share of requests.
- Only ALB supports slow start mode

## Static IP and Elastic IP Address

- NLB automatically provides a static IP per AZ (subnet) that can be used by applications as the front-end IP of the load balancer.
- NLB also allows the option to assign an Elastic IP per AZ (subnet) thereby providing your own fixed IP.
- Classic ELB and ALB does not support Static and Elastic IP address

## Connection Draining OR Deregistration Delay

- Connection draining enables the load balancer to complete in-flight requests made to instances that are de-registering or unhealthy.
- All Load Balancer types support connection draining/deregistration delay.  
    

## Idle Connection Timeout

- Idle Connection Timeout helps specify a time period, which ELB uses to close the connection if no data has been sent or received by the time that the idle timeout period elapses
- Can be configured for  CLB & ALB (default 60 seconds)  
    
- Cannot be configured for NLB (350 secs for TCP, 120 secs for UDP)  
    
- It is recommended to enable HTTP keep-alive in the web server settings for the EC2 instances, thus making the ELB reuse the backend connections until the keep-alive timeout expires.

## PrivateLink Support

- CLB and ALB do not support PrivateLink (TCP, TLS)
- Only NLB supports PrivateLink (TCP, TLS)

## Zonal Isolation

- Only NLB supports Zonal Isolation which supports application architectures in a single zone. It automatically fails over to other healthy AZs, if something fails in an AZ
- CLB and ALB do not support Zonal Isolation.

## Deletion Protection

- Only ALB & NLB supports Deletion Protection, wherein a load balancer can’t be deleted if deletion protection is enabled
- CLB does not support deletion protection.

## Preserve Source IP Address

- As the ELB intercepts the traffic between the client and the back-end servers, the back-end server does not know the IP address, Protocol, and the Port used between the Client and the Load balancer.
- Classic ELB (HTTP/HTTPS) and ALB do not preserve the client-side source IP.  It needs to be retrieved using `X-Forward-XXX`.
    - **X-Forwarded-For** request header to help back-end servers identify the IP address of a client when you use an HTTP or HTTPS load balancer.
    - **X-Forwarded-Proto** request header to help back-end servers identify the protocol (HTTP/S) that a client used to connect to the server
    - **X-Forwarded-Port** request header to help back-end servers identify the port that an HTTP or HTTPS load balancer uses to connect to the client.
- CLB (SSL/TLS) uses Proxy Protocol Version 1 and NLB uses Proxy Protocol Version 2 to provide the information.  
    
- NLB preserves the client-side source IP or needs Proxy Protocol allowing the back-end to see the IP address of the client.
    - If targets are registered by instance ID or ECS tasks, the source IP addresses of the clients are preserved and provided to the applications.
    - If targets are registered by IP address
        - for TCP & TLS, the source IP addresses are the private IP addresses of the load balancer nodes. Use Proxy Protocol.
        - for UDP & TCP\_UDP, it is enabled by default and the source IP addresses of the clients are preserved.

## Health Checks

- All Load Balancer types support Health checks to determine if the instance is healthy or unhealthy
- ALB provides health check improvements that allow detailed error codes from 200-399 to be configured

## Supported Platforms

- Classic ELB supports both EC2-Classic and EC2-VPC
- ALB and NLB support only EC2-VPC.

## WebSockets

- CLB does not support WebSockets
- Only ALB and NLB support WebSockets

## Cross-zone Load Balancing

- By default, Load Balancer will distribute requests evenly across its enabled AZs, irrespective of the instances it hosts.
- Cross-zone Load Balancing help distribute incoming requests evenly across all instances in its enabled AZs.
- CLB -> Cross Zone load balancing is disabled, by default, and can be enabled and free of charge.
- ALB -> Cross Zone load balancing is enabled by default and free.
- NLB -> Cross Zone load balancing is disabled, by default, and can be enabled but is charged for inter-az data transfer.

## Stick Sessions (Cookies)

- Stick Sessions (Session Affinity) enables the load balancer to bind a user’s session to a specific instance, which ensures that all requests from the user during the session are sent to the same instance
- CLB, ALB, and NLB support sticky sessions to maintain session affinity
- CLB and ALB maintain session stickiness using cookies.
- ~NLB does not support sticky sessions.~ NLB now supports sticky sessions.
- NLB uses a built-in 5-tuple hash table in order to maintain stickiness across backend servers.
- NLB idle timeout for TCP connections is 350 seconds. Once the timeout is reached or the session is terminated, the NLB will forget the stickiness and incoming packets will be considered as a new flow and could be load balanced to a new target.

![CLB vs ALB vs NLB Security](https://jayendrapatil.com/wp-content/uploads/2017/08/CLB-vs-ALB-vs-NLB-Security.png)

## SSL Termination/Offloading

- SSL Termination helps decrypt requests from clients before sending them to targets and hence reducing the load. SSL certificate must be installed on the load balancer.
- All load balancers types support SSL Termination.

## Server Name Indication

- CLB only supports a single certificate and does not support SNI  
    
- ALB and NLB support multiple certificates and use SNI to serve multiple secure websites using a single TLS listener.
    - If the hostname provided by a client matches a single certificate in the certificate list, the load balancer selects this certificate.
    - If a hostname provided by a client matches multiple certificates in the certificate list, the load balancer selects the best certificate that the client can support.

## ~Back-end Server Authentication~

- ~Back-end Server Authentication enables authentication of the instances.~ 
- ~Load balancer communicates with an instance only if the public key that the instance presents to the load balancer matches a public key in the authentication policy for the load balancer.~
- ~Classic Load Balancer supports Back-end Server Authentication~
- ~ALB **does not** support Back-end Server Authentication~

## CloudWatch Metrics

- All Load Balancer types integrate with CloudWatch to provide metrics, with ALB providing additional metrics

## Access Logs

- Access logs capture detailed information about requests sent to the load balancer. Each log contains information such as request received time, client’s IP address, latencies, request paths, and server responses
- All Load Balancer types provide access logs, with ALB providing additional attributes

## AWS Certification Exam Practice Questions

> - Questions are collected from Internet and the answers are marked as per my knowledge and understanding (which might differ with yours).
> - AWS services are updated everyday and both the answers and questions might be outdated soon, so research accordingly.
> - AWS exam questions are not updated to keep up the pace with AWS updates, so even if the underlying feature has changed the question might not be updated
> - Open to further feedback, discussion and correction.

1. A company wants to use load balancer for their application. However, the company wants to forward the requests without any header modification. What service should the company use?
    1. Classic Load Balancer
    2. **Network Load Balancer**
    3. Application Load Balancer
    4. Use Route 53
    
2. A Solutions Architect is building an Amazon ECS-based web application that requires that headers are not modified when being forwarded to Amazon ECS. Which load balancer should the Architect use?
    1. Application Load Balancer
    2. **Network Load Balancer**
    3. A virtual load balancer appliance from AWS marketplace
    4. Classic Load Balancer
3. An application tier currently hosts two web services on the same set of instances, listening on different ports. Which AWS service should a solutions architect use to route traffic to the service based on the incoming request?
    1. **AWS Application Load Balancer**
    2. Amazon CloudFront
    3. Amazon Route 53
    4. AWS Classic Load Balancer
4. A Solutions Architect needs to deploy an HTTP/HTTPS service on Amazon EC2 instances with support for WebSockets using load balancers. How can the Architect meet these requirements?
    1. Configure a Network Load balancer.
    2. **Configure an Application Load Balancer.**
    3. Configure a Classic Load Balancer.
    4. Configure a Layer-4 Load Balancer.
5. A company is hosting an application in AWS for third party access. The third party needs to whitelist the application based on the IP. Which AWS service can the company use in the whitelisting of the IP address?
    1. AWS Application Load Balancer
    2. AWS Classic Load balancer
    3. **AWS Network Load Balancer**
    4. AWS Route 53

## References

[AWS\_Elastic\_Load\_Balancing\_features](https://aws.amazon.com/elasticloadbalancing/features/)