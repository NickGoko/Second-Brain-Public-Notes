---
tags:
  - cloud/aws
review-frequency: high
reviewed: 2023-12-21
---
**Elastic Load Balancing**<mark style="background: #ADCCFFA6;"> automatically distributes incoming application traffic across multiple targets</mark>, such as <mark style="background: #ADCCFFA6;">Amazon EC2 instances, containers, and IP addresses.</mark>

- **Network traffic can be distributed across a single or multiple Availability Zones (AZs) within an AWS Region.**

There are four types of Elastic Load Balancer (ELB) on AWS:

- **Classic Load Balancer (CLB)** – this is the oldest of the three and provides basic <mark style="background: #ADCCFFA6;">load balancing at both layer 4 and layer 7.</mark>
- **Application Load Balancer (ALB)** – <mark style="background: #ADCCFFA6;">layer 7 load balancer</mark> that <mark style="background: #ABF7F7A6;">routes connections based on the content of the request.</mark>
- **Network Load Balancer (NLB)** –<mark style="background: #ADCCFFA6;"> layer 4 load balancer</mark> that <mark style="background: #ABF7F7A6;">routes connections based on IP protocol data.</mark>
- **Gateway Load Balancer (GLB)** –<mark style="background: #ADCCFFA6;"> layer 3/4 load balancer</mark> <mark style="background: #ABF7F7A6;">used in front of virtual appliances</mark> such as <mark style="background: #ABF7F7A6;">firewalls and IDS/IPS systems.</mark>

**_Note:_** _The CLB is not covered in detail on this page as it is on old generation load balancer and is no longer featured on most AWS exams._

![[Pasted image 20240229213938.png]]  
The following table provides a comparison of some of the key features relevant to AWS exams:

|   |   |   |   |   |
|---|---|---|---|---|
|**Feature**|**Application Load Balancer**|**Network Load Balancer**|**Classic Load Balancer**|**Gateway Load Balancer**|
|**OSI Layer**|Layer 7|Layer 4|Layer 4/7|Layer 3 Gateway + Layer 4 Load Balancing|
|**Target Type**|IP, Instance, Lambda|IP, Instance, ALB|N/A|IP, Instance|
|**Protocols**|HTTP, HTTPS|TCP|TCP, SSL, HTTP, HTTPS|IP|
|**WebSockets**|✔|✔||✔|
|**IP addresses as a target**|✔|✔|||
|**HTTP header-based routing**|✔||||
|**HTTP/2/gRPC**|✔||||
|**Configurable idle connection timeout**|✔||✔||
|**Cross-zone load balancing**|✔|✔|✔|✔|
|**SSL Offloading**|✔|✔|✔||
|**Server Name Indication (SNI)**|✔|✔|✔||
|**Sticky sessions**|✔|✔|✔|✔|
|**Static / Elastic IP Address**||✔|||
|**Custom Security policies**|||✔||

- <mark style="background: #BBFABBA6;">Elastic Load Balancing provides fault tolerance for applications by automatically balancing traffic across targets</mark> –

**Targets** can be <mark style="background: #BBFABBA6;">Amazon EC2 instances, containers, IP addresses, and Lambda functions.</mark>

- <mark style="background: #BBFABBA6;">ELB distributes traffic across Availability Zones while ensuring only healthy targets receive traffic.</mark>

<mark style="background: #FF5582A6;">Only 1 subnet per AZ can be enabled for each ELB.</mark>

Amazon Route 53 can be used for region load balancing with ELB instances configured in each region.

ELBs can be **Internet** facing or **internal-only.**

Internet facing ELB:

- ELB nodes have public IPs.
- Routes traffic to the private IP addresses of the EC2 instances.
- Need one public subnet in each AZ where the ELB is defined.
- ELB DNS name format: <`name>-<id-number>.<region>.elb.amazonaws.com.`

Internal only ELB:

- ELB nodes have private IPs.
- Routes traffic to the private IP addresses of the EC2 instances.
- ELB DNS name format: ``**internal**-<name>-<id-number>.<region>.elb.amazonaws.com.``

Internal-only load balancers do not need an Internet gateway.

EC2 instances and containers can be registered against an ELB.

ELB nodes use IP addresses within your subnets, ensure at least a /27 subnet and make sure there are at least 8 IP addresses available for the ELB to scale.

An ELB forwards traffic to eth0 (primary IP address).

An ELB listener is the process that checks for connection requests:

- CLB listeners support the TCP and HTTP/HTTPS protocols.
- ALB listeners support the HTTP and HTTPS protocols.
- NLB listeners support the TCP, UDP and TLS protocols.
- GLB listeners support the IP protocol.

Deleting an ELB does not affect the instances registered against it (they won’t be deleted; they just won’t receive any more requests).

For ALB at least 2 subnets must be specified.

For NLB only one subnet must be specified (recommended to add at least 2).

ELB uses a DNS record TTL of 60 seconds to ensure new ELB node IP addresses are used to service clients.

By default the ELB has an idle connection timeout of 60 seconds, set the idle timeout for applications to at least 60 seconds.

Perfect Forward Secrecy (PFS) provides additional safeguards against the eavesdropping of encrypted data, using a unique random session key.

Server Order Preference lets you configure the load balancer to enforce cipher ordering, providing more control over the level of security used by clients to connect with your load balancer.

ELB does not support client certificate authentication (API Gateway does support this).

## ELB Security Groups

Security groups control the ports and protocols that can reach the front-end listener.

In non-default VPCs you can choose which security group to assign.

You must assign a security group for the ports and protocols on the front-end listener.

You need to also allow the ports and protocols for the health check ports and back-end listeners.

Security group configuration for ELB:

Inbound to ELB (allow).

- Internet-facing ELB:
    - Source: 0.0.0.0/0.
    - Protocol: TCP.
    - Port: ELB listener ports.

![Internet-Facing ELB Security Group Inbound Rules](https://digitalcloud.training/wp-content/uploads/2022/01/internet-facing-elb-security-group-inbound-rules.jpeg)

- Internal-only ELB:
    - Source: VPC CIDR.
    - Protocol: TCP.
    - Port: ELB Listener ports.

![Internal-Only ELB Security Group Inbound Rules](https://digitalcloud.training/wp-content/uploads/2022/01/internal-only-elb-security-group-inbound-rules.jpeg)

Outbound (allow, either type of ELB):

- Destination: EC2 registered instances security group.
- Protocol: TCP.
- Port: Health Check/Listener.

![Internet-Facing ELB Security Group Outbound Rules](https://digitalcloud.training/wp-content/uploads/2022/01/internet-facing-elb-security-group-outbound-rules.jpeg)

Security group configuration for registered instances:

Inbound to registered instances (Allow, either type of ELB).

- Source: ELB Security Group.
- Protocol: TCP.
- Port: Health Check/Listener.

![EC2 Registered Instances Security Group Inbound Rules](https://digitalcloud.training/wp-content/uploads/2022/01/ec2-registered-instances-security-group-inbound-ru.jpeg)

Outbound (Allow, for both types of ELB).

- Destination: ELB Security Group.
- Protocol: TCP.
- Port: Ephemeral.

![EC2 Registered Instances Security Group Outbound Rules](https://digitalcloud.training/wp-content/uploads/2022/01/ec2-registered-instances-security-group-outbound-r.jpeg)

It is also important to ensure NACL settings are set correctly.

## Distributed Denial of Service (DDoS) Protection:

ELB automatically distributes incoming application traffic across multiple targets, such as EC2 instances, containers, and IP addresses, and multiple Availability Zones, which minimizes the risk of overloading a single resource.

ELB only supports valid TCP requests so DDoS attacks such as UDP and SYN floods are not able to reach EC2 instances.

ELB also offers a single point of management and can serve as a line of defense between the internet and your backend, private EC2 instances.

You can also attach AWS Web Application Firewall (WAF) Web ACLs to Application Load Balancers to protect against web exploits.

## ELB Monitoring

Monitoring takes place using:

- CloudWatch – every 1 minute.
    - ELB service only sends information when requests are active.
    - Can be used to trigger SNS notifications.
- Access Logs.
    - Disabled by default.
    - Includes information about the clients (not included in CloudWatch metrics).
    - Can identify requester, IP, request type etc.
    - Can be optionally stored and retained in S3.
- CloudTrail.
    - Can be used to capture API calls to the ELB.
    - Can be stored in an S3 bucket.

## Target Groups

Target groups are a logical grouping of targets and are used with ALB, NLB, and GLB.

Targets are the endpoints and can be EC2 instances, ECS containers, IP addresses, Lambda functions, and other load balancers.

Target groups can exist independently from the ELB.

A single target can be in multiple target groups.

Only one protocol and one port can be defined per target group.

You cannot use public IP addresses as targets.

You cannot use instance IDs and IP address targets within the same target group.

A target group can only be associated with one load balancer.

The following diagram illustrates the basic components. Notice that each listener contains a default rule, and one listener contains another rule that routes requests to a different target group. One target is registered with two target groups.

![ALB Listeners, targets and rules](https://digitalcloud.training/wp-content/uploads/2022/01/alb-listeners-targets-and-rules.jpeg)

Target groups are used for registering instances against an ALB, NLB, or GLB.

Target groups are a regional construct (as are ELBs).

The following diagram shows how target groups can be used with an ALB using host-based and target-based routing to route traffic to multiple websites, running on multiple ports, on a single EC2 instance:

![ALB Host-Path Routing](https://digitalcloud.training/wp-content/uploads/2022/01/alb-host-path-routing.jpeg)

The following attributes can be defined:

- Deregistration delay – the amount of time for Elastic Load Balancing to wait before deregistering a target.
- Slow start duration – the time, in seconds, during which the load balancer sends a newly registered target a linearly increasing share of the traffic to the target group.
- Stickiness – indicates whether sticky sessions are enabled.

The default settings for attributes are shown below:

![ELB Target Group Attributes](https://digitalcloud.training/wp-content/uploads/2022/01/elb-target-group-attributes.jpeg)

Auto Scaling groups can scale each target group individually.

You can only use Auto Scaling with the load balancer if using instance IDs in your target group.

Health checks are defined per target group.

ALB/NLB/GLB can route to multiple target groups.

You can register the same EC2 instance or IP address with the same target group multiple times using different ports (used for routing requests to microservices).

If you register by instance ID the traffic is routed using the primary private IP address of the primary network interface.

If you register by IP address you can route traffic to an instance using any private address from one or more network interfaces.

You cannot mix different types within a target group (EC2, ECS, IP, Lambda function).

IP addresses can be used to register:

- Instances in a peered VPC.
- AWS resources that are addressable by IP address and port.
- On-premises resources linked to AWS through Direct Connect or a VPN connection.

## Application Load Balancer (ALB)

The Application Load Balancer operates at the request level (layer 7), routing traffic to targets – EC2 instances, containers and IP addresses based on the content of the request.

You can load balance HTTP/HTTPS applications and use layer 7-specific features, such as X-Forwarded-For headers.

The ALB supports HTTPS termination between the clients and the load balancer.

The ALB supports management of SSL certificates through AWS IAM and AWS Certificate Manager for predefined security policies.

The ALB supports Server Name Indication (SNI) which allows multiple secure websites to use a single secure listener.

With Server Name Indication (SNI) a client indicates the hostname to which it wants to connect.

IP addresses can be configured as targets which allows load balancing to applications hosted in AWS or on-premises using the IP addresses of the back-end instances/servers as targets.

You need at least two Availability Zones, and you can distribute incoming traffic across your targets in multiple Availability Zones.

The ALB automatically scales its request handling capacity in response to incoming application traffic.

You can configure an ALB to be Internet facing or create a load balancer without public IP addresses to serve as an internal (non-Internet-facing) load balancer.

The ALB supports content-based routing which allows the routing of requests to a service based on the content of the request. For example:

- **Host-based routing** routes client requests based on the Host field of the HTTP header allowing you to route to multiple domains from the same load balancer.
- **Path-based routing** routes a client request based on the URL path of the HTTP header (e.g. /images or /orders).

Support for microservices and containers with load balancing across multiple ports on a single EC2 instance.

Integration with Amazon Cognito for user authentication.

The slow start mode allows targets to “warm up” with a ramp-up period.

Health Checks:

- Can have custom response codes in health checks (200-399).
- Details provided in the API and management console for health check failures.
- Reason codes are returned with failed health checks.
- Health checks do not support WebSockets.
- Fail open means that if no AZ contains a healthy target the load balancer nodes route requests to all targets.

Detailed access log information is provided and saved to an S3 bucket every 5 or 6 minutes.

Deletion protection is possible.

Deregistration delay is like connection draining.

**Sticky Sessions:**

- Uses cookies to ensure a client is bound to an individual back-end instance for the duration of the cookie lifetime.
- ALB supports duration-based cookies and application-based cookies.
- For application-based cookies the cookie name is specified for each target group.
- For duration-based cookies the name of the cookie is always AWSALB.
- Sticky sessions are enabled at the target group level.
- WebSockets connections are inherently sticky (following the upgrade process).

### Listeners and Rules

Listeners:

- Each ALB needs at least one listener and can have up to 10.
- Listeners define the port and protocol to listen on.
- Can add one or more listeners.
- Cannot have the same port in multiple listeners.

**Listener rules:**

- Rules determine how the load balancer routes requests to the targets in one or more target groups.
- Each rule consists of a priority, one or more actions, an optional host condition, and an optional path condition.
- Only one action can be configured per rule.
- One or more rules are required.
- Each listener has a default rule, and you can optionally define additional rules.
- Rules determine what action is taken when the rule matches the client request.
- Rules are defined on listeners.
- You can add rules that specify different target groups based on the content of the request (content-based routing).
- If no rules are found the default rule will be followed which directs traffic to the default target groups.

The image below shows a ruleset with a host-based and path-based entry and a default rule at the end:

![ALB Ruleset](https://digitalcloud.training/wp-content/uploads/2022/01/alb-ruleset.jpeg)

**Default rules:**

- When you create a listener you define an action for the default rule.
- Default rules cannot have conditions.
- You can delete the non-default rules for a listener at any time.
- You cannot delete the default rule for a listener.
- When you delete a listener all its rules are deleted.
- If no conditions for any of a listener’s rules are met, the action for the default rule is taken.

**Rule priority:**

- Each rule has a priority, and they are evaluated in order of lowest to highest.
- The default rule is evaluated last.
- You can change the value of a non-default rule at any time.
- You cannot change the value of the default rule.

**Rule action:**

- Only one target group per action.
- Each rule has a type and a target group.
- The only supported action type is forward, which forwards requests to the target group.
- You can change the target group for a rule at any time.

**Rule conditions:**

- There are two types of rule condition: host and path.
- When the conditions for a rule are met the action is taken.
- Each rule can have up to 2 conditions, 1 path condition and 1 host condition.
- Optional condition is the path pattern you want the ALB to evaluate for it to route requests.

**Request routing:**

- After the load balancer receives a request it evaluates the listener rules in priority order to determine which rule to apply, and then selects a target from the target group for the rule action using the round robin routing algorithm.
- Routing is performed independently for each target group even when a target is registered with multiple target groups.
- You can configure listener rules to route requests to different target groups based on the content of the application traffic.

**Content-based routing:**

- ALB can route requests based on the content of the request in the host field: host-based or path-based.
- Host-based is domain name-based routing e.g. example.com or app1.example.com.
- The host field contains the domain name and optionally the port number.
- Path-based is URL based routing e.g. example.com/images, example.com/app1.
- You can also create rules that combine host-based and path-based routing.
- Anything that doesn’t match content routing rules will be sent to a default target group.
- The ALB can also route based on [other information](https://docs.aws.amazon.com/elasticloadbalancing/latest/application/load-balancer-listeners.html) in the HTTP header including query string parameters, request method, and source IP addresses

### ALB and ECS

ECS service maintains the “desired count” of instances.

Optionally a load balancer can distribute traffic across tasks.

All containers in a single task definition are placed on a single EC2 container instance.

ECS service can only use a single load balancer.

ALB does not support multiple listeners in a single task definition.

ALB supports dynamic host-port mapping which means that multiple ports from the same service are allowed on the same container host.

ALB supports path-based routing and priority rules.

The ALB integrates with the EC2 container service using service load balancing.

Federated authentication:

- ALB supports authentication from OIDC compliant identity providers such as Google, Facebook, and Amazon.
- Implemented through an authentication action on a listener rule that integrates with Amazon Cognito to create user pools.
- AWS SAM can also be used with Amazon Cognito.

## Network Load Balancer

Network Load Balancer operates at the connection level (Layer 4), routing connections to targets – Amazon EC2 instances, containers and IP addresses based on IP protocol data.

The NLB is designed to handle millions of requests/sec and to support sudden volatile traffic patterns at extremely low latencies.

The NLB can be configured with a single static/Elastic IP address for each Availability Zone.

You can load balance any application hosted in AWS or on-premises using IP addresses of the application back-ends as targets.

The NLB supports connections from clients to IP-based targets in peered VPCs across different AWS Regions.

NLB supports both network and application target health checks.

NLB supports long-running/lived connections (ideal for WebSocket applications).

NLB supports failover between IP addresses within and across AWS Regions (uses Amazon Route 53 health checks).

The integration with Amazon Route 53 enables the removal of a failed load balancer IP address from service and subsequent redirection of traffic to an alternate NLB in another region.

NLB support cross-zone load balancing, but it is not enabled by default when the NLB is created through the console.

Target groups for NLBs support the following protocols and ports:

- **Protocols:** TCP, TLS, UDP, TCP_UDP.
- **Ports:** 1-65535.

The table below summarizes the supported listener and protocol combinations and target group settings:

|   |   |   |   |
|---|---|---|---|
|**Listener Protocol**|**Target Group Protocol**|**Target Group Type**|**Health Check Protocol**|
|TCP|TCP \| TCP_UDP|instance \| ip|HTTP \| HTTPS \| TCP|
|TLS|TCP \| TLS|Instance \| ip|HTTP \| HTTPS \| TCP|
|UDP|UDP \| TCP_UDP|instance|HTTP \| HTTPS \| TCP|
|TCP_UDP|TCP_UDP|instance|HTTP \| HTTPS \| TCP|

Amazon CloudWatch reports Network Load Balancer metrics.

You can use VPC Flow Logs to record all requests sent to your load balancer.

## Monitoring

AWS CloudTrail captures API calls for auditing.

You only pay for the S3 storage charges.

CloudTrail only monitors API calls.

Access logs can be used to monitor other actions such as the time the request was received, the client’s IP address, request paths etc.

Access logging is optional and disabled by default.

You are only charged for the S3 storage with access logging.

With access logging, the ALB logs requests sent to the load balancer including requests that never reached targets.

The ALB does not log health check requests.

# FAQ
## General

**Q: How do I decide which load balancer to select for my application?**

A: Elastic Load Balancing (ELB) supports four types of load balancers. You can select the appropriate load balancer based on your application needs. If you need to load balance HTTP requests, we recommend you use the Application Load Balancer (ALB). For network/transport protocols (layer4 – TCP, UDP) load balancing, and for extreme performance/low latency applications we recommend using Network Load Balancer. If your application is built within the Amazon Elastic Compute Cloud (Amazon EC2) Classic network, you should use Classic Load Balancer. If you need to deploy and run third-party virtual appliances, you can use Gateway Load Balancer.  

**Q: Can I privately access Elastic Load Balancing APIs from my Amazon Virtual Private Cloud (VPC) without using public IPs?**

A: Yes, you can privately access Elastic Load Balancing APIs from your Amazon Virtual Private Cloud (VPC) by creating [VPC endpoints](http://docs.aws.amazon.com/AmazonVPC/latest/UserGuide/vpc-endpoints.html). With VPC endpoints, the routing between the VPC and Elastic Load Balancing APIs is handled by the AWS network without the need for an Internet gateway, network address translation (NAT) gateway, or virtual private network (VPN) connection. The latest generation of VPC Endpoints used by Elastic Load Balancing are powered by AWS PrivateLink, an AWS technology enabling the private connectivity between AWS services using Elastic Network Interfaces (ENI) with private IPs in your VPCs. To learn more about [AWS PrivateLink](https://aws.amazon.com/privatelink/), visit the AWS PrivateLink [documentation](http://docs.aws.amazon.com/AmazonVPC/latest/UserGuide/VPC_Introduction.html#what-is-privatelink.html).  

**Q: Is there an SLA for load balancers?**

A: Yes, Elastic Load Balancing guarantees a monthly availability of at least 99.99% for your load balancers (Classic, Application or Network). To learn more about the SLA and know if you are qualified for a credit, [visit here](https://aws.amazon.com/elasticloadbalancing/sla/).  

## Application Load Balancer

**Q: Which operating systems does an Application Load Balancer support?**

A: An Application Load Balancer supports targets with any operating system currently supported by the Amazon EC2 service.

**Q: Which protocols does an Application Load Balancer support?**

A: An Application Load Balancer supports load balancing of applications using HTTP and HTTPS (Secure HTTP) protocols.

**Q: Is HTTP/2 Supported on an Application Load Balancer?**

A: Yes. HTTP/2 support is enabled natively on an Application Load Balancer. Clients supporting HTTP/2 can connect to an Application Load Balancer over TLS.  

**Q: How can I use static IP or PrivateLink on my Application Load Balancer?**

A: You can forward traffic from your Network Load Balancer, which provides support for PrivateLink and a static IP address per Availability Zone, to your Application Load Balancer. Create an Application Load Balancer-type target group, register your Application Load Balancer to it, and configure your Network Load Balancer to forward traffic to the Application Load Balancer-type target group.  

**Q: What TCP ports can I use to load balance?**

A: You can perform load balancing for the following TCP ports: 1-65535

**Q: Is WebSockets supported on an Application Load Balancer?**

A: Yes. WebSockets and Secure WebSockets support is available natively and ready for use on an Application Load Balancer.

**Q: Is Request tracing supported on an Application Load Balancer?**

A: Yes. Request tracing is enabled by default on your Application Load Balancer.

**Q: Does a Classic Load Balancer have the same features and benefits as an Application Load Balancer?**

A: While there is some overlap, there is no feature parity between the two types of load balancers. Application Load Balancers are the foundation of our application layer load-balancing platform for the future.

**Q: Can I configure my Amazon EC2 instances to accept traffic only from my Application Load Balancers?**

A: Yes.

**Q: Can I configure a security group for the front end of an Application Load Balancer?**  

A: Yes.

**Q: Can I use the existing APIs that I use with my Classic Load Balancer with an Application Load Balancer?**

A: No. Application Load Balancers require a new set of application programming interfaces (APIs).

**Q: How do I manage both Application and Classic Load Balancers simultaneously?**

A: The ELB Console will allow you to manage Application and Classic Load Balancers from the same interface. If you are using the command-line interface (CLI) or a software development kit (SDK), you will use a different ‘service’ for Application Load Balancers. For example, in the CLI you will describe your Classic Load Balancers using \`aws elb describe-load-balancers\` and your Application Load Balancers using \`aws elbv2 describe-load-balancers\`.

**Q: Can I convert my Classic Load Balancer to an Application Load Balancer (and vice-versa)?**  

A: No, you cannot convert one load balancer type into another.

**Q: Can I migrate to Application Load Balancer from Classic Load Balancer?**

A: Yes. You can migrate to Application Load Balancer from Classic Load Balancer using one of the options listed in this [document](https://docs.aws.amazon.com/elasticloadbalancing/latest/userguide/migrate-to-application-load-balancer.html).

**Q: Can I use an Application Load Balancer as a Layer-4 load balancer?**

A: No. If you need Layer-4 features, you should use Network Load Balancer.

**Q: Can I use a single Application Load Balancer for handling HTTP and HTTPS requests?**

A: Yes, you can add listeners for HTTP port 80 and HTTPS port 443 to a single Application Load Balancer.

**Q: Can I get a history of Application Load Balancing API calls made on my account for security analysis and operational troubleshooting purposes?**

A: Yes. To receive a history of Application Load Balancing API calls made on your account, use [AWS CloudTrail](https://aws.amazon.com/cloudtrail/).

**Q: Does an Application Load Balancer support HTTPS termination?**

A: Yes, you can terminate HTTPS connection on the Application Load Balancer. You must install a Secure Sockets Layer (SSL) certificate on your load balancer. The load balancer uses this certificate to terminate the connection and then decrypt requests from clients before sending them to targets.

**Q: What are the steps to get a SSL certificate?**

A: You can either use [AWS Certificate Manager](https://aws.amazon.com/certificate-manager/) to provision an SSL/TLS certificate or you can obtain the certificate from other sources by creating the certificate request, getting the certificate request signed by a CA, and then uploading the certificate either using AWS Certification Manager or the [AWS Identity and Access Management](https://aws.amazon.com/iam/) (IAM) service.

**Q: How does an Application Load Balancer integrate with AWS Certificate Manager (ACM)?**

A: An Application Load Balancer is integrated with AWS Certificate Management (ACM). Integration with ACM simplifies binding a certificate to the load balancer, thereby streamlining the entire SSL offload process. Purchasing, uploading, and renewing SSL/TLS certificates is a complex, manual, and time-consuming process. With ACM integration with Application Load Balancer, this whole process has been shortened to simply requesting a trusted SSL/TLS certificate and selecting the ACM certificate to provision it with the load balancer.

**Q: Is back-end server authentication supported with an Application Load Balancer?**

A: No, only encryption is supported to the back-ends with an Application Load Balancer.

**Q: How can I enable Server Name Indication (SNI) for my Application Load Balancer?**

A: SNI is automatically enabled when you associate more than one TLS certificate with the same secure listener on a load balancer. Similarly, SNI mode for a secure listener is automatically disabled when you have only one certificate associated to a secure listener.

**Q: Can I associate multiple certificates for the same domain to a secure listener?**

A: Yes, you can associate multiple certificates for the same domain to a secure listener. For example, you can associate:

- ECDSA and RSA certificates
- Certificates with different key sizes (e.g. 2K and 4K) for SSL/TLS certificates
- Single-Domain, Multi-Domain (SAN) and Wildcard certificates

**Q: Is IPv6 supported with an Application Load Balancer?**

A: Yes, IPv6 is supported with an Application Load Balancer.

**Q: How do you set up rules on an Application Load Balancer?**

A: You can configure rules for each of the listeners on the load balancer. The rules include conditions and corresponding actions if the conditions are satisfied. The supported conditions are Host header, path, HTTP headers, methods, query parameters, and source IP classless inter-domain routing (CIDR). The supported actions are redirect, fixed response, authenticate, and forward. Once you have set this up, the load balancer will use the rules to determine how a particular HTTP request should be routed. You can use multiple conditions and actions in a rule, and in each condition can specify a match on multiple values.

**Q: Are there limits on the resources for an Application Load Balancer?**

A: Your AWS account has these [limits](http://docs.aws.amazon.com/elasticloadbalancing/latest/application/load-balancer-limits.html) for an Application Load Balancer.

**Q: How can I protect my web applications behind a load balancer from web attacks?**

A: You can integrate your Application Load Balancer with AWS Web Application Firewall (WAF), a web application firewall that helps protect web applications from attacks by allowing you to configure rules based on IP addresses, HTTP headers, and custom uniform resource identifier (URI) strings. Using these rules, AWS WAF can block, allow, or monitor (count) web requests for your web application. Please see AWS WAF developer guide for more information.

**Q: Can I load balance to any arbitrary IP address?**

A: You can use any IP address from the load balancer’s VPC CIDR for targets within load balancer’s VPC, and any IP address from RFC 1918 ranges (10.0.0.0/8, 172.16.0.0/12, and 192.168.0.0/16) or RFC 6598 range (100.64.0.0/10) for targets located outside the load balancer’s VPC (for example, targets in Peered VPC, Amazon EC2 Classic, and on-premises locations reachable over AWS Direct Connect or VPN connection).

**Q: How can I load balance applications distributed across a VPC and on-premises location?**

A: There are various ways to achieve hybrid load balancing. If an application runs on targets distributed between a VPC and an on-premises location, you can add them to the same target group using their IP addresses. To migrate to AWS without impacting your application, gradually add VPC targets to the target group and remove on-premises targets from the target group. 

If you have two different applications such that the targets for one application are in a VPC and the targets for other applications are in on-premises location, you can put the VPC targets in one target group and the on-premises targets in another target group and use content based routing to route traffic to each target group. You can also use separate load balancers for VPC and on-premises targets and use DNS weighting to achieve weighted load balancing between VPC and on-premises targets.

**Q: How can I load balance to EC2-Classic instances?**

A: You cannot load balance to EC2-Classic Instances when registering their Instance IDs as targets. However if you link these EC2-Classic instances to the load balancer's VPC using ClassicLink and use the private IPs of these EC2-Classic instances as targets, then you can load balance to the EC2-Classic instances. If you are using EC2 Classic instances today with a Classic Load Balancer, you can easily migrate to an Application Load Balancer.

**Q: How do I enable cross-zone load balancing in Application Load Balancer?**

A: Cross-zone load balancing is already enabled by default in Application Load Balancer.

**Q: When should I authenticate users using the Application Load Balancer’s integration with Amazon Cognito vs. the Application Load Balancers’ native support for OpenID Connect (IODC) identity providers (IdPs)?**

A: You should use authentication through Amazon Cognito if:

- You want to provide flexibility to your users to authenticate via social network identities (Google, Facebook, and Amazon) or enterprise identities (SAML) or via your own user directories provided by Amazon Cognito’s User Pool.
- You are managing multiple identity providers including OpenID Connect and want to create a single authentication rule in Application Load Balancer (ALB) that can use Amazon Cognito to federate your multiple identity providers.
- You need to actively manage user profiles with one or more social or OpenID Connect identity providers from one central place. For example, you can put users in groups and add custom attributes to represent user status and control access for paid users.

Alternatively, if you have invested in developing custom IdP solutions and simply want to authenticate with a single OpenID Connect-compatible identity provider, you may prefer using Application Load Balancer’s native OIDC solution.  

**Q: What type of redirects does Application Load Balancer support?**

A: The following three types of redirects are supported.

| Types of redirects | Examples |
| --- | --- |
| HTTP to HTTP | http://hostA to http://hostB |
| HTTP to HTTPS |     
http://hostA to https://hostB  
https://hostA:portA/pathA to https://hostB:portB/pathB

 |  
| HTTPS to HTTPS | https://hostA to https://hostB |

**Q: What content types does ALB support for the message body of fixed-response action?**

A: The following content types are supported: text/plain, text/css, text/html, application/javascript, application/json.

**Q: How does AWS Lambda invocation via Application Load Balancer work?**  

A: HTTP(S) requests received by a load balancer are processed by the content-based routing rules. If the request content matches the rule—with an action to forward it to a target group through a Lambda function as a target—then the corresponding Lambda function is invoked. The content of the request (including headers and body) is passed on to the Lambda function in JavaScript object notation (JSON) format. The response from the Lambda function should be in JSON format. The response from the Lambda function is transformed into an HTTP response and sent to the client. The load balancer invokes your Lambda function using the AWS Lambda Invoke API, and requires that you provide invoke permissions for your Lambda function to the Elastic Load Balancing service.

**Q: Does Lambda invocation via Application Load Balancer support requests over both HTTP and HTTPS protocol?**

A: Yes. Application Load Balancer supports Lambda invocation for requests over both HTTP and HTTPS protocol.

**Q: In which AWS Regions can I use Lambda functions as targets with the Application Load Balancer?**

A: You can use Lambda as a target with the Application Load Balancer in US East (N. Virginia), US East (Ohio), US West (Northern California), US West (Oregon), Asia Pacific (Mumbai), Asia Pacific (Seoul), Asia Pacific (Singapore), Asia Pacific (Sydney), Asia Pacific (Tokyo), Canada ( Central), EU (Frankfurt), EU (Ireland), EU (London), EU (Paris), South America (São Paulo), and GovCloud (US-West) AWS Regions.

**Q: Is the Application Load Balancer available in AWS Local Zones?**  

A: Yes, Application Load Balancer is available in the Local Zone in Los Angeles. Within the Los Angeles Local Zone, Application Load Balancer will operate in a single subnet and scale automatically to meet varying levels of application load without manual intervention.

Application Load Balancer Pricing FAQs

**Q: How does Application Load Balancer pricing work?**

A: You are charged for each hour or partial hour that an Application Load Balancer is running and the number of Load Balancer Capacity Units (LCU) used per hour.

**Q: What is a Load Balancer Capacity Unit (LCU)?**

A: An LCU is a new metric for determining how you pay for an Application Load Balancer. An LCU defines the maximum resource consumed in any one of the dimensions (new connections, active connections, bandwidth and rule evaluations) the Application Load Balancer processes your traffic.

**Q: Will I be billed on Classic Load Balancers by LCU?**

A: No, Classic Load Balancers will continue to be billed for bandwidth and hourly usage.

**Q: How do I know the number of LCUs an Application Load Balancer is using?**

A: We expose the usage of all four dimensions that constitute an LCU via Amazon CloudWatch.

**Q: Will I be billed on all the dimensions in an LCU?**

A: No. The number of LCUs per hour will be determined based on maximum resource consumed amongst the four dimensions that constitutes a LCU.

**Q: Will I be billed on partial LCUs?**

A: Yes.

**Q: Is a free tier offered on an Application Load Balancer for new AWS accounts?**

A: Yes. For new AWS accounts, a free tier for an Application Load Balancer offers 750 hours and 15 LCUs. This free tier offer is only available to new AWS customers, and is available for 12 months following your AWS sign-up date.

**Q: Can I use a combination of Application Load Balancer and Classic Load Balancer as part of my free tier?**

A: Yes. You can use both Classic and Application Load Balancers for 15 GB and 15 LCUs respectively. The 750 load balancer hours are shared between both Classic and Application Load Balancers.

**Q: What are rule evaluations?**

A: Rule evaluations are defined as the product of number of rules processed and the request rate averaged over an hour.

**Q: How does the LCU billing work with different certificate types and key sizes?**

A: Certificate key size affects only the number of new connections per second in the LCU computation for billing. The following table lists the value of this dimension for different key sizes for RSA and ECDSA certificates.

| RSA certificates |   |   |   |   |
| --- | --- | --- | --- | --- |
| **Key Size** | **<=2K**  | **<=4K**  | **<=8K**  | **\>8K**  |
| New connections/sec | 25 | 5 | 1 | 0.25 |

| **ECDSA Certificates** |   |   |   |   |
| --- | --- | --- | --- | --- |
| **Key Size**  | **<=256** | **<=384** | **<=521** | **\>521**  |
| New connections/sec | 25 | 5 | 1 | 0.25 |

**Q: Am I charged for regional AWS data transfer when enabling cross-zone load balancing in Application Load Balancer?**  

A: No. Since cross-zone load balancing is always on with Application Load Balancer, you are not charged for this type of regional data transfer.

**Q: Is user authentication in Application Load Balancer charged separately?**

A: No. There is no separate charge for enabling the authentication functionality in Application Load Balancer. When using Amazon Cognito with Application Load Balancer, Amazon Cognito pricing will apply.

**Q: How do you charge for Application Load Balancer usage with AWS Lambda targets?**

A: You are charged as usual for each hour or partial hour that an Application Load Balancer is running and the number of Load Balancer Capacity Units (LCU) used per hour. For Lambda targets, each LCU offers 0.4 GB processed bytes per hour, 25 new connections per second, 3,000 active connections per minute, and 1,000 rule evaluations per second. For the processed bytes dimension, each LCU provides 0.4 GB per hour for Lambda targets versus 1 GB per hour for all other target types like Amazon EC2 instances, containers, and IP addresses. Please note that usual AWS Lambda charges apply to Lambda invocations by Application Load Balancer.

**Q: How can I differentiate the bytes processed by Lambda targets versus bytes processed by other targets (Amazon EC2, containers, and on-premises servers)?**

A: Applications Load Balancers emit two new CloudWatch metrics. LambdaTargetProcessedBytes metric indicates the bytes processed by Lambda targets, and the StandardProcessedBytes metric indicates bytes processed by all other target types.  

## Network Load Balancer

**Q: Can I create a TCP or UDP (Layer 4) listener for my Network Load Balancer?**

A: Yes. Network Load Balancers support both TCP, UDP, and TCP+UDP (Layer 4) listeners, as well as TLS listeners.  

**Q: What are the key features available with the Network Load Balancer?**

A: Network Load Balancer provides both TCP and UDP (Layer 4) load balancing. It is architected to handle millions of requests per second and sudden volatile traffic patterns, and provides extremely low latencies. In addition, Network Load Balancer also supports TLS termination, preserves the source IP of the clients, and provides stable IP support and zonal isolation. It also supports long-running connections that are useful for WebSocket type applications.

**Q: Can Network Load Balancer process both TCP and UDP protocol traffic on the same port?**

A: Yes. To achieve this, you can use a TCP+UDP listener. For example, for a DNS service using both TCP and UDP, you can create a TCP+UDP listener on port 53, and the load balancer will process traffic for both UDP and TCP requests on that port. You must associate a TCP+UDP listener with a TCP+UDP target group.  

**Q: How does Network Load Balancer compare to what I get with the TCP listener on a Classic Load Balancer?**

A: Network Load Balancer preserves the source IP of the client, which is not preserved in the Classic Load Balancer. Customers can use proxy protocol with Classic Load Balancer to get the source IP. Network Load Balancer automatically provides a static IP per Availability Zone (AZ) to the load balancer and also enables assigning an Elastic IP to the load balancer per AZ. This is not supported with Classic Load Balancer.

**Q: Can I migrate to Network Load Balancer from Classic Load Balancer?**

A: Yes. You can migrate to Network Load Balancer from Classic Load Balancer using one of the options listed in this document.

**Q: Are there limits on the resources for my Network Load Balancer?**

A: Yes, please refer to Network Load Balancer limits documentation for more information.

**Q: Can I use the AWS Management Console to set up my Network Load Balancer?**

A: Yes, you can use the AWS Management Console, AWS CLI, or the API to set up a Network Load Balancer.

**Q: Can I use the existing API for Classic Load Balancers for my Network Load Balancers?**

A: No. To create a Classic Load Balancer, use the 2012-06-01 API. To create a Network Load Balancer or an Application Load Balancer, use the 2015-12-01 API.

**Q: Can I create my Network Load Balancer in a single Availability Zone?**

A: Yes, you can create your Network Load Balancer in a single AZ by providing a single subnet when you create the load balancer.

**Q: Does Network Load Balancer support DNS regional and zonal fail-over?**

A: Yes, you can use Amazon Route 53 health checking and DNS failover features to enhance the availability of the applications running behind Network Load Balancers. Using Route 53 DNS failover, you can run applications in multiple AWS Availability zones and designate alternate load balancers for failover across regions. 

In the event that you have your Network Load Balancer configured for multi-AZ, if there are no healthy Amazon EC2 instances registered with the load balancer for that AZ, or if the load balancer nodes in a given zone are unhealthy, then Route 53 will fail away to alternate load balancer nodes in other healthy AZs.

**Q: Can I have a Network Load Balancer with a mix of ELB-provided IPs and Elastic IPs or assigned private IPs?**

A: No. A Network Load Balancer’s addresses must be completely controlled by you, or completely controlled by ELB. This is to ensure that when using Elastic IPs with a Network Load Balancer, all addresses known to your clients do not change.

**Q: Can I assign more than one EIP to my Network Load Balancer in each subnet?**

A: No. For each associated subnet a Network Load Balancer is in, the Network Load Balancer can only support a single public/internet facing IP address.

**Q: If I remove/delete a Network Load Balancer what will happen to the Elastic IP addresses that were associated with it?**

A: The Elastic IP Addresses that were associated with your load balancer will return to your allocated pool and be available for future use.

**Q: Does Network Load Balancer support internal load balancers?**

A: Network Load Balancer can be set up as an internet-facing load balancer or an internal load balancer, similar to what is possible with Application Load Balancer and Classic Load Balancer.

**Q: Can the internal Network Load balancer support more than one private IP in each subnet?**

A: No. For each associated subnet that a load balancer is in, the Network Load Balancer can only support a single private IP.

**Q: Can I set up Websockets with my Network Load Balancer?**

A: Yes, configure TCP listeners that route the traffic to the targets that implement WebSockets protocol (https://tools.ietf.org/html/rfc6455 ). Because WebSockets is a layer 7 protocol and Network Load Balancer is operating at layer 4, no special handling exists in Network Load Balancer for WebSockets or other higher level protocols.

**Q: Can I load balance to any arbitrary IP address?**

A: Yes. You can use any IP address from the load balancer’s VPC CIDR for targets within load balancer’s VPC and any IP address from RFC 1918 ranges (10.0.0.0/8, 172.16.0.0/12, and 192.168.0.0/16) or RFC 6598 range (100.64.0.0/10) for targets located outside the load balancer’s VPC (EC2-Classic and on-premises locations reachable over AWS Direct Connect). Load balancing to IP address target type is supported for TCP listeners only, and is currently not supported for UDP listeners.

**Q: Can I use Network Load Balancer to setup AWS PrivateLink?**  

A: Yes, Network Load Balancers with TCP and TLS Listeners can be used to setup AWS PrivateLink. You cannot set up PrivateLink with UDP listeners on Network Load Balancers.

**Q: What is a UDP flow?**

A: While user datagram protocol (UDP) is connectionless, the load balancer maintains UDP flow state based on 5-tuple hash, ensuring that packets sent in the same context are consistently forwarded to the same target. The flow is considered active as long as traffic is flowing and until the idle timeout is reached. Once the timeout threshold is reached, the load balancer will forget the affinity, and the incoming UDP packet will be considered a new flow and load-balanced to a new target.

**Q: What is the idle timeout supported by Network Load Balancer?**

A: Network Load Balancer idle timeout for TCP connections is 350 seconds. The idle timeout for UDP flows is 120 seconds.

**Q: What is the benefit of targeting containers behind a load balancer with IP addresses instead of instance IDs?**  

A: Each container on an instance can now have its own security group, and does not need to share security rules with other containers. You can attach security groups to an ENI, and each ENI on an instance can have a different security group. You can map a container to the IP address of a particular ENI to associate security group(s) per container. Load balancing using IP addresses also allows multiple containers running on an instance use the same port (say port 80). The ability to use the same port across containers allows containers on an instance to communicate with each other through well-known ports instead of random ports.

**Q: How can I load balance applications distributed across a VPC and on-premises location?**

A: There are various ways to achieve hybrid load balancing. If an application runs on targets distributed between a VPC and an on-premises location, you can add them to the same target group using their IP addresses. To migrate to AWS without impacting your application, gradually add VPC targets to the target group and remove on-premises targets from the target group. You can also use separate load balancers for VPC and on-premises targets and use DNS weighting to achieve weighted load balancing between VPC and on-premises targets.

**Q: How can I load balance to EC2-Classic instances?**

A: You cannot load balance to EC2-Classic Instances when registering their Instance IDs as targets. However if you link these EC2-Classic instances to the load balancer's VPC using ClassicLink and use the private IPs of these EC2-Classic instances as targets, then you can load balance to the EC2-Classic instances. If you are using EC2 Classic instances today with a Classic Load Balancer, you can easily migrate to a Network Load Balancer.

**Q: How do I enable cross-zone load balancing in Network Load Balancer?**

A: You can enable cross-zone loading balancing only after creating your Network Load Balancer. You achieve this by editing the load balancing attributes section and then selecting the cross-zone load balancing support checkbox.

**Q: Am I charged for regional AWS data-transfer when I enable cross-zone load balancing in Network Load Balancer?**

A: Yes, you will be charged for regional data transfer between Availability Zones with Network Load Balancer when cross-zone load balancing is enabled. Check the charges in the data transfer section of the [Amazon EC2 On-Demand Pricing page](https://aws.amazon.com/ec2/pricing/on-demand/).

**Q: Is there any impact of cross-zone load balancing on Network Load Balancer limits?**

A: Yes. Network Load Balancer currently supports 200 targets per Availability Zone. For example, if you are in two AZs, you can have up to 400 targets registered with Network Load Balancer. If cross-zone load balancing is on, then the maximum targets reduce from 200 per AZ to 200 per load balancer. So, in the example above: When cross-zone load balancing is on, even though your load balancer is in two AZs, you are limited to 200 targets that can be registered to the load balancer.

**Q: Does Network Load Balancer support TLS termination?**

A: Yes, you can terminate TLS connections on the Network Load Balancer. You must install an SSL certificate on your load balancer. The load balancer uses this certificate to terminate the connection and then decrypt requests from clients before sending them to targets.

**Q: Is source IP is preserved when terminating TLS on Network Load Balancer?**

A: Source IP continues to be preserved even if you terminate TLS on the Network Load Balancer.

**Q: What are the steps to get a SSL certificate?**

A: You can either use [AWS Certificate Manager](https://aws.amazon.com/certificate-manager/) to provision an SSL/TLS certificate, or you can obtain the certificate from other sources by creating the certificate request, getting the certificate request signed by a certificate authority (CA), and then uploading the certificate either using AWS Certification Manager (ACM) or the [AWS Identity and Access Management](https://aws.amazon.com/iam/) (IAM) service.

**Q: How can I enable Server Name Indication (SNI) for my Network Load Balancer?**

A: SNI is automatically enabled when you associate more than one TLS certificate with the same secure listener on a load balancer. Similarly, SNI mode for a secure listener is automatically disabled when you have only one certificate associated to a secure listener.

**Q: How does the Network Load Balancer integrate with AWS Certificate Manager (ACM) or Identity Access Manager (IAM)?**

A: Network Load Balancer is integrated with AWS Certificate Management (ACM). Integration with ACM makes it very simple to bind a certificate to the load balancer thereby making the entire SSL offload process very easy. Purchasing, uploading, and renewing SSL/TLS certificates is a time-consuming manual and complex process. With ACM integration with Network Load Balancer, this whole process has been shortened to simply requesting a trusted SSL/TLS certificate and selecting the ACM certificate to provision it with the load balancer. Once you create a Network Load balancer, you can now configure a TLS listener followed by an option to select a certificate from either ACM or Identity Access Manager (IAM). This experience is similar to what you have in Application Load Balancer or Classic Load Balancer.

**Q: Is back-end server authentication supported with Network Load Balancer?**

A: No, only encryption is supported to the back-ends with Network Load Balancer.

**Q: What are the certificate types supported by Network Load Balancer?**

A: Network Load Balancer only supports RSA certificates with 2K key size. We currently do not support RSA certificate key sizes greater than 2K or ECDSA certificates on the Network Load Balancer.

**Q: In which AWS Regions is TLS Termination on Network Load Balancer supported?**

A: You can use TLS Termination on Network Load Balancer in US East (N. Virginia), US East (Ohio), US West (Northern California), US West (Oregon), Asia Pacific (Mumbai), Asia Pacific (Seoul), Asia Pacific (Singapore), Asia Pacific (Sydney), Asia Pacific (Tokyo), Canada (Central), EU (Frankfurt), EU (Ireland), EU (London), EU (Paris), South America (São Paulo), and GovCloud (US-West) AWS Regions.

Network Load Balancer Pricing FAQs

**Q: How does Network Load Balancer pricing work?**

A: You are charged for each hour or partial hour that a Network Load Balancer is running and the number of Load Balancer Capacity Units (LCU) used by Network Load Balancer per hour.

**Q: What is a Load Balancer Capacity Unit (LCU)?**

A: An LCU is a new metric for determining how you pay for a Network Load Balancer. An LCU defines the maximum resource consumed in any one of the dimensions (new connections/flows, active connections/flows, and bandwidth) the Network Load Balancer processes your traffic.

**Q: What are the LCU metrics for TCP traffic on Network Load Balancer?**

A: The LCU metrics for the TCP traffic are as follows:

- 800 new TCP connections per second.
- 100,000 active TCP connections (sampled per minute).
- 1 GB per hour for Amazon EC2 instances, containers, and IP addresses as targets.

**Q: What are the LCU metrics for UDP traffic on Network Load Balancer?**

A: The LCU metrics for the UDP traffic are as follows:

- 400 new flows per second.
- 50,000 active UDP flows (sampled per minute).
- 1 GB per hour for Amazon EC2 instances, containers, and IP addresses as targets.  
    

**Q: What are the LCU metrics for TLS traffic on Network Load Balancer?**

A: The LCU metrics for the TLS traffic are as follows:

- 50 new TLS connections per second.
- 3,000 active TLS connections (sampled per minute).
- 1 GB per hour for Amazon EC2 instances, containers, and IP addresses as targets.

**Q: Will I be billed on all the dimensions (Processed Bytes, New Flows and Active Flows)?**

A: No, for each protocol you are charged only on one of the three dimensions (the highest for the hour).  

**Q: Is new connections/flows per sec same as requests/sec?**

A: No. Multiple requests can be sent in a single connection.

**Q: Will I be billed on Classic Load Balancers by LCU?**

A: No. Classic Load Balancers will continue to be billed for bandwidth and hourly charge.

**Q: How do I know the number of LCUs a Network Load Balancer is using?**

A: We will expose the usage of all three dimensions that constitutes a LCU via Amazon CloudWatch.

**Q: Will I be billed on all the dimensions in an LCU?**

A: No. The number of LCUs per hour will be determined based on maximum resource consumed amongst the three dimensions that constitutes a LCU.

**Q: Will I be billed on partial LCUs?**

A: Yes.

**Q: Is a free tier offered on a Network Load Balancer for new AWS accounts?**

A: Yes. For new AWS accounts, a free tier for a Network Load Balancer offers 750 hours and 15 LCUs. This free tier offer is only available to new AWS customers, and is available for 12 months following your AWS sign-up date.

**Q: Can I use a combination of Network Load Balancer, Application Load Balancer and Classic Load Balancer as part of my free tier?**

A: Yes. You can use Application and Network each for 15 LCUs and Classic for 15 GB respectively. The 750 load balancer hours are shared between Application, Network, and Classic Load Balancers.

## Gateway Load Balancer

### Getting Started

**Q: When should I use Gateway Load Balancer, as opposed to Network Load Balancer or Application Load Balancer?**

A: You should use Gateway Load Balancer when deploying inline virtual appliances where network traffic is not destined for the Gateway Load Balancer itself. Gateway Load Balancer transparently passes all Layer 3 traffic through third-party virtual appliances, and is invisible to the source and destination of the traffic. For more details on how these load balancers compare, see the [features comparison](https://aws.amazon.com/elasticloadbalancing/features/#Product_comparisons) page.

**Q: Is Gateway Load Balancer deployed per Region or per Availability Zone (AZ)?**  

A: Gateway Load Balancer runs within one AZ.

**Q: What are the key features available with the Gateway Load Balancer?**

A: Gateway Load Balancer provides both Layer 3 gateway and Layer 4 load balancing capabilities. It is a transparent bump-in-the-wire device that does not change any part of the packet. It is architected to handle millions of requests/second, volatile traffic patterns, and introduces extremely low latency. See **Gateway Load Balancer** features in [this](https://aws.amazon.com/elasticloadbalancing/features/) table.   

**Q: Does Gateway Load Balancer perform TLS termination?**  

A: Gateway Load Balancer does not perform TLS termination and does not maintain any application state. These functions are performed by the third-party virtual appliances it directs traffic to, and receives traffic from.  

**Q: Does Gateway Load Balancer maintain application state?**

A: Gateway Load Balancer does not maintain application state, but it maintains flow stickiness to a specific appliance using 5-tuple (for TCP/UDP flows) or 3-tuple (for non-TCP/UDP flows).  

**Q: How does Gateway Load Balancer define a flow?**  

A: By default, Gateway Load Balancer defines a flow as a combination of a 5-tuple that comprises of Source IP, Destination IP, Protocol, Source Port, and Destination Port. Using the default 5-tuple hash, Gateway Load Balancer makes sure that both directions of a flow (i.e., source to destination, and destination to source) are consistently forwarded to the same target. The flow is considered active as long as traffic is flowing and until the idle timeout is reached. Once the timeout threshold is reached, the load balancer will forget the affinity, and incoming traffic packet will be considered as a new flow and may be load-balanced to a new target.  

Note that the default 5-tuple hash can affect TCP based applications that use separate streams or port numbers for control and data, such as FTP, Microsoft RDP, Windows RPC and SSL VPN. Control and data flows of such applications can land on different target appliances and can cause traffic disruption. If you want to support such protocols, you can enable GWLB flow stickiness using 3-tuple (source IP, destination IP, transport protocol) or 2-tuple (source IP, destination IP). Please see [flow stickiness documentation](https://docs.aws.amazon.com/elasticloadbalancing/latest/gateway/target-groups.html#flow-stickiness) for how to change flow stickiness type.

**Q: What is the idle timeout supported by Gateway Load Balancer?**

A: Gateway Load Balancer idle timeout for TCP connections is 350 seconds. The idle timeout for non-TCP flows is 120 seconds. These timeouts are fixed and cannot be changed.  

**Q: Can appliances fragment the packets?  
**

A: No. Target appliances of Gateway Load Balancer (GWLB) should not fragment packets they have received when sending them back to the GWLB. Fragments created by the appliance are dropped at Gateway Load Balancer because layer 4 header is not present in the IP fragments. To prevent fragmentation from happening on the appliance, we recommend enabling jumbo frame on your appliance or setting your appliance’s network interface to use the maximum desired MTU, thus achieving transparent forwarding behavior by keeping the original packet contents as is.

**Q: How does Gateway Load Balancer handle the failure of one virtual appliance instance in a single Availability Zone?**  

A: When a single virtual appliance instance fails, Gateway Load Balancer removes it from the routing list and reroutes traffic to a healthy appliance instance.

**Q: How does Gateway Load Balancer handle the failure of all virtual appliances within a single AZ?**  

A: If all virtual appliances within an Availability Zone fail, Gateway Load Balancer will drop the network traffic. We recommend deploying Gateway Load Balancers in multiple AZs for greater availability. If all appliances fail in one AZ, scripts can be used to either add new appliances, or direct traffic to a Gateway Load Balancer in a different AZ.  

**Q: Can I configure an appliance to be a target for more than one Gateway Load Balancer?**

A: Yes, multiple Gateway Load Balancers can point to same set of virtual appliances.  

**Q: What type of listener can I create for my Gateway Load Balancer?**

A: Gateway Load Balancer is a transparent bump-in-the-wire device and listens to all types of IP traffic (including TCP, UDP, ICMP, GRE, ESP and others). Hence only IP listener is created on a Gateway Load Balancer.  

**Q: Are there limits on the resources for my Gateway Load Balancer?**

A: Yes, please refer to Gateway Load Balancer [limits documentation](https://docs.aws.amazon.com/elasticloadbalancing/latest/gateway/quotas-limits.html) for more information.

**Q: Can I use the AWS Management Console to set up my Gateway Load Balancer?**

A: Yes, you can use the AWS Management Console, AWS CLI, or the API to set up a Gateway Load Balancer.

**Q: Can I create my Gateway Load Balancer in a single Availability Zone?**

A: Yes, you can create your Gateway Load Balancer in a single availability zone by providing a single subnet when you create the load balancer. However, we recommend using multiple availability zones for improved availability. You cannot add or remove availability zones for a Gateway Load Balancer after you create it.  
  
**Q: How do I enable cross-zone load balancing in Gateway Load Balancer?**

A: By default, cross-zone load balancing is disabled. You can enable cross-zone loading balancing only after creating your Gateway Load Balancer. You achieve this by editing the load balancing attributes section and then by selecting the cross-zone load balancing support checkbox.  
  
**Q: Am I charged for AWS data-transfer when I enable cross-zone load balancing in Gateway Load Balancer?**

A: Yes, you will be charged for data transfer between Availability Zones with Gateway Load Balancer when cross-zone load balancing is enabled. Check the charges in the data-transfer section at Amazon EC2 On-Demand Pricing page.  
  
**Q: Is there any impact of cross-zone load balancing on Gateway Load Balancer limits?**

A: Yes. Gateway Load Balancer currently supports 300 targets per Availability Zone. For example, if you created Gateway Load Balancer in 3 Availability-Zones, you can have up to 900 targets registered. If cross-zone load balancing is on, then the maximum number of targets reduces from 300 per Availability Zone to 300 per Gateway Load Balancer.  
  

### Gateway Load Balancer Pricing FAQs

**Q: How does Gateway Load Balancer pricing work?**

A: You are charged for each hour or partial hour that a Gateway Load Balancer is running and the number of Load Balancer Capacity Units (LCU) used by Gateway Load Balancer per hour.  

**Q: What is a Load Balancer Capacity Unit (LCU)?**

A: An LCU is an Elastic Load Balancing metric for determining how you pay for a Gateway Load Balancer. An LCU defines the maximum resource consumed in any one of the dimensions (new connections/flows, active connections/flows, and bandwidth) the Gateway Load Balancer processes your traffic.  

**Q: What is the LCU metrics for the Gateway Load Balancer?**

A: The LCU metrics for the TCP traffic is as follows:

- 600 new flows (or connections) per second.
- 60,000 active flows (or connections) (sampled per minute).  
    
- 1 GB per hour for EC2 instances, containers and IP addresses as targets.

**Q: Will I be billed on all the dimensions (Processed Bytes, New Flows and Active Flows)?**  
  
A: No, you are charged only on one of the three dimensions (the highest for the hour).  
  

**Q: Is new flows (or connections) per second same as requests/sec?**

A: No. Multiple requests can be sent in a single connection.

**Q: How do I know the number of LCUs a Gateway Load Balancer is using?**

A: You can track usage of all three dimensions of a LCU via Amazon CloudWatch.

**Q: Will I be billed on partial LCUs?**

A: Yes.  

### Gateway Load Balancer Endpoints

**Q: Why do I need a Gateway Load Balancer Endpoint?**

In order to be valuable, virtual appliances need to introduce as little additional latency as possible, and traffic flowing to and from the virtual appliance must follow a secure connection. Gateway Load Balancer Endpoints create the secured, low-latency connections necessary to meet these requirements.  

**Q: How do Gateway Load Balancer Endpoints help with centralization?**

Using a Gateway Load Balancer Endpoint, appliances can reside in different AWS accounts and VPCs. This allows appliances to be centralized in one location for easier management and reduced operational overhead.  

**Q: How do Gateway Load Balancer Endpoints work?**

Gateway Load Balancer Endpoints are a new type of VPC endpoint that uses PrivateLink technology. As network traffic flows from a source (an Internet Gateway, a VPC, etc.) to the Gateway Load Balancer, and back, a Gateway Load Balancer Endpoint ensures private connectivity between the two. All traffic flows over the AWS network and data is never exposed to the internet, increasing both security and performance.

**Q: How are PrivateLink Interface endpoints different than Gateway Load Balancer Endpoints?**  

A PrivateLink Interface endpoint is paired with a Network Load Balancer (NLB) in order to distribute TCP and UDP traffic that is destined for the web applications. In contrast, Gateway Load Balancer Endpoints are used with Gateway Load Balancers to connect the source and destination of traffic. Traffic flows from the Gateway Load Balancer Endpoint to the Gateway Load Balancer, through the virtual appliances, and back to the destination over secured PrivateLink connections.  
  
**Q: How many Gateway Load Balancer Endpoints can I connect to one Gateway Load Balancer?**

Gateway Load Balancer Endpoint is a VPC Endpoint and there is no limit on how many VPC Endpoints can connect to a service that uses Gateway Load Balancer. However, we recommend connecting no more than 50 Gateway Load Balancer Endpoints per one Gateway Load Balancer to reduce the risk of broader impact in case of service failure.  

## Classic Load Balancer

**Q: Which operating systems does the Classic Load Balancer support?**

A: The Classic Load Balancer supports Amazon EC2 instances with any operating system currently supported by the Amazon EC2 service.

**Q: Which protocols does the Classic Load Balancer support?**

A: The Classic Load Balancer supports load balancing of applications using HTTP, HTTPS (Secure HTTP), SSL (Secure TCP) and TCP protocols.

**Q: What TCP ports can I load balance?**

A: You can perform load balancing for the following TCP ports:

- \[EC2-VPC\] 1-65535
- \[EC2-Classic\] 25, 80, 443, 465, 587, 1024-65535

**Q: Does the Classic Load Balancer support IPv6 traffic?**

A: Yes. Each Classic Load Balancer has an associated IPv4, IPv6, and dualstack (both IPv4 and IPv6) DNS name. IPv6 is not supported in VPC. You can use an Application Load Balancer for native IPv6 support in VPC.

**Q: Can I configure my Amazon EC2 instances to only accept traffic from Classic Load Balancers?**

A: Yes.

**Q: Can I configure a security group for the front-end of Classic Load Balancers?**

A: If you are using Amazon Virtual Private Cloud, you can configure security groups for the front end of your Classic Load Balancers.

**Q: Can I use a single Classic Load Balancer for handling HTTP and HTTPS requests?**

A: Yes, you can map HTTP port 80 and HTTPS port 443 to a single Classic Load Balancer.

**Q: How many connections will my load balanced Amazon EC2 instances need to accept from each Classic Load Balancer?**

A: Classic Load Balancers do not cap the number of connections that they can attempt to establish with your load balanced Amazon EC2 instances. You can expect this number to scale with the number of concurrent HTTP, HTTPS, or SSL requests or the number of concurrent TCP connections that the Classic load balancers receive.

**Q: Can I load balance Amazon EC2 instances launched using a Paid AMI?**

A: You can load balance Amazon EC2 instances launched using a paid AMI from [AWS Marketplace](https://aws.amazon.com/marketplace). However, Classic Load Balancers do not support instances launched using a paid AMI from [Amazon DevPay](http://aws.amazon.com/devpay/) site.

**Q: Can I use Classic Load Balancers in Amazon Virtual Private Cloud?**

A: Yes. See the Elastic Load Balancing [web page](https://aws.amazon.com/elasticloadbalancing/).

**Q: Can I get a history of Classic Load Balancer API calls made on my account for security analysis and operational troubleshooting purposes?**

A: Yes. To receive a history of Classic Load Balancer API calls made on your account, simply turn on CloudTrail in the AWS Management Console.

**Q: Do Classic Load Balancers support SSL termination?**

A: Yes, you can terminate SSL on Classic Load Balancers. You must install an SSL certificate on each load balancer. The load balancers use this certificate to terminate the connection and then decrypt requests from clients before sending them to the back-end instances.

**Q: What are the steps to get a SSL certificate?**

A: You can either use [AWS Certificate Manager](https://aws.amazon.com/certificate-manager/) to provision a SSL/TLS certificate or you can obtain the certificate from other sources by creating the certificate request, getting the certificate request signed by a CA, and then uploading the certificate using the AWS Identity and Access Management (IAM) service.

**Q: How do Classic Load Balancers integrate with AWS Certificate Manager (ACM)?**

A: Classic Load Balancers are now integrated with AWS Certificate Management (ACM). Integration with ACM makes it very simple to bind a certificate to each load balancer thereby making the entire SSL offload process very easy. Typically purchasing, uploading, and renewing SSL/TLS certificates is a time-consuming manual and complex process. With ACM integrated with Classic Load Balancers, this whole process has been shortened to simply requesting a trusted SSL/TLS certificate and selecting the ACM certificate to provision it with each load balancer.

**Q: How do I enable cross-zone load balancing in Classic Load Balancer?**

A: You can enable cross-zone load balancing using the console, the AWS CLI, or an AWS SDK. See Cross-Zone Load Balancing [documentation](https://docs.aws.amazon.com/elasticloadbalancing/latest/classic/enable-disable-crosszone-lb.html#enable-cross-zone) for more details.

**Q: Am I charged for regional AWS data-transfer when I enable cross-zone load balancing in Classic Load Balancer?**

A: No, you are not charged for regional data transfer between Availability Zones when you enable cross-zone load balancing for your Classic Load Balancer.