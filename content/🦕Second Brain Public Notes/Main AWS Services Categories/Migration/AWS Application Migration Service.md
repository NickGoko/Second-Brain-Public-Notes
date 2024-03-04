---
tags:
  - cloud/aws
---


# FAQ
**Q: What is AWS Application Migration Service?  
**[AWS Application Migration Service](https://aws.amazon.com/application-migration-service/) (AWS MGN) is the recommended service for migrations to AWS. AWS Application Migration Service simplifies and expedites your migration to AWS by automatically converting your source servers from physical, virtual, or cloud infrastructure to run natively on AWS. It further simplifies your migration and reduces costs by allowing you to use the same automated process for a wide range of applications, without changes to applications, their architecture, or the migrated servers. You can use AWS Application Migration Service to perform non-disruptive tests prior to cutover. After testing, you can use AWS Application Migration Service to quickly migrate your applications to the cloud during a short cutover window, typically measured in minutes. You can also use AWS Application Migration Service to automate application modernizations on your migrated servers.

**Q: How do I get started with AWS Application Migration Service?  
**To start using AWS Application Migration Service, simply [click here](https://console.aws.amazon.com/mgn/home) or sign into the AWS Management Console and navigate to “AWS Application Migration Service” in the “Migration & Transfer” category. You can follow the steps provided in the console to set up and operate AWS Application Migration Service, or refer to the [Quick Start Guide](https://docs.aws.amazon.com/mgn/latest/ug/quick-start-guide-gs.html).

The [AWS Application Migration Service (AWS MGN) – A Technical Introduction](https://www.aws.training/Details/eLearning?id=71732) training is recommended if you want to learn more about how to use the service, or if you are assisting customers with a migration using AWS Application Migration Service. This free online training is offered by AWS Training and Certification, and covers key concepts, service architecture, and implementation approaches for AWS Application Migration Service.

**Q: What source infrastructure does AWS Application Migration Service support?  
**You can use AWS Application Migration Service to migrate your applications to AWS from physical servers, VMware vSphere, Microsoft Hyper-V, and other cloud providers. You can also use AWS Application Migration Service to migrate Amazon EC2 instances between AWS Regions or between AWS accounts, and to [migrate from EC2-Classic to a VPC](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/vpc-migrate.html).

**Q: What operating systems and applications are supported by AWS Application Migration Service?  
**AWS Application Migration Service allows you to migrate physical, virtual, and cloud source servers to AWS for a variety of [supported operating systems](https://docs.aws.amazon.com/mgn/latest/ug/Supported-Operating-Systems.html) (OS). AWS Application Migration Service supports commonly used applications such as SAP, Oracle, and Microsoft SQL Server.

**Q: Does AWS Application Migration Service support agentless replication?**  
Yes. AWS Application Migration Service supports agentless replication from VMware vCenter versions 6.7 and 7.0 to AWS. You can perform agentless snapshot replication from your vCenter source environment to AWS by installing the AWS MGN vCenter Client in your vCenter environment. This option is intended for users who want to rehost their applications to AWS but cannot install agents due to company policies or technical restrictions. When possible, we recommend using the agent-based replication option as it provides continuous data replication and shortens cutover windows.

**Q: How can I receive product support for AWS Application Migration Service?**  
Contact [AWS Premium Support](https://aws.amazon.com/premiumsupport/) to receive product support for AWS Application Migration Service according to your support plan.

**Q: What does “AWS MGN” stand for?  
**The shortened service name for AWS Application Migration Service is AWS MGN. “MGN” is an abbreviation of the word “migration.”