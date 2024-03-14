---
tags:
  - cloud/aws
---

https://aws.amazon.com/transit-gateway/

![](https://i.imgur.com/JvxTMTu.png)  
AWS Transit Gateway connects your Amazon Virtual Private Clouds (VPCs) and on-premises networks through a central hub. This connection simplifies your network and puts an end to complex peering relationships. Transit Gateway acts as a highly scalable cloud router—each new connection is made only once.  
![](https://i.imgur.com/rggZ1D1.png)

## AWS Transit Gateway Features

## Routing

AWS Transit Gateways supports dynamic and static layer 3 routing between Amazon Virtual Private Clouds (VPCs) and VPN. Routes determine the next hop depending on the destination IP address of the packet, and can point to an Amazon VPC or to a VPN connection.

## Edge Connectivity

You can create VPN connections between your AWS Transit Gateway and on-premises gateways using VPN. You can create multiple VPN connections that announce the same prefixes and enable Equal Cost Multipath (ECMP) between these connections. By load-balancing traffic over multiple paths, ECMP can increase the bandwidth.

## Transit Gateway Connect

AWS Transit Gateway Connect enables native integration of Software-Defined Wide Area Network (SD-WAN) appliances into AWS. Customers can now seamlessly extend their SD-WAN edge into AWS using standard protocols such as Generic Routing Encapsulation (GRE) and Border Gateway Protocol (BGP). It provides customers with added benefits such as improved bandwidth and supports dynamic routing with increased route limits, thus removing the need to set up multiple IPsec VPNs between the SD-WAN appliances and Transit Gateway.  

## Amazon VPC Feature Interoperability

AWS Transit Gateway enables the resolution of public DNS hostnames to private IP addresses when queried from Amazon VPCs that are also attached to the AWS Transit Gateway.

An instance in an Amazon VPC can access a NAT gateway, Network Load Balancer, AWS PrivateLink, and Amazon Elastic File System in other Amazon VPCs that are also attached to the AWS Transit Gateway.

## Monitoring

AWS Transit Gateway provides statistics and logs that are then used by services such as Amazon CloudWatch and Amazon VPC Flow Logs. You can use Amazon CloudWatch to get bandwidth usage between Amazon VPCs and a VPN connection, packet flow count, and packet drop count. You can also enable Amazon VPC Flow Logs on AWS Transit Gateway so you can capture information on the IP traffic routed through the AWS Transit Gateway.

AWS Transit Gateway Network Manager includes events and metrics to monitor the quality of your global network, both in AWS and on premises. Event alerts specify changes in the topology, routing, and connection status. Usage metrics provide information on up/down connection, bytes in/out, packets in/out, and packets dropped.  

## Management

You can use the command-line interface (CLI), AWS Management Console, or AWS CloudFormation to create and manage your AWS Transit Gateway. AWS Transit Gateway provides Amazon CloudWatch metrics, such as the number of bytes sent and received between Amazon VPCs and VPNs, the packet count, and the drop count. In addition, you can use Amazon VPC Flow Logs with AWS Transit Gateway to capture information about the IP traffic going through the AWS Transit Gateway attachment.

## Peering

With transit gateway peering, you can establish peering connections between transit gateways in the same AWS region or across regions. Peering allows customers to directly route traffic between two transit gateways. Inter-region peering provides you with a simple and cost-effective way to share resources between AWS Regions or replicate data for geographic redundancy. Intra-region peering allows multiple teams within your organization to deploy their own transit gateways and easily interconnect their networks in the same AWS region.  

## Multicast

With Transit Gateway multicast, you can now easily create and manage multicast groups in the cloud, much easier than deploying and managing legacy hardware on premises. You can scale up and down your multicast solution in the cloud to simultaneously distribute a stream of content to multiple subscribers. With Transit Gateway multicast you have fine-grain control over who can produce and who can consume multicast traffic.  

## Security

AWS Transit Gateway is integrated with Identity and Access Management (IAM), enabling you to manage access to AWS Transit Gateway securely. Using IAM, you can create and manage AWS users and groups, and use permissions to allow and deny their access to the AWS Transit Gateway. 

## Automated Provisioning

Once you’ve registered existing AWS Transit Gateways, the Network Manager automatically identifies the Site-to-Site VPN connections and the on-premises resources with which they are associated. The SD-WAN consoles from vendors that have integrated AWS Transit Gateway, such as Cisco, Aruba, Silver Peak, or Aviatrix, automatically provision new AWS Site-to-Site VPN connections in Transit Gateway Network Manager and automate the definition of your on-premises network in Transit Gateway Network Manager. You can also manually define your on-premises network in Transit Gateway Network Manager.  

## Single Management Portal across Cloud and On-premises Networks

Manage your private network that spans the cloud and your premises, from a single pane of glass on the AWS Management Console.  

## Events

Get notified of network changes, routing changes, and connection status updates.  

## Metrics

Monitor your global network through performance and traffic metrics, such as bytes in/out, packets in/out, and packets dropped.  

## SD-WAN Network Manager Compatibility

Compatible SD-WAN partners of AWS, such as Cisco, Aruba, Silver Peak, Aviatrix, and Versa have pre-configured AWS Site-to-Site VPNs so that SD-WAN solutions can automate the connection of your remote sites with AWS. With AWS Transit Gateway Network Manager, you get a unified view of your network across AWS and on-premises networks.

![[Module 7 - Connecting Networks#AWS Transit Gateway]]