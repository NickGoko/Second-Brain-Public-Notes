---
tags:
  - cloud/aws
---


https://aws.amazon.com/directconnect/


![[Module 7 - Connecting Networks#Connecting to Your Remote Network with AWS Direct Connect]]


## AWS Direct Connect Resiliency Recommendations
[Using AWS Direct Connect for High Resiliency](#)  
Amazon Web Services (AWS) offers customers the ability to achieve highly resilient network connections between Amazon Virtual Private Cloud (Amazon VPC) and their on-premises infrastructure. This capability extends customer access to AWS resources in a reliable, scalable, and cost-effective way. This page documents our best practices for ensuring high resiliency with AWS Direct Connect.

### Recommended Best Practices
Highly resilient, fault-tolerant network connections are key to a well-architected system. AWS recommends connecting from multiple data centers for physical location redundancy. When designing remote connections, consider using redundant hardware and telecommunications providers. Additionally, it is a best practice to use dynamically routed, active/active connections for automatic load balancing and failover across redundant network connections. Provision sufficient network capacity to ensure that the failure of one network connection does not overwhelm and degrade redundant connections.

#### High Resiliency for Critical Workloads
![](https://i.imgur.com/j87IPTZ.png)  
For critical production workloads that require high resiliency, it is recommended to have one connection at multiple locations. As shown in the figure above, such a topology ensures resilience to connectivity failure due to a fiber cut or a device failure as well as a complete location failure. You can use [AWS Direct Connect gateway](https://docs.aws.amazon.com/directconnect/latest/UserGuide/direct-connect-gateways.html) to access any AWS Region (except AWS Regions in China) from any AWS Direct Connect location.

#### Maximum Resiliency for Critical Workloads
![](https://i.imgur.com/TONBFpy.png)

Maximum resilience is achieved by separate connections terminating on separate devices in more than one location. This configuration offers customers maximum resilience to failure. As shown in the figure above, such a topology provides resilience to device failure, connectivity failure, and complete location failure. You can use [AWS Direct Connect gateway](https://docs.aws.amazon.com/directconnect/latest/UserGuide/direct-connect-gateways.html) to access any AWS Region (except AWS Regions in China) from any AWS Direct Connect locations.

#### Non-Critical Production Workloads or Development Workloads
![](https://i.imgur.com/p7TgHT2.png)  
<mark style="background: #CACFD9A6;">For non-critical production workloads and development workloads that do not require high resiliency, it is recommended to have at least two connections terminating on different devices at a single location.</mark> As shown in the figure above, such a topology helps in the case of the device failure at a location but does not help in the event of a total location failure.

#### Multi-Region Resiliency
For additional resiliency, customers can also explore the use of multi-region failover. This can be done using Transit Gateway Cross Region peering and Direct Connect Gateway. One such implementation is explained in this [blog](https://aws.amazon.com/blogs/networking-and-content-delivery/influencing-traffic-over-hybrid-networks-using-longest-prefix-match/).
#### AWS Site-to-Site VPN Connections as a Backup for the Direct Connect
Some AWS customers would like the benefits of one or more AWS Direct Connect connections for their primary connectivity to AWS, coupled with a lower-cost backup connection. To achieve this objective, they can establish AWS Direct Connect connections with a VPN backup.

It is important to understand that AWS Site to Site VPN supports up to 1.25 Gbps throughput per VPN tunnel and does not support Equal Cost Multi Path (ECMP) for egress data path in the case of multiple AWS Site to Site VPN tunnels terminating on the same VGW. Thus, we do not recommend customers use AWS Site to Site VPN as a backup for AWS Direct Connect connections with speeds greater than 1 Gbps.    
  
For additional resiliency, AWS customers can consider using AWS Site to Site VPN terminating on an AWS Transit Gateway as a back up to their AWS Direct Connect connections. Using AWS Site to Site VPN with Transit Gateway, you can ECMP traffic across multiple VPN tunnels to achieve up to 50Gbps. It is important to note that single VPN tunnel bandwidth is still limited to 1.25 Gbps.


#### Recommendation for AWS Direct Connect Partner Selection
[AWS Direct Connect Partners](https://aws.amazon.com/directconnect/partners/) help customers establish network connectivity between AWS Direct Connect locations and their data centers, offices or colocation environments. When selecting AWS Direct Connect Partners, consider a dual-vendor approach, if financially feasible, to ensure private-network diversity. When planning your connectivity, work with your selected Partner(s) to determine which of the above best practices are right for your needs, and learn how your selected Partner(s) can enable you to achieve them.

#### Summary
AWS recommends customers use multiple dynamically routed, rather than statically routed, connections to AWS at multiple AWS Direct Connect locations. This will allow remote connections to fail over automatically. Dynamic routing also enables remote connections to automatically leverage available preferred routes, if applicable, to the on-premises network. 

Highly resilient connections require redundant hardware, even when connecting from the same physical location. Avoid relying on a single on-premises device connecting to a single AWS Direct Connect device. 

Consider using AWS Site to Site VPN terminating on an AWS Transit Gateway as a backup for your mission critical workloads. You can also consider multi-region failover with Transit Gateway Cross Region Peering and Direct Connect Gateway.


AWS Direct Connect is a network service that provides an alternative to using the Internet to connect a customer’s on-premises sites to AWS.

Data is transmitted through a private network connection between AWS and a customer’s datacenter or corporate network.

Benefits:
- Reduce cost when using large volumes of traffic.
- Increase reliability (predictable performance).
- Increase bandwidth (predictable bandwidth).
- Decrease latency.

Each AWS Direct Connect connection can be configured with one or more virtual interfaces (VIFs).

Public VIFs allow access to public services such as S3, EC2, and DynamoDB.

Private VIFs allow access to your VPC.

Must use public IP addresses on public VIFs.

Must use private IP addresses on private VIFs.

Cannot do layer 2 over Direct Connect (L3 only).

From Direct Connect you can connect to all AZs **within the region.**

You can establish IPSec connections over public VIFs to remote regions.

Route propagation can be used to send customer side routes to the VPC.

You can only have one 0.0.0.0/0 (all IP addresses) entry per route table.

You can bind multiple ports for higher bandwidth.

Virtual interfaces are configured to connect to either AWS public services (e.g. EC2/S3) or private services (e.g. VPC based resources).

The diagram below shoes the components of AWS Direct Connect:

![AWS Direct Connect Components](https://digitalcloud.training/wp-content/uploads/2022/01/aws-direct-connect-components.jpeg)

- <mark style="background: #FFF3A3A6;">Direct Connect is charged by port hours and data transfer.</mark>
- Available in 1 Gbps, 10 Gbps, and 100 Gbps (limited Regions).  
	Speeds of 50 Mbps, 100 Mbps, 200 Mbps, 300 Mbps, 400 Mbps, and 500 Mbps can be purchased through AWS Direct Connect Partners (APN Partners).

Uses 802.1q VLANs.

Each connection consists of a single dedicated connection between ports on the customer router and an Amazon router.

for HA you must have 2x DX connections – can be active/active or active/standby.

Route tables need to be updated to point to a Direct Connect connection.

VPN can be maintained as a backup with a higher BGP priority.

Recommended to enable Bidirectional Forwarding Detection (BFD) for faster detection and failover.

You cannot extend your on-premises VLANs into the AWS cloud using Direct Connect.

Can aggregate up to 4 Direct Connect ports into a single connection using Link Aggregation Groups (LAG).

AWS Direct Connect supports both single (IPv4) and dual stack (IPv4/IPv6) configurations on public and private VIFs.

Technical requirements for connecting virtual interfaces:

- A public or private ASN. If you are using a public ASN you must own it. If you are using a private ASN, it must be in the 64512 to 65535 range.
- A new unused VLAN tag that you select.
- Private Connection (VPC) – The VPC Virtual Private Gateway (VGW) ID.
- Public Connection – Public IPs (/30) allocated by you for the BGP session.

AWS Direct Connect does not offer encryption.

You can encrypting data sent over DX by establishing a VPN tunnel over the DX connection.

- Running an AWS VPN connection over a DX connection provides consistent levels of throughput and encryption algorithms that protect your data.
- Though a private VIF is typically used to connect to a VPC, in the case of running an IPSec VPN over the top of a DX connection it is necessary to use a public VIF.

## AWS Direct Connect Gateway

Grouping of Virtual Private Gateways (VGWs) and Private Virtual Interfaces (VIFs) that belong to the same AWS account.

Direct Connect Gateway enables you to interface with VPCs in any AWS Region (except AWS China Region).

You associate an _AWS Direct Connect gateway_ with either of the following gateways:

- A transit gateway when you have multiple VPCs in the same Region.
- A virtual private gateway.

Can share private virtual interface to interface with more than one Virtual Private Clouds (VPCs) reducing the number of BGP sessions.

A Direct Connect gateway is a globally available resource.

You can create the Direct Connect gateway in any public Region and access it from all other public Regions.

The diagram below depicts the components of an AWS Direct Connect Gateway configuration:

![AWS Direct Connect Gateway](https://digitalcloud.training/wp-content/uploads/2022/01/aws-direct-connect-gateway.jpeg)

# FAQ
## General Questions

**Q: What is AWS Direct Connect?**

AWS Direct Connect is a networking service that provides an alternative to using the internet to connect to AWS. Using AWS Direct Connect, data that would have previously been transported over the internet is delivered through a private network connection between your facilities and AWS. In many circumstances, private network connections can reduce costs, increase bandwidth, and provide a more consistent network experience than internet-based connections. All AWS services, including Amazon Elastic Compute Cloud (EC2), Amazon Virtual Private Cloud (VPC), Amazon Simple Storage Service (S3), and Amazon DynamoDB can be used with AWS Direct Connect.

**Q: Where is AWS Direct Connect available?**  

A complete list of AWS Direct Connect locations is available on the AWS Direct Connect [locations](https://aws.amazon.com/directconnect/locations/) page. When using AWS Direct Connect, you can connect to VPCs deployed in any AWS Region and Availability Zone. You can also connect to AWS Local Zones.

**Q: What is the difference between dedicated and hosted connections?**

A dedicated connection is made through a 1 Gbps, 10 Gbps, or 100 Gbps Ethernet port dedicated to a single customer. Hosted connections are sourced from a AWS Direct Connect Partner that has a network link between themselves and AWS. 

**Q: How can I get started with AWS Direct Connect?**

Use the [AWS Direct Connect tab](https://console.aws.amazon.com/directconnect/v2/home) on the AWS Management Console to create a new connection. When requesting a connection, you will be asked to select a AWS Direct Connect location, the number of ports, and the port speed. You work with a [Direct Connect Partner](https://aws.amazon.com/directconnect/partners/) if you need assistance extending your office or data center network to a AWS Direct Connect location.

**Q: Can I use AWS Direct Connect if my network is not present at an AWS Direct Connect location?**

Yes. AWS Direct Connect Partners can help you extend your preexisting data center or office network to a AWS Direct Connect location. Please see [AWS Direct Connect Partners](https://aws.amazon.com/directconnect/partners/) for more information. With AWS Direct Connect Gateway, you can access any AWS Region from any AWS Direct Connect Location (excluding China).

**Q: Does AWS act as my "first mile" or "last mile" provider to connect my on-premises locations to AWS?**

No, you need to make connections between the local service providers used at your on-premises locations, or work with an AWS Direct Connect Delivery Partner, to connect to AWS Direct Connect locations.

**Q: How do I request a cross connect at an AWS Direct Connect location?**  

After you have downloaded your Letter of Authorization and Connecting Facility Assignment (LOA-CFA), you must complete your cross-network connection. If you already have equipment located in an AWS Direct Connect location, contact the appropriate provider to complete the cross connect. For specific instructions for each provider and cross connect pricing, refer to the AWS Direct Connect documentation: [Requesting cross connects](https://docs.aws.amazon.com/directconnect/latest/UserGuide/Colocation.html) at [AWS Direct Connect locations](https://aws.amazon.com/directconnect/locations/).

## Definitions

**Q: What is an AWS Direct Connect gateway?**

An AWS Direct Connect gateway is a grouping of virtual private gateways (VGWs) and private virtual interfaces (VIFs). An AWS Direct Connect gateway is a globally available resource. You can create the AWS Direct Connect gateway in any Region and access it from all other Regions.

**Q: What is a virtual interface (VIF)?**

A virtual interface (VIF) is necessary to access AWS services, and is either public or private. A public virtual interface enables access to public services, such as Amazon S3. A private virtual interface enables access to your VPC. For more information, see [AWS Direct Connect virtual interfaces](https://docs.aws.amazon.com/directconnect/latest/UserGuide/WorkingWithVirtualInterfaces.html).

**Q: What is a virtual private gateway (VGW)?**

A virtual private gateway (VGW) is part of a VPC that provides edge routing for AWS managed VPN connections and AWS Direct Connect connections. You associate an AWS Direct Connect gateway with the virtual private gateway for the VPC. For more details, refer to this [documentation](https://docs.aws.amazon.com/directconnect/latest/UserGuide/virtualgateways.html).

**Q: What is a link aggregation group (LAG)?**

A link aggregation group (LAG) is a logical interface that uses the link aggregation control protocol (LACP) to aggregate multiple dedicated connections at a single AWS Direct Connect endpoint, allowing you to treat them as a single, managed connection. LAGs streamline configuration because the LAG configuration applies to all connections in the group. For details on creating, updating, associating/disassociating, and deleting a LAG refer to the AWS Direct Connect documentation: [Link aggregation groups - AWS Direct Connect](https://docs.aws.amazon.com/directconnect/latest/UserGuide/lags.html).

- There is no extra charge for using a LAG.
- Dynamic LACP bundles are used; static LACP bundles are not supported.
- VIFs on two different LAGs can be connected to the same VGW. To improve failover times between paths when using multiple LAGs, bidirectional forwarding detection (BFD) is supported.

**Q: What is the AWS Direct Connect Resiliency Toolkit?**

The AWS Direct Connect Resiliency Toolkit provides a connection wizard that helps you choose between multiple resiliency models. These models help you to determine—then place an order for—the number of dedicated connections to achieve your SLA objective. You select a resiliency model, and then the AWS Direct Connect Resiliency Toolkit guides you through the dedicated connection ordering process. The resiliency models are designed to ensure that you have the appropriate number of dedicated connections in multiple locations.

**Q: What is the AWS Direct Connect Failover Testing feature?**

The AWS Direct Connect Failover Testing feature allows you to test the resiliency of your AWS Direct Connect connection by disabling the Border Gateway Protocol session between your on-premises networks and AWS. You can use the AWS Management Console or AWS Direct Connect application programming interface (API). Please refer to this [document](https://docs.aws.amazon.com/directconnect/latest/UserGuide/resilency_failover.html) to learn more about this feature. It is supported in all commercial AWS Regions (except GovCloud (US).

**Q: What are local preference communities for private virtual interfaces (VIFs)?**

The location preference communities for private and transit virtual interfaces provides a feature to let you influence the return path for traffic sources from VPC(s).  

**Q: What are local preference communities for private and transit virtual interfaces (VIFs)?** 

The location preference communities for private and transit virtual interfaces provides you a feature to let you influence the return path for traffic sources from VPC(s).  

**Q: What is an AWS Direct Connect Gateway — Bring your own private ASN?**

A configurable private autonomous system number (ASN) makes it possible to set the ASN on the AWS side of the Border Gateway Protocol (BGP) session for private or transit VIFs on any newly created AWS Direct Connect Gateway. This is available in all commercial AWS Regions (except AWS China Region) and AWS GovCloud (US).

**Q: What is a transit virtual interface?**

A transit virtual interface is a type of virtual interface you can create on any AWS Direct Connect connection. A transit virtual interface can only be attached to an AWS Direct Connect gateway. You can use an AWS Direct Connect gateway attached with one or more transit virtual interfaces to interface with up to six AWS Transit Gateways in any supported AWS Regions. Similar to the private virtual interface, you can establish one IPv4 BGP session and one IPv6 BGP session over a single transit virtual interface.

**Q: What is multi-account support for AWS Direct Connect gateway?**

Multi-account support for AWS Direct Connect gateway is a feature that allows you to associate up to 20 Amazon Virtual Private Clouds (Amazon VPCs) or up to six AWS Transit Gateways from multiple AWS accounts with an AWS Direct Connect gateway.

**Q: What is MACsec?**

802.1AE MAC Security (MACsec) is an [IEEE standard](https://1.ieee802.org/security/802-1ae/) that provides data confidentiality, data integrity, and data origin authenticity. You can use AWS Direct Connect connections that support MACsec to encrypt your data from your on-premises network or collocated device to your chosen AWS Direct Connect point of presence.

**Q: What is AWS Direct Connect SiteLink?**

When the AWS Direct Connect SiteLink feature is enabled at two or more AWS Direct Connect locations, you can send data between those locations, bypassing AWS Regions. AWS Direct Connect SiteLink works with both hosted and dedicated connections.

**Q: Does AWS act as my "first mile" or "last mile" provider to connect my on-premises locations to AWS?**  

No, you need to make connections between the local service providers used at your on-premises locations to connect to AWS.  

## High Availability and Resilience

**Q: Does having a link aggregation group (LAG) make my connection more resilient?**

No, a LAG doesn't make your connectivity to AWS more resilient. If you have more than one link in your LAG, and if your minimum links are set to one, your LAG will let you protect against single link failure. However, it will not protect against a single device failure or device maintenance at AWS where your LAG is terminating.  

To achieve high availability connectivity to AWS, we recommend making connections at multiple AWS Direct Connect locations. Refer to [AWS Direct Connect Resiliency Recommendations](https://aws.amazon.com/directconnect/resiliency-recommendation/) to learn more about achieving highly available network connectivity.

**Q: How do I order connections to AWS Direct Connect for high availability?**

We recommend following the resiliency best practices detailed in the [AWS Direct Connect Resiliency Recommendations](https://aws.amazon.com/directconnect/resiliency-recommendation/) page to determine the best resiliency model for your use case. After selecting a resiliency model, the [AWS Direct Connect Resiliency Toolkit](https://docs.aws.amazon.com/directconnect/latest/UserGuide/resiliency_toolkit.html) can guide you through the process of ordering redundant connections. AWS also encourages you to use the Resiliency Toolkit failover test feature to test your configurations before going live.

Each dedicated AWS Direct Connect connection consists of a single dedicated connection between ports on your router and an AWS Direct Connect device. We recommend establishing a second connection for redundancy. When you request multiple ports at the same AWS Direct Connect location, they will be provisioned on redundant AWS equipment.

If you have configured a backup IPsec VPN connection instead, all VPC traffic will failover to the VPN connection automatically. Traffic to/from public resources, such as Amazon S3, will be routed over the internet. If you do not have a backup AWS Direct Connect link or an IPsec VPN link, then Amazon VPC traffic will be dropped in the event of a failure. Traffic to/from public resources will be routed over the internet.

**Q: How do I check to see if my connections are terminated on different AWS devices?  
  
**After your connections are approved, you can validate the setup by going to “Connections”, selecting the desired connections, and looking at the “General configuration”,  “AWS logical device”.  Different device IDs indicate different AWS devices.  

**Q: Does AWS Direct Connect offer a Service Level Agreement (SLA)?**

Yes, AWS Direct Connect offers an SLA. [Details are here](https://aws.amazon.com/directconnect/sla/).

**Q: When using the failover test feature, can I configure the duration of the test or cancel the test while it's running?**

Yes, you can configure the duration of the test by setting the minimum and maximum duration for the test to be 1 minute and 180 minutes, respectively.  You can cancel the test while it is running. When the test is cancelled, we restore the Border Gateway Protocol session, and your test history reflects that the test was canceled.

**Q: Can I see my past test history when using the failover test feature? How long do you keep the test history?**

Yes, you can review your test history using the AWS Management Console or through AWS CloudTrail. We preserve your test history for 365 days. If you delete the virtual interface, your test history is also deleted.

**Q: What happens after a failover test is complete?**

After the configured test duration, we restore the Border Gateway Protocol session between your on-premises networks and AWS using the Border Gateway Protocol session parameters negotiated before starting the test.

**Q: Who can initiate a failover test using the AWS Direct Connect Resiliency Toolkit?**

Only the owner of the AWS account that includes the virtual interface can initiate the test.

**Q: Can I delete the virtual interface while the failover test for the same virtual interface is in progress?**

Yes, you can delete the virtual interface while a test for the same virtual interface is in progress.

**Q: Can I run failover tests for any type of virtual interface?**

Yes, you can run tests for the Border Gateway Protocol session(s) established using any type of virtual interface.

**Q: If I have established IPv4 and IPv6 Border Gateway Protocol sessions, can I run this test for each Border Gateway Protocol session?**

Yes, you can initiate a test for one or both Border Gateway Protocol sessions.  

## AWS Direct Connect SiteLink

**Q: Do I need new AWS Direct Connect connections to use AWS Direct Connect SiteLink, and do they need to be the same type?**  

You can use AWS Direct Connect SiteLink with your existing AWS Direct Connect connections. It works with any type of AWS Direct Connect connection (dedicated or hosted).

**Q: Where and how do I configure AWS Direct Connect SiteLink?**

You enable and disable AWS Direct Connect SiteLink when configuring virtual interfaces (VIFs). To establish a connection using AWS Direct Connect SiteLink, you must enable AWS Direct Connect SiteLink at two or more VIFs at two or more AWS Direct Connect locations. You must attach all locations to the same AWS Direct Connect gateway. You can configure your VIF to enable or disable AWS Direct Connect SiteLink using the AWS Management Console, AWS Command Line Interface, or APIs. AWS Direct Connect SiteLink is integrated with AWS CloudWatch so you can monitor traffic sent over this link.

**Q: Does AWS Direct Connect SiteLink require an AWS Direct Connect gateway connection?**

Yes. To use AWS Direct Connect SiteLink, you must connect AWS Direct Connect SiteLink-enabled virtual interfaces (VIFs) to an AWS Direct Connect gateway. The VIF type can be private or transit.

**Q: How can I tell what I’m being charged for AWS Direct Connect SiteLink?**

On billing statements, charges related to AWS Direct Connect SiteLink will appear on a separate line from other AWS Direct Connect-related charges.

**Q: What does a simple two-site network architecture look like with AWS Direct Connect SiteLink?**

To build a simple network, configure a private virtual interface (VIF) and enable AWS Direct Connect SiteLink on that VIF at each site. Then create an AWS Direct Connect gateway and associate each of your AWS Direct Connect SiteLink-enabled VIFs with it in order to create a network.

**Q: How do I implement a hub-and-spoke architecture with AWS Direct Connect SiteLink?**

To create a hub-and-spoke architecture, create an AWS Direct Connect gateway and associate it with all AWS Direct Connect SiteLink-enabled private VIFs.

**Q: How do I create a segmented network architecture with AWS Direct Connect SiteLink?**

Bring up multiple AWS Direct Connect gateways, and associate subsets of AWS Direct Connect SiteLink-enabled private virtual interfaces (VIFs) with each. AWS Direct Connect SiteLink-enabled VIFs on an AWS Direct Connect gateway cannot communicate with AWS Direct Connect SiteLink-enabled VIFs on another AWS Direct Connect gateway, creating a segmented network.

**Q: What types of virtual interfaces (VIFs) are supported by AWS Direct Connect SiteLink?**

AWS Direct Connect SiteLink is supported on private and transit VIFs. However, you cannot attach an AWS Direct Connect gateway (DXGW) to an AWS Transit Gateway when the AWS Direct Connect gateway was previously associated with a virtual private gateway, or is attached to a private virtual interface.

**Q: Does AWS Direct Connect SiteLink require BGP?**

Yes. AWS Direct Connect SiteLink requires BGP.

**Q: Does AWS Direct Connect SiteLink support IPv6?**

Yes. AWS Direct Connect SiteLink supports IPv6.

**Q: Does AWS Direct Connect SiteLink support MACsec?**

Yes. AWS Direct Connect SiteLink supports MACsec provided the port and PoP location support MACsec encryption.

**Q: Is Quality of Service (QoS) supported on AWS Direct Connect SiteLink-enabled virtual interfaces (VIFs)?**  

AWS Direct Connect does not provide managed QoS functionality. When you configure QoS on devices that are connected using AWS Direct Connect SiteLink, DSCP markings will be preserved on forwarded traffic.

**Q: Does AWS Direct Connect SiteLink support local preference BGP communities?**

Yes. You can use existing AWS Direct Connect local preference tags with AWS Direct Connect SiteLink. The following local preference BGP community tags are supported:  
7224:7100 - Low preference  
7224:7200 - Medium preference  
7224:7300 - High preference  

**Q: When should I use AWS Direct Connect SiteLink and when should I use AWS Cloud WAN?**

Depending on your use case, you might choose one, the other, or both. [Cloud WAN](https://aws.amazon.com/cloud-wan/) can create and manage networks of VPCs across multiple Regions. AWS Direct Connect SiteLink, on the other hand, connects DX locations together, bypassing AWS Regions to improve performance. AWS Direct Connect is one of multiple connectivity options that you will be able to use with a Cloud WAN network in the future.  

## AWS Local Zones

**Q: Can I use AWS Direct Connect to reach resources running in AWS Local Zones?**

Yes, when using AWS Direct Connect, you can connect to VPCs deployed in AWS Local Zones. Your data travels directly to and from AWS Local Zones over an AWS Direct Connect connection, without traversing an AWS Region. This improves performance and can reduce latency.

**Q: How do I configure AWS Local Zones to work with AWS Direct Connect?**

An AWS Direct Connect link to AWS Local Zones works the same way as connecting to a Region.

To connect to a Region, first extend your VPC from the parent Region into AWS Local Zones by creating a new subnet and assigning it to the AWS Local Zone. (Details on this process are on the [Extend a VPC to a Local Zone, Wavelength Zone, or Outpost](https://docs.aws.amazon.com/vpc/latest/userguide/Extend_VPCs.html) page in our documentation.) Then, associate your Virtual Gateway (VGW) to an AWS Direct Connect private virtual interface, or AWS Direct Connect Gateway, to make the connection. (Details can be found in the [Virtual private gateway associations](https://docs.aws.amazon.com/directconnect/latest/UserGuide/virtualgateways.html) entry in our documentation.)

You can also connect to the AWS Local Zones using AWS Direct Connect Public Virtual Interfaces using an Internet Gateway (IGW).

**Q: Are there any differences in how AWS Direct Connect connects to an AWS Local Zone compared to a Region?**

Yes, there are differences. AWS Local Zones do not support AWS Transit Gateway at this time. If you are connecting to an AWS Local Zone subnet through an AWS Transit Gateway, your traffic enters the parent Region, is processed by your AWS Transit Gateway, is sent to the AWS Local Zone, then returns (or hairpins) from the Region. Second, ingress routing destinations do not route directly to AWS Local Zones. Traffic will ingress to the parent Region first before connecting back to your AWS Local Zones. Third, unlike the Region where the maximum MTU size is 9001, the maximum MTU size for the packet connecting to Local Zones is 1468. Path MTU discovery is supported and recommended. Last, the Single flow limit (5-tuple) for connectivity to an AWS Local Zone is approximately 2.5 Gbps at maximum MTU (1468) compared to 5 Gbps at the Region. NOTE: The limitations on MTU size and single flow do not apply to AWS Direct Connect connectivity to the AWS Local Zone in Los Angeles.

**Q: Can I use AWS Site-to-Site VPN as a backup for my AWS Direct Connect link to an AWS Local Zone?**

No. Unlike connectivity to a Region, you cannot use an AWS Site-to-Site VPN as a backup to your AWS Direct Connect connection to an AWS Local Zone. For redundancy, you must use two or more AWS Direct Connect connections.

**Q: Can I use my current AWS Direct Connect Gateway (DXGW) to associate the Virtual Gateway (VGW)?**

Yes, provided the current AWS Direct Connect Gateway is not associated with an AWS Transit Gateway. Because AWS Transit Gateway is not supported in AWS Local Zones—and a DXGW that is associated with an AWS Transit Gateway cannot be associated with a VGW—you cannot associate a DXGW associated with an AWS Transit Gateway. You must create a new DXGW and associate it with the VGW.  
  

## Services Interoperability

**Q: Can I use the same private network connection with Amazon Virtual Private Cloud (VPC) and other AWS services simultaneously?**

Yes. Each AWS Direct Connect connection can be configured with one or more virtual interfaces. Virtual interfaces may be configured to access AWS services such as Amazon EC2 and Amazon S3 using public IP space, or resources in a VPC using private IP space.

**Q: If I’m using Amazon CloudFront and my origin is in my own data center, can I use AWS Direct Connect to transfer the objects stored in my own data center?**

Yes, if you are using Amazon CloudFront and your origin is in your own data center, you can use AWS Direct Connect to transfer the objects stored in your own data center. You must have a Direct Connect Public VIF and if you are filtering your route imports, you must ensure you import all Anycast routes. You also must advertise your custom origins prefix to AWS. You can find more details about advertised IP prefixes and Direct Connect Routing policy [here](https://docs.aws.amazon.com/directconnect/latest/UserGuide/routing-and-bgp.html).

**Q: Can I order a port for AWS GovCloud (US) in the AWS Management Console?**

To order a port to connect to AWS GovCloud (US) you must use the AWS GovCloud (US) Management Console.

**Q: Do AWS Global Accelerator (AGA) public endpoint prefixes get advertised from AWS to on-prem over Direct Connect public virtual interfaces ?**

A: Yes. The Direct Connect public virtual interface will advertise the AnyCast prefixes used by AGA public endpoints.  

## Link Aggregation Groups

**Q: What’s the max number of links I can have in a LAG group?**

The maximum number of links is 4x in a LAG group.

**Q: Are link aggregation groups (LAG) in active/active or active/passive mode?**

They are in active/active. In other words, AWS ports send Link Aggregation Control Protocol Data Units (LACPDUs) continuously. 

**Q: Can the maximum transmission unit of a LAG change?**

The maximum transmission unit of the LAG can be changed. Please refer to Jumbo Frame documentation [here](https://docs.aws.amazon.com/directconnect/latest/UserGuide/set-jumbo-frames-vif.html) to know more.

**Q: Can I have my ports configured for active/passive instead of active/active?**

The LAG at your endpoint can be configured with LACP active or passive modes. The AWS side is always configured as active mode LACP.

**Q: Can I mix interface types and have a few 1 G ports and a few 10 G ports in the same LAG?**

No, you can create LAG using the same type of ports (either 1 G or 10 G).

**Q: What ports types will this be available on?**

It will be available for 1 G, 10 G, and 100 G Dedicated Connection ports.

**Q: Can I LAG hosted connections as well?**

No. It will only be available for 1 G, 10 G, and 100 G Dedicated Connections. It will not be available for hosted connections.

**Q: Can I create a LAG out of my existing ports?**

Yes, if your ports are on the same AWS Direct Connect device. Please note this will cause your ports to go down for a moment while they are reconfigured as a LAG. They will not come back up until LAG is configured on your side.

**Q: Can I have a LAG that spans multiple AWS Direct Connect devices?**

LAG will only include ports on the same AWS Direct Connect devices. We don’t support multi-chassis LAG.

**Q: How do I add links to my LAG once it’s set up?**

You must request another port for your LAG. If no ports are available in the same device, you must order a new LAG and migrate your connections. For example, if you have 3x 1 G links, and would like to add a fourth, and we do not have a port available on that device, you must order a new LAG of 4x 1 G ports.

**Q: You’re out of ports and I have to order a new LAG, but I have Virtual Interfaces (VIFs) configured. How do I move those?**

You can have multiple VIFs attached to a VGW at once, and you can configure VIFs on a connection even when it’s down. We suggest you create the new VIFs on your new LAG, and then move the connections over to the new LAG once you’ve created all of your VIFs. Remember to delete the old connections so we stop billing you for them.

**Q: Can I delete a single port from my LAG?**

Yes, but only if your minimum links are set to lower than the remaining ports. For example, if you have four ports and minimum links set to four, you won’t be able to delete a port from the LAG. If minimum links are set to three, you can then delete a port from the LAG. We will return a notification with the specific panel/port you’ve deleted and a reminder to disconnect the cross connect and circuit from AWS.

**Q: Can I delete my LAG all at once?**

Yes, but just like a regular connection you won’t be able to delete it if you have VIFs configured.

**Q: If I have only two ports in my LAG can I still delete one?**  

Yes, you can have a single port in a LAG.

**Q: Can I order a LAG with only one port?**

Yes. Please note we can’t promise that ports will be available on the same chassis if you want to add more ports in the future.

**Q: Can I convert a LAG back to individual ports?**

Yes. This can be done with the _DisassociateConnectionWithLag_ API call. 

**Q: Can you create a tool to move my virtual interfaces (VIFs) for me?**

You can use _AssociateVirtualInterface_ API or console to do this operation.

**Q: Does the LAG show as a single connection or a collection of connections?**

It will show as a single dxlag and we’ll list the connection id’s under it.

**Q: What does minimum links mean, and why do I have a check box for it when I order my bundle?**

Minimum links is a feature in LACP where you can set the minimum number of links that must be active in a bundle for that bundle to be active and pass traffic. If, for example, you have four ports, your minimum links is set to three, and you only have two active ports, your bundle will not be active. If you have three or more then the bundle is active and will pass traffic if you have a VIF configured.

If you don’t select minimum links, it will default to zero. You can change the minimum links value after you’ve set up the bundle, either using the AWS Management Console or using an API.  

**Q: When I associate my existing AWS Direct Connect connection with a LAG, what happens with virtual interfaces (VIFs) already created with a connection?**

When an AWS Direct Connect connection with existing Virtual Interfaces (VIFs) is associated to a LAG, Virtual Interfaces are migrated to the LAG. Please note that certain parameters associated with VIFs must be unique, such as VLAN numbers, to be moved to LAG.

**Q: Can I set link priority on a specific link?**

We treat all links as equal, so we won’t set “link priority” on any specific link.

**Q: Can I have a 40 GE interface on my side that connects to 4x 10 GE on the AWS side?**

To do this, you need 4x 10 GE interfaces on your router to connect to AWS. A single 40 GE interface connecting to a 4x 10 GE LACP is not supported.  

## Billing

**Q: Are there any setup charges or a minimum service term commitment required to use AWS Direct Connect?**

There are no setup charges, and you may cancel at any time. Services provided by AWS Direct Connect Partners may have other terms or restrictions that apply.

**Q: How will I be charged and billed for my use of AWS Direct Connect?**  

AWS Direct Connect has two separate charges: port hours and data transfer. Pricing is per port-hour consumed for each port type. Partial port hours consumed are billed as full hours. The account that owns the port will be charged the port hour charges.

Data transfer through AWS Direct Connect will be billed in the same month in which the usage occurred. See additional information that follows to understand how data transfer will be billed.

**Q: Will Regional data transfer be billed at the AWS Direct Connect rate?  
**

No, data transfer between Availability Zones in a Region will be billed at the regular Regional data transfer rate in the same month in which the usage occurred.

**Q: What defines billable port-hours for Hosted Connections?  
**

Port hours are billed once you have accepted the Hosted Connection. Port charges will continue to be billed as long as the Hosted Connection is provisioned for your use. If you no longer want to be charged for your Hosted Connection, work with your AWS Direct Connect Partner to cancel the Hosted Connection.  

**Q: What is the format for Hosted Connection port-hour charges?**  

All Hosted Connection port-hour charges at an AWS Direct Connect location are grouped by capacity.

For example, consider the bill for a customer with two separate 200 Mbps Hosted Connections at an AWS Direct Connect location, and no other Hosted Connections at that location. The port-hour charges for the two separate 200 Mbps Hosted Connections will be summarized under a single item with a label ending in “HCPortUsage:200M”. For a month with 720 total hours, the port-hour total for this item will be 1,440, or the total number of hours in the month multiplied by the total number of 200 Mbps Hosted Connections at this location.

The Hosted Connection capacity identifiers that may appear on your bill are as follows:

HCPortUsage:50M  
HCPortUsage:100M  
HCPortUsage:200M  
HCPortUsage:300M  
HCPortUsage:400M  
HCPortUsage:500M  
HCPortUsage:1G  
HCPortUsage:2G  
HCPortUsage:5G  
HCPortUsage:10G

Note that these capacity identifiers will appear by location depending on which Hosted Connection capacities you have at each location.  

**Q: Which AWS account gets charged for the Data Transfer Out performed over a public virtual interface?**

For publicly addressable AWS resources (for example, Amazon S3 buckets, Classic EC2 instances, or EC2 traffic that goes through an internet gateway), if the outbound traffic is destined for public prefixes owned by the same AWS payer account and actively advertised to AWS through an AWS Direct Connect public virtual Interface, the Data Transfer Out (DTO) usage is metered toward the resource owner at the AWS Direct Connect data transfer rate.

For AWS Direct Connect pricing information, Refer to the AWS Direct Connect [pricing](https://aws.amazon.com/directconnect/pricing/) page for more detailed information. If using an AWS Direct Connect Partner to facilitate an AWS Direct Connect connection, contact the AWS Direct Connect Partner regarding any fees they may charge.  

**Q: Which AWS account gets charged for the Data Transfer Out performed over a transit/private virtual interface?**  

With the introduction of the granular Data Transfer Out allocation feature, the AWS account responsible for the Data Transfer Out will be charged for the Data Transfer Out performed over a transit/private virtual interface. The AWS account responsible for the Data Transfer Out will be determined based on the customer’s use of the private/transit virtual interface as follows:

Private virtual interface(s) is used to interface with Amazon Virtual Private Cloud(s) with or without AWS Direct Connect gateway(s). In the case of the private virtual interface, the AWS account that owns the AWS resources responsible for the Data Transfer Out will be charged.  

Transit virtual interface(s) are used to interface with AWS Transit Gateway(s). In the case of a transit virtual interface, the AWS account that owns the Amazon Virtual Private Cloud(s) attached to the AWS Transit Gateway associated with the AWS Direct Connect gateway attached to the transit virtual interface is charged. Please note that all applicable AWS Transit Gateway specific charges (Data Processing and Attachment) will be in addition to the Direct Connect Data Transfer Out.  

**Q: How does AWS Direct Connect work with consolidated billing?**

AWS Direct Connect data transfer usage will be aggregated to your management account.  

**Q: How do I cancel the AWS Direct Connect service?**

You can cancel AWS Direct Connect by deleting your ports from the AWS Management Console. You should also cancel any service(s) purchased by a third party. For example, contact the colocation provider to disconnect any cross-connects to AWS Direct Connect, and/or a network service provider who is providing network connectivity from your remote locations to the AWS Direct Connect location.

**Q: Do your prices include taxes?**  

Except as otherwise noted, our prices are exclusive of applicable taxes and duties, including VAT and applicable sales tax. For customers with a Japanese billing address, use of AWS services is subject to Japanese Consumption Tax. [Learn more.](https://aws.amazon.com/c-tax-faqs/)  

## Specifications

**Q: What connection speeds are available?**

For Dedicated Connections, 1 Gbps, 10 Gbps, and 100 Gbps ports are available. For Hosted Connections, connection speeds of 50 Mbps, 100 Mbps, 200 Mbps, 300 Mbps, 400 Mbps, 500 Mbps, 1 Gbps, 2 Gbps, 5 Gbps and 10 Gbps may be ordered from approved AWS Direct Connect Partners. See [AWS Direct Connect Partners](https://aws.amazon.com/directconnect/partners/) for more information. 

**Q: Are there limits on the amount of data that I can transfer using AWS Direct Connect?**

No. You may transfer any amount of data up to the limit of your selected port capacity.

**Q: Are there limits on the number of routes I can advertise towards AWS using AWS Direct Connect?**

Yes, you can advertise up to 100 routes over each Border Gateway Protocol session using AWS Direct Connect. [Learn more about AWS Direct Connect limits](https://docs.aws.amazon.com/directconnect/latest/UserGuide/limits.html).

**Q: What happens if I advertise more than 100 routes over a Border Gateway Protocol session?**

Your Border Gateway Protocol session will go down if you advertise over 100 routes over a Border Gateway Protocol session. This will prevent all network traffic flowing over that virtual interface until you reduce the number of routes to less than 100.

**Q: What are the technical requirements for the connection?**

AWS Direct Connect supports 1000BASE-LX, 10GBASE-LR, or 100GBASE-LR4 connections over single mode fiber using Ethernet transport. Your device must support 802.1Q VLANs. See the [AWS Direct Connect User Guide](https://docs.aws.amazon.com/directconnect/latest/UserGuide/Welcome.html) for more detailed requirements information.

**Q: Can I extend one of my VLANs to the AWS Cloud using AWS Direct Connect?**

No, VLANs are used in AWS Direct Connect only to separate traffic between virtual interfaces.

**Q: What are the technical requirements for virtual interfaces to public AWS services, such as Amazon EC2 and Amazon S3?**

- This connection requires the use of the Border Gateway Protocol (BGP) with an Autonomous System Number (ASN) and IP Prefixes. You will need the following information to complete the connection:
- A public or private ASN. If you are using a public ASN, you must own it. If you are using a private ASN, it must be in the 64512 to 65535 range.
- A new unused VLAN tag you select.
- Public IPs (/31 or /30) allocated to the BGP session. RFC 3021 (Using 31-Bit Prefixes on IPv4 Point-to-Point Links) is supported on all Direct Connect virtual interface types.
- By default, Amazon will advertise global public IP prefixes via BGP. You must advertise public IP prefixes (/31 or smaller) that you own or are AWS-provided via BGP. For more details, consult the [AWS Direct Connect User Guide](https://aws.amazon.com/directconnect/faqs/).  
    
- See the information that follows below for more details on AWS Direct Connect, Bring Your Own ASN.

**Q: What IP address will be assigned to each end of a virtual interface?**

If you are configuring a virtual interface to the public AWS Cloud, the IP addresses for both ends of the connection must be allocated from public IP space that you own. If the virtual interface is connected to a VPC, and you choose to have AWS automatically generate the peer IP CIDR, the IP address space for both ends of the connection is allocated by AWS and is in the 169.254.0.0/16 range.

**Q: Can I locate my hardware next to the equipment that powers AWS Direct Connect?**  

You can purchase rack space within the facility housing the AWS Direct Connect location and deploy your equipment nearby. However, due to security practices, your equipment cannot be placed within AWS Direct Connect rack or cage areas. For more information, contact the operator of your facility. Once deployed, you can connect your equipment to AWS Direct Connect using a cross-connect.

**Q: How do I enable BFD on my AWS Direct Connect connection?**

Asynchronous BFD is automatically enabled for each AWS Direct Connect virtual interface, but will not take effect until it's configured on your router. AWS has set the BFD liveness detection minimum interval to 300, and the BFD liveness detection multiplier to 3.

**Q: How do I set up AWS Direct Connect for the AWS GovCloud (US) Region?**

See the AWS GovCloud (US) User Guide for detailed instructions on setting up AWS Direct Connect for use with the [AWS GovCloud (US) Region](https://docs.aws.amazon.com/govcloud-us/latest/UserGuide/govcloud-dc.html). 

**Q: What are the technical requirements for virtual interfaces (VIF) to VPCs?**

AWS Direct Connect requires Border Gateway Protocol (BGP). To complete the connection, you will need:

• A public or private ASN. If you are using a public ASN, you must own it. If you are using a private ASN, it must be in the 64512 to 65535 range.  
• A new unused VLAN tag that you select.  
• The VPC Virtual Private Gateway (VGW) ID  
• AWS will allocate private IPs (/30) in the 169.x.x.x range for the BGP session and will advertise the VPC CIDR block over BGP. You can advertise the default route via BGP.

**Q: Can I establish a Layer 2 connection between VPC and my network?**

No, Layer 2 connections are not supported.  

## VPN Connections

**Q: How does AWS Direct Connect differ from an IPsec VPN Connection?**  

VPN connections use IPsec to establish encrypted network connectivity between your intranet and an Amazon VPC over the public internet. VPN Connections can be configured in minutes and are a good solution if you have an immediate need, have low to modest bandwidth requirements, and can tolerate the inherent variability of internet-based connectivity. AWS Direct Connect bypasses the internet; instead, it uses dedicated, private network connections between your network and AWS.

**Q: Can I use AWS Direct Connect and a VPN Connection to the same VPC simultaneously?**

Yes, but only for failover. The AWS Direct Connect path will always be preferred, when established, regardless of AS path prepending. Make sure your VPN connections can handle the failover traffic from AWS Direct Connect.

**Q: Is there any difference to the BGP configuration/setup details outlined for AWS Direct Connect?**  

VPN BGP will work the same as AWS Direct Connect.

## AWS Transit Gateway Support

**Q: Which AWS Regions offer AWS Direct Connect support for AWS Transit Gateway?**

Support for AWS Transit Gateway is available in all commercial AWS Regions.

**Q: How do I create transit virtual interface?**

You can use the AWS Management Console or API operations to create transit virtual interface.

**Q: Can I allocate a transit virtual interface in another AWS account?**

Yes, you can allocate transit virtual interface in any AWS account.

**Q: Can I attach a transit virtual interface to my Virtual Private Gateway?**

No, you cannot attach transit virtual interface to your Virtual Private Gateway.

**Q: Can I attach a private virtual interface to my AWS Transit Gateway?**

No, you cannot attach private virtual interface to your AWS Transit Gateway.

**Q: What are the quotas associated with a transit virtual interface?**

Please refer to [AWS Direct Connect quotas page](https://docs.aws.amazon.com/directconnect/latest/UserGuide/limits.html) to learn more about the limits associated with transit virtual interface.

**Q: I have an existing AWS Direct Connect gateway attached to a private virtual interface, can I attach a transit virtual interface to this AWS Direct Connect gateway?**

No, an AWS Direct Connect Gateway can only have one type of virtual interface attached.

**Q: Can I associate my AWS Transit Gateway to the AWS Direct Connect gateway attached to a private virtual interface?**

No, an AWS Transit Gateway can only be associated with the AWS Direct Connect gateway attached to transit virtual interface.

**Q: How long does it take to establish an association between AWS Transit Gateway and AWS Direct Connect gateway?**

It can take up to 40 minutes to establish an association between AWS Transit Gateway and AWS Direct Connect gateway.

**Q: How many total virtual interfaces can I create per 1 Gbps, 10 Gbps, or 100 Gbps dedicated connection?**

You can create up to 51 virtual interfaces per 1 Gbps, 10 Gbps, or 100 Gbps dedicated connection inclusive of the transit virtual interface.

**Q: Can I create a transit virtual interface on a hosted connection of any speed?**

Yes.

**Q: I have 4x10 Gbps LAG, how many transit virtual interfaces can I create on this link aggregation group (LAG)?**

You can create one transit virtual interface on the 4x10G LAG.

**Q: Does a transit virtual interface support jumbo frames?**

Yes, a transit virtual interface will support jumbo frames. Maximum transmission unit (MTU) size will be limited to 8,500.

**Q: Do you support all the Border Gateway Protocol (BGP) attributes that you support on the private virtual interface for the transit virtual interface?**

Yes, you can continue to use supported BGP attributes (AS\_PATH, Local Pref, NO\_EXPORT) on the transit virtual interface.

## AWS Direct Connect Gateway

**Q: Why is an AWS Direct Connect gateway necessary?**

An AWS Direct Connect gateway performs several functions:

- AWS Direct Connect gateway will give you the ability to interface with VPCs in any AWS Region (except the AWS China Region), so you can use your AWS Direct Connect connections to interface with more than one AWS Region.
- You can share a private virtual interface to interface with up to 10 VPCs to reduce the number of Border Gateway Protocol sessions between your on-premises network and AWS deployments.
- By attaching transit virtual interface(s) (VIF) to an AWS Direct Connect gateway and associating AWS Transit Gateway(s) with the Direct Connect gateway, you can share transit virtual interface(s) to connect with up to three AWS Transit Gateways. This can reduce the number of Border Gateway Protocol sessions between your on-premises network and AWS deployments. Once a transit VIF is connected to an AWS Direct Connect Gateway, that Gateway cannot also host another Private VIF - it is dedicated to the transit VIF.
- You can associate multiple virtual private gateways (VGWs, associated with a VPC) to an AWS Direct Connect gateway, as long as the IP CIDR blocks of the Amazon VPC associated with the Virtual Private Gateway do not overlap.

**Q: Can I associate more than one AWS Transit Gateway with an AWS Direct Connect gateway?**

You can associate up to three Transit Gateway to an AWS Direct Connect gateway as long as the IP CIDR blocks announced from your Transit Gateways do not overlap.

**Q: Can I associate VPCs owned by any AWS account with an AWS Direct Connect gateway owned by any AWS account?**

Yes, you can associate VPCs owned by any AWS account with an AWS Direct Connect gateway owned by any AWS account.

**Q: Can I associate AWS Transit Gateway that are owned by any AWS account with an AWS Direct Connect gateway that is owned by any AWS account?**

Yes, you can associate a Transit Gateway owned by any AWS account with an AWS Direct Connect gateway owned by any AWS account.

**Q: If I use an AWS Direct Connect gateway, does my traffic to the desired AWS Region go by way of the associated home AWS Region?**

No. When using AWS Direct Connect gateway, your traffic will take the shortest path to and from your AWS Direct Connect location to the destination AWS Region, regardless of the associated home AWS Region of the AWS Direct Connect location where you are connected.

**Q: Are there additional fees when using AWS Direct Connect gateway and working with remote AWS Regions?**

There are no charges for using an AWS Direct Connect gateway. You will pay applicable egress data charges based on the source remote AWS Region and port hour charges. See the [AWS Direct Connect pricing page for details](https://aws.amazon.com/directconnect/pricing/). 

**Q: Do I need to use the same AWS account with my private/transit virtual interfaces(s), AWS Direct Connect gateway, Virtual Private Gateway, or AWS Transit Gateways in order to use an AWS Direct Connect gateway?**

Private virtual interfaces and AWS Direct Connect gateways must be in the same AWS account. Similarly, transit virtual interfaces and AWS Direct Connect gateways must be in the same AWS account. Virtual private gateway(s) and AWS Transit Gateway(s) can be in different AWS accounts than the account that owns the AWS Direct Connect gateway.

**Q: If I associate virtual private gateways (VGWs) to an AWS Direct Connect gateway, **can I continue to use all VPC features?****

Networking features, such as Elastic File System, Elastic Load Balancing, Application Load Balancer, Security Groups, Access Control List, and AWS PrivateLink, work with AWS Direct Connect gateway. AWS Direct Connect gateway does not support AWS VPN CloudHub functionality. However, if you are using an AWS Site-to-Site VPN connection to a virtual gateway (VGW) that is associated with your AWS Direct Connect gateway, you can use your VPN connection for failover.

Features that are not currently supported by AWS Direct Connect are; AWS Classic VPN, AWS VPN (such as edge-to-edge routing), VPC peering, VPC endpoints.

**Q: I am working with an AWS Direct Connect Partner to get private virtual interface (VIF) provisioned for my account, can I use an AWS Direct Connect gateway?**  

Yes, you can associate a provisioned private virtual interface (VIF) with your AWS Direct Connect gateway when you confirm that you are provisioned as private in your AWS account.

**Q: Can I connect to VPCs in my local Region?**

You can continue to attach your virtual interfaces (VIFs) to virtual private gateways (VGWs). You will still have intra-Region VPC connectivity, and will be charged the egress rate for the related geographic Regions.

**Q: What are the quotas associated with an AWS Direct Connect gateway?**

Please refer to the [AWS Direct Connect quotas](https://docs.aws.amazon.com/directconnect/latest/UserGuide/limits.html) page for information on this topic.

**Q: Can virtual private gateways (VGWs, associated with a VPC) be part of more than one AWS Direct Connect gateway?**

No, a VGW-VPC pair cannot be part of more than one AWS Direct Connect gateway.

**Q: Can you attach a private virtual interface (VIF) to more than one AWS Direct Connect gateway?**

No, one private virtual interface can only attach to one AWS Direct Connect gateway OR one Virtual Private Gateway. We recommend that you follow [AWS Direct Connect resiliency recommendations](https://aws.amazon.com/directconnect/resiliency-recommendation/) and attach more than one private virtual interface. 

**Q: Does AWS Direct Connect gateway break existing AWS VPN CloudHub functionality?**

No, AWS Direct Connect gateway does not break AWS VPN CloudHub. AWS Direct Connect gateway enables connectivity between on-premises networks and VPCs in any AWS Region. AWS VPN CloudHub enables connectivity between on-premises networks using AWS Direct Connect or a VPN within the same Region. The VIF is associated with the VGW directly. Existing AWS VPN CloudHub functionality will continue to be supported. You can attach an AWS Direct Connect virtual interface (VIF) directly to a virtual private gateway (VGW) to support intra-Region AWS VPN CloudHub.

**Q: What type of traffic is, and is not, supported by AWS Direct Connect gateway?**

Please refer to [AWS Direct Connect User Guide](https://docs.aws.amazon.com/directconnect/latest/UserGuide/dc-ug.pdf) to review supported and not supported traffic patterns. 

**Q: I currently have a VPN in us-east-1 attached to a virtual private gateway (VGW). I want to use AWS VPN CloudHub in us-east-1 between the VPN and a new VIF. Can I do this with AWS Direct Connect gateway?**

No, you cannot do this with an AWS Direct Connect gateway, but the option to attach a VIF directly to a VGW is available to use the VPN <-> AWS Direct Connect AWS VPN CloudHub use case.

**Q: I have an existing private virtual interface associated with virtual private gateway (VGW), can I associate my existing private virtual interface with an AWS Direct Connect gateway?**

No, an existing private virtual interface associated with VGW cannot be associated with an AWS Direct Connect gateway. To do this, you must create a new private virtual interface, and at the time of creation, associate it with your AWS Direct Connect gateway.

**Q: If I have a virtual private gateway (VGW) attached to a VPN and an AWS Direct Connect gateway, and my AWS Direct Connect circuit goes down, will my VPC traffic route out to the VPN?**

Yes, as long as the VPC route table has routes to the virtual private gateway (VGW) towards the VPN.

**Q: Can I attach a virtual private gateway (VGW) to an AWS Direct Connect gateway if it is not attached to a VPC?**

No, you cannot associate an unattached VGW to AWS Direct Connect gateway.

**Q: I have created an AWS Direct Connect gateway with one AWS Direct Connect Private VIF, and three non-overlapping virtual private gateways (VGWs) -- each associated with a VPC. What happens if I detach one of the VGW from the VPC?**

Traffic from your on-premises network to the detached VPC will stop, and VGW's association with the AWS Direct Connect gateway will be deleted.

**Q: I have created an AWS Direct Connect gateway with one AWS Direct Connect VIF, and three non-overlapping VGW-VPC pairs, what happens if I detach one of the virtual private gateways (VGW) from the AWS Direct Connect gateway?**

Traffic from your on-premises network to the detached VGW (associated with a VPC) will stop.

**Q: Can I send traffic from a VPC that is associated with an AWS Direct Connect gateway to another VPC associated to the same AWS Direct Connect gateway?**

No, AWS Direct Connect gateway's only support routing traffic from AWS Direct Connect VIFs to VGW (associated with VPC). In order to send traffic between two VPCs, you must configure a VPC peering connection.

**Q: I currently have a VPN in us-east-1 that is attached to a virtual private gateway (VGW). If I associate this VGW to an AWS Direct Connect gateway, can I send traffic from my VPN to a VIF attached to the AWS Direct Connect gateway in a different AWS Region?**

No, an AWS Direct Connect gateway will not route traffic between a VPN and an AWS Direct Connect VIF. To enable this use case, you must create a VPN in the AWS Region of the VIF and attach the VIF and the VPN to the same VGW.

**Q: Can I resize a VPC that is associated with an AWS Direct Connect gateway?**

Yes, you can resize the VPC. If you resize your VPC, you must resend the proposal with the resized VPC CIDR to the AWS Direct Connect gateway owner. Once the AWS Direct Connect gateway owner approves the new proposal, the resized VPC CIDR will be advertised towards your on-premises network.

**Q: Is there a way to configure an AWS Direct Connect gateway to selectively propagate prefixes to/from VPCs?**

Yes, AWS Direct Connect gateway offers a way for you to selectively announce prefixes towards your on-premises networks. For prefixes that are advertised from your on-premises networks, each VPC associated with an AWS Direct Connect gateway receives all prefixes announced from your on-premises networks. If you want to limit traffic to and from any specific VPC, you should consider using Access Control Lists (ACLs) for each VPC.

## Local Preference Communities

**Q: Can I use this feature for my existing EBGP sessions?**

Yes, all existing BGP sessions on private virtual interfaces support the use of local preference communities.

**Q: Will this feature be available on both Public and Private Virtual Interfaces?**

No, this feature is currently available for private and transit virtual interfaces only.

**Q: Will this feature work with an AWS Direct Connect gateway?**

Yes, this feature will work with private virtual interfaces attached with AWS Direct Connect gateway.

**Q: Can I verify that communities are being received by AWS?**

No, at this time we do not provide such monitoring features.

**Q: What are the supported local preference communities for an AWS Direct Connect private virtual interface?**

The following communities are supported for private virtual interface and are evaluated in order of lowest to highest preference. Communities are mutually exclusive. Prefixes marked with the same communities, and bearing identical MED\*, AS\_PATH attributes are candidates for multi-pathing.

- 7224:7100 – Low Preference
- 7224:7200 – Medium Preference
- 7224:7300 – High Preference

**Q: What is the default behavior, in case I do not use the supported communities?**

If you do not specify Local Preference communities for your private VIF, the default local preference is based on the distance to the AWS Direct Connect Locations from the local Region. In such situation, egress behavior across multiple VIFs from multiple AWS Direct Connect Locations may be arbitrary.

**Q: I have two private VIFs on a physical connection at an AWS Direct Connect location; can I use supported communities to influence egress behavior across these two private VIFs?**

Yes, you can use this feature to influence egress traffic behavior between two VIFs on the same physical connection.

**Q: Does the local preference communities feature support failover?**

Yes. This can be accomplished by advertising prefixes over the primary/active virtual interface with a community for higher local preference than prefixes advertised over the backup/passive virtual interface. This feature is backward compatible with pre-existing methods for achieving failover; if your connection is currently configured for failover, no additional changes are necessary.

**Q: I have already configured my routers with AS\_PATH, do I need to change the configuration to use community tags and disrupt my network?**

No, we will continue to respect AS\_PATH attribute. This feature is an additional knob you can use to get better control over the incoming traffic from AWS. AWS Direct Connect follows the standard approach for path selection. Bear in mind that local preference is evaluated before the AS\_PATH attribute.

**Q: I have two AWS Direct Connect connections, one is 1 Gbps and another is 10 Gbps, and both are advertising the same prefix. I would like to receive all traffic for this destination across the 10 Gbps AWS Direct Connect connection, but still be able to failover to the 1 Gbps connection. Can local preference communities be used to balance traffic in this scenario?**

Yes. By marking the prefix advertised over the 10 Gbps AWS Direct Connection with a community of a higher local preference, it will be the preferred path. If the 10 Gbps fails or the prefix is withdrawn, the 1 Gbps interface becomes the return path.

**Q: How wide will AWS multipath traffic to my network?**

We will multipath per prefix at up to 16 next-hops wide, where each next-hop is a unique AWS endpoint.

**Q: Can I have v4 and v6 BGP sessions running over a single VPN tunnel?**

At this time, we only allow v4 BGP session running single VPN tunnel with IPv4 address.  

**Q: Is there any difference to the BGP configuration/setup details outlined for AWS Direct Connect?**

VPN BGP will work the same as AWS Direct Connect.

**Q: Can I terminate my tunnel to an endpoint with an IPv6 address?**

At this time, we only support IPv4 endpoint address for VPN. 

**Q: Can I terminate my tunnel to an IPv4 address and run IPv6 BGP sessions over the tunnel?**

At this time, we only allow v4 BGP session running single VPN tunnel with IPv4 address.  

## AWS Direct Connect Gateway - Private ASN

**Q: What is this feature?**

Configurable Private Autonomous System Number (ASN). This allows customers to set the ASN on the AWS side of the BGP session for private VIFs on any newly created AWS Direct Connect Gateway.

**Q: Where are these features available?**

All commercial AWS Regions (except AWS China Region) and AWS GovCloud (US).

**Q: How can I configure/assign my ASN to be advertised as the AWS side ASN?**

You can configure/assign an ASN to be advertised as the AWS side ASN during creation of the new AWS Direct Connect gateway. You can create an AWS Direct Connect gateway using the AWS Management Console or a CreateDirectConnectGateway API operation.

**Q: Can I use any ASN - public and private?**

You can assign any private ASN to the AWS side. You cannot assign any other public ASN.

**Q: Why can't I assign a public ASN for the AWS half of the BGP session?**

AWS is not validating ownership of the ASNs, therefore we're limiting the AWS side ASN to private ASNs. We want to protect customers from BGP spoofing.

**Q: What ASN can I choose?**

You can choose any private ASN. Ranges for 16-bit private ASNs include 64512 to 65534. You can also provide 32-bit ASNs between 4200000000 and 4294967294.

**Q: What will happen if I try to assign a public ASN to the AWS half of the BGP session?**

We will ask you to re-enter a private ASN once you attempt to create the AWS Direct Connect gateway.

**Q: If I don't provide an ASN for the AWS half of the BGP session, what ASN can I expect from AWS?**

AWS will provide an ASN of 64512 for the AWS Direct Connect gateway if you don't choose one.

**Q: Where can I view the AWS side ASN?**

You can view the AWS side ASN in the AWS Direct Connect console and in the response of the DescribeDirectConnectGateways or DescribeVirtualInterfaces API operations.

**Q: If I have a public ASN, will it work with a private ASN on the AWS side?**

Yes, you can configure the AWS side of the BGP session with a private ASN and your side with a public ASN.

**Q: I have private VIFs already configured and want to set a different AWS side ASN for the BGP session on an existing VIF. How can I make this change?**

You must create a new AWS Direct Connect gateway with desired ASN, and create a new VIF with the newly created AWS Direct Connect gateway. Your device configuration also must change appropriately.

**Q: I'm attaching multiple private VIFs to a single AWS Direct Connect gateway. Can each VIF have a separate AWS side ASN?**

No, you can assign/configure separate AWS side ASN for each AWS Direct Connect gateway, not each VIF. The AWS side ASN for VIF is inherited from the AWS side ASN of the attached AWS Direct Connect gateway.

**Q: Can I use different private ASNs for my AWS Direct Connect Gateway and Virtual Private Gateway?**

Yes, you can use different private ASNs for your AWS Direct Connect Gateway and Virtual Private Gateway. The AWS side ASN you receive depends on your private virtual interface association.

**Q: Can I use same private ASNs for my AWS Direct Connect Gateway and Virtual Private Gateway?**

Yes, you can use same private ASNs for your AWS Direct Connect Gateway and Virtual Private Gateway. The AWS side ASN you receive depends on your private virtual interface association.

**Q: I'm attaching multiple Virtual Private Gateways with their own private ASN to a single AWS Direct Connect gateway configured with its own private ASN. Which private ASN takes precedence, VGW or AWS Direct Connect Gateway?**

AWS Direct Connect Gateway private ASN will be used as the AWS side ASN for the Border Gateway Protocol (BGP) session between your network and AWS.

**Q: Where can I select my own private ASN?**

You can select your own private ASN in the AWS Direct Connect gateway console. Once the AWS Direct Connect gateway is configured with an AWS side ASN, the private virtual interfaces associated with the AWS Direct Connect gateway use your configured ASN as the AWS side ASN.

**Q: I use AWS VPN CloudHub today. Will I have to adjust my configuration in the future?**

You will not have to make any changes.

**Q: I want to select a 32-bit ASN. What is the range of 32-bit private ASNs?**

We support 32-bit ASNs from 4200000000 to 4294967294.

**Q: Once the AWS Direct Connect gateway is created, can I change or modify the AWS side ASN?**

No, you cannot modify the AWS side ASN after creation. You can delete the AWS Direct Connect gateway and recreate a new AWS Direct Connect gateway with the desired private ASN.  

## MACsec

**Q: Does MACsec replace other encryption technologies I currently use in my network?**

MACsec is not intended as a replacement for any specific encryption technology. For simplicity, and for defense in depth, you should continue to use any encryption technologies that you already use. We offer MACsec as an encryption option you can integrate into your network in addition to other encryption technologies you currently use.

**Q: Which type of AWS Direct Connect connections support MACsec?**

MACsec is supported on 10 Gbps and 100 Gbps dedicated AWS Direct Connect connections at selected [points of presence](https://aws.amazon.com/directconnect/locations/). For MACsec to work, your dedicated connection must be transparent to Layer 2 traffic and the device terminating the Layer 2 adjacency must support MACsec. If you are using a last-mile connectivity partner, check that your last-mile connection can support MACsec. MACsec is not supported on 1 Gbps dedicated connections or any hosted connections.

**Q: Do I need any special hardware to use MACsec?**

Yes. You will need a MACsec-capable device on your end of the Ethernet connection to an AWS Direct Connect location. Refer to the [MAC Security](https://docs.aws.amazon.com/directconnect/latest/UserGuide/MACsec.html) section of our user guide to verify supported operation modes and required MACsec features.

**Q: Do I need a new AWS Direct Connect connection to use MACsec with my MACsec-capable device?**  

MACsec requires that your connection is terminated on a MACsec-capable device on the AWS Direct Connect side of the connection. You can check if your existing connection is MACsec-capable through the AWS Management Console or by using the _[DescribeConnections](https://docs.aws.amazon.com/directconnect/latest/APIReference/API_DescribeConnections.html)_ AWS Direct Connect API. If your existing MACsec connection is not terminated on a MACsec-capable device, you can request a new MACsec-capable connection using the AWS Management Console or the _[CreateConnection](https://docs.aws.amazon.com/directconnect/latest/APIReference/API_CreateConnection.html)_ API.  

**Q: Which MACsec cipher suites do you support?**

For 100Gbps connections we support the GCM-AES-XPN-256 cipher suite. For 10Gbps connections we support GCM-AES-256 and GCM-AES-XPN-256.

**Q: Why do you only support 256-bit keys?**

We support only 256-bit MACsec keys to provide the latest advanced data protection.

**Q: Do you require the use of Extended Packet Numbering (XPN)?**

We require the use of XPN for 100Gbps connections. For 10Gbps connections we support both GCM-AES-256 and GCM-AES-XPN-256. High-speed connections, such as 100 Gbps dedicated connections, can quickly exhaust MACsec’s original 32-bit packet numbering space, which would require you to rotate your encryption keys every few minutes to establish a new Connectivity Association. To avoid this situation, the IEEE Std 802.1AEbw-2013 amendment introduced extended packet numbering, increasing the numbering space to 64-bits, easing the timeliness requirement for key rotation.

**Q: Do you support the use of Secure Channel Identifier (SCI)?**  

Yes. We require SCI to be on. This setting cannot be changed.

**Q: Do you support IEEE 802.1Q (Dot1q/VLAN) tag offset/dot1q-in-clear?**  

No, we do not support moving the VLAN tag outside of the encrypted payload.

**Q: Is there an additional charge for MACsec ?**

No, there is no additional charge for MACsec.  

## Maintenance Events

**Q: When will I be informed about maintenance events on Direct Connect?**  

Scheduled maintenance is planned and we provide 3 notifications - 14 calendar days, followed by 7 calendar days and followed by 1 calendar day notifications. Emergency maintenance may be performed at any time and you may receive up to 60-minute notification(s) depending upon the nature of the maintenance. You can subscribe to notifications on the AWS Direct Connect Console. For more details, see [Notifications for Direct Connect scheduled maintenance or events](https://repost.aws/knowledge-center/get-direct-connect-notifications).   

**Q: How can I get notifications for Direct Connect scheduled maintenance or events?  
**  
To help you manage events, the [AWS Personal Health Dashboard](https://docs.aws.amazon.com/health/latest/ug/getting-started-phd.html) displays relevant information and also provides notifications for activities. You can also set up an [email notification](https://repost.aws/knowledge-center/get-direct-connect-notifications) to receive notifications for scheduled maintenance or events that affect Direct Connect.

**Q: Why can’t maintenance be performed on only nights and weekends?**

Due the global scale of Direct Connect, we are unable to limit maintenance to only weekends. We spread our planned maintenance out across all days of the week. Maintenance is usually carried out per device (dxcon-xxxxxx, for example) to limit impact. We highly recommends that you follow the [AWS Direct Connect resiliency recommendations](https://aws.amazon.com/directconnect/resiliency-recommendation/) to set up resilient network connections to AWS resources in a reliable, scalable and cost-effective way.

**Q: I received a notice that Direct Connect is performing maintenance at a time that impacts our business. How do I prepare for maintenance on my Direct Connect connection?**

When a Direct Connect connection is down for maintenance, that connection can be down from a few minutes to a few hours. To prepare for this downtime, take one of the following actions:

- Request a redundant Direct Connect connection.
- Configure a [AWS Site-to-Site VPN](https://docs.aws.amazon.com/vpn/latest/s2svpn/VPC_VPN.html) (virtual private network) connection as a backup.

It's a best practice to shift your traffic to another circuit  during Direct Connect maintenance. To prevent any production traffic disruption, use one of the preceding options before the scheduled maintenance period. You can also use the [AWS Direct Connect Resiliency Toolkit](https://docs.aws.amazon.com/directconnect/latest/UserGuide/resiliency_toolkit.html) to [perform scheduled failover tests](https://docs.aws.amazon.com/directconnect/latest/UserGuide/resiliency_failover.html) and verify the resiliency of your connections

**Q: Can the maintenance be rescheduled for a different date/time?**

From time to time, AWS conducts planned maintenance to improve availability and deliver new features to our customers. Our normal process for non-emergent/planned maintenance provides customers with at least 14 calendar days of advance notice to allow our customers to prepare ahead of time by testing their redundancy to ensure minimal impact. For more information, see [How do I cancel a Direct Connect maintenance event](https://repost.aws/knowledge-center/direct-connect-cancel-maintenance)?

**Q: If I have multiple connections to the same Direct Connect location, will all my connections go down during maintenance?**

If you've followed our High Availability and Resilience recommendations, our maintenance scheduling algorithm will detect your redundant setup and schedule maintenance at different times for each connection.  If all your connections are on the same AWS logical device, then you will be impacted by the maintenance.

**Q: Do partners coordinate their maintenance schedules with AWS?**

Partners are included in planned maintenance notifications from AWS so they can plan accordingly. AWS does not have visibility to partner maintenance activities. You will need to check with your partner/provider for their planned maintenance schedule(s). Customer’s may want to consider using two different partners in different Direct Connect locations to minimize the risk of partner maintenance windows overlapping.