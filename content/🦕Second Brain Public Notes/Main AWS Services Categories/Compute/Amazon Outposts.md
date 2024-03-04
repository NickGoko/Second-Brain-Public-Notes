---
tags:
  - cloud/aws
---


# FAQ
## General

### Why Would I Use AWS Outposts Rack instead of Operating in an AWS Region?
You can use Outposts rack to support your applications that have low latency or local data processing requirements.  
These applications may need to generate near real-time responses to end user applications or need to communicate with other on-premises systems or control on-site equipment. 

These can include workloads running on factory floors for automated operations in manufacturing, real-time patient diagnosis or medical imaging, and content and media streaming.  
You can use Outposts rack to securely store and process customer data that needs to remain on premises or in countries where there is no AWS Region.  
You can run data intensive workloads on Outposts rack and process data locally when transmitting data to AWS Regions is expensive and wasteful and for better control on data analysis, backup and restore.

### In Which AWS Regions is Outposts Rack Available?

Outposts rack is supported in the following AWS Regions and customers can connect their Outposts to the following AWS Regions:

<table><tbody><tr><td>US East (Ohio)</td><td>us-east-2</td></tr><tr><td>US East (N. Virginia)</td><td>us-east-1</td></tr><tr><td>US West (N. California)</td><td>us-west-1</td></tr><tr><td>US West (Oregon)</td><td>us-west-2</td></tr><tr><td>Canada (Central)</td><td>ca-central-1</td></tr><tr><td>South America (São Paulo)</td><td>sa-east-1</td></tr><tr><td>EU (Frankfurt)</td><td>eu-central-1</td></tr><tr><td>EU (Ireland)</td><td>eu-west-1</td></tr><tr><td>EU (Stockholm)</td><td>eu-north-1</td></tr><tr><td>EU (Paris)</td><td>eu-west-3</td></tr><tr><td>EU (London)</td><td>eu-west-2</td></tr><tr><td>EU (Milan)</td><td>eu-south-1</td></tr><tr><td>Middle East (Bahrain)</td><td>me-south-1</td></tr><tr><td>Middle East (UAE)</td><td>me-central-1</td></tr><tr><td>Israel (Tel Aviv)</td><td>il-central-1</td></tr><tr><td>Africa (Cape Town)</td><td>af-south-1</td></tr><tr><td>Asia Pacific (Sydney)</td><td>ap-southeast-2</td></tr><tr><td>Asia Pacific (Tokyo)</td><td>ap-northeast-1</td></tr><tr><td>Asia Pacific (Seoul)</td><td>ap-northeast-2</td></tr><tr><td>Asia Pacific (Singapore)</td><td>ap-southeast-1</td></tr><tr><td>Asia Pacific (Hong Kong)</td><td>ap-east-1</td></tr><tr><td>Asia Pacific (Mumbai)</td><td>ap-south-1</td></tr><tr><td>Asia Pacific (Osaka)</td><td>ap-northeast-3</td></tr><tr><td>Asia Pacific (Jakarta)</td><td>ap-southeast-3</td></tr><tr><td>AWS GovCloud (US-West)</td><td>us-gov-west-1</td></tr><tr><td>AWS GovCloud (US-East)</td><td>us-gov-east-1</td></tr></tbody></table>

### In Which Countries and Territories is Outposts Rack Available?

Outposts rack can be shipped to and installed in the following countries and territories.

- NA - US, Canada, Mexico
- EMEA - All EU countries, United Kingdom (UK), Switzerland, Norway, Bahrain, United Arab Emirates (UAE), Israel, South Africa, Gibraltar, Morocco, Nigeria, Kenya, Oman, Kazakhstan, Serbia, Qatar, Egypt, Iceland, Turkey
- APAC - Australia, New Zealand, Japan, South Korea, Hong Kong Special Administrative Region, Macau, Taiwan, Singapore, Indonesia, Malaysia, Thailand, the Philippines, Brunei, India, Vietnam, Bangladesh
- SA - Brazil, Colombia, Argentina, Chile, Peru, Ecuador, Trinidad and Tobago, Uruguay
- CA - Puerto Rico, Costa Rica, Panama, Guatemala

Support for more countries and territories is coming soon.

### Can I order an Outpost to a Country or Territory where Outposts Rack Has not Launched and Link it back to a Supported Region?

No, we can deliver and install Outposts rack only in countries and territories where Outposts rack can be delivered and supported.

### Can I Use Outposts Rack when it is not Connected to the AWS Region or in a Disconnected Environment?

<mark style="background: #CACFD9A6;">An Outpost relies on connectivity to the parent AWS Region. </mark>Outposts rack is not designed for disconnected operations or environments with limited to no connectivity. We recommend that customers have highly available networking connections back to their AWS Region. If interested in leveraging AWS services in disconnected environments such as cruise ships or remote mining locations, learn more about AWS services such as Snowball Edge, which is optimized to operate in environments with limited to no connectivity.

### Can I Reuse My Existing Servers in an Outpost?

No, AWS Outposts rack leverages AWS designed infrastructure, and is only supported on AWS-designed hardware that is optimized for secure, high-performance, and reliable operations.

### Is there a Software-only Version of AWS Outposts Rack?

No, AWS Outposts rack is a fully managed service that provides you with native access to AWS services.

### Can I order My Own Hardware that Can Be Installed as part of My Outposts Rack?

No, AWS Outposts rack provides fully integrated AWS designed configurations with built in top-of-rack switches and redundant power supply to ensure an ideal AWS experience. You can order as much compute and storage infrastructure as you need by selecting from the range of available Outposts rack options, or work with us to create a custom combination with your desired Amazon Elastic Compute Cloud (EC2), Amazon Elastic Block Store (EBS), and Amazon Simple Storage Service (S3) capacity. These are pre-validated and tested to ensure that you can get started quickly with no additional effort or configuration required on-site.

## AWS Services

Close all

### Can I Create EC2 Instances Using an EBS Backed AMI on My Outposts?

Yes, you can launch EC2 instances using the AMIs backed with EBS gp2 volume types.

### Where Are EBS Snapshots Stored?

EBS snapshots of EBS Volumes on Outposts rack are stored by default on Amazon S3 in the Region. If the Outpost is provisioned with Amazon S3 on Outposts you have the option to store your snapshots locally on your Outpost. EBS snapshots are incremental, which means that only the blocks on your Outpost that have changed after your most recent snapshot are saved. You can at any time restore (hydrate) EBS Volume on Outposts from the stored snapshots. To learn more, visit the EBS Snapshots [documentation](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/snapshots-outposts.html).

### How Do I Enforce Data Residency on Outposts Rack Using EBS Local Snapshots on Outposts?

You can set resource-level IAM policies and permissions on your Outpost for EBS Local Snapshots on Outposts and AMI images to enforce data residency. Each account (or IAM user or role) can set up a data residency enforcement policy for single or multiple Outposts. This will block the creation or copy of local snapshots and images as well as API/CLI calls outside the specified Outposts rack ARN. All of the create, update, and copy operations are logged in CloudTrail audit logs, so you can track that local snapshots reside in your location. To learn more, visit the EBS Snapshots [documentation](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/snapshots-outposts.html).

### What Use Cases Are Best Suited to Run on S3 on Outposts?

[S3 on Outposts](https://aws.amazon.com/s3/outposts/) is ideal for customers with data residency requirements or those in regulated industries that need to securely store and process customer data that needs to remain on premises or in locations where there is no AWS region. Additionally, customers can use S3 on Outposts to run data intensive workloads to process data locally and store on-premises. S3 on Outposts will also help if you have applications that need to communicate with other on-premises systems or control on-site equipment, such as within a factory, hospital, or research facility.

### How Can I Establish Network Connectivity between My Outpost and the AWS Region?

You can choose to establish Outposts rack service link VPN connection to the parent AWS Region via an AWS Direct Connect private connection, a public virtual interface, or the public Internet.

### Is Application Load Balancer Available on Outposts Rack?

Yes, Application Load Balancer is available on Outposts rack in all AWS Regions where Outposts rack is available, except the AWS GovCloud (US) Regions.

### Can Outposts Rack Support Real-time Applications with Low-latency Requirements?

Yes, with Amazon RDS on Outposts you can run managed Microsoft SQL Server, MySQL, and PostgreSQL databases on premises for low latency workloads that need to be run in close proximity to on premises data and applications. You can manage RDS databases both in the cloud and on premises using the same AWS Management Console, APIs, and CLI. For ultra low-latency applications, ElastiCache on Outposts enables sub-millisecond responses for real-time applications, including workloads running on factory floors for automated operations in manufacturing, real-time patient diagnosis, and media streaming.

### Can Outposts Rack Be Used to Meet Data Residency Requirements?

Yes. Customer data can be configured to remain on Outposts rack using Amazon Elastic Block Store (EBS) and Amazon Simple Storage Service (S3) on Outposts, in the customer’s on-premises location or specified co-location facility. Well-architected applications using Outposts rack and AWS services and tools address the data residency requirements we most commonly hear from our customers. AWS Identity and Access Management (IAM) lets you control access to AWS resources. You can use IAM and granular data control rules to specify which types of data must remain on Outposts rack and cannot be replicated to the AWS Region. S3 on Outposts stores data on your Outpost by default, and you may choose to replicate some or all of your data to AWS Regions based on your specific residency requirements. ElastiCache on Outposts allows you to securely process customer data locally on the Outposts rack. Some limited meta-data (e.g. instance IDs, monitoring metrics, metering records, tags, bucket names, etc.) will flow back to the AWS Region.  
  
To ensure your unique data residency requirements are met, we recommend you confirm and work closely with your compliance and security teams.

### Is Resource Sharing Available on AWS Outposts Rack?

Yes. AWS Resource Access Manager (RAM) is a service that enables you to share your AWS resources with any AWS account or within your AWS Organization. RAM support lets you, the Outpost owner, create and manage Outpost resources — EC2 instances, EBS volumes, subnets, and local gateways (LGWs) centrally — and share the resources across multiple AWS accounts within the same AWS organization. This allows others to configure VPCs, launch and run instances, and create EBS volumes on the shared Outpost.

### Which EC2 Instances Are Available on Outposts Rack?

EC2 instances built on the [AWS Nitro System](https://aws.amazon.com/ec2/nitro/), for general purpose, compute optimized, memory optimized, storage optimized, and GPU optimized with Intel Xeon Scalable processors are supported on AWS Outposts rack, and Graviton processors based EC2 instances are coming soon.

### How Can I Use Route 53 Resolver on Outposts?

You can use [Route 53 Resolver](https://aws.amazon.com/route53/resolver/) to resolve Domain Name Server (DNS) queries locally on Outposts racks, improving the availability and performance of your on-premises applications. When you enable Route 53 Resolver on Outposts, Route 53 automatically stores DNS responses on Outposts racks and provides continued DNS resolution for your applications even during unexpected network disconnects to the parent AWS Region. By serving DNS responses locally, Route 53 Resolver on Outposts also enables low-latency DNS resolution, improving the performance of your on-premises applications.

In addition, you can connect the Route 53 Resolvers on Outposts racks with DNS servers in your on-premises data centers through Route 53 Resolver endpoints. This enables resolution of DNS queries between the Outposts racks and your other on-premises resources.

## Getting Started with Ordering and Installation

Close all

### Are there Any Prerequisites for Deploying Outposts 42U Racks at My Location?

Your site must support the basic power, networking and space requirements to host an Outpost. An Outposts rack needs 5-15 kVA, can support 1/10/40/100 Gbps uplinks, and space for a 42U rack (80” X 24” X 48” dimensions). As Outposts rack requires reliable network connectivity to the AWS Region, you should plan for a public internet connection. Customers must have Enterprise Support or Enterprise On-Ramp Support, which provides 24x7 remote support within 15 minutes or within 30 minutes depending on the Support plan selected.

## Billing

Close all

### What Happens at Term End?

At the end of your Outposts rack term, you can either renew your subscription and keep your existing Outposts rack(s), or return your Outposts rack(s). If you do not notify AWS which option you intend to take, your Outposts rack(s) will be renewed on a monthly basis, at the rate of the No Upfront payment option corresponding to your AWS Outposts rack configuration. For more information, see term end documentation [here](https://docs.aws.amazon.com/outposts/latest/userguide/term-end-racks.html).

## Security and compliance

Close all

### Do the Same compliance Certifications for AWS Services Today Apply for Services on Outposts Rack?

AWS Outposts rack itself is HIPAA eligible, PCI, SOC, ISMAP, IRAP and FINMA compliant, ISO, CSA STAR, and HITRUST certified, and we expect to add more compliance certifications in coming months. You can see the latest certification status for [AWS Services on Outposts rack on our Services in Scope](https://aws.amazon.com/compliance/services-in-scope/) page. AWS Services on Outposts rack like RDS or Elasticache Redis that have achieved certifications like PCI are also considered certified on Outposts rack. As AWS Outposts rack runs at the customer’s data center, under the AWS Shared Responsibility model customers own the responsibility for physical security and access controls around the Outpost for compliance certification.

### Is AWS Outposts Rack GxP Compatible?

Yes, AWS Outposts rack is GxP compatible. AWS Outposts rack extends AWS services to AWS-managed infrastructure that is physically located at a customer site. Outposts rack capacity can be accessed locally over a local gateway that is mapped to the customer’s local network, in addition to having a connection path back to the AWS Region. You can learn more about using the AWS Cloud, including Outposts rack, for GxP systems [here](https://aws.amazon.com/compliance/gxp-part-11-annex-11/). GxP-regulated life sciences organizations using AWS services are responsible for designing and verifying their GxP compliance.

### Who is Responsible for the Physical Security of the Outposts Rack at My Datacenter?

AWS provides services that allow data to be encrypted at rest and in-transit and other granular security controls and auditing mechanisms. In addition, customer data is wrapped to a physical Nitro Security Key. Destroying the device is equivalent to destroying the data.  As part of the shared responsibility model, customers are responsible for attesting to physical security and access controls around the Outpost, as well as environmental requirements for facility, networking, and power as published [here](https://docs.aws.amazon.com/outposts/latest/userguide/outposts-requirements.html). Prior to returning the Outposts rack hardware, the Nitro Security Key will be removed to ensure customer content is crypto shredded.

### What is AWS Outposts FedRAMP Authorization Status?

FedRAMP has granted authorization to AWS Outposts, excluding the hardware components of the service. The physical and environmental controls for the AWS Outposts protection while at the customers’ sites are the customers’ responsibilities. Customers and agencies can make a risk-based decision to use AWS Outposts or conduct a Type Accreditation to review the hardware components of AWS Outposts to process FedRAMP workloads. Assessment results previously conducted by the AWS Third Party Assessment Organization can be accessed via [CapLinked](https://secure.caplinked.com/workspaces/aws-workspace).

## Support and Maintenance

Close all

### How Does AWS Maintain AWS Outposts Rack Infrastructure?

When your Outpost is installed and is visible in the AWS Management Console, AWS will monitor it as part of the public Region and will automatically execute software upgrades and patches.

If there is a need to perform physical maintenance, AWS will reach out to schedule a time to visit your site. AWS may replace a given module as appropriate but will not perform any host or network switch servicing on customer premises.

### What Happens when My Facility's Network Connection Goes Down?

EC2 instances and EBS volumes on the Outpost will continue to operate normally and can be accessed locally via the local gateway. Similarly, AWS service resources such as ECS worker nodes continue to run locally. However, API availability will be degraded, for instance run/start/stop/terminate APIs may not work. Instance metrics and logs will continue to be cached locally for a few hours, and will be pushed to the AWS Region when connectivity returns. Disconnection beyond a few hours however may result in loss of metrics and logs. If you expect to lose network connectivity, we strongly recommend regularly testing your workload to ensure it behaves properly in this state when an Outpost is disconnected. For S3 on Outposts, if the network connection to your Outpost is lost, you will not be able to access your objects. Requests to store and retrieve objects are authenticated using the regional AWS Identity and Access Management (IAM) service, and if the Outpost has no connectivity to the home AWS Region, you are not able to access your data. Your data remains safely stored on your Outpost during periods of disconnect, and once connectivity is restored authentication and requests can resume.

### What Type of Control Plane Information Flows back to the Parent AWS Region?

As an example, information about instance health, instance activity (launched, stopped), and the underlying hypervisor system may be sent back to the parent AWS Region. This information enables AWS to provide alerting on instance health and capacity, and apply patches and updates to the Outpost. Your team does not need to implement your own tooling to manage these elements, or to actively push security updates and patches for your Outpost. For S3 on Outposts, certain data management and telemetry data, such as bucket names and metrics, may be stored in the AWS Region for reporting and management. When disconnected, this information cannot be sent back to the parent Region.

### How Does AWS Support Adding Capacity to Existing Outposts?

There are two mechanisms to increase your compute and storage capacity of your AWS Outposts rack. First, you can increase capacity by adding additional Outposts racks from the Outposts rack catalog. Second, if your existing Outposts racks have available power and positions within the rack, you can increase from a “small” to a “medium” or “large” configuration, or from a” medium” to a “large” configuration. You will be able to add compute and storage capacity a maximum of twice within a rack that supports 10KVA – 15KVA power consumption. Note: The 1U and 2U Outposts servers cannot be installed in the 42U Outposts form factor.