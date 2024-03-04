---
tags:
  - cloud/aws
---
**AWS Organizations** <mark style="background: #BBFABBA6;">helps you centrally manage and govern your environment as you grow and scale your AWS resources</mark>.

AWS accounts are natural boundaries for permissions, security, costs, and workloads.

Using a multi-account environment is a recommended best-practice when scaling your cloud environment.  
![](https://i.imgur.com/dXx2igD.png)  
![](https://i.imgur.com/85fu8Eb.png)

AWS Organizations provides many features for managing multi-account environments, including:
- <mark style="background: #FFF3A3A6;">Simplify account creation by programmatically creating new accounts using the AWS Command Line Interface (CLI), SDKs, or APIs</mark>.
- <mark style="background: #ADCCFFA6;">Group accounts into organizational units (OUs)</mark>, or groups of accounts that serve a single application or service.
- Apply tag polices to classify or track resources in your organization and provide attribute-based access control for users or applications.
- Delegate responsibility for supported AWS services to accounts so users can manage them on behalf of your organization.
- Centrally provide tools and access for your security team to manage security needs on behalf of the organization.
- Set up Amazon Single Sign-On (SSO) to provide access to AWS accounts and resources using your active directory, and customize permissions based on separate job roles.

![[Pasted image 20240229205744.png]]

![[Pasted image 20240229215342.png]]


![[Pasted image 20240229220813.png]]


- <mark style="background: #FFB86CA6;">Apply service control policies (SCPs) to users, accounts, or OUs to control access to AWS resources, services, and Regions within your organization</mark>.
- <mark style="background: #CACFD9A6;">Share AWS resources within your organization using AWS Resource Allocation Management (RAM)</mark>.
- Activate AWS CloudTrail across accounts, which creates a log of all activity in your cloud environment that cannot be turned off or modified by member accounts.
- Organizations provides you with a single consolidated bill.
- In addition, you can view usage from resources across accounts and track costs using AWS Cost Explorer and optimize your usage of compute resources using AWS Compute Optimizer.

![](https://i.imgur.com/ao4m7D9.png)

- AWS Organizations is available to all AWS customers at no additional charge.

The [**AWS Organizations API**](https://docs.aws.amazon.com/organizations/latest/APIReference/Welcome.html) enables automation for account creation and management.

AWS Organizations is available in two feature sets:
- Consolidated billing.
- All features.

- By default, organizations support consolidated billing features.
- Consolidated billing separates paying accounts and linked accounts.

- You can use AWS Organizations to set up a single payment method for all the AWS accounts in your organization through consolidated billing.
- With consolidated billing, you can see a combined view of charges incurred by all your accounts.
- Can also take advantage of pricing benefits from aggregated usage, such as volume discounts for Amazon EC2 and Amazon S3.
- Limit of 20 linked accounts for consolidated billing (default).
- Policies can be assigned at different points in the hierarchy.

Can help with cost control through volume discounts.

Unused reserved EC2 instances are applied across the group.

Paying accounts should be used for billing purposes only.

Billing alerts can be setup at the paying account which shows billing for all linked accounts.

## Key Concepts

Some of the key concepts you need to understand are listed here:

**AWS Organization –** <mark style="background: #FFB86CA6;">an organization is a collection of AWS accounts that you can organize into a hierarchy and manage centrally.</mark>

**AWS Account –** An AWS account is a container for your AWS resources.

**Management Account –** A management account is the AWS account you use to create your organization.

**Member Account –** A member account is an AWS account, other than the management account, that is part of an organization.

**Administrative Root –** An administrative root is the starting point for organizing your AWS accounts. The administrative root is the top-most container in your organization’s hierarchy.

**Organizational Unit (OU) –** <mark style="background: #FF5582A6;">An organizational unit (OU) is a group of AWS accounts within an organization. An OU can also contain other OUs enabling you to create a hierarchy.</mark>

**Policy –** A policy is a “document” with one or more statements that define the controls that you want to apply to a group of AWS accounts. A  
WS Organizations supports a specific type of policy called a **Service Control Policy (SCP)**.  
 An SCP defines the AWS service actions, such as Amazon EC2 RunInstances, that are available for use in different accounts within an organization.

![](https://i.imgur.com/SkOR5Ke.png)


Best practices for the management account:
- [**Use the management account only for tasks that require the management account.**](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_best-practices_mgmt-acct.html#best-practices_mgmt-use)
- [**Use a group email address for the management account’s root user.**](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_best-practices_mgmt-acct.html#best-practices_mgmt-acct_email-address)
- [**Use a complex password for the management account’s root user.**](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_best-practices_mgmt-acct.html#best-practices_mgmt-acct_complex-password)
- [**Enable MFA for your root user credentials.**](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_best-practices_mgmt-acct.html#best-practices_mgmt-acct_mfa)
- [**Add a phone number to the account contact information.**](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_best-practices_mgmt-acct.html#best-practices_mgmt-acct_phone-number)
- [**Review and keep track of who has access.**](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_best-practices_mgmt-acct.html#best-practices_mgmt-acct_review-access)
- [**Document the processes for using the root user credentials.**](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_best-practices_mgmt-acct.html#best-practices_mgmt-acct_document-processes)
- [**Apply controls to monitor access to the root user credentials.**](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_best-practices_mgmt-acct.html#best-practices_mgmt-acct_monitor-access)

## Migrating Accounts between Organizations

Accounts can be migrated between organizations.

- <mark style="background: #ADCCFFA6;">You must have root or IAM access to both the member and management accounts.</mark>

- Use the AWS Organizations console for just a few accounts.  
	Use the AWS Organizations API or AWS Command Line Interface (AWS CLI) if there are many accounts to migrate.

- Billing history and billing reports for all accounts stay with the management account in an organization.

-<mark style="background: #ABF7F7A6;"> Before migration download any billing or report history for any member accounts that you want to keep.</mark>

- <mark style="background: #CACFD9A6;">When a member account leaves an organization, all charges incurred by the account are charged directly to the standalone account.</mark>

Even if the account move only takes a minute to process, it is likely that some charges will be incurred by the member account.

## Service Control Policies (SCPs)
**Service control policies (SCPs)** <mark style="background: #D2B3FFA6;">are a type of organization policy that you can use to manage permissions in your organization.</mark>  
![](https://i.imgur.com/kvwLCoF.png)  
![](https://i.imgur.com/HrjUKII.png)

<mark style="background: #FFF3A3A6;">SCPs offer central control over the maximum available permissions for all accounts in your organization. </mark>  
SCPs help you to ensure your accounts stay within your organization’s access control guidelines.

- <mark style="background: #FF5582A6;">SCPs are available only in an organization that has all features enabled</mark>.
- <mark style="background: #ADCCFFA6;">SCPs aren’t available if your organization has enabled only the consolidated billing features.</mark>

- SCPs alone are not sufficient to granting permissions to the accounts in your organization.

>No permissions are granted by an SCP.  
<mark style="background: #BBFABBA6;">An SCP defines a guardrail, or sets limits, on the actions that the account’s administrator can delegate to the IAM users and roles in the affected accounts.</mark>

<mark style="background: #CACFD9A6;">The administrator must still attach identity-based or resource-based policies to IAM users or roles, or to the resources in your accounts to grant permissions.</mark>

<mark style="background: #BBFABBA6;">The effective permissions are the logical intersection between what is allowed by the SCP and what is allowed by the IAM and resource-based policies.</mark>

SCP Inheritance:
- SCPs **_affect only IAM users and roles_** that are managed by accounts that are part of the organization. <mark style="background: #FF5582A6;">SCPs don’t affect resource-based policies directly. They also don’t affect users or roles from accounts outside the organization.</mark>
- <mark style="background: #FFB86CA6;">An SCP restricts permissions for IAM users and roles in member accounts, including the member account’s root user.</mark>
- Any account has only those permissions permitted by **_every_** parent above it.
- <mark style="background: #BBFABBA6;">If a permission is blocked at any level above the account, either implicitly (by not being included in an Allow policy statement) or explicitly (by being included in a Deny policy statement), a user or role in the affected account can’t use that permission</mark>, even if the account administrator attaches the AdministratorAccess IAM policy with _/_ permissions to the user.
- <mark style="background: #CACFD9A6;">SCPs affect only</mark> **_member_** <mark style="background: #CACFD9A6;">accounts in the organization. They have no effect on users or roles in the management account.</mark>
- Users and roles must still be granted permissions with appropriate IAM permission policies. <mark style="background: #FFF3A3A6;">A user without any IAM permission policies has no access, even if the applicable SCPs allow all services and all actions.</mark>
- <mark style="background: #ADCCFFA6;">If a user or role has an IAM permission policy that grants access to an action that is also allowed by the applicable SCPs, the user or role can perform that action.</mark>
- <mark style="background: #FFB8EBA6;">If a user or role has an IAM permission policy that grants access to an action that is either not allowed or explicitly denied by the applicable SCPs, the user or role can’t perform that action.</mark>
- <mark style="background: #FF5582A6;">SCPs affect all users and roles in attached accounts</mark>, **_including the root user_**.  
	  The only exceptions are those described in [**Tasks and entities not restricted by SCPs**](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_manage_policies_scps.html#not-restricted-by-scp).
- SCPs **_do not_** affect any service-linked role. <mark style="background: #083CA4A6;">Service-linked roles enable other AWS services to integrate with AWS Organizations and can’t be restricted by SCPs</mark>.
- When you disable the SCP policy type in a root, all SCPs are automatically detached from all AWS Organizations entities in that root. AWS Organizations entities include organizational units, organizations, and accounts.
- If you re-enable SCPs in a root, that root reverts to only the default FullAWSAccess policy automatically attached to all entities in the root.
- Any attachments of SCPs to AWS Organizations entities from before SCPs were disabled are lost and aren’t automatically recoverable, although you can manually reattach them.
- If both a permissions boundary (an advanced IAM feature) and an SCP are present, then the boundary, the SCP, and the identity-based policy must all allow the action.

You **_can’t_** use SCPs to restrict the following tasks:
- Any action performed by the management account.
- Any action performed using permissions that are attached to a service-linked role.
- Register for the Enterprise support plan as the root user.
- Change the AWS support level as the root user.
- Provide trusted signer functionality for CloudFront private content.
- Configure reverse DNS for an Amazon Lightsail email server as the root user.
- Tasks on some AWS-related services:
    - Alexa Top Sites.
    - Alexa Web Information Service.
    - Amazon Mechanical Turk.
    - Amazon Product Marketing API.

## Resource Groups

- You can use resource groups to organize your AWS resources.
- In AWS, a resource is an entity that you can work with.

Resource groups make it easier to manage and automate tasks on large numbers of resources at one time.

Resource groups allow you to group resources and then tag them.

The Tag Editor assists with finding resources and adding tags.

**You can access Resource Groups through any of the following entry points:**

- On the navigation bar of the AWS Management Console.
- In the AWS Systems Manager console, from the left navigation pane entry for Resource Groups.
- By using the Resource Groups API, in AWS CLI commands or AWS SDK programming languages.

A resource group is a collection of AWS resources that are all in the same AWS region, and that match criteria provided in a query.

In Resource Groups, there are two types of queries on which you can build a group.

Both query types include resources that are specified in the format AWS::service::resource.

- **Tag-based –** Tag-based queries include lists of resources and tags. Tags are keys that help identify and sort your resources within your organization. Optionally, tags include values for keys.
- **AWS CloudFormation stack-based –** In an AWS CloudFormation stack-based query, you choose an AWS CloudFormation stack in your account in the current region, and then choose resource types within the stack that you want to be in the group. You can base your query on only one AWS CloudFormation stack.

Resource groups can be nested; a resource group can contain existing resource groups in the same region.


# FAQ
## General

Close all

### What is AWS Organizations?

AWS Organizations helps you centrally govern your environment as you scale your workloads on AWS.  
Whether you are a growing startup or a large enterprise, Organizations helps you to programmatically create new accounts and allocate resources, simplify billing by setting up a single payment method for all of your accounts, create groups of accounts to organize your workflows, and apply policies to these groups for governance.  
In addition, AWS Organizations is integrated with other AWS services so you can define central configurations, security mechanisms, and resource sharing across accounts in your organization.

### Which Central Governance and Management Capabilities Does AWS Organizations Enable?

AWS Organizations enables the following capabilities:
- Automate AWS account creation and management, and provision resources with AWS CloudFormation Stacksets
- Maintain a secure environment with policies and management of AWS security services
- Govern access to AWS services, resources, and regions
- Centrally manage policies across multiple AWS accounts
- Audit your environment for compliance 
- View and manage costs with consolidated billing 
- Configure AWS services across multiple accounts

### Which AWS Regions is AWS Organizations Available In?

AWS Organizations is available in all AWS commercial regions, AWS GovCloud (US) regions, and China regions The service endpoints for AWS Organizations are located in US East (N. Virginia) for commercial organizations and AWS GovCloud (US-West) for AWS GovCloud (US) organizations, and AWS China (Ningxia) region, operated by NWCD.

### How Do I Get Started?

To get started, you must first decide which of your AWS accounts will become the management account (formerly known as master account). You can either create a new AWS account or select an existing one.

1. Sign in as an administrator to the [AWS Management Console](https://console.aws.amazon.com/) using the AWS account you want to use to manage your organization.
2. Go to the AWS Organizations console.
3. Choose **Create Organization**.
4. Select what features you want to enable for your organization. Either **all features**, or **consolidated billing only features**. Selecting **all features** is recommended if you want to take advantage of all of the central management capabilities of AWS Organizations.
5. Add AWS accounts to your organization by using one of the following two methods: 
    1. Invite existing AWS accounts to your organization by using their AWS account ID or associated email address.
    2. Create new AWS accounts.
6. Model your organizational hierarchy by grouping your AWS accounts in OUs.
7. Create policies (such as service control policies or backup policies) for OUs, accounts, or the organization (only available for all-features organizations).
8. Enable [AWS services that are integrated with AWS Organizations](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_integrated-services-list.html?org_product_faq_supportedservices).

You can also use the [AWS CLI](https://aws.amazon.com/cli/) (for command-line access) or [SDKs](https://docs.aws.amazon.com/organizations/latest/APIReference/API_CreateOrganization.html?org_product_faq_api) to perform the same steps to create a new organization.

Note: You can initiate the creation of a new organization only from an AWS account that is not already a member of another organization.

For more information, see [Getting started with AWS Organizations](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_getting-started.html?org_product_faq_gs).

## AWS Control Tower

### What is AWS Control Tower?
AWS **Control Tower**, built on AWS services such as AWS Organizations, offers the easiest way to set up and govern a new, secure, multi-account AWS environment.  
It <mark style="background: #ADCCFFA6;">establishes a landing zone, which is a well-architected, multi-account environment based on best-practice blueprints, and enables governance using guardrails you can choose.</mark>  
<mark style="background: #FFF3A3A6;">Guardrails are SCPs and AWS Config rules that implement governance for security, compliance, and operations.</mark>

### What is the Difference between AWS Control Tower and AWS Organizations?

[AWS Control Tower](https://aws.amazon.com/controltower/?org_product_faq_CT) <mark style="background: #BBFABBA6;">offers an abstracted, automated, and prescriptive experience on top of AWS Organizations. It automatically sets up AWS Organizations as the underlying AWS service to organize accounts and implements preventive guardrails using SCPs.</mark>  
Control Tower and Organizations work well together.  
You can use Control Tower to set up your environment and set guardrails, then using AWS Organizations, you can further create custom policies (such as tag, backup or SCPs) that centrally control the use of AWS services and resources across multiple AWS accounts.

### AWS Control Tower Uses Guardrails. What is a Guardrail?
<mark style="background: #FFB86CA6;">Guardrails are pre-packaged SCP and AWS Config governance rules</mark> for security, operations, and compliance that customers can select and apply enterprise-wide or to specific groups of accounts.  
A guardrail is expressed in plain English, and enforces a specific governance policy for your AWS environment that can be enabled within an organizational unit (OU).

### When Should I Use AWS Control Tower?
<mark style="background: #CACFD9A6;">AWS Control Tower is for customers who want to create or manage their multi-account AWS environment with built-in best practices. </mark>  
It offers prescriptive guidance to govern your AWS environment at scale and gives you control over your environment without sacrificing the speed and agility AWS provides for builders.  
<mark style="background: #FFF3A3A6;">You will benefit from AWS Control Tower if you are building a new AWS environment, starting out on your journey on AWS, starting a new cloud initiative, are completely new to AWS, or have an existing multi-account AWS environment.</mark>

## Core Concepts
### What is an Organization?

An organization is a collection of AWS accounts that you can organize into a hierarchy and manage centrally.

### What is an AWS Account?

An AWS account is a container for your AWS resources. You create and manage your AWS resources in an AWS account, and the AWS account provides administrative capabilities for access and billing.

Using multiple AWS accounts is a best practice for scaling your environment, as it provides a natural billing boundary for costs, isolates resources for security, gives flexibility or individuals and teams, in addition to being adaptable for new business processes.

### What is a Management account (formerly Known as Master account)?

A management account is the AWS account you use to create your organization. From the management account, you can create other accounts in your organization, invite and manage invitations for other accounts to join your organization, and remove accounts from your organization. You can also attach policies to entities such as administrative roots, organizational units (OUs), or accounts within your organization. The management account is the ultimate owner of the organization, having final control over security, infrastructure, and finance policies. This account has the role of a payer account and is responsible for paying all charges accrued by the accounts in its organization. You cannot change which account in your organization is the management account.

### What is a Member Account?

A member account is an AWS account, other than the management account, that is part of an organization. If you are an administrator of an organization, you can create member accounts in the organization and invite existing accounts to join the organization. You also can apply policies to member accounts. A member account can belong to only one organization at a time.

### What is an Administrative Root?

An administrative root is contained in the management account and is the starting point for organizing your AWS accounts. The administrative root is the top-most container in your organization’s hierarchy. Under this root, you can create OUs to logically group your accounts and organize these OUs into a hierarchy that best matches your business needs.

### What is an Organizational Unit (OU)?

<mark style="background: #FFF3A3A6;">An organizational unit (OU) is a group of AWS accounts within an organization.</mark> <mark style="background: #CACFD9A6;">An OU can also contain other OUs enabling you to create a hierarchy</mark>.  
For example, you can group all accounts that belong to the same department into a departmental OU. Similarly, you can group all accounts running security services into a security OU. OUs are useful when you need to apply the same controls to a subset of accounts in your organization. Nesting OUs enables smaller units of management. For example, you can create OUs for each workload, then create two nested OUs in each workload OU to divide production workloads from pre-production. These OUs inherit the policies from the parent OU in addition to any controls assigned directly to the team-level OU.

### What is a Policy?

<mark style="background: #FFB86CA6;">A policy is a “document” with one or more statements that define the controls that you want to apply to a group of AWS accounts.</mark> AWS Organizations supports the following policies:
- Backup policies—requires AWS backups on a specified cadence
- <mark style="background: #D2B3FFA6;">Tag policies—defines tag keys and allowed values</mark>
- AI services opt-out policies—controls how AI services store or use content
- [Service Control Policies](https://aws.amazon.com/organizations/faqs/#scps) (SCPs)—<mark style="background: #BBFABBA6;">An SCP defines the AWS service actions, such as Amazon EC2 RunInstances, that are available for use in different accounts within an organization.</mark>

## Organizing AWS Accounts

### Can I Define and Manage My Organization Regionally?

All organization entities are globally accessible, except for organizations managed in China, similar to how AWS Identity and Access Management (IAM) works today. You do not need to specify an AWS Region when you create and manage your organization, but you will need to create a separate organization for accounts used in China. Users in your AWS accounts can use AWS services in any geographic region in which that service is available.

### Can I Change Which AWS account is the Management Account?

<mark style="background: #CACFD9A6;">No. You cannot change which AWS account is the management account. Therefore, you should select your management account carefully.</mark>

### How Do I Add an AWS account to My Organization?

Use one of the following two methods to add an AWS account to your organization:

<u>Method 1: Invite an existing account to join your organization</u>

1\. Sign in as an administrator of the management account and navigate to the AWS Organizations console.

2\. Choose the Accounts tab.

3\. Choose Add account and then choose Invite account.

4\. Provide the email address of the account that you want to invite or the AWS account ID of the account.

**Note**: You can invite more than one AWS account by providing a comma-separated list of email addresses or AWS account IDs.

The specified AWS account receives an email inviting it to join your organization. An administrator in the invited AWS account must accept or reject the request using the AWS Organizations console, AWS CLI, or Organizations API. If the administrator accepts your invitation, the account becomes visible in the list of member accounts in your organization. Any applicable policies, such as [SCPs](https://aws.amazon.com/organizations/faqs/#scps), will be enforced automatically in the newly added account. For example, if your organization has an SCP attached to the root of your organization it will directly be enforced on the newly created accounts.

<u>Method 2: Create an AWS account in your organization</u>

1\. Sign in as an administrator of your management account and navigate to the AWS Organizations console.

2\. Choose the Accounts tab.

3\. Choose Add account and then choose Create account.

4\. Provide a name for the account and the email address for the account.

You can also create an account by using the AWS SDK or AWS CLI. For both methods, after you add the new account, you can move it to an organizational unit (OU). The new account automatically inherits the policies attached to the OU.

### Can an AWS account Be a Member of More than One Organization?

No. An AWS account can be a member of only one organization at a time.

### How Can I Access an AWS account that Was Created in My Organization?

As part of AWS account creation, AWS Organizations creates an IAM role with full administrative permissions in the new account. IAM users and IAM roles with appropriate permissions in the master account can assume this IAM role to gain access to the newly created account.

### Can I Set up Multi-factor Authentication (MFA) on the AWS account that I Create in My Organization Programmatically?

No. This currently is not supported.

### Can I Move an AWS account that I Have Created Using AWS Organizations to Another Organization?

Yes. However, you must first remove the account from your organization and make it a standalone account (see below). After making the account standalone, it can then be invited to join another organization.

### Can I Remove an AWS account that I Created Using Organizations and Make it a Standalone Account?

Yes. When you create an account in an organization using the AWS Organizations console, API, or CLI commands, AWS does not collect all of the information required of standalone accounts.  
For each account that you want to make standalone, you need to update this information, which can include: providing contact information, agreeing to the [AWS Customer Agreement](https://aws.amazon.com/agreement/), providing a valid payment method, and choosing a support plan option.  
AWS uses the payment method to charge for any billable (not AWS Free Tier) AWS activity that occurs while the account is not attached to an organization. 


### How Many AWS Accounts Can I Manage in My Organization?

This can vary. If you need additional accounts, go to the [AWS Support Center](https://console.aws.amazon.com/support/home) and open a support case to request an increase.

### How Can I Remove an AWS Member account from an Organization?

You can remove a member account by using one of the following two methods. You might have to provide additional information to remove an account that you created using Organizations. If the attempt to remove an account fails, go to the [AWS Support Center](https://console.aws.amazon.com/support/home) and ask for help with removing an account.

<u>Method 1: Remove an invited member account by signing in to the management account</u>

1\. Sign in as an administrator of the master account and navigate to the AWS Organizations console.

2\. In the left pane, choose **Accounts**.

3\. Choose the account that you want to remove and then choose **Remove account**.

4\. If the account does not have a valid payment method, you must provide one.

<u>Method 2: Remove an invited member account by signing in to the member account</u>

1\. Sign in as an administrator of the member account that you want to remove from the organization.

2\. Navigate to the AWS Organizations console.

3\. Choose \*Leave organization\*.

4\. If the account does not have a payment method, you must provide one.

### How Can I Create an Organizational Unit (OU)?

To create an OU, follow these steps:

1\. Sign in as an administrator of the management account and navigate to the AWS Organizations console.

2\. Choose the **Organize accounts** tab.

3\. Navigate in the hierarchy to where you want to create the OU. You can create it directly under the root, or you can create it within another OU.

4\. Choose to **Create organizational unit** and provide a name for your OU. The name must be unique within your organization.

**Note**: You can rename the OU later.

You now can add AWS accounts to your OU. You can also use the AWS CLI and AWS APIs to create and manage an OU.

### How Can I Add a Member AWS account to an OU?

Follow these steps to add member accounts to an OU:

1\. In the AWS Organizations console, choose the Organize accounts tab.

2\. Choose the AWS account, and then choose Move account.

3\. In the dialog box, select the OU to which you want to move the AWS account.

Alternatively, you can use the AWS CLI and AWS APIs to add AWS accounts to an OU.

### Can an AWS account Be a Member of Multiple OUs?

<mark style="background: #ADCCFFA6;">No. An AWS account can be a member of only one OU at a time.</mark>

### Can an OU Be a Member of Multiple OUs?

No. An OU can be a member of only one OU at a time.

### How Many Levels Can I Have in My OU Hierarchy?

You can nest your OUs five levels deep. Including root and AWS accounts created in the lowest OUs, your hierarchy can be five levels deep.

## Control Management

### At what Levels of My Organization Can I Apply a Policy?

<mark style="background: #BBFABBA6;">You can attach a policy to the root of your organization (applies to all accounts in your organization), to individual organizational units (OUs), which applies to all accounts in the OU including nested OUs, or to individual accounts.</mark>

### How Can I Attach a Policy?

You can attach a policy in one of two ways:

- In the AWS Organizations console, navigate to where you want to assign the policy (the root, an OU, or an account), and then choose **Attach Policy**.
- In the Organizations console, choose the **Policies** tab and do one of the following:  
    Choose an existing policy, choose **Attach Policy** from the **Actions** drop-down list, and then choose the root, OU, or account to which you want to attach the policy.
- Choose **Create Policy**, and then as part of the policy creation workflow, choose the root, OU, or account to which you want to attach the new policy.

For more information, see [Managing Policies](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_manage_policies.html?org_product_faq_managepolicies).

### Are Policies Inherited through Hierarchical Connections in My Organization?

Yes. For example, let’s assume that you have arranged your AWS accounts into OUs according to your application development stages: DEV, TEST, and PROD. Policy P1 is attached to the organization’s root, policy P2 is attached to the DEV OU, and policy P3 is attached to AWS account A1 in the DEV OU. With this setup, P1+P2+P3 all apply to account A1.  
For more information, see [About Service Control Policies](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_manage_policies_about-scps.html?org_product_faq_aboutSCP).

### What Types of Policies Does AWS Organizations Support?

Currently, AWS Organizations supports the following policies:

- Backup policies—requires backups on a specified cadence using AWS Backup
- Tag policies—defines tag keys and allowed values
- AI services opt-out policies—controls how AI services store or use content from the organization
- Service Control Policies (SCPs)—define and enforce the actions that IAM users, groups, and roles can perform in the accounts to which the SCP is applied

### What is a Service Control Policy (SCP)?

<mark style="background: #D2B3FFA6;">Service Control Policies (SCPs) allow you to control which AWS service actions are accessible to principals (account root, IAM users, and IAM roles) in the accounts of your organization.</mark> 

An SCP is required but is not the only control that determines which principals in an account can access resources to grant principals in an account access to resources.  
The effective permission on a principal in an account that has an SCP attached is the intersection of what is allowed explicitly in the SCP and what is allowed explicitly in the permissions attached to the principal. For example, if an SCP applied to an account states that the only actions allowed are Amazon EC2 actions, and the permissions on a principal in the same AWS account allow both EC2 actions and Amazon S3 actions, the principal is able to access only the EC2 actions.  
Principals in a member account (including the root user for the member account) cannot remove or change SCPs that are applied to that account.  

### What Does an SCP Look Like?

SCPs follow the same rules and grammar as IAM policies.  
For information about SCP syntax, see [SCP Syntax](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_reference_scp-syntax.html). For example SCPs, see [Example Service Control Policies](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_manage_policies_example-scps.html).  

{ 

 "Version":"2012-10-17", 

 "Statement":\[ 

 { 

 "Effect":"Allow", 

 "Action":\["EC2:\*","S3:\*"\], 

 "Resource":"\*" 

 } 

 \] 

 }

<u>Blacklist example</u>  
The following SCP allows access to all AWS service actions except the S3 action, PutObject. All principals (account root, IAM user, and IAM role) with appropriate permissions assigned directly to them in an account with this SCP applied can access any action except the S3 PutObject action. 

{ 

 "Version":"2012-10-17", 

 "Statement":\[ 

 { 

 "Effect":"Allow", 

 "Action": "\*:\*", 

 "Resource":"\*" 

 }, 

 { 

 "Effect":"Deny", 

 "Action":"S3:PutObject", 

 "Resource":"\*" 

 } 

 \] 

 }

For more examples, see [Strategies for Using SCPs](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_manage_policies_about-scps.html#SCP_strategies).

### If I Attach an Empty SCP to an AWS Account, Does that Mean that I Allow All AWS Service Actions in that AWS Account?

No. SCPs behave the same way as IAM policies: an empty IAM policy is equivalent to a default DENY. <mark style="background: #FF5582A6;">Attaching an empty SCP to an account is equivalent to attaching a policy that explicitly denies all actions.</mark>

### What Are the effective Permissions if I Apply an SCP to My Organization and My Principals also Have IAM Policies?

The effective permissions granted to a principal (account root, IAM user, and IAM role) in an AWS account with an SCP applied are the intersection between those allowed by the SCP and the permissions granted to the principal by IAM permission policies. For example, if an IAM user has "Allow": "ec2:\* " and "Allow": "sqs:\* ", and the SCP attached to the account has "Allow": "ec2:\* " and "Allow": "s3:\* ", the resultant permission for the IAM user is "Allow": "ec2:\* " The principal cannot perform any Amazon SQS (not allowed by the SCP) or S3 actions (not granted by the IAM policy).

### Can I Simulate the Effect of an SCP on an AWS Account?

Yes, the IAM policy simulator can include the effects of SCPs. You can use the policy simulator in a member account in your organization to understand the effect on individual principals in that account. An administrator in a member account with the appropriate AWS Organizations permissions can see if an SCP is affecting the access for the principals (account root, IAM user, and IAM role) in your member account.  
For more information, see [Service Control Policies](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_manage_policies_scp.html?org_product_faq_scp).

### Can I Create and Manage an Organization without Enforcing an SCP?

Yes. You decide which policies that you want to enforce.  
For example, you could create an organization that takes advantage only of the consolidated billing functionality. This allows you to have a single-payer account for all accounts in your organization and automatically receive default tiered-pricing benefits.

## Billing

Close all

### What Does AWS Organizations Cost?

AWS Organizations is offered at no additional charge.

### Who Pays for Usage Incurred by Users under an AWS Member account in My Organization?

<mark style="background: #FFF3A3A6;">The owner of the management account is responsible for paying for all usage, data, and resources used by the accounts in the organization.</mark>

### Will My Bill Reflect the Organizational Unit Structure that I Created in My Organization?

No. For now, your bill will not reflect the structure that you have defined in your organization. You can use [cost allocation tags](https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/cost-alloc-tags.html) in individual AWS accounts to categorize and track your AWS costs, and this allocation will be visible in the consolidated bill for your organization.

## Integrated AWS Services

### Why Should I Enable an AWS Service Integrated with AWS Organizations?

AWS services have integrated with AWS Organizations to provide customers with centralized management and configuration across accounts in their organization. This enables you to manage services across your accounts from a single place, simplifying deployment and configurations.

### Which AWS Services Are Currently Integrated with AWS Organizations?

For a list of AWS services integrated with AWS Organizations, see [AWS Services That You Can Use with AWS Organizations](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_integrated-services-list.html?org_product_faq_services).