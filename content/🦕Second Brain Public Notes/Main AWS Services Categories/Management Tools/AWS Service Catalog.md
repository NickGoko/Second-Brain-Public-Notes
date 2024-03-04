---
tags:
  - cloud/aws
---
AWS Service Catalog enables organizations to create and manage catalogs of IT services that are approved for AWS.

These IT services can include everything from virtual machine images, servers, software, and databases to complete multi-tier application architectures.

AWS Service Catalog allows organizations to centrally manage commonly deployed IT services, and helps organizations achieve consistent governance and meet compliance requirements.

End users can quickly deploy only the approved IT services they need, following the constraints set by your organization.

AWS Service Catalog supports the following types of users:

- **Catalog administrators (administrators)** – Manage a catalog of products (applications and services), organizing them into portfolios and granting access to end users. Catalog administrators prepare AWS CloudFormation templates, configure constraints, and manage IAM roles that are assigned to products to provide for advanced resource management.
- **End users** – Receive AWS credentials from their IT department or manager and use the AWS Management Console to launch products to which they have been granted access.

Products:

- A _product_ is an IT service that you want to make available for deployment on AWS.
- A product consists of one or more AWS resources, such as EC2 instances, storage volumes, databases, monitoring configurations, and networking components, or packaged AWS Marketplace products.
- AWS CloudFormation templates define the AWS resources required for the product, the relationships between resources, and the parameters that end users can plug in when they launch the product to configure security groups, create key pairs, and perform other customizations.

Portfolios:

- A _portfolio_ is a collection of _products_, together with configuration information.
- Portfolios help manage who can use specific products and how they can use them.
- With AWS Service Catalog, you can create a customized portfolio for each type of user in your organization and selectively grant access to the appropriate portfolio.
- When you add a new _version_ of a product to a portfolio, that version is automatically available to all current users.
- You also can share your portfolios with other AWS accounts and allow the administrator of those accounts to distribute your portfolios with additional _constraints_, such as limiting which EC2 instances a user can create.
- Through the use of portfolios, permissions, sharing, and constraints, you can ensure that users are launching products that are configured properly for the organization’s needs and standards.

Versioning:

- AWS Service Catalog allows you to manage multiple versions of the products in your catalog.
- This allows you to add new versions of templates and associated resources based on software updates or configuration changes.
- When you create a new version of a product, the update is automatically distributed to all users who have access to the product, allowing the user to select which version of the product to use.

Permissions:

- Granting a user access to a portfolio enables that user to browse the portfolio and launch the products in it.
- You apply AWS Identity and Access Management (IAM) permissions to control who can view and modify your catalog. IAM permissions can be assigned to IAM users, groups, and roles.
- When a user launches a product that has an IAM role assigned to it, AWS Service Catalog uses the role to launch the product’s cloud resources using AWS CloudFormation.
- By assigning an IAM role to each product, you can avoid giving users permissions to perform unapproved operations and enable them to provision resources using the catalog.

Constraints:

- _Constraints_ control the ways that specific AWS resources can be deployed for a product.
- You can use them to apply limits to products for governance or cost control.
- There are different types of AWS Service Catalog constraints: _launch constraints_, _notification constraints_, and _template constraints_.
- With **launch constraints**, you specify a role for a product in a portfolio. This role is used to provision the resources at launch, so you can restrict user permissions without impacting users’ ability to provision products from the catalog.
- **Notification constraints** enable you to get notifications about stack events using an Amazon SNS topic.
- **Template constraints** restrict the configuration parameters that are available for the user when launching the product (for example, EC2 instance types or IP address ranges). With template constraints, you reuse generic AWS CloudFormation templates for products and apply restrictions to the templates on a per-product or per-portfolio basis.

## Sharing and Importing Portfolios

To make your AWS Service Catalog products available to users who are not in your AWS account, such as users who belong to other organizations or to other AWS accounts in your organization, you share your portfolios with them.

You can share in several ways, including account-to-account sharing, organizational sharing, and deploying catalogs using stack sets.

Before you share your products and portfolios to other accounts, you must decide whether you want to share a reference of the catalog or to deploy a copy of the catalog into each recipient account.

Note that if you deploy a copy, you must redeploy if there are updates you want to propagate to the recipient accounts.

You can use stack sets to deploy your catalog to many accounts at the same time. If you want to share a reference (an imported version of your portfolio that stays in sync with the original), you can use account-to-account sharing or you can share using AWS Organizations.

When you share a portfolio using account-to-account sharing or AWS Organizations, you allow an AWS Service Catalog administrator of another AWS account to import your portfolio into his or her account and distribute the products to end users in that account.

This _imported portfolio_ isn’t an independent copy. The products and constraints in the imported portfolio stay in sync with changes that you make to the _shared portfolio_, the original portfolio that you shared.

The _recipient administrator_, the administrator with whom you share a portfolio, cannot change the products or constraints, but can add AWS Identity and Access Management (IAM) access for end users.

The recipient administrator can distribute the products to end users who belong to his or her AWS account in the following ways:

- By adding IAM users, groups, and roles to the imported portfolio.
- By adding products from the imported portfolio to a _local portfolio_, a separate portfolio that the recipient administrator creates and that belongs to his or her AWS account. The recipient administrator then adds IAM users, groups, and roles to the local portfolio. The constraints that you applied to the products in the shared portfolio are also present in the local portfolio. The recipient administrator can add additional constraints to the local portfolio but cannot remove the imported constraints.