---
tags:
  - cloud/aws
---


https://aws.amazon.com/privatelink/

### AWS PrivateLink Concepts
You can use Amazon VPC to define a virtual private cloud (VPC), which is a logically isolated virtual network. You can launch AWS resources in your VPC. You can allow the resources in your VPC to connect to resources outside that VPC. For example, add an internet gateway to the VPC to allow access to the internet, or add a VPN connection to allow access to your on-premises network.

<mark style="background: #D2B3FFA6;">Alternatively, use AWS PrivateLink to allow the resources in your VPC to connect to services in other VPCs using private IP addresses, as if those services were hosted directly in your VPC.</mark>

The following diagram provides a high-level overview of how AWS PrivateLink works. Service consumers create interface VPC endpoints to connect to endpoint services that are hosted by service providers.  
![](https://i.imgur.com/6fdhyTs.png)

#### [Service Providers](#)
The owner of a service is the _service provider_ Service providers include AWS, AWS Partners, and other AWS accounts. Service providers can host their services using AWS resources, such as EC2 instances, or using on-premises servers. 
###### Concepts
- [Endpoint services](https://docs.aws.amazon.com/vpc/latest/privatelink/concepts.html#concepts-endpoint-services)
- [Service names](https://docs.aws.amazon.com/vpc/latest/privatelink/concepts.html#concepts-service-names)
- [Service states](https://docs.aws.amazon.com/vpc/latest/privatelink/concepts.html#concepts-service-states)
#### Endpoint Services
A service provider creates an _endpoint service_ to make their service available in a Region. A service provider must specify a load balancer when creating an endpoint service. The load balancer receives requests from service consumers and routes them to your service.

By default, your endpoint service is not available to service consumers. You must add permissions that allow specific AWS principals to connect to your endpoint service.
#### Service Names
Each endpoint service is identified by a service name. A service consumer must specify the name of the service when creating a VPC endpoint. Service consumers can query the service names for AWS services. Service providers must share the names of their services with service consumers.
#### Service States
The following are the possible states for an endpoint service:

- `Pending` - The endpoint service is being created.
    
- `Available` - The endpoint service is available.
    
- `Failed` - The endpoint service could not be created.
    
- `Deleting` - The service provider deleted the endpoint service and deletion is in progress.
    
- `Deleted` - The endpoint service is deleted.


#### Service Consumers

The user of a service is a _service consumer_. Service consumers can access endpoint services from AWS resources, such as EC2 instances, or from on-premises servers.

###### Concepts

- [VPC endpoints](https://docs.aws.amazon.com/vpc/latest/privatelink/concepts.html#concepts-vpc-endpoints)
- [Endpoint network interfaces](https://docs.aws.amazon.com/vpc/latest/privatelink/concepts.html#concepts-endpoint-network-interfaces)
- [Endpoint policies](https://docs.aws.amazon.com/vpc/latest/privatelink/concepts.html#concepts-endpoint-policies)
- [Endpoint states](https://docs.aws.amazon.com/vpc/latest/privatelink/concepts.html#concepts-endpoint-states)

#### VPC Endpoints
A service consumer creates a _VPC endpoint_ to connect their VPC to an endpoint service. A service consumer must specify the service name of the endpoint service when creating a VPC endpoint. There are multiple types of VPC endpoints. You must create the type of VPC endpoint that's required by the endpoint service.

- `Interface` - Create an _interface endpoint_ to send TCP traffic to an endpoint service. Traffic destined for the endpoint service is resolved using DNS.
    
- `GatewayLoadBalancer` - Create a _Gateway Load Balancer endpoint_ to send traffic to a fleet of virtual appliances using private IP addresses. You route traffic from your VPC to the Gateway Load Balancer endpoint using route tables. The Gateway Load Balancer distributes traffic to the virtual appliances and can scale with demand.
    

There is another type of VPC endpoint, `Gateway`, which creates a _gateway endpoint_ to send traffic to Amazon S3 or DynamoDB. Gateway endpoints do not use AWS PrivateLink, unlike the other types of VPC endpoints. For more information, see [Gateway endpoints](https://docs.aws.amazon.com/vpc/latest/privatelink/gateway-endpoints.html).

#### Endpoint Network Interfaces

An _endpoint network interface_ is a requester-managed network interface that serves as an entry point for traffic destined to an endpoint service. For each subnet that you specify when you create a VPC endpoint, we create an endpoint network interface in the subnet.

If a VPC endpoint supports IPv4, its endpoint network interfaces have IPv4 addresses. If a VPC endpoint supports IPv6, its endpoint network interfaces have IPv6 addresses. The IPv6 address for an endpoint network interface is unreachable from the internet. When you describe an endpoint network interface with an IPv6 address, notice that `denyAllIgwTraffic` is enabled.

The IP addresses of an endpoint network interface will not change during the lifetime of its VPC endpoint.

#### Endpoint Policies

A _VPC endpoint policy_ is an IAM resource policy that you attach to a VPC endpoint. It determines which principals can use the VPC endpoint to access the endpoint service. The default VPC endpoint policy allows all actions by all principals on all resources over the VPC endpoint.

#### Endpoint States

When you create a VPC endpoint, the endpoint service receives a connection request. The service provider can accept or reject the request. If the service provider accepts the request, the service consumer can use the VPC endpoint after it enters the `Available` state.

The following are the possible states for a VPC endpoint:

- `PendingAcceptance` - The connection request is pending. This is the initial state if requests are manually accepted.
    
- `Pending` - The service provider accepted the connection request. This is the initial state if requests are automatically accepted. The VPC endpoint returns to this state if the service consumer modifies the VPC endpoint.
    
- `Available` - The VPC endpoint is available for use.
    
- `Rejected` - The service provider rejected the connection request. The service provider can also reject a connection after it is available for use.
    
- `Expired` - The connection request expired.
    
- `Failed` - The VPC endpoint could not be made available.
    
- `Deleting` - The service consumer deleted the VPC endpoint and deletion is in progress.
    
- `Deleted` - The VPC endpoint is deleted.
    

#### AWS PrivateLink Connections

Traffic from your VPC is sent to an endpoint service using a connection between the VPC endpoint and the endpoint service. Traffic between a VPC endpoint and an endpoint service stays within the AWS network, without traversing the public internet.

A service provider adds [permissions](https://docs.aws.amazon.com/vpc/latest/privatelink/configure-endpoint-service.html#add-remove-permissions) so that service consumers can access the endpoint service. The service consumer initiates the connection and the service provider accepts or rejects the connection request.

With interface VPC endpoints, service consumers can use [endpoint polices](https://docs.aws.amazon.com/vpc/latest/privatelink/vpc-endpoints-access.html) to control which IAM principals can use a VPC endpoint to access an endpoint service.

#### Private Hosted Zones

A _hosted zone_ is a container for DNS records that define how to route traffic for a domain or subdomain. With a _public hosted zone_, the records specify how to route traffic on the internet. With a _private hosted zone_, the records specify how to route traffic in your VPCs.

You can configure Amazon Route 53 to route domain traffic to a VPC endpoint. For more information, see [Routing traffic to a VPC endpoint using your domain name](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/routing-to-vpc-interface-endpoint.html).

You can use Route 53 to configure split-horizon DNS, where you use the same domain name for both a public website and an endpoint service powered by AWS PrivateLink. DNS requests for the public hostname from the consumer VPC resolve to the private IP addresses of the endpoint network interfaces, but requests from outside the VPC continue to resolve to the public endpoints.


![[Module 7 - Connecting Networks#Connecting Your VPC to Supported AWS Services]]

### Creating an Interface VPC Endpoint
#### Accessing an AWS Service Using an Interface VPC Endpoint
You can create an interface VPC endpoint to connect to services powered by AWS PrivateLink, including many AWS services. For an overview, see [AWS PrivateLink concepts](https://docs.aws.amazon.com/vpc/latest/privatelink/concepts.html) and [Access AWS services through AWS PrivateLink](https://docs.aws.amazon.com/vpc/latest/privatelink/privatelink-access-aws-services.html).

For each subnet that you specify from your VPC, we create an endpoint network interface in the subnet and assign it a private IP address from the subnet address range. An endpoint network interface is a requester-managed network interface; you can view it in your AWS account, but you can't manage it yourself.  
You are billed for hourly usage and data processing charges.
###### Contents
- [Prerequisites](https://docs.aws.amazon.com/vpc/latest/privatelink/create-interface-endpoint.html#prerequisites-interface-endpoints)
- [Create a VPC endpoint](https://docs.aws.amazon.com/vpc/latest/privatelink/create-interface-endpoint.html#create-interface-endpoint-aws)
- [Shared subnets](https://docs.aws.amazon.com/vpc/latest/privatelink/create-interface-endpoint.html#interface-endpoint-shared-subnets)

##### Prerequisites
- Deploy the resources that will access the AWS service in your VPC.
- To use private DNS, you must enable DNS hostnames and DNS resolution for your VPC. For more information, see [View and update DNS attributes](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-dns.html#vpc-dns-updating) in the _Amazon VPC User Guide_.
- To enable IPv6 for an interface endpoint, the AWS service must support access over IPv6. For more information, see [IP address types](https://docs.aws.amazon.com/vpc/latest/privatelink/privatelink-access-aws-services.html#aws-service-ip-address-type).
- Create a security group that allows the resources in your VPC to communicate with the endpoint network interfaces for the VPC endpoint. To ensure that tools such as the AWS CLI can make requests over HTTPS from resources in the VPC to the AWS service, the security group must allow inbound HTTPS traffic.
- If your resources are in a subnet with a network ACL, verify that the network ACL allows traffic between the endpoint network interfaces and the resources in the VPC.
- There are quotas on your AWS PrivateLink resources.

##### Create a VPC Endpoint
Use the following procedure to create an interface VPC endpoint that connects to an AWS service.
###### To Create an Interface Endpoint for an AWS Service
1. Open the Amazon VPC console at [https://console.aws.amazon.com/vpc/](https://console.aws.amazon.com/vpc/).
2. In the navigation pane, choose **Endpoints**.
3. Choose **Create endpoint**.
4. For **Service category**, choose **AWS services**.
5. For **Service name**, select the service. For more information, see [AWS services that integrate with AWS PrivateLink](https://docs.aws.amazon.com/vpc/latest/privatelink/aws-services-privatelink-support.html).
6. For **VPC**, select the VPC from which you'll access the AWS service.
7. If, in Step 5, you selected the service name for Amazon S3, and if you want to configure [private DNS support](https://docs.aws.amazon.com/vpc/latest/privatelink/vpc-endpoints-s3.html#private-dns-s3), select **Additional settings**, **Enable DNS name**. When you make this selection, it also automatically selects **Enable private DNS only for inbound endpoint**. You can configure private DNS with an inbound Resolver endpoint only for interface endpoints for Amazon S3. If you do not have a gateway endpoint for Amazon S3 and you select **Enable private DNS only for inbound endpoint**, you'll receive an error when you attempt the final step in this procedure.  
    If, in Step 5, you selected the service name for any service other than Amazon S3, **Additional settings**, **Enable DNS name** is already selected. We recommend that you keep the default.
8. For **Subnets**, select one subnet per Availability Zone from which you'll access the AWS service. You can't select multiple subnets from the same Availability Zone. We create an endpoint network interface in each subnet that you select. By default, we select IP addresses from the subnet IP address ranges and assign them to the endpoint network interfaces. To choose the IP addresses for an endpoint network interface, select **Designate IP addresses** and enter an IPv4 address from the subnet address range. If the endpoint service supports IPv6, you can also enter an IPv6 address from the subnet address range.
9. For **IP address type**, choose from the following options:
    - **IPv4** – Assign IPv4 addresses to your endpoint network interfaces. This option is supported only if all selected subnets have IPv4 address ranges and the service accepts IPv4 requests.
    - **IPv6** – Assign IPv6 addresses to your endpoint network interfaces. This option is supported only if all selected subnets are IPv6 only subnets and the service accepts IPv6 requests.
    - **Dualstack** – Assign both IPv4 and IPv6 addresses to your endpoint network interfaces. This option is supported only if all selected subnets have both IPv4 and IPv6 address ranges and the service accepts both IPv4 and IPv6 requests.
10. For **Security groups**, select the security groups to associate with the endpoint network interfaces for the VPC endpoint. By default, we associate the default security group for the VPC.
11. For **Policy**, select **Full access** to allow all operations by all principals on all resources over the VPC endpoint. Otherwise, select **Custom** to attach a VPC endpoint policy that controls the permissions that principals have for performing actions on resources over the VPC endpoint. This option is available only if the service supports VPC endpoint policies. For more information, see [Endpoint policies](https://docs.aws.amazon.com/vpc/latest/privatelink/vpc-endpoints-access.html).
12. (Optional) To add a tag, choose **Add new tag** and enter the tag key and the tag value.
13. Choose **Create endpoint**.
###### To Create an Interface Endpoint Using the Command line
- [create-vpc-endpoint](https://docs.aws.amazon.com/cli/latest/reference/ec2/create-vpc-endpoint.html) (AWS CLI)
- [New-EC2VpcEndpoint](https://docs.aws.amazon.com/powershell/latest/reference/items/New-EC2VpcEndpoint.html) (Tools for Windows PowerShell)

##### Shared Subnets
You can't create, describe, modify, or delete VPC endpoints in subnets that are shared with you. However, you can use the VPC endpoints in subnets that are shared with you.

### Configure an Interface Endpoint.
After you create an interface VPC endpoint, you can update its configuration.
#### Tasks
- [Add or remove subnets](https://docs.aws.amazon.com/vpc/latest/privatelink/interface-endpoints.html#add-remove-subnets)
- [Associate security groups](https://docs.aws.amazon.com/vpc/latest/privatelink/interface-endpoints.html#associate-security-groups)
- [Edit the VPC endpoint policy](https://docs.aws.amazon.com/vpc/latest/privatelink/interface-endpoints.html#edit-vpc-endpoint-policy)
- [Enable private DNS names](https://docs.aws.amazon.com/vpc/latest/privatelink/interface-endpoints.html#enable-private-dns-names)
- [Manage tags](https://docs.aws.amazon.com/vpc/latest/privatelink/interface-endpoints.html#add-remove-interface-endpoint-tags)

#### Add or Remove Subnets
You can choose one subnet per Availability Zone for your interface endpoint. If you add a subnet, we create an endpoint network interface in the subnet and assign it a private IP address from the IP address range of the subnet. If you remove a subnet, we delete its endpoint network interface.
###### To Change the Subnets Using the Console
1. Open the Amazon VPC console at [https://console.aws.amazon.com/vpc/](https://console.aws.amazon.com/vpc/).
2. In the navigation pane, choose **Endpoints**.
3. Select the interface endpoint.
4. Choose **Actions**, **Manage subnets**.
5. Select or deselect Availability Zones as needed. For each Availability Zone, select one subnet. By default, we select IP addresses from the subnet IP address ranges and assign them to the endpoint network interfaces. To choose the IP addresses for an endpoint network interface, select **Designate IP addresses** and enter an IPv4 address from the subnet address range. If the endpoint service supports IPv6, you can also enter an IPv6 address from the subnet address range.  
    If you specify an IP address for a subnet that already has an endpoint network interface for this VPC endpoint, we replace the endpoint network interface with a new one. This processes temporarily disconnects the subnet and the VPC endpoint.
6. Choose **Modify subnets**.
###### To Change the Subnets Using the Command line
- [modify-vpc-endpoint](https://docs.aws.amazon.com/cli/latest/reference/ec2/modify-vpc-endpoint.html) (AWS CLI)
- [Edit-EC2VpcEndpoint](https://docs.aws.amazon.com/powershell/latest/reference/items/Edit-EC2VpcEndpoint.html) (Tools for Windows PowerShell)


#### Associate Security Groups
You can change the security groups that are associated with the network interfaces for your interface endpoint. The security group rules control the traffic that is allowed to the endpoint network interface from the resources in your VPC.
###### To Change the Security Groups Using the Console
1. Open the Amazon VPC console at [https://console.aws.amazon.com/vpc/](https://console.aws.amazon.com/vpc/).
2. In the navigation pane, choose **Endpoints**.
3. Select the interface endpoint.
4. Choose **Actions**, **Manage security groups**.
5. Select or deselect security groups as needed.
6. Choose **Modify security groups**.


###### To Change the Security Groups Using the Command line
- [modify-vpc-endpoint](https://docs.aws.amazon.com/cli/latest/reference/ec2/modify-vpc-endpoint.html) (AWS CLI)
- [Edit-EC2VpcEndpoint](https://docs.aws.amazon.com/powershell/latest/reference/items/Edit-EC2VpcEndpoint.html) (Tools for Windows PowerShell)

#### Edit the VPC Endpoint Policy
If the AWS service supports endpoint policies you can edit the endpoint policy for the endpoint. After you update an endpoint policy, it can take a few minutes for the changes to take effect. For more information, see [Endpoint policies](https://docs.aws.amazon.com/vpc/latest/privatelink/vpc-endpoints-access.html).
###### To Change the Endpoint Policy Using the Console
1. Open the Amazon VPC console at [https://console.aws.amazon.com/vpc/](https://console.aws.amazon.com/vpc/).
2. In the navigation pane, choose **Endpoints**.
3. Select the interface endpoint.
4. Choose **Actions**, **Manage policy**.
5. Choose **Full Access** to allow full access to the service, or choose **Custom** and attach a custom policy.
6. Choose **Save**.
###### To Change the Endpoint Policy Using the Command line
- [modify-vpc-endpoint](https://docs.aws.amazon.com/cli/latest/reference/ec2/modify-vpc-endpoint.html) (AWS CLI)
- [Edit-EC2VpcEndpoint](https://docs.aws.amazon.com/powershell/latest/reference/items/Edit-EC2VpcEndpoint.html) (Tools for Windows PowerShell)

#### Enable Private DNS Names
You can enable private DNS names for your VPC endpoint. To use private DNS names, you must enable both [DNS hostnames and DNS resolution](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-dns.html#vpc-dns-updating) for your VPC. After you enable private DNS names, it might take a few minutes for the private IP addresses to become available. The DNS records that we create when you enable private DNS names are private. Therefore, the private DNS name is not publicly resolvable.

###### To Change the Private DNS Names Option Using the Console
1. Open the Amazon VPC console at [https://console.aws.amazon.com/vpc/](https://console.aws.amazon.com/vpc/).
2. In the navigation pane, choose **Endpoints**.
3. Select the interface endpoint.
4. Choose **Actions**, **Modify private DNS name**.
5. Select or clear **Enable for this endpoint** as required.
6. If the service is Amazon S3, selecting **Enable for this endpoint** in the previous step also selects **Enable private DNS only for inbound endpoint**. If you prefer the standard private DNS functionality, clear **Enable private DNS only for inbound endpoint**. If you do not have a gateway endpoint for Amazon S3 in addition to an interface endpoint for Amazon S3, and you select **Enable private DNS only for inbound endpoint**, you'll receive an error when you save changes in the next step. For more information, see [Private DNS](https://docs.aws.amazon.com/vpc/latest/privatelink/vpc-endpoints-s3.html#private-dns-s3).
7. Choose **Save changes**.

###### To Change the Private DNS Names Option Using the Command line
- [modify-vpc-endpoint](https://docs.aws.amazon.com/cli/latest/reference/ec2/modify-vpc-endpoint.html) (AWS CLI)
- [Edit-EC2VpcEndpoint](https://docs.aws.amazon.com/powershell/latest/reference/items/Edit-EC2VpcEndpoint.html) (Tools for Windows PowerShell)

#### Manage Tags
You can tag your interface endpoint to help you identify it or categorize it according to your organization's needs.
###### To Manage Tags Using the Console
1. Open the Amazon VPC console at [https://console.aws.amazon.com/vpc/](https://console.aws.amazon.com/vpc/).
2. In the navigation pane, choose **Endpoints**.
3. Select the interface endpoint.
4. Choose **Actions**, **Manage tags**.
5. For each tag to add choose **Add new tag** and enter the tag key and tag value. 
6. To remove a tag, choose **Remove** to the right of the tag key and value.
7. Choose **Save**.
###### To Manage Tags Using the Command line
- [create-tags](https://docs.aws.amazon.com/cli/latest/reference/ec2/create-tags.html) and [delete-tags](https://docs.aws.amazon.com/cli/latest/reference/ec2/delete-tags.html) (AWS CLI)
- [New-EC2Tag](https://docs.aws.amazon.com/powershell/latest/reference/items/New-EC2Tag.html) and [Remove-EC2Tag](https://docs.aws.amazon.com/powershell/latest/reference/items/Remove-EC2Tag.html) (Tools for Windows PowerShell)


### Receive Alerts for Interface Endpoints Events
You can create a notification to receive alerts for specific events related to your interface endpoint. For example, you can receive an email when a connection request is accepted or rejected.
###### Tasks
- [Create an SNS notification](https://docs.aws.amazon.com/vpc/latest/privatelink/manage-notifications-endpoint.html#create-sns-notification)
- [Add an access policy](https://docs.aws.amazon.com/vpc/latest/privatelink/manage-notifications-endpoint.html#add-access-policy)
- [Add a key policy](https://docs.aws.amazon.com/vpc/latest/privatelink/manage-notifications-endpoint.html#add-key-policy)

#### Create an SNS Notification
Use the following procedure to create an Amazon SNS topic for the notifications and subscribe to the topic.
###### To Create a Notification for an Interface Endpoint Using the Console
1. Open the Amazon VPC console at [https://console.aws.amazon.com/vpc/](https://console.aws.amazon.com/vpc/).
2. In the navigation pane, choose **Endpoints**.
3. Select the interface endpoint.
4. From the **Notifications** tab, choose **Create notification**.
5. For **Notification ARN**, choose the ARN for the SNS topic that you created.
6. To subscribe to an event, select it from **Events**.
    - **Connect** – The service consumer created the interface endpoint. This sends a connection request to the service provider.
    - **Accept** – The service provider accepted the connection request.
    - **Reject** – The service provider rejected the connection request.
    - **Delete** – The service consumer deleted the interface endpoint.
7. Choose **Create notification**.
    
###### To Create a Notification for an Interface Endpoint Using the Command line
- [create-vpc-endpoint-connection-notification](https://docs.aws.amazon.com/cli/latest/reference/ec2/create-vpc-endpoint-connection-notification.html) (AWS CLI)

#### Add an Access Policy
Add an access policy to the Amazon SNS topic that allows AWS PrivateLink to publish notifications on your behalf, such as the following. For more information, see [How do I edit my Amazon SNS topic's access policy?](http://aws.amazon.com/premiumsupport/knowledge-center/sns-edit-topic-access-policy/) Use the `aws:SourceArn` and `aws:SourceAccount` global condition keys to protect against the [confused deputy problem](https://docs.aws.amazon.com/IAM/latest/UserGuide/confused-deputy.html).

```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": {
        "Service": "vpce.amazonaws.com"
      },
      "Action": "SNS:Publish",
      "Resource": "arn:aws:sns:region:account-id:topic-name",
      "Condition": {
        "ArnLike": {
          "aws:SourceArn": "arn:aws:ec2:region:account-id:vpc-endpoint/endpoint-id"
        },
        "StringEquals": {
          "aws:SourceAccount": "account-id"
        }
      }
    }
  ]
}
```

#### Add a Key Policy
f you're using encrypted SNS topics, the resource policy for the KMS key must trust AWS PrivateLink to call AWS KMS API operations. The following is an example key policy.
```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": {
        "Service": "vpce.amazonaws.com"
      },
      "Action": [
        "kms:GenerateDataKey*",
        "kms:Decrypt"
      ],
      "Resource": "arn:aws:kms:region:account-id:key/key-id",
      "Condition": {
        "ArnLike": {
          "aws:SourceArn": "arn:aws:ec2:region:account-id:vpc-endpoint/endpoint-id"
        },
        "StringEquals": {
          "aws:SourceAccount": "account-id"
        }
      }
    }
  ]
}
```

#### Delete an Interface Endpoint
When you are finished with a VPC endpoint, you can delete it. Deleting an interface endpoint also deletes its endpoint network interfaces.
###### To Delete an Interface Endpoint Using the Console
1. Open the Amazon VPC console at [https://console.aws.amazon.com/vpc/](https://console.aws.amazon.com/vpc/).
2. In the navigation pane, choose **Endpoints**.
3. Select the interface endpoint.
4. Choose **Actions**, **Delete VPC endpoints**.
5. When prompted for confirmation, enter `delete`.
6. Choose **Delete**.
###### To Delete an Interface Endpoint Using the Command line
- [delete-vpc-endpoints](https://docs.aws.amazon.com/cli/latest/reference/ec2/delete-vpc-endpoints.html) (AWS CLI)


## Gateway Endpoints
Gateway VPC endpoints provide reliable connectivity to Amazon S3 and DynamoDB without requiring an internet gateway or a NAT device for your VPC. Gateway endpoints do not use AWS PrivateLink, unlike other types of VPC endpoints.  
There is no additional charge for using gateway endpoints.  
Amazon S3 supports both gateway endpoints and interface endpoints.


- You can access Amazon S3 and DynamoDB through their public service endpoints or through gateway endpoints. This overview compares these methods.
### Access through an Internet Gateway
The following diagram shows how instances access Amazon S3 and DynamoDB through their public service endpoints. Traffic to Amazon S3 or DynamoDB from an instance in a public subnet is routed to the internet gateway for the VPC and then to the service. Instances in a private subnet can't send traffic to Amazon S3 or DynamoDB, because by definition private subnets do not have routes to an internet gateway. To enable instances in the private subnet to send traffic to Amazon S3 or DynamoDB, you would add a NAT device to the public subnet and route traffic in the private subnet to the NAT device. While traffic to Amazon S3 or DynamoDB traverses the internet gateway, it does not leave the AWS network.

![](https://i.imgur.com/15UU1lS.png)

### Access through a Gateway Endpoint
The following diagram shows how instances access Amazon S3 and DynamoDB through a gateway endpoint. Traffic from your VPC to Amazon S3 or DynamoDB is routed to the gateway endpoint. Each subnet route table must have a route that sends traffic destined for the service to the gateway endpoint using the prefix list for the service. For more information, see [AWS-managed prefix lists](https://docs.aws.amazon.com/vpc/latest/userguide/working-with-aws-managed-prefix-lists.html) in the _Amazon VPC User Guide_.

![](https://i.imgur.com/qHJaU4Z.png)

### Routing
When you create a gateway endpoint, you select the VPC route tables for the subnets that you enable. The following route is automatically added to each route table that you select. The destination is a prefix list for the service owned by AWS and the target is the gateway endpoint.

|Destination|Target|
|---|---|
|`prefix_list_id`|`gateway_endpoint_id`|

#### Considerations
- You can review the endpoint routes that we add to your route table, but you cannot modify or delete them. To add an endpoint route to a route table, associate it with the gateway endpoint. We delete the endpoint route when you disassociate the route table from the gateway endpoint or when you delete the gateway endpoint.
    
- All instances in the subnets associated with a route table associated with a gateway endpoint automatically use the gateway endpoint to access the service. Instances in subnets that aren't associated with these route tables use the public service endpoint, not the gateway endpoint.
    
- A route table can have both an endpoint route to Amazon S3 and an endpoint route to DynamoDB. You can have endpoint routes to the same service (Amazon S3 or DynamoDB) in multiple route tables. You can't have multiple endpoint routes to the same service (Amazon S3 or DynamoDB) in a single route table.
    
- We use the most specific route that matches the traffic to determine how to route the traffic (longest prefix match). For route tables with an endpoint route, this means the following:
    
    - If there is a route that sends all internet traffic (0.0.0.0/0) to an internet gateway, the endpoint route takes precedence for traffic destined for the service (Amazon S3 or DynamoDB) in the current Region. Traffic destined for a different AWS service uses the internet gateway.
        
    - Traffic that's destined for the service (Amazon S3 or DynamoDB) in a different Region goes to the internet gateway because prefix lists are specific to a Region.
        
    - If there is a route that specifies the exact IP address range for the service (Amazon S3 or DynamoDB) in the same Region, that route takes precedence over the endpoint route.

### Gateway Endpoints for Amazon S3
You can access Amazon S3 from your VPC using gateway VPC endpoints. After you create the gateway endpoint, you can add it as a target in your route table for traffic destined from your VPC to Amazon S3.

There is no additional charge for using gateway endpoints.

Amazon S3 supports both gateway endpoints and interface endpoints. With a gateway endpoint, you can access Amazon S3 from your VPC, without requiring an internet gateway or NAT device for your VPC, and with no additional cost. However, gateway endpoints do not allow access from on-premises networks, from peered VPCs in other AWS Regions, or through a transit gateway. For those scenarios, you must use an interface endpoint, which is available for an additional cost. For more information, see [Types of VPC endpoints for Amazon S3](https://docs.aws.amazon.com/AmazonS3/latest/userguide/privatelink-interface-endpoints.html#types-of-vpc-endpoints-for-s3) in the _Amazon S3 User Guide_.
###### Contents
- [Considerations](https://docs.aws.amazon.com/vpc/latest/privatelink/vpc-endpoints-s3.html#gateway-endpoint-considerations-s3)
- [Private DNS](https://docs.aws.amazon.com/vpc/latest/privatelink/vpc-endpoints-s3.html#private-dns-s3)
- [Create a gateway endpoint](https://docs.aws.amazon.com/vpc/latest/privatelink/vpc-endpoints-s3.html#create-gateway-endpoint-s3)
- [Control access using bucket policies](https://docs.aws.amazon.com/vpc/latest/privatelink/vpc-endpoints-s3.html#bucket-policies-s3)
- [Associate route tables](https://docs.aws.amazon.com/vpc/latest/privatelink/vpc-endpoints-s3.html#associate-route-tables-s3)
- [Edit the VPC endpoint policy](https://docs.aws.amazon.com/vpc/latest/privatelink/vpc-endpoints-s3.html#edit-vpc-endpoint-policy-s3)
- [Delete a gateway endpoint](https://docs.aws.amazon.com/vpc/latest/privatelink/vpc-endpoints-s3.html#delete-gateway-endpoint-s3)

#### Considerations
- A gateway endpoint is available only in the Region where you created it. Be sure to create your gateway endpoint in the same Region as your S3 buckets.
    
- If you're using the Amazon DNS servers, you must enable both [DNS hostnames and DNS resolution](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-dns.html#vpc-dns-updating) for your VPC. If you're using your own DNS server, ensure that requests to Amazon S3 resolve correctly to the IP addresses maintained by AWS.
    
- Check whether you are using an AWS service that requires access to an S3 bucket. For example, a service might require access to buckets that contain log files, or might require you to download drivers or agents to your EC2 instances. If so, ensure that your endpoint policy allows the AWS service or resource to access these buckets using the `s3:GetObject` action.
    
- You can't use the `aws:SourceIp` condition in an identity policy or a bucket policy for requests to Amazon S3 that traverse a VPC endpoint. Instead, use the `aws:VpcSourceIp` condition. Alternatively, you can use route tables to control which EC2 instances can access Amazon S3 through the VPC endpoint.
    
- The outbound rules for the security group for instances that access Amazon S3 through the gateway endpoint must allow traffic to Amazon S3. You can use the ID of the [prefix list](https://docs.aws.amazon.com/vpc/latest/userguide/working-with-aws-managed-prefix-lists.html) for Amazon S3 as the destination in the outbound rule.
    
- Gateway endpoints support only IPv4 traffic.
    
- The source IPv4 addresses from instances in your affected subnets as received by Amazon S3 change from public IPv4 addresses to the private IPv4 addresses in your VPC. An endpoint switches network routes, and disconnects open TCP connections. The previous connections that used public IPv4 addresses are not resumed. We recommend that you do not have any critical tasks running when you create or modify an endpoint; or that you test to ensure that your software can automatically reconnect to Amazon S3 after the connection break.
    
- Endpoint connections cannot be extended out of a VPC. Resources on the other side of a VPN connection, VPC peering connection, transit gateway, or AWS Direct Connect connection in your VPC cannot use a gateway endpoint to communicate with Amazon S3.
    
- Your account has a default quota of 20 gateway endpoints per Region, which is adjustable. There is also a limit of 255 gateway endpoints per VPC.

#### Private DNS
You can configure private DNS to optimize costs when you create both a gateway endpoint and an interface endpoint for Amazon S3.

###### Route 53 Resolver

Amazon provides a DNS server, called the [Route 53 Resolver](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/resolver.html), for your VPC. The Route 53 Resolver automatically resolves local VPC domain names and records in private hosted zones. However, you can't use the Route 53 Resolver from outside your VPC. Route 53 provides Resolver endpoints and Resolver rules so that you can use the Route 53 Resolver from outside your VPC. An _inbound Resolver endpoint_ forwards DNS queries from the on-premises network to Route 53 Resolver. An _outbound Resolver endpoint_ forwards DNS queries from the Route 53 Resolver to the on-premises network.

When you configure your interface endpoint for Amazon S3 to use private DNS only for the inbound Resolver endpoint, we create an inbound Resolver endpoint. The inbound Resolver endpoint resolves DNS queries to Amazon S3 from on-premises to the private IP addresses of the interface endpoint. We also add ALIAS records for the Route 53 Resolver to the public hosted zone for Amazon S3, so that DNS queries from your VPC resolve to the Amazon S3 public IP addresses, which routes traffic to the gateway endpoint.

###### Private DNS

If you configure private DNS for your interface endpoint for Amazon S3 but do not configure private DNS only for the inbound Resolver endpoint, requests from both your on-premises network and your VPC use the interface endpoint to access Amazon S3. Therefore, you pay to use the interface endpoint for traffic from the VPC, instead of using the gateway endpoint for no additional charge.  
![](https://i.imgur.com/7yjoVTS.png)

###### Private DNS only for the Inbound Resolver Endpoint
If you configure private DNS only for the inbound Resolver endpoint, requests from your on-premises network use the interface endpoint to access Amazon S3, and requests from your VPC use the gateway endpoint to access Amazon S3. Therefore, you optimize your costs, because you pay to use the interface endpoint only for traffic that can't use the gateway endpoint.

![](https://i.imgur.com/QDTLXpo.png)

###### Configure Private DNS
You can configure private DNS for an interface endpoint for Amazon S3 when you create it or after you create it. For more information, see [Create a VPC endpoint](https://docs.aws.amazon.com/vpc/latest/privatelink/create-interface-endpoint.html#create-interface-endpoint-aws) (configure during creation) or [Enable private DNS names](https://docs.aws.amazon.com/vpc/latest/privatelink/interface-endpoints.html#enable-private-dns-names) (configure after creation).

### Create a Gateway Endpoint
Use the following procedure to create a gateway endpoint that connects to Amazon S3.
###### To Create a Gateway Endpoint Using the Console

1. Open the Amazon VPC console at [https://console.aws.amazon.com/vpc/](https://console.aws.amazon.com/vpc/).
2. In the navigation pane, choose **Endpoints**.
3. Choose **Create endpoint**.
4. For **Service category**, choose **AWS services**.
5. For **Services**, add the filter **Type: Gateway** and select **com.amazonaws.**`region`**.s3**.
6. For **VPC**, select the VPC in which to create the endpoint.
7. For **Route tables**, select the route tables to be used by the endpoint. We automatically add a route that points traffic destined for the service to the endpoint network interface.
8. For **Policy**, select **Full access** to allow all operations by all principals on all resources over the VPC endpoint. Otherwise, select **Custom** to attach a VPC endpoint policy that controls the permissions that principals have to perform actions on resources over the VPC endpoint.
9. (Optional) To add a tag, choose **Add new tag** and enter the tag key and the tag value.
10. Choose **Create endpoint**.
    
###### To Create a Gateway Endpoint Using the Command line
- [create-vpc-endpoint](https://docs.aws.amazon.com/cli/latest/reference/ec2/create-vpc-endpoint.html) (AWS CLI)

### Control Access Using Bucket Policies

You can use bucket policies to control access to buckets from specific endpoints, VPCs, IP address ranges, and AWS accounts. These examples assume that there are also policy statements that allow the access required for your use cases.
###### Example: Restrict Access to a Specific Endpoint

You can create a bucket policy that restricts access to a specific endpoint by using the [aws:sourceVpce](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_condition-keys.html#condition-keys-sourcevpce) condition key. The following policy denies access to the specified bucket using the specified actions unless the specified gateway endpoint is used. Note that this policy blocks access to the specified bucket using the specified actions through the AWS Management Console.

```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "Allow-access-to-specific-VPCE",
      "Effect": "Deny",
      "Principal": "*",
      "Action": ["s3:PutObject", "s3:GetObject", "s3:DeleteObject"],
      "Resource": ["arn:aws:s3:::bucket_name",
                   "arn:aws:s3:::bucket_name/*"],
      "Condition": {
        "StringNotEquals": {
          "aws:sourceVpce": "vpce-1a2b3c4d"
        }
      }
    }
  ]
}
```

###### Example: Restrict Access to a Specific VPC
You can create a bucket policy that restricts access to specific VPCs by using the [aws:sourceVpc](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_condition-keys.html#condition-keys-sourcevpc) condition key. This is useful if you have multiple endpoints configured in the same VPC. The following policy denies access to the specified bucket using the specified actions unless the request comes from the specified VPC. Note that this policy blocks access to the specified bucket using the specified actions through the AWS Management Console.

```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "Allow-access-to-specific-VPC",
      "Effect": "Deny",
      "Principal": "*",
      "Action": ["s3:PutObject", "s3:GetObject", "s3:DeleteObject"],
      "Resource": ["arn:aws:s3:::example_bucket",
                   "arn:aws:s3:::example_bucket/*"],
      "Condition": {
        "StringNotEquals": {
          "aws:sourceVpc": "vpc-111bbb22"
        }
      }
    }
  ]
}
```

###### Example: Restrict Access to a Specific IP Address Range
You can create a policy that restricts access to specific IP address ranges by using the [aws:VpcSourceIp](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_condition-keys.html#condition-keys-vpcsourceip) condition key. The following policy denies access to the specified bucket using the specified actions unless the request comes from the specified IP address. Note that this policy blocks access to the specified bucket using the specified actions through the AWS Management Console.
```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "Allow-access-to-specific-VPC-CIDR",
      "Effect": "Deny",
      "Principal": "*",
      "Action": ["s3:PutObject", "s3:GetObject", "s3:DeleteObject"],
      "Resource": ["arn:aws:s3:::bucket_name",
                   "arn:aws:s3:::bucket_name/*"],
      "Condition": {
        "NotIpAddress": {
          "aws:VpcSourceIp": "172.31.0.0/16"
        }
      }
    }
  ]
}
```

###### Example: Restrict Access to Buckets in a Specific AWS account
You can create a policy that restricts access to the S3 buckets in a specific AWS account by using the `s3:ResourceAccount` condition key. The following policy denies access to S3 buckets using the specified actions unless they are owned by the specified AWS account.
```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "Allow-access-to-bucket-in-specific-account",
      "Effect": "Deny",
      "Principal": "*",
      "Action": ["s3:GetObject", "s3:PutObject", "s3:DeleteObject"],
      "Resource": "arn:aws:s3:::*",
      "Condition": {
        "StringNotEquals": {
          "s3:ResourceAccount": "111122223333"
        }
      }
    }
  ]
}
```

### Associate Route Tables

You can change the route tables that are associated with the gateway endpoint. When you associate a route table, we automatically add a route that points traffic destined for the service to the endpoint network interface. When you disassociate a route table, we automatically remove the endpoint route from the route table.
###### To Associate Route Tables Using the Console
1. Open the Amazon VPC console at [https://console.aws.amazon.com/vpc/](https://console.aws.amazon.com/vpc/).
    
2. In the navigation pane, choose **Endpoints**.
    
3. Select the gateway endpoint.
    
4. Choose **Actions**, **Manage route tables**.
    
5. Select or deselect route tables as needed.
    
6. Choose **Modify route tables**.
    
###### To Associate Route Tables Using the Command line
- [modify-vpc-endpoint](https://docs.aws.amazon.com/cli/latest/reference/ec2/modify-vpc-endpoint.html) (AWS CLI)


### Edit the VPC Endpoint Policy

You can edit the endpoint policy for a gateway endpoint, which controls access to Amazon S3 from the VPC through the endpoint. The default policy allows full access. For more information, see [Endpoint policies](https://docs.aws.amazon.com/vpc/latest/privatelink/vpc-endpoints-access.html).

###### To Change the Endpoint Policy Using the Console

1. Open the Amazon VPC console at [https://console.aws.amazon.com/vpc/](https://console.aws.amazon.com/vpc/).
    
2. In the navigation pane, choose **Endpoints**.
    
3. Select the gateway endpoint.
    
4. Choose **Actions**, **Manage policy**.
    
5. Choose **Full Access** to allow full access to the service, or choose **Custom** and attach a custom policy.
    
6. Choose **Save**.
    

The following are example endpoint policies for accessing Amazon S3.

###### Example: Restrict Access to a Specific Bucket

You can create a policy that restricts access to specific S3 buckets only. This is useful if you have other AWS services in your VPC that use S3 buckets.

```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "Allow-access-to-specific-bucket",
      "Effect": "Allow",
      "Principal": "*",
      "Action": [
         "s3:ListBucket",
         "s3:GetObject",
         "s3:PutObject"
      ],
      "Resource": [
        "arn:aws:s3:::bucket_name",
        "arn:aws:s3:::bucket_name/*"
      ]
    }
  ]
}
```

###### Example: Restrict Access to a Specific IAM Role
You can create a policy that restricts access to a specific IAM role. You must use `aws:PrincipalArn` to grant access to a principal.
```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "Allow-access-to-specific-IAM-role",
      "Effect": "Allow",
      "Principal": "*",
      "Action": "*",
      "Resource": "*",
      "Condition": {
        "ArnEquals": {
          "aws:PrincipalArn": "arn:aws:iam::111122223333:role/role_name"
        }
      }
    }
  ]
}
```

###### Example: Restrict Access to Users in a Specific account
You can create a policy that restricts access to a specific account.
```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "Allow-callers-from-specific-account",
      "Effect": "Allow",
      "Principal": "*",
      "Action": "*",
      "Resource": "*",
      "Condition": {
        "StringEquals": {
          "aws:PrincipalAccount": "111122223333"
        }
      }
    }
  ]
}
```

### Delete a Gateway Endpoint
When you are finished with a gateway endpoint, you can delete it. When you delete a gateway endpoint, we remove the endpoint route from the subnet route tables.

You can't delete a gateway endpoint if private DNS is enabled.
###### To Delete a Gateway Endpoint Using the Console
1. Open the Amazon VPC console at [https://console.aws.amazon.com/vpc/](https://console.aws.amazon.com/vpc/).
2. In the navigation pane, choose **Endpoints**.
3. Select the gateway endpoint.
4. Choose **Actions**, **Delete VPC endpoints**.
5. When prompted for confirmation, enter `delete`.
6. Choose **Delete**.
###### To Delete a Gateway Endpoint Using the Command line
- [delete-vpc-endpoints](https://docs.aws.amazon.com/cli/latest/reference/ec2/delete-vpc-endpoints.html) (AWS CLI)


### Gateway Endpoints for Amazon DynamoDB
[Endpoints for DynamoDB](https://docs.aws.amazon.com/vpc/latest/privatelink/vpc-endpoints-ddb.html)

### Access SaaS Products through AWS PrivateLink
[Access SaaS products](https://docs.aws.amazon.com/vpc/latest/privatelink/privatelink-access-saas.html)


### Access Virtual Appliances through AWS PrivateLink
[Access virtual appliances](https://docs.aws.amazon.com/vpc/latest/privatelink/vpce-gateway-load-balancer.html)

### Create an Inspection System as a Gateway Load Balancer Endpoint Service
[Create a Gateway Load Balancer endpoint service](https://docs.aws.amazon.com/vpc/latest/privatelink/create-gateway-load-balancer-endpoint-service.html)

