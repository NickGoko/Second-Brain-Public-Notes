---
tags:
  - cloud/aws
Associations: "[[Security- IAM]]"
---

# Introduction

![[Module 8 - Securing User and Application Access#AWS Identity and Access Management(IAM)]]



![[Pasted image 20240215083140.png]]  
![](https://i.imgur.com/090nyOZ.png)

 ![](https://i.imgur.com/lI8Me5r.png)  
![](https://i.imgur.com/LyAF159.png)  
  ![](https://i.imgur.com/3EvVEMd.png)  
![](https://i.imgur.com/AaQ9yAV.png)  
![](https://i.imgur.com/X52UOk1.png)

![](https://i.imgur.com/GmHizsM.png)

![](https://i.imgur.com/VQ9fSkB.png)


![[Pasted image 20240229221344.png]]
## IAM Features
IAM gives you the following features:  
**Shared access to your AWS account**  
You can grant other people permission to administer and use resources in your AWS account without having to share your password or access key.

**Granular permissions**  
You can grant different permissions to different people for different resources. For example, you might allow some users complete access to Amazon Elastic Compute Cloud (Amazon EC2), Amazon Simple Storage Service (Amazon S3), Amazon DynamoDB, Amazon Redshift, and other AWS services. For other users, you can allow read-only access to just some S3 buckets, or permission to administer just some EC2 instances, or to access your billing information but nothing else.

**Secure access to AWS resources for applications that run on Amazon EC2**  
You can use IAM features to securely provide credentials for applications that run on EC2 instances. These credentials provide permissions for your application to access other AWS resources. Examples include S3 buckets and DynamoDB tables.

**Multi-factor authentication (MFA)**  
You can add two-factor authentication to your account and to individual users for extra security. With MFA you or your users must provide not only a password or access key to work with your account, but also a code from a specially configured device. If you already use a FIDO security key with other services, and it has an AWS supported configuration, you can use WebAuthn for MFA security. For more information, see [Supported configurations for using FIDO security keys](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_mfa_fido_supported_configurations.html).

**Identity federation**

You can allow users who already have passwords elsewhere—for example, in your corporate network or with an internet identity provider—to get temporary access to your AWS account.

**Identity information for assurance**

If you use [AWS CloudTrail](https://aws.amazon.com/cloudtrail/), you receive log records that include information about those who made requests for resources in your account. That information is based on IAM identities.

**PCI DSS Compliance**

IAM supports the processing, storage, and transmission of credit card data by a merchant or service provider, and has been validated as being compliant with Payment Card Industry (PCI) Data Security Standard (DSS). For more information about PCI DSS, including how to request a copy of the AWS PCI Compliance Package, see [PCI DSS Level 1](https://aws.amazon.com/compliance/pci-dss-level-1-faqs/).

**Integrated with many AWS services**

For a list of AWS services that work with IAM, see [AWS services that work with IAM](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_aws-services-that-work-with-iam.html).

**Eventually Consistent**

IAM, like many other AWS services, is [eventually consistent](https://wikipedia.org/wiki/Eventual_consistency). IAM achieves high availability by replicating data across multiple servers within Amazon's data centers around the world. If a request to change some data is successful, the change is committed and safely stored. However, the change must be replicated across IAM, which can take some time. Such changes include creating or updating users, groups, roles, or policies. We recommend that you do not include such IAM changes in the critical, high-availability code paths of your application. Instead, make IAM changes in a separate initialization or setup routine that you run less frequently. Also, be sure to verify that the changes have been propagated before production workflows depend on them. For more information, see [Changes that I make are not always immediately visible](https://docs.aws.amazon.com/IAM/latest/UserGuide/troubleshoot_general.html#troubleshoot_general_eventual-consistency).

**Free to use**

AWS Identity and Access Management (IAM) and AWS Security Token Service (AWS STS) are features of your AWS account offered at no additional charge. You are charged only when you access other AWS services using your IAM users or AWS STS temporary security credentials. For information about the pricing of other AWS products,

To help secure your AWS resources, follow these best practices for AWS Identity and Access Management (IAM).  
		![](https://i.imgur.com/ASakfc3.png)  

### Roles terms and Concepts
 ![](https://i.imgur.com/rUbgLSX.png)

 ![](https://i.imgur.com/q6zJDHN.png)

[IAM ROLE](#) = is an IAM identity that you can create that has specific permissions.  
<mark style="background: #ADCCFFA6;">So in summary. A role is a AWS identity like a User. However the difference is a roles can be assumed by anyone who needs it and a Role doesn't need standard long term credentials like a password or access keys like a User would need. It provides temporary security credentials for your role session. </mark>

Roles can be used by the following:
- An IAM user in the same AWS account as the role
- An IAM user in a different AWS account than the role
- A web service offered by AWS such as Amazon Elastic Compute Cloud (Amazon EC2)
- An external user authenticated by an external identity provider (IdP) service that is compatible with SAML 2.0 or OpenID Connect, or a custom-built identity broker.

You can use roles to <mark style="background: #CACFD9A6;">delegate access to users, applications, or services that don't normally have access to your AWS resources</mark>. 
1. For example granting users in your AWS account access to resources they don't have. Roles can also be used to grand access to resources in another account.
2. Roles can be used to allow a mobile app to use AWS resources. Because you don't want to embed AWS keys within the app.(where is tough to update and user can extract them)
3. Roles can also be use to grant access to users who have identities outside AWS. Identities like a corporate directory.
4. Roles can also be used to grant access to third parties who can perform an audit on your resources. 

[AWS service role](#)  
	A service role is an role/IAM Role that a service assumes to perform actions on your behalf. An IAM administrator can create, modify, and delete a service role from within IAM.  
	A role that a service assumes to perform actions on your behalf is called a service role.  
	When a role serves a specialized purpose for a service, it is categorized as a [service role for EC2 instances](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_terms-and-concepts.html#iam-term-service-role-ec2) (for example), or a [[#^fd6465|Service Linked Role]]  
	- You must configure permissions to allow an <mark style="background: #ABF7F7A6;">IAM entity (user or role) </mark>to create or edit a service role. As i will show below on this document.  
	- ![](https://i.imgur.com/G0JUxH8.png)  
	![](https://i.imgur.com/qCb5wH6.png)  
	[To allow an IAM entity to create any service role](#)  
	AWS recommends that you <mark style="background: #BBFABBA6;">allow only administrative users to create any service role</mark>. <mark style="background: #FF5582A6;">A person with permissions to create a role and attach any policy can escalate their own permissions</mark>. Instead, create a policy that allows them to create only the roles that they need or have an administrator create the service role on their behalf.  
	To attach a policy that allows an administrator to access your entire AWS account, use the [AdministratorAccess](https://console.aws.amazon.com/iam/home#policies/arn:aws:iam::aws:policy/AdministratorAccess)  AWS managed policy.  
	[To allow an IAM entity to edit a service role](#)  
	Add the following policy to the IAM entity that needs to edit the service role.
```JSON
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "EditSpecificServiceRole",
            "Effect": "Allow",
            "Action": [
                "iam:AttachRolePolicy",
                "iam:DeleteRolePolicy",
                "iam:DetachRolePolicy",
                "iam:GetRole",
                "iam:GetRolePolicy",
                "iam:ListAttachedRolePolicies",
                "iam:ListRolePolicies",
                "iam:PutRolePolicy",
                "iam:UpdateRole",
                "iam:UpdateRoleDescription"
            ],
            "Resource": "arn:aws:iam::*:role/SERVICE-ROLE-NAME"
        },
        {
            "Sid": "ViewRolesAndPolicies",
            "Effect": "Allow",
            "Action": [
                "iam:GetPolicy",
                "iam:ListRoles"
            ],
            "Resource": "*"
        }
    ]
}
```
[To allow an IAM entity to delete a specific service role](#)  
Add the following statement to the permissions policy for the IAM entity that needs to delete the specified service role.
```json
{
    "Effect": "Allow",
    "Action": "iam:DeleteRole",
    "Resource": "arn:aws:iam::*:role/SERVICE-ROLE-NAME"
}
```

[To allow an IAM entity to delete any service role](#)  
AWS recommends that you allow only administrative users to delete any service role. Instead, create a policy that allows them to delete only the roles that they need or have an administrator delete the service role on their behalf.
>[!bookmark]
>## Creating a role for a service (AWS CLI)
Creating a role from the AWS CLI involves multiple steps. When you use the console to create a role, many of the steps are done for you, but with the AWS CLI you must explicitly perform each step yourself.  
You must create the role and then assign a permissions policy to the role. If the service you are working with is Amazon EC2, then you must also create an instance profile and add the role to it.

[AWS service role for an EC2 instance](#)  
	![](https://i.imgur.com/DrgtdoQ.png)  
	[Using an IAM role to grant permissions to applications running on Amazon EC2 instances](#)  
	- Applications that run on an Amazon EC2 instance must include AWS credentials in the AWS API requests. You could have your developers store AWS credentials directly within the Amazon EC2 instance and allow applications in that instance to use those credentials. But developers would then have to manage the credentials and ensure that they securely pass the credentials to each instance and update each Amazon EC2 instance when it's time to update the credentials. That's a lot of additional work.  
	- Instead, you can and should use an IAM role to manage _temporary_ credentials for applications that run on an Amazon EC2 instance. When you use a role, you don't have to distribute long-term credentials (such as sign-in credentials or access keys) to an Amazon EC2 instance. Instead, the role supplies temporary permissions that applications can use when they make calls to other AWS resources. When you launch an Amazon EC2 instance, you specify an IAM role to associate with the instance. Applications that run on the instance can then use the role-supplied temporary credentials to sign API requests.  
	- Using roles to grant permissions to applications that run on Amazon EC2 instances requires a bit of extra configuration. An application running on an Amazon EC2 instance is abstracted from AWS by the virtualized operating system. Because of this extra separation, you need an additional step to assign an AWS role and its associated permissions to an Amazon EC2 instance and make them available to its applications.  
	This extra step is the creation of an _[instance profile](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_use_switch-role-ec2_instance-profiles.html)_ attached to the instance.  
	The instance profile contains the role and can provide the role's temporary credentials to an application that runs on the instance. Those temporary credentials can then be used in the application's API calls to access resources and to limit access to only those resources that the role specifies.  
	![](https://i.imgur.com/UWZq7uL.png)  
	Using roles in this way has several benefits. Because role credentials are temporary and updated automatically, you don't have to manage credentials, and you don't have to worry about long-term security risks. In addition, if you use a single role for multiple instances, you can make a change to that one role and the change propagates automatically to all the instances.  
	![](https://i.imgur.com/DMFFFcJ.png) ^85ea08

[AWS service-linked role](#)  
A service-linked role is a type of service role that is linked to an AWS service. The service can assume the role to perform an action on your behalf. Service-linked roles appear in your AWS account and are owned by the service. An IAM administrator can view, but not edit the permissions for service-linked roles.  
![](https://i.imgur.com/FNZjLEq.png) ^fd6465

[Role Chaining](#)  
	Role chaining is when you use a role to assume a second role through the AWS CLI or API. For example, `RoleA` has permission to assume `RoleB`. You can enable User1 to assume `RoleA` by using their long-term user credentials in the AssumeRole API operation. This returns `RoleA` short-term credentials. With role chaining, you can use `RoleA`'s short-term credentials to enable User1 to assume `RoleB`.  
	When you assume a role, you can pass a session tag and set the tag as transitive. Transitive session tags are passed to all subsequent sessions in a role chain. To learn more about session tags, see [Passing session tags in AWS STS](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_session-tags.html).  
	Role chaining limits your AWS CLI or AWS API role session to a maximum of one hour. When you use the [AssumeRole](https://docs.aws.amazon.com/STS/latest/APIReference/API_AssumeRole.html) API operation to assume a role, you can specify the duration of your role session with the `DurationSeconds` parameter. You can specify a parameter value of up to 43200 seconds (12 hours), depending on the [maximum session duration setting](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_use.html#id_roles_use_view-role-max-session) for your role. However, if you assume a role using role chaining and provide a `DurationSeconds` parameter value greater than one hour, the operation fails.  
	AWS does not treat using roles to [grant permissions to applications that run on EC2 instances](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_use_switch-role-ec2.html) as role chaining.

[Delegation](#)  
	The granting of permissions to someone to allow access to resources that you control. Delegation involves setting up a trust between two accounts. The first is the account that owns the resource (the trusting account). The second is the account that contains the users that need to access the resource (the trusted account). The trusted and trusting accounts can be any of the following:  
	- The same account.  
	- Separate accounts that are both under your organization's control.  
	- Two accounts owned by different organizations.  
	To delegate permission to access a resource, you [create an IAM role](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_create_for-user.html) in the trusting account that has two [policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_terms-and-concepts.html#term_policy) attached. The _permissions policy_ grants the user of the role the needed permissions to carry out the intended tasks on the resource. The _trust policy_ specifies which trusted account members are allowed to assume the role.  
	When you create a trust policy, you cannot specify a wildcard `(*) `as part of and ARN in the principal element. The trust policy is attached to the role in the trusting account, and is one-half of the permissions. The other half is a permissions policy attached to the user in the trusted account that [allows that user to switch to, or assume the role](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_use_permissions-to-switch.html). A user who assumes a role temporarily gives up his or her own permissions and instead takes on the permissions of the role. When the user exits, or stops using the role, the original user permissions are restored. An additional parameter called [external ID](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_create_for-user_externalid.html) helps ensure secure use of roles between accounts that are not controlled by the same organization.

[Federation](#)  
	The creation of a trust relationship between an external identity provider and AWS. Users can sign in to a web identity provider, such as **Login with Amazon**, **Facebook**, **Google**, or any IdP that is compatible with **OpenID Connect** (OIDC). Users can also sign in to an enterprise identity system that is compatible with Security Assertion Markup Language (SAML) 2.0, such as Microsoft Active Directory Federation Services. When you use OIDC and SAML 2.0 to configure a trust relationship between these external identity providers and AWS, the user is assigned to an IAM role. The user also receives temporary credentials that allow the user to access your AWS resources.

[Federated User](#)  
	Instead of creating an IAM user, you can use existing identities from AWS Directory Service, your enterprise user directory, or a web identity provider. These are known as _federated users_. AWS assigns a role to a federated user when access is requested through an [identity provider](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_providers.html). For more information about federated users, see [Federated users and roles](https://docs.aws.amazon.com/IAM/latest/UserGuide/introduction_access-management.html#intro-access-roles).

[Trust Policy](#)  
	A [JSON policy document](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_grammar.html) in which you define the principals that you _trust_ to assume the role. A role trust policy is a required [resource-based policy](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies.html#policies_resource-based) that is attached to a role in IAM. The [principals](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_elements_principal.html) that you can specify in the trust policy include users, roles, accounts, and services.

	
**Permissions policy***

A permissions document in [JSON](http://www.json.org/) format in which you define what actions and resources the role can use. The document is written according to the rules of the [IAM policy language](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies.html).

**Permissions boundary**

An advanced feature in which you use policies to limit the maximum permissions that an identity-based policy can grant to a role. You cannot apply a permissions boundary to a service-linked role. For more information, see [Permissions boundaries for IAM entities](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_boundaries.html).

**Principal**

An entity in AWS that can perform actions and access resources. A principal can be an AWS account root user, an IAM user, or a role. You can grant permissions to access a resource in one of two ways:

- You can attach a permissions policy to a user (directly, or indirectly through a group) or to a role.
    
- For those services that support [resource-based policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/introduction_access-management.html#intro-access-resource-based-policies), you can identify the principal in the `Principal` element of a policy attached to the resource.
    

If you reference an AWS account as principal, it generally means any principal defined within that account.  
![](https://i.imgur.com/JIIziP5.png)

[Role for cross-account access](#)  
A role that grants access to resources in one account to a trusted principal in a different account. Roles are the primary way to grant cross-account access. However, some AWS services allow you to attach a policy directly to a resource (instead of using a role as a proxy). These are called resource-based policies, and you can use them to grant principals in another AWS account access to the resource. Some of these resources include Amazon Simple Storage Service (S3) buckets, S3 Glacier vaults, Amazon Simple Notification Service (SNS) topics, and Amazon Simple Queue Service (SQS) queues. To learn which services support resource-based policies, see [AWS services that work with IAM](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_aws-services-that-work-with-iam.html). For more information about resource-based policies, see [Cross account resource access in IAM](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies-cross-account-resource-access.html).



### Policies and Permissions in IAM
You manage access in AWS by creating policies and attaching them to IAM identities (users, groups of users, or roles) or AWS resources. A policy is an object in AWS that, when associated with an identity or resource, defines their permissions. AWS evaluates these policies when an IAM principal (user or role) makes a request. Permissions in the policies determine whether the request is allowed or denied. Most policies are stored in AWS as JSON documents.  
AWS supports six types of policies: _identity-based policies, resource-based policies, permissions boundaries, Organizations SCPs, ACLs, and session policies._  
[Policy types](#)  
	The following policy types, listed in order from most frequently used to less frequently used, are available for use in AWS. For more details, see the sections below for each policy type.
- **[Identity-based policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies.html#policies_id-based)** – Attach [managed](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies.html#managedpolicy) and [inline](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies.html#inline) policies to IAM identities (users, groups to which users belong, or roles). Identity-based policies grant permissions to an identity.
- Identity-based policies are JSON permissions policy documents that control what actions an identity (users, groups of users, and roles) can perform, on which resources, and under what conditions. Identity-based policies can be further categorized:
	- **Managed policies** – Standalone identity-based policies that you can attach to multiple users, groups, and roles in your AWS account. There are two types of managed policies:
	    - **AWS managed policies** – Managed policies that are created and managed by AWS.
	    - **Customer managed policies** – Managed policies that you create and manage in your AWS account. Customer managed policies provide more precise control over your policies than AWS managed policies.
	- **Inline policies** – Policies that you add directly to a single user, group, or role. Inline policies maintain a strict one-to-one relationship between a policy and an identity. They are deleted when you delete the identity.
    
- **[Resource-based policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies.html#policies_resource-based)** – Attach inline policies to resources. The most common examples of resource-based policies are Amazon S3 bucket policies and IAM role trust policies. Resource-based policies grant permissions to the principal that is specified in the policy. Principals can be in the same account as the resource or in other accounts.
	- Resource-based policies are JSON policy documents that you attach to a resource such as an Amazon S3 bucket. These policies grant the specified principal permission to perform specific actions on that resource and defines under what conditions this applies. Resource-based policies are inline policies. There are no managed resource-based policies.  
	To enable cross-account access, you can specify an entire account or IAM entities in another account as the principal in a resource-based policy. Adding a cross-account principal to a resource-based policy is only half of establishing the trust relationship. When the principal and the resource are in separate AWS accounts, you must also use an identity-based policy to grant the principal access to the resource. However, if a resource-based policy grants access to a principal in the same account, no additional identity-based policy is required.  
	The IAM service supports only one type of resource-based policy called a role _trust policy_, which is attached to an IAM role. An IAM role is both an identity and a resource that supports resource-based policies. For that reason, you must attach both a trust policy and an identity-based policy to an IAM role. Trust policies define which principal entities (accounts, users, roles, and federated users) can assume the role.


- **[Permissions boundaries](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies.html#policies_bound)** – Use a managed policy as the permissions boundary for an IAM entity (user or role). That policy defines the maximum permissions that the identity-based policies can grant to an entity, but does not grant permissions. Permissions boundaries do not define the maximum permissions that a resource-based policy can grant to an entity.
	- A permissions boundary is an advanced feature in which you set the maximum permissions that an identity-based policy can grant to an IAM entity. When you set a permissions boundary for an entity, the entity can perform only the actions that are allowed by both its identity-based policies and its permissions boundaries. Resource-based policies that specify the user or role as the principal are not limited by the permissions boundary. An explicit deny in any of these policies overrides the allow.
    
- **[Organizations SCPs](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies.html#policies_scp)** – Use an AWS Organizations service control policy (SCP) to define the maximum permissions for account members of an organization or organizational unit (OU). SCPs limit permissions that identity-based policies or resource-based policies grant to entities (users or roles) within the account, but do not grant permissions.
	- AWS Organizations is a service for grouping and centrally managing the AWS accounts that your business owns. If you enable all features in an organization, then you can apply service control policies (SCPs) to any or all of your accounts. SCPs are JSON policies that specify the maximum permissions for an organization or organizational unit (OU). The SCP limits permissions for entities in member accounts, including each AWS account root user. An explicit deny in any of these policies overrides the allow.
    
- **[Access control lists (ACLs)](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies.html#policies_acl)** – Use ACLs to control which principals in other accounts can access the resource to which the ACL is attached. ACLs are similar to resource-based policies, although they are the only policy type that does not use the JSON policy document structure. ACLs are cross-account permissions policies that grant permissions to the specified principal. ACLs cannot grant permissions to entities within the same account.
	- Access control lists (ACLs) are service policies that allow you to control which principals in another account can access a resource. ACLs cannot be used to control access for a principal within the same account. ACLs are similar to resource-based policies, although they are the only policy type that does not use the JSON policy document format. Amazon S3, AWS WAF, and Amazon VPC are examples of services that support ACLs.
    
- **[Session policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies.html#policies_session)** – Pass advanced session policies when you use the AWS CLI or AWS API to assume a role or a federated user. Session policies limit the permissions that the role or user's identity-based policies grant to the session. Session policies limit permissions for a created session, but do not grant permissions. For more information, see [Session Policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies.html#policies_session).
	- Session policies are advanced policies that you pass as a parameter when you programmatically create a temporary session for a role or federated user. The permissions for a session are the intersection of the identity-based policies for the IAM entity (user or role) used to create the session and the session policies. Permissions can also come from a resource-based policy. An explicit deny in any of these policies overrides the allow.  
	You can create role session and pass session policies programmatically using the `AssumeRole`, `AssumeRoleWithSAML`, or `AssumeRoleWithWebIdentity` API operations. You can pass a single JSON inline session policy document using the `Policy` parameter. You can use the `PolicyArns` parameter to specify up to 10 managed session policies. For more information about creating a role session, see [Requesting temporary security credentials](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_temp_request.html).

	When you create a federated user session, you use the access keys of the IAM user to programmatically call the `GetFederationToken` API operation. You must also pass session policies. The resulting session's permissions are the intersection of the identity-based policy and the session policy. For more information about creating a federated user session, see [GetFederationToken—federation through a custom identity broker](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_temp_request.html#api_getfederationtoken).

	A resource-based policy can specify the ARN of the user or role as a principal. In that case, the permissions from the resource-based policy are added to the role or user's identity-based policy before the session is created. The session policy limits the total permissions granted by the resource-based policy and the identity-based policy. The resulting session's permissions are the intersection of the session policies and the resource-based policies plus the intersection of the session policies and identity-based policies.  
	![](https://i.imgur.com/nJ6UUZQ.png)  
![](https://i.imgur.com/8EaAPeg.png)  
![](https://i.imgur.com/OrO6AXO.png)  
A permissions boundary can set the maximum permissions for a user or role that is used to create a session. In that case, the resulting session's permissions are the intersection of the session policy, the permissions boundary, and the identity-based policy. However, a permissions boundary does not limit permissions granted by a resource-based policy that specifies the ARN of the resulting session.  
![](https://i.imgur.com/Q3k3nFR.png)

[Policies and the root user](#)

The AWS account root user is affected by some policy types but not others. You cannot attach identity-based policies to the root user, and you cannot set the permissions boundary for the root user. However, you can specify the root user as the principal in a resource-based policy or an ACL. A root user is still the member of an account. If that account is a member of an organization in AWS Organizations, the root user is affected by any SCPs for the account.

### TopicsSecurity Best Practices
- [Require human users to use federation with an identity provider to access AWS using temporary credentials](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html#bp-users-federation-idp)
	- Human users, also known as _human identities,_ are the people, administrators, developers, operators, and consumers of your applications. They must have an identity to access your AWS environments and applications. Human users that are members of your organization are also known as _workforce identities._ Human users can also be external users with whom you collaborate, and who interact with your AWS resources. They can do this via a web browser, client application, mobile app, or interactive command-line tools.

	Require your human users to use temporary credentials when accessing AWS. You can use an identity provider for your human users to provide federated access to AWS accounts by assuming roles, which provide temporary credentials. For centralized access management, we recommend that you use [AWS IAM Identity Center (IAM Identity Center)](https://docs.aws.amazon.com/singlesignon/latest/userguide/getting-started.html) to manage access to your accounts and permissions within those accounts. You can manage your user identities with IAM Identity Center, or manage access permissions for user identities in IAM Identity Center from an external identity provider. For more information, see [What is AWS IAM Identity Center](https://docs.aws.amazon.com/singlesignon/latest/userguide/what-is.html) in the _AWS IAM Identity Center User Guide_.

- [Require workloads to use temporary credentials with IAM roles to access AWS](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html#bp-workloads-use-roles)
- [Require multi-factor authentication (MFA)](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html#enable-mfa-for-privileged-users)
- [Update access keys when needed for use cases that require long-term credentials](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html#rotate-credentials)
- [Follow best practices to protect your root user credentials](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html#lock-away-credentials)
- [Apply least-privilege permissions](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html#grant-least-privilege)
- [Get started with AWS managed policies and move toward least-privilege permissions](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html#bp-use-aws-defined-policies)
- [Use IAM Access Analyzer to generate least-privilege policies based on access activity](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html#bp-gen-least-privilege-policies)
- [Regularly review and remove unused users, roles, permissions, policies, and credentials](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html#remove-credentials)
- [Use conditions in IAM policies to further restrict access](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html#use-policy-conditions)
- [Verify public and cross-account access to resources with IAM Access Analyzer](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html#bp-preview-access)
- [Use IAM Access Analyzer to validate your IAM policies to ensure secure and functional permissions](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html#best-practice-policy-validation)
- [Establish permissions guardrails across multiple accounts](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html#bp-permissions-guardrails)
- [Use permissions boundaries to delegate permissions management within an account](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html#bp-permissions-boundaries)


### [Business use case for IAM](https://docs.aws.amazon.com/IAM/latest/UserGuide/IAM_UseCases.html)


### Common Scenarios for Roles: Users, Applications, and Services
As with most AWS features, you generally have two ways to use a role: interactively in the IAM console, or programmatically with the AWS CLI, Tools for Windows PowerShell, or API. • IAM users in your account using the IAM console can switch to a role to temporarily use the permissions of the role in the console. The users give up their original permissions and take on the permissions assigned to the role. When the users exit the role, their original permissions are restored. • An application or a service offered by AWS (like Amazon EC2) can assume a role by requesting temporary security credentials for a role with which to make programmatic requests to AWS. You use a role this way so that you don't have to share or maintain long-term security credentials (for example, by creating an IAM user) for each entity that requires access to a resource.

The simplest way to use roles is to grant your IAM users permissions to switch to roles that you create within your own or another AWS account. They can switch roles easily using the IAM console to use permissions that you don't ordinarily want them to have, and then exit the role to surrender those permissions. This can help prevent accidental access to or modification of sensitive resources. For more complex uses of roles, such as granting access to applications and services, or federated external users, you can call the AssumeRole API. This API call returns a set of temporary credentials that the application can use in subsequent API calls. Actions attempted with the temporary credentials have only the permissions granted by the associated role. An application doesn't have to "exit" the role the way a user in the console does; rather the application simply stops using the temporary credentials and resumes making calls with the original credentials. Federated users sign in by using credentials from an identity provider (IdP). AWS then provides temporary credentials to the trusted IdP to pass on to the user for including in subsequent AWS resource requests. Those credentials provide the permissions granted to the assigned role.

This section provides overviews of the following scenarios:

- [Provide access for an IAM user in one AWS account that you own to access resources in another account that you own](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_common-scenarios_aws-accounts.html)
- [Provide access to non AWS workloads](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_common-scenarios_non-aws.html)
- [Provide access to IAM users in AWS accounts owned by third parties](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_common-scenarios_third-party.html)
- [Provide access for services offered by AWS to AWS resources](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_common-scenarios_services.html)
- [Provide access for externally authenticated users (identity federation)](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_common-scenarios_federated-users.html)








![](https://i.imgur.com/ykLpqU9.png)  
![](https://i.imgur.com/bOwrM3c.png)  



### ABACAttribute-based Access Control
Attribute-based access control (ABAC) is an authorization strategy that defines permissions based on attributes. In AWS, these attributes are called _tags_. You can attach tags to IAM resources, including IAM entities (users or roles) and to AWS resources. You can create a single ABAC policy or small set of policies for your IAM principals. These ABAC policies can be designed to allow operations when the principal's tag matches the resource tag. ABAC is helpful in environments that are growing rapidly and helps with situations where policy management becomes cumbersome.

For example, you can create three roles with the `access-project` tag key. Set the tag value of the first role to `Heart`, the second to `Star`, and the third to `Lightning`. You can then use a single policy that allows access when the role and the resource are tagged with the same value for `access-project`. For a detailed tutorial that demonstrates how to use ABAC in AWS, see [IAM tutorial: Define permissions to access AWS resources based on tags](https://docs.aws.amazon.com/IAM/latest/UserGuide/tutorial_attribute-based-access-control.html).  
![](https://i.imgur.com/DepYQXa.png)


#### Comparing ABAC to the Traditional RBAC Model
The traditional authorization model used in IAM is called role-based access control (RBAC). RBAC defines permissions based on a person's job function, known outside of AWS as a _role_. Within AWS a role usually refers to an IAM role, which is an identity in IAM that you can assume. IAM does include [managed policies for job functions](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_job-functions.html) that align permissions to a job function in an RBAC model.

In IAM, you implement RBAC by creating different policies for different job functions. You then attach the policies to identities (IAM users, groups of users, or IAM roles). As a [best practice](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html), you grant the minimum permissions necessary for the job function. This is known as [granting least privilege](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html#grant-least-privilege). Do this by listing the specific resources that the job function can access. The disadvantage to using the traditional RBAC model is that when employees add new resources, you must update policies to allow access to those resources.

For example, assume that you have three projects, named `Heart`, `Star`, and `Lightning`, on which your employees work. You create an IAM role for each project. You then attach policies to each IAM role to define the resources that anyone allowed to assume the role can access. If an employee changes jobs within your company, you assign them to a different IAM role. People or programs can be assigned to more than one role. However, the `Star` project might require additional resources, such as a new Amazon EC2 container. In that case, you must update the policy attached to the `Star` role to specify the new container resource. Otherwise, `Star` project members aren't allowed to access the new container.

![](https://i.imgur.com/WZ5njzw.png)

##### ABAC Provides the following Advantages over the Traditional RBAC Model:

- **ABAC permissions scale with innovation.** It's no longer necessary for an administrator to update existing policies to allow access to new resources. For example, assume that you designed your ABAC strategy with the `access-project` tag. A developer uses the role with the `access-project` = `Heart` tag. When people on the `Heart` project need additional Amazon EC2 resources, the developer can create new Amazon EC2 instances with the `access-project` = `Heart` tag. Then anyone on the `Heart` project can start and stop those instances because their tag values match.
    
- **ABAC requires fewer policies.** Because you don't have to create different policies for different job functions, you create fewer policies. Those policies are easier to manage.
    
- **Using ABAC, teams can change and grow quickly.** This is because permissions for new resources are automatically granted based on attributes. For example, if your company already supports the `Heart` and `Star` projects using ABAC, it's easy to add a new `Lightning` project. An IAM administrator creates a new role with the `access-project` = `Lightning` tag. It's not necessary to change the policy to support a new project. Anyone that has permissions to assume the role can create and view instances tagged with `access-project` = `Lightning`. Additionally, a team member might move from the `Heart` project to the `Lightning` project. The IAM administrator assigns the user to a different IAM role. It's not necessary to change the permissions policies.
    
- **Granular permissions are possible using ABAC.** When you create policies, it's a best practice to [grant least privilege](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html#grant-least-privilege). Using traditional RBAC, you must write a policy that allows access to only specific resources. However, when you use ABAC, you can allow actions on all resources, but only if the resource tag matches the principal's tag.
    
- **Use employee attributes from your corporate directory with ABAC.** You can configure your SAML-based or web identity provider to pass session tags to AWS. When your employees federate into AWS, their attributes are applied to their resulting principal in AWS. You can then use ABAC to allow or deny permissions based on those attributes.


![[✘Attribute Based Access Contol]]



### AWS Re:Invent 2018 Breakout Sessions | Security, Identity, And Compliance. [Video](https://www.youtube.com/watch?v=vbjFjMNVEpc)
<mark style="background: #ADCCFFA6;">Most Workloads On AWS Resemble A Finely Crafted Cake, With Delight At Every Layer.  
In This Session, We Help You Master Identity At Each Layer Of Deliciousness: From Platform, To Infrastructure, To Applications, Using Services Like AWS Identity And Access Management (IAM), AWS Directory Service, Amazon Cognito, And Many More. Leave With A Firm Mental Model For How Identity Works Both Harmoniously And Independently Throughout These Layers, And With Ready-To-Use Reference Architectures And Sample Code. We Keep Things Fun And Lively Along The Way With Lots Of Demos,</mark>  
![](https://i.imgur.com/7XduDHW.png)


# FAQ
## General

Close all

### What is AWS Identity and Access Management (IAM)?

IAM provides fine-grained access control across all of AWS. With IAM, you can control access to services and resources under specific conditions. Use IAM policies to manage permissions for your workforce and systems to ensure [least privilege](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html#grant-least-privilege). IAM is offered at no additional charge. For more information, see [What is IAM?](https://docs.aws.amazon.com/IAM/latest/UserGuide/introduction.html)

### How Does IAM Work and what Can I Do with It?

IAM provides authentication and authorization for AWS services. A service evaluates if an AWS request is allowed or denied. Access is denied by default and is allowed only when a policy explicitly grants access. You can attach policies to roles and resources to control access across AWS. For more information, see [Understanding how IAM works](https://docs.aws.amazon.com/IAM/latest/UserGuide/intro-structure.html).

### What Are Least-privilege Permissions?

When you set permissions with IAM policies, grant only the permissions required to perform a task. This practice is known as  [granting least privilege.](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html#grant-least-privilege) You can apply least-privilege permissions in IAM by defining the actions that can be taken on specific resources under specific conditions. For more information, see  [Access management for AWS resources](https://docs.aws.amazon.com/IAM/latest/UserGuide/access.html).

### How Do I Get Started with IAM?

To get started using IAM to manage permissions for AWS services and resources, create an IAM role and grant it permissions. For [workforce users](https://aws.amazon.com/single-sign-on/faqs/#General), create a role that can be assumed by your identity provider. For systems, create a role that can be assumed by the service you are using, such as Amazon EC2 or AWS Lambda. After you create a role, you can attach a policy to the role to grant permissions that meet your needs. When you are just starting out, you might not know the specific permissions you need, so you can start with broader permissions. [AWS managed policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_managed-vs-inline.html#aws-managed-policies) provide permissions to help you get started and are available in all AWS accounts. Then, reduce permissions further by defining [customer managed policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_managed-vs-inline.html#customer-managed-policies) specific to your use cases. You can create and manage policies and roles in the IAM console, or via AWS APIs or the AWS CLI. For more information, see [Getting started with IAM](https://docs.aws.amazon.com/IAM/latest/UserGuide/getting-started.html).

## IAM Resources

Close all

### What Are IAM Roles and how Do They Work?

AWS Identity and Access Management (IAM) roles provide a way to access AWS by relying on [temporary security credentials](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_temp.html). Each role has a set of [permissions](https://aws.amazon.com/iam/details/manage-permissions/) for making AWS service requests, and a role is not associated with a specific user or group. Instead, trusted entities such as [identity providers](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_providers.html) or AWS services assume roles. For more information, see [IAM roles](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles.html).

### Why Should I Use IAM Roles?

You should use IAM roles to grant access to your AWS accounts by relying on short-term credentials, a security best practice. Authorized identities, which can be AWS services or users from your identity provider, can assume roles to make AWS requests. To grant permissions to a role, attach an IAM policy to it. For more information, see [Common scenarios for roles](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_common-scenarios.html).

### What Are IAM Users and Should I Still Be Using Them?

IAM users are identities with long-term credentials. You might be using IAM users for [workforce users](https://aws.amazon.com/single-sign-on/faqs/#General). In this case, AWS recommends using an identity provider and federating into AWS by assuming roles. You also can use roles to grant cross-account access to services and features such as AWS Lambda functions. In some scenarios, you might require IAM users with [access keys](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html) that have long-term credentials with access to your AWS account. For these scenarios, AWS recommends using IAM [access last used information](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_finding-unused.html) to rotate credentials often and remove credentials that are not being used. For more information, see [Overview of AWS identity management: Users](https://docs.aws.amazon.com/IAM/latest/UserGuide/introduction_identity-management.html).

### What Are IAM Policies?

IAM [policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies.html) define permissions for the entities you attach them to. For example, to grant access to an IAM role, attach a policy to the role. The permissions defined in the policy determine whether requests are allowed or denied. You also can attach policies to some resources, such as Amazon S3 buckets, to grant direct, cross-account access. And you can attach policies to an AWS organization or organizational unit to restrict access across multiple accounts. AWS evaluates these policies when an IAM role makes a request. For more information, see [Identity-based policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies.html#policies_id-based).

## Granting Access

Close all

### How Do I Grant Access to Services and Resources by Using IAM?

To grant access to services and resources by using AWS Identity and Access Management (IAM), attach IAM policies to roles or resources. You can start by attaching [AWS managed policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_managed-vs-inline.html#aws-managed-policies), which are owned and updated by AWS and are available in all AWS accounts. If you know the specific permissions required for your use cases, you can create [customer managed policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_managed-vs-inline.html#customer-managed-policies) and attach them to roles. Some AWS resources provide a way to grant access by defining a policy attached to resources, such as Amazon S3 buckets. These [resource-based policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_identity-vs-resource.html) allow you to grant direct, cross-account access to the resources they are attached to. For more information, see [Access management for AWS resources](https://docs.aws.amazon.com/IAM/latest/UserGuide/access.html).

### How Do I Create IAM Policies?

To assign permissions to a role or resource, create a policy, which is a [JavaScript Object Notation (JSON)](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_grammar.html) document that defines permissions. This document includes permissions statements that grant or deny access to specific service actions, resources, and conditions. After you create a policy, you can attach it to one or more AWS roles to grant permissions to your AWS account. To grant direct, cross-account access to resources, such as Amazon S3 buckets, use resource-based policies. Create your policies in the IAM console or via AWS APIs or the AWS CLI. For more information, see [Creating IAM policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_create.html).

### What Are AWS Managed Policies and when Should I Use Them?

AWS managed policies are created and administered by AWS and cover common use cases. Getting started, you can grant broader permissions by using the AWS managed policies that are available in your AWS account and common across all AWS accounts. Then, as you refine your requirements, you can reduce permissions by defining customer managed policies specific to your use cases with the goal of achieving least-privilege permissions. For more information, see [AWS managed policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_managed-vs-inline.html#aws-managed-policies).

### What Are Customer Managed Policies and when Should I Use Them?

To grant only the permissions required to perform tasks, you can create customer managed policies that are specific to your use cases and resources. Use customer managed policies to continue refining permissions for your specific requirements. For more information, see [Customer managed policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_managed-vs-inline.html#customer-managed-policies).

### What Are Inline Policies and when Should I Use Them?

Inline policies are embedded in and inherent to specific IAM roles. Use inline policies if you want to maintain a strict one-to-one relationship between a policy and the identity to which it is applied. For example, you can grant administrative permissions to ensure they are not attached to other roles. For more information, see [Inline policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_managed-vs-inline.html#inline-policies).

### What Are Resource-based Policies and when Should I Use Them?

Resource-based policies are permissions policies that are attached to resources. For example, you can attach resource-based policies to Amazon S3 buckets, Amazon SQS queues, VPC endpoints, and AWS Key Management Service encryption keys. For a list of services that support resource-based policies, see [AWS services that work with IAM](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_aws-services-that-work-with-iam.html). Use resource-based policies to grant direct, cross-account access. With resource-based policies, you can define who has access to a resource and which actions they can perform with it. For more information, see [Identity-based policies and resource-based policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_identity-vs-resource.html).

### What is Role-based Access Control (RBAC)?

RBAC provides a way for you to assign permissions based on a person’s job function, known outside of AWS as a role. IAM provides RBAC by defining IAM roles with permissions that align with job functions. You then can grant individuals access to assume these roles to perform specific job functions. With RBAC, you can audit access by looking at each IAM role and its attached permissions. For more information, see [Comparing ABAC to the traditional RBAC model](https://docs.aws.amazon.com/IAM/latest/UserGuide/introduction_attribute-based-access-control.html#introduction_attribute-based-access-control_compare-rbac).

### How Do I Grant Access with RBAC?

As a best practice, grant access only to the specific service actions and resources required to perform each task. This is known as [granting least privilege](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html#grant-least-privilege). When employees add new resources, you must update policies to allow access to those resources.

### What is Attribute-based Access Control (ABAC)?

ABAC is an authorization strategy that defines permissions based on attributes. In AWS, these attributes are called [tags](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_tags.html), and you can define them on AWS resources, IAM roles, and in role sessions. With ABAC, you define a set of permissions based on the value of a tag. You can grant fine-grained permissions to specific resources by requiring the tags on the role or session to match the tags on the resource. For example, you can author a policy that grants developers access to resources tagged with the job title “developers.” ABAC is helpful in environments that are growing rapidly by granting permissions to resources as they are created with specific tags. For more information, see [Attribute-Based Access Control for AWS](https://aws.amazon.com/identity/attribute-based-access-control/).

### How Do I Grant Access by Using ABAC?

To grant access by using ABAC, first define the tag keys and values you want to use for access control. Then, ensure your IAM role has the appropriate tag keys and values. If multiple identities use this role, you also can define session tag keys and values. Next, ensure that your resources have the appropriate tag keys and values. You also can require users to create resources with appropriate tags and restrict access to modify them. After your tags are in place, define a policy that grants access to specific actions and resource types, but only if the role or session tags match the resource tags. For a detailed tutorial that demonstrates how to use ABAC in AWS, see [IAM tutorial: Define permissions to access AWS resources based on tags](https://docs.aws.amazon.com/IAM/latest/UserGuide/tutorial_attribute-based-access-control.html).

## Restricting Access

Close all

### How Do I Restrict Access by Using IAM?

With AWS Identity and Access Management (IAM), all access is denied by default and requires a policy that grants access. As you manage permissions at scale, you might want to implement [permissions guardrails](https://docs.aws.amazon.com/prescriptive-guidance/latest/security-reference-architecture/organizations.html) and restrict access across your accounts. To restrict access, specify a Deny statement in any policy. If a Deny statement applies to an access request, it always prevails over an Allow statement. For example, if you allow access to all actions in AWS but deny access to IAM, any request to IAM is denied. You can include a Deny statement in any type of policy, including identity-based, resource-based, and service control policies with AWS Organizations. For more information, see [Controlling access with AWS Identity and Access Management](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/using-iam-template.html).

### What Are AWS Organizations Service Control Policies (SCPs) and when Should I Use Them?

[SCPs](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_manage_policies_scps.html) are similar to IAM policies and use almost the same syntax. However, SCPs don’t grant permissions. Instead, SCPs allow or deny access to AWS services for individual AWS accounts with Organizations member accounts, or for groups of accounts within an organizational unit. The specified actions from an SCP affect all IAM users and roles, including the root user of the member account. For more information, see [Policy evaluation logic](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_evaluation-logic.html). 

## Analyzing Access

Close all

### How Do I Work toward Least-privilege Permissions?

When you get started granting permissions, you can start with broader permissions as you explore and experiment. As your use cases mature, AWS recommends that you refine permissions to grant only the permissions required with the goal of achieving [least-privilege permissions](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html#grant-least-privilege). AWS provides tools to help you refine your permissions. You can start with [AWS managed policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_managed-vs-inline.html#aws-managed-policies), which are created and administered by AWS and include permissions for common use cases. As you refine your permissions, define specific permissions in [customer managed policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_managed-vs-inline.html#customer-managed-policies). To help you determine the specific permissions you require, use [AWS Identity and Access Management (IAM) Access Analyzer](https://docs.aws.amazon.com/IAM/latest/UserGuide/what-is-access-analyzer.html), review AWS CloudTrail logs, and inspect last access information. You also can use the [IAM policy simulator](https://policysim.aws.amazon.com/) to test and troubleshoot policies.

### What is IAM Access Analyzer?

Achieving least privilege is a continuous cycle to grant the right fine-grained permissions as your requirements evolve. IAM Access Analyzer helps you streamline permissions management in each step of this cycle. [Policy generation](https://aws.amazon.com/blogs/security/iam-access-analyzer-makes-it-easier-to-implement-least-privilege-permissions-by-generating-iam-policies-based-on-access-activity/) with IAM Access Analyzer generates a fine-grained policy based on the access activity captured in your logs. This means that after you build and run an application, you can generate policies that grant only the required permissions to operate the application. [Policy validation](https://aws.amazon.com/blogs/aws/iam-access-analyzer-update-policy-validation/) with IAM Access Analyzer uses more than 100 policy checks to guide you to author and validate secure and functional policies. You can use these checks while creating new policies or to validate existing policies. Custom policy checks are a paid feature to validate that developer-authored policies adhere to your specified security standards ahead of deployments. Custom policy checks use the power of automated reasoning—provable security assurance backed by mathematical proof— to enable security teams to proactively detect nonconformant updates to policies.

[Public and cross-account findings](https://docs.aws.amazon.com/IAM/latest/UserGuide/what-is-access-analyzer.html#what-is-access-analyzer-resource-identification) with IAM Access Analyzer help you verify and refine access allowed by your resource policies from outside your AWS organization or account. For more information, see [Using IAM Access Analyzer](https://docs.aws.amazon.com/IAM/latest/UserGuide/what-is-access-analyzer.html). Unused access with IAM Access Analyzer continuously analyzes your accounts to identify unused access and creates a centralized dashboard with findings. The findings highlight unused roles, unused access keys for IAM users, and unused passwords for IAM users. For active IAM roles and users, the findings provide visibility into unused services and actions.

### How Do I Remove Unused Permissions?

You might have IAM users, roles, and permissions that you no longer require in your AWS account. We recommend that you remove them with the goal of achieving least-privilege access. For IAM users, you can review password and access key last used information. For roles, you can review role last used information. This information is available through the IAM console, APIs, and SDKs. Last used information helps you identify users and roles that are no longer in use and safe to remove. You also can refine permissions by reviewing service and last accessed information to identify unused permissions. For more information, see [Refining permissions in AWS using last accessed information](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_access-advisor.html).

If you enable the unused access analyzer as a paid feature, IAM Access Analyzer continuously analyzes your accounts to identify unused access and creates a centralized dashboard with findings. The dashboard helps security teams review findings centrally and prioritize accounts based on the volume of findings. Security teams can use the dashboard to review findings centrally and prioritize which accounts to review based on the volume of findings. The findings highlight unused roles, unused access keys for IAM users, and unused passwords for IAM users. For active IAM roles and users, the findings provide visibility into unused services and actions. that simplifies inspecting unused access to guide you toward least privilege. With this feature, you pay per IAM role or IAM user analyzed per month.

### What is the IAM Policy Simulator and when Should I Use It?

The [IAM policy simulator](https://policysim.aws.amazon.com/) evaluates policies you choose and determines the effective permissions for each of the actions you specify. Use the policy simulator to test and troubleshoot [identity-based and resource-based policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_identity-vs-resource.html), [IAM permissions boundaries](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_boundaries.html), and [SCPs](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_manage_policies_scps.html). For more information, see [Testing IAM policies with the IAM policy simulator](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_testing-policies.html).

### What Are IAM Access Analyzer Custom Policy Checks?

IAM Access Analyzer custom policy checks validate that IAM policies adhere to your security standards ahead of deployments. Custom policy checks use the power of [automated reasoning](https://www.amazon.science/blog/a-gentle-introduction-to-automated-reasoning)—provable security assurance backed by mathematical proof— to enable security teams to proactively detect nonconformant updates to policies. For example, IAM policy changes that are more permissive than their previous version. Security teams can use these checks to streamline their reviews, automatically approving policies that conform with their security standards, and inspecting more deeply when they don't. This new kind of validation provides higher security assurance in the cloud. Security and development teams can automate policy reviews at scale by integrating these custom policy checks into the tools and environments where developers author their policies, such as their CI/CD pipelines.

### What is IAM Access Analyzer Unused Access?

IAM Access Analyzer simplifies inspecting unused access to guide you toward least privilege. Security teams can use IAM Access Analyzer to gain visibility into unused access across their AWS organization and automate how they rightsize permissions. When the unused access analyzer is enabled, IAM Access Analyzer continuously analyzes your accounts to identify unused access and creates a centralized dashboard with findings. The dashboard helps security teams review findings centrally and prioritize accounts based on the volume of findings. Security teams can use the dashboard to review findings centrally and prioritize which accounts to review based on the volume of findings. The findings highlight unused roles, unused access keys for IAM users, and unused passwords for IAM users. For active IAM roles and users, the findings provide visibility into unused services and actions.