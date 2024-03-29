---
tags:
  - cloud/aws
---


# FAQ
## General

**Q: Who are the primary users of AWS Data Exchange?**

AWS Data Exchange makes it easy for AWS customers to securely exchange and use third-party data on AWS. Data analysts, product managers, portfolio managers, data scientists, quants, clinical trial technicians, and developers in nearly every industry would like access to more data to drive analytics, train machine learning (ML) models, and make data-driven decisions. But there is no one place to find data from multiple providers and no consistency in how providers deliver data, leaving them to deal with a mix of shipped physical media, FTP credentials, and bespoke API calls. Conversely, many organizations would like to make their data available for either research or commercial purposes, but it’s too hard and expensive to build and maintain data delivery, entitlement, and billing technology, which further depresses the supply of valuable data.

****Q:** What AWS Regions is AWS Data Exchange available in?**

AWS Data Exchange has a single global product catalog oﬀered by providers available from any supported AWS Region. You can see the same catalog regardless of which Region you are using. The resources underlying the product (data sets, revisions, assets) are regional resources that you manage programmatically or through the AWS Data Exchange console in speciﬁc AWS Regions. For a list of AWS Regions in which AWS Data Exchange is available today, see [Service endpoints](https://docs.aws.amazon.com/general/latest/gr/dataexchange.html#dataexchange_region).  

****Q:** What is the difference between AWS Data Exchange and the Registry of Open Data on AWS?**

All publicly available data sets on the [Registry of Open Data](https://registry.opendata.aws/) on AWS are also available through [AWS Data Exchange](https://aws.amazon.com/marketplace/search/results?FULFILLMENT_OPTION_TYPE=DATA_EXCHANGE&CONTRACT_TYPE=OPEN_DATA_LICENSES&filters=FULFILLMENT_OPTION_TYPE%2CCONTRACT_TYPE). On AWS Data Exchange, customers can now discover and access more than 100 petabytes of high-value, cloud-optimized data sets available for public use from leading organizations such as NOAA, NASA, or the UK Met Office. These include open data sets hosted by the [AWS Open Data Sponsorship Program](https://aws.amazon.com/opendata) and in the [Amazon Sustainability Data Initiative](https://sustainability.aboutamazon.com/environment/the-cloud/asdi) (ASDI) catalog. Open data sets are different than other commercial or free data sets in four key ways. First, AWS Data Exchange requires customers to explicitly agree to the Data Subscription Agreement outlining the terms that the data provider set when publishing their product, whereas open data does not have terms of use and is only governed by the provider specific open data license. Second, customers must authenticate using an AWS account to subscribe to commercial or free data sets whereas open data sets can be accessed without any authentication via S3 APIs. Third, AWS Data Exchange gives data providers access to daily, weekly and monthly reports detailing subscription activity, whereas with Registry of Open Data on AWS, data providers must analyze their own logs to track usage of data. Finally, to become a data provider on AWS Data Exchange, qualified customers must [register as a data provider](https://aws.amazon.com/marketplace/management/tour/) on the AWS Marketplace Management Portal to be eligible to list both free and commercial products, whereas any customer can add free data to [Registry of Open Data on AWS through GitHub](https://github.com/awslabs/open-data-registry/) and may apply to the Open Data Sponsorship Program for AWS to sponsor the costs of storage and bandwidth for select open data sets.

**Q: What is AWS Data Exchange for APIs?**

AWS Data Exchange for APIs is a feature that enables customers to find, subscribe to, and use third-party API products from providers on AWS Data Exchange. With AWS Data Exchange for APIs, customers can use AWS-native authentication and governance, explore consistent API documentation, and utilize supported AWS SDKs to make API calls. Now, by adding their APIs to the AWS Data Exchange catalog, data providers can reach millions of AWS customers that consume API-based data and more easily manage subscriber authentication, entitlement, and billing.  

## Subscriber

****Q:** What type of data can I subscribe to on AWS Data Exchange?**

Today, AWS Data Exchange contains more than 3,500 data products from a broad range of domains, including financial services (for example, top US businesses by revenue); healthcare and life sciences (for example, population health management); geospatial (for example, satellite imagery); weather (for example, historical and future trajectories of temperature); and mapping (for example, street level imagery and foot traffic patterns). For a complete list of data providers, navigate to [the AWS Data Exchange catalog](https://console.aws.amazon.com/dataexchange/home?region=us-east-1#/products). If customers need additional data sources not currently available on AWS Data Exchange, they can [log these requests](https://console.aws.amazon.com/dataexchange/home?region=us-east-1#/products/product-request) here.

****Q:** How can I see the catalog of AWS Data Exchange products?**

Anyone can browse the AWS Data Exchange catalog in [AWS Marketplace](https://aws.amazon.com/marketplace/b/2649387011?ref_=header_nav_category_2649387011) under the Data category, or by searching AWS Marketplace for keywords of interest. Authenticated AWS customers can also browse the AWS Data Exchange catalog alongside existing subscriptions on the AWS Data Exchange console. For more information about subscribing to data products, see [Getting started as a subscriber](https://docs.aws.amazon.com/data-exchange/latest/userguide/subscribe-to-data-sets.html#subscriber-getting-started).

****Q:** How will I know when new revisions to data sets I’m subscribed to become available?**

As a subscriber with an active subscription to a product, you'll receive an Amazon CloudWatch Events event from AWS Data Exchange every time the provider publishes new revisions. You can use this CloudWatch event to automate consumption of new data. For more information about CloudWatch Events, see [Logging and monitoring on AWS Data Exchange](https://docs.aws.amazon.com/data-exchange/latest/userguide/logging-and-monitoring.html).

****Q:** Can I migrate preexisting data subscriptions to be delivered by AWS Data Exchange?**

Yes. AWS Data Exchange allows qualified data providers to fulfill to existing subscribers using a Bring Your Own Subscription (BYOS) entitlement at no additional cost. With a BYOS offer, the existing billing relationship will continue between you and the data provider. Talk to your data provider about using this capability.

****Q:** What are the subscription durations that are available for AWS Data Exchange products?**

Data providers list products subscriptions with 1to 36-month duration terms. You can find subscription duration options on each product’s detail page.

****Q:** Can I set my subscription to auto-renew?**

Providers have the option to enable auto-renewal on individual offers. As a subscriber, you can choose to set your subscription to auto-renew on the offers that have the auto-renewal functionality enabled. Auto-renewal is available for public and private offers that do not have payment schedules.  

****Q:** Can data providers change the terms of the offer that I am subscribed to? How would it affect my subscription and renewal?**

Yes. Data providers can update the terms of the offer at any time, but this will not affect existing subscriptions. For subscriptions set to auto-renew, AWS Data Exchange will automatically renew the subscription at the latest terms that the provider specified on or by renewal date, **which may be different from the original subscription terms**. For more information, see [Product subscriptions](https://docs.aws.amazon.com/data-exchange/latest/userguide/product-subscriptions.html).

****Q:** How are refunds handled?** 

AWS Data Exchange requires data providers to specify their refund policy, which you can see on the subscription details page. For any refund requests, you'll need to contact the provider directly. After a provider approves a refund request, AWS will process and issue the approved refund.

****Q:** How do I remain compliant with applicable data privacy laws when subscribing to AWS Data Exchange products?**

Security and Compliance is a [shared responsibility](https://aws.amazon.com/compliance/shared-responsibility-model/) among AWS, the data provider, and the subscriber. Detailed restrictions around eligible data sets and other related legal compliance matters are set forth in [Terms and Conditions for AWS Marketplace Providers](https://aws.amazon.com/marketplace/management/terms), which every data provider must agree to before listing any data products. If AWS learns that these terms are breached in any way, AWS will remove such content from AWS Data Exchange and the data provider may be suspended from the service.

Providers and subscribers are responsible for conducting their own additional due-diligence to ensure compliance with any data privacy laws. If you suspect that a data product or AWS Data Exchange resources are being used for abusive or illegal purposes, you can complete and submit the form found on [Report Amazon AWS abuse](https://support.aws.amazon.com/#/contacts/report-abuse).

****Q:** Are there are any restrictions for how AWS Data Exchange and any data obtained through AWS Data Exchange can be used?**

Yes, AWS explicitly prohibits the use of AWS Data Exchange for any illegal or fraudulent activities. Data may not be used for any activities that result in the violation of an individual’s rights or unlawfully discriminate against others based on race, ethnicity, sexual orientation, gender identity, or other related groups. Subscribers may not use any content obtained through AWS Data Exchange that was anonymized or aggregated (such that it is no longer associated with an identifiable individual) by the data provider to create, generate, or infer any information relating to a person’s identity (for example, attempting to triangulate with other data sources).

****Q:** How do I report abusive content or request information be removed from a product suspected of abuse?**

If you suspect that a data product or AWS Data Exchange resources are being used for abusive or illegal purposes, you can complete and submit the form found on [Report Amazon AWS abuse](https://support.aws.amazon.com/#/contacts/report-abuse). If AWS learns that our terms are breached in any way, AWS may remove the subscriber’s access to the data product and the data provider or the subscriber may be suspended or terminated from future use of AWS Data Exchange

****Q:** I currently consume third-party data directly into my S3 bucket(s). Why should I consider using AWS Data Exchange to consume data from third parties instead?** 

AWS Data Exchange centralizes, simplifies, and accelerates your data acquisition process.

AWS Data Exchange allows you to consolidate your ingestion across data providers and receive your data using a single API. You can easily subscribe to new data products, and migrate any existing data feeds through the Bring Your Own Subscription feature.

AWS Data Exchange sends you a CloudWatch Events event as new data is published, allowing you to automate ingestion without having to manage any physical media, FTP credentials, or other legacy technology. It also stores copies of data you've licensed, allowing you to access point-in-time history all in one secure location.  

AWS Data Exchange also centralizes your billing so you can receive one invoice from AWS instead of one for each data provider. With the AWS Data Exchange console, you can easily track your subscriptions in one place, and better manage your data pipeline.  

****Q:** How do I pay for my data product subscriptions?**

When you purchase a data product on AWS Data Exchange with upfront payments, you'll receive an invoice from AWS immediately. When you purchase a data product on AWS Data Exchange with multiple payments, you'll receive an invoice based on the dates specified in the [payment schedule](https://docs.aws.amazon.com/data-exchange/latest/userguide/product-subscriptions.html) that will appear as part of your AWS Marketplace charges. You can see a breakout of charges for each data product by name in the Detail section of the invoice. You'll receive separate bills for usage of AWS infrastructure and analytics services such as Amazon Simple Storage Service (Amazon S3) or Amazon Athena. For more information related to AWS Billing and Cost Management, see [Paying for products](https://docs.aws.amazon.com/marketplace/latest/buyerguide/buyer-paying-for-products.html).

**Q: How do I find API products in the AWS Data Exchange catalog?**

You can find products containing APIs in the [AWS Marketplace catalog](https://aws.amazon.com/marketplace/search/results?FULFILLMENT_OPTION_TYPE=DATA_EXCHANGE&DATA_AVAILABLE_THROUGH=API_GATEWAY_APIS&filters=FULFILLMENT_OPTION_TYPE%2CDATA_AVAILABLE_THROUGH), or you can navigate to the [AWS Data Exchange catalog](https://console.aws.amazon.com/dataexchange/home?region=us-east-1#/products) and select **_API_** under the _**Data available through**_ filter.  

**Q: How do I subscribe to an API product?**

After you’ve found the API that you want to subscribe to, select the product to learn more on the product detail page. Next, choose _**Continue to subscribe**_, review the subscription terms, and then choose the **_Subscribe_** button at the bottom of the page.  
  
**Note:** You may be asked to submit information to the data provider before you can request to subscribe to their product. For more information on subscribing and using an API product, see the [Subscribing to a product containing APIs](https://docs.aws.amazon.com/data-exchange/latest/userguide/subscribing-to-product.html#subscribing-to-API-product.html) topic in the _AWS Data Exchange User Guide_.  

**Q: How do I make an API call?**

First, ensure you have successfully subscribed to a product containing an API data set. Then, navigate to the product’s asset detail page to view API schemas and code snippets that will help you structure your API call. You can also utilize the AWS SDK to automatically sign your API requests with your AWS credentials. For more information about how to structure API calls to AWS Data Exchange products containing API data sets, see the [Making an API call (console)](https://docs.aws.amazon.com/data-exchange/latest/userguide/subscribing-to-product.html#make-api-call-console) in the _AWS Data Exchange User Guide._  

**Q: Does AWS Data Exchange for APIs have a Service Level Agreement (SLA)?**

AWS Data Exchange for APIs does not currently offer an SLA.  

**Q: Are there any AWS Data Exchange for APIs-specific SDKs that I should be aware of?**  

We have added AWS Data Exchange for APIs-specific operations to the following SDKs:

- [AWS SDK for Go](https://aws.amazon.com/sdk-for-go/) 
- [AWS SDK for JavaScript](https://aws.amazon.com/sdk-for-javascript/) 
- [AWS SDK for Node.js](https://docs.aws.amazon.com/sdk-for-javascript/v3/developer-guide/getting-started-nodejs.html) 
- [AWS SDK for PHP](https://aws.amazon.com/sdk-for-php/) 
- [AWS SDK for Python](https://aws.amazon.com/sdk-for-python/) 
- [AWS SDK for Ruby](https://aws.amazon.com/sdk-for-ruby/)  
    

For more information, see the [AWS Data Exchange API Reference](https://docs.aws.amazon.com/data-exchange/latest/apireference/aws-data-exchange-api-reference.pdf).

## Provider

****Q:** How do I qualify to become a data provider on AWS Data Exchange?**

To become a data provider on AWS Data Exchange, data providers must agree to the [Terms and Conditions for AWS Marketplace Providers](https://aws.amazon.com/marketplace/management/terms) (“AWS Marketplace Terms & Conditions”). Data providers must use a valid legal entity domiciled in the United States or a member state of the EU, supply valid banking and taxation identification, and be qualified by the AWS Data Exchange business operations team. Each data provider will also undergo a detailed review by the AWS Data Exchange team prior to being granted permission to list data products on the catalog.

****Q:** How is data organized in AWS Data Exchange?**

Data in AWS Data Exchange is organized using three building blocks: data sets, revisions, and assets. A data set is a container for data that belongs together (for example, end of data pricing for equities trading in the US). Data sets contain a series of revisions, which data providers publish as needed to make new assets available. Revisions can represent changes or new data (for example, today’s end of day prices), corrections to previous revisions, or entirely new snapshots. Assets are any file that can be stored in Amazon Simple Storage Service (S3) (for example, CSV, Parquet, or image files). For more information about working with data, see [Data in AWS Data Exchange](https://docs.aws.amazon.com/data-exchange/latest/userguide/data-sets.html). Using these building blocks, you can organize the data hierarchically to build complex data models or as single data files.

****Q:** After I create data sets, how do I publish and make them available to my subscribers?**

Data sets are made available to subscribers as part of a product. A product is a collection of one or more data sets, metadata that makes the product discoverable in the AWS Data Exchange catalog, pricing, and a Data Subscription Agreement with terms for your customers. For more information, see [Publishing a new product](https://docs.aws.amazon.com/data-exchange/latest/userguide/publishing-products.html).

****Q:** Can I choose which customers can subscribe to my data?**

Yes. You have an option to enable subscription verification on any public product, which will require prospective subscribers to fill out a subscription request form including their identity and intended use-case details before subscribing. For these products, you'll have up to 45 days to either approve or decline the subscription request. Note that public products that include personal data are required to have subscription verification enabled. For more information, see [Subscription verification for providers](https://docs.aws.amazon.com/data-exchange/latest/userguide/subscription-verification-pro.html).

You can also offer private products to specific subscribers by using their AWS Account ID. Private products can be custom-made from existing products on the public catalog or completely new products only offered to the specific customers of your choosing and not listed on the public catalog.  

****Q:** Do I have to package files in a specific format?**

AWS Data Exchange allows you to package files in any file format, but you’ll want to consider what will allow subscribers to most conveniently gain insight from the data. Parquet formatted files, for example, will allow subscribers to instantly run queries using Amazon Athena in a cost-effective way. Binary or other proprietary file formats will require that subscribers understand how to parse the information, which AWS recommends explaining in each product description.

****Q:** Who owns the data I am distributing as a provider through AWS Data Exchange?**

You retain ownership of the data you distribute as a data provider on AWS Data Exchange. The [Terms and Conditions for AWS Marketplace Providers](https://aws.amazon.com/marketplace/management/seller-settings/terms) require each data provider to attest that they have the legal right to distribute the data they publish. Subscribers must legally agree to the Data Subscription Agreement specified by the data provider before gaining access to data sets contained in a product, which remains available for both data providers and subscribers. Consistent with the AWS acceptable use policy, AWS Data Exchange may suggest corrective action where there is evidence of abuse, but it is the data provider’s responsibility to enforce and govern the terms of use.

****Q:** How do I specify the Data Subscription Agreement (DSA)?**  

AWS Data Exchange provides an optional Data Subscription Agreement (DSA) template that incorporates inputs from multiple AWS customers and data providers. You can choose to use this DSA template, copy and edit it with their own terms and conditions, or specify custom terms by uploading a DSA of your choice. AWS Data Exchange will associate the DSA specified for the product without any further modifications. For more information, see [Publishing a new product](https://docs.aws.amazon.com/data-exchange/latest/userguide/publishing-products.html).

****Q:** What ways can I price my data sets?**

AWS Data Exchange currently supports subscription-based pricing from 1to 36-month duration terms.

****Q:** Is AWS Data Exchange suitable for data providers who want to distribute their data for free?**

Yes. Many data providers make their data products available for free for research, scientific, or other noncommercial use cases.

****Q:** Can I customize pricing or terms for select customers?**

Yes. Private offers allow you to make public products available to select AWS customers and to set terms including price, duration, payment schedule, DSA, or refund policy. For more information, see [Create private offers](https://docs.aws.amazon.com/data-exchange/latest/userguide/private-offer-configuration.html).  

****Q:** Are there any restrictions on what data can be made available on AWS Data Exchange?**

Yes. [Publishing guidelines](https://docs.aws.amazon.com/data-exchange/latest/userguide/publishing-guidelines.html) for listing products on AWS Data Exchange and [Terms and Conditions for AWS Marketplace Providers](https://aws.amazon.com/marketplace/management/terms) restrict certain categories of data. Unless a provider is enrolled in the Extended Provider Program, data products listed on AWS Data Exchange may not include information that can be used to identify any person, except information that is already legally available to the public, such as newspaper articles, open court records, public company filings, or public online profiles. For more information about the Extended Provider Program, please [contact AWS Support](https://console.aws.amazon.com/support/home#/case/create?issueType=customer-service).

****Q:** Can I remove a product that I published from the catalog?**

Yes. You can unpublish a product at any time to ensure that no new subscribers are able to view and subscribe to your product, including auto-renewal cancellation for existing subscribers. You'll need to keep data current for any existing subscribers until each subscription expires.

****Q:** What happens if I need to remove data from AWS Data Exchange?**  

You can remove or change the price or Data Subscription Agreement (DSA) of a product at any time, although existing subscriptions will remain in effect until their next renewal. If a data provider erroneously publishes data, you can open a support case [open a support case](https://console.aws.amazon.com/support/cases#/create?issueType=customer-service) to have the data unpublished.

****Q:** How do I know who is subscribing to the data I have listed on AWS Data Exchange?**

AWS Data Exchange provides daily, weekly, and monthly reports detailing subscription activity.

****Q:** When and how often will I receive payments?**

You will receive a disbursement for subscriptions less fulfillment fees once a month. AWS will disburse all funds that AWS has received from subscribers by that date to the bank account linked to the AWS account that you used at registration.

****Q:** How will AWS handle collection and remittances of US sales and use tax?**

When listing your data sets, you can enable collection and remittance of US sales and use tax. You can also configure your tax nexus to account for places where you have a physical presence to direct AWS to collect appropriate taxes. It's helpful to review the [AWS Marketplace U.S Tax Collection Support Terms and Conditions](https://s3.amazonaws.com/aws-mp-seller-tax-terms/AWS_Marketplace_Tax_Support_Terms_and_Conditions.pdf). For details on sales tax collection in other geographies, see [AWS Marketplace Sellers & Tax Collection](https://aws.amazon.com/tax-help/marketplace/).

****Q:** Is Amazon.com or AWS providing customers’ data on AWS Data Exchange?**

No. Neither Amazon.com nor AWS are providing customers’ data on AWS Data Exchange.

****Q:** Can AWS access data products listed on AWS Data Exchange?**

AWS is vigilant about our customers’ privacy. Companies listing data products on the AWS Data Exchange own them and are able to maintain control over who accesses their content. AWS does not access or use data products except as necessary to provide the AWS Data Exchange service.

****Q:** I currently publish data directly into my subscribers' S3 buckets. Why should I consider using AWS Data Exchange to publish data to third parties instead?**

With AWS Data Exchange you can publish data simultaneously to all your customers and spend more time growing your business rather than managing logistics.

AWS Data Exchange allows you to publish data to your customers through an easy-to-use API and console. The data model for AWS Data Exchange simplifies managing and publishing data through three reusable constructs: data sets, revisions, and assets. AWS customers can subscribe to these published data products directly from AWS Marketplace. The service automatically grants entitlements to customers who have an active subscription to the product, which means that you don’t have to manually configure and maintain custom permissions to an Amazon Simple Storage Service (S3) bucket for each subscription.  
  
AWS Data Exchange automatically sends an Amazon CloudWatch Events event to all subscribers when new revisions are published, which allows subscribers to automate their consumption of new data. When a subscription is no-longer active, AWS Data Exchange revokes that subscriber's entitlement to your data.  
  
If your product is already available on AWS Data Exchange, you can simply use Bring Your Own Subscription (BYOS) to configure an entitlement to your existing subscribers for no additional cost and without any additional programming work. For more information about using BYOS to migrate and fulfill existing subscriptions with AWS customers, see [Create Bring Your Own Subscription offers](https://docs.aws.amazon.com/data-exchange/latest/userguide/create-byos-offers.html).  

**Q: How do I publish a product containing APIs?**

As a provider, you first need to set up an AWS account and [register as an AWS Marketplace seller](https://docs.aws.amazon.com/marketplace/latest/userguide/seller-registration-process.html). You can then publish an API product by following the steps detailed in the [Publishing a product containing APIs](https://docs.aws.amazon.com/data-exchange/latest/userguide/publishing-products.html#publish-API-product) topic in the _AWS Data Exchange User Guide_.  

**Q: Do providers have to offer a Service Level Agreement (SLA) to AWS Data Exchange when offering an API product?**

AWS Data Exchange for APIs does not require providers to offer an uptime or availability SLA. Providers and subscribers can negotiate custom terms as part of a DSA. See [Publishing Products](https://docs.aws.amazon.com/data-exchange/latest/userguide/publishing-products.html) for further information.  

**Q: What guidelines do I need to follow as a provider on AWS Data Exchange for APIs?**

In addition to following guidelines under the [Terms and Conditions for AWS Marketplace Sellers](http://aws.amazon.com/marketplace/management/seller-settings/terms) and the [AWS Customer Agreement](https://aws.amazon.com/agreement/), providers of products containing APIs must respond to subscriber support inquiries within 1 business day, as set forth in the _AWS Data Exchange User Guide_. Not following the guidelines may result in products being removed from AWS Data Exchange. For more information, see [Publishing guidelines](https://docs.aws.amazon.com/data-exchange/latest/userguide/publishing-guidelines.html) topic in the _AWS Data Exchange User Guide_.  

**Q: Can products contain APIs, Amazon S3 objects, and Amazon Redshift data shares?**

Yes. As a data provider, you can publish products containing multiple data set types.