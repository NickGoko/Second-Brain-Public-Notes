---
tags:
  - cloud/aws
---

- Gateway Load Balancer <mark style="background: #BBFABBA6;">helps deploy, scale, and manage virtual appliances, such as firewalls, intrusion detection and prevention systems (IDS/IPS), and deep packet inspection systems.</mark>
- <mark style="background: #D2B3FFA6;">GWLB and its registered virtual appliance instances exchange application traffic using the GENEVE (Generic Network Virtualization Encapsulation) protocol on port 6081</mark>.
- <mark style="background: #BBFABBA6;">Operates at Layer 3 of the OSI model, the network layer.</mark>  
   transparently passes all Layer 3 traffic through third-party virtual appliances, and is invisible to the source and destination of the traffic.
- Combines a transparent network gateway (that is, a single entry and exit point for all traffic) and <mark style="background: #CACFD9A6;">distributes traffic while scaling the virtual appliances with the demand</mark>.
- Listens for all IP packets across all ports and forwards traffic to the target group that’s specified in the listener rule.
- Runs within one AZ and is recommended to be deployed in multiple AZs for greater availability. If all appliances fail in one AZ, scripts can be used to either add new appliances or direct traffic to a GWLB in a different AZ.
- <mark style="background: #CACFD9A6;">Cannot add or remove availability zones after the GWLB is created</mark>.
- Is architected to handle millions of requests/second, volatile traffic patterns, and introduces extremely low latency.
- <mark style="background: #CACFD9A6;">Does not perform TLS termination and does not maintain any application state</mark>.  
  These functions are performed by the third-party virtual appliances it directs traffic to and receives traffic from.
- maintains stickiness of flows to a specific target appliance using 5-tuple (TCP/UDP flows) or 3-tuple (for non-TCP/UDP flows).
- supports a maximum transmission unit (MTU) size of 8500 bytes.
- supports cross-zone load balancing, which is disabled by default. You pay charges for inter-AZ data transfer if enabled.

## Gateway Load Balancer Endpoint – GWLBE

- <mark style="background: #ADCCFFA6;">GWLB uses Gateway Load Balancer endpoints</mark> – GWLBE to exchange traffic across VPC boundaries securely.
- <mark style="background: #FFB86CA6;">A Gateway Load Balancer endpoint is a</mark> [VPC endpoint](https://jayendrapatil.com/aws-vpc-endpoints/) that provides private connectivity between virtual appliances in the service provider VPC and application servers in the service consumer VPC.
- One GWLB can be connected to many GWLBEs.
- GWLB is deployed in the same VPC as the virtual appliances.
- <mark style="background: #ADCCFFA6;">Virtual appliances are registered with a target group for the GWLB.</mark>
- Traffic to and from a GWLBE is configured using route tables.
- Traffic flows from the service consumer VPC over the GWLBE to the GWLB in the service provider VPC, and then returns to the service consumer VPC
- GWLBE and the application servers must be created in different subnets. This enables you to configure the GWLBE as the next hop in the route table for the application subnet.

## Gateway Load Balancer Flow

![AWS Gateway Load Balancer GWLB](https://jayendrapatil.com/wp-content/uploads/2022/07/AWS-Gateway-Load-Balancer-GWLB.png)

### Traffic from the Internet to the Application (blue arrows)

- Traffic enters the service consumer VPC through the internet gateway.
- Traffic is sent to the GWLBE, as a result of VPC ingress routing.
- Traffic is sent to the GWLB for inspection through the security appliance.
- Traffic is sent back to the GWLBE after inspection.
- Traffic is sent to the application servers (destination subnet).

### Traffic from the Application to the Internet (orange arrows):

- Traffic is sent to the Gateway Load Balancer endpoint due to the default route configured on the application server subnet.
- Traffic is sent to the GWLB for inspection through the security appliance.
- Traffic is sent back to the GWLBE after inspection.
- Traffic is sent to the internet gateway based on the route table configuration.
- Traffic is routed back to the internet.

## Gateway Load Balancer High Availability

![AWS Gateway Load Balancer HA](https://jayendrapatil.com/wp-content/uploads/2022/07/AWS_Gateway_Load_Balancer_HA.png)

## [AWS Gateway Load Balancer vs Network Firewall](https://jayendrapatil.com/aws-network-firewall-vs-gateway-load-balancer/)

![AWS Network Firewall vs Gateway Load Balancer](https://jayendrapatil.com/wp-content/uploads/2022/09/AWS-Network-Firewall-vs-Gateway-Load-Balancer.jpg)

## AWS Certification Exam Practice Questions

> - Questions are collected from Internet and the answers are marked as per my knowledge and understanding (which might differ with yours).
> - AWS services are updated everyday and both the answers and questions might be outdated soon, so research accordingly.
> - AWS exam questions are not updated to keep up the pace with AWS updates, so even if the underlying feature has changed the question might not be updated
> - Open to further feedback, discussion and correction.

## References

[AWS\_Gateway\_Load\_Balancer](https://docs.aws.amazon.com/elasticloadbalancing/latest/gateway/introduction.html)