---
tags:
  - cloud/aws
---
[Skip to content](https://jayendrapatil.com/aws-elb-application-load-balancer/#content)

- <mark style="background: #BBFABBA6;">Application Load Balancer operates at layer 7 (application layer) and allows defining routing rules based on content across multiple services or containers running on one or more EC2 instances.</mark>
- scales the load balancer as traffic to the application changes over time.
- can scale to the vast majority of workloads automatically.
- supports health checks, used to monitor the health of registered targets so that the load balancer can send requests only to the healthy targets.

![](https://dmhnzl5mp9mj6.cloudfront.net/application-management_awsblog/images/img2.png)
<!--⚠️Imgur upload failed, check dev console-->
![[Pasted image 20240229220402.png]]
## Application Load Balancer Components

![](https://docs.aws.amazon.com/elasticloadbalancing/latest/application/images/component_architecture.png)

- **A load balancer**
    - <mark style="background: #ADCCFFA6;">serves as the single point of contact for clients.</mark>
    - <mark style="background: #FFF3A3A6;">distributes incoming application traffic across multiple targets</mark>, such as EC2 instances, in multiple AZs, which increases the availability of the application.
    - <mark style="background: #ABF7F7A6;">one or more listeners can be added to the load balancer.</mark>
- **A listener**
    - <mark style="background: #FFF3A3A6;">checks for connection requests from clients, using the configured protocol and port</mark>
    - <mark style="background: #BBFABBA6;">rules defined determine, how the load balancer routes request to its registered targets.</mark>
    - <mark style="background: #ADCCFFA6;">each rule consists of a priority, one or more actions, and one or more conditions.</mark>
    - _supported actions_ are
        - <mark style="background: #CACFD9A6;">forward,</mark>
        - <mark style="background: #CACFD9A6;">redirect,</mark>
        - <mark style="background: #CACFD9A6;">fixed-response</mark>
        
    - _supported rule conditions_ are
        - host-header
        - http-request-method
        - path-pattern
        - source-ip
        - http-header
        - query-string
    - <mark style="background: #FFB8EBA6;">when the conditions for a rule are met, its actions are performed.</mark>
    - a default rule for each listener must be defined, and optionally additional rules can be defined
- **Target group**
    - routes requests to one or more registered targets, such as EC2 instances, using the specified protocol and port number
    - a target can be registered with multiple target groups.
    - health checks can be configured on a per target group basis.
    - health checks are performed on all targets registered to a target group that is specified in a listener rule for the load balancer.
    - target group supports
        - - **EC2 instances** (can be managed as a part of the [ASG](https://jayendrapatil.com/aws-auto-scaling/#Auto-Scaling-Groups-ASG))
            - **ECS tasks**
            - **Lambda functions**
            - **Private IP Addresses on AWS or On-premises** over [VPN](https://jayendrapatil.com/aws-vpc-vpn-cloudhub/) or [DX](https://jayendrapatil.com/aws-direct-connect-dx/).
    - supports weighted target group routing
        - enables routing of the traffic forwarded by a rule to multiple target groups.
        - enables use cases like blue-green, canary and hybrid deployments without the need for multiple load balancers.
        - also enables zero-downtime migration between on-premises and cloud or between different compute types like EC2 and Lambda.

- <mark style="background: #D2B3FFA6;">When a load balancer receives a request, it evaluates the listener rules in priority order to determine which rule to apply and then selects a target from the target group for the rule action.</mark>
- Listener rules can be configured to route requests to different target groups <mark style="background: #FFF3A3A6;">based on the content of the application traffic.</mark>
- Routing is performed independently for each target group, even when a target is registered with multiple target groups.
- <mark style="background: #083CA4A6;">Routing algorithm used can be configured at the target group level.</mark>
- _Default routing algorithm_ is <mark style="background: #FF5582A6;">round-robin</mark>; alternatively, <mark style="background: #FFB8EBA6;">the least outstanding requests routing algorithm</mark> can also be specified  
![[Pasted image 20240229181550.png]]
## Classic Load Balancer Vs Application Load Balancer Vs Network Load Balancer

Refer Blog Post @ [Classic Load Balancer vs Application Load Balancer vs Network Load Balancer](https://jayendrapatil.com/aws-classic-load-balancer-vs-application-load-balancer/)

## Application Load Balancer Benefits

- Support for <mark style="background: #FFF3A3A6;">Path-based routing</mark>,  <mark style="background: #ADCCFFA6;">where listener rules can be configured to forward requests based on the URL in the request</mark>. <mark style="background: #ABF7F7A6;">This enables structuring applications as smaller services (microservices), and route requests to the correct service based on the content of the URL.</mark>
  
- Support for routing requests to multiple services on a single EC2 instance by registering the instance using multiple ports using Dynamic Port mapping.
  
- <mark style="background: #ABF7F7A6;">Support for containerized applications</mark>. [EC2 Container Service (ECS)](https://jayendrapatil.com/aws-ec2-container-service-ecs/) can select an unused port when scheduling a task and register the task with a target group using this port, enabling efficient use of the clusters.
- <mark style="background: #FFF3A3A6;">Support for monitoring the health of each service independently</mark>, as health checks are defined at the target group level and many [CloudWatch](https://jayendrapatil.com/aws-cloudwatch-agent/) metrics are reported at the target group level.
- Attaching a target group to an Auto Scaling group enables scaling each service dynamically based on demand.

## Application Load Balancer Features

- supports load balancing of applications using **HTTP and HTTPS (Secure HTTP) protocols**
- supports **HTTP/2**, which is enabled natively. Clients that support HTTP/2 can connect over TLS
- supports **WebSockets** and Secure WebSockets natively
- supports **Request tracing**, by default.
    - <mark style="background: #FFF3A3A6;">request tracing can be used to track HTTP requests from clients to targets or other services.</mark>
    - Load balancer upon receiving a request from a client, adds or updates the **X-Amzn-Trace-Id** header before sending the request to the target
    - Any services or applications between the load balancer and the target can also add or update this header.
- supports **Sticky Sessions (Session Affinity)** using load balancer generated cookies, to route requests from the same client to the same target
- supports **SSL termination**, <mark style="background: #FFF3A3A6;">to decrypt the request on ALB before sending it to the underlying targets.</mark>
    - <mark style="background: #CACFD9A6;">an SSL certificate can be installed on the load balancer</mark>.
    - <mark style="background: #CACFD9A6;">the load balancer uses this certificate to terminate the connection and then decrypt requests from clients before sending them to targets.</mark>
- supports layer 7 specific features like **X-Forwarded-For** headers to help determine the actual client IP, port and protocol
- automatically **scales** its request handling capacity in response to incoming application traffic.
- supports **hybrid load balancing,**
    - <mark style="background: #FFF3A3A6;">If an application runs on targets distributed between a VPC and an on-premises location, they can be added to the same target group using their IP addresses</mark>
- provides **High Availability**, by <mark style="background: #FFF3A3A6;">allowing you to specify more than one AZ and distribution of incoming traffic across multiple AZs.</mark>
- integrates with [**ACM**](https://jayendrapatil.com/aws-certificate-manager-acm/) <mark style="background: #ADCCFFA6;">to provision and bind an SSL/TLS certificate to the load balancer thereby making the entire SSL offload process very easy</mark>
- supports multiple certificates for the same domain to a secure listener
- supports **IPv6** addressing, for an Internet-facing load balancer
- supports **Cross-zone load balancing**, by default
- supports **Security Groups** to control the traffic allowed to and from the load balancer.
- provides **Access Logs**, to record all requests sent to the load balancer, and store the logs in S3 for later analysis in compressed format
- provides **Delete Protection**, to prevent the ALB from accidental deletion
- supports **Connection Idle Timeout** – ALB maintains two connections for each request one with the Client (front end) and one with the target instance (back end). If no data has been sent or received by the time that the idle timeout period elapses, ALB closes the front-end connection
- integrates with [**CloudWatch**](https://jayendrapatil.com/aws-cloudwatch-overview/) to provide metrics, such as request counts, error counts, error types, and request latency
- integrates with [**AWS WAF**](https://jayendrapatil.com/aws-waf/), a web application firewall that helps protect web applications from attacks by allowing rules configuration based on IP addresses, HTTP headers, and custom URI strings
- integrates with [**CloudTrail**](https://jayendrapatil.com/aws-cloudtrail/) to receive a history of ALB API calls made on the AWS account
- back-end server authentication (MTLS) is NOT supported

## Application Load Balancer Listeners

- <mark style="background: #ADCCFFA6;">A listener is a process that checks for connection requests, using the configured protocol and port</mark>
- Listener supports HTTP & HTTPS protocol with Ports from 1-65535
- ALB supports SSL Termination for HTTPS listeners, which helps to offload the work of encryption and decryption so that the targets can focus on their main work.
- ~HTTPS listener supports exactly one SSL server certificate on the listener.~
- <mark style="background: #FFF3A3A6;">HTTPS listener must have at least one SSL server certificate on the listener</mark>
- WebSockets with both HTTP and HTTPS listeners (Secure WebSockets)
- Supports HTTP/2 with HTTPS listeners
    - 128 requests can be sent in parallel using one HTTP/2 connection.
    - <mark style="background: #ADCCFFA6;">ALB converts these to individual HTTP/1.1 requests and distributes them across the healthy targets in the target group using the round-robin routing algorithm.</mark>
    - HTTP/2 uses front-end connections more efficiently resulting in fewer connections between clients and the load balancer.
    - Server-push feature of HTTP/2 is not supported
- Each listener has a default rule, and can optionally define additional rules.
- Each rule consists of a priority, action, optional host condition, and optional path condition.
    - Priority – Rules are evaluated in priority order, from the lowest value to the highest value. The default rule has the lowest priority
    - Action – Each rule action has a type and a target group. Currently, the only supported type is forward, which forwards requests to the target group. You can change the target group for a rule at any time.
    - Condition – There are two types of rule conditions: host and path. When the conditions for a rule are met, then its action is taken
- **Host Condition or Host-based routing**
    - Host conditions can be used to define rules that forward requests to different target groups based on the hostname in the host header
    - This enables support for multiple domains using a single ALB _for e.g. orders.example.com, images.example.com, registration.example.com_
    - Each host condition has one hostname. If the hostname in
- **Path Condition or path-based routing**
    - Path conditions can be used to define rules that forward requests to different target groups based on the URL in the request
    - Each path condition has one path pattern _for e.g. example.com/orders, example.com/images, example.com/registration_
    - If the URL in a request matches the path pattern in a listener rule exactly, the request is routed using that rule.

## Advantages over Classic Load Balancer

- Support for **path-based routing**, where rules can be configured for the listener to forward requests based on the content of the URL
- Support for **host-based routing**, where rules can be configured for the listener to forward requests based on the host field in the HTTP header.
- Support for **routing based on fields in the request**, such as standard and custom HTTP headers and methods, query parameters, and source IP address
- Support for routing requests to multiple applications on a single EC2 instance. Each instance or IP address can be registered with the same target group using multiple ports
- Support for **registering targets by IP address**, including targets outside the VPC for the load balancer.
- Support for **redirecting requests** from one URL to another.
- Support for **returning a custom HTTP response**.
- Support for **registering Lambda functions** as targets.
- Support for the load balancer to authenticate users of the applications through their corporate or social identities before routing requests.
- Support **containerized** applications with ECS using Dynamic port mapping
- Support monitoring the health of each service independently, as health checks and many CloudWatch metrics are defined at the target group level
- Attaching the target group to an Auto Scaling group enables scaling of each service dynamically based on demand
- Access logs contain additional information & stored in compressed format
- Improved load balancer performance.

## Application Load Balancer Pricing
- charged for each hour or partial hour that an ALB is running and the number of Load Balancer Capacity Units (LCU) used per hour.
- An LCU is a new metric for determining ALB pricing
- An LCU defines the maximum resource consumed in any one of the dimensions (new connections, active connections, bandwidth and rule evaluations) the Application Load Balancer processes the traffic.

## AWS Certification Exam Practice Questions

> - Questions are collected from Internet and the answers are marked as per my knowledge and understanding (which might differ with yours).
> - AWS services are updated everyday and both the answers and questions might be outdated soon, so research accordingly.
> - AWS exam questions are not updated to keep up the pace with AWS updates, so even if the underlying feature has changed the question might not be updated
> - Open to further feedback, discussion and correction.

1. You are designing an application which requires websockets support, to exchange real-time messages with end-users without the end users having to request (or poll) the server for an update? Which ELB option should you choose?
    1. Use Application Load Balancer and enable comet support
    2. Use Classic Load Balancer which supports WebSockets
    3. **Use Application Load Balancer which supports WebSockets**
    4. Use Classic Load Balancer and enable comet support
2. Which of the following Internet protocols does an AWS Application Load Balancer Support? Choose 2 answers  
    A. ICMP  
    B. UDP  
    C. **HTTP**  
    D. SNTP  
    E. **Websocket**
3. Your organization has configured an application behind ALB. However, Clients are complaining that they cannot connect to an Internet-facing load balancer. What cannot be the issue?
    1. Internet-facing load balancer is attached to a private subnet
    2. ALB Security Groups does not allow the traffic
    3. Subnet NACLs do not allow the traffic
    4. **ALB was not assigned an EIP**
4. To protect your ALB from accidental deletion, you should
    1. enable Multi-Factor Authentication (MFA) protected access
    2. **enable Delete Protection on the ALB**
    3. enabled Termination Protection on the ALB
    4. ALB does not provide any feature to prevent accidental deletion
5. Your organization is using ALB for servicing requests. One of the API request is facing consistent performance issues. Upon checking the flow, you find that the request flows through multiple services. How can you track the performance or timing issues in the application stack at the granularity of an individual request?
    1. **Track the request using “X-Amzn-Trace-Id” HTTP header**
    2. Track the request using “X-Amzn-Track-Id” HTTP header
    3. Track the request using “X-Aws-Track-Id” HTTP header
    4. Track the request using “X-Aws-Trace-Id” HTTP header

### References

Refer AWS documentation – [ELB\_Application\_Load\_Balancer](http://docs.aws.amazon.com/elasticloadbalancing/latest/application/introduction.html)