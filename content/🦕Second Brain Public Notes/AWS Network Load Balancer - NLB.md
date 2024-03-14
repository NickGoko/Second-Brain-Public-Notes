---
tags:
  - cloud/aws
---


![[Pasted image 20240312093755.png]]
- Network Load Balancer – <mark style="background: #FFF3A3A6;">NLB operates at the connection level (Layer 4), routing connections to targets</mark> – EC2 instances, and containers based on IP protocol data.
- <mark style="background: #FFB86CA6;">NLB is suited for load balancing of TCP traffic</mark>
- <mark style="background: #FFF3A3A6;">NLB is capable of handling millions of requests per second while maintaining ultra-low latencies</mark> (~100 ms vs 400 ms for ALB)
- <mark style="background: #ADCCFFA6;">NLB is optimized to handle sudden and volatile traffic patterns while using a single static IP address per Availability Zone.</mark>
- <mark style="background: #FFB8EBA6;">NLB also supports TLS termination, preserves the source IP of the clients, and provides stable IP support and Zonal isolation.</mark>
- NLB supports long-running connections that are very useful for WebSocket-type applications.
- NLB is integrated with other AWS services such as [Auto Scaling](https://jayendrapatil.com/aws-auto-scaling/), [EC2 Container Service (ECS)](https://jayendrapatil.com/aws-ec2-container-service-ecs/), and [CloudFormation](https://jayendrapatil.com/aws-cloudformation/).
- NLB supports connections from clients over [VPC peering](https://jayendrapatil.com/aws-vpc-peering/), [AWS-managed VPN](https://jayendrapatil.com/aws-vpc-vpn-cloudhub/), and third-party VPN solutions.
- **For TCP traffic**,
    - <mark style="background: #CACFD9A6;">the load balancer selects a target using a</mark> **flow hash algorithm** <mark style="background: #FFF3A3A6;">based on the protocol, source IP address, source port, destination IP address, destination port, and TCP sequence number.</mark>
    - <mark style="background: #ABF7F7A6;">TCP connections from a client having different source ports and sequence numbers and can be routed to different targets.</mark>
    - Each individual TCP connection is routed to a single target for the life of the connection.
- **For UDP traffic**,
    - <mark style="background: #FFF3A3A6;">the load balancer selects a target using a flow hash algorithm based on the protocol, source IP address, source port, destination IP address, and destination port.</mark>
    - <mark style="background: #ABF7F7A6;">A UDP flow has the same source and destination, so it is consistently routed to a single target throughout its lifetime.</mark>
    - <mark style="background: #CACFD9A6;">Different UDP flows have different source IP addresses and ports, so they can be routed to different targets.</mark>
- back-end server authentication (MTLS) is not supported.


## Classic Load Balancer Vs Application Load Balancer Vs Network Load Balancer

Refer Blog Post @ [Classic Load Balancer vs Application Load Balancer vs Network Load Balancer](https://jayendrapatil.com/aws-classic-load-balancer-vs-application-load-balancer/)

## Network Load Balancer Features

### Connection-based Layer 4 Load Balancing

- Allows load balancing of both TCP and UDP traffic, routing connections to targets – EC2 instances, microservices, and containers.

### High Availability
- is highly available.
- <mark style="background: #ADCCFFA6;">accepts incoming traffic from clients and distributes this traffic across the targets within the same AZ (except for Cross-zone load balancing)</mark>.
- monitors the health of its registered targets and routes the traffic only to healthy targets
- if a health check fails and an unhealthy target is detected, it stops routing traffic to that target and reroutes traffic to remaining healthy targets.
- if configured with multiple AZs and if all the targets in a single AZ fail, it routes traffic to healthy targets in the other AZs

### Availability Zones
- can be used to route traffic across multiple Availability Zones.
- However, AZ must be enabled before the traffic is routed to that AZ.
- AZ can be enabled, even after the NLB creation.
- <mark style="background: #ABF7F7A6;">AZ once enabled, cannot be removed.</mark>
- <mark style="background: #ADCCFFA6;">Cross-zone load balancing works only for AZs enabled with NLB.</mark>

### High Throughput
- is designed to handle traffic as it grows and can load balance millions of requests/sec.
- can also handle sudden volatile traffic patterns.

### **Low Latency**
- offers extremely low latencies for latency-sensitive applications.

### Cross Zone Load Balancing
- enables cross-zone loading balancing only after creating the NLB
- is disabled, by default, and charges apply for inter-az traffic.
- only works for the AZs that are enabled on the AZ

### Sticky Sessions
- Sticky sessions (source IP affinity) are a mechanism to route requests from the same client to the same target.
- <mark style="background: #CACFD9A6;">Stickiness is defined at the target group level</mark>  
![[Pasted image 20240312102526.png]]  
![](https://i.imgur.com/FWdvOzW.png)

### Load Balancing Using IP Addresses as Targets
- <mark style="background: #ABF7F7A6;">allows load balancing of any application hosted in AWS or on-premises using IP addresses of the application backends as targets.</mark>
- allows load balancing to an application backend hosted on any IP address and any interface on an instance.
- ability to load balance across AWS and on-premises resources help migrate-to-cloud, burst-to-cloud or failover-to-cloud.
- applications hosted in on-premises locations can be used as targets over a [Direct Connect](https://jayendrapatil.com/aws-direct-connect-dx/) connection and EC2-Classic (using ClassicLink).  
![Uploading file...5j59x]()

### Preserve Source IP Address
- preserves client-side source IP allowing the back-end to see the client IP address.
- <mark style="background: #FFF3A3A6;">Target groups can be created with target type as instance ID or IP address.</mark>
    - If targets are registered by instance ID or ECS tasks, the source IP addresses of the clients are preserved and provided to the applications.
    - If targets are registered by IP address
        - for TCP & TLS, the source IP addresses are the private IP addresses of the load balancer nodes. Use Proxy Protocol.
        - for UDP & TCP\_UDP, it is enabled by default and the source IP addresses of the clients are preserved.

### **Static IP support**
- automatically provides a static IP per Availability Zone (subnet) that can be used by applications as the front-end IP of the load balancer.
- creates a network interface for each enabled AZ. Each load balancer node in the AZ uses this network interface to get a static IP address.
- Internet-facing load balancer can optionally associate one Elastic IP address per subnet.

### **Elastic IP support**
- an Elastic IP per Availability Zone (subnet) can also be assigned, optionally, thereby providing a fixed IP.

### **Health Checks**
- <mark style="background: #FFF3A3A6;">supports both network and application target health checks using HTTP, HTTPS, and TCP.</mark>
- Network-level health check
    - is based on the overall response of the underlying target (instance or a container) to normal traffic.
    - target is marked unavailable if it is slow or unable to respond to new connection requests
- Application-level health check
    - is based on a specific URL on a given target to test the application health deeper

### **DNS Fail-over**
- integrates with [Route 53](https://jayendrapatil.com/aws-route-53/)
- <mark style="background: #FF5582A6;">Route 53 will direct traffic to load balancer nodes in other AZs, if there are no healthy targets with NLB or if the NLB itself is unhealthy</mark>
- <mark style="background: #BBFABBA6;">if NLB is unresponsive, Route 53 will remove the unavailable load balancer IP address from service and direct traffic to an alternate Network Load Balancer in another region.</mark>

### Integration with AWS Services
- is integrated with other AWS services such as [Auto Scaling](https://jayendrapatil.com/aws-auto-scaling/), [EC2 Container Service (ECS)](https://jayendrapatil.com/aws-ec2-container-service-ecs/), [CloudFormation](https://jayendrapatil.com/aws-cloudformation/), CodeDeploy, and [AWS Config](https://jayendrapatil.com/aws-config/).

### Long-lived TCP Connections
- supports long-lived TCP connections ideal for WebSocket-type of applications

### Central API Support
- uses the same API as Application Load Balancer.
- enables you to work with target groups, health checks, and load balance across multiple ports on the same EC2 instance to support containerized applications.

### Robust Monitoring and Auditing
- integrated with CloudWatch to report Network Load Balancer metrics.
- CloudWatch provides metrics such as Active Flow count, Healthy Host Count, New Flow Count, Processed bytes, and more.
- integrated with CloudTrail to track API calls to the NLB

### Enhanced Logging
- Flow Logs feature helps record all requests sent to the load balancer.
- Flow Logs capture information about the IP traffic going to and from network interfaces in the VPC.
- Flow log data is stored using CloudWatch Logs.

### Zonal Isolation
- is designed for application architectures in a single zone.
- can be enabled in a single AZ to support architectures that require zonal isolation
- automatically fails-over to other healthy AZs, if something fails in an AZ
- it’s recommended to configure the load balancer and targets in multiple AZs for achieving high availability

### Zonal DNS Name

- supports DNS names for each of its nodes.
- by default, resolving the Regional NLB DNS name returns the IP address for all NLB nodes in all enabled AZs.
- can be used to determine the IP address of each node.
- useful to minimize latency and inter-az data transfer costs.

## Advantages over Classic Load Balancer

- <mark style="background: #ABF7F7A6;">Ability to handle volatile workloads and scale to millions of requests per second, without the need of pre-warming</mark>
- <mark style="background: #FFF3A3A6;">Support for static IP/Elastic IP addresses for the load balancer</mark>
- <mark style="background: #ABF7F7A6;">Support for registering targets by IP address, including targets outside the VPC (on-premises) for the load balancer.</mark>
- <mark style="background: #FFF3A3A6;">Support for routing requests to multiple applications on a single EC2 instance</mark>. A single instance or IP address can be registered with the same target group using multiple ports.
- <mark style="background: #FFF3A3A6;">Support for containerized applications. Using Dynamic port mapping, ECS can select an unused port when scheduling a task and register the task with a target group using this port.</mark>
- Support for monitoring the health of each service independently, as health checks are defined at the target group level and many CloudWatch metrics are reported at the target group level. Attaching a target group to an Auto Scaling group enables scaling each service dynamically based on demand

## Network Load Balancer Limitations
- <mark style="background: #FFB86CA6;">can’t associate Security Groups with NLBs</mark>
- <mark style="background: #ADCCFFA6;">can’t disable/remove an AZ once you enable it.</mark>
- <mark style="background: #FFF3A3A6;">can’t modify ENIs created by NLB in each AZ</mark>
- <mark style="background: #ABF7F7A6;">can’t change EIPs and Private IPs attached to the ENIs after NLB creation.</mark>
- <mark style="background: #CACFD9A6;">can’t register EC2 instances by instance ID for instances in another VPC even if VPC peering is done.</mark>

## Network Load Balancer with AWS PrivateLink
- Interface Endpoints can be used to create custom applications in VPC and configure them as an AWS PrivateLink-powered service (referred to as an _endpoint service_) exposed through a Network Load Balancer. The custom applications can be hosted within AWS or on-premises.

![](https://jayendrapatil.com/wp-content/uploads/2019/05/VPC-Interface-Endpoints.png)

## Network Load Balancer Pricing

- charged for each hour or partial hour that an NLB is running and the number of Load Balancer Capacity Units (LCU) used per hour.
- An LCU is a new metric for determining NLB pricing
- An LCU defines the maximum resource consumed in any one of the dimensions (new connections/flows, active connections/flows, bandwidth and rule evaluations) the Network Load Balancer processes your traffic.

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
    
2. A company is hosting an application in AWS for third party access. The third party needs to <mark style="background: #ABF7F7A6;">whitelist the application based on the IP</mark>. Which AWS service can the company use in the whitelisting of the IP address?
    1. AWS Application Load Balancer
    2. AWS Classic Load balancer
    3. **AWS Network Load Balancer**
    4. AWS Route 53

## References

AWS Documentation – [ELB\_Network\_Load\_Balancer](https://docs.aws.amazon.com/elasticloadbalancing/latest/network/introduction.html)