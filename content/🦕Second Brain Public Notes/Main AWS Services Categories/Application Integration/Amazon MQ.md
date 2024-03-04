---
tags:
  - cloud/aws
---
![[Module 12 - Building Decoupled Architectures#Sending Messages between Cloud Applications and On-premises with Amazon MQ]]


![[Pasted image 20240214003553.png]]  
![](https://i.imgur.com/PRiVest.png)


# FAQ
**Q: What is Amazon MQ?**

Amazon MQ is a managed message broker service for [Apache ActiveMQ](http://activemq.apache.org/components/classic/) and [RabbitMQ](https://www.rabbitmq.com/) that makes it easy to set up and operate message brokers in the cloud. You get direct access to the ActiveMQ and RabbitMQ consoles and industry standard APIs and protocols for messaging, including JMS, NMS, AMQP 1.0 and 0.9.1, STOMP, MQTT, and WebSocket. You can easily move from any message broker that uses these standards to Amazon MQ because you don’t have to rewrite any messaging code in your applications.

**Q: Who should use Amazon MQ?**

Amazon MQ is suitable for enterprise IT pros, developers, and architects who are managing a message broker themselves–whether on-premises or in the cloud–and want to move to a fully managed cloud service without rewriting the messaging code in their applications.

**Q: What does Amazon MQ manage on my behalf?**

Amazon MQ manages the work involved in setting up a message broker, from provisioning the infrastructure capacity you request–including broker instances and storage–to installing the broker software. Once your broker is up and running, Amazon manages ongoing software upgrades, security updates, and fault detection and recovery. Amazon MQ stores messages redundantly across multiple Availability Zones (AZs) for message durability. With active/standby brokers, Amazon MQ automatically fails over to a standby instance in the event of a failure so you can continue sending and receiving messages.

**Q: When would I use Amazon MQ vs. managing ActiveMQ, or RabbitMQ, on Amazon EC2 myself?**

The choice depends on how closely you want to manage your message broker and underlying infrastructure. Amazon MQ provides a managed message broker service that takes care of operating your message broker, including set up, monitoring, maintenance, and provisioning the underlying infrastructure for high availability and durability. You may want to consider Amazon MQ when you want to offload operational overhead and associated costs. If you want greater control in order to customize features and configurations or to use custom plugins, you may want to consider installing and running your message broker on Amazon EC2 directly.

**Q: How do I migrate if I'm using a different message broker instead of ActiveMQ or RabbitMQ?**

Amazon MQ provides compatibility with the most common messaging APIs, such as Java Message Service (JMS) and .NET Message Service (NMS), and protocols, including AMQP, STOMP, MQTT, and WebSocket. This makes it easy to switch from any standards-based message broker to Amazon MQ without rewriting the messaging code in your applications. In most cases, you can simply update the endpoints of your Amazon MQ broker to connect to your existing applications, and start sending messages.

**Q: How does Amazon MQ work with other AWS services?**

Any application that runs on an AWS compute service, such as [Amazon EC2](https://aws.amazon.com/ec2/), [Amazon ECS](https://aws.amazon.com/ecs/), or [AWS Lambda](https://aws.amazon.com/lambda/), can use Amazon MQ. Amazon MQ is also integrated with the following AWS services:

- [Amazon CloudWatch](https://aws.amazon.com/cloudwatch/) - monitor metrics and generate alarms
- [Amazon CloudWatch Logs](https://aws.amazon.com/cloudwatch/features/) - publish logs from your Amazon MQ brokers to Amazon CloudWatch Logs
- [AWS CloudTrail](https://aws.amazon.com/cloudtrail/) - log, continuously monitor, and retain Amazon MQ API calls
- [AWS CloudFormation](https://aws.amazon.com/cloudformation/) - automate the process of creating, updating, and deleting message brokers
- [AWS Identity and Access Management (IAM)](https://aws.amazon.com/iam/) - authentication and authorization of the service API
- [AWS Key Management Service (KMS)](https://aws.amazon.com/kms/) - create and control the keys used to encrypt your data

**Q: How can I get started with Amazon MQ?**

Amazon MQ makes it easy to setup and operate message brokers in the cloud. With Amazon MQ, you can use the [AWS Management Console](https://console.aws.amazon.com/amazon-mq/home), CLI, or API calls to launch a production-ready message broker in minutes. In most cases, you can simply update the endpoints of your Amazon MQ broker to connect to your existing applications and start sending messages.

Try a short tutorial, [Create a Connected Message Broker](https://docs.aws.amazon.com/amazon-mq/latest/developer-guide/amazon-mq-getting-started.html), to get started today.

**Q: How am I charged for Amazon MQ?**

With Amazon MQ, you pay only for what you use. You are charged for broker instance and storage usage, and standard data transfer fees. It’s easy to get started with Amazon MQ with our free tier for one year. See [Amazon MQ pricing](https://aws.amazon.com/amazon-mq/pricing/) for details.

**Q: Does Amazon MQ meet compliance standards?**

Yes. Amazon MQ is HIPAA eligible, and meets standards for PCI, SOC, and ISO compliance.

Amazon MQ is HIPAA eligible, which means you can use it to store and transmit messages between healthcare systems, including messages containing protected health information (PHI). Amazon MQ is PCI DSS compliant, which means you can use it to process, store, or transmit payment information. Amazon MQ is also ISO 9001, 27001, 27017, and 27018 certified. These certifications are among the most recognized global security standards attesting to quality and information security management in the cloud, and the protection of personally identifiable information. Amazon MQ is SOC 1, 2, and 3 compliant, allowing you to get deep insight into the security processes and controls that protect customer data.

For a complete list of AWS services and compliance programs, please see [AWS Services in Scope by Compliance Program](https://aws.amazon.com/compliance/services-in-scope/).

**Q: When should I use Amazon MQ vs. Amazon SQS and SNS?**

Amazon MQ, [Amazon SQS](https://aws.amazon.com/sqs/), and [Amazon SNS](https://aws.amazon.com/sns/) are messaging services that are suitable for anyone from startups to enterprises. If you're using messaging with existing applications, and want to move your messaging to the cloud quickly and easily, we recommend you consider Amazon MQ. It supports industry-standard APIs and protocols so you can switch from any standards-based message broker to Amazon MQ without rewriting the messaging code in your applications. If you are building brand new applications in the cloud, we recommend you consider Amazon SQS and Amazon SNS. Amazon SQS and SNS are lightweight, fully managed message queue and topic services that scale almost infinitely and provide simple, easy-to-use APIs. You can use Amazon SQS and SNS to decouple and scale microservices, distributed systems, and serverless applications, and improve reliability.

**Q: When should I use Amazon MQ vs. AWS IoT Message Broker?**

You can use Amazon MQ when you want to offload operational overhead and associated costs with an open source messaging application such as ActiveMQ or any commercial message brokers. You can use Amazon MQ when you are migrating from commercial brokers or open source brokers such as ActiveMQ to reduce broker maintenance, licensing costs and improve broker stability. Amazon MQ is also suitable for Application Integration use cases where you are developing new cloud based applications using micro-services that communicate with complex messaging patterns and require low-latency, high availability and message durability. Amazon MQ supports industry standard APIs such as JMS and NMS, and protocols for messaging, including AMQP, STOMP, MQTT, and WebSocket.

You can use [AWS IoT Message Broker](https://aws.amazon.com/iot-core/features/#Message_Broker) when your use case involves IoT devices’ telemetry, device management, device security and IoT Analysis. AWS IoT Message Broker is suitable for IoT industry customers connecting large device fleets and collecting telemetry data to send it to native AWS services. AWS IoT Message broker supports industry standard lightweight protocols such as MQTT, HTTP and MQTT over WebSocket.

**Q: How do I use my own custom keys to encrypt the data in Amazon MQ?**

Amazon MQ supports the [AWS Key Management Service](https://aws.amazon.com/kms/) (AWS KMS) to create and manage keys for at-rest encryption of your data in Amazon MQ. When you create a broker, you can select the KMS key used to encrypt your data for Amazon MQ for ActiveMQ from the following three options: a KMS key in the Amazon MQ service account, a KMS key in your account that Amazon MQ creates and manages, or a KMS key in your account that you create and manage. For Amazon MQ for RabbitMQ a KMS key in the Amazon MQ service account is used. In addition to encryption at rest, all data transferred between Amazon MQ and client applications is securely transmitted using TLS/SSL.

**Q: How can I monitor my broker instances, queues, and topics?**

Amazon MQ and [Amazon CloudWatch](https://aws.amazon.com/cloudwatch/) are integrated so you can view and analyze metrics for your broker instances, as well as your queues and topics. You can view and analyze metrics from the Amazon MQ console, the CloudWatch console, the command line, or programmatically. Metrics are automatically collected and pushed to CloudWatch every minute.

**Q: Does Amazon MQ have a Service Level Agreement?**

Yes. AWS will use commercially reasonable efforts to make Active/Standby ActiveMQ Brokers, and RabbitMQ Clusters, available with a Monthly Uptime Percentage of at least 99.9% during any monthly billing cycle (the "Service Commitment"). In the event Amazon MQ does not meet the Monthly Uptime Percentage commitment, you will be eligible to receive a Service Credit. For details, please review the full [Amazon MQ Service Level Agreement](https://aws.amazon.com/amazon-mq/sla/).

**Q: What type of storage is available with Amazon MQ for ActiveMQ?**

Amazon MQ for ActiveMQ supports two types of broker storage – durability optimized using [Amazon Elastic File System](https://aws.amazon.com/efs/) (Amazon EFS) and throughput optimized using [Amazon Elastic Block Store](https://aws.amazon.com/ebs/) (EBS). To take advantage of high durability and replication across multiple Availability Zones, use durability optimized brokers backed by Amazon EFS. To take advantage of high throughput for your high volume applications, use throughput optimized brokers backed by EBS. Throughput optimized message brokers reduce the number of brokers required, and cost of operating, high-volume applications using Amazon MQ.

**Q: What plugins are available for Amazon MQ for RabbitMQ?**

Amazon MQ for RabbitMQ includes the management, shovel, federation, and consistent hash exchange plugins on all brokers.  

**Q: What is an Amazon MQ network of brokers?**

Amazon MQ for ActiveMQ uses the “network of brokers” feature that is part of Apache ActiveMQ. A network of brokers consists of multiple brokers connected together. Brokers in the network share information about the clients and destinations each broker hosts. The brokers use this information to route messages through the network. With Amazon MQ, the brokers in the network can either be active-standby brokers (each active broker in the network has a standby node, with shared storage, that will take over if the active node fails), or single-instance brokers (if the node fails, it will be unavailable until it is restarted). Each broker in the network maintains its own unique message store which is replicated across multiple AZs within a region. The nodes in the network forward messages to each other, so messages are stored by a single broker at any given time.

You should use network of brokers if you require high availability with fast reconnection in the case of broker failure, or if you need the ability to scale horizontally.