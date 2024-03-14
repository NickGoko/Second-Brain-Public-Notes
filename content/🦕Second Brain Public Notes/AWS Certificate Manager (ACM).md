---
tags:
  - cloud/aws
---

![](https://i.imgur.com/OLOaswk.png)  
![](https://i.imgur.com/nZLXV5C.png)  
![](https://i.imgur.com/yH4jewm.png)  
![](https://i.imgur.com/ENKiFdu.png)  
![](https://i.imgur.com/sYs0oDz.png)

# FAQ
### General

**Q: What is AWS Certificate Manager?**

AWS Certificate Manager (ACM) is <mark style="background: #FFB86CA6;">a service that lets you easily provision, manage, and deploy public and private Secure Sockets Layer/Transport Layer Security (SSL/TLS) certificates for use with AWS services and your internal connected resources</mark>.  
SSL/TLS certificates are used to secure network communications and establish the identity of websites over the Internet as well as resources on private networks. ACM removes the time-consuming manual process of purchasing, uploading, and renewing SSL/TLS certificates. With AWS Certificate Manager, you can quickly request a certificate, deploy it on AWS resources such as Elastic Load Balancers, Amazon CloudFront distributions, and APIs on API Gateway, and let ACM handle certificate renewals. It also enables you to create private certificates for your internal resources and manage the certificate lifecycle centrally. Public and private SSL/TLS certificates provisioned through ACM and used exclusively with ACM-integrated services, such as Elastic Load Balancing, Amazon CloudFront, and Amazon API Gateway, are free. You pay for the AWS resources you create to run your application. You pay a monthly fee for the operation of each private CA until you delete it, and for the private certificates you issue that are not used exclusively with [ACM-integrated services](https://docs.aws.amazon.com/acm/latest/userguide/acm-services.html).

**Q: What is an SSL/TLS certificate?**

SSL/TLS certificates allow web browsers to identify and establish encrypted network connections to web sites using the Secure Sockets Layer/Transport Layer Security (SSL/TLS) protocol. Certificates are used within a cryptographic system known as a public key infrastructure (PKI). PKI provides a way for one party to establish the identity of another party using certificates if they both trust a third-party - known as a certificate authority. You can visit the [Concepts](https://docs.aws.amazon.com/acm/latest/userguide/acm-concepts.html) topic in the ACM User Guide for additional information and definitions.

**Q: What are private certificates?**

Private certificates identify resources within an organization, such as applications, services, devices, and users. In establishing a secure encrypted communications channel, each endpoint uses a certificate and cryptographic techniques to prove its identity to the other endpoint. Internal API endpoints, web servers, VPN users, IoT devices, and many other applications use private certificates to establish encrypted communication channels that are necessary for their secure operation.

**Q: What is the difference between public and private certificates?**

Both public and private certificates help customers identify resources on networks and secure communication between these resources. Public certificates identify resources on the public Internet, whereas private certificates do the same for private networks. One key difference is that applications and browsers trust public certificates automatically by default, whereas an administrator must explicitly configure applications to trust private certificates. Public CAs, the entities that issue public certificates, must follow strict rules, provide operational visibility, and meet security standards imposed by the browser and operating system vendors that decide which CAs their browsers and operating systems trust automatically. Private CAs are managed by private organizations, and private CA administrators can make their own rules for issuing private certificates, including practices for issuing certificates and what information a certificate can include. 

**Q: What are the benefits of using AWS Certificate Manager (ACM)?**

ACM makes it easier to enable SSL/TLS for a website or application on the AWS platform. ACM eliminates many of the manual processes previously associated with using and managing SSL/TLS certificates. ACM can also help you avoid downtime due to misconfigured, revoked, or expired certificates by managing renewals. You get SSL/TLS protection and easy certificate management. Enabling SSL/TLS for Internet-facing sites can help improve the search rankings for your site and help you meet regulatory compliance requirements for encrypting data in transit.

When you use ACM to manage certificates, certificate private keys are securely protected and stored using strong encryption and key management best practices. ACM lets you use the AWS Management Console, AWS CLI, or ACM APIs to centrally manage all of the SSL/TLS ACM certificates in an AWS Region. ACM is integrated with other AWS services, so you can request an SSL/TLS certificate and provision it with your Elastic Load Balancing load balancer or Amazon CloudFront distribution from the AWS Management Console, through AWS CLI commands, or with API calls.

**Q: What types of certificates can I manage with ACM?**  

ACM enables you to manage the lifecycle of your public and private certificates. ACM’s capabilities depend on whether the certificate is public or private, how you obtain the certificate, and where you deploy it.  

<u>Public certificates</u> - You can request Amazon-issued public certificates in ACM. ACM manages the renewal and deployment of public certificates used with ACM-integrated services, including Amazon CloudFront, Elastic Load Balancing, and Amazon API Gateway.

<u>Private certificates</u> – You can choose to delegate private certificate management to ACM. When used in this way, ACM can automatically renew and deploy private certificates used with ACM-integrated services, including Amazon CloudFront, Elastic Load Balancing, and Amazon API Gateway. You can easily deploy these private certificates using the AWS Management console, APIs, and command-line interface (CLI). You can export private certificates from ACM and use them with EC2 instances, containers, on-premises servers, and IoT devices. AWS Private CA automatically renews these certificates and sends an Amazon CloudWatch notification when the renewal is completed. You can write client-side code to download renewed certificates and private keys and deploy them with your application.  

<u>Imported certificates</u> – If you want to use a third-party certificate with Amazon CloudFront, Elastic Load Balancing, or Amazon API Gateway, you may import it into ACM using the AWS Management Console, AWS CLI, or ACM APIs. ACM can not renew imported certificates, but it can help you manage the renewal process. You are responsible for monitoring the expiration date of your imported certificates and for renewing them before they expire. You can use [ACM CloudWatch metrics](https://docs.amazonaws.cn/en_us/acm/latest/userguide/cloudwatch-metrics.html) to monitor the expiration dates of an imported certificates and import a new third-party certificate to replace an expiring one.  

**Q: How can I get started with ACM?**  

To get started with ACM, navigate to Certificate Manager in the AWS Management Console and use the wizard to request an SSL/TLS certificate. If you have already created a Private CA, you can choose whether you want a public or private certificate, and then enter the name of your site. You can also request a certificate using the AWS CLI or API. After the certificate is issued, you can use it with other AWS services that are integrated with ACM. For each integrated service, you simply select the SSL/TLS certificate you want from a drop-down list in the AWS Management Console. Alternatively, you can execute an AWS CLI command or call an AWS API to associate the certificate with your resource. The integrated service then deploys the certificate to the resource you selected.  For more information about requesting and using certificates provided by ACM, learn more in the [ACM User Guide](https://aws.amazon.com/certificate-manager/getting-started/). In addition to using private certificates with ACM-integrated services, you can also export private certificates for use on EC2 instances, on ECS containers, or anywhere.  

**Q: With which AWS services can I use ACM certificates?**

• You can use public and private ACM certificates with the following AWS services:  
• Elastic Load Balancing – Refer to the [Elastic Load Balancing documentation](https://aws.amazon.com/documentation/elastic-load-balancing/)  
• Amazon CloudFront – Refer to the [CloudFront documentation](https://aws.amazon.com/documentation/cloudfront/)  
• Amazon API Gateway – Refer to the [API Gateway documentation](https://aws.amazon.com/documentation/apigateway/)  
• AWS CloudFormation – Support is currently limited to ACM-issued public and private certificates. Refer to the [AWS CloudFormation documentation](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-certificatemanager-certificate.html)  
• AWS Elastic Beanstalk – Refer to the [AWS Elastic Beanstalk documentation](https://aws.amazon.com/documentation/elastic-beanstalk/)  
• AWS Nitro Enclaves – Refer to the [AWS Nitro Enclaves documentation](https://docs.aws.amazon.com/enclaves/latest/user/nitro-enclave-refapp.html)  

**Q: In what Regions is ACM available?**  

Please visit the [AWS Global Infrastructure](https://aws.amazon.com/about-aws/global-infrastructure/regional-product-services/) pages to see the current Region availability for AWS services. To use an ACM certificate with Amazon CloudFront, you must request or import the certificate in the US East (N. Virginia) region. ACM certificates in this region that are associated with a CloudFront distribution are distributed to all the geographic locations configured for that distribution.

### ACM Certificates

**Q: What types of certificates does ACM manage?**

ACM manages public, private, and imported certificates. Learn more about ACM's capabilities in the [Issuing and Managing Certificates](https://docs.aws.amazon.com/acm/latest/userguide/gs.html) documentation.  

**Q: Can ACM provide certificates with multiple domain names?**

Yes. Each certificate must include at least one domain name, and you can add additional names to the certificate if you want to. For example, you can add the name “www.example.net” to a certificate for “www.example.com” if users can reach your site by either name. You must own or control all of the names included in your certificate request. 

**Q: What is a wildcard domain name?**

A wildcard domain name matches any first level subdomain or hostname in a domain. A first-level subdomain is a single domain name label that does not contain a period (dot). For example, you can use the name \*.example.com to protect www.example.com, images.example.com, and any other host name or first-level subdomain that ends with .example.com. Learn more in the [ACM User Guide](https://docs.aws.amazon.com/acm/latest/userguide/acm-overview.html).

**Q: Can ACM provide certificates with wildcard domain names?**

Yes.

**Q: Does ACM provide certificates outside of SSL/TLS?**

No.

**Q: Can I use ACM certificates for code signing or email encryption?**

No.

**Q: Does ACM provide certificates used to sign and encrypt email (S/MIME certificates)?**

No.

**Q: What is the validity period for ACM certificates?**

Certificates issued through ACM are valid for 13 months (395 days). If you issue private certificates directly from a private CA and manage the keys and certificates without using ACM for certificate management, you can choose any validity period, including an absolute end date or a relative time that is days, months, or years from the present time.

**Q: What algorithms do ACM-issued certificates use?**

By default, certificates issued in ACM use RSA keys with a 2048-bit modulus and SHA-256. Additionally, you can request Elliptic Curve Digital Signature Algorithm (ECDSA) certificates with either P-256 or P-384. Learn more about algorithms in the [ACM User Guide](https://docs.aws.amazon.com/acm/latest/userguide/acm-certificate.html#algorithms).  

**Q: How do I revoke a certificate?**

You can request ACM to revoke a public certificate by visiting the [AWS Support Center](http://aws.amazon.com/support) and creating a case. To revoke a private certificate issued by your AWS Private CA, refer to the [AWS Private CA User Guide](https://docs.aws.amazon.com/acm-pca/latest/userguide/PcaWelcome.html). 

**Q: Can I use the same ACM certificate in more than one AWS Region?**  

No. ACM certificates must be in the same Region as the resource where they are being used. The only exception is Amazon CloudFront, a global service that requires certificates in the US East (N. Virginia) region. ACM certificates in this region that are associated with a CloudFront distribution are distributed to all the geographic locations configured for that distribution.

**Q: Can I provision a certificate with ACM if I already have a certificate from another provider for the same domain name?**

Yes.

**Q: Can I use certificates on Amazon EC2 instances or on my own servers?**

You can use private certificates issued with Private CA with EC2 instances, containers, and on your own servers. At this time, public ACM certificates can be used only with specific AWS services, including AWS Nitro Enclaves. See [ACM service integrations.  
](https://docs.aws.amazon.com/acm/latest/userguide/acm-services.html)

**Q: Does ACM allow local language characters in domain names, otherwise known as Internationalized Domain Names (IDNs)?**

ACM does not allow Unicode encoded local language characters; however, ACM allows ASCII-encoded local language characters for domain names.

**Q: Which domain name label formats does ACM allow?**

ACM allows only UTF-8 encoded ASCII, including labels containing “xn—”, commonly known as Punycode for domain names. ACM does not accept Unicode input (u-labels) for domain names.

**Q: Can I import a third-party certificate and use it with AWS services?**

Yes. If you want to use a third-party certificate with Amazon CloudFront, Elastic Load Balancing, or Amazon API Gateway, you may import it into ACM using the AWS Management Console, AWS CLI, or ACM APIs. ACM does not manage the renewal process for imported certificates. You can use the AWS Management Console to monitor the expiration dates of an imported certificates and import a new third-party certificate to replace an expiring one.

### ACM Public Certificates

**Q: What are public certificates?**

Both public and private certificates help customers identify resources on networks and secure communication between these resources. Public certificates identify resources on the Internet.

**Q: What type of public certificates does ACM provide?**

ACM provides Domain Validated (DV) public certificates for use with websites and applications that terminate SSL/TLS. For more details about ACM certificates, see [Certificate Characteristics](http://docs.aws.amazon.com/acm/latest/userguide/acm-certificate.html).

**Q: Are ACM public certificates trusted by browsers, operating systems, and mobile devices?**

ACM public certificates are trusted by most modern browsers, operating systems, and mobile devices. ACM-provided certificates have 99% browser and operating system ubiquity, including Windows XP SP3 and Java 6 and later.

**Q: How can I confirm that my browser trusts ACM public certificates?**

Some browsers that trust ACM certificates display a lock icon and do not issue certificate warnings when connected to sites that use ACM certificates over SSL/TLS, for example using HTTPS.

Public ACM certificates are verified by Amazon’s certificate authority (CA). Any browser, application, or OS that includes the Amazon Root CA 1, Amazon Root CA 2, Amazon Root CA 3, Amazon Root CA 4, Starfield Services Root Certificate Authority - G2 trusts ACM certificates. For more information about root CAs, visit the [Amazon Trust Services Repository](https://www.amazontrust.com/repository/).  

**Q: Does ACM provide public Organizational Validation (OV) or Extended Validation (EV) certificates?**

No.

**Q: Where does Amazon describe its policies and practices for issuing public certificates?**

They are described in the Amazon Trust Services Certificate Policies and Amazon Trust Services Certification Practices Statement documents. Refer to the [Amazon Trust Services repository](https://www.amazontrust.com/repository/) for the latest versions.

**Q: Will a certificate for www.example.com also work for example.com?**

No. If you want your site to be referenced by both domain names (www.example.com and example.com), you must request a certificate that includes both names.

**Q: How can ACM help my organization meet my compliance requirements?**

Using ACM helps you comply with regulatory requirements by making it easy to facilitate secure connections, a common requirement across many compliance programs such as PCI, FedRAMP, and HIPAA. For specific information about compliance, please refer to http://aws.amazon.com/compliance.

**Q: Does ACM have a service level agreement (SLA)?**

No, ACM does not have an SLA. 

**Q: Does ACM provide a secure site seal or trust logo that I can display on my web site?**

No. If you would like to use a site seal, you can obtain one from a third-party vendor. We recommend choosing a vendor that evaluates and asserts the security of your site, or your business practices, or both.

**Q: Does Amazon allow its trademarks or logo to be used as a certificate badge, site seal, or trust logo?**

No. Seals and badges of this type can be copied to sites that do not use the ACM service, and used inappropriately to establish trust under false pretenses. To protect our customers and the reputation of Amazon, we do not allow our logo to be used in this manner.

### Provision Public Certificates

**Q: How can I provision a public certificate from ACM?**

You can use the AWS Management Console, AWS CLI, or ACM APIs/SDKs. To use the AWS Management Console, navigate to the Certificate Manager, choose Request a certificate, select Request a public certificate, enter the domain name for your site, and follow the instructions on the screen to complete your request. You can add additional domain names to your request if users can reach your site by other names. Before ACM can issue a certificate, it validates that you own or control the domain names in your certificate request. You can choose DNS validation or email validation when requesting a certificate. With DNS validation, you write a record to the public DNS configuration for your domain to establish that you own or control the domain. After you use DNS validation once to establish control of your domain, you can obtain additional certificates and have ACM renew existing certificates for the domain as long as the record remains in place and the certificate remains in use. You do not have to validate control of the domain again. If you choose email validation instead of DNS validation, emails are sent to the domain owner requesting approval to issue the certificate. After validating that you own or control each domain name in your request, the certificate is issued and ready to be provisioned with other AWS services, such as Elastic Load Balancing or Amazon CloudFront. Refer to the [ACM Documentation](https://docs.aws.amazon.com/acm/latest/userguide/acm-overview.html) for details.  

**Q: Why does ACM validate domain ownership for public certificates?**

Certificates are used to establish the identity of your site and secure connections between browsers and applications and your site. To issue a publicly trusted certificate, Amazon must validate that the certificate requester has control over the domain name in the certificate request.

**Q: How does ACM validate domain ownership before issuing a public certificate for a domain?**

Prior to issuing a certificate, ACM validates that you own or control the domain names in your certificate request. You can choose DNS validation or email validation when requesting a certificate. With DNS validation, you can validate domain ownership by adding a CNAME record to your DNS configuration. Refer to [DNS validation](https://aws.amazon.com/certificate-manager/faqs//#DNS_Validation_.28Public_Certificates.29) for further details. If you do not have the ability to write records to the public DNS configuration for your domain, you can use email validation instead of DNS validation. With email validation, ACM sends emails to the registered domain owner, and the owner or an authorized representative can approve issuance for each domain name in the certificate request. Refer to [Email validation](https://aws.amazon.com/certificate-manager/faqs//#Email_Validation_.28Public_Certificates.29) for further details.

**Q. Which validation method should I use for my public certificate: DNS or email?**

We recommend that you use DNS validation if you have the ability to change the DNS configuration for your domain. Customers who are unable to receive validation emails from ACM and those using a domain registrar that does not publish domain owner email contact information in WHOIS should use DNS validation. If you cannot modify your DNS configuration, you should use email validation.  

**Q. Can I convert an existing public certificate from email validation to DNS validation?**

No, but you can request a new, free certificate from ACM and choose DNS validation for the new one.

**Q: How long does it take for a public certificate to be issued?**

The time to issue a certificate after all of the domain names in a certificate request have been validated may be several hours or longer.

**Q: What happens when I request a public certificate?**

ACM attempts to validate ownership or control of each domain name in your certificate request, according to the validation method you chose, DNS or email, when making the request. The status of the certificate request is Pending validation while ACM attempts to validate that you own or control the domain. Refer to the [DNS validation](https://aws.amazon.com/certificate-manager/faqs//#DNS_Validation_.28Public_Certificates.29) and [Email validation](https://aws.amazon.com/certificate-manager/faqs//#Email_Validation_.28Public_Certificates.29) sections below for more information about the validation process. After all of the domain names in the certificate request are validated, the time to issue certificates may be several hours or longer. When the certificate is issued, the status of the certificate request changes to Issued and you can start using it with other AWS services that are integrated with ACM.

**Q: Does ACM check DNS Certificate Authority Authorization (CAA) records before issuing public certificates?**

Yes. DNS Certificate Authority Authorization (CAA) records allow domain owners to specify which certificate authorities are authorized to issue certificates for their domain. When you request an ACM Certificate, AWS Certificate Manager looks for a CAA record in the DNS zone configuration for your domain. If a CAA record is not present, then Amazon can issue a certificate for your domain. Most customers fall into this category.

If your DNS configuration contains a CAA record, that record must specify one of the following CAs before Amazon can issue a certificate for your domain: amazon.com, amazontrust.com, awstrust.com, or amazonaws.com. Refer to [Configure a CAA Record](https://docs.aws.amazon.com/acm/latest/userguide/setup-caa.html) or [Troubleshooting CAA Problems](https://docs.aws.amazon.com/acm/latest/userguide/troubleshooting-caa.html) in the AWS Certificate Manager User Guide for more information.

**Q: Does ACM support any other methods for validating a domain?**

Not at this time.

### DNS Validation

**Q. What is DNS validation?**

With DNS validation, you can validate your ownership of a domain by adding a CNAME record to your DNS configuration. DNS Validation makes it easy for you to establish that you own a domain when requesting public SSL/TLS certificates from ACM.

**Q. What are the benefits of DNS validation?**

DNS validation makes it easy to validate that you own or control a domain so that you can obtain an SSL/TLS certificate. With DNS validation, you simply write a CNAME record to your DNS configuration to establish control of your domain name. To simplify the DNS validation process, the ACM management console can configure DNS records for you if you manage your DNS records with Amazon Route 53. This makes it easy to establish control of your domain name with a few mouse clicks. Once the CNAME record is configured, ACM automatically renews certificates that are in use (associated with other AWS resources) as long as the DNS validation record remains in place. Renewals are fully automatic and touchless.

**Q. Who should use DNS validation?**

Anyone who requests a certificate through ACM and has the ability to change the DNS configuration for the domain they are requesting should consider using DNS validation.

**Q. Does ACM still support email validation?**

Yes. ACM continues to support email validation for customers who can’t change their DNS configuration.

**Q. What records do I need to add to my DNS configuration to validate a domain?**

You must add a CNAME record for the domain you want to validate. For example, to validate the name www.example.com, you add a CNAME record to the zone for example.com. The record you add contains a unique token that ACM generates specifically for your domain and your AWS account. You can obtain the two parts of the CNAME record (name and label) from ACM. For further instructions, refer to the [ACM User Guide.](http://docs.aws.amazon.com/acm/latest/userguide/acm-overview.html)

**Q. How can I add or modify DNS records for my domain?**

For more information about how to add or modify DNS records, check with your DNS provider. The [Amazon Route 53 DNS documentation](http://docs.aws.amazon.com/Route53/latest/DeveloperGuide/resource-record-sets-creating.html) provides further information for customers who use Amazon Route 53 DNS.

**Q. Can ACM simplify DNS validation for Amazon Route 53 DNS customers?**

Yes. For customers who are using Amazon Route 53 DNS to manage DNS records, the [ACM console](https://console.aws.amazon.com/acm/home) can add records to your DNS configuration for you when you request a certificate. Your Route 53 DNS hosted zone for your domain must be configured in the same AWS account as the one you are making the request from, and you must have sufficient permissions to make a change to your Amazon Route 53 configuration. For further instructions, refer to the [ACM User Guide](https://docs.aws.amazon.com/acm/latest/userguide/acm-overview.html).

**Q. Does DNS Validation require me to use a specific DNS provider?**

No. You can use DNS validation with any DNS provider as long as the provider allows you to add a CNAME record to your DNS configuration.

**Q. How many DNS records do I need if I want more than one certificate for the same domain?**

One. You can obtain multiple certificates for the same domain name in the same AWS account using one CNAME record. For example, if you make 2 certificate requests from the same AWS account for the same domain name, you need only 1 DNS CNAME record.

**Q. Can I validate multiple domain names with the same CNAME record?**

No. Each domain name must have a unique CNAME record.

**Q. Can I validate a wildcard domain name using DNS validation?**

Yes.

**Q. How does ACM construct CNAME records?**

DNS CNAME records have two components: a name and a label. The name component of an ACM-generated CNAME is constructed from an underscore character (\_) followed by a token, which is a unique string that is tied to your AWS account and your domain name. ACM pre-pends the underscore and token to your domain name to construct the name component. ACM constructs the label from an underscore character prepended to a different token which is also tied to your AWS account and your domain name. ACM pre-pends the underscore and token to a DNS domain name used by AWS for validations: acm-validations.aws. The following examples show the formatting of CNAMEs for www.example.com, subdomain.example.com, and \*.example.com.

> \_TOKEN1.www.example.com         CNAME     \_TOKEN2.acm-validations.aws  
> \_TOKEN3.subdomain.example.com CNAME     \_TOKEN4.acm-validations.aws  
> \_TOKEN5.example.com                 CNAME      \_TOKEN6.acm-validations.aws

Notice that ACM removes the wildcard label (\*) when generating CNAME records for wildcard names. As a result, the CNAME record generated by ACM for a wildcard name (such as \*.example.com) is the same record returned for the domain name without the wildcard label (example.com).

**Q. Can I validate all subdomains of a domain using one CNAME record?**

No. Each domain name, including host names and subdomain names, must be validated separately, each with a unique CNAME record.

**Q. Why does ACM use CNAME records for DNS validation instead of TXT records?**

Using a CNAME record allows ACM to renew certificates for as long as the CNAME record exists. The CNAME record directs to a TXT record in an AWS domain (acm-validations.aws) that ACM can update as needed to validate or re-validate a domain name, without any action from you.

**Q. Does DNS validation work across AWS Regions?**

Yes. You can create one DNS CNAME record and use it to obtain certificates in the same AWS account in any AWS Region where ACM is offered. Configure the CNAME record once and you can get certificates issued and renewed from ACM for that name without creating another record.

**Q. Can I choose different validation methods in the same certificate?**

No. Each certificate can have only one validation method.

**Q. How do I renew a certificate validated with DNS validation?**

ACM automatically renews certificates that are in use (associated with other AWS resources) as long as the DNS validation record remains in place.

**Q. Can I revoke permission to issue certificates for my domain?**

Yes. Simply remove the CNAME record. ACM does not issue or renew certificates for your domain using DNS validation after you remove the CNAME record and the change is distributed through DNS. The propagation time to remove the record depends on your DNS provider.

**Q. What happens if I remove the CNAME record?**

ACM cannot issue or renew certificates for your domain using DNS validation if you remove the CNAME record.

### Email Validation

**Q: What is email validation?**

With email validation, an approval request email is sent to the registered domain owner for each domain name in the certificate request. The domain owner or an authorized representative (approver) can approve the certificate request by following the instructions in the email. The instructions direct the approver to navigate to the approval website and click the link in the email or paste the link from the email into a browser to navigate to the approval web site. The approver confirms the information associated with the certificate request, such as the domain name, certificate ID (ARN), and the AWS account ID initiating the request, and approves the request if the information is accurate.

**Q: When I request a certificate and choose email validation, to which email addresses is the certificate approval request sent?**

When you request a certificate using email validation, a WHOIS lookup for each domain name in the certificate request is used to retrieve contact information for the domain. Email is sent to the domain registrant, administrative contact, and technical contact listed for the domain. Email is also sent to five special email addresses, which are formed by prepending admin@, administrator@, hostmaster@, webmaster@ and postmaster@ to the domain name you’re requesting. For example, if you request a certificate for server.example.com, email is sent to the domain registrant, technical contact, and administrative contact using contact information returned by a WHOIS query for the example.com domain, plus admin@server.example.com, administrator@server.example.com, hostmaster@server.example.com, postmaster@server.example.com, and webmaster@server.example.com.  
  
The five special email addresses are constructed differently for domain names that begin with "www" or wildcard names beginning with an asterisk (\*). ACM removes the leading "www" or asterisk and email is sent to the administrative addresses formed by pre-pending admin@, administrator@, hostmaster@, postmaster@, and webmaster@ to the remaining portion of the domain name. For example, if you request a certificate for www.example.com, email is sent to the WHOIS contacts, as described previously, plus admin@example.com rather than admin@www.example.com. The remaining four special email addresses are similarly formed.

After you request a certificate, you can display the list of email addresses to which the email was sent for each domain using the ACM console, AWS CLI, or APIs.

**Q: Can I configure the email addresses to which the certificate approval request is sent?**

No, but you can configure the base domain name to which you want the validation email to be sent. The base domain name must be a superdomain of the domain name in the certificate request. For example, if you want to request a certificate for server.domain.example.com but want to direct the approval email to admin@domain.example.com, you can do so using the AWS CLI or API. See [ACM CLI Reference](https://docs.aws.amazon.com/cli/latest/reference/acm/request-certificate.html) and [ACM API Reference](https://docs.aws.amazon.com/acm/latest/APIReference/API_RequestCertificate.html) for further details.

**Q: Can I use domains that have proxy contact information (such as Privacy Guard or WhoisGuard)?**

Yes; however, email delivery may be delayed as a result of the proxy. Email sent through a proxy may end up in your spam folder. Refer to the [ACM User Guide](http://docs.aws.amazon.com/acm/latest/userguide/troubleshooting-email.html) for troubleshooting suggestions.

**Q: Can ACM validate my identity using the technical contact for my AWS account?**

No. Procedures and policies for validating the domain owner’s identity are very strict, and determined by the [CA/Browser Forum](https://cabforum.org/) which sets policy standards for publicly trusted certificate authorities. To learn more, please refer to the latest Amazon Trust Services Certification Practices Statement in the [Amazon Trust Services Repository](https://www.amazontrust.com/repository/).

**Q: What should I do if I did not receive the approval email?**

Refer to the [ACM User Guide](http://docs.aws.amazon.com/acm/latest/userguide/troubleshooting-email.html) for troubleshooting suggestions.

### Private Key Protection

**Q: How are the private keys of ACM-provided certificates managed?**

A key pair is created for each certificate provided by ACM. ACM is designed to protect and manage the private keys used with SSL/TLS certificates. Strong encryption and key management best practices are used when protecting and storing private keys.

**Q: Does ACM copy certificates across AWS Regions?**

No. The private key of each ACM certificate is stored in the Region in which you request the certificate. For example, when you obtain a new certificate in the US East (N. Virginia) Region, ACM stores the private key in the N. Virginia Region. ACM certificates are only copied across Regions if the certificate is associated with a CloudFront distribution. In that case, CloudFront distributes the ACM certificate to the geographic locations configured for your distribution.

### Managed Renewal and Deployment

**Q: What is ACM managed renewal and deployment?**

ACM managed renewal and deployment manages the process of renewing SSL/TLS ACM certificates and deploying certificates after they are renewed.

**Q: What are the benefits of using ACM managed renewal and deployment?**

ACM can manage renewal and deployment of SSL/TLS certificates for you. ACM makes configuring and maintaining SSL/TLS for a secure web service or application more operationally sound than potentially error-prone manual processes. Managed renewal and deployment can help you avoid downtime due to expired certificates. ACM operates as a service that is [integrated with other AWS services](http://docs.aws.amazon.com/acm/latest/userguide/acm-services.html). This means you can centrally manage and deploy certificates on the AWS platform by using the AWS management console, AWS CLI, or APIs. With Private CA, you can create private certificates and you can export them. ACM renews exported certificates, allowing your client side automation code to download and deploy them. 

**Q: Which ACM certificates can be renewed and deployed automatically?**

<u>Public Certificates</u>

ACM can renew and deploy public ACM certificates without any additional validation from the domain owner. If a certificate cannot be renewed without additional validation, ACM manages the renewal process by validating domain ownership or control for each domain name in the certificate. After each domain name in the certificate has been validated, ACM renews the certificate and automatically deploys it with your AWS resources. If ACM cannot validate domain ownership, we will let you (the AWS account owner) know.

If you chose DNS validation in your certificate request, ACM can renew your certificate indefinitely without any further action from you, as long as the certificate is in use (associated with other AWS resources) and your CNAME record remains in place. If you selected email validation when requesting a certificate, you can improve ACM’s ability to automatically renew and deploy ACM certificates, by ensuring that the certificate is in use, that all domain names included in the certificate can be resolved to your site, and that all domain names are reachable from the Internet.

<u>Private Certificates</u>

ACM provides two options for managing private certificates issued with AWS Private CA. ACM provides different renewal capabilities depending on how you are managing your private certificates. You can choose the best management option for each private certificate you issue.

> 1. ACM can fully automate renewal and deployment of private certificates issued with AWS Private CAs and used with ACM-integrated services, such as Elastic Load Balancing and API Gateway. ACM can renew and deploy private certificates that are issued through ACM as long as the private CA that issued the certificate remains in the Active state.

> 1. For private certificates you export from ACM for use with on-premises resources, EC2 instances, and IoT devices, ACM renews your certificate automatically. You are responsible for retrieving the new certificate and private key and deploying them with your application.

**Q: When does ACM renew certificates?  
**  
ACM begins the renewal process up to 60 days prior to the certificate’s expiration date. The validity period for ACM certificates is currently 13 months (395 days). Refer to the [ACM User Guide](http://docs.aws.amazon.com/acm/latest/userguide/managed-renewal.html) for more information about managed renewal.

**Q: Will I be notified before my certificate is renewed and the new certificate is deployed?**

No. ACM may renew or rekey the certificate and replace the old one without prior notice.

**Q: Can ACM renew public certificates containing bare domains, such as “example.com” (also known as zone apex or naked domains)?**

If you chose DNS validation in your certificate request for a public certificate, then ACM can renew your certificate without any further action from you, as long as the certificate is in use (associated with other AWS resources) and your CNAME record remains in place.

If you selected email validation when requesting a public certificate with a bare domain, ensure that a DNS lookup of the bare domain resolves to the AWS resource that is associated with the certificate. Resolving the bare domain to an AWS resource may be challenging unless you use Route 53 or another DNS provider that supports alias resource records (or their equivalent) for mapping bare domains to AWS resources. For more information, refer to the [Route 53 Developer Guide](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/resource-record-sets-choosing-alias-non-alias.html).

**Q: Does my site drop existing connections when ACM deploys the renewed certificate?**

No, connections established after the new certificate is deployed use the new certificate, and existing connections are not affected.  

**Q: Can I use the same certificate with multiple Elastic Load Balancing load balancers and multiple CloudFront distributions?**

Yes.

**Q: Can I use public certificates for internal Elastic Load Balancing load balancers with no public internet access?**

Yes, but you can also consider using AWS Private CA to issue private certificates that ACM can renew without validation. See [Managed Renewal and Deployment](https://aws.amazon.com/certificate-manager/faqs//#Managed_Renewal_and_Deployment) for details about how ACM handles renewals for public certificates that are not reachable from the Internet and private certificates.

### Logging

**Q: Can I audit the use of certificate private keys?**

Yes. Using AWS CloudTrail you can review logs that tell you when the private key for the certificate was used.

**Q: What logging information is available from AWS CloudTrail?**

You can identify which users and accounts called AWS APIs for services that support AWS CloudTrail, the source IP address the calls were made from, and when the calls occurred. For example, you can identify which user made an API call to associate a certificate provided by ACM with an Elastic Load Balancer and when the Elastic Load Balancing service decrypted the key with a KMS API call.  

### Billing

**Q: How will I be charged and billed for my use of ACM certificates?**

Public and private certificates provisioned through AWS Certificate Manager for use with [ACM-integrated services](https://docs.aws.amazon.com/acm/latest/userguide/acm-services.html), such as Elastic Load Balancing, Amazon CloudFront, and Amazon API Gateway services are free. You pay for the AWS resources you create to run your application. AWS Private CA has pay as you go pricing; visit the [AWS Private CA Pricing page](https://aws.amazon.com/private-ca/pricing/) for more details and examples.