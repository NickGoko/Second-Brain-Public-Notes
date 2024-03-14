---
tags:
  - cloud/aws
---

![](https://i.imgur.com/HiZXZo9.png)  
![](https://i.imgur.com/QfEVW4X.png)  
![](https://i.imgur.com/OQIDwP7.png)

# FAQ
### What is AWS Lake Formation?

**AWS Lake Formation** <mark style="background: #D2B3FFA6;">makes it easier to centrally govern, secure, and globally share data for analytics and machine learning (ML).</mark>  
With _Lake Formation_, <mark style="background: #ABF7F7A6;">you can centralize data security and governance using the AWS Glue Data Catalog, letting you manage metadata and data permissions in one place with familiar database-style features. </mark>

<mark style="background: #FFF3A3A6;">It also delivers fine-grained data access control, so you can help ensure users have access to the right data, down to the row and column level. </mark>  
You can then scale permissions across your users.  
Lake Formation also makes it easier to share data internally across your organization, across Regions, and externally using AWS Data Exchange, letting you create a data mesh or meet other data sharing needs with no data movement.  
And, because Lake Formation tracks data interactions by role and user, it provides comprehensive data access auditing to help ensure the right data was accessed by the right users at the right time.

### How Does Lake Formation Relate to AWS Glue and the AWS Glue Data Catalog?

Lake Formation shares console controls and the AWS Glue Data Catalog with AWS Glue.  
 AWS Glue focuses on data integration and ETL.  
  
See [AWS Lake Formation features](https://aws.amazon.com/lake-formation/features/) for more details.

### How Does Lake Formation Integrate with Amazon DataZone?

Lake Formation and the AWS Glue Data Catalog are integral parts of Amazon Data Zone. Amazon DataZone supports granting access to Data Catalog tables that are managed in AWS Lake Formation. Amazon DataZone uses Lake Formation to manage permissions and facilitate sharing of data products. For example, in Amazon DataZone when a producer makes data available for a subscription, it has to be in the Data Catalog. When a subscription is granted, Amazon DataZone orchestrates the creation of Lake Formation grants.

### Can I Use Third-party Business Intelligence Tools with Lake Formation?

Yes. You can use third-party business applications, such as Tableau and Looker, to connect to your AWS data sources through services such as Amazon Athena or Amazon Redshift. Access to data is managed by Lake Formation and the underlying AWS Glue Data Catalog, so regardless of which application you use, you’re assured that access to your data is governed and controlled.

### Do Third-party Tools Integrate with Lake Formation?

There are several third-party tools that integrate with Lake Formation, including Ahana, Dremio, Privacera, Collibra, and Starburst.

## Centralized Permissions Management

### How Does Lake Formation Simplify and Centralize Permissions Management?

Lake Formation centralizes permission management on your resources in the AWS Glue Data Catalog, including databases and tables, letting you manage permissions for your data and metadata in one place. You can define and manage access for your users and applications by role with Lake Formation in the Data Catalog using familiar database-like grants, bringing the simplicity of data warehouses and databases to your data lake.

### How Does Lake Formation Work with AWS Identity and Access Management (IAM)?

Integration with AWS Identity and Access Management (IAM) authenticates users and roles, enforcing permissions across AWS analytics and ML services, including Amazon Athena, Amazon QuickSight, Amazon Redshift, and Amazon SageMaker. Lake Formation provides a permissions model that is based on a straightforward grant and revoke mechanism. Lake Formation permissions combine with IAM permissions to control access to data stored in data lakes and to the metadata that describes that data. When a principal makes a request to access AWS Glue Data Catalog resources or underlying data, for the request to succeed it must pass permission checks by both IAM and Lake Formation. IAM and Lake Formation are complementary to each other, and Lake Formation does not impact existing IAM permissions.

### What Data Granularity Does Lake Formation Permissions Support?

Different users across your organization require different levels of access to your data. It’s important that users have access to the right data—and no more—to do their jobs. Lake Formation fine-grained access control (FGAC) lets you manage permissions to the column, row, and cell level. FGAC makes it easier to comply with increased business regulations, apply better data governance, and deftly protect and manage consumers’ sensitive data.

## Security Management and Governance

Close all

### How Does Lake Formation Help Scale Permissions across Users?

Lake Formation makes it easier to scale permissions across your users. You can set attributes on data and apply permissions on those attributes to scale. Lake Formation tag-based access control (LF-TBAC) uses attributes of the data to help keep permissions up to date as data changes. With LF-TBAC, administrators set the appropriate tags on their data, and then the existing policies will enforce the desired access to new data resources. This helps scale permissions management across a large number of AWS Glue Data Catalog resources, reducing management time and effort.

## Secure Data Sharing

### How Does Lake Formation Streamline Data Sharing?

AWS Lake Formation simplifies cross-account data sharing, letting you create a data mesh or meet other data-sharing needs with minimal data movement. Lake Formation cross-account capabilities allow users to share distributed data with confidence across multiple AWS accounts, AWS Organizations, AWS Regions, or directly with IAM principals in another account, while ensuring proper data governance so that data owners control who has data access.

### What is the Role of the AWS Glue Data Catalog in Data Sharing?

The AWS Glue Data Catalog acts as a hub for managing and sharing your data, whether natively in the Glue Data Catalog or as a connector to other catalogs, such as Hive Metastore. You can set up and enforce permissions on datasets presented through the Data Catalog, making it easier to control access to your data no matter where it lives.

### How Does Lake Formation Simplify External or Business-to-business Data Sharing?

Lake Formation integrates with AWS Data Exchange so you can share data with external businesses without moving or copying the data.

### How Does Lake Formation Integrate with other AWS Services?

AWS services such as Amazon Athena, AWS Glue, Amazon Redshift Spectrum, and Amazon EMR can use Lake Formation to securely access data in Amazon Simple Storage Service (Amazon S3) locations registered with Lake Formation. With Lake Formation, you can define and manage FGAC permissions for your data in the AWS Glue Data Catalog. Each of these AWS services is a trusted caller to Lake Formation, and Lake Formation provides access to data stored in Amazon S3 through temporary credentials. Amazon QuickSight and [Amazon SageMaker Studio](https://aws.amazon.com/sagemaker/studio/) integrations are also supported if using one of the supported engines.

For more information, see [Lake Formation Permissions Management Workflow](https://docs.aws.amazon.com/lake-formation/latest/dg/how-it-works.html#lf-workflow).

## Data Access Monitoring and Auditing

### How Can Lake Formation Help Monitor and Audit Data Access?

Lake Formation provides comprehensive audit logs with AWS CloudTrail to monitor access and demonstrate compliance with centrally defined policies. You can audit data access history across analytics and ML services that read the data in your data lake with Lake Formation. This lets you see which users or roles have attempted to access what data, with which services, and when. You can access audit logs in the same way you access other CloudTrail logs using the CloudTrail APIs and console. For more information about CloudTrail logs, see [Logging AWS Lake Formation API Calls Using AWS CloudTrail](https://docs.aws.amazon.com/lake-formation/latest/dg/logging-using-cloudtrail.html).

