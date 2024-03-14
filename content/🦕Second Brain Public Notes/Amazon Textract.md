---
tags:
  - cloud/aws
---



![](https://i.imgur.com/reR29vY.png)

# FAQ
## General

**Q: What is Amazon Textract?**

Amazon Textract is a document analysis service that detects and extracts printed text, handwriting, structured data (such as fields of interest and their values) and tables from images and scans of documents. Amazon Textract's machine learning models have been trained on millions of documents so that virtually any document type you upload is automatically recognized and processed for text extraction. When information is extracted from documents, the service returns a confidence score for each element it identifies so that you can make informed decisions about how you want to use the results. For instance, if you are extracting information from tax documents you can set custom rules to flag any extracted information with a confidence score lower than 95%. Also, all extracted data are returned with bounding box coordinates, which is a rectangular frame that fully encompasses each piece of data identified, so that you can quickly identify where a word or number appears on a document. You can access these features with the Amazon Textract API, in the AWS Management Console, or using the AWS command-line interface (CLI).  

**Q: What are the most common use cases for Amazon Textract?**

The most common use cases for Amazon Textract include:

- Importing documents and forms into business applications  
    
- Creating smart search indexes   
    
- Building automated document processing workflows  
    
- Maintaining compliance in document archives  
    
- Extracting text for Natural Language Processing (NLP)
- Extracting text for document classification

**Q: What type of text can Amazon Textract detect and extract?**

Amazon Textract can detect printed text and handwriting from the Standard English alphabet and ASCII symbols. Amazon Textract can extract printed text, forms and tables in English, German, French, Spanish, Italian and Portuguese. Amazon Textract also extracts explicitly labeled data, implied data, and line items from an itemized list of goods or services from almost any invoice or receipt in English without any templates or configuration. Amazon Textract can also extract specific or implied data such as names and addresses from identity documents in English such as U.S. passports and driver’s licenses without the need for templates or configuration. Finally, Amazon Textract can extract any specific data from documents without worrying about the structure or variations of the data in the document using Queries in English.  

**Q: What document formats does Amazon Textract support?**

Amazon Textract currently supports PNG, JPEG, TIFF, and PDF formats. For synchronous APIs, you can submit images either as an S3 object or as a byte array. For asynchronous APIs, you can submit S3 objects. If your document is already in one of the file formats that Amazon Textract supports (PDF, TIFF, JPG, PNG), don't convert or downsample it before uploading it to Amazon Textract.  

**Q: How do I get started with Amazon Textract?**

To get started with Amazon Textract, you can click the “Get Started with Amazon Textract” button on the [Amazon Textract page](https://aws.amazon.com/textract/). You must have an Amazon Web Services account; if you do not already have one, you will be prompted to create one during the process. Once you are signed in to your AWS account, try out Amazon Textract with your own images or PDF documents using the [Amazon Textract Management Console](https://console.aws.amazon.com/textract/). You can also download the [Amazon Textract SDKs](https://docs.aws.amazon.com/AWSJavaScriptSDK/latest/AWS/Textract.html) to start creating your own applications. Please refer to our step-by-step [Getting Started Guide](http://docs.aws.amazon.com/textract/latest/dg/what-is.html) for more information.

**Q: What APIs does Amazon Textract offer?**

Amazon Textract performs OCR using the Detect Document Text API, but goes a step further in the document analyzing process and also performs key-value pair detection so that text extractions remain organized in their intended structure. The Analyze Document API can detect printed text, handwriting, fields, values, their relationships, tables, and other entities within a document along with their associated confidence scores. With the Analyze Document API, developers can automatically capture structured data from a wide variety of documents including tax forms, financial reports, medical records, and loan applications. Analyze Document API also provides developers the flexibility to specify the data they need to extract from documents using Queries without worrying about the structure of the data or variations in how the data is laid out across different formats and versions of the document. Using Custom Queries, the Queries feature can be customized for improved extraction accuracy in business specific documents. The Analyze Expense API can find the vendor name on a receipt even if it's only indicated within a logo on the page without an explicit label called “vendor”. It can also find and extract item, quantity, and prices that are not labeled with column headers for line items. With the Analyze Expense API, developers can used normalized key names and column headers when extracting data from invoices and receipts so that downstream applications can easily compare output from many documents. The Analyze ID API understands the context of identity documents such as U.S. passports and driver’s licenses without the need for templates or configuration. Using Analyze ID, businesses providing ID verification services and those in finance, healthcare, and insurance can easily automate account creation, appointment scheduling, employment applications, and more by allowing customers to submit a picture or scan of their identity document. For details, please refer to the [Amazon Textract API](https://docs.aws.amazon.com/textract/latest/dg/API_Reference.html) reference.  

**Q: What features does the Analyze Document API have?**

Analyze Document API has the following features – Forms, Tables, Queries, Custom Queries, Signatures, and Layout. You can use these features independently or use any combination of these features together. Use Forms to extract data such as key-value pairs (e.g., “First Name” and associated value “Jane Smith”). Use Tables to extract tabular or table data organized in columns and rows. Use Queries to specify the information you need from a document in the form of natural language questions (e.g., “What is the customer name?”) and receive the answer (e.g., “Jane Doe”) as part of the response. Use Custom Queries to customize the Queries features on business-specific documents. You can use Signatures to detect signatures on documents and use layout to identify layout elements in a document.  

**Q: How should customers construct/craft/word queries?**

We have published detailed guidance on best practices for crafting Queries as part of our [API Documentation](https://docs.aws.amazon.com/textract/latest/dg/what-is.html) on the Textract Resources page. In general, customers should try to ask a natural language question utilizing words from the document to construct a query.  

**Q: Are there any limits to the number of Queries I can ask per document?**

Queries are processed on a per page basis and information can be extracted using Queries via both synchronous or asynchronous operations. For synchronous operations, a maximum of 15 Queries per page is supported. For asynchronous operations, a maximum of 30 queries per page is supported.  

**Q: How can I get the best results from Amazon Textract?**

Amazon Textract uses machine learning to read virtually any type of document in order to extract printed text, handwriting, and structured information. Keep the following tips in mind in order to get the best results:

- Make sure your document uses a language supported by Amazon Textract (Currently English, Spanish, Italian, Portuguese, French, German. Handwriting, Invoices and Receipts, Identity documents and Queries processing are in English only).
- Provide as high quality an image as you can, ideally at least 150 DPI.
- If your document is already in one of the file formats that Amazon Textract supports (PDF, JPG, PNG), don't convert or downsample it before uploading it to Amazon Textract.
- Amazon Textract's table feature works best when the tables in your document are visually separated from surrounding elements on the page (e.g. not overlaid on an image or complex pattern), and the text within the table is upright (e.g. not rotated relative to other text on the page).

You can get started with analyzing you own documents with Amazon Textract with just a few clicks in the [Amazon Textract Management Console](https://console.aws.amazon.com/textract/). If you have trouble achieving high accuracy with receipts, identification, or industrial diagrams, please contact us on [amazon-textract@amazon.com](mailto:amazon-textract@amazon.com) for assistance.  

**Q: How do I use the confidence score Amazon Textract provides?**

A confidence score is a number between 0 and 100 that indicates the probability that a given prediction is correct. With Amazon Textract, all extracted printed text, handwriting, and structured data are returned with bounding box coordinates, which is a rectangular frame that fully encompasses each piece of data identified. This allows you to identify the score for each extracted entity so that you can make informed decisions on how you want to use the results.  

**Q: In which AWS regions is Amazon Textract available?**

Amazon Textract is currently available in the US East (Northern Virginia), US East (Ohio), US West (Oregon), US West (N. California), AWS GovCloud (US-West), AWS GovCloud (US-East), Canada (Central), EU (Ireland), EU (London), EU (Frankfurt), EU (Paris), Asia Pacific (Singapore), Asia Pacific (Sydney), Asia Pacific (Seoul), and Asia Pacific (Mumbai) Regions.

**Q: Does Amazon Textract work with AWS CloudTrail?**

Yes. Amazon Textract supports logging of the following actions as CloudTrail events - DetectDocumentText, AnalyzeDocument, StartDocumentTextDetection, StartDocumentAnalysis, GetDocumentTextDetection, and GetDocumentAnalysis. For more details, please see [Logging Amazon Textract API Calls with AWS CloudTrail](https://docs.aws.amazon.com/textract/latest/dg/logging-using-cloudtrail.html).

**Q: How can I request a service limit increase for Amazon Textract?**  

You can view and manage your Amazon Textract service quotas (formerly referred to as service limits) in the [AWS Service Quotas console](https://console.aws.amazon.com/servicequotas/home). You can also estimate the quota requirements for your use case using the [Textract Service Quota calculator](https://console.aws.amazon.com/textract/home#/quotaCalculator). To create a service quota increase request:

1\. Login to AWS Console and navigate to the [AWS Service Quotas console](https://console.aws.amazon.com/servicequotas/home) and select “Textract” under AWS services.  
2\. Select the desired quota and click “Request Quota Increase” on the subsequent page.  
3\. Enter in the desired quota value and click “Request”.

**Q: What are the best practices to limit throttling when using Amazon Textract?**

We recommend the following approach to mitigate throttling:

1\. Implement retry logic. Follow the [Error handling](https://docs.aws.amazon.com/textract/latest/dg/handling-errors.html) guidelines to configure retries for throttling errors.  
2\. Configure exponential backoff and jitter. Configuring exponential backoff and jitter as you configure retries allows you to improve the achievable throughput. See [Error retries and exponential backoff in AWS](https://docs.aws.amazon.com/general/latest/gr/api-retries.html).  
3\. Smoothen your traffic flow. Spiky traffic affects throughput. To get maximum throughput for the allotted transactions per second (TPS), use a queueing serverless architecture or another mechanism to “smooth” traffic so it is more consistent.  
4\. Start with samples that apply best practices.  Try using our [IDP CDK Samples](https://github.com/aws-samples/amazon-textract-idp-cdk-stack-samples) using [CDK Constructs](https://github.com/aws-samples/amazon-textract-idp-cdk-constructs).  
5\. Use the [Textract Service Quota calculator](https://console.aws.amazon.com/textract/home#/quotaCalculator) to estimate the quota requirements for your use case and submit a quota increase request from the [AWS Service Quotas console](http://console.aws.amazon.com/servicequotas/home/services/textract/).

## Billing

**Q: How does Amazon Textract count the number of pages processed?**

An image (PNG, TIFF, or JPEG) counts as a single page. For PDFs, each page in the document is counted as a page processed.

**Q: Which APIs am I charged for with Amazon Textract?**

Refer to the Amazon Textract [pricing page](https://aws.amazon.com/textract/pricing/) to learn more about pricing.

**Q: How much does Amazon Textract cost?**

Amazon Textract charges you based on the number of pages and images processed. For more information, visit the [pricing page](https://aws.amazon.com/textract/pricing/).

**Q: Does Amazon Textract participate in the AWS Free Tier?**

Yes. As part of the [AWS Free Tier](https://aws.amazon.com/free/), you can get started with Amazon Textract for free. The Free Tier lasts for three months, and new AWS customers can analyze up to:

**Detect Document Text API**: 1,000 pages per month  
**Analyze Document API**:

- 1000 Pages per month when using Signatures only

- 100 Pages per month when using Forms, Tables, and Layout features

- 100 pages per month each for Queries, Forms + Queries, Tables + Queries, Forms + Tables + Queries

- There is no free-tier for Custom Queries

**Analyze Expense API**: 100 pages per month  
**Analyze ID API**: 100 pages per month  
**Analyze Lending API**: 2,000 pages per month

## Data Privacy

**Q. Are document and image inputs processed by Amazon Textract stored, and how are they used by AWS?**

Amazon Textract may store and use document and image inputs processed by the service solely to provide and maintain the service and to improve and develop the quality of Amazon Textract and other Amazon machine-learning/artificial-intelligence technologies. Use of your content is necessary for continuous improvement of your Amazon Textract customer experience, including the development and training of related technologies. We do not use any personally identifiable information that may be contained in your content to target products, services or marketing to you or your end users. Your trust, privacy, and the security of your content are our highest priority and we implement appropriate and sophisticated technical and physical controls, including encryption at rest and in transit, designed to prevent unauthorized access to, or disclosure of, your content and ensure that our use complies with our commitments to you. Please see [https://aws.amazon.com/compliance/data-privacy-faq/](https://aws.amazon.com/compliance/data-privacy-faq/) for more information. You may opt out of having your document and image inputs used to improve or develop the quality of Amazon Textract and other Amazon machine-learning/artificial-intelligence technologies using an AWS Organizations opt-out policy. For information about how to opt out, see [Managing AI services opt-out policy](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_manage_policies_ai-opt-out.html).  

**Q: Is the content processed by Amazon Textract moved outside the AWS region where I am using Amazon Textract?**

Any content processed by Amazon Textract is encrypted and stored at rest in the AWS region where you are using Amazon Textract. Unless you opt out as provided below, some portion of content processed by Amazon Textract may be stored in another AWS region solely in connection with the continuous improvement and development of your Amazon Textract customer experience and other Amazon machine-learning/artificial-intelligence technologies. You can request deletion of image and video inputs associated with your account by contacting AWS Support. Your trust, privacy, and the security of your content are our highest priority and we implement appropriate and sophisticated technical and physical controls, including encryption at rest and in transit, designed to prevent unauthorized access to, or disclosure of, your content and ensure that our use complies with our commitments to you. Please see [https://aws.amazon.com/compliance/data-privacy-faq/](https://aws.amazon.com/compliance/data-privacy-faq/) for more information. Your content will not be stored in another AWS region if you opt out of having your content used to improve and develop the quality of Amazon Textract and other Amazon machine-learning/artificial-intelligence technologies. For information about how to opt out, see [Managing AI services opt-out policy](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_manage_policies_ai-opt-out.html).  

**Q. Can I delete images and documents stored by Amazon Textract?**

Yes. You can request deletion of document and image inputs associated with your account by contacting AWS Support. Deleting image and document inputs may degrade your Amazon Textract experience.

**Q: Who has access to my content that is processed and stored by Amazon Textract?**

Only authorized employees will have access to your content that is processed by Amazon Textract. Your trust, privacy, and the security of your content are our highest priority, and we implement appropriate and sophisticated technical and physical controls, including encryption at rest and in transit, designed to prevent unauthorized access to, or disclosure of, your content and ensure that our use complies with our commitments to you. Please see [https://aws.amazon.com/compliance/data-privacy-faq/](https://aws.amazon.com/compliance/data-privacy-faq/) for more information.

**Q: Do I still own my content that is processed and stored by Amazon Textract?**

Yes. You always retain ownership of your content, and we will only use your content with your consent.

**Q. How does Amazon Textract handle the content used for adapter generation in Custom Queries?**

Any content used for generating adapters is processed internally within Amazon Textract for the duration of the training. The content is encrypted at rest and in transit. The content is stored and processed in the AWS region where you are training the adapter, and is deleted once training completes. Please see [https://docs.aws.amazon.com/textract/latest/dg/data-protection.html](https://docs.aws.amazon.com/textract/latest/dg/data-protection.html) for more information.

**Q: Is Amazon Textract HIPAA eligible?**

Yes, AWS has expanded its HIPAA compliance program to include Amazon Textract as a HIPAA eligible service. If you have an executed Business Associate Agreement (BAA) with AWS, you can use Amazon Textract to extract text including protected health information (PHI) from images.

[Learn more about HIPAA Compliance »](https://aws.amazon.com/compliance/hipaa-compliance/)  

**Q: What Compliance Programs are in scope for Amazon Textract?**

Textract is HIPAA eligible, and compliant with PCI, ISO, and SOC. For more information please visit AWS Artifact in the AWS Management Console, or visit [https://aws.amazon.com/compliance/services-in-scope/](https://aws.amazon.com/compliance/services-in-scope/). Textract also supports Amazon [Virtual Private Cloud](https://aws.amazon.com/vpc/) (Amazon VPC) endpoints via [AWS PrivateLink](https://aws.amazon.com/privatelink/), enabling customers to securely initiate API calls to Amazon Textract from within their VPC and avoid using the public internet.  
