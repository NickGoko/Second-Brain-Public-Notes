---
tags:
  - cloud/aws
---

![[AWS Solutions Architect Skillbuilder#AWS Snowmobile]]

![[AWS Solutions Architect Skillbuilder#AWS Snowmobile Features]]
# FAQ
## General

**Q: What is AWS Snowmobile?**

AWS Snowmobile is the first exabyte-scale data migration service that allows you to move very large datasets from on-premises to AWS. Each Snowmobile is a secured data truck with up to 100PB storage capacity that can be dispatched to your site and connected directly to your network backbone to perform high-speed data migration. You can quickly migrate an exabyte of data with ten Snowmobiles in parallel from a single location or multiple data centers. Snowmobile is offered by AWS as a managed service.  

**Q: How does Snowmobile work?**

After you have placed your inquiry for a Snowmobile, AWS personnel will contact you to determine requirements for deploying a Snowmobile and schedule the job, and will drive the required Snowmobile equipment to your site. Once on site, they will connect it to your local network so that you can use your high-speed local connection to quickly transfer data from your local storage appliances or servers to the Snowmobile. After the data transfer is complete, the Snowmobile will be returned to your designated AWS region where your data will be uploaded into the AWS storage services you have selected, such as S3 or Glacier. Finally, AWS will work with you to validate that your data has been successfully uploaded.  

**Q: Who should use a Snowmobile?**

Snowmobile enables customers to quickly migrate exabyte-scale datasets from on-premises to AWS in a more secure, fast, and low-cost manner. Use cases include migrating 100’s of petabytes of data (such as video libraries, genomic sequences, seismic data, satellite images), and financial records to run big data analytics on AWS, or shutting down legacy data centers and moving all local data in exabytes to AWS. Before Snowmobile, migrating data at such scale would typically take years which was too slow for many customers. With Snowmobile, you can now request multiple data trucks each with up to 100PB capacity to be dispatched on-site, connected to your local high speed network backbone, and transfer your exabyte-scale datasets to AWS in as quickly as a few weeks, plus transport time.  

**Q: What are the specifications of a Snowmobile?**

Each Snowmobile comes with up to 100PB of storage capacity housed in a 45-foot long High Cube shipping container that measures 8 foot wide, 9.6 foot tall and has a curb weight of approximately 68,000 pounds. The ruggedized shipping container is tamper-resistant, water-resistant, temperature controlled, and GPS-tracked.  

**Q: How should I choose between Snowmobile and Snowball?**

To migrate large datasets of 10PB or more in a single location, you should use Snowmobile. For datasets less than 10PB or distributed in multiple locations, you should use Snowball. In addition, you should evaluate the amount of available bandwidth in your network backbone. If you have a high speed backbone with hundreds of Gb/s of spare throughput, then you can use Snowmobile to migrate the large datasets all at once. If you have limited bandwidth on your backbone, you should consider using multiple Snowballs to migrate the data incrementally.  

**Q: How much data can I transfer to Snowmobile?**

Each Snowmobile has a total capacity of up to 100 petabytes and multiple Snowmobiles can be used in parallel to transfer exabytes of data. 

**Q: Are there site requirements to use a Snowmobile?**

The Snowmobile needs physical access to your data center to allow for network connectivity. It comes with a removable connector rack with up to two kilometers of networking cable that can directly connect to the network backbone in your data center. The Snowmobile can be parked in a covered area at your data center, or in an uncovered area that is adjacent to your data center, and close enough to run the networking cable. The parking area needs to hold a standard 45-foot High Cube trailer with a minimum of 6’-0” (1.83m) of peripheral clearance. Snowmobile can operate at ambient temperatures up to 85F (29.4C) before an auxiliary chiller unit is required. AWS can provide the auxiliary chiller if needed based on the site survey findings.  

**Q: How is a Snowmobile powered?**

A fully powered Snowmobile requires ~350KW. Snowmobile can be connected to available utility power sources at your location if sufficient capacity is available. Otherwise, AWS can dispatch a separate generator set along with the Snowmobile if your site permits such generator use. This generator set takes a similar amount of space as the Snowmobile which is parking for a vehicle approximately the same size as a 45-foot container trailer.  

## Getting Started

**Q: What is a Snowmobile job?**

A Snowmobile job encapsulates the end-to-end data migration process using a Snowmobile. There are five main steps:

1. Site Survey, where AWS personnel will work with you to understand your migration objectives, data center environment, and network configurations in order to help you determine a migration plan;
2. Site Preparation, where you (the customer) will identify and make available local resources such as parking space and power source for the Snowmobile, local security, network address, ports, and available rack positions to connect the Snowmobile with the local network backbone;
3. Dispatch and Setup, where AWS personnel will dispatch a Snowmobile to your site and configure it for you so it can be accessed securely as a network storage target;
4. Data Migration, where you will copy data from any number of sources within your data center to the Snowmobile, and
5. Return and Upload, where the Snowmobile is returned to an AWS region that you have designated where your data will be uploaded into the AWS storage services you have selected.

Learn more about our [Migration Services](https://docs.aws.amazon.com/aws-technical-content/latest/aws-overview/migration-services.html) here.  

**Q: How do I connect my data center to Snowmobile?**

Each Snowmobile comes with a removable high-speed connector rack on wheels with two kilometers of ruggedized networking cable. The connector rack can be rolled to a location inside your data center and connected directly to your network backbone. This way, the Snowmobile will operate as a network storage target inside your network for you to perform high-speed data transfer.  

**Q: How do I copy my data to a Snowmobile?**

Once the Snowmobile is connected to your data center, it will appear as a network storage target. You can copy data from local storage devices to the Snowmobile using the same tools and in the same manner as data copied to any network attached storage device with an NFS interface.  

**Q: Can I connect to Snowmobile via a NFS endpoint?**

Yes. The Snowmobile will appear as a standard NFS mount on your network that you can connect to via your existing tools and applications.  

**Q: How do I get started with Snowmobile?**

Please [contact your sales team](https://aws.amazon.com/contact-us/) to request a Snowmobile.  

## Using Snowmobile

**Q: How long does it take to transfer my data to a Snowmobile?**

The Snowmobile is designed to transfer data at a rate up to 1 Tb/s, which means you could fill a 100PB Snowmobile in less than 10 days. The actual transfer speed may vary depending on the available local network capacity at your site and the speed of your on-premises storage devices. AWS will provide a way for you to test your local network throughput and the copy speed from your data sources to properly size the Snowmobile job, before dispatching the Snowmobile.  

**Q: What type of connections does Snowmobile provide?**

The Snowmobile comes with a removable connector cabinet that needs to be mounted on one of your data center racks where it can be connected directly to your high-speed network backbone. The connector rack provides multiple 40Gb/s interfaces that can transfer up to 1 Tb/s in aggregate.  

**Q: After my data has been imported to AWS, what happens to the copy on Snowmobile?**

When the data import has been processed and verified, AWS performs a software erasure of the Snowmobile that follows the National Institute of Standards and Technology (NIST) guidelines for media sanitization (NIST 800-88).  

**Q: How do I verify that my data has been successfully copied to Snowmobile?**

At the time your data is copied into the Snowmobile, a set of logs will be generated with checksums for each file transferred. These logs are available to you for verification. The logs are also used when data is imported from the Snowmobile to AWS to verify that all data has been transferred successfully.  

**Q: Do I need to keep a local copy of my data while a copy is shipped back to AWS on a Snowmobile?**

Yes. You should always keep your source copy until AWS has worked with you to verify that the Snowmobile copy has been successfully uploaded to AWS.  

**Q: Can I export data from AWS with Snowmobile?**

Snowmobile does not support data export. It is designed to let you quickly, easily, and more securely migrate exabytes of data to AWS. When you need to export data from AWS, you can use AWS Snowball Edge to quickly export up to 100TB per appliance and run multiple export jobs in parallel as necessary. Visit the [Snowball Edge FAQs](https://aws.amazon.com/snowball-edge/faqs/) to learn more.  

## Security

**Q: How is Snowmobile designed to keep data secure digitally?**

Your data is encrypted with keys you provided before it is written to the Snowmobile. All data is encrypted with 256-bit encryption. You can manage your encryption keys with the [AWS Key Management Service (KMS)](https://aws.amazon.com/kms/). Your keys are never permanently stored on the Snowmobile, and are erased as soon as power is removed from the Snowmobile.  

**Q: How is Snowmobile designed to keep data secure physically?**

In addition to digital encryption, the Snowmobile is only operated by AWS personnel and physical access to the data container is controlled via secure access hardware controls. All data storage equipment is separated from the network access ports used to load or remove data. This way, physical access to the data container is not needed to operate the container after it has been set up. In addition, Snowmobile is protected by 24/7 video surveillance and alarm monitoring, GPS tracking, and may be escorted by a security vehicle during transit.  

**Q: Can I still choose to encrypt my data before transferring to Snowmobile?**

Yes. You can always encrypt your data before transferring it to the Snowmobile.

## Region Availability

**Q: What AWS Regions are supported?**

Snowmobile can be made available for use with AWS services in specific AWS regions. To discuss data transport needs specific for your region please follow up with [AWS Sales](https://aws.amazon.com/contact-us/aws-sales/), or see the [Regional Service Availability](https://aws.amazon.com/about-aws/global-infrastructure/regional-product-services/) pages for more information.  

## Pricing

**Q: How much does a Snowmobile job cost?**

Snowmobile provides a practical solution to exabyte-scale data migration and is significantly faster and cheaper than any network-based solutions, which can take decades and millions of dollars of investment in networking and logistics. Snowmobile jobs cost $0.005/GB/month based on the amount of provisioned Snowmobile storage capacity and the end to end duration of the job, which starts when a Snowmobile departs an AWS data center for delivery to the time when data ingestion into AWS is complete. Please see [AWS Snowmobile pricing](https://aws.amazon.com/snowmobile/pricing/) or contact [AWS Sales](https://aws.amazon.com/contact-us/aws-sales/) for an evaluation.