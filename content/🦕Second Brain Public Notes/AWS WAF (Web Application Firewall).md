---
tags:
  - cloud/aws
---



<mark style="background: #BBFABBA6;">AWS WAF and AWS Shield help protect your AWS resources from web exploits and DDoS attacks.</mark>

**AWS WAF** is<mark style="background: #FFB86CA6;"> a web application firewall service that helps protect your web apps from common exploits that could affect app availability, compromise security, or consume excessive resources.</mark>  
![](https://i.imgur.com/RRB0GfE.png)


**AWS Shield** <mark style="background: #FF5582A6;">provides expanded DDoS attack protection for your AWS resources. Get 24/7 support from our DDoS response team and detailed visibility into DDoS events</mark>.


AWS WAF <mark style="background: #FFF3A3A6;">helps protect web applications from attacks by allowing you to configure rules that allow, block, or monitor (count) web requests based on conditions that you define.</mark>

- These _conditions_ <mark style="background: #ADCCFFA6;">include IP addresses, HTTP headers, HTTP body, URI strings, SQL injection and cross-site scripting.</mark>
- Can allow or block web requests based on strings that appear in the requests using string match conditions.  
![](https://i.imgur.com/ALSOPAv.png)  
 ![](https://i.imgur.com/SWMdc94.png)

For example, AWS WAF can match values in the following request parts:
- Header – A specified request header, for example, the User-Agent or Referer header.
- HTTP method – <mark style="background: #CACFD9A6;">The HTTP method, which indicates the type of operation that the request is asking the origin to perform.</mark> CloudFront supports the following methods: DELETE, GET, HEAD, OPTIONS, PATCH, POST, and PUT.
- Query string – The part of a URL that appears after a ? character, if any.
- URI – The URI path of the request, which identifies the resource, for example, /images/daily-ad.jpg.
- Body – The part of a request that contains any additional data that you want to send to your web server as the HTTP request body, such as data from a form.
- Single query parameter (value only) – Any parameter that you have defined as part of the query string.
- All query parameters (values only) – As above buy inspects all parameters within the query string.

New rules can be deployed within minutes, letting you respond quickly to changing traffic patterns.

When AWS services receive requests for web sites, the requests are forwarded to AWS WAF for inspection against defined rules.

Once a request meets a condition defined in the rules, AWS WAF instructs the underlying service to either block or allow the request based on the action you define.

With AWS WAF you pay only for what you use.

AWS WAF pricing is based on how many rules you deploy and how many web requests your web application receives.

There are no upfront commitments.

AWS WAF is tightly integrated with Amazon CloudFront and the Application Load Balancer (ALB), services.

When you use AWS WAF on Amazon CloudFront, rules run in all AWS Edge Locations, located around the world close to end users.

This means security doesn’t come at the expense of performance.

Blocked requests are stopped before they reach your web servers.

When you use AWS WAF on an Application Load Balancer, your rules run in region and can be used to protect internet-facing as well as internal load balancers.

### Web Traffic Filtering

AWS WAF lets you create rules to filter web traffic based on conditions that include IP addresses, HTTP headers and body, or custom URIs.

This gives you an additional layer of protection from web attacks that attempt to exploit vulnerabilities in custom or third-party web applications.

In addition, AWS WAF makes it easy to create rules that block common web exploits like SQL injection and cross site scripting.

AWS WAF allows you to create a centralized set of rules that you can deploy across multiple websites.

This means that in an environment with many websites and web applications you can create a single set of rules that you can reuse across applications rather than recreating that rule on every application you want to protect.

### Full Feature API

AWS WAF can be completely administered via APIs.

This provides organizations with the ability to create and maintain rules automatically and incorporate them into the development and design process.

For example, a developer who has detailed knowledge of the web application could create a security rule as part of the deployment process.

This capability to incorporate security into your development process avoids the need for complex handoffs between application and security teams to make sure rules are kept up to date.

AWS WAF can also be deployed and provisioned automatically with AWS CloudFormation sample templates that allow you to describe all security rules you would like to deploy for your web applications delivered by Amazon CloudFront.

AWS WAF is integrated with Amazon CloudFront, which supports custom origins outside of AWS – this means you can protect web sites not hosted in AWS.

Support for IPv6 allows the AWS WAF to inspect HTTP/S requests coming from both IPv6 and IPv4 addresses.

### Real-time Visibility

AWS WAF provides real-time metrics and captures raw requests that include details about IP addresses, geo locations, URIs, User-Agent and Referers.

AWS WAF is fully integrated with Amazon CloudWatch, making it easy to setup custom alarms when thresholds are exceeded, or attacks occur.

This information provides valuable intelligence that can be used to create new rules to better protect applications.

# FAQ
**What is AWS WAF?**

AWS WAF is a web application firewall that helps protect web applications from attacks by allowing you to configure rules that allow, block, or monitor (count) web requests based on conditions that you define. These conditions include IP addresses, HTTP headers, HTTP body, URI strings, SQL injection and cross-site scripting.

**How does AWS WAF block or allow traffic?**

As the underlying service receives requests for your web sites, it forwards those requests to AWS WAF for inspection against your rules. Once a request meets a condition defined in your rules, AWS WAF instructs the underlying service to either block or allow the request based on the action you define.

**How does AWS WAF protect my web site or application?**

AWS WAF is tightly integrated with Amazon CloudFront, the Application Load Balancer (ALB), Amazon API Gateway, and AWS AppSync – services that AWS customers commonly use to deliver content for their websites and applications. When you use AWS WAF on Amazon CloudFront, your rules run in all AWS Edge Locations, located around the world close to your end users. This means security doesn’t come at the expense of performance. Blocked requests are stopped before they reach your web servers. When you use AWS WAF on regional services, such as Application Load Balancer, Amazon API Gateway, and AWS AppSync, your rules run in region and can be used to protect internet-facing resources as well as internal resources.  

**Can I use AWS WAF to protect web sites not hosted in AWS?**

Yes, AWS WAF is integrated with Amazon CloudFront, which supports custom origins outside of AWS.

**Which types of attacks can AWS WAF help me to stop?**

AWS WAF helps protects your website from common attack techniques like SQL injection and Cross-Site Scripting (XSS). In addition, you can create rules that can block or rate-limit traffic from specific user-agents, from specific IP addresses, or that contain particular request headers. See the [AWS WAF Developer Guide](http://docs.aws.amazon.com/console/waf) for examples.

**Which bot mitigation capabilities are available with AWS WAF?**

AWS WAF Bot Control gives you visibility and control over common and pervasive bot traffic to your applications. With Bot Control, you can easily monitor, block, or rate-limit pervasive bots, such as scrapers, scanners, and crawlers, and you can allow common bots, such as status monitors and search engines. You can use the Bot Control managed rule group alongside other Managed Rules for WAF or with your own custom WAF rules to protect your applications. See the [AWS WAF Bot Control section in the developer guide](https://docs.aws.amazon.com/waf/latest/developerguide/).   

**Can I get a history of all AWS WAF API calls made on my account for security, operational or compliance auditing?**

Yes. To receive a history of all AWS WAF API calls made on your account, you simply turn on AWS CloudTrail in the [CloudTrail's AWS Management Console](https://console.aws.amazon.com/cloudtrail/home?region=us-east-1#/gettingStarted). For more information, visit AWS CloudTrail home page or visit the [AWS WAF Developer Guide](http://docs.aws.amazon.com/waf/latest/developerguide/logging-using-cloudtrail.html).

**Does AWS WAF support IPv6?**

Yes, support for IPv6 allows the AWS WAF to inspect HTTP/S requests coming from both IPv6 and IPv4 addresses.

**Does IPSet match condition for an AWS WAF Rule support IPv6?**

Yes, you can setup new IPv6 match condition(s) for new and existing WebACLs, as per the [documentation](http://docs.aws.amazon.com/waf/latest/developerguide/web-acl-ip-conditions.html).

**Can I expect to see IPv6 address appear in the AWS WAF sampled requests where applicable?**

Yes. The sampled requests will show the IPv6 address where applicable.

**Can I use IPv6 with all AWS WAF features?**

Yes. You will be able to use all the existing features for traffic both over IPv6 and IPv4 without any discernible changes to performance, scalability or availability of the service.

**What services does AWS WAF support?**

AWS WAF can be deployed on Amazon CloudFront, the Application Load Balancer (ALB), Amazon API Gateway, and AWS AppSync. As part of Amazon CloudFront it can be part of your Content Distribution Network (CDN) protecting your resources and content at the Edge locations. As part of the Application Load Balancer it can protect your origin web servers running behind the ALBs. As part of Amazon API Gateway, it can help secure and protect your REST APIs. As part of AWS AppSync, it can help secure and protect your GraphQL APIs.  

**In what AWS Regions is AWS WAF available in?**

Please refer to the [AWS Region Services](https://aws.amazon.com/about-aws/global-infrastructure/regional-product-services/) table.  

**Is AWS WAF HIPAA eligible?**

Yes, AWS has expanded its HIPAA compliance program to include AWS WAF as a HIPAA eligible service. If you have an executed Business Associate Agreement (BAA) with AWS, you can use AWS WAF to protect your web applications from common web exploits. For more information, see [HIPAA Compliance](https://aws.amazon.com/compliance/hipaa-compliance/).

**How does AWS WAF pricing work? Are there any upfront costs?**

AWS WAF charges based on the number of web access control lists (web ACLs) that you create, the number of rules that you add per web ACL, and the number of web requests that you receive. There are no upfront commitments. AWS WAF charges are in addition to [Amazon CloudFront pricing](https://aws.amazon.com/cloudfront/pricing/), the [Application Load Balancer (ALB) pricing](https://aws.amazon.com/elasticloadbalancing/pricing/), [Amazon API Gateway pricing](https://aws.amazon.com/api-gateway/pricing/), and/or [AWS AppSync pricing](https://aws.amazon.com/appsync/pricing/).

**What is Rate-based Rule in AWS WAF?**

Rate-based Rules are type of Rule that can be configured in AWS WAF, allowing you to specify the number of web requests that are allowed by a client IP in a trailing, continuously updated, 5 minute period. If an IP address breaches the configured limit, new requests will be blocked until the request rate falls below the configured threshold.  

**How does a Rate-based rule compare to a regular AWS WAF Rule?**

Rate-based Rules are similar to regular Rules, with one addition: the ability to configure a rate-based threshold. If, for example, the threshold for the Rate-based Rule is set to (say) 2,000, the rule will block all IPs that have more than 2,000 requests in the last 5 minute interval. A Rate-based Rule can also contain any other AWS WAF Condition that is available for a regular rule.

**What does the Rate-based Rule cost?**

A Rate-based Rule costs the same as a regular AWS WAF Rule which is $1 per rule per WebACL per month

**What are the use cases for the Rate-based Rule?**

Here are some popular use cases customers can address with Rate-based rules:

- I want to block or count an IP address when that IP address exceeds the configured threshold rate (configurable in web requests per trailing 5 minute period)
- I want to know which IP address are currently being blocked because they exceeded the configured threshold rate
- I want IP addresses that have been added to the block list to be automatically removed when they are no longer violating the configured threshold rate
- I want to exempt certain high-traffic source IP ranges from being blocked by my Rate-based rules  
    

**Are the existing matching conditions compatible with the Rate-base Rule?**

Yes. Rate-based rules are compatible with existing AWS WAF match conditions. This allows you to further refine your match criteria and limit rate-based mitigations to specific URLs of your website or traffic coming from specific referrers (or user agents) or add other custom match criteria.

**Can I use Rate-based rule to mitigate Web layer DDoS attacks?**

Yes. This new rules type is designed to protect you from use cases such web-layer DDoS attacks, brute force login attempts and bad bots.

**What visibility features does Rate-based Rules offer?**

Rate-based Rules support all the visibility features currently available on the regular AWS WAF Rules. Additionally, they will get visibility into the IP addresses blocked as a result of the Rate-based Rule.

**Can I use Rate-based rule to limit access to a certain parts of my Webpage?**

Yes. Here is an example. Suppose that you want to limit requests to the login page on your website. To do this, you could add the following string match condition to a rate-based rule:

- The Part of the request to filter on is “URI”.  
    
- The Match Type is “Starts with”.  
    
- A Value to match is “/login” (this need to be whatever identifies the login page in the URI portion of the web request)  
    

Additionally, you would specify a Rate Limit of, say, 15,000 requests per 5 minutes. Adding this rate-based rule to a web ACL will limit requests to your login page per IP address without affecting the rest of your site.

**Can I exempt certain high-traffic source IP ranges from being blocked by my Rate-based Rule(s)?**

Yes. You can do this by having a separate IP match condition that allows the request within the Rate-base Rule.  

**How accurate is your GeoIP database?**

The accuracy of the IP Address to country lookup database varies by region. Based on recent tests, our overall accuracy for the IP address to country mapping is 99.8%.