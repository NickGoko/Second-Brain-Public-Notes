---
tags:
  - cloud/aws
---

![](https://i.imgur.com/uWIhbXj.png)

# FAQ
## General

**Q: What is Amazon Macie?**  
  
A: Amazon Macie is <mark style="background: #ADCCFFA6;">a data security service that discovers sensitive data using machine learning and pattern matching, provides visibility into data security risks, and enables automated protection against those risks.</mark>

**Q: What are the key benefits of Macie?**  
A: Macie uses machine learning and pattern matching to discover sensitive data at scale in a cost-efficient way. Macie automatically detects a large and growing list of sensitive data types, including personally identifiable information (PII) such as names, addresses, and credit card numbers. It also gives you constant visibility of your data stored in Amazon Simple Storage Service (Amazon S3). Macie’s setup is simplified with one selection in the AWS Management Console or a single API call. Macie provides multi-account support using AWS Organizations, so you can enable Macie across all of your accounts with a few selections.

**Q: How much does Macie cost?**  
A: With Macie, you are charged based on three dimensions: the number of S3 buckets evaluated for bucket inventory and monitoring, the number of S3 objects monitored for automated data discovery, and the quantity of data inspected for automated and targeted sensitive data discovery. See the [Macie pricing page](https://aws.amazon.com/macie/pricing/) for the latest pricing information.

**Q: Is there a free trial?**  
A: Yes, there is a 30-day free trial for each new account to Macie. The free trial includes 30 days of automated sensitive data discovery in S3 and bucket-level security and access controls. The AWS Management Console provides a cost estimate of the service based on your total number of buckets in the account. If you are in a multi-account configuration, the cost estimate is rolled up across all accounts to show you what your estimated total would be after each account’s free trial ends. Macie also includes 1 GB of data processed for sensitive data discovery per month at no cost. This free tier offer does not expire and is not bound by the 30-day free trial period.

**Q: Is Macie a regional or global service?**  
A: Macie is a regional service. Macie must be enabled on a region-by-region basis and helps you view findings across all your accounts within each Region. This verifies that all data analyzed is regionally based and doesn’t cross AWS regional boundaries.

**Q: What Regions does Macie support?**  
A: The latest on regional availability can be found at the AWS Region Table.

**Q: How can I get started with Macie?**  
A: Macie can be enabled with one selection in the AWS Management Console or a single API call. Macie provides multi-account support using AWS Organizations, so you can enable Macie across all of your accounts with a few selections.

**Q: How does Macie support custom data types?**  
A: With Macie, you can add custom-defined data types using regular expressions to help Macie discover proprietary or unique sensitive data for your business. For example, you might have a specific format for your employee IDs; a possible format is to have a capital letter, which defines if someone is a full-time or part-time employee, followed by a dash, and then eight numbers (such as F-12345678 for a full-time employee). These custom sensitive data types defined are unique to each customer and are not shared with other customers.

**Q: Can I exclude buckets sampled by automated data discovery?**  
A: Yes. You can navigate to buckets of interest using the Macie S3 bucket inventory and mark them to be excluded from automated sensitive data discovery. If you would like to exclude large numbers of buckets, you can use the Macie API operations to mark buckets as excluded. You can also apply this configuration on the Settings page in the Macie console.

**Q: Is there a free trial for automated sensitive data discovery?**  
A: Yes. There is a 30-day free trial for all new and existing accounts to try automated sensitive data discovery. During the first 30 days, there is no charge for automated sensitive data discovery. See the Macie pricing page for cost estimates after the 30-day free trial.

**Q: What bucket-level metadata is used to enrich the Macie data map for S3?**  
A: Metadata that Macie uses for data map enrichment includes public accessibility, encryption type, shared or replicated status with accounts outside of your AWS organization, total storage volume, classifiable storage volume, and estimated total data scanned. It also includes an indication of the presence of sensitive data and a sensitivity score for each bucket. This score is calculated based on the results of automated sensitive data discovery and any targeted sensitive data discovery jobs that you have run. You can review a distribution of the types of sensitive data found in the S3 bucket table within the Macie console or through the Macie API operations.