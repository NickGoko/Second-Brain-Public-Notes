---
tags:
  - cloud/aws
---
The AWS shared responsibility model defines what you (as an AWS account holder/user) and AWS are responsible for when it comes to security and compliance.

Security and Compliance is a shared responsibility between AWS and the customer. This shared model can help relieve customer’s operational burdens as AWS operates, manages, and controls the components from the host operating system and virtualization layer down to the physical security of the facilities in which the service operates.

The customer assumes responsibility and management of the guest operating system (including updates and security patches), other associated application software as well as the configuration of the AWS provided security group firewall.

AWS are responsible for “Security **of** the Cloud” .

- AWS is responsible for protecting the infrastructure that runs all the services offered in the AWS Cloud.
- This infrastructure is composed of the hardware, software, networking, and facilities that run AWS Cloud services.

Customers are responsible for “Security **in** the Cloud”.

- For EC2 this includes network level security (NACLs, security groups), operating system patches and updates, IAM user access management, and client and server-side data encryption.

The following diagram shows the split of responsibilities between AWS and the customer:

![AWS Shared Responsibility Model](https://digitalcloud.training/wp-content/uploads/2022/02/aws-shared-responsibility-model.jpeg)

Inherited Controls – Controls which a customer fully inherits from AWS.

- Physical and Environmental controls.

Shared Controls – Controls which apply to both the infrastructure layer and customer layers, but in separate contexts or perspectives.

In the AWS shared security model, a shared control, AWS provides the requirements for the infrastructure and the customer must provide their own control implementation within their use of AWS services.

Examples  of shared controls include:

- **Patch Management** – AWS is responsible for patching and fixing flaws within the infrastructure, but customers are responsible for patching their guest OS and applications.
- **Configuration Management** – AWS maintains the configuration of its infrastructure devices, but a customer is responsible for configuring their own guest operating systems, databases, and applications.
- **Awareness & Training** – AWS trains AWS employees, but a customer must train their own employees.

Customer Specific – Controls which are solely the responsibility of the customer based on the application they are deploying within AWS services. .

Examples of customer specific controls include:

- Service and Communications Protection or Zone Security which may require a customer to route or zone data within specific security environments.