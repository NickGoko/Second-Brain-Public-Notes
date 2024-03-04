---
tags:
  - cloud/aws
---


https://aws.amazon.com/route53/  
![](https://i.imgur.com/yP8duuJ.png)  
![](https://i.imgur.com/o8RsPBg.png)


A private hosted zone is a container. It holds information about how you want Route53 to respond to DNS queries for a domain and its sub domains within one or more Amazon VPCs. 

Amazon Route 53 is a highly available and scalable Domain Name System (DNS) service.

Amazon Route 53 offers the following functions:
- Domain name registry.
- DNS resolution.
- Health checking of resources.

Route 53 can perform any combination of these functions.

Route 53 provides a worldwide distributed DNS service.

Route 53 is located alongside all edge locations.

Health checks verify Internet connected resources are reachable, available, and functional.

Route 53 can be used to route Internet traffic for domains registered with another domain registrar (any domain).

When you register a domain with Route 53 it becomes the authoritative DNS server for that domain and creates a public hosted zone.

To make Route 53 the authoritative DNS for an existing domain without transferring the domain create a Route 53 public hosted zone and change the DNS Name Servers on the existing provider to the Route 53 Name Servers.

Changes to Name Servers may not take effect for up to 48 hours due to the DNS record Time To Live (TTL) values.

You can transfer domains to Route 53 only if the Top-Level Domain (TLD) is supported.

You can transfer a domain from Route 53 to another registrar by contacting AWS support.

You can transfer a domain to another account in AWS however it does not migrate the hosted zone by default (optional).

It is possible to have the domain registered in one AWS account and the hosted zone in another AWS account.

Primarily uses UDP port 53 (can use TCP).

AWS offer a 100% uptime SLA for Route 53.

You can control management access to your Amazon Route 53 hosted zone by using IAM.

There is a default limit of 50 domain names, but this can be increased by contacting support.

Private DNS is a Route 53 feature that lets you have authoritative DNS within your VPCs without exposing your DNS records (including the name of the resource and its IP address(es) to the Internet.

You can use the AWS Management Console or API to register new domain names with Route 53.  
![](https://i.imgur.com/iw5r2yb.png)  
![](https://i.imgur.com/oX344Mw.png)  
![](https://i.imgur.com/IrMopDH.png)
  
![](https://i.imgur.com/qPUC9iQ.png)  
![](https://i.imgur.com/cjEwf7H.png)  
![](https://i.imgur.com/axYVINp.png)  
![](https://i.imgur.com/wjKMxqz.png)

![](https://i.imgur.com/45QLF7D.png)


![[Pasted image 20240229222928.png]]
## Hosted Zones

A hosted zone is a collection of records for a specified domain.

A hosted zone is analogous to a traditional DNS zone file; it represents a collection of records that can be managed together.

There are two types of zones:

- Public host zone – determines how traffic is routed on the Internet.
- Private hosted zone for VPC – determines how traffic is routed within VPC (resources are not accessible outside the VPC).

Amazon Route 53 automatically creates the Name Server (NS) and Start of Authority (SOA) records for the hosted zones.

Amazon Route 53 creates a set of 4 unique name servers (a delegation set) within each hosted zone.

You can create multiple hosted zones with the same name and different records.

NS servers are specified by Fully Qualified Domain Name (FQDN), but you can get the IP addresses from the command line (e.g. dig or nslookup).

For private hosted zones you can see a list of VPCs in each region and must select one.

For private hosted zones you must set the following VPC settings to “true”:

- enableDnsHostname.
- enableDnsSupport.

You also need to create a DHCP options set.

You can extend an on-premises DNS to VPC.

You cannot extend Route 53 to on-premises instances.

You cannot automatically register EC2 instances with private hosted zones (would need to be scripted).

Health checks check the instance health by connecting to it.

Health checks can be pointed at:

- Endpoints.
- Status of other health checks.
- Status of a CloudWatch alarm.

Endpoints can be IP addresses or domain names.

You can associate the Route 53 private hosted zone in one account with a VPC in another account.

To associate a Route 53 private hosted zone in one AWS account (Account A) with a virtual private cloud that belongs to another AWS account (Account B), follow these steps using the AWS CLI:

1. From an instance in Account A, authorize the association between the private hosted zone in Account A and the virtual private cloud in Account B.
2. From an instance in Account B, create the association between the private hosted zone in Account A and the virtual private cloud in Account B.
3. Delete the association authorization after the association is created.

## Health Checks

Health checks check the instance health by connecting to it.

Health checks can be pointed at:  
	- Endpoints.  
	- Status of other health checks.  
	- Status of a CloudWatch alarm.

- Endpoints can be IP addresses or domain names.

You can create the following types of health checks:

- **HTTP**: Route 53 tries to establish a TCP connection. If successful, Route 53 submits an HTTP request and waits for an HTTP status code of 200 or greater and less than 400.
- **HTTPS**: Route 53 tries to establish a TCP connection. If successful, Route 53 submits an HTTPS request and waits for an HTTP status code of 200 or greater and less than 400.
- **HTTP_STR_MATCH**: Route 53 tries to establish a TCP connection. If successful, Route 53 submits an HTTP request and searches the first 5,120 bytes of the response body for the string that you specify in SearchString.
- **HTTPS_STR_MATCH**: Route 53 tries to establish a TCP connection. If successful, Route 53 submits an HTTPS request and searches the first 5,120 bytes of the response body for the string that you specify in SearchString.
- **TCP**: Route 53 tries to establish a TCP connection.
- **CLOUDWATCH_METRIC**: The health check is associated with a CloudWatch alarm. If the state of the alarm is OK, the health check is considered healthy. If the state is ALARM, the health check is considered unhealthy. If CloudWatch doesn’t have sufficient data to determine whether the state is OK or ALARM, the health check status depends on the setting for InsufficientDataHealthStatus: Healthy, Unhealthy, or LastKnownStatus.
- **CALCULATED**: For health checks that monitor the status of other health checks, Route 53 adds up the number of health checks that Route 53 health checkers consider to be healthy and compares that number with the value of HealthThreshold.

## Records

Amazon Route 53 currently supports the following DNS record types:

- A (address record).
- AAAA (IPv6 address record).
- CNAME (canonical name record).
- CAA (certification authority authorization).
- MX (mail exchange record).
- NAPTR (name authority pointer record).
- NS (name server record).
- PTR (pointer record).
- SOA (start of authority record).
- SPF (sender policy framework).
- SRV (service locator).
- TXT (text record).
- Alias (an Amazon Route 53-specific virtual record).

<mark style="background: #FFB86CA6;">The Alias record is a Route 53 specific record type.</mark>

Alias records are used to map resource record sets in your hosted zone to Amazon Elastic Load Balancing load balancers, Amazon CloudFront distributions, AWS Elastic Beanstalk environments, or Amazon S3 buckets that are configured as websites.

You can use Alias records to map custom domain names (such as api.example.com) both to API Gateway custom regional APIs and edge-optimized APIs and to Amazon VPC interface endpoints.

The Alias is pointed to the DNS name of the service.

You cannot set the TTL for Alias records for ELB, S3, or Elastic Beanstalk environment (uses the service’s default).

Alias records work like a CNAME record in that you can map one DNS name (e.g. example.com) to another ‘target’ DNS name (e.g. elb1234.elb.amazonaws.com).

An Alias record can be used for resolving apex / naked domain names (e.g. example.com rather than sub.example.com).

A CNAME record can’t be used for resolving apex / naked domain names.

Generally use an Alias record where possible.

Route 53 supports wildcard entries for all record types, except NS records.

The following table details the differences between Alias and CNAME records:

|   |   |
|---|---|
|**CNAME Records**|**Alias Records**|
|Route 53 charges for CNAME queries|Route 53 doesn’t charge for alias queries to AWS resources|
|You can’t create a CNAME record at the top node of a DNS namespace (zone apex)|You can create an alias record at the zone apex (however you can’t route to a CNAME at the zone apex)|
|A CNAME record redirects queries for a domain name regardless of record type|Route 53 follows the pointer in an alias record only when the record type also matches|
|A CNAME can point to any DNS record that is hosted anywhere|An alias record can only point to a CloudFront distribution, Elastic Beanstalk environment, ELB, S3 bucket as a static website, or to another record in the same hosted zone that you’re creating the alias record in|
|A CNAME record is visible in the answer section of a reply from a Route 53 DNS server|An alias record is only visible in the Route 53 console or the Route 53 API|
|A CNAME record is followed by a recursive resolver|An alias record is only followed inside Route 53. This means that both the alias record and its target must exist in Route 53|

## Routing Policies

Routing policies determine how Route 53 responds to queries.

The following table highlights the key function of each type of routing policy:

|   |   |
|---|---|
|**Policy**|**What it Does**|
|Simple|Simple DNS response providing the IP address associated with a name|
|Failover|If primary is down (based on health checks), routes to secondary destination|
|**Geolocation**|Uses geographic location you’re in (e.g. Europe) to route you to the closest region|
|**Geoproximity**|<mark style="background: #ADCCFFA6;">Routes you to the closest region within a geographic area</mark> |
|**Latency**|<mark style="background: #FFF3A3A6;">Directs you based on the lowest latency route to resources</mark> |
|**Multivalue answer**|Returns several IP addresses and functions as a basic load balancer|
|**Weighted**|Uses the relative weights assigned to resources to determine which to route to|

### Simple Routing Policy

- An A record is associated with one or more IP addresses.
- Uses round robin.
- Does not support health checks.

The following diagram depicts an Amazon Route 53 Simple routing policy configuration:

![Amazon Route 53 Simple Routing Policy](https://digitalcloud.training/wp-content/uploads/2022/01/amazon-route-53-simple-routing-policy.jpeg)

Failover:
- Failover to a secondary IP address.
- Associated with a health check.
- Used for active-passive.
- Routes only when the resource is healthy.
- Can be used with ELB.
- When used with Alias records set Evaluate Target Health to “Yes” and do not use health checks.

The following diagram depicts an Amazon Route 53 Failover routing policy configuration:

![Amazon Route 53 Failover Routing Policy](https://digitalcloud.training/wp-content/uploads/2022/01/amazon-route-53-failover-routing-policy.jpeg)

![](https://i.imgur.com/vBgjpJ1.png)


### Geo-location Routing Policy

- <mark style="background: #FFB86CA6;">Caters to different users in different countries and different languages</mark>.
- Contains users within a particular geography and offers them a customized version of the workload based on their specific needs.
- Geolocation can be used for localizing content and presenting some or all your website in the language of your users.
- Can also protect distribution rights.
- Can be used for spreading load evenly between regions.
- If you have multiple records for overlapping regions, Route 53 will route to the smallest geographic region.
- You can create a default record for IP addresses that do not map to a geographic location.

The following diagram depicts an Amazon Route 53 Geolocation routing policy configuration:

![Amazon Route 53 Geolocation Routing Policy](https://digitalcloud.training/wp-content/uploads/2022/01/amazon-route-53-geolocation-routing-policy.jpeg)

Geo-proximity routing policy (requires Route Flow):
- <mark style="background: #BBFABBA6;">Use for routing traffic based on the location of resources and, optionally, shift traffic from resources in one location to resources in another</mark>.  

![[Pasted image 20240210194211.png]]
### Latency Routing Policy

AWS maintains a database of latency from different parts of the world.

- <mark style="background: #BBFABBA6;">Focused on improving performance by routing to the region with the lowest latency</mark>.
- You create latency records for your resources in multiple EC2 locations.
- Latency-based Routing Policy <mark style="background: #FFB86CA6;">helps respond to the DNS query based on which data center gives the user the lowest network latency</mark>.
- Latency-based routing policy can be used when there are multiple resources performing the same function and <mark style="background: #ADCCFFA6;">Route 53 needs to be configured to respond to the DNS queries with the resources that provide the fastest response with the lowest latency</mark>.

- **Latency between hosts on the Internet can change over time as a result of changes in network connectivity and routing. Latency-based routing is based on latency measurements performed over a period of time, and the measurements reflect these changes** _for e.g. if the latency from the user in Singapore to Ireland improves, the user can be routed to Ireland_
- Latency-based routing cannot guarantee users from the same geographic will be served from the same location for any compliance reason  
The following diagram depicts an Amazon Route 53 Latency based routing policy configuration:

![Amazon Route 53 Latency Routing Policy](https://digitalcloud.training/wp-content/uploads/2022/01/amazon-route-53-latency-routing-policy.jpeg)

### Multi-value Answer Routing Policy
- Use for responding to DNS queries with up to eight healthy records selected at random.  
![](https://i.imgur.com/W49I5zc.png)

### Weighted Routing Policy
- Like simple but you can specify a weight per IP address.
- You create records that have the same name and type and assign each record a relative weight.
- Numerical value that favors one IP over another.
- To stop sending traffic to a resource you can change the weight of the record to 0.

The following diagram depicts an Amazon Route 53 Weighted routing policy configuration:

![Amazon Route 53 Weighted Routing Policy](https://digitalcloud.training/wp-content/uploads/2022/01/amazon-route-53-weighted-routing-policy.jpeg)

## Traffic Flow

Route 53 Traffic Flow provides Global Traffic Management (GTM) services.

Traffic flow policies allow you to create routing configurations for resources using routing types such as **failover** and **geolocation**.

Create policies that route traffic based on specific constraints, including latency, endpoint health, load, geo-proximity, and geography.

Scenarios include:
- Adding a simple backup page in Amazon S3 for a website.
- Building sophisticated routing policies that consider an end user’s geographic location, proximity to an AWS region, and the health of each of your endpoints.

<mark style="background: #FF5582A6;">Amazon Route 53 Traffic Flow also includes a versioning feature that allows you to maintain a history of changes to your routing policies, and easily roll back to a previous policy version using the console or API.</mark>

## Route 53 Resolver

**Route 53 Resolver** is <mark style="background: #BBFABBA6;">a set of features that enable bi-directional querying between on-premises and AWS over private connections.</mark>
- Used for enabling DNS resolution for hybrid clouds.

Route 53 Resolver Endpoints.
- **Inbound query capability** is provided by Route 53 Resolver Endpoints, allowing DNS queries that originate on-premises to resolve AWS hosted domains.
- Connectivity needs to be established between your on-premises DNS infrastructure and AWS through a Direct Connect (DX) or a Virtual Private Network (VPN).
- Endpoints are configured through IP address assignment in each subnet for which you would like to provide a resolver.

![Amazon Route 53 Resolver Inbound Endpoints](https://digitalcloud.training/wp-content/uploads/2022/01/amazon-route-53-resolver-inbound-endpoints.jpeg)

Conditional forwarding rules:
- Outbound DNS queries are enabled using Conditional Forwarding Rules. .
- Domains hosted within your on-premises DNS infrastructure can be configured as forwarding rules in Route 53 Resolver.
- Rules will trigger when a query is made to one of those domains and will attempt to forward DNS requests to your DNS servers that were configured along with the rules.
- Like the inbound queries, this requires a private connection over DX or VPN.

![Amazon Route 53 Resolver Outbound Endpoints](https://digitalcloud.training/wp-content/uploads/2022/01/amazon-route-53-resolver-outbound-endpoints.jpeg)

There are a couple of ways to provide resolution of Microsoft Active Directory Domain Controller DNS zones and AWS records:

- Define an outbound Amazon Route 53 Resolver. Set a conditional forwarding rule for the Active Directory domain to the Active Directory servers. Configure the DNS settings in the VPC DHCP options set to use the AmazonProvidedDNS servers.
- Configure the DHCP options set associated with the VPC to assign the IP addresses of the Domain Controllers as DNS servers. Update the DNS service on the Active Directory servers to forward all non-authoritative queries to the VPC Resolver.

## Charges

You pay per hosted zone per month (no partial months).

A hosted zone deleted within 12 hours of creation is not charged (queries are charged).

Additional charges for:

- Queries.
- Traffic Flow.
- Health Checks.
- Route 53 Resolver ENIs + queries.
- Domain names.

Alias records are free of charge when the records are mapped to one of the following:

- Elastic Load Balancers.
- Amazon CloudFront distributions.
- AWS Elastic Beanstalk environments.
- Amazon S3 buckets that are configured as website endpoints.

Health checks are charged with different prices for AWS vs non-AWS endpoints.

You do not pay for the records that you add to your hosted zones.

Latency-based routing queries are more expensive.

Geo DNS and geo-proximity also have higher prices.


![[Module 9 - Implementing Elasticity, High Availability, and Monitoring#Amazon Route 53]]

# FAQ
**Q. What is DNS Failover?**

DNS Failover consists of two components: health checks and failover. Health checks are automated requests sent over the Internet to your application to verify that your application is reachable, available, and functional. You can configure the health checks to be similar to the typical requests made by your users, such as requesting a web page from a specific URL. With DNS failover, Route 53 only returns answers for resources that are healthy and reachable from the outside world, so that your end users are routed away from a failed or unhealthy part of your application.

**Q. How do I get started with DNS Failover?**

Visit the [Amazon Route 53 Developer Guide](http://docs.aws.amazon.com/Route53/latest/DeveloperGuide/health-checks.html) for details on getting started. You can also configure DNS Failover from within the Route 53 Console.

**Q. Does DNS Failover support Elastic Load Balancers (ELBs) as endpoints?**

Yes, you can configure DNS Failover for Elastic Load Balancers (ELBs). To enable DNS Failover for an ELB endpoint, create an Alias record pointing to the ELB and set the “Evaluate Target Health” parameter to true. Route 53 creates and manages the health checks for your ELB automatically. You do not need to create your own Route 53 health check of the ELB. You also do not need to associate your resource record set for the ELB with your own health check, because Route 53 automatically associates it with the health checks that Route 53 manages on your behalf. The ELB health check will also inherit the health of your backend instances behind that ELB. For more details on using DNS Failover with ELB endpoints, please consult the [Route 53 Developer Guide](http://docs.aws.amazon.com/Route53/latest/DeveloperGuide/dns-failover.html).

**Q. Can I configure a backup site to be used only when a health check fails?**

Yes, you can use DNS Failover to maintain a backup site (for example, a static site running on an Amazon S3 website bucket) and fail over to this site in the event that your primary site becomes unreachable.

**Q. What DNS record types can I associate with Route 53 health checks?**

You can associate any record type supported by Route 53 except SOA and NS records.

**Q. Can I health check an endpoint if I don’t know its IP address?**

Yes. You can configure DNS Failover for Elastic Load Balancers and Amazon S3 website buckets via the Amazon Route 53 Console without needing to create a health check of your own. For these endpoint types, Route 53 automatically creates and manages health checks on your behalf which are used when you create an Alias record pointing to the ELB or S3 website bucket and enable the "Evaluate Target Health" parameter on the Alias record.

For all other endpoints, you can specify either the DNS name (e.g. www.example.com) or the IP address of the endpoint when you create a health check for that endpoint.

**Q. One of my endpoints is outside AWS. Can I set up DNS Failover on this endpoint?**  
![](https://i.imgur.com/3NdncX9.png)  
![](https://i.imgur.com/2rFotbC.png)  
![[Pasted image 20240212123437.png]]![[Pasted image 20240212123437.png]]  
Yes. Just like you can create a Route 53 resource record that points to an address outside AWS, you can set up health checks for parts of your application running outside AWS, and you can fail over to any endpoint that you choose, regardless of location. For example, you may have a legacy application running in a datacenter outside AWS and a backup instance of that application running within AWS. You can set up health checks of your legacy application running outside AWS, and if the application fails the health checks, you can fail over automatically to the backup instance in AWS.

**Q. If failover occurs and I have multiple healthy endpoints remaining, will Route 53 consider the load on my healthy endpoints when determining where to send traffic from the failed endpoint?**

No, Route 53 does not make routing decisions based on the load or available traffic capacity of your endpoints. You will need to ensure that you have available capacity at your other endpoints, or the ability to scale at those endpoints, in order to handle the traffic that had been flowing to your failed endpoint.

**Q. How many consecutive health check observations does an endpoint need to fail to be considered “failed”?**

<mark style="background: #FFB86CA6;">The default is a threshold of three health check observations: when an endpoint has failed three consecutive observations</mark>, Route 53 will consider it failed. However, Route 53 will continue to perform health check observations on the endpoint and will resume sending traffic to it once it passes three consecutive observations. You can change this threshold to any value between 1 and 10 observations. For more details, see the [Amazon Route 53 Developer Guide](http://docs.aws.amazon.com/Route53/latest/DeveloperGuide/health-checks-creating-deleting.html).

**Q. When my failed endpoint becomes healthy again, how is the DNS failover reversed?**

After a failed endpoint passes the number of consecutive health check observations that you specify when creating the health check (the default threshold is three observations), Route 53 will restore its DNS records automatically, and traffic to that endpoint will resume with no action required on your part.

**Q. What is the interval between health check observations?**

By default, health check observations are conducted at an interval of 30 seconds. You can optionally select a fast interval of 10 seconds between observations.

By checking three times more often, fast interval health checks enable Route 53 to confirm more quickly that an endpoint has failed, shortening the time required for DNS failover to redirect traffic in response to the endpoint’s failure.

Fast interval health checks also generate three times the number of requests to your endpoint, which may be a consideration if your endpoint has a limited capacity to serve web traffic. Visit the [Route 53 pricing page](http://aws.amazon.com/route53/pricing/) for details on pricing for fast interval health checks and other optional health check features. For more details, see the [Amazon Route 53 Developer Guide](http://docs.aws.amazon.com/Route53/latest/DeveloperGuide/health-checks-creating-deleting.html).

**Q. How much load should I expect a health check to generate on my endpoint (for example, a web server)?**

Each health check is conducted from multiple locations around the world. The number and set of locations is configurable; you can modify the number of locations from which each of your health checks is conducted using the Amazon Route 53 console or API. Each location checks the endpoint independently at the interval that you select: the default interval of 30 seconds, or an optional fast interval of 10 seconds. Based on the current default number of health checking locations, you should expect your endpoint to receive one request every 2-3 seconds on average for standard interval health checks and one or more requests per second for fast-interval health checks.

**Q. Do Route 53 health checks follow HTTP redirects?**

No. Route 53 health checks consider an HTTP 3xx code to be a successful response, so they don’t follow the redirect. This may cause unexpected results for string-matching health checks. The health check searches for the specified string in the body of the redirect. Because the health check doesn’t follow the redirect, it never sends a request to the location that the redirect points to and never gets a response from that location. For string matching health checks, we recommend that you avoid pointing the health check at a location that returns an HTTP redirect.

**Q. What is the sequence of events when failover happens?**

In simplest terms, the following events will take place if a health check fails and failover occurs:

Route 53 conducts a health check of your application. In this example, your application fails three consecutive health checks, triggering the following events.

Route 53 disables the resource records for the failed endpoint and no longer serves these records. This is the failover step, which causes traffic to begin being routed to your healthy endpoint(s) instead of your failed endpoint.

**Q. Do I need to adjust the TTL for my records in order to use DNS Failover?**

The time for which a DNS resolver caches a response is set by a value called the time to live (TTL) associated with every record. We recommend a TTL of 60 seconds or less when using DNS Failover, to minimize the amount of time it takes for traffic to stop being routed to your failed endpoint. In order to configure DNS Failover for ELB and S3 Website endpoints, you need to use Alias records which have fixed TTL of 60 seconds; for these endpoint types, you do not need to adjust TTLs in order to use DNS Failover.

**Q. What happens if all of my endpoints are unhealthy?**

Route 53 can only fail over to an endpoint that is healthy. If there are no healthy endpoints remaining in a resource record set, Route 53 will behave as if all health checks are passing.

**Q. Can I use DNS Failover without using Latency Based Routing (LBR)?**

Yes. You can configure DNS Failover without using LBR. In particular, you can use DNS failover to configure a simple failover scenario where Route 53 monitors your primary website and fails over to a backup site in the event that your primary site is unavailable.

**Q. Can I configure a health check on a site accessible only via HTTPS?**

Yes. Route 53 supports health checks over HTTPS, HTTP or TCP.

**Q. Do HTTPS health checks validate the endpoint’s SSL certificate?**

No, HTTPS health checks test whether it’s possible to connect with the endpoint over SSL and whether the endpoint returns a valid HTTP response code. However, they do not validate the SSL certificate returned by the endpoint.

**Q. Do HTTPS health checks support Server Name Indication (SNI)?**

Yes, HTTPS health checks support SNI.

**Q. How can I use health checks to verify that my web server is returning the correct content?**

You can use Route 53 health checks to check for the presence of a designated string in a server response by selecting the “Enable String Matching” option. This option can be used to check a web server to verify that the HTML it serves contains an expected string. Or, you can create a dedicated status page and use it to check the health of the server from an internal or operational perspective. For more details, see the [Amazon Route 53 Developer Guide](http://docs.aws.amazon.com/Route53/latest/DeveloperGuide/health-checks-creating-deleting.html).

**Q. How do I see the status of a health check that I’ve created?**

You can view the current status of a health check, as well as details on why it has failed, in the Amazon Route 53 console and via the Route 53 API.

Additionally, each health check’s results are published as Amazon CloudWatch metrics showing the endpoint’s health and, optionally, the latency of the endpoint’s response. You can view a graph of the Amazon CloudWatch metric in the health checks tab of the Amazon Route 53 console to see the current and historical status of the health check. You can also create Amazon CloudWatch alarms on the metric in order to send notifications if the status of the health check changes.

The Amazon CloudWatch metrics for all of your Amazon Route 53 health checks are also visible in the Amazon CloudWatch console. Each Amazon CloudWatch metric contains the Health Check ID (for example, 01beb6a3-e1c2-4a2b-a0b7-7031e9060a6a) which you can use to identify which health check the metric is tracking.

**Q. How can I measure the performance of my application’s endpoints using Amazon Route 53?**

Amazon Route 53 health checks include an optional latency measurement feature which provides data on how long it takes your endpoint to respond to a request. When you enable the latency measurement feature, the Amazon Route 53 health check will generate additional Amazon CloudWatch metrics showing the time required for Amazon Route 53’s health checkers to establish a connection and to begin receiving data. Amazon Route 53 provides a separate set of latency metrics for each AWS region where Amazon Route 53 health checks are conducted.

**Q. How can I be notified if one of my endpoints starts failing its health check?**

Because each Route 53 health check publishes its results as a CloudWatch metric, you can configure the full range of CloudWatch notifications and automated actions which can be triggered when the health check value changes beyond a threshold that you specify. First, in either the Route 53 or CloudWatch console, configure a CloudWatch alarm on the health check metric. Then add a notification action and specify the email or SNS topic that you want to publish your notification to. Please consult the [Route 53 Developer Guide](http://docs.aws.amazon.com/Route53/latest/DeveloperGuide/monitoring-health-checks.html) for full details.

**Q: I created an alarm for my health check, but I need to re-send the confirmation email for the alarm's SNS topic. How can I re-send this email?**

Confirmation emails can be re-sent from the SNS console. To find the name of the SNS topic associated with the alarm, click the alarm name within the Route 53 console and looking in the box labeled "Send notification to."

Within the SNS console, expand the list of topics, and select the topic from your alarm. Open the "Create Subscription" box and select Email for protocol and enter the desired email address. Clicking "Subscribe" will re-send the confirmation email.

**Q. I’m using DNS Failover with Elastic Load Balancers (ELBs) as endpoints. How can I see the status of these endpoints?**

The recommended method for setting up DNS Failover with ELB endpoints is to use Alias records with the "Evaluate Target Health" option. Because you don't create your own health checks for ELB endpoints when using this option, there are no specific CloudWatch metrics generated by Route 53 for these endpoints.

You can get metrics on the health of your load balancer in two ways. First, Elastic Load Balancing publishes metrics that indicate the health of the load balancer and the number of healthy instances behind it. For details on configuring CloudWatch metrics for ELB, consult the [ELB developer guide](http://docs.aws.amazon.com/ElasticLoadBalancing/latest/DeveloperGuide/US_MonitoringLoadBalancerWithCW.html). Second, you can create your own health check against the CNAME provided by the ELB, e.g. elb-example-123456678.us-west-2.elb.amazonaws.com. You won’t use this health check for DNS Failover itself (because the “Evaluate Target Health” option provides DNS Failover for you), but you can view the CloudWatch metrics for this health check and create alarms to be notified if the health check fails.

For complete details on using DNS Failover with ELB endpoints, please consult the [Route 53 Developer Guide](http://docs.aws.amazon.com/Route53/latest/DeveloperGuide/dns-failover.html).

**Q. For Alias records pointing to Amazon S3 Website buckets, what is being health checked when I set Evaluate Target Health to “true”?**

Amazon Route 53 performs health checks of the Amazon S3 service itself in each AWS region. When you enable Evaluate Target Health on an Alias record pointing to an Amazon S3 Website bucket, Amazon Route 53 will take into account the health of the Amazon S3 service in the AWS region where your bucket is located. Amazon Route 53 does not check whether a specific bucket exists or contains valid website content; Amazon Route 53 will only fail over to another location if the Amazon S3 service itself is unavailable in the AWS region where your bucket is located.

**Q. What is the cost to use CloudWatch metrics for my Route 53 health checks?**

CloudWatch metrics for Route 53 health checks are available free of charge.

**Q. Can I configure DNS Failover based on internal health metrics, such as CPU load, network, or memory?**

Yes. Amazon Route 53’s metric based health checks let you perform DNS failover based on any metric that is available within Amazon CloudWatch, including AWS-provided metrics and custom metrics from your own application. When you create a metric based health check within Amazon Route 53, the health check becomes unhealthy whenever its associated Amazon CloudWatch metric enters an alarm state.

Metric based health checks are useful to enable DNS failover for endpoints that cannot be reached by a standard Amazon Route 53 health check, such as instances within a Virtual Private Cloud (VPC) that only have private IP addresses. Using Amazon Route 53’s calculated health check feature, you can also accomplish more sophisticated failover scenarios by combining the results of metric based health checks with the results of standard Amazon Route 53 health checks, which make requests against an endpoint from a network of checkers around the world. For example, you can create a configuration which fails away from an endpoint if either its public-facing web page is unavailable, or if internal metrics such as CPU load, network in/out, or disk reads show that the server itself is unhealthy.

**Q. My web server is receiving requests from a Route 53 health check that I did not create. How can I stop these requests?**

Occasionally, Amazon Route 53 customers create health checks that specify an IP address or domain name that does not belong to them. If your web server is getting unwanted HTTP(s) requests that you have traced to Amazon Route 53 health checks, please provide information on the unwanted health check [using this form](https://aws.amazon.com/forms/route53-unwanted-healthchecks), and we will work with our customer to fix the problem.

**Q. If I specify a domain name as my health check target, will Amazon Route 53 check over IPv4 or IPv6?**

If you specify a domain name as the endpoint of an Amazon Route 53 health check, Amazon Route 53 will look up the IPv4 address of that domain name and will connect to the endpoint using IPv4. Amazon Route 53 will not attempt to look up the IPv6 address for an endpoint that is specified by domain name. If you want to perform a health check over IPv6 instead of IPv4, select "IP address" instead of "domain name" as your endpoint type, and enter the IPv6 address in the “IP address” field.

**Q. Where can I find the IPv6 address ranges for Amazon Route 53’s DNS servers and health checkers?**

AWS now publishes its current IP address ranges in JSON format. To view the current ranges, download the .json file using the following link. If you access this file programmatically, ensure that the application downloads the file only after successfully verifying the TLS certificate that is returned by the AWS server.

Download: [ip-ranges.json](https://ip-ranges.amazonaws.com/ip-ranges.json)

To find IP ranges for Route 53 servers, search for the following values in the "service" field:

Route 53 DNS servers: Search for "ROUTE53"

Route 53 health checkers: Search for "ROUTE53\_HEALTHCHECKS"

For more information, see [AWS IP Address Ranges](http://docs.aws.amazon.com/general/latest/gr/aws-ip-ranges.html) in the Amazon Web Services General Reference.

Please note that the IPv6 ranges may not yet appear in this file. For reference, the IPv6 ranges for Amazon Route 53 health checkers are as follows:

2600:1f1c:7ff:f800::/53  
2a05:d018:fff:f800::/53  
2600:1f1e:7ff:f800::/53  
2600:1f1c:fff:f800::/53  
2600:1f18:3fff:f800::/53  
2600:1f14:7ff:f800::/53  
2600:1f14:fff:f800::/53  
2406:da14:7ff:f800::/53  
2406:da14:fff:f800::/53  
2406:da18:7ff:f800::/53  
2406:da1c:7ff:f800::/53  
2406:da1c:fff:f800::/53  
2406:da18:fff:f800::/53  
2600:1f18:7fff:f800::/53  
2a05:d018:7ff:f800::/53  
2600:1f1e:fff:f800::/53  
2620:107:300f::36b7:ff80/122  
2a01:578:3::36e4:1000/122  
2804:800:ff00::36e8:2840/122  
2620:107:300f::36f1:2040/122  
2406:da00:ff00::36f3:1fc0/122  
2620:108:700f::36f4:34c0/122  
2620:108:700f::36f5:a800/122  
2400:6700:ff00::36f8:dc00/122  
2400:6700:ff00::36fa:fdc0/122  
2400:6500:ff00::36fb:1f80/122  
2403:b300:ff00::36fc:4f80/122  
2403:b300:ff00::36fc:fec0/122  
2400:6500:ff00::36ff:fec0/122  
2406:da00:ff00::6b17:ff00/122  
2a01:578:3::b022:9fc0/122  
2804:800:ff00::b147:cf80/122

## Domain Name Registration

**Q. Can I register domain names with Amazon Route 53?**

Yes. You can use the AWS Management Console or API to register new domain names with Route 53. You can also request to transfer in existing domain names from other registrars to be managed by Route 53. Domain name registration services are provided under our [Domain Name Registration Agreement](https://aws.amazon.com/route53/domain-registration-agreement/).

**Q. What Top Level Domains (“TLDs”) do you offer?**

Route 53 offers a wide selection of both generic Top Level Domains (“gTLDs”: for example, .com and .net) and country-code Top Level Domains (“ccTLDs”: for example, .de and .fr). For the complete list, please see the [Route 53 Domain Registration Price List](https://d32ze2gidvkk54.cloudfront.net/Amazon_Route_53_Domain_Registration_Pricing_20140731.pdf).

**Q. How can I register a domain name with Route 53?**

To get started, log into your account and click on “Domains”. Then, click the big blue “Register Domain” button and complete the registration process.

**Q. How long does it take to register a domain name?**

Depending on the TLD you’ve selected, registration can take from a few minutes to several hours. Once the domain is successfully registered, it will show up in your account.

**Q. How long is my domain name registered for?**

The initial registration period is typically one year, although the registries for some top-level domains (TLDs) have longer registration periods. When you register a domain with Amazon Route 53 or you transfer domain registration to Amazon Route 53, we configure the domain to renew automatically. For more information, see [Renewing Registration](http://docs.aws.amazon.com/Route53/latest/DeveloperGuide/domain-renew.html) for a Domain in the Amazon Route 53 Developer Guide.

**Q. What information do I need to provide to register a domain name?**

In order to register a domain name, you need to provide contact information for the registrant of the domain, including name, address, phone number, and email address. If the administrative and technical contacts are different, you need to provide that contact information, too.

**Q. Why do I need to provide personal information to register a domain?**

ICANN, the governing body for domain registration, requires that registrars provide contact information, including name, address, and phone number, for every domain name registration, and that registrars make this information publicly available via a Whois database. For domain names that you register as an individual (i.e., not as a company or organization), Route 53 provides privacy protection, which hides your personal phone number, email address, and physical address, free of charge. Instead, the Whois contains the registrar’s name and mailing address, along with a registrar-generated forwarding email address that third parties may use if they wish to contact you.

**Q. Does Route 53 offer privacy protection for domain names I have registered?**

Yes, Route 53 provides privacy protection at no additional charge. The privacy protection hides your phone number, email address, and physical address. Your first and last name will be hidden if the TLD registry and registrar allow it. When you enable privacy protection, a Whois query for the domain will contain the registrar’s mailing address in place of your physical address, and the registrar’s name in place of your name (if allowed). Your email address will be a registrar-generated forwarding email address that third parties may use if they wish to contact you. Domain names registered by companies or organizations are eligible for privacy protection if the TLD registry and registrar allow it.

**Q. Where can I find the requirements for specific TLDs?**

For a list of TLDs please see the [price list](https://d32ze2gidvkk54.cloudfront.net/Amazon_Route_53_Domain_Registration_Pricing_20140731.pdf) and for the specific registration requirements for each, please see the [Amazon Route 53 Developer Guide](http://docs.aws.amazon.com/Route53/latest/DeveloperGuide/registrar-tld-list.html) and our [Domain Name Registration Agreement](https://aws.amazon.com/route53/domain-registration-agreement/).

**Q. What name servers are used to register my domain name?**

When your domain name is created we automatically associate your domain with four unique Route 53 name servers, known as a delegation set. You can view the delegation set for your domain in the Amazon Route 53 console. They're listed in the hosted zone that we create for you automatically when you register a domain.

By default, Route 53 will assign a new, unique delegation set for each hosted zone you create. However, you can also use the Route 53 API to create a “reusable delegation set”, which you can then apply to multiple hosted zones that you create. For customers with large numbers of domain names, reusable delegation sets make migration to Route 53 simple, because you can instruct your domain name registrar to use the same delegation set for all your domains managed by Route 53. This feature also makes it possible for you to create “white label” name server addresses such as ns1.example.com, ns2.example.com, etc., which you can point to your Route 53 name servers. You can then use your “white label” name server addresses as the authoritative name servers for as many of your domain names as desired. For more details, see the [Amazon Route 53 documentation](http://docs.aws.amazon.com/Route53/latest/APIReference/actions-on-reusable-delegation-sets.html).

**Q. Will I be charged for my name servers?**

You will be charged for the hosted zone that Route 53 creates for your domain name, as well as for the DNS queries against this hosted zone that Route 53 serves on your behalf. If you do not wish to be charged for Route 53’s DNS service, you can delete your Route 53 hosted zone. Please note that some TLDs require you to have valid name servers as part of your domain name registration. For a domain name under one of these TLDs, you will need to procure DNS service from another provider and enter that provider’s name server addresses before you can safely delete your Route 53 hosted zone for that domain name.

**Q. What is Amazon Registrar, Inc. and what is a registrar of record?**

AWS resells domain names that are registered with ICANN-accredited registrars. Amazon Registrar, Inc. is an Amazon company that is accredited by ICANN to register domains. The registrar of record is the “Sponsoring Registrar” listed in the WHOIS record for your domain to indicate which registrar your domain is registered with.

**Q. Who is Gandi?**

Amazon is a reseller of the registrar Gandi. As the registrar of record, Gandi is required by ICANN to contact the registrant to verify their contact information at the time of initial registration. You MUST verify your contact information if requested by Gandi within the first 15 days of registration in order to prevent your domain name from being suspended. Gandi also sends out reminder notices before the domain comes up for renewal.

**Q. Which top-level domains does Amazon Route 53 register through Amazon Registrar and which ones does it register through Gandi?**

See our [documentation](http://docs.aws.amazon.com/Route53/latest/DeveloperGuide/registrar-tld-list.html) for a list of the domains that you can currently register using Amazon Route 53. This list includes information about which registrar is the current registrar of record for each TLD that we sell.

**Q. What is Whois? Why is my information shown in Whois?**

Whois is a publicly available database for domain names that lists the contact information and the name servers that are associated with a domain name. Anyone can access the Whois database by using the WHOIS command, which is widely available. It's included in many operating systems, and it's also available as a web application on many websites. The Internet Corporation for Assigned Names and Numbers (ICANN) requires that all domain names have publicly available contact information in case someone needs to get in contact with the domain name holder.

**Q. How do I transfer my domain name to Route 53?**

To get started, log into your account and click on “Domains”. Then, click the “Transfer Domain” button at the top of the screen and complete the transfer process. Please make sure before you start the transfer process, (1) your domain name is unlocked at your current registrar, (2) you have disabled privacy protection on your domain name (if applicable), and (3) that you have obtained the valid Authorization Code, or “authcode”, from your current registrar which you will need to enter as part of the transfer process.

**Q. How do I transfer my existing domain name registration to Amazon Route 53 without disrupting my existing web traffic?**

First, you need to get a list of the DNS record data for your domain name, generally available in the form of a “zone file” that you can get from your existing DNS provider. With the DNS record data in hand, you can use Route 53’s Management Console or simple web-services interface to create a hosted zone that can store the DNS records for your domain name and follow its transfer process, which will include such steps as updating the name servers for your domain name to the ones associated with your hosted zone. To complete the domain name transfer process, contact the registrar with whom you registered your domain name and follow its transfer process, which will include steps such as updating the name servers for your domain name to the ones associated with your hosted zone. As soon as your registrar propagates the new name server delegations, the DNS queries from your end users will start to get answered by the Route 53 DNS servers.

**Q. How do I check on the status of my transfer request?**

You can view the status of domain name transfers in the “Alerts” section on the homepage of the Route 53 console.

**Q. What do I do if my transfer wasn’t successful?**

You will need to contact your current registrar in order to determine why your transfer failed. Once they have resolved the issue, you can resubmit your transfer request.

**Q. How do I transfer my domain name to a different registrar?**

In order to move your domain name away from Route 53, you need to initiate a transfer request with your new registrar. They will request the domain name be moved to their management.

**Q. Is there a limit to the number of domains I can manage using Amazon Route 53?**

Each new Amazon Route 53 account is limited to a maximum of 50 domains. Complete our [request form for a higher limit](https://aws.amazon.com/route53-request/) and we will respond to your request within two business days.

**Q. Does Amazon Route 53 DNS support DNSSEC?**

Yes. You can enable DNSSEC signing for existing and new public hosted zones.  

**Q. How do I transfer a domain registration that has DNSSEC enabled to Amazon Route 53?**

See our [documentation](http://docs.aws.amazon.com/Route53/latest/DeveloperGuide/domain-configure-dnssec.html) for a step-by-step guide on transferring your DNSSEC-enabled domain to Amazon Route 53.  

## Route 53 Resolver

**Q. What is Amazon Route 53 Resolver?**

Route 53 Resolver is a regional DNS service that provides recursive DNS lookups for names hosted in EC2 as well as public names on the internet. This functionality is available by default in every Amazon Virtual Private Cloud (VPC). For hybrid cloud scenarios you can configure conditional forwarding rules and DNS endpoints to enable DNS resolution across AWS Direct Connect and AWS Managed VPN.

**Q. What is recursive DNS?**

Amazon Route 53 is both an Authoritative DNS service and Recursive DNS service. Authoritative DNS contains the final answer to a DNS query, generally an IP address. Clients (such as mobile devices, applications running in the cloud, or servers in your datacenter) don’t actually talk directly to authoritative DNS services, except in very rare cases. Instead, clients talk to recursive DNS services (also known as DNS resolvers) which find the correct authoritative answer for any DNS query. Route 53 Resolver is a recursive DNS service.

When receiving a query, a recursive DNS service like Route 53 Resolver may either be configured to automatically forward the query directly to a specific recursive DNS server, or it may recursively search beginning with the root of the domain and continuing until it finds the final answer. In either case, once an answer is found, the recursive DNS server may cache the answer for a period of time so it can answer subsequent queries for the same name more quickly in the future.

**Q. What are conditional forwarding rules?**

Conditional forwarding rules allow Resolver to forward queries for specified domains to the target IP address of your choice, typically an on-premises DNS resolver. Rules are applied at the VPC level and can be managed from one account and shared across multiple accounts.

**Q. What are DNS endpoints?**

A DNS endpoint includes one or more elastic network interfaces (ENI) that attach to your Amazon Virtual Private Cloud (VPC). Each ENI is assigned an IP address from the subnet space of the VPC where it is located. This IP address can then serve as a forwarding target for on-premises DNS servers to forward queries. Endpoints are required both for DNS query traffic that you're forwarding from VPCs to your network and from your network to your VPCs over AWS Direct Connect and Managed VPN.  

**Q. How do I share rules across accounts?**

Route 53 Resolver is integrated with AWS Resource Access Manager (RAM) which provides customers with a simple way to share their resources across AWS accounts or within their AWS Organization. Rules can be created in one primary account and then shared across multiple accounts using RAM. Once shared, the rules still need to be applied to VPCs in those accounts before they can take effect. For more information, see the AWS RAM [documentation](https://docs.aws.amazon.com/ram/index.html#lang/en_us).  

**Q. What happens if I decide to stop sharing rules with other accounts?**

Those rules will no longer be usable by the accounts you previously shared them with. This means that if those rules were associated to VPCs in those accounts, they will be disassociated from those VPCs.

**Q. What regions are available for Route 53 Resolver?**

Visit our [AWS Region Table](https://aws.amazon.com/about-aws/global-infrastructure/regional-product-services/) to see which regions Route 53 Resolver has launched in.

**Q. Does regional support for Route 53 Resolver mean that all of Amazon Route 53 is now regional?**

No. Amazon Route 53 public and private DNS, traffic flow, health checks, and domain name registration are all global services.

**Q. How can I use Route 53 Resolver on Outposts?**

You can use Route 53 Resolver to resolve Domain Name Server (DNS) queries locally on [AWS Outposts racks](https://aws.amazon.com/outposts/rack/), improving the availability and performance of your on-premises applications. When you enable Route 53 Resolver on Outposts, Route 53 automatically stores DNS responses on Outposts racks and provides continued DNS resolution for your applications even during unexpected network disconnects to the parent AWS Region. By serving DNS responses locally, Route 53 Resolver on Outposts also enables low-latency DNS  
resolution, improving the performance of your on-premises applications.

In addition, you can connect the Route 53 Resolvers on Outposts racks with DNS servers in your on-premises data centers through Route 53 Resolver endpoints. This enables resolution of DNS queries between the Outposts racks and your other on-premises resources.

**Q. How do I get started with Route 53 Resolver?**

Visit the Amazon Route 53 [developer guide](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/resolver.html) for details on getting started. You can also configure Resolver from within the Amazon Route 53 console.

**Q. Does Route 53 Resolver support DNS over HTTPS (DoH)?**

Yes, Amazon Route 53 Resolver supports using the DNS over HTTPS (DoH) protocol for both inbound and outbound resolver endpoints.

## Route 53 Resolver DNS Firewall

**Q: What is Amazon Route 53 Resolver DNS Firewall?**

A: Amazon Route 53 Resolver DNS Firewall is a feature that allows you to quickly deploy DNS protections across all of your Amazon Virtual Private Clouds (VPCs). The Route 53 Resolver DNS Firewall allows you to block queries made for known malicious domains (i.e. create “denylists”) and to allow queries for trusted domains (create “allowlists”) when using the Route 53 Resolver for recursive DNS Resolution. You can also quickly get started with protections against common DNS threats by using AWS Managed Domain Lists. Amazon Route 53 Resolver DNS Firewall works together with AWS Firewall Manager so you can build policies based on DNS Firewall rules, and then centrally apply those policies across your VPCs and accounts.

**Q: When should I use Route 53 Resolver DNS Firewall?**

A: If you want to be able to filter the domain names that can be queried over DNS from within your VPCs, then DNS Firewall is for you. It gives you flexibility in choosing the configuration that works best for your organization’s security posture in two ways: (1) If you have strict DNS exfiltration requirements and want to deny all outbound DNS queries for domains that aren’t on your lists of approved domains, you can create such rules for a “walled-garden” approach to DNS security. (2) If your organization prefers to allow all outbound DNS lookups within your accounts by default and only requires the ability to block DNS requests for known malicious domains, you can use DNS Firewall to create denylists, which include all the malicious domain names your organization is aware of. DNS Firewall also comes with AWS Managed Domain Lists that help you protect against suspicious domains and Command-and-Control (C&C) bots.

**Q: How does Amazon Route 53 Resolver DNS Firewall differ from other firewall offerings on AWS and the AWS Marketplace?**

A: Route 53 Resolver DNS Firewall complements existing network and application security services on AWS by providing control and visibility to Route 53 Resolver DNS traffic (e.g. AmazonProvidedDNS) for your entire VPC. Depending on your use case, you may choose to implement DNS Firewall along your existing security controls, such as AWS Network Firewall, Amazon VPC Security Groups, AWS Web Application Firewall rules, or AWS Marketplace appliances.

**Q: Can Amazon Route 53 Resolver DNS Firewall manage security across multiple AWS accounts?**

A: Yes. Route 53 Resolver DNS Firewall is a regional feature and secures Route 53 Resolver DNS network traffic at an organization and account level. For maintaining policy and governance across multiple accounts, you should use [AWS Firewall Manager](https://aws.amazon.com/firewall-manager/).

**Q: How much does Amazon Route 53 Resolver DNS Firewall cost?**

Pricing is based on the number of domain names stored within your firewall and the number of DNS queries inspected. Please visit [Amazon Route 53 Pricing](https://aws.amazon.com/route53/pricing/) for more information.

**Q: Which AWS tools can I use to log and monitor my Amazon Route 53 Resolver DNS Firewall activity?**

A: You can log your DNS Firewall activity to an Amazon S3 bucket or Amazon CloudWatch log groups for further analysis and investigation. You can also use Amazon Kinesis Firehose to send your logs to a third-party provider.  

**Q: How do Amazon Route 53 Resolver 53 DNS Firewall and AWS Network Firewall differ in protection against malicious DNS query threats?**

A: Amazon Route 53 Resolver DNS Firewall and AWS Network Firewall both offer protection against outbound DNS query threats but for different deployment models. Amazon Route 53 Resolver DNS Firewall is designed to deliver granular control to block DNS requests to malicious or compromised domains if you are using Amazon Route 53 Resolver for DNS resolution. AWS Network Firewall offers similar capabilities to filter/block outbound DNS queries to known malicious domains if you are using an external DNS service to resolve DNS requests.


# AWS Route 53 Routing Policy
AWS [Route 53](https://jayendrapatil.com/aws-route-53/) routing policy determines how AWS would respond to the DNS queries and provides multiple routing policy options.

## Simple Routing Policy

- Simple routing policy is a simple round-robin policy and can be applied when there is a single resource doing the function for the domain _e.g. web server that serves content for the website._
- <mark style="background: #FFF3A3A6;">Simple routing helps configure standard DNS records, with no special Route 53 routing such as weighted or latency.</mark>
- <mark style="background: #ABF7F7A6;">Route 53 responds to the DNS queries based on the values in the resource record set</mark> _e.g. IP address in an A record._
- Simple routing <mark style="background: #ABF7F7A6;">does not allow the creation of multiple records with the same name and type</mark>, but multiple values can be specified in the same record, such as multiple IP addresses.
- Route 53 displays all the values to resolve it recursively in random order and the resolver displays the values for the client. The client then chooses a value and resends the query.
- <mark style="background: #CACFD9A6;">Simple routing policy does not support health checks, so the record would be returned to the client even if it is unhealthy.</mark>
- With Alias record enabled, only one AWS resource or one record can be specified in the current hosted zone.

![[Pasted image 20240210192503.png]]
## Weighted Routing Policy

- Weighted routing policy <mark style="background: #FFF3A3A6;">helps route traffic to different resources in specified proportions (weights)</mark> _e.g., 75% to one server and 25% to the_ _other during a pilot release_
- <mark style="background: #CACFD9A6;">Weights can be assigned between any number from 0 to 255 inclusive</mark>.
- <mark style="background: #ABF7F7A6;">Weighted routing policy can be applied when there are multiple resources that perform the same function</mark> _e.g., webservers serving the same site_
- <mark style="background: #FFF3A3A6;">Weighted resource record sets allow associating multiple resources with a single DNS name.</mark>
- Weighted routing policy use cases include
    - load balancing between regions
    - <mark style="background: #BBFABBA6;">A/B testing and piloting new versions of software</mark>
- <mark style="background: #CACFD9A6;">To create a group of weighted resource record sets, two or more resource record sets can be created that has the same combination of DNS name and type, and each resource record set is assigned a unique identifier and a relative weight.</mark>
- When processing a DNS query, Route 53 searches for a resource record set or a group of resource record sets that have the specified name and type.
- Route 53 selects one from the group. <mark style="background: #CACFD9A6;">The probability of any one resource record set being selected depends on its weight as a proportion of the total weight for all resource record sets in the group</mark> _for e.g., suppose www.example.com has three resource record sets with weights of 1 (20%), 1 (20%), and 3 (60%)(sum = 5).  
  On average, Route 53 selects each of the first two resource records sets one-fifth of the time and returns the third resource record set three-fifths of the time._
- <mark style="background: #CACFD9A6;">Weighted routing policy supports health checks.</mark>

![[Pasted image 20240210192400.png]]
## Latency-based Routing (LBR) Policy
- _Latency-based Routing Policy_ helps <mark style="background: #BBFABBA6;">respond to the DNS query based on which data center gives the user the lowest network latency.</mark>
- Latency-based routing policy can be used when there are multiple resources performing the same function and Route 53 needs to be configured to respond to the DNS queries with the resources that provide the fastest response with the lowest latency.
- A latency resource record set can be created for the EC2 resource in each region that hosts the application. When Route 53 receives a query for the corresponding domain, it selects the latency resource record set for the EC2 region that gives the user the lowest latency.  
  Route 53 then responds with the value associated with that resource record set _for e.g., you might have web servers for example.com in the EC2 data centers in Ireland and in Tokyo. When a user browses example.com from Singapore, Route 53 will pick up the data center (Tokyo) which has the lowest latency from the user’s location_
- **Latency between hosts on the Internet can change over time as a result of changes in network connectivity and routing.  
  Latency-based routing is based on latency measurements performed over a period of time, and the measurements reflect these changes** _for e.g. if the latency from the user in Singapore to Ireland improves, the user can be routed to Ireland_
- <mark style="background: #CACFD9A6;">Latency-based routing cannot guarantee users from the same geographic will be served from the same location for any compliance reason</mark>
- Latency resource record sets can be created using any record type that Route 53 supports except NS or SOA.
- <mark style="background: #CACFD9A6;">Latency-based routing policy supports health checks.</mark>

![[Pasted image 20240210192551.png]]
## Failover Routing Policy

- _Failover routing policy_ allows **active-passive** failover configuration, in which <mark style="background: #FFB86CA6;">one resource (primary) takes all traffic when it’s healthy and the other resource (secondary) takes all traffic when the first isn’t healthy.</mark>
- Route 53 health checking agents will monitor each location/endpoint of the application to determine its availability.
- Failover routing policy is applicable for Public hosted zones only.  
![](https://i.imgur.com/BBY93Yj.png)

## Geolocation Routing Policy

- _Geolocation routing policy_ <mark style="background: #FFF3A3A6;">helps respond to DNS queries based on the geographic location of the users i.e. location from which the DNS queries originate.</mark>
- Geolocation routing policy use cases include
    - <mark style="background: #BBFABBA6;">localization of content and presenting some or all of the website in the user’s language</mark>
    - <mark style="background: #FFB86CA6;">restrict distribution of content to only the locations in which you have distribution rights.</mark>
    - <mark style="background: #FF5582A6;">balancing load across endpoints in a predictable, easy-to-manage way, so that each user location is consistently routed to the same endpoint.</mark>
      
- Geolocation routing policy allows geographic locations to be specified by continent, country, or by state (only in the US)
- Geolocation record sets, if created, for overlapping geographic regions _for e.g. continent, and then for the country within the same continent_, <mark style="background: #FFF3A3A6;">priority goes to the smallest geographic region, which allows some queries for a continent to be routed to one resource and queries for selected countries on that continent to a different resource</mark>
- Geolocation works by mapping IP addresses to locations, which might not be mapped to an exact geographic location.
- <mark style="background: #CACFD9A6;">A default resource record set can be created to handle these queries and also the ones which do not have an explicit record set created.</mark>
- <mark style="background: #FFF3A3A6;">Route 53 returns a “no answer” response for queries from those locations if a default resource record set is not created.</mark>
- <mark style="background: #CACFD9A6;">Two geolocation resource record sets that specify the same geographic location</mark> **cannot** <mark style="background: #CACFD9A6;">be created.</mark>
- Route 53 supports the edns-client-subnet extension of EDNS0 (EDNS0 adds several optional extensions to the DNS protocol.) to improve the accuracy of geolocation routing.

## Geoproximity Routing Policy
- _Geo-proximity routing_ <mark style="background: #FFB86CA6;">helps route traffic to the resources based on the geographic location of the users and the resources.</mark>
- <mark style="background: #BBFABBA6;">Geoproximity routing can be configured with a bias to optionally choose to route more traffic or less to a given resource</mark>. <mark style="background: #FF5582A6;">A bias expands or shrinks the size of the geographic region from which traffic is routed to a resource.</mark>
- Route 53 Traffic flow can be used to create Geoproximity routing flows.
- Route 53 supports both the AWS region where the resource is created and the latitude and longitude of the resource.  
![](https://i.imgur.com/W0hKQSU.png)

## Multivalue Routing Policy

- <mark style="background: #FFF3A3A6;">Multivalue routing helps return multiple values</mark>, _e.g. IP addresses for the web servers_, in response to DNS queries.
- Multivalue routing also helps check the health of each resource, so only the values for healthy resources are returned.
- <mark style="background: #BBFABBA6;">Route 53 responds to DNS queries with up to eight healthy records and gives different answers to different DNS resolvers.</mark>
- <mark style="background: #FFB86CA6;">Multivalue answer routing is not a substitute for a load balancer, but the ability to return multiple health-checkable IP addresses is a way to use DNS to improve availability and load balancing.</mark>
- To route traffic approximately randomly to multiple resources, such as web servers, one multivalue answer record can be created for each resource and, optionally, associate a Route 53 health check with each record. If a web server becomes unavailable after the resolver caches a response, client software can try another IP address in the response.  
![](https://i.imgur.com/ACZl6o5.png)

## Route 53 Traffic Flow

- _Route 53 Traffic Flow_ helps easily manage traffic globally through a variety of routing types combined with DNS Failover in order to enable a variety of low-latency, fault-tolerant architectures.
- Traffic Flow provides a simple visual editor, to easily manage how the end-users are routed to the application’s endpoints – whether in a single AWS region or distributed around the globe.
- Traffic Flow routes traffic based on multiple criteria, such as endpoint health, geographic location, and latency.
- Traffic Flow’s versioning feature maintains a history of changes to the traffic policies to allow easy rollback to the previous version.

## Route 53 Complex Routing Policies

![Route 53 Complex Routing Policies](https://jayendrapatil.com/wp-content/uploads/2016/06/Route-53-Complex-Routing-Policies.png)

- Route 53 can be used to define more complex and nested routing policies
- A combination of alias records (such as weighted alias and failover alias) and non-alias records can be used to build a decision tree that gives you greater control over how Route 53 responds to requests.
- Resources would be created from the bottom of the tree

## AWS Certification Exam Practice Questions

> - Questions are collected from Internet and the answers are marked as per my knowledge and understanding (which might differ with yours).
> - AWS services are updated everyday and both the answers and questions might be outdated soon, so research accordingly.
> - AWS exam questions are not updated to keep up the pace with AWS updates, so even if the underlying feature has changed the question might not be updated
> - Open to further feedback, discussion and correction.

1. You have deployed a web application targeting a global audience across multiple AWS Regions under the domain name example.com. You decide to use Route 53 Latency-Based Routing to serve web requests to users from the region closest to the user. To provide business continuity in the event of server downtime you configure weighted record sets associated with two web servers in separate Availability Zones per region. During a DR test you notice that when you disable all web servers in one of the regions Route 53 does not automatically direct all users to the other region. What could be happening? (Choose 2 answers)
    1. Latency resource record sets cannot be used in combination with weighted resource record sets.
    2. **You did not setup an http health check for one or more of the weighted resource record sets associated with the disabled web servers**
    3. The value of the weight associated with the latency alias resource record set in the region with the disabled servers is higher than the weight for the other region.
    4. One of the two working web servers in the other region did not pass its HTTP health check
    5. **You did not set “Evaluate Target Health” to “Yes” on the latency alias resource record set associated with example.com in the region where you disabled the servers.**
2. The compliance department within your multi-national organization requires that all data for your customers that reside in the European Union (EU) must not leave the EU and also data for customers that reside in the US must not leave the US without explicit authorization. What must you do to comply with this requirement for a web based profile management application running on EC2?
    1. Run EC2 instances in multiple AWS Availability Zones in single Region and leverage an Elastic Load Balancer with session stickiness to route traffic to the appropriate zone to create their profile (should be in 2 different regions – US and Europe)
    2. Run EC2 instances in multiple Regions and leverage Route 53’s Latency Based Routing capabilities to route traffic to the appropriate region to create their profile (Latency based routing policy would not guarantee the compliance requirement)
    3. **Run EC2 instances in multiple Regions and leverage a third party data provider to determine if a user needs to be redirect to the appropriate region to create their profile**
    4. Run EC2 instances in multiple AWS Availability Zones in a single Region and leverage a third party data provider to determine if a user needs to be redirect to the appropriate zone to create their profile(should be in 2 different regions – US and Europe)
3. A US-based company is expanding their web presence into Europe. The company wants to extend their AWS infrastructure from Northern Virginia (us-east-1) into the Dublin (eu-west-1) region. Which of the following options would enable an equivalent experience for users on both continents?
    1. Use a public-facing load balancer per region to load-balance web traffic, and enable HTTP health checks.
    2. Use a public-facing load balancer per region to load-balance web traffic, and enable sticky sessions.
    3. **Use Amazon Route 53, and apply a geolocation routing policy to distribute traffic across both regions**
    4. Use Amazon Route 53, and apply a weighted routing policy to distribute traffic across both regions.
4. You have been asked to propose a multi-region deployment of a web-facing application where a controlled portion of your traffic is being processed by an alternate region. Which configuration would achieve that goal?
    1. **Route 53 record sets with weighted routing policy**
    2. Route 53 record sets with latency based routing policy
    3. Auto Scaling with scheduled scaling actions set
    4. Elastic Load Balancing with health checks enabled
5. Your company is moving towards tracking web page users with a small tracking image loaded on each page. Currently you are serving this image out of us-east, but are starting to get concerned about the time it takes to load the image for users on the west coast. What are the two best ways to speed up serving this image? Choose 2 answers
    1. **Use Route 53’s Latency Based Routing and serve the image out of us-west-2 as well as us-east-1**
    2. **Serve the image out through CloudFront**
    3. Serve the image out of S3 so that it isn’t being served of your web application tier
    4. Use EBS PIOPs to serve the image faster out of your EC2 instances
6. Your API requires the ability to stay online during AWS regional failures. Your API does not store any state, it only aggregates data from other sources – you do not have a database. What is a simple but effective way to achieve this uptime goal?
    1. Use a CloudFront distribution to serve up your API. Even if the region your API is in goes down, the edge locations CloudFront uses will be fine.
    2. Use an ELB and a cross-zone ELB deployment to create redundancy across datacenters. Even if a region fails, the other AZ will stay online.
    3. Create a Route53 _Weighted Round Robin record_, and if one region goes down, have that region redirect to the other region.  
       ![](https://i.imgur.com/5yrFdUL.png)

    4. **Create a Route53 Latency Based Routing Record with Failover and point it to two identical deployments of your stateless API in two different regions. Make sure both regions use Auto Scaling Groups behind ELBs.** (Refer [link](http://docs.aws.amazon.com/Route53/latest/DeveloperGuide/dns-failover.html))

## References

- [AWS User Guide – Route\_53\_Routing\_Policy](http://docs.aws.amazon.com/Route53/latest/DeveloperGuide/routing-policy.html)