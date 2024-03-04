---
tags:
  - cloud/aws
---


**Amazon Inspector** is <mark style="background: #BBFABBA6;">an automated security assessment service that helps improve the security and compliance of applications deployed on AWS.</mark>  
![](https://i.imgur.com/UqdBDcR.png)  
![](https://i.imgur.com/lgUguZU.png)

Amazon Inspector automatically assesses applications for exposure, vulnerabilities, and deviations from best practices.

After performing an assessment,<mark style="background: #FFF3A3A6;"> Amazon Inspector produces a detailed list of security findings prioritized by level of severity.</mark>

Amazon Inspector tests the network accessibility of your Amazon EC2 instances and the security state of your applications that run on those instances.

Amazon Inspector security assessments help you check for unintended network accessibility of your Amazon EC2 instances and for vulnerabilities on those EC2 instances.

After performing an assessment, Amazon Inspector produces a detailed list of security findings that is organized by level of severity.

These findings can be reviewed directly or as part of detailed assessment reports which are available via the Amazon Inspector console or API.

With Amazon Inspector, you can automate security vulnerability assessments throughout your development and deployment pipelines or for static production systems.

This allows you to make security testing a regular part of development and IT operations.

## Benefits of Inspector

**Configuration scanning and activity monitoring engine** – Amazon Inspector provides an agent that analyzes system and resource configuration.

**Built-in content library** – Amazon Inspector includes a built-in library of rules and reports.

**Automation through an API** – Amazon Inspector can be fully automated through an API.

## Amazon Inspector Agent

Amazon Inspector also offers predefined software called an agent that you can optionally install in the operating system of the EC2 instances that you want to assess.

The agent monitors the behavior of the EC2 instances, including network, file system, and process activity. It also collects a wide set of behavior and configuration data (telemetry).

## Rules and Packages

You can use Amazon Inspector to assess your assessment targets (collections of AWS resources) for potential security issues and vulnerabilities.

Amazon Inspector compares the behavior and the security configuration of the assessment targets to selected security rules packages.

In the context of Amazon Inspector, a rule is a security check that Amazon Inspector performs during the assessment run.

Amazon Inspector assessments are offered to you as pre-defined rules packages mapped to common security best practices and vulnerability definitions.

Examples of built-in rules include checking for access to your EC2 instances from the internet, remote root login being enabled, or vulnerable software versions installed.

These rules are regularly updated by AWS security researchers.

An Amazon Inspector assessment can use any combination of the following rules packages:

### Network Assessments

**Network Reachability** – The rules in the Network Reachability package analyze your network configurations to find security vulnerabilities of your EC2 instances. The findings that Amazon Inspector generates also provide guidance about restricting access that is not secure.

### Host Assessments

**Common vulnerabilities and exposures** – The rules in this package help verify whether the EC2 instances in your assessment targets are exposed to common vulnerabilities and exposures (CVEs).

**Center for Internet Security (CIS) Benchmarks** – The CIS Security Benchmarks program provides well-defined, unbiased, consensus-based industry best practices to help organizations assess and improve their security.

**Security best practices for Amazon Inspector** – Use Amazon Inspector rules to help determine whether your systems are configured securely.

# FAQ
## General

**Q: What is Amazon Inspector?**

Amazon Inspector is an automated vulnerability management service that continually scans Amazon Elastic Compute Cloud (EC2), AWS Lambda functions, and container images in Amazon ECR and within continuous integration and continuous delivery (CI/CD) tools, in near-real time for software vulnerabilities and unintended network exposure.  

**Q: What are the key benefits of Amazon Inspector?**

Amazon Inspector removes the operational overhead associated with deploying and configuring a vulnerability management solution by allowing you to deploy Amazon Inspector across all accounts with a single step. Additional benefits include:  

- Automated discovery and continual scanning that delivers near real-time vulnerability findings
- Central management, configuration, and view of findings for all your organization’s accounts by setting a Delegated Administrator (DA) account
- A highly contextualized and meaningful Amazon Inspector risk score for each finding to help you set more accurate response priorities
- An intuitive Amazon Inspector dashboard for coverage metrics, including accounts, Amazon EC2 instances, Lambda functions, and container images in Amazon ECR and within CI/CD tools, in near-real time.
- Maximize vulnerability assessment coverage by seamlessly scanning EC2 instances, switching between agent-based and agentless scanning (preview).
- Centrally manage software bill of materials (SBOM) exports for all monitored resources. 
- Integration with AWS Security Hub and Amazon EventBridge to automate workflows and ticket routing

**Q: How do I migrate from Amazon Inspector Classic to the new Amazon Inspector?**

Q: You can deactivate Amazon Inspector Classic by simply deleting all assessment templates in your account. To access findings for existing assessment runs, you can download them as reports or export them using the Amazon Inspector API. You can activate the new Amazon Inspector with a few steps in the AWS Management Console, or by using the new Amazon Inspector APIs. You can find the detailed migration steps in the [Amazon Inspector Classic User Guide](https://docs.aws.amazon.com/inspector/v1/userguide/index.html).  

**Q: How is Amazon Inspector different from Amazon Inspector Classic?**

Amazon Inspector has been rearchitected and rebuilt to create a new vulnerability management service. Here are the key enhancements over Amazon Inspector Classic:  

- **Built for scale**: The new Amazon Inspector is built for scale and the dynamic cloud environment. There’s no limit to the number of instances or images that can be scanned at a time.
- **Support for container images and Lambda functions**: The new Amazon Inspector also scans container images residing in Amazon ECR and within CI/CD tools, and Lambda functions for software vulnerabilities. Container-related findings are also pushed to the Amazon ECR console.
- **Support for multi-account management**: The new Amazon Inspector is integrated with AWS Organizations, allowing you to delegate an administrator account for Amazon Inspector for your organization. This Delegated Administrator (DA) account is a centralized account that consolidates all findings and can configure all member accounts.
- **AWS Systems Manager Agent**: With the new Amazon Inspector, you no longer need to install and maintain a standalone Amazon Inspector agent on all of your Amazon EC2 instances. The new Amazon Inspector uses the widely deployed AWS Systems Manager Agent (SSM Agent), which removes that need.
- **Automated and continual scanning**: The new Amazon Inspector automatically detects all newly launched Amazon EC2 instances, Lambda functions, and eligible container images pushed to Amazon ECR and immediately scans them for software vulnerabilities and unintended network exposure. When an event occurs that may introduce a new vulnerability, the involved resources are automatically rescanned. Events that initiate rescanning a resource include installing a new package in an EC2 instance, installing a patch, and when a new common vulnerabilities and exposures (CVE) that impacts the resource is published.
- **Amazon Inspector risk score**: The new Amazon Inspector calculates an Inspector risk score by correlating up-to-date CVE information with temporal and environmental factors such as network accessibility and exploitability information to add context to help prioritize your findings.  
    
- **Vulnerability assessment coverage**: The new Amazon Inspector enhances vulnerability assessment by seamlessly scanning EC2 instances and switching between agent-based and agentless scanning (preview).
- **Software bill of materials (SBOM) export**: The new Amazon Inspector centrally manages and exports SBOM for all monitored resources. 

**Q: Can I use Amazon Inspector and Amazon Inspector Classic simultaneously in the same account?**

Yes, you can use both simultaneously in the same account.  

**Q: How is the Amazon Inspector container image scanning service for Amazon ECR different than the Amazon ECR Clair-based solution?**  

|   | **Amazon Inspector container image scanning**  | **Amazon ECR Clair-based solution** |
| --- | --- | --- |
|         
**Scanning engine**

 | 

Amazon Inspector is a vulnerability management service developed by AWS that has built-in support for container images residing in Amazon ECR

 | 

Amazon ECR offers a managed [open-source Clair project](https://docs.aws.amazon.com/AmazonECR/latest/userguide/image-scanning.html) as the basic scanning solution

 |  
| 

**Package coverage**

 | 

Identifies vulnerabilities in both operating system (OS) packages and programming language (such as Python, Java, and Ruby) packages

 | 

Identifies software vulnerabilities only in OS packages

 |  
| 

**Scanning frequency**

 | 

Offers both continual scanning and on-push scanning

 | 

Offers only on-push scanning

 |  
| **Vulnerability intelligence** | 

Provides enhanced vulnerability intelligence such as whether an exploit is available for a CVE and fixed in package version remediation guidance

 | 

Provides only basic information about a software vulnerability

 |  
| 

**Findings**

 | 

Findings are available in both the Amazon Inspector and Amazon ECR consoles, as well as the Amazon Inspector and Amazon ECR Application Programming Interface (APIs) and Software Development Kit (SDK)

 | 

Findings are available in the Amazon ECR console and Amazon ECR APIs and SDK

 |  
| 

**Vulnerability scoring**

 | 

Provides a contextual Inspector score and Common Vulnerability Scoring System (CVSS) v2 and v3 scores from both National Vulnerability Database (NVD) and vendors

 | CVSS v2 scores only |  
| 

**AWS service integrations**

 | 

Integrated with AWS Security Hub, AWS Organizations, and AWS EventBridge

 | 

No built-in integrations with other AWS services are available

 |

**Q: What is the pricing for Amazon Inspector?**

See the [Amazon Inspector pricing page](https://aws.amazon.com/inspector/pricing/) for full pricing details.  

**Q: Is there a free trial for Amazon Inspector?**

All accounts new to Amazon Inspector are eligible for a [15-day free trial](https://console.aws.amazon.com/inspector/v2/home) to evaluate the service and estimate its cost. During the trial, all eligible Amazon EC2 instances, AWS Lambda functions, and container images pushed to Amazon ECR are continually scanned at no cost. You can also review estimated spend in the Amazon Inspector console.  

**Q: In what Regions is Amazon Inspector available?**

Amazon Inspector is available globally. Specific availability by Region is [listed here](https://aws.amazon.com/about-aws/global-infrastructure/regional-product-services/).  

## Getting Started

**Q: How do I get started?**

You can activate Amazon Inspector for your entire organization or an individual account with a few steps in the AWS Management Console. Once activated, Amazon Inspector automatically discovers running Amazon EC2 instances, Lambda functions, and Amazon ECR repositories and immediately starts continually scanning workloads for software vulnerabilities and unintended network exposure. If you’re new to Amazon Inspector, there’s a [15-day free trial](https://console.aws.amazon.com/inspector/v2/home) as well.  

**Q: What is an Amazon Inspector finding?**

An Amazon Inspector finding is a potential security vulnerability. For example, when Amazon Inspector detects software vulnerabilities or open network paths to your compute resources, it creates security findings.  

**Q: Can I manage Amazon Inspector using my AWS Organizations structure?**

Yes. Amazon Inspector is integrated with AWS Organizations. You can assign a DA account for Amazon Inspector, which acts as the primary administrator account for Amazon Inspector and can manage and configure it centrally. The DA account can centrally view and manage findings for all the accounts that are part of your AWS organization.  

**Q: How do I delegate an administrator for the Amazon Inspector service?**

The AWS Organizations Management account can assign a DA account for Amazon Inspector in the Amazon Inspector console or by using Amazon Inspector APIs.  

**Q: Do I have to activate specific scanning types (that is, Amazon EC2 scanning, Lambda functions scanning, or Amazon ECR container image scanning)?**  

If you’re starting Amazon Inspector for the first time, all scanning types, including EC2 scanning, Lambda scanning, and ECR container image scanning are activated by default. However, you can deactivate any or all of these across all accounts in your organization. Existing users can activate new features in the Amazon Inspector console or by using Amazon Inspector APIs.  

**Q: Do I need any agents to use Amazon Inspector?**

No, you don’t need an agent for scanning. For vulnerability scanning of Amazon EC2 instances, you can use the AWS Systems Manager Agent (SSM Agent) for an agent-based solution. Amazon Inspector also offers agentless scanning (preview) if you don’t have the SSM Agent deployed or configured. For assessing network reachability of Amazon EC2 instances, vulnerability scanning of container images, or vulnerability scanning of Lambda functions, no agents are necessary.   

**Q: How can I install and configure the Amazon Systems Manager Agent?**

To successfully scan Amazon EC2 instances for software vulnerabilities, Amazon Inspector requires that these instances are managed by [AWS Systems Manager](https://docs.aws.amazon.com/systems-manager/latest/userguide/what-is-systems-manager.html) and the [SSM agent](https://docs.aws.amazon.com/systems-manager/latest/userguide/prereqs-ssm-agent.html). See [Systems Manager prerequisites](https://docs.aws.amazon.com/systems-manager/latest/userguide/systems-manager-prereqs.html) in the AWS Systems Manager User Guide for instructions to activate and configure Systems Manager. For information about managed instances, see the Managed Instances section in the AWS Systems Manager User Guide.  

**Q: How do I know which Amazon ECR repositories are configured for scanning? And how do I manage which repositories should be configured for scanning?**

Amazon Inspector supports the configuration of inclusion rules to select which ECR repositories are scanned. Inclusion rules can be created and managed under the registry settings page within the ECR console or using ECR APIs. The ECR repositories that match the inclusion rules are configured for scanning. Detailed scanning status of repositories is available in both the ECR and Amazon Inspector consoles.  

## Working with Amazon Inspector

**Q: How do I know if my resources are being actively scanned?**

The Environmental Coverage panel in the Amazon Inspector dashboard shows the metrics for accounts, Amazon EC2 instances, Lambda functions, and ECR repositories being actively scanned by Amazon Inspector. Each instance and image have a scanning status: Scanning or Not Scanning. Scanning means the resource is continually being scanned in near real time. A status of Not Scanning could mean the initial scan has not been performed yet, the OS is unsupported, or something else is preventing the scan.  

**Q: How often are the automated rescans performed?**

All scans are automatically performed based on events. All workloads are initially scanned upon discovery and subsequently rescanned.

- For Amazon EC2 instances: For SSM agent-based scans, rescans are started when a new software package is installed or uninstalled on an instance, when a new CVE is published, and after a vulnerable package is updated (to confirm there are no additional vulnerabilities). For agentless scans, scans are performed every 24 hours.
- For Amazon ECR container images: Automated rescans are started for eligible container images when a new CVE affecting an image is published. The automated rescans for container images continue for the duration configured in the Amazon Inspector console or APIs. Available configurations are 30 days (by default), 14 days, 60 days, 90 days, 180 days, or lifetime. This duration is calculated based on last push or pull date of a container image.
- For Lambda functions: All new Lambda functions are initially assessed upon discovery, and continually reassessed when there is an update to the Lambda function or a new CVE is published.

**Q: How long are container images continually rescanned with Amazon Inspector?**

Container images residing in Amazon ECR repositories that are configured for continual scanning are scanned for the duration configured in the Amazon Inspector console or APIs. Available configurations are 30 days (by default), 14 days, 60 days, 90 days, 180 days, or lifetime.

- When Amazon Inspector ECR scanning is activated, Amazon Inspector only picks up images pushed or pulled in last 30 days for scanning, but continually scans them for the duration configured i.e, 30 days (by default), 14 days, 60 days, 90 days, 180 days, or lifetime. The continual rescan duration is calculated based on last push or pull date of a container image. For example, when activating Amazon Inspector ECR scanning, Amazon Inspector will pick up images pushed or pulled in the last 30 days for scanning. However post-activation, if you select 180 days rescan duration, Amazon Inspector will continue to scan the images if they were pushed in the last 180 days or have been pulled at least once in the last 180 days. If an image hasn’t been push or pulled in the last 180 days, Amazon Inspector will stop monitoring it.
- All images pushed to ECR after Amazon Inspector ECR scanning is activated are continually scanned for the configured duration i.e, 30 days (by default), 14 days, 60 days, 90 days, 180 days, or lifetime. The automated rescan duration is calculated based on last push or pull date of a container image. For example, after activating Amazon Inspector ECR scanning, if you select 180 days rescan duration, Amazon Inspector will continue to scan the images if they were pushed in the last 180 days or have been pulled at least once in the last 180 days. However, if an image hasn’t been pushed or pulled in the last 180 days, Amazon Inspector will stop monitoring it.
- If the image is in “scan eligibility expired” state, you can pull the image to bring it back under Amazon Inspector monitoring. The image will be continually scanned for the rescan duration configured from the last pulled date.

**Q: Can I exclude my resources from being scanned?**

- **For Amazon EC2 instances**: Yes, an EC2 instance can be excluded from scanning by adding a resource tag. You can use the key ‘InspectorEc2Exclusion’, and value is `<optional>`.
- **For container images residing in Amazon ECR**: Yes. Although you can select which Amazon ECR repositories are configured for scanning, all images within a repository will be scanned. You can create inclusion rules to select which repositories should be scanned.  
    
- **For Lambda functions:** Yes, a Lambda function can be excluded from scanning by adding a resource tag. For standard scanning, use the key 'InspectorExclusion' and the value 'LambdaStandardScanning'. For code scanning, use the key 'InspectorCodeExclusion' and the value 'LambdaCodeScanning'.  
    

**Q: How do I use Amazon Inspector to assess my Lambda functions for security vulnerabilities?**  

In a multi-account structure, you can activate Amazon Inspector for Lambda vulnerabilities assessments for all your accounts within the AWS Organization from the Amazon Inspector console or APIs through the Delegated Administrator (DA) account, while other member accounts can activate Amazon Inspector for their own account if the central security team hasn’t already activated it for them. Accounts that are not a part of the AWS Organization can activate Amazon Inspector for their individual account through the Amazon Inspector console or APIs.  

**Q: If a Lambda function has multiple versions, which version will Amazon Inspector assess?**  

Amazon Inspector will continually monitor and assess only the $LATEST version. Automated rescans will continue only for the latest version, so new findings will be generated only for the latest version. In the console, you will be able to see the findings from any version by selecting the version from the dropdown.  

**Q: Can I activate Lambda code scanning without activating Lambda standard scanning?**

No. You have two options: either activate Lambda standard scanning alone or enable Lambda standard and code scanning together. Lambda standard scanning provides fundamental security protection against vulnerable dependencies used in the application deployed as Lambda functions and association layers. Lambda code scanning provides additional security value by scanning your custom proprietary application code within a Lambda function for code security vulnerabilities such as injection flaws, data leaks, weak cryptography, or embedded secrets.

**Q: How does changing the SSM inventory collection frequency from the default 30 minutes to 12 hours impact the continual scanning by Amazon Inspector?**

Changing the default SSM inventory collection frequency can have an impact on the continual nature of scanning. Amazon Inspector relies on SSM Agent to collect the application inventory to generate findings. If the application inventory duration is increased from the default of 30 minutes, that will delay the detection of changes to the application inventory, and new findings might be delayed.  

**Q: What is Amazon Inspector risk score?**

The Amazon Inspector risk score is a highly contextualized score that is generated for each finding by correlating common vulnerabilities and exposures (CVE) information with network reachability results, exploitability data, and social media trends. This makes it easier for you to prioritize findings and focus on the most critical findings and vulnerable resources. You can see how the Inspector risk score was calculated and which factors influenced the score in the Inspector Score tab within the Findings Details side panel.

For example: There is a new CVE identified on your Amazon EC2 instance, which can only be exploited remotely. If the Amazon Inspector continual network reachability scans also discover that the instance is not reachable from the internet, it knows that the vulnerability is less likely to be exploited. Therefore, Amazon Inspector correlates the scan results with the CVE to adjust the risk score downward, more accurately reflecting the impact of the CVE on that particular instance.  

**Q: How is a finding severity determined?**  

| **Amazon Inspector Score**  | **Severity**  |
| --- | --- |
| 0 | Informational |
| 0.2–3.9 | Low |
| 4.0–6.9 | Medium |
| 7.0–8.9 | High |
| 9.0–10.0 | Critical |

**Q: How do suppression rules work?**

Amazon Inspector allows you to suppress findings based on the customized criteria you define. You can create suppression rules for findings that are considered acceptable by your organization.  

**Q: How can I export my findings, and what do they include?**  

You can generate reports in multiple formats (CSV or JSON) with a few steps in the Amazon Inspector console or through the Amazon Inspector APIs. You can download a full report with all findings, or generate and download a customized report based on the view filters set in the console.

**Q: Can I activate Lambda code scanning without activating Lambda standard scanning?**

No. You have two options: either activate Lambda standard scanning alone or enable Lambda standard and code scanning together. Lambda standard scanning provides fundamental security protection against vulnerable dependencies used in the application deployed as Lambda functions and association layers. Lambda code scanning provides additional security value by scanning your custom proprietary application code within a Lambda function for code security vulnerabilities such as injection flaws, data leaks, weak cryptography, or embedded secrets.  

**Q: How can I export SBOM for my resources, and what do they include?**

You can generate and export SBOMs for all resources monitored with Amazon Inspector, in multiple formats (CycloneDx or SPDX), with a few steps in the Amazon Inspector console or through the Amazon Inspector APIs. You can download a full report with SBOM for all resources, or selectively generate and download SBOMs for a few select resources based on the set view filters.

**Q: How do I enable agentless scanning for my account?** 

For existing Amazon Inspector customers using a single account, you can enable agentless scanning (preview) by visiting the account management page within the Amazon Inspector console or using APIs.

For existing Amazon Inspector customers using AWS Organizations, your Delegated Admin needs to either completely migrate the entire organization to an agentless solution or continue using the SSM agent-based solution exclusively. You can change the scan mode  configuration from the EC2 settings page in the console or through APIs.

For new Amazon Inspector customers, during the agentless scanning preview period, instances are scanned in agent-based scan mode when you enable EC2 scanning. You can switch to hybrid scan mode if needed. In the hybrid scan mode, Amazon Inspector relies on SSM Agents for application inventory collection to perform vulnerability assessments and automatically falls back on agentless scanning for instances that don’t have SSM Agents installed or configured.  

**Q: What is the frequency for agentless scans?**

Amazon Inspector will automatically trigger a scan every 24 hours for instances that are marked for agentless scanning (preview). There will be no change to the continuous scanning behavior for instances marked for SSM agent-based scans.   

**Q: Where can I see which instances are being scanned using agent vs agentless when I’m using hybrid scan mode for EC2 scanning?**

You can see the scanning mode in the ‘monitored using’ column by simply visiting the resource coverage pages in the Amazon Inspector console or by using Amazon Inspector coverage APIs.   

**Q: Is it possible for member accounts in a multi-account setup to modify the scan mode for EC2 scanning for their respective accounts?** 

No, in a multi-account setup, only delegated admins can set up scan mode configuration for the complete organization.  

**Q: How do I integrate Amazon Inspector in my CI/CD tools for container image scanning?**  

Application and platform teams can integrate Amazon Inspector into their build pipelines using purpose-built Amazon Inspector plugins designed for various CI/CD tools, such as Jenkins and TeamCity. These plugins are available in the marketplace of each respective CI/CD tool. Once the plugin is installed, you can add a step in the pipeline to perform an assessment of the container image and take actions, such as blocking the pipeline based on the assessment results. When vulnerabilities are identified in the assessment, actionable security findings are generated. These findings include vulnerability details, remediation recommendations, and exploitability details. They are returned to the CI/CD tool in both JSON and CSV formats, which can then be translated into a human-readable dashboard by the Amazon Inspector plugin or can be downloaded by teams.  

**Q: Do I need to enable Amazon Inspector to use Amazon Inspector CI/CD integration for container image scanning?**  
  
No, you don’t need to enable Amazon Inspector to use this feature provided you have an active AWS account.  
  

**Q: Can I scan my private Amazon EC2 instances by setting up Amazon Inspector as a VPC endpoint?**

Yes. Amazon Inspector uses SSM Agent to collect application inventory, which can be set up as [Amazon Virtual Private Cloud (VPC) endpoints](https://docs.aws.amazon.com/systems-manager/latest/userguide/setup-create-vpc.html) to avoid sending information over the internet.  

**Q: Which operating systems does Amazon Inspector support?**

You can find the list of operating systems (OS) supported [here](https://docs.aws.amazon.com/inspector/latest/user/supported.html).  

**Q: Which programming language packages does Amazon Inspector support for container image scanning?**

You can find the list of programming language packages supported [here](https://docs.aws.amazon.com/inspector/latest/user/supported.html).  
  

**Q: Will Amazon Inspector work with instances that use Network Address Translation (NAT)?**

Yes. Instances that use NAT are automatically supported by Amazon Inspector.  

**Q: I use a proxy for my instances. Will Amazon Inspector work with these instances?**

Yes. See [how to configure SSM Agent to use a proxy](https://docs.aws.amazon.com/systems-manager/latest/userguide/sysman-proxy-with-ssm-agent.html) for more information.  

**Q: Can Amazon Inspector be integrated with other AWS services for logging and notifications?**

Amazon Inspector integrates with Amazon EventBridge to provide notification for events such as a new finding, change of state of a finding, or creation of a suppression rule. Amazon Inspector also integrates with [AWS CloudTrail](https://aws.amazon.com/cloudtrail/) for call logging.  

**Q: Does Amazon Inspector offer “CIS Operating System Security Configuration Benchmarks” scans?**

No. While Amazon Inspector does not currently support CIS scans, this capability will be added in the future. However, you can continue to use the CIS scan rules package offered in Amazon Inspector Classic.  

**Q: Does Amazon Inspector work with AWS Partner solutions?**

Yes. See [Amazon Inspector Partners](https://aws.amazon.com/inspector/partners/) for more information.  

**Q: Can I deactivate Amazon Inspector?**

Yes. You can deactivate all scanning types (Amazon EC2 scanning, Amazon ECR container image scanning, and Lambda function scanning) by deactivating the Amazon Inspector service, or you can deactivate each scanning type individually for an account.  

**Q: Can I suspend Amazon Inspector?**

No. Amazon Inspector does not support a suspended state.
