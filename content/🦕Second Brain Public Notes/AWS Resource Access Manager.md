---
tags:
  - cloud/aws
---

![Amazon AWS Resource Access Manager Services](https://digitalcloud.training/wp-content/uploads/2022/01/AWS-Cheat-Sheets-Images.jpg)  
**AWS Resource Access Manager (RAM)** is <mark style="background: #FFF3A3A6;">a service that enables you to share AWS resources easily and securely with any AWS account or within your AWS Organization.</mark>

<mark style="background: #ABF7F7A6;">You can share AWS Transit Gateways, Subnets, AWS License Manager configurations, and Amazon Route 53 Resolver rules resources with RAM.</mark>

**RAM** <mark style="background: #FFB86CA6;">eliminates the need to create duplicate resources in multiple accounts, reducing the operational overhead of managing those resources in every single account you own.</mark>

<mark style="background: #FFF3A3A6;">You can create resources centrally in a multi-account environment, and use RAM to share those resources across accounts</mark> in three simple steps:
1. Create a Resource Share.
2. Specify resources.
3. Specify accounts.

<mark style="background: #FFB8EBA6;">RAM is available at no additional charge.</mark>

## **Key benefits:**
- **Reduce Operational Overhead –** <mark style="background: #BBFABBA6;">Procure AWS resources centrally and use RAM to share resources such as subnets or License Manager configurations with other accounts</mark>. This eliminates the need to provision duplicate resources in every account in a multi-account environment.
- **Improve Security and Visibility –** <mark style="background: #BBFABBA6;">RAM leverages existing policies and permissions set in AWS Identity and Access Management (IAM) to govern the consumption of shared resources.</mark>  
	  RAM also provides comprehensive visibility into shared resources to set alarms and visualize logs through integration with Amazon CloudWatch and AWS CloudTrail.
- **Optimize Costs –** Sharing resources such as AWS License Manager configurations across accounts allows you to leverage licenses in multiple parts of your company to increase utilization and optimize costs.