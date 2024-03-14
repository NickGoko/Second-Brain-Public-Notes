---
tags:
  - cloud/aws
---
![[Pasted image 20240210235359.png]]  
 
![[Pasted image 20240210235455.png]]

**CloudFront** is <mark style="background: #ABF7F7A6;">a web service that gives businesses and web application developers an easy and cost-effective way to distribute content with low latency and high data transfer speeds.</mark>

<mark style="background: #ADCCFFA6;">CloudFront is a good choice for distribution of frequently accessed static content that benefits from edge delivery—like popular website images, videos, media files or software downloads.</mark>

- Used for dynamic, static, streaming, and interactive content.

- CloudFront is a global service:
	- Ingress to upload objects.
	- Egress to distribute content.

Amazon CloudFront provides a simple API that lets you:
- Distribute content with low latency and high data transfer rates by serving requests using a network of edge locations around the world.
- Get started without negotiating contracts and minimum commitments.

You can use a zone apex name on CloudFront.

CloudFront supports wildcard CNAME.

Supports wildcard SSL certificates, Dedicated IP, Custom SSL and SNI Custom SSL (cheaper).

Supports Perfect Forward Secrecy which creates a new private key for each SSL session.  
![[Pasted image 20240214150019.png]]
## Edge Locations and Regional Edge Caches

- An edge location is the location where content is cached (separate to AWS regions/AZs).
- Requests are automatically routed to the nearest edge location.
- Edge locations are not tied to Availability Zones or regions.
- <mark style="background: #ADCCFFA6;">Regional Edge Caches are located between origin web servers and global edge locations and have a larger cache.</mark>  
<mark style="background: #FFF3A3A6;">Regional Edge Caches have larger cache-width than any individual edge location, so your objects remain in cache longer at these locations.</mark>

Regional Edge caches aim to get content closer to users.

Proxy methods PUT/POST/PATCH/OPTIONS/DELETE go directly to the origin from the edge locations and do not proxy through Regional Edge caches.

Dynamic content goes straight to the origin and does not flow through Regional Edge caches.

<mark style="background: #FFB86CA6;">Edge locations are not just read only, you can write to them too.  
</mark>  
The diagram below shows where Regional Edge Caches and Edge Locations are placed in relation to end users:

![Amazon CloudFront Edge Locations and Regional Edge Caches](https://digitalcloud.training/wp-content/uploads/2022/01/amazon-cloudfront-edge-locations-and-regional-edge.jpeg)

## Origins

<mark style="background: #ADCCFFA6;">An origin is the origin of the files that the CDN will distribute.</mark>

- <mark style="background: #BBFABBA6;">Origins can be either an S3 bucket, an EC2 instance, an Elastic Load Balancer, or Route 53</mark> – can also be external (non-AWS).
- When using Amazon S3 as an origin you place all your objects within the bucket.
- You can use an existing bucket and the bucket is not modified in any way.
- By default all newly created buckets are private.
- You can setup access control to your buckets using:
	- Bucket policies.
	- Access Control Lists.

- <mark style="background: #ADCCFFA6;">You can make objects publicly available or use CloudFront signed URLs.</mark>

A _custom origin server_ is <mark style="background: #FFB86CA6;">a HTTP server which can be an EC2 instance or an on-premises/non-AWS based web server.</mark>

<mark style="background: #ABF7F7A6;">When using an on-premises or non-AWS based web server you must specify the DNS name, ports, and protocols that you want CloudFront to use when fetching objects from your origin.</mark>  
![[Pasted image 20240210235423.png]]  
![[Pasted image 20240211002205.png]]

- Most CloudFront features are supported for custom origins except RTMP distributions (must be an S3 bucket).

When using EC2 for custom origins Amazon recommend:
- Use an AMI that automatically installs the software for a web server.
- Use ELB to handle traffic across multiple EC2 instances.
- Specify the URL of your load balancer as the domain name of the origin server.

S3 static website:

- Enter the S3 static website hosting endpoint for your bucket in the configuration.
- Example: `http://<bucketname>.s3-website-<region>.amazonaws.com.`

![[Pasted image 20240211002104.png]]  
![[Pasted image 20240211002130.png]]


- <mark style="background: #ADCCFFA6;">Objects are cached for 24 hours by default.</mark>

- The expiration time is controlled through the TTL.

The minimum expiration time is 0.

Static websites on Amazon S3 are considered custom origins.

AWS origins are Amazon S3 buckets (not a static website).

CloudFront keeps persistent connections open with origin servers.

Files can also be uploaded to CloudFront.

**High availability with Origin Failover:**
- Can set up CloudFront with origin failover for scenarios that require high availability.
- Uses an origin group in which you designate a primary origin for CloudFront plus a second origin that CloudFront automatically switches to when the primary origin returns specific HTTP status code failure responses.
- For more info, check this [**article**](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/high_availability_origin_failover.html).
- Also works with Lambda@Edge functions.

## **CloudFront Summary**
- provides low latency and high data transfer speeds for distribution of static, dynamic web or streaming content to web users
- delivers the content through a worldwide network of data centers called **Edge Locations**
- keeps persistent connections with the origin servers so that the files can be fetched from the origin servers as quickly as possible.
- dramatically **reduces the number of network hops** that users’ requests must pass through
- supports **multiple origin server options**, like AWS hosted service _for e.g. S3, EC2, ELB_ or an on premise server, which stores the original, definitive version of the objects
- **single distribution can have multiple origins** and Path pattern in a cache behavior determines which requests are routed to the origin
- supports **Web Download** distribution and **RTMP** **Streaming** distribution
    - Web distribution supports static, dynamic web content, on demand using progressive download & HLS and live streaming video content
    - RTMP supports streaming of media files using Adobe Media Server and the Adobe Real-Time Messaging Protocol (RTMP) **ONLY**
- supports HTTPS using either
    - **dedicated IP address**, which is expensive as dedicated IP address is assigned to each CloudFront edge location
    - **Server Name Indication (SNI)**, which is free but supported by modern browsers only with the domain name available in the request header
- For E2E HTTPS connection,
    - **Viewers -> CloudFront** needs either **self signed certificate, or certificate issued by CA or ACM**
    - **CloudFront -> Origin** needs **certificate issued by ACM for ELB and by CA for other origins**
-  Security
    - **Origin Access Identity** (OAI) can be used to restrict the content from S3 origin to be accessible from CloudFront only
    - supports **Geo restriction (Geo-Blocking) to whitelist or blacklist** countries that can access the content
    - **Signed URLs** 
        - for RTMP distribution as signed cookies aren’t supported
        - to restrict access to individual files, _for e.g., an installation download for your application._
        - users using a client, _for e.g. a custom HTTP client,_ that doesn’t support cookies
    - **Signed Cookies**
        - provide access to multiple restricted files, _for e.g., video part files in HLS format or all of the files in the subscribers’ area of a website._
        - don’t want to change the current URLs
    - integrates with AWS **WAF**, a web application firewall that helps protect web applications from attacks by allowing rules configured based on IP addresses, HTTP headers, and custom URI strings
- supports **GET, HEAD, OPTIONS, PUT, POST, PATCH, DELETE** to get object & object headers, add, update, and delete objects
    - **only caches** responses to **GET and HEAD** requests and, optionally, OPTIONS requests
    - **does not cache** responses to **PUT, POST, PATCH, DELETE** request methods and these requests are proxied back to the origin
- object **removal** from cache
    - would be removed upon **expiry (TTL)** from the cache, by default 24 hrs
    - can be **invalidated** **explicitly**, but has a cost associated, however might continue to see the old version until it expires from those caches
    - objects can be **invalidated only for Web distribution**
    - change object name, **versioning**, to serve different version
- supports adding or modifying custom headers before the request is sent to origin which can be used to
    - **validate** if user is accessing the content from CDN
    - **identifying CDN** from which the request was forwarded from, in case of multiple CloudFront distribution
    - for **viewers not supporting CORS** to return the Access-Control-Allow-Origin header for every request
- supports **Partial GET requests** using range header to download object in smaller units improving the efficiency of partial downloads and recovery from partially failed transfers
- supports **compression** to compress and serve compressed files when viewer requests include Accept-Encoding: gzip in the request header
- supports different **price class** to include all regions, to include only least expensive regions and other regions to exclude most expensive regions
- supports **access logs** which contain detailed information about every user request for both web and RTMP distribution

## Distributions
<mark style="background: #ADCCFFA6;">To distribute content with CloudFront you need to create a distribution.</mark>

<mark style="background: #FFB8EBA6;">The distribution includes the configuration of the CDN </mark>including:
- Content origins.
- Access (public or restricted).
- Security (HTTP or HTTPS).
- Cookie or query-string forwarding.
- Geo-restrictions.
- Access logs (record viewer activity).

There are two types of distribution.

**Web Distribution**:
- Static and dynamic content including .html, .css, .php, and graphics files.
- Distributes files over HTTP and HTTPS.
- Add, update, or delete objects, and submit data from web forms.
- Use <mark style="background: #FFF3A3A6;">live streaming</mark> to stream an event in real time.

**RTMP**:
- <mark style="background: #FFF3A3A6;">Distribute streaming media files</mark> using Adobe Flash Media Server’s RTMP protocol.
- Allows an end user to begin playing a media file before the file has finished downloading from a CloudFront edge location.
- <mark style="background: #CACFD9A6;">Files must be stored in an S3 bucket.</mark>

To use CloudFront live streaming, create a web distribution.

For serving both the media player and media files you need two types of distributions:
- A web distribution for the media player.
- An RTMP distribution for the media files.

- S3 buckets can be configured to create access logs and cookie logs which log all requests made to the S3 bucket.

- Amazon Athena can be used to analyze access logs.
- CloudFront is integrated with CloudTrail.
- CloudTrail saves logs to the S3 bucket you specify.

<mark style="background: #FFB8EBA6;">CloudTrail captures information about all requests whether they were made using the CloudFront console, the CloudFront API, the AWS SDKs, the CloudFront CLI, or another service.</mark>

CloudTrail can be used to determine which requests were made, the source IP address, who made the request etc.

To view CloudFront requests in CloudTrail logs you must update an existing trail to include global services.

To delete a distribution it must first be disabled (can take up to 15 minutes).

The diagram below depicts Amazon CloudFront Distributions and Origins:

![Amazon CloudFront Distributions and Origins](https://digitalcloud.training/wp-content/uploads/2022/01/amazon-cloudfront-distributions-and-origins.jpeg)

## Cache Behavior

Allows you to configure a variety of CloudFront functionality for a given URL path pattern.

For each cache behavior you can configure the following functionality:

- The path pattern (e.g. /images/_.jpg, /images_.php).
- The origin to forward requests to (if there are multiple origins).
- Whether to forward query strings.
- Whether to require signed URLs.
- Allowed HTTP methods.
- Minimum amount of time to retain the files in the CloudFront cache (regardless of the values of any cache-control headers).

The default cache behavior only allows a path pattern of /*.

Additional cache behaviors need to be defined to change the path pattern following creation of the distribution.

You can restrict access to content using the following methods:

- Restrict access to content using signed cookies or signed URLs.
- Restrict access to objects in your S3 bucket.

A special type of user called an Origin Access Identity (OAI) can be used to restrict access to content in an Amazon S3 bucket.

By using an OAI you can restrict users so they cannot access the content directly using the S3 URL, they must connect via CloudFront.

You can define the viewer protocol policy:
- HTTP and HTTPS.
- Redirect HTTP to HTTPS.
- HTTPS only.

You can define the Allowed HTTP Methods:

- GET, HEAD.
- GET, HEAD, OPTIONS.
- GET, HEAD, OPTIONS, PUT, POST, PATCH, DELETE.

For web distributions you can configure CloudFront to require that viewers use HTTPS.

Field-Level Encryption:

- Field-level encryption adds an additional layer of security on top of HTTPS that lets you protect specific data so that it is only visible to specific applications.
- Field-level encryption allows you to securely upload user-submitted sensitive information to your web servers.
- The sensitive information is encrypted at the edge closer to the user and remains encrypted throughout application processing.

Origin policy:

- HTTPS only.
- Match viewer – CloudFront matches the protocol with your custom origin.
- Use match viewer only if you specify Redirect HTTP to HTTPS or HTTPS only for the viewer protocol policy.
- CloudFront caches the object once even if viewers make requests using HTTP and HTTPS.

Object invalidation:

- You can remove an object from the cache by invalidating the object.
- You cannot cancel an invalidation after submission.
- You cannot invalidate media files in the Microsoft Smooth Streaming format when you have enabled Smooth Streaming for the corresponding cache behavior.  
![[Pasted image 20240211002505.png]]  
Objects are cached for the TTL (always recorded in seconds, default is 24 hours, default max is 1 year).

Only caches for GET requests (not PUT, POST, PATCH, DELETE).

Dynamic content is cached.

Consider how often your files change when setting the TTL.

Invalidation can be used to immediately revoke cached objects – chargeable.

Deletions propagate.

## Cache Hit Ratio

A good cache hit ratio means more requests are served from the cache.

Methods of improving the cache hit ratio include:

- Use the Cache-Control max-age directive to increase the time objects remain in the cache
- Use Origin Shield.
- Forward only the query string parameters for which your origin will return unique objects.
- Configure CloudFront to forward only specified cookies instead of forwarding all cookies.
- Configure CloudFront to forward and cache based on only specified headers instead of forwarding and caching based on all headers.

## Restrictions

<mark style="background: #BBFABBA6;">Blacklists and whitelists can be used for geography – you can only use one at a time.</mark>

There are two options available for geo-restriction (geo-blocking):
- Use the CloudFront geo-restriction feature (use for restricting access to all files in a distribution and at the country level).
- Use a 3rd party geo-location service (use for restricting access to a subset of the files in a distribution and for finer granularity at the country level).  
![[Pasted image 20240211002237.png]]

## Lambda@Edge

Can be used to run Lambda at Edge Locations.

Lets you run Node.js and Python Lambda functions to customize content that CloudFront delivers.

Executes the functions in AWS locations closer to the viewer.

You can use Lambda functions to change CloudFront requests and responses at the following points:

- After CloudFront receives a request from a viewer (viewer request).
- Before CloudFront forwards the request to the origin (origin request).
- After CloudFront receives the response from the origin (origin response).
- Before CloudFront forwards the response to the viewer (viewer response).

Lambda@Edge can do the following:

- Inspect cookies and rewrite URLs to perform A/B testing.
- Send specific objects to your users based on the User-Agent header.
- Implement access control by looking for specific headers before passing requests to the origin.
- Add, drop, or modify headers to direct users to different cached objects.
- Generate new HTTP responses.
- Cleanly support legacy URLs.
- Modify or condense headers or URLs to improve cache utilization.
- Make HTTP requests to other Internet resources and use the results to customize responses.

_**Exam tip:**_ _Lambda@Edge can be used to load different resources based on the User-Agent HTTP header._

## Signed URLs and Signed Cookies

A signed URL includes additional information, for example, an expiration date and time, that gives you more control over access to your content. This additional information appears in a policy statement, which is based on either a canned policy or a custom policy.

CloudFront signed cookies allow you to control who can access your content when you don’t want to change your current URLs or when you want to provide access to multiple restricted files, for example, all the files in the subscribers’ area of a website.

Application must authenticate user and then send three Set-Cookie headers to the viewer; the viewer stores the name-value pair and adds them to the request in a Cookie header when requesting access to content.

Use signed URLs in the following cases:

- You want to restrict access to individual files, for example, an installation download for your application.
- Your users are using a client (for example, a custom HTTP client) that doesn’t support cookies.

Use signed cookies in the following cases:

- You want to provide access to multiple restricted files, for example, all the files for a video in HLS format or all the files in the subscribers’ area of website.
- You don’t want to change your current URLs.

## Origin Access Identity
Used in combination with signed URLs and signed cookies to restrict direct access to an S3 bucket (prevents bypassing the CloudFront controls).

An **origin access identity (OAI)** is <mark style="background: #FFF3A3A6;">a special CloudFront user that is associated with the distribution.</mark>

Permissions must then be changed on the Amazon S3 bucket to restrict access to the OAI.

If users request files directly by using Amazon S3 URLs, they’re denied access.

The origin access identity has permission to access files in your Amazon S3 bucket, but users don’t.

## AWS WAF

AWS WAF is a web application firewall that lets you monitor HTTP and HTTPS requests that are forwarded to CloudFront and lets you control access to your content.

With AWS WAF you can shield access to content based on conditions in a web access control list (web ACL) such as:

- Origin IP address.
- Values in query strings.

CloudFront responds to requests with the requested content or an HTTP 403 status code (forbidden).

CloudFront can also be configured to deliver a custom error page.

Need to associate the relevant distribution with the web ACL.

## Security

PCI DSS compliant but recommended not to cache credit card information at edge locations.

HIPAA compliant as a HIPAA eligible service.

Distributed Denial of Service (DDoS) protection:

- CloudFront distributes traffic across multiple edge locations and filters requests to ensure that only valid HTTP(S) requests will be forwarded to backend hosts. CloudFront also supports geo-blocking, which you can use to prevent requests from geographic locations from being served.

## Domain Names

CloudFront typically creates a domain name such as a232323.cloudfront.net.

Alternate domain names can be added using an alias record (Route 53).

For other service providers use a CNAME (cannot use the zone apex with CNAME).

Moving domain names between distributions:

- You can move subdomains yourself.
- For the root domain you need to use AWS support.

## High Availability

CloudFront caches content at Edge Locations around the world. The more objects served by the cache, the fewer the requests to the origin.  This reduces the load on your origin server and reduces latency.

You can set up CloudFront with [**origin failover**](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/high_availability_origin_failover.html) for scenarios that require high availability.

To set up origin failover, you must have a distribution with at least two origins. Next, you create an origin group for your distribution that includes two origins, setting one as the primary. Finally, you create or update a cache behavior to use the origin group.

## Monitoring and Reporting

You can view [**operational metrics**](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/viewing-cloudfront-metrics.html) about your CloudFront distributions and Lambda@Edge functions in the CloudFront console.

The following default metrics are included for all CloudFront distributions, at no additional cost:

**Requests**

The total number of viewer requests received by CloudFront, for all HTTP methods and for both HTTP and HTTPS requests.

**Bytes downloaded**

The total number of bytes downloaded by viewers for GET, HEAD, and OPTIONS requests.

**Bytes uploaded**

The total number of bytes that viewers uploaded to your origin with CloudFront, using POST and PUT requests.

**4xx error rate**

The percentage of all viewer requests for which the response’s HTTP status code is 4xx.

**5xx error rate**

The percentage of all viewer requests for which the response’s HTTP status code is 5xx.

**Total error rate**

The percentage of all viewer requests for which the response’s HTTP status code is 4xx or 5xx.

In addition to the default metrics, you can enable additional metrics for an additional cost.

These additional metrics must be enabled for each distribution separately:

**Cache hit rate**

The percentage of all cacheable requests for which CloudFront served the content from its cache. HTTP POST and PUT requests, and errors, are not considered cacheable requests.

**Origin latency**

The total time spent from when CloudFront receives a request to when it starts providing a response to the network (not the viewer), for requests that are served from the origin, not the CloudFront cache. This is also known as _first byte latency_, or _time-to-first-byte_.

**Error rate by status code**

The percentage of all viewer requests for which the response’s HTTP status code is a particular code in the 4xx or 5xx range. This metric is available for all the following error codes: 401, 403, 404, 502, 503, and 504.

## Logging and Auditing

S3 buckets can be configured to create access logs and cookie logs which log all requests made to the S3 bucket.

Amazon Athena can be used to analyze access logs.

CloudFront is integrated with CloudTrail.

CloudTrail saves logs to the S3 bucket you specify.

CloudTrail captures information about all requests whether they were made using the CloudFront console, the CloudFront API, the AWS SDKs, the CloudFront CLI, or another service.

CloudTrail can be used to determine which requests were made, the source IP address, who made the request etc.

To view CloudFront requests in CloudTrail logs you must update an existing trail to include global services.

## Charges

There is an option for reserved capacity over 12 months or longer (starts at 10TB of data transfer in a single region).

You pay for:

- Data Transfer Out to Internet.
- Data Transfer Out to Origin.
- Number of HTTP/HTTPS Requests.
- Invalidation Requests.
- Dedicated IP Custom SSL.
- Field level encryption requests.

You do not pay for:

- Data transfer between AWS regions and CloudFront.
- Regional edge cache.
- AWS ACM SSL/TLS certificates.
- Shared CloudFront certificates.  
![[Pasted image 20240211002341.png]]  
![[Pasted image 20240211002404.png]]  
![[Pasted image 20240211002424.png]]

![[Module 11 - Caching Content#**Amazon CloudFront**]]

# FAQ
## General

**Q. What is Amazon CloudFront?**

Amazon CloudFront is a web service that gives businesses and web application developers an easy and cost effective way to distribute content with low latency and high data transfer speeds. Like other AWS services, Amazon CloudFront is a self-service, pay-per-use offering, requiring no long term commitments or minimum fees. With CloudFront, your files are delivered to end-users using a global network of edge locations.

**Q. What can I do with Amazon CloudFront?**

Amazon CloudFront provides a simple API that lets you:

- Distribute content with low latency and high data transfer rates by serving requests using a network of edge locations around the world.
- Get started without negotiating contracts and minimum commitments.

**Q. How do I get started with Amazon CloudFront?**

Click the “Create Free Account” button on the Amazon CloudFront detail page. If you choose to use another AWS service as the origin for the files served through Amazon CloudFront, you must [sign up](https://portal.aws.amazon.com/billing/signup) for that service before creating CloudFront distributions.

**Q. How do I use Amazon CloudFront?**

To use Amazon CloudFront, you:

- For static files, store the definitive versions of your files in one or more origin servers. These could be Amazon S3 buckets. For your dynamically generated content that is personalized or customized, you can use Amazon EC2 – or any other web server – as the origin server. These origin servers will store or generate your content that will be distributed through Amazon CloudFront.
- Register your origin servers with Amazon CloudFront through a simple API call. This call will return a CloudFront.net domain name that you can use to distribute content from your origin servers via the Amazon CloudFront service. For instance, you can register the Amazon S3 bucket “bucketname.s3.amazonaws.com” as the origin for all your static content and an Amazon EC2 instance “dynamic.myoriginserver.com” for all your dynamic content. Then, using the API or the AWS Management Console, you can create an Amazon CloudFront distribution that might return “abc123.cloudfront.net” as the distribution domain name.
- Include the cloudfront.net domain name, or a CNAME alias that you create, in your web application, media player, or website. Each request made using the cloudfront.net domain name (or the CNAME you set-up) is routed to the edge location best suited to deliver the content with the highest performance. The edge location will attempt to serve the request with a local copy of the file. If a local copy is not available, Amazon CloudFront will get a copy from the origin. This copy is then available at that edge location for future requests.

**Q. How does Amazon CloudFront provide higher performance?**

Amazon CloudFront employs a global network of edge locations and regional edge caches that cache copies of your content close to your viewers. Amazon CloudFront ensures that end-user requests are served by the closest edge location. As a result, viewer requests travel a short distance, improving performance for your viewers. For files not cached at the edge locations and the regional edge caches, Amazon CloudFront keeps persistent connections with your origin servers so that those files can be fetched from the origin servers as quickly as possible. Finally, Amazon CloudFront uses additional optimizations – e.g. wider TCP initial congestion window – to provide higher performance while delivering your content to viewers.

**Q. How does Amazon CloudFront lower my costs to distribute content over the Internet?**

Like other AWS services, Amazon CloudFront has no minimum commitments and charges you only for what you use. Compared to self-hosting, Amazon CloudFront spares you from the expense and complexity of operating a network of cache servers in multiple sites across the internet and eliminates the need to over-provision capacity in order to serve potential spikes in traffic. Amazon CloudFront also uses techniques such as collapsing simultaneous viewer requests at an edge location for the same file into a single request to your origin server. This reduces the load on your origin servers reducing the need to scale your origin infrastructure, which can bring you further cost savings.

Additionally, if you are using an AWS origin (e.g., Amazon S3, Amazon EC2, etc.), effective December 1, 2014, **we are no longer charging for AWS data transfer out to Amazon CloudFront**. This applies to data transfer from all AWS regions to all global CloudFront edge locations.

**Q. How does Amazon CloudFront speed up my entire website?**

Amazon CloudFront uses standard cache control headers you set on your files to identify static and dynamic content. Delivering all your content using a single Amazon CloudFront distribution helps you make sure that performance optimizations are applied to your entire website or web application. When using AWS origins, you benefit from improved performance, reliability, and ease of use as a result of AWS’s ability to track and adjust origin routes, monitor system health, respond quickly when any issues occur, and the integration of Amazon CloudFront with other AWS services. You also benefit from using different origins for different types of content on a single site – e.g. Amazon S3 for static objects, Amazon EC2 for dynamic content, and custom origins for third-party content – paying only for what you use.

**Q. How is Amazon CloudFront different from Amazon S3?**

Amazon CloudFront is a good choice for distribution of frequently accessed static content that benefits from edge delivery—like popular website images, videos, media files or software downloads.

**Q. How is Amazon CloudFront different from traditional content delivery solutions?**

Amazon CloudFront lets you quickly obtain the benefits of high performance content delivery without negotiated contracts or high prices. Amazon CloudFront gives all developers access to inexpensive, pay-as-you-go pricing – with a self-service model. Developers also benefit from tight integration with other Amazon Web Services. The solution is simple to use with Amazon S3, Amazon EC2, and Elastic Load Balancing as origin servers, giving developers a powerful combination of durable storage and high performance delivery. Amazon CloudFront also integrates with Amazon Route 53 and AWS CloudFormation for further performance benefits and ease of configuration.

**Q. What types of content does Amazon CloudFront support?**

Amazon CloudFront supports content that can be sent using the HTTP or WebSocket protocols. This includes dynamic web pages and applications, such as HTML or PHP pages or WebSocket-based applications, and any popular static files that are a part of your web application, such as website images, audio, video, media files or software downloads. Amazon CloudFront also supports delivery of live or on-demand media streaming over HTTP.

**Q. Does Amazon CloudFront work with non-AWS origin servers?**

Yes. Amazon CloudFront works with any origin server that holds the original, definitive versions of your content, both static and dynamic. There is no additional charge to use a custom origin.

**Q. How does Amazon CloudFront enable origin redundancy?**

For every origin that you add to a CloudFront distribution, you can [assign a backup origin](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/high_availability_origin_failover.html) that can be used to automatically serve your traffic if the primary origin is unavailable. You can choose a combination of HTTP 4xx/5xx status codes that, when returned from the primary origin, trigger the failover to the backup origin. The two origins can be any combination of AWS and non-AWS origins.

**Q: Does Amazon CloudFront offer a Service Level Agreement (SLA)?**

Yes. The Amazon CloudFront SLA provides for a service credit if a customer’s monthly uptime percentage is below our service commitment in any billing cycle. More information can be found [here](https://aws.amazon.com/cloudfront/sla/).

**Q: Can I use the AWS Management Console with Amazon CloudFront?**

Yes. You can use the AWS Management Console to configure and manage Amazon CloudFront though a simple, point-and-click web interface. The AWS Management Console supports most of Amazon CloudFront’s features, letting you get Amazon CloudFront’s low latency delivery without writing any code or installing any software. Access to the AWS Management Console is provided free of charge at [https://console.aws.amazon.com](https://console.aws.amazon.com/).

**Q: What tools and libraries work with Amazon CloudFront?**

There are a variety of tools for managing your Amazon CloudFront distribution and libraries for various programming languages available in our [resource center](https://aws.amazon.com/cloudfront/resources/).

**Q. Can I point my zone apex (example.com versus www.example.com) at my Amazon CloudFront distribution?**

Yes. By using Amazon Route 53, AWS’s authoritative DNS service, you can configure an ‘Alias’ record that lets you map the apex or root (example.com) of your DNS name to your Amazon CloudFront distribution. Amazon Route 53 will then respond to each request for an Alias record with the right IP address(es) for your CloudFront distribution. Route 53 doesn't charge for queries to Alias records that are mapped to a CloudFront distribution. These queries are listed as "Intra-AWS-DNS-Queries" on the Amazon Route 53 usage report.

## Edge Locations

**Q. What is CloudFront Regional Edge Cache?**

CloudFront delivers your content through a worldwide network of data centers called edge locations. The regional edge caches are located between your origin web server and the global edge locations that serve content directly to your viewers. This helps improve performance for your viewers while lowering the operational burden and cost of scaling your origin resources.

**Q. How does regional edge caching work?**

Amazon CloudFront has multiple globally dispersed [Regional Edge Caches](https://aws.amazon.com/cloudfront/features/) (or RECs), providing an additional caching layer close your end-users. They are located between your origin webserver and AWS edge locations that serve content directly to your users. As cached objects become less popular, individual edge locations may remove those objects to make room for more commonly requested content. Regional Edge Caches have a larger cache width than any individual edge location, so objects remain cached longer. This helps keep more of your content closer to your viewers, reducing the need for CloudFront to go back to your origin webserver and improving overall performance for viewers. For example, CloudFront edge locations in Europe now go to the regional edge cache in Frankfurt to fetch an object before going back to your origin webserver. Regional edge cache locations can be used with any origin, such as S3, EC2, or custom origins. RECs are skipped in Regions currently hosting your application origins.  

**Q. Is regional edge cache feature enabled by default?**

Yes. You do not need to make any changes to your CloudFront distributions; this feature is enabled by default for all new and existing CloudFront distributions. There are no additional charges to use this feature.

**Q. Where are the edge network locations used by Amazon CloudFront located?**

Amazon CloudFront uses a global network of edge locations and regional edge caches for content delivery. You can see a full list of Amazon CloudFront locations [here](https://aws.amazon.com/cloudfront/details/).

**Q. Can I choose to serve content (or not serve content) to specified countries?**

Yes, the Geo Restriction feature lets you specify a list of countries in which your users can access your content. Alternatively, you can specify the countries in which your users cannot access your content. In both cases, CloudFront responds to a request from a viewer in a restricted country with an HTTP status code 403 (Forbidden).

**Q. How accurate is your GeoIP database?**

The accuracy of the IP Address to country lookup database varies by region. Based on recent tests, our overall accuracy for the IP address to country mapping is 99.8%.

**Q. Can I serve a custom error message to my end users?**

Yes, you can create custom error messages (for example, an HTML file or a .jpg graphic) with your own branding and content for a variety of HTTP 4xx and 5xx error responses. Then you can configure Amazon CloudFront to return your custom error messages to the viewer when your origin returns one of the specified errors to CloudFront.

**Q. How long will Amazon CloudFront keep my files at the edge locations?**

By default, if no cache control header is set, each edge location checks for an updated version of your file whenever it receives a request more than 24 hours after the previous time it checked the origin for changes to that file. This is called the “expiration period.” You can set this expiration period as short as 0 seconds, or as long as you’d like, by setting the cache control headers on your files in your origin. Amazon CloudFront uses these cache control headers to determine how frequently it needs to check the origin for an updated version of that file. For expiration period set to 0 seconds, Amazon CloudFront will revalidate every request with the origin server. If your files don’t change very often, it is best practice to set a long expiration period and implement a versioning system to manage updates to your files.

**Q. How do I remove an item from Amazon CloudFront edge locations?**

There are multiple options for removing a file from the edge locations. You can simply delete the file from your origin and as content in the edge locations reaches the expiration period defined in each object’s HTTP header, it will be removed. In the event that offensive or potentially harmful material needs to be removed before the specified expiration time, you can use the Invalidation API to remove the object from all Amazon CloudFront edge locations. You can see the charge for making invalidation requests [here](https://aws.amazon.com/cloudfront/pricing/).

**Q. Is there a limit to the number of invalidation requests I can make?**

If you're invalidating objects individually, you can have invalidation requests for up to 3,000 objects per distribution in progress at one time. This can be one invalidation request for up to 3,000 objects, up to 3,000 requests for one object each, or any other combination that doesn't exceed 3,000 objects.

If you're using the \* wildcard, you can have requests for up to 15 invalidation paths in progress at one time. You can also have invalidation requests for up to 3,000 individual objects per distribution in progress at the same time; the limit on wildcard invalidation requests is independent of the limit on invalidating objects individually. If you exceed this limit, further invalidation requests will receive an error response until one of the earlier request completes.

You should use invalidation only in unexpected circumstances; if you know beforehand that your files will need to be removed from cache frequently, it is recommended that you either implement a versioning system for your files and/or set a short expiration period.  

## Compliance

**Q. Is Amazon CloudFront PCI compliant?**

Amazon CloudFront \[excluding content delivery through CloudFront Embedded POPs\] is included in the set of services that are compliant with the Payment Card Industry Data Security Standard (PCI DSS) Merchant Level 1, the highest level of compliance for service providers. Please see our [developer's guide](http://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/compliance.html) for more information.

**Q: Is Amazon CloudFront HIPAA eligible?**

AWS has expanded its HIPAA compliance program to include Amazon CloudFront \[excluding content delivery through CloudFront Embedded POPs\] as a HIPAA eligible service. If you have an executed Business Associate Agreement (BAA) with AWS, you can use Amazon CloudFront \[excluding content delivery through CloudFront Embedded POPs\] to accelerate the delivery of protected health information (PHI). For more information, see [HIPAA Compliance](https://aws.amazon.com/compliance/hipaa-compliance/) and our [developer's guide](http://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/compliance.html).

**Q: Is Amazon CloudFront SOC compliant?**

Amazon CloudFront \[excluding content delivery through CloudFront Embedded POPs\] is compliant with SOC (System & Organization Control) measures. SOC Reports are independent third-party examination reports that demonstrate how AWS achieves key compliance controls and objectives. For more information see, [AWS SOC Compliance](https://aws.amazon.com/compliance/soc-faqs/) and our [developer's guide](http://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/compliance.html).

**Q: How do I request an AWS SOC1, SOC 2, or SOC 3 Report?**

The AWS SOC 1 and SOC 2 reports are available to customers by using AWS Artifact, a self-service portal for on-demand access to AWS compliance reports. Sign in to [AWS Artifact in the AWS Management Console](https://console.aws.amazon.com/artifact), or learn more at [Getting Started with AWS Artifact](https://aws.amazon.com/artifact/getting-started/). The latest [AWS SOC 3 Report](https://d1.awsstatic.com/whitepapers/compliance/AWS_SOC3.pdf) is publicly available on the AWS website.  

## HTTP, HTTP/2 and HTTP/3

**Q. What types of HTTP requests are supported by Amazon CloudFront?**

Amazon CloudFront currently supports GET, HEAD, POST, PUT, PATCH, DELETE and OPTIONS requests.

**Q. Does Amazon CloudFront cache POST responses?**

Amazon CloudFront does not cache the responses to POST, PUT, DELETE, and PATCH requests – these requests are proxied back to the origin server. You may enable [caching](https://aws.amazon.com/caching/cdn/) for the responses to OPTIONS requests.

**Q. How do I use HTTP/2?**

If you have an existing Amazon CloudFront distribution, you can turn on HTTP/2 using the API or the Management Console. In the Console, go to the “Distribution Configuration” page and navigate to the section “Supported HTTP Versions.” There, you can select "HTTP/2, HTTP/1.1, or HTTP/1.0". HTTP/2 is automatically enabled for all new CloudFront distributions.

**Q. What if my origin does not support HTTP/2?**

Amazon CloudFront currently supports HTTP/2 for delivering content to your viewers’ clients and browsers. For communication between the edge location and your origin servers, Amazon CloudFront will continue to use HTTP/1.1.

**Q. Does Amazon CloudFront support HTTP/2 without TLS?**

Not currently. However, most of the modern browsers support HTTP/2 only over an encrypted connection. You can learn more about using SSL with Amazon CloudFront [here](https://aws.amazon.com/cloudfront/custom-ssl-domains/).  

**Q. What is HTTP/3?**

HTTP/3 is the third major version of the Hypertext Transfer Protocol. HTTP/3 uses QUIC, a user datagram protocol (UDP) based, stream-multiplexed, and secure transport protocol that combines and improves upon the capabilities of existing transmission control protocol (TCP), TLS, and HTTP/2. HTTP/3 offers several benefits over previous HTTP versions, including faster response times and enhanced security.

**Q. What is QUIC?**

HTTP/3 is powered by QUIC, a new highly performant, resilient, and secure internet transport protocol. CloudFront's HTTP/3 support is built on top of s2n-quic, a new open source QUIC protocol implementation in Rust. To learn more about QUIC, refer the “[Introducing s2n-quic](https://aws.amazon.com/blogs/security/introducing-s2n-quic-open-source-protocol-rust/)“ blog. 

**Q. What are the key benefits of using HTTP/3 with Amazon CloudFront?**

Customers are constantly looking to deliver faster and more secure applications for their end users. As internet penetration increases globally and more users come online via mobile and from remote networks, the need for improved performance and reliability is greater than ever. HTTP/3 enables this as it offers several performance improvements over previous HTTP versions:  

1. **Faster and reliable connections** - CloudFront uses 1-RTT for TLS handshake for HTTP/3 reducing the connection establishment time and a corresponding reduction in handshake failure compared to previous HTTP versions.
2. **Better web performance** - CloudFront’s HTTP/3 implementation supports client-side connection migrations, allowing client applications to recover from poor connections with minimal interruptions. Unlike TCP, QUIC is not lossless making it better suited for congested networks with high packet loss. Also, QUIC allows faster re-connections during Wifi or cellular handoffs.  
    
3. **Security** - HTTP/3 offers more comprehensive security compared to previous versions of HTTP by encrypting packets exchanged during TLS handshakes. This makes inspection by middleboxes harder providing additional privacy, and reducing man-in-the-middle attacks. CloudFront's HTTP/3 support is built on top of s2n-quic and Rust, both with a strong emphasis on efficiency and performance.  
    

**Q. How do I enable HTTP/3 on my CloudFront distributions?**  

You can turn on HTTP/3 for new and existing Amazon CloudFront distributions using the CloudFront Console, the UpdateDistribution API action, or using a Cloudformation template. In the Console, go to the “Distribution Configuration” page and navigate to the section “Supported HTTP Versions.” There, you can select "HTTP/3, HTTP/2, HTTP/1.1, or HTTP/1.0."  

**Q. Do I need to make changes to my applications before enabling HTTP/3?**

When you enable HTTP/3 on your CloudFront distribution, CloudFront automatically adds the Alt-Svc header, which it uses to advertise that HTTP/3 support is available and you don’t need to manually add the Alt-Svc header. We expect you to enable support for multiple protocols in your applications, such that if the application fails to establish a HTTP/3 connection it will fall back to HTTP /1.1 or HTTP/2. i.e., clients that do not support HTTP/3 will still be able to communicate with HTTP/3 enabled CloudFront distributions using HTTP/1.1 or HTTP/2. Fallback support is a required part of the HTTP/3 specification and is implemented by all major browsers that support HTTP/3.  

**Q. What if my origin does not support HTTP/3?**

CloudFront currently supports HTTP/3 for communication between your viewers’ clients/browsers and CloudFront edge locations. For communication between the edge location and your origin servers, CloudFront will continue to use HTTP/1.1.  

**Q. How do Amazon CloudFront's TLS security policies interact with HTTP/3?**

HTTP/3 uses QUIC - which requires TLSv1.3. Therefore, independent of the security policy you have chosen, only TLSv1.3 and the supported TLSv1.3 cipher suites can be used to establish HTTP/3 connections. For more details, refer to the supported protocols and ciphers between viewers and CloudFront section of the CloudFront developers guide for details.  

**Q. Is there a separate charge for enabling HTTP/3?**

No, there is no separate charge for enabling HTTP/3 on Amazon CloudFront distributions. HTTP/3 requests will be charged at the request pricing rates as per your pricing plan.  

## WebSocket

**Q. What are WebSockets?**

WebSocket is a real-time communication protocol that provides bidirectional communication between a client and a server over a long-held TCP connection. By using a persistent open connection, the client and the server can send real-time data to each other without the client having to frequently reinitiate connections checking for new data to exchange. WebSocket connections are often used in chat applications, collaboration platforms, multiplayer games, and financial trading platforms. Refer to our documentation to learn more about [using the WebSocket protocol](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/distribution-working-with.websockets.html) with Amazon CloudFront. 

**Q. How do I enable my Amazon CloudFront distribution to support the WebSocket protocol?**

You can use WebSockets globally, and no additional configuration is needed to enable the WebSocket protocol within your CloudFront resource as it is now supported by default.  

**Q. When is a WebSocket connection established through Amazon CloudFront?**

Amazon CloudFront establishes WebSocket connections only when the client includes the 'Upgrade: websocket' header and the server responds with the HTTP status code 101 confirming that it can switch to the WebSocket protocol.  

**Q. Does Amazon CloudFront support secured WebSockets over TLS?**

Yes. Amazon CloudFront supports encrypted WebSocket connections (WSS) using the SSL/TLS protocol.

## Security

**Q. Can I configure my CloudFront distribution to deliver content over HTTPS using my own domain name?**

By default, you can deliver your content to viewers over HTTPS by using your CloudFront distribution domain name in your URLs, for example, https://dxxxxx.cloudfront.net/image.jpg. If you want to deliver your content over HTTPS using your own domain name and your own SSL certificate, you can use one of our Custom SSL certificate support features. [Learn more](https://aws.amazon.com/cloudfront/custom-ssl-domains/).

**Q. What is Field-Level Encryption?**

Field-Level Encryption is a feature of CloudFront that allows you to securely upload user-submitted data such as credit card numbers to your origin servers. Using this functionality, you can further encrypt sensitive data in an HTTPS form using field-specific encryption keys (which you supply) before a PUT/ POST request is forwarded to your origin. This ensures that sensitive data can only be decrypted and viewed by certain components or services in your application stack. To learn more about field-level encryption, see [Field-Level Encryption](http://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/field-level-encryption.html) in our documentation.

**Q. I am already using SSL/ TLS encryption with CloudFront, do I still need Field-Level Encryption?**

Many web applications collect sensitive data such as credit card numbers from users that is then processed by application services running on the origin infrastructure. All these web applications use SSL/TLS encryption between the end user and CloudFront, and between CloudFront and your origin. Now, your origin could have multiple micro-services that perform critical operations based on user input. However, typically sensitive information only needs to be used by a small subset of these micro-services, which means most components have direct access to these data for no reason. A simple programming mistake, such as logging the wrong variable could lead to a customer’s credit card number being written to a file.

With field-level encryption, CloudFront’s edge locations can encrypt the credit card data. From that point on, only applications that have the private keys can decrypt the sensitive fields. So the order fulfillment service can only view encrypted credit card numbers, but the payment services can decrypt credit card data. This ensures a higher level of security since even if one of the application services leaks cipher text, the data remains cryptographically protected.

**Q. What is the difference between SNI Custom SSL and Dedicated IP Custom SSL of Amazon CloudFront?**

**Dedicated IP Custom SSL** allocates dedicated IP addresses to serve your SSL content at each CloudFront edge location. Because there is a one to one mapping between IP addresses and SSL certificates, Dedicated IP Custom SSL works with browsers and other clients that do not support SNI. Due to the current IP address costs, Dedicated IP Custom SSL is $600/month prorated by the hour.

**SNI Custom SSL** relies on the SNI extension of the Transport Layer Security protocol, which allows multiple domains to serve SSL traffic over the same IP address by including the hostname viewers are trying to connect to. As with Dedicated IP Custom SSL, CloudFront delivers content from each Amazon CloudFront edge location and with the same security as the Dedicated IP Custom SSL feature. SNI Custom SSL works with most modern browsers, including Chrome version 6 and later (running on Windows XP and later or OS X 10.5.7 and later), Safari version 3 and later (running on Windows Vista and later or Mac OS X 10.5.6. and later), Firefox 2.0 and later, and Internet Explorer 7 and later (running on Windows Vista and later). Older browsers that do not support SNI cannot establish a connection with CloudFront to load the HTTPS version of your content. SNI Custom SSL is available at no additional cost beyond standard CloudFront data transfer and request fees.

**Q. What is Server Name Indication?**

Server Name Indication (SNI) is an extension of the Transport Layer Security (TLS) protocol. This mechanism identifies the domain (server name) of the associated SSL request so the proper certificate can be used in the SSL handshake. This allows a single IP address to be used across multiple servers. SNI requires browser support to add the server name, and while most modern browsers support it, there are a few legacy browsers that do not. For more details see the SNI section of the [CloudFront Developer Guide](http://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/SecureConnections.html#CNAMEsAndHTTPS) or the [SNI Wikipedia article](http://en.wikipedia.org/wiki/Server_Name_Indication).

**Q. Does CloudFront Integrate with AWS Certificate Manager?**

Yes, you can now provision SSL/TLS certificates and associate them with CloudFront distributions within minutes. Simply provision a certificate using the new AWS Certificate Manager (ACM) and deploy it to your CloudFront distribution with a couple of clicks, and let ACM manage certificate renewals for you. ACM allows you to provision, deploy, and manage the certificate with no additional charges.

Note that CloudFront still supports using certificates that you obtained from a third-party certificate authority and uploaded to the IAM certificate store.

**Q. Does Amazon CloudFront support access controls for paid or private content?**

Yes, Amazon CloudFront has an optional private content feature. When this option is enabled, Amazon CloudFront will only deliver files when you say it is okay to do so by securely signing your requests. Learn more about this feature by reading the [CloudFront Developer Guide](http://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/PrivateContent.html).

**Q. How can I safeguard my web applications delivered via CloudFront from DDoS attacks?**

As an AWS customer, you get [AWS Shield Standard](https://aws.amazon.com/shield/) at no additional cost. AWS Shield is a managed service that provides protection against DDoS attacks for web applications running on AWS. AWS Shield Standard provides protection for all AWS customers against common and most frequently occurring Infrastructure (layer 3 and 4) attacks like SYN/UDP Floods, Reflection attacks, and others to support high availability of your applications on AWS.

[AWS Shield Advanced](https://aws.amazon.com/shield/) is an optional paid service available to AWS Business Support and AWS Enterprise Support customers. AWS Shield Advanced provides additional protections against larger and more sophisticated attacks for your applications running on Elastic Load Balancing (ELB), Amazon CloudFront and Route 53.

**Q. How can I protect my web applications delivered via CloudFront?**

You can integrate your CloudFront distribution with [AWS WAF](https://aws.amazon.com/waf/), a web application firewall that helps protect web applications from attacks by allowing you to configure rules based on IP addresses, HTTP headers, and custom URI strings. Using these rules, AWS WAF can block, allow, or monitor (count) web requests for your web application. Please see [AWS WAF Developer Guide](http://docs.aws.amazon.com/console/waf) for more information.  

## Caching

**Q. Can I add or modify request headers forwarded to the origin?**

Yes, you can configure Amazon CloudFront to add custom headers, or override the value of existing headers, to requests forwarded to your origin. You can use these headers to help validate that requests made to your origin were sent from CloudFront; you can even configure your origin to only allow requests that contain the custom header values you specify. Additionally, if you use multiple CloudFront distributions with the same origin, you can use custom headers to distinguish origin request made by each different distribution. Finally, custom headers can be used to help determine the right CORS headers returned for your requests. You can configure custom headers via the CloudFront API and the AWS Management Console. There are no additional charges for this feature. For more details on how to set your custom headers, you can read more [here](http://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/forward-custom-headers.html).

**Q. How does Amazon CloudFront handle HTTP cookies?**

Amazon CloudFront supports delivery of dynamic content that is customized or personalized using HTTP cookies. To use this feature, you specify whether you want Amazon CloudFront to forward some or all of your cookies to your custom origin server. Amazon CloudFront then considers the forwarded cookie values when identifying a unique object in its cache. This way, your end users get both the benefit of content that is personalized just for them with a cookie and the performance benefits of Amazon CloudFront. You can also optionally choose to log the cookie values in Amazon CloudFront access logs.

**Q. How does Amazon CloudFront handle query string parameters in the URL?**

A query string may be optionally configured to be part of the cache key for identifying objects in the Amazon CloudFront cache. This helps you build dynamic web pages (e.g. search results) that may be cached at the edge for some amount of time.

**Q. Can I specify which query parameters are used in the cache key?**

Yes, [the query string whitelisting feature](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/distribution-web-values-specify.html#DownloadDistValuesQueryStringWhiteList) allows you to easily configure Amazon CloudFront to only use certain parameters in the cache key, while still forwarding all of the parameters to the origin.

**Q. Is there a limit to the number of query parameters that can be whitelisted?**

Yes, you can configure Amazon CloudFront to whitelist up to 10 query parameters.

**Q. What parameter types are supported?**

Amazon CloudFront supports URI query parameters as defined in section 3.4 of RFC3986. Specifically, it supports query parameters embedded in an HTTP GET string after the ‘?’ character, and delimited by the ‘&’ character.

**Q. Does CloudFront support gzip compression?**

Yes, CloudFront can automatically compress your text or binary data. To use the feature, simply specify in your cache behavior settings that you would like CloudFront to compress objects automatically and ensure that your client adds Accept-Encoding: gzip in the request header (most modern web browsers do this by default). For more information on this feature, please see [our developer guide](http://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/ServingCompressedFiles.html).  

## Streaming

**Q. What is streaming? Why would I want to stream?**

Generally, streaming refers to delivering audio and video to end users over the Internet without having to download the media file prior to playback. The protocols used for streaming include those that use HTTP for delivery such as Apple’s HTTP Live Streaming (HLS), MPEG Dynamic Adaptive Streaming over HTTP (MPEG-DASH), Adobe’s HTTP Dynamic Streaming (HDS) and Microsoft’s Smooth Streaming. These protocols are different than the delivery of web pages and other online content because streaming protocols deliver media in real time – viewers watch the bytes as they are delivered. Streaming content has several potential benefits for you and your end-users:

- Streaming can give viewers more control over their viewing experience. For instance, it is easier for a viewer to seek forward and backward in a video using streaming than using traditional download delivery.
- Streaming can give you more control over your content, as no file remains on the viewer's client or local drive when they finish watching a video.
- Streaming can help reduce your costs, as it only delivers the portions of a media file that viewers actually watch. In contrast, with traditional downloads, frequently the whole media file will be delivered to viewers, even if they only watch a portion of the file.

**Q. Does Amazon CloudFront support video-on-demand (VOD) streaming protocols?**

Yes, Amazon CloudFront provides you with multiple options to deliver on-demand video content. If you have media files that have been converted to HLS, MPEG-DASH, or Microsoft Smooth Streaming, for example using [AWS Elemental MediaConvert](https://aws.amazon.com/mediaconvert/), prior to being stored in Amazon S3 (or a custom origin), you can use an [Amazon CloudFront web distribution](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/distribution-working-with.html) to stream in that format without having to run any media servers.

Alternatively, you can also run a third party streaming server (e.g. Wowza Media Server available on AWS Marketplace) on Amazon EC2, which can convert a media file to the required HTTP streaming format. This server can then be designated as the origin for an Amazon CloudFront web distribution.

Visit the [Video on Demand (VOD)](https://aws.amazon.com/answers/media-entertainment/video-on-demand-on-aws/) on AWS page to learn more.

**Q. Does Amazon CloudFront support live streaming to multiple platforms?**

Yes. You can use Amazon CloudFront live streaming with any live video origination service that outputs HTTP-based streams, such as [AWS Elemental MediaPackage](https://aws.amazon.com/mediapackage/) or [AWS Elemental MediaStore](https://aws.amazon.com/mediastore/). MediaPackage is a video origination and just-in-time packaging service that allows video distributors to securely and reliably deliver streaming content at scale using multiple delivery and content protection standards. MediaStore is an HTTP origination and storage service that offers the high performance, immediate consistency, and predictable low latency required for live media combined with the security and durability of Amazon storage.

Visit the [AWS Live Video Streaming page](https://aws.amazon.com/answers/media-entertainment/live-streaming/) to learn more.  

## Origin Shield

**Q. What is Origin Shield?**

Origin Shield is a centralized caching layer that helps increase your cache hit ratio to reduce the load on your origin. Origin Shield also decreases your origin operating costs by collapsing requests across regions so as few as one request goes to your origin per object. When enabled, CloudFront will route all origin fetches through Origin Shield, and only make a request to your origin if the content is not already stored in Origin Shield's cache.

**Q. When should I use Origin Shield?**

Origin Shield is ideal for workloads with viewers that are spread across different geographical regions or workloads that involve just-in-time packaging for video streaming, on-the-fly image handling, or similar processes. Using Origin Shield in front of your origin will reduce the number of redundant origin fetches by first checking its central cache and only making a consolidated origin fetch for content not already in Origin Shield’s cache. Similarly, Origin Shield can be used in a multi-CDN architecture to reduce the number of duplicate origin fetches across CDNs by positioning Amazon CloudFront as the origin to other CDNs. Refer to the Amazon CloudFront Developer Guide for more details on these and other [Origin Shield Use Cases](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/origin-shield.html#origin-shield-use-cases).

**Q. Which Origin Shield Region should I use?**

Amazon CloudFront offers Origin Shield in AWS Regions where CloudFront has a [regional edge cache](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/HowCloudFrontWorks.html#CloudFrontRegionaledgecaches). When you enable Origin Shield, you should choose the AWS Region for Origin Shield that has the lowest latency to your origin. You can use Origin Shield with origins that are in an AWS Region, and with origins that are not in AWS. For more information, see [Choosing the AWS Region](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/origin-shield.html#choose-origin-shield-region) for Origin Shield in the Amazon CloudFront Developer Guide.

**Q. Is Origin Shield resilient and highly available?**

Yes. All Origin Shield Regions are built using a highly-available architecture that spans several Availability Zones with fleets of auto-scaling Amazon EC2 instances. Connections from CloudFront locations to Origin Shield also use active error tracking for each request to automatically route the request to a secondary Origin Shield location if the primary Origin Shield location is unavailable.  

## Limits

**Q. Can I use Amazon CloudFront if I expect usage peaks higher than 150 Gbps or 250,000 RPS?**

Yes. Complete our request for higher limits [here](https://aws.amazon.com/cloudfront-request/), and we will add more capacity to your account within two business days.

**Q: Is there a limit to the number of distributions my Amazon CloudFront account may deliver?**  
For the current limit on the number of distributions that you can create for each AWS account, see [Amazon CloudFront Limits](http://docs.aws.amazon.com/general/latest/gr/aws_service_limits.html#limits_cloudfront) in the Amazon Web Services General Reference. To request a higher limit, please go to the [CloudFront Limit Increase Form](https://aws.amazon.com/support/createCase?type=service_limit_increase&serviceLimitIncreaseType=cloudfront-distributions).

**Q: What is the maximum size of a file that can be delivered through Amazon CloudFront?**

<mark style="background: #FF5582A6;">The maximum size of a single file that can be delivered through Amazon CloudFront is 30 GB</mark>. This limit applies to all Amazon CloudFront distributions.

## Logging and Reporting

**Q: What logging capabilities are available with Amazon CloudFront?**

When you create or modify a CloudFront distribution, you can enable access logging. CloudFront provides two ways to log the requests that are delivered from your distributions: **Standard logs** and **Real-time logs**.

**CloudFront standard logs** are delivered to the Amazon S3 bucket of your choice (log records are delivered within minutes of a viewer request). When enabled, CloudFront will automatically publish detailed log information in a W3C extended format into an Amazon S3 bucket that you specify. Access logs contain detailed information about each request for your content, including the object requested, the date and time of the request, the edge location serving the request, the client IP address, the referrer, the user agent, the cookie header, and the result type (for example, cache hit, or miss, or error). CloudFront doesn’t charge for standard logs, though you incur Amazon S3 charges for storing and accessing the log files.

**CloudFront real-time** logs are delivered to the data stream of your choice in Amazon Kinesis Data Streams (log records are delivered within seconds of a viewer request). You can choose the sampling rate for your real-time logs—that is, the percentage of requests for which you want to receive real-time log records. You can also choose the specific fields that you want to receive in the log records. CloudFront real-time logs contain all the same data points as the standard logs and also contain certain additional information about each request such as viewer request headers, and country code, in a W3C extended format. CloudFront charges for real-time logs, in addition to the charges you incur for using Kinesis Data Streams.

**Q: How do I determine the appropriate CloudFront logs for my use case?**

You can choose a destination depending on your use case. If you have time sensitive use cases and require access log data quickly within a few seconds, then choose the real-time logs. If you need your real-time log pipeline to be cheaper, you can choose to filter the log data by enabling logs only for specific cache behaviors, or choosing a lower sampling rate. The real-time log pipeline is built for quick data delivery. Therefore, log records may be dropped if there are data delays. On the other hand, if you need a low cost log processing solution with no requirement for real-time data then the current standard log option is ideal for you. The standard logs in S3 are built for completeness and the logs are typically available in a few mins. These logs can be enabled for the entire distribution and not for specific cache behaviors. Therefore, if you require logs for adhoc investigation, audit, and analysis, you can choose to only enable the standard logs in S3. You could choose to use a combination of both the logs. Use a filtered list of real-time logs for operational visibility and then use the standard logs for audit.

**Q: What are the different log destination options available?**  
CloudFront standard logs are delivered to your S3 bucket. You can also use the integration build by third party solutions such as DataDog and Sumologic to create dashboards from these logs.

The real-time logs are delivered to your Kinesis Data Stream. From Kinesis Data Streams, the logs can be published to Amazon Kinesis Data Firehose. Amazon Kinesis Data Firehose supports easy data delivery to Amazon S3, Amazon Redshift, Amazon Elasticsearch Service, and service providers like Datadog, New Relic, and Splunk. Kinesis Firehose also supports data delivery to a generic HTTP endpoint.

**Q: How many Kinesis shards do I need in Kinesis Data Stream?**  
Use the following steps to estimate the number of shards you need:

1. Calculate (or estimate) the number of requests per second that your CloudFront distribution receives. You can use the CloudFront usage reports or the CloudFront metrics to help you calculate your requests per second.
2. Determine the typical size of a single real-time log record. A typical record that includes all available fields is around 1 KB. If you’re not sure what your log record size is, you can enable real-time logs with a low sampling rate (for example, 1%), and then calculate the average record size using monitoring data in Kinesis Data Streams (total number of records divided by total incoming bytes).
3. Multiply the number of requests per second (from step 1) by the size of a typical real-time log record (from step 2) to determine the amount of data per second that your real-time log configuration is likely to send to the Kinesis data stream.
4. Using the data per second, calculate the number of shards that you need. A single shard can handle no more than 1 MB per second and 1,000 requests (log records) per second. When calculating the number of shards that you need, we recommend adding up to 25% as a buffer.

For example, assume your distribution receives 10,000 requests per second, and that your real-time log records size is typically 1 KB. This means that your real-time log configuration could generate 10,000,000 bytes (10,000 multiplied by 1,000), or 9.53 MB, per second. In this scenario you would need just 10 Kinesis shards. You should consider creating at least 12 shards to have some buffer.  

**Q: Does Amazon CloudFront offer ready-to-use reports so I can learn more about my usage, viewers, and content being served?**

Yes. Whether it's receiving detailed cache statistics reports, monitoring your CloudFront usage, seeing where your customers are viewing your content from, or setting near real-time alarms on operational metrics, Amazon CloudFront offers a variety of solutions for your reporting needs. You can access all our reporting options by visiting the Amazon CloudFront Reporting & Analytics dashboard in the AWS Management Console. You can also learn more about our various reporting options by viewing Amazon CloudFront's [Reports & Analytics page](https://aws.amazon.com/cloudfront/reporting/).

**Q: Can I tag my distributions?**

Yes. Amazon CloudFront supports cost allocation tagging. Tags make it easier for you to allocate costs and optimize spending by categorizing and grouping AWS resources. For example, you can use tags to group resources by administrator, application name, cost center, or a specific project. To learn more about cost allocation tagging, see [Using Cost Allocation Tags](http://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/cost-alloc-tags.html). If you are ready to add tags to you CloudFront distributions, see [Amazon CloudFront Add Tags page](http://docs.aws.amazon.com/console/cloudfront/tagging).

**Q: Can I get a history of all Amazon CloudFront API calls made on my account for security, operational or compliance auditing?**

Yes. To receive a history of all Amazon CloudFront API calls made on your account, you simply turn on AWS CloudTrail in the [CloudTrail's AWS Management Console](https://console.aws.amazon.com/cloudtrail). For more information, visit [AWS CloudTrail home page](https://aws.amazon.com/cloudtrail/).

**Q: Do you have options for monitoring and alarming metrics in real time?**

You can monitor, alarm and receive notifications on the operational performance of your Amazon CloudFront distributions within just a few minutes of the viewer request using Amazon CloudWatch. CloudFront automatically publishes six operational metrics, each at 1-minute granularity, into Amazon CloudWatch. You can then use CloudWatch to set alarms on any abnormal patterns in your CloudFront traffic. To learn how to get started monitoring CloudFront activity and setting alarms via CloudWatch, please view our walkthrough in the [Amazon CloudFront Developer Guide](http://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/monitoring-using-cloudwatch.html) or simply navigate to the [Amazon CloudFront Management Console](https://console.aws.amazon.com/cloudfront/home) and select Monitoring & Alarming in the navigation pane.  

## CloudFront Functions

**Q: What is CloudFront Functions?  
**

CloudFront Functions is a serverless edge compute feature allowing you to run JavaScript code at CloudFront edge locations for lightweight HTTP(s) transformations and manipulations. Functions is purpose-built to give customers the flexibility of a full programming environment with the performance and security that modern web applications require. At a fraction of the price of [AWS Lambda@Edge](https://aws.amazon.com/lambda/edge/), customers can scale instantly and affordably to support millions of requests per second.

**Q: How do I customize content with CloudFront Functions?**

CloudFront Functions is natively built into CloudFront, allowing customers to easily build, test, and deploy functions within the same service. You can also utilize CloudFront KeyValueStore with CloudFront Functions to store and retrieve lookup data to complement your function logic. Our [GitHub repo](https://github.com/aws-samples/amazon-cloudfront-functions) makes it easy for developers to get started by offering a large collection of example code that can be used as starting point for building functions. You can build functions on the CloudFront console using the IDE or the CloudFront APIs/CLI. Once your code is authored, you can test your function against a production CloudFront distribution, ensuring your function will execute properly once deployed. The test functionality in the console offers a visual editor to quickly create test events and validate functions. Once associated to a CloudFront distribution, the code is deployed to AWS’s globally distributed network of edge locations for execution in response to CloudFront requests.

**Q: What are the use cases for CloudFront Functions?**

CloudFront Functions is ideal for lightweight, short-running functions like the following:

- **Cache key normalization**: You can transform HTTP request attributes (headers, query strings, cookies, even the relative path of the request URL) to create an optimal cache key, which can improve your cache hit ratio.
- **Header manipulation**: You can insert, modify, or delete HTTP headers in the request or response. For example, you can add HTTP strict transport security (HSTS) or cross-origin resource sharing (CORS) headers to every response.
- **URL redirects or rewrites**: You can redirect viewers to other pages based on information in the request, or redirect all request from one path to another.
- **Request authorization**: You can validate authorization tokens, such as JSON web tokens (JWT), by inspecting authorization headers or other request metadata.

**Q: What is CloudFront KeyValueStore?**

CloudFront KeyValueStore is a global, low-latency, fully managed key-value data store. KeyValueStore enables the retrieval of key value data from within CloudFront Functions, making functions more customizable by allowing independent data updates. The key value data is accessible across all CloudFront edge locations, providing a highly efficient, in-memory key-value store with fast reads from within CloudFront Functions.  

**Q: What are the use cases for CloudFront KeyValueStore?**

CloudFront KeyValueStore is ideal for frequent reads at the edge locations and infrequent updates such as :

- **Maintain URL rewrites and redirects:** Redirect users to a specific country site based on geo-location. Storing and updating these geo-based URLs in KeyValueStore simplifies the management of URLs.
- **A/B testing and feature flags**: Run experiments by assigning a percentage of traffic to a version of your website. You can update experiment weights without updating function code or your CloudFront distribution.
- **Access authorization:** Implement access control and authorization for the content delivered through CloudFront by creating and validating user-generated tokens, such as HMAC tokens or JSON web tokens (JWT), to allow or deny requests. 

**Q: Is CloudFront Functions replacing Lambda@Edge?  
**  
No - CloudFront Functions is meant to compliment Lambda@Edge, not replace it. The combination of Lambda@Edge and CloudFront Functions allows you to pick the right tool for the job. You can choose to use both CloudFront Functions and Lambda@Edge on different event triggers within the same cache behavior in your CloudFront distributions. As an example, you can use Lambda@Edge to manipulate streaming manifest files on-the-fly to inject custom tokens to secure live streams. You can use CloudFront Functions to validate those token when a user makes a request for a segment from the manifest.

**Q: Should I use CloudFront Functions or Lambda@Edge?  
**  
The combination of CloudFront Functions and Lambda@Edge gives you two powerful and flexible options for running code in response to CloudFront events. Both offer secure ways to execute code in response to CloudFront events without managing infrastructure. CloudFront Functions was purpose-built for lightweight, high scale, and latency sensitive request/response transformations and manipulations. Lambda@Edge uses general-purpose runtimes that support a wide range of computing needs and customizations. You should use Lambda@Edge for computationally intensive operations. This could be computations that take longer to complete (several milliseconds to seconds), take dependencies on external 3rd party libraries, require integrations with other AWS services (e.g., S3, DynamoDB), or need networks calls for data processing. Some of the popular advanced Lambda@Edge use cases include HLS streaming manifest manipulation, integrations with 3rd party authorization and bot detection services, server-side rendering (SSR) of single-page apps (SPA) at the edge and more. See the [Lambda@Edge use cases page](https://aws.amazon.com/lambda/edge/) for more details.

**Q: How does AWS keep CloudFront Functions secure?  
**  
CloudFront Functions delivers the performance, scale and cost-effectiveness that you expect, but with a unique security model that offers strict isolation boundaries between the Functions code. When you run custom code in a shared, multi-tenant compute environment, maintaining a highly secure execution environment is key. A bad actor may attempt exploit bugs present in the runtime, libraries, or CPU to leak sensitive data from the server or from another customer’s functions. Without a rigorous isolation barrier between function code, these exploits are possible. Both AWS Lambda and Lambda@Edge already achieve this security isolation through the [Firecracker based VM isolation](https://aws.amazon.com/about-aws/whats-new/2018/11/firecracker-lightweight-virtualization-for-serverless-computing). With CloudFront Functions, we have developed a process-based isolation model that provides the same security bar against side-channel attacks like Spectre and Meltdown, timing-based attacks or other code vulnerabilities. CloudFront Functions cannot access or modify data belonging to other customers. We do this by running functions in a dedicated process on a dedicated CPU. CloudFront Functions executes on process workers that only serve one customer at a time and all customer-specific data is cleared (flushed) between executions.

CloudFront Functions’ does not use V8 as a JavaScript engine. Functions’ security model is different, and considered more secure than the v8 isolates based model offered by some other vendors.

**Q: How do I know my CloudFront Function will execute successfully?  
**  
You can test any function by using the built in test functionality. Testing a function will execute your code against a CloudFront distribution to validate the function returns the expected result. In addition to validating the code execution, you are also provided with a **compute utilization metric**. The compute utilization metric gives you a percentage of how close your function is to the execution time limit. For example, a compute utilization of 30 means your function is using 30% total allowable execution time. Test objects can be created by using a visual editor, allowing you to easily add query strings, headers, URLs, and HTTP methods for each object, or you can create test objects using a JSON representation of the request or response. Once the test has been run, the results and the compute utilization metric can be seen in either the same visual editor style or by viewing the JSON response. If the function executes successfully and the Compute Utilization metric is not near 100, you know the function will work when associated to a CloudFront distribution.

**Q: How can I monitor a CloudFront Function?  
**  
CloudFront Functions output both metrics and execution logs to monitor the usage and performance of a function. Metrics are generated for each invocation of a function and you can see metrics from each function individually on the CloudFront or CloudWatch console. Metrics include the number of invocations, compute utilization, validation errors and execution errors. If your function results in a validation error or execution error, the error message will also appear in your CloudFront access logs, giving you better visibility into how the function impacts your CloudFront traffic. In addition to metrics, you can also generate execution logs by including a console.log() statement inside your function code. Any log statement will generate a CloudWatch log entry that will be sent to CloudWatch. Logs and metrics are included as part of the [CloudFront Functions price](https://aws.amazon.com/cloudfront/pricing/). 

## Lambda@Edge

**Q: What is Lambda@Edge?**

[Lambda@Edge](https://aws.amazon.com/lambda/edge/)  is an extension of [AWS Lambda](https://aws.amazon.com/lambda/) allowing you to run code at global edge locations without provisioning or managing servers. Lambda@Edge offers powerful and flexible serverless computing for complex functions and full application logic closer to your viewers. Lambda@Edge functions run in a Node.js or Python environment. You publish functions to a single AWS Region, and when you associate the function with a CloudFront distribution, Lambda@Edge automatically replicates your code around the world. Lambda@Edge scales automatically, from a few requests per day to thousands per second.

**Q: How do I customize content with Lambda@Edge?**

Lambda@Edge are executed by associating functions against specific cache behaviors in CloudFront. You can also specify at which point during the CloudFront request or response processing the function should execute (i.e., when a viewer request lands, when a request is forwarded to or received back from the origin, or right before responding back to the end viewer). You to write code using Node.js or Python from the Lambda console, API, or using frameworks like the [Serverless Application Model (SAM)](https://aws.amazon.com/serverless/sam/). When you have tested your function, you associate it with the selected CloudFront cache behavior and event trigger. Once saved, the next time a request is made to your CloudFront distribution, the function is propagated to the CloudFront edge, and will scale and execute as needed. Learn more in our [documentation](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/lambda-at-the-edge.html).

**Q: What Lambda@Edge events can be triggered with Amazon CloudFront?**  

Your Lambda@Edge functions will automatically trigger in response to the following Amazon CloudFront events:

- **Viewer Request**: This event occurs when an end user or a device on the Internet makes an HTTP(S) request to CloudFront, and the request arrives at the edge location closest to that user.
- **Viewer Response**: This event occurs when the CloudFront server at the edge is ready to respond to the end user or the device that made the request.
- **Origin Request**: This event occurs when the CloudFront edge server does not already have the requested object in its cache, and the viewer request is ready to be sent to your backend origin webserver (e.g. Amazon EC2, or Application Load Balancer, or Amazon S3).
- **Origin Response**: This event occurs when the CloudFront server at the edge receives a response from your backend origin webserver.  
    

## Continuous Deployment

**Q: What is continuous deployment on CloudFront?**

Continuous deployment on CloudFront provides the ability to test and validate the configuration changes with a portion of live traffic before deploying changes to all viewers.

Continuous deployment with CloudFront gives you a high level of deployment safety. You can now deploy two separate but identical environments—blue and green, and enable simple integration into your continuous integration and delivery (CI/CD) pipelines with the ability to roll out releases gradually without any domain name system (DNS) changes. It ensures that your viewer gets a consistent experience through session stickiness by binding the viewer session to the same environment. Additionally, you can compare the performance of your changes by monitoring standard and real-time logs and quickly revert to the previous configuration when a change negatively impacts a service.   

**Q: How can I set up continuous deployment on CloudFront?**

You can set up continuous deployment by associating a staging distribution to a primary distribution through CloudFront console, SDK, Command Line Interface (CLI), or CloudFormation template. You can then define rules to split traffic by configuring the client header or dialing up a percentage of traffic to test with the staging distribution. Once set up, you can update the staging configuration with desired changes. CloudFront will manage the split of traffic to users and provide associated analytics to help you decide whether to continue deployment or rollback. Once testing with staging distributions is validated, you can merge changes to the main distribution.

Please visit the [documentation](https://docs.aws.amazon.com/cloudfront/latest/DeveloperGuide/test-configuration-changes.html) to learn more about the feature.

**Q: How will I measure the results of continuous deployment?**

Continuous deployment allows for real user monitoring through real web traffic. You can use any of the existing available methods of monitoring—CloudFront console, CloudFront API, CLI, or CloudWatch—to individually measure operational metrics of both primary and staging distribution. You can measure the success criteria of your specific application by measuring and comparing throughput, latency, and availability metrics between the two distributions.

**Q: Can I use existing distributions?**

Yes, you can use any existing distributions as a baseline to create a staging distribution and introduce and test changes.

**Q: How does continuous deployment work with CloudFront Functions & Lambda@Edge?**

With continuous deployment, you can associate different functions with the primary and staging distributions. You can also use the same function with both distributions. If you update a function that’s used by both distributions, they both receive the update.  

**Q: How do I use continuous deployment distributions with AWS CloudFormation?**

Each resource in your CloudFormation stack maps to a specific AWS resource. A staging distribution will have its own resource ID and work like any other AWS resource. You can use CloudFormation to create/update that resource.

**Q: How does continuous deployment on CloudFront support session stickiness?**

When you use a weight-based configuration to route traffic to a staging distribution, you can also enable session stickiness, which helps make sure that CloudFront treats requests from the same viewer as a single session. When you enable session stickiness, CloudFront sets a cookie so that all requests from the same viewer in a single session are served by one distribution, either the primary or the staging.

**Q: How much does it cost?**

Continuous deployment feature is available at all CloudFront edge locations at no additional cost.  

## IPv6

**Q. What is IPv6?**

Every server and device connected to the Internet must have a numeric Internet Protocol (IP) address. As the Internet and the number of people using it grows exponentially, so does the need for IP addresses. IPv6 is a new version of the Internet Protocol that uses a larger address space than its predecessor IPv4. Under IPv4, every IP address is 32 bits long, which allows 4.3 billion unique addresses. An example IPv4 address is 192.0.2.1. In comparison, IPv6 addresses are 128 bits, which allow for approximately three hundred and forty trillion, trillion unique IP addresses. An example IPv6 address is: 2001:0db8:85a3:0:0:8a2e:0370:7334

**Q. What can I do with IPv6?**

Using IPv6 support for Amazon CloudFront, your applications can connect to Amazon CloudFront edge locations without needing any IPv6 to IPv4 translation software or systems. You can meet the requirements for IPv6 adoption set by governments - including the [U.S. Federal government](https://www.cio.gov/policies-and-priorities/IPV6/) – and benefit from IPv6 extensibility, simplicity in network management, and additional built-in support for security.

**Q. Should I expect a change in Amazon CloudFront performance when using IPv6?**

No, you will see the same performance when using either IPv4 or IPv6 with Amazon CloudFront.

**Q: Are there any Amazon CloudFront features that will not work with IPv6?**

All existing features of Amazon CloudFront will continue to work on IPv6, though there are two changes you may need for internal IPv6 address processing before you turn on IPv6 for your distributions.

1. If you have turned on the [Amazon CloudFront Access Logs feature](http://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/AccessLogs.html#BasicDistributionFileFormat), you will start seeing your viewer’s IPv6 address in the “c-ip” field and may need to verify that your log processing systems continue to work for IPv6.
2. When you enable IPv6 for your Amazon CloudFront distribution, you will get IPv6 addresses in the ‘[X-Forwarded-For](http://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/RequestAndResponseBehaviorS3Origin.html#RequestS3IPAddresses)’ header that is sent to your origins. If your origin systems are only able to process IPv4 addresses, you may need to verify that your origin systems continue to work for IPv6.  
    

Additionally, if you use IP whitelists for Trusted Signers, you should use an IPv4-only distribution for your Trusted Signer URLs with IP whitelists and an IPv4 / IPv6 distribution for all other content. This model sidesteps an issue that would arise if the signing request arrived over an IPv4 address and was signed as such, only to have the request for the content arrive via a different IPv6 address that is not on the whitelist.

To learn more about IPv6 support in Amazon CloudFront, see “[IPv6 support on Amazon CloudFront](http://docs.aws.amazon.com/console/cloudfront/ipv6)” in the Amazon CloudFront Developer Guide.

**Q: Does that mean if I want to use IPv6 at all I cannot use Trusted Signer URLs with IP whitelist?**

No. If you want to use IPv6 and Trusted Signer URLs with IP whitelist you should use two separate distributions. You should dedicate a distribution exclusively to your Trusted Signer URLs with IP whitelist and disable IPv6 for that distribution. You would then use another distribution for all other content, which will work with both IPv4 and IPv6.

**Q. If I enable IPv6, will the IPv6 address appear in the Access Log?**

Yes, your viewer’s IPv6 addresses will now be shown in the “c-ip” field of the access logs, if you have the Amazon CloudFront Access Logs feature enabled. You may need to verify that your log processing systems continue to work for IPv6 addresses before you turn on IPv6 for your distributions. Please contact Developer Support if you have any issues with IPv6 traffic impacting your tool or software’s ability to handle IPv6 addresses in access logs. For more details, please refer to the [Amazon CloudFront Access Logs](http://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/AccessLogs.html#BasicDistributionFileFormat) documentation.

**Q: Can I disable IPv6 for all my new distributions?**

Yes, for both new and existing distributions, you can use the Amazon CloudFront console or API to enable / disable IPv6 per distribution.

**Q: Are there any reasons why I would want to disable IPv6?**

In discussions with customers, the only common case we heard about was internal IP address processing. When you enable IPv6 for your Amazon CloudFront distribution, in addition to getting an IPv6 address in your detailed access logs, you will get IPv6 addresses in the ‘[X-Forwarded-For](http://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/RequestAndResponseBehaviorS3Origin.html#RequestS3IPAddresses)’ header that is sent to your origins. If your origin systems are only able to process IPv4 addresses, you may need to verify that your origin systems continue to work for IPv6 addresses before you turn on IPv6 for your distributions.

**Q: I enabled IPv6 for my distribution but a DNS lookup doesn’t return any IPv6 addresses. What is happening?**

Amazon CloudFront has very diverse connectivity around the globe, but there are still certain networks that do not have ubiquitous IPv6 connectivity. While the long term future of the Internet is obviously IPv6, for the foreseeable future every endpoint on the Internet will have IPv4 connectivity. When we find parts of the Internet that have better IPv4 connectivity than IPv6, we will prefer the former.

**Q: If I use Route 53 to handle my DNS needs and I created an alias record pointing to an Amazon CloudFront distribution, do I need to update my alias records to enable IPv6?**

Yes, you can create Route 53 alias records pointing to your Amazon CloudFront distribution to support both IPv4 and IPv6 by using “A” and “AAAA” record type respectively. If you want to enable IPv4 only, you need only one alias record with type “A”. For details on alias resource record sets, please refer to the [Amazon Route 53 Developer Guide](http://docs.aws.amazon.com/Route53/latest/DeveloperGuide/resource-record-sets-choosing-alias-non-alias.html?shortFooter=true).  
![[Pasted image 20240211002620.png]]
## Billing

**Q: What usage types are covered in the AWS free tier for Amazon CloudFront?**

Starting Dec 1 2021, all AWS customers will receive 1 TB of data transfer out, 10,000,000 HTTP/HTTPS requests, plus 2,000,000 CloudFront Functions invocations each month for free. All other usage types (eg. Invalidations, Proxy requests, Lambda@edge, Origin shield, Data Transfer to Origin etc.) are excluded from the free tier.  

**Q: If we sign-up for Consolidated Billing, can we get the AWS Free Tier for each account?**

No, customers that use Consolidated Billing to consolidate payment across multiple accounts will only have access to one Free Tier per Organization.

**Q: What happens if my usage is in multiple regions, and I exceed the free tiers?**

The 1 TB data transfer and 10 million Get requests are monthly free tier limits across all Edge locations. If your usage exceeds the monthly free tier limits, you simply pay standard, On-Demand AWS service rates for each region. See the AWS [CloudFront Pricing page](https://aws.amazon.com/cloudfront/pricing/) for full pricing details.  

**Q: How do I know how much I’ve used and if I’ve gone over the free usage tiers?**

You can see current and past usage activity by region by logging into your account and going to the Billing & Cost Management Dashboard. From there you can manage your costs and usage using [AWS Budgets](https://console.aws.amazon.com/billing/home?#/budgets), visualize your cost drivers and usage trends via [Cost Explorer](https://console.aws.amazon.com/billing/home?#/costexplorer), and dive deeper into your costs using the [Cost and Usage Reports.](https://console.aws.amazon.com/billing/home?#/reports) To learn more about how to control your AWS costs, check out the Control your AWS costs 10-Minute Tutorial.

**Q: Does the free tier apply to customers subscribed to CloudFront Security Savings bundle?**

Customers subscribed to CloudFront Security Savings bundle will also benefit from the free tier. If you feel the need to lower your commitment to the CloudFront Security Savings bundle in light of the free tier, please reach out to customer service and we will evaluate your request for changes. We will provide more details about this in the coming days. Please stay tuned. 

For additional questions, please refer to [https://aws.amazon.com/free/free-tier-faqs/](https://aws.amazon.com/free/free-tier-faqs/).  

**Q. How will I be charged for my use of Amazon CloudFront?**

Amazon CloudFront charges are based on actual usage of the service in five areas: Data Transfer Out, HTTP/HTTPS Requests, Invalidation Requests, Real-time Log Requests, and Dedicated IP Custom SSL certificates associated with a CloudFront distribution.

With the [AWS Free Usage Tier](https://aws.amazon.com/free/), you can get started with Amazon CloudFront for free and keep your rates down as you grow your usage. All CloudFront customers receive 1 TB data transfer out and 10,000,000 HTTP and HTTPS Requests for Amazon CloudFront free of charge, even when these limits are exceeded. If 

- **Data Transfer Out to Internet**  
    You are charged for the volume of data transferred out from Amazon CloudFront edge locations, measured in GB. You can see the rates for Amazon CloudFront data transfer to the internet here. Note that your data transfer usage is totaled separately for specific geographic regions, and then cost is calculated based on pricing tiers for each area. If you use other AWS services as the origins of your files, you are charged separately for your use of those services, including for storage and compute hours. If you use an AWS origin (such as Amazon S3, Amazon EC2, and so on), effective December 1, 2014, **we do not charge for AWS data transfer out to Amazon CloudFront**. This applies to data transfer from all AWS Regions to all global CloudFront edge locations.
- **Data Transfer Out to Origin**  
    You will be charged for the volume of data transferred out, measured in GB, from the Amazon CloudFront edge locations to your origin (both AWS origins and other origin servers). You can see the rates for Amazon CloudFront data transfer to Origin [here](https://aws.amazon.com/cloudfront/pricing/).
- **HTTP/HTTPS Requests**  
    You will be charged for number of HTTP/HTTPS requests made to Amazon CloudFront for your content. You can see the rates for HTTP/HTTPS requests [here](https://aws.amazon.com/cloudfront/pricing/).
- **Invalidation Requests**  
    You are charged per path in your invalidation request. A path listed in your invalidation request represents the URL (or multiple URLs if the path contains a wildcard character) of the object you want to invalidate from CloudFront cache. You can request up to 1,000 paths each month from Amazon CloudFront at no additional charge. Beyond the first 1,000 paths, you will be charged per path listed in your invalidation requests. You can see the rates for invalidation requests [here](https://aws.amazon.com/cloudfront/pricing/).
- **Real-time log Requests**  
    Real-time logs are charged based on the number of log lines that are generated; you pay $0.01 for every 1,000,000 log lines that CloudFront publishes to your log destination.  
    
- **Dedicated IP Custom SSL**  
    You pay $600 per month for each custom SSL certificate associated with one or more CloudFront distributions using the Dedicated IP version of custom SSL certificate support. This monthly fee is pro-rated by the hour. For example, if you had your custom SSL certificate associated with at least one CloudFront distribution for just 24 hours (i.e. 1 day) in the month of June, your total charge for using the custom SSL certificate feature in June will be (1 day / 30 days) \* $600 = $20. To use Dedicated IP Custom SSL certificate support, upload a SSL certificate and use the AWS Management Console to associate it with your CloudFront distributions. If you need to associate more than two custom SSL certificates with your CloudFront distribution, please include details about your use case and the number of custom SSL certificates you intend to use in the [CloudFront Limit Increase Form](https://aws.amazon.com/support/createCase?type=service_limit_increase&serviceLimitIncreaseType=cloudfront-distributions).  
    

Usage tiers for data transfer are measured separately for each geographic region. The prices above are exclusive of applicable taxes, fees, or similar governmental charges, if any exist, except as otherwise noted.  

**Q: Does your prices include taxes?**

Except as otherwise noted, our prices are exclusive of applicable taxes and duties, including VAT and applicable sales tax. For customers with a Japanese billing address, use of AWS services is subject to Japanese Consumption Tax. [Learn more](https://aws.amazon.com/jp/c-tax-faqs/).

**Q: How much will the real-time logs cost me?**  
If you have a distribution serving 1,000 requests per second with a log size of 1KB and create a Kinesis Data Stream in US East (Ohio) with 2 shards:

Monthly cost of Kinesis Data Stream: $47.74/month as calculated using the Kinesis calculator [here](https://aws.amazon.com/kinesis/data-streams/pricing/).

Monthly cost of CloudFront real-time logs: Requests per month X cost of real-time logs = 1,000 \* (60 sec \* 60 min \*24 hrs \* 30 days) X ($0.01 /1,000,000) = $25.92 /month

**Q: How am I charged for 304 responses?**

A 304 is a response to a conditional GET request and will result in a charge for the HTTP/HTTPS request and the Data Transfer Out to Internet. A 304 response does not contain a message-body; however, the HTTP headers will consume some bandwidth for which you would be charged standard CloudFront data transfer fees. The amount of data transfer depends on the headers associated with your object.

**Q. Can I choose to only serve content from less expensive Amazon CloudFront regions?**

Yes, "Price Classes" provides you an option to lower the prices you pay to deliver content out of Amazon CloudFront. By default, Amazon CloudFront minimizes end user latency by delivering content from its entire global network of edge locations. However, because we charge more where our costs are higher, this means that you pay more to deliver your content with low latency to end-users in some locations. Price Classes let you reduce your delivery prices by excluding Amazon CloudFront’s more expensive edge locations from your Amazon CloudFront distribution. In these cases, Amazon CloudFront will deliver your content from edge locations within the locations in the price class you selected and charge you the data transfer and request pricing from the actual location where the content was delivered.

If performance is most important to you, you don’t need to do anything; your content will be delivered by our whole network of locations. However, if you wish to use another Price Class, you can configure your distribution through the AWS Management Console or via the Amazon CloudFront API. If you select a price class that does not include all locations, some of your viewers, especially those in geographic locations that are not in your price class, may experience higher latency than if your content were being served from all Amazon CloudFront locations.

Note that Amazon CloudFront may still occasionally serve requests for your content from an edge location in a location that is not included in your price class. When this occurs, you will only be charged the rates for the least expensive location in your price class.

You can see the list of locations making up each price class [here](https://aws.amazon.com/cloudfront/pricing/).  

## CloudFront Security Savings Bundle

**Q. What is the CloudFront Security Savings Bundle?**

The CloudFront Security Savings Bundle is a flexible self-service pricing plan that helps you save up to 30% on your CloudFront bill in exchange for making a commitment to a consistent amount of monthly usage (e.g. $100/month) for a 1 year term.  As an added benefit, AWS WAF (Web Application Firewall) usage, up to 10% of your committed plan amount, to protect CloudFront resources is included at no additional charge.  For example, making a commitment of $100 of CloudFront usage per month would cover a $142.86 worth of CloudFront usage for a 30% savings compared to standard rates. Additionally, up to $10 of AWS WAF usage is included to protect your CloudFront resources at no additional charge each month  (up to 10% of your CloudFront commitment).  Standard CloudFront and AWS WAF charges apply to any usage above what is covered by your monthly spend commitment.  As your usage grows, you can buy additional savings bundles to obtain discounts on incremental usage. 

**Q: What types of usage are covered by a CloudFront Security Savings Bundle?**

By purchasing a CloudFront Security Savings Bundle, you receive a 30% savings that will appear on the CloudFront service portion of your monthly bill that will offset any CloudFront billed usage types including data transfer out, data transfer to origin, HTTP/S request fees, field level encryption requests, Origin Shield, invalidations, dedicated IP custom SSL, and Lambda@Edge charges.  You will also receive with additional benefits that help cover AWS WAF usage associated with your CloudFront distributions.   

**Q: How do I get started with a CloudFront Security Savings Bundle?**  
You can get started with the CloudFront Security Savings Bundle by visiting the [CloudFront console](https://console.aws.amazon.com/cloudfront/v2/home#/savings-bundle/overview) to  get recommendations on commitment amount based on your historical CloudFront and AWS WAF usage or by entering in your own estimated monthly usage. You get a comparison between CloudFront Security Savings Bundle monthly costs to on-demand costs and see estimated savings to help decide on the right plan for your needs.  Once you sign up for a Savings Bundle, you will be charged your monthly commitment and see credits appear that offset your CloudFront and WAF usage charges.  Standard service charges apply to any usage above what is covered by your monthly spend commitment.   

**Q: What happens when my CloudFront Security Savings Bundle  expires after the 1-year term?**

Once your CloudFront Security Savings Bundle term expires, standard service charges will apply for your CloudFront and AWS WAF usage.   The monthly Savings Bundle commit will no longer be billed and savings bundle benefits will no longer apply.  Any time prior to expiration of your bundle term, you can choose to opt-in to automatically renew the CloudFront Security Savings Bundle for another 1 year term.  

**Q. How does CloudFront Security Savings Bundle work with AWS Organizations/ Consolidated Billing?**

CloudFront Security Savings Bundle can be purchased in any account within an AWS Organization/Consolidated Billing family.   CloudFront Security Savings Bundle benefits are applied as credits on your bill. The benefits provided by the Savings Bundle is applicable to usage across all accounts within an AWS Organization/consolidated billing family by default (credit sharing is turned on) and is dependent on when the subscribing account joins or leaves an organization.  See [AWS Credits](https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/useconsolidatedbilling-credits.html) to learn more how AWS credits apply across single and multiple accounts.  

**Q: Can I have multiple CloudFront Security Savings Bundles active at the same time?**

Yes, you may purchase additional CloudFront Security Savings Bundles as your usage grows to get discounts on the incremental usage.   All active CloudFront Security Savings Bundles will be taken into account when calculating your AWS bill.

**Q: How will the CloudFront Security Savings Bundle show up on my bill?**

Your monthly commitment charges will appear under a separate CloudFront Security Bundle section on your bill.  Usage covered by your CloudFront Security Bundle savings will appear under both CloudFront and WAF portions of your bill as credits to offset your standard usage charges.  

**Q: Can I be notified if my usage exceeds my CloudFront Security Savings Bundle monthly commitment?**

Yes, AWS Budgets allows you to set cost and usage thresholds and get notifications by email or Amazon SNS topic when your actual or forecasted charges exceed the threshold.  You can create a custom AWS Budget filtered for the CloudFront Service and set the budget threshold amount to the CloudFront on-demand usage covered by your CloudFront Security Savings Bundle to be notified once that threshold has been exceeded.   For more information about budgets, see [Managing your costs with AWS Budgets](https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/budgets-managing-costs.html) and [Creating a budget](https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/budgets-create.html) in the AWS Billing and Cost Management User Guide. 

**Q: What portion of my WAF bill is covered by the CloudFront Security Savings Bundle?**

As an added benefit of the CloudFront Security Savings Bundle, AWS WAF usage, up to 10% of your committed plan amount, to protect CloudFront resources is included at no additional charge. Standard CloudFront and AWS WAF charges apply for any usage beyond what is covered by CloudFront Security Savings Bundle.  Managed WAF rules subscribed through the AWS Marketplace are not covered by the CloudFront Security Savings Bundle. 

**Q: What if I already have a custom pricing agreement for CloudFront, can I subscribe to the CloudFront Security Savings Bundle too?**

You may only be subscribed to one or the other.  Please contact your AWS Account Manager if you have questions about your custom pricing agreement.

**Q: Can I subscribe to a CloudFront Security Savings Bundle via API?**

You can subscribe to the CloudFront Security Savings Bundle only through the [CloudFront console.](https://console.aws.amazon.com/cloudfront/v2/home#/savings-bundle/overview)  We will evaluate making it available via API as a future enhancement.

