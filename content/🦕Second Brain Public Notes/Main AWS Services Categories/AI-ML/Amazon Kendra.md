---
tags:
  - cloud/aws
---

![](https://i.imgur.com/VH325ZP.png)

# FAQ
### What is Amazon Kendra?

Amazon Kendra is <mark style="background: #D2B3FFA6;">a highly accurate and easy-to-use enterprise search service that’s powered by machine learning (ML)</mark>.  
 <mark style="background: #ABF7F7A6;">It allows developers to add search capabilities to their applications so their end users can discover information stored within the vast amount of content spread across their company</mark>. This includes data from manuals, research reports, FAQs, human resources (HR) documentation, and customer service guides, which may be found across various systems such as Amazon Simple Storage Service (S3), Microsoft SharePoint, Salesforce, ServiceNow, RDS databases, or Microsoft OneDrive. When you type a question, the service uses ML algorithms to understand the context and return the most relevant results, whether that means a precise answer or an entire document. For example, you can ask a question such as "How much is the cash reward on the corporate credit card?” and Amazon Kendra will map to the relevant documents and return a specific answer (such as “2%”). Kendra provides sample code so you can get started quickly and easily integrate highly accurate search into your new or existing applications.

### How Does Amazon Kendra Work with other AWS Services?

Amazon Kendra provides ML-powered search capabilities for all unstructured data that you store in AWS. Amazon Kendra offers easy-to-use native connectors to popular AWS repository types such as Amazon S3 and Amazon RDS databases. Other AI services such as Amazon Comprehend, Amazon Transcribe, and Amazon Comprehend Medical can be used to pre-process documents, generate searchable text, extract entities, and enrich metadata for more-specialized search experiences.

### What Types of Questions Can I Ask Amazon Kendra?

Amazon Kendra supports the following common types of questions:

- Factoid questions (who, what, when, where): “Who is Amazon’s CEO?” or “When is Prime Day 2022?” These questions require fact-based answers that may be returned in the form of a single word or phrase. The precise answer, however, must be explicitly stated in the ingested text content.
- Descriptive question: “How do I connect my Echo Plus to my network?” The answer could be a sentence, a passage, or an entire document.
- Keyword searches: “Health Benefits” or “IT Help Desk.” In cases where the intent and scope are not clear, Amazon Kendra will use its deep learning models to return relevant documents.

### What if My Data doesn’t Contain the Precise Answer Amazon Kendra is Looking For?

When your data doesn’t contain a precise answer to a question, Amazon Kendra returns a list of the most-relevant documents ranked by its deep learning models.

### What Types of Questions Will Amazon Kendra Be Unable to Answer?

Amazon Kendra does not yet support questions where the answers require cross-document passage aggregation or calculations.

### How Do I Get up and Running with Amazon Kendra?

The Amazon Kendra console provides the easiest way to get started. You can point Amazon Kendra at unstructured and semi-structured documents such as FAQs stored in Amazon S3. After ingestion, you can start testing Kendra by typing queries directly in the “search” section of the console. You can then deploy Amazon Kendra search in two easy ways: (1) use the visual UI editor in our Experience Builder (no code required), or (2) implement the Amazon Kendra API using a few lines of code for more-precise control. Code samples are also provided in the console to speed up API implementation.

### How Can I Customize Amazon Kendra to Better Fit My company’s Domain or Business Specialty?

Amazon Kendra offers domain-specific expertise for IT, pharma, insurance, energy, industrial, financial services, legal, media and entertainment, travel and hospitality, health, human resources, news, telecommunications, and automotive. You can further fine-tune and extend Kendra's domain-specific understanding by providing your own synonym lists. Simply upload a file with your specific terminology, and Amazon Kendra will use these synonyms to enrich user searches.

### What File Types Does Amazon Kendra Support?

Amazon Kendra supports unstructured and semi-structured data in .html, MS Office (.doc, .ppt), PDF, and text formats. With the [MediaSearch solution](https://aws.amazon.com/blogs/machine-learning/make-your-audio-and-video-files-searchable-using-amazon-transcribe-and-amazon-kendra/), you can also use Amazon Kendra to search audio and video files.

### How Does Amazon Kendra Handle Incremental Data Updates?

Amazon Kendra provides two methods of keeping your index up to date. First, connectors provide scheduling to automatically sync your data sources on a regular basis. Second, the Amazon Kendra API allows you to build your own connector to send data directly to Amazon Kendra from your data source via your existing ETL jobs or applications.

### What Languages Does Amazon Kendra Support?

For information on language support, refer to this [documentation page](https://docs.aws.amazon.com/kendra/latest/dg/in-adding-languages).

### What Code Changes Do I Need to Make to Use Amazon Kendra?

Ingesting content does not require coding when using the native connectors. You can also write your own custom connectors to integrate with other data sources, using the Amazon Kendra SDK. You can deploy Amazon Kendra search in two easy ways: (1) use the visual UI editor in our Experience Builder (no code required), or (2) implement the Kendra API using a few lines of code for more flexibility. Code samples are also provided in the console to speed up API implementation. The SDK provides full control and flexibility of the end-user experience.

### In what Regions is Amazon Kendra Available?

See the [AWS Regional Services](https://aws.amazon.com/about-aws/global-infrastructure/regional-product-services/) page for more details.

### Can I Add Custom Connectors?

You can write your own connectors using the Amzon Kendra Custom Data Source API. In addition, Amazon Kendra has a search-expert partner ecosystem that can help build connectors currently not available from AWS. Please contact us for more details on our partner network.

### How Does Amazon Kendra Handle Security?

Amazon Kendra encrypts your data in transit and at rest. You have three choices for encryption keys for data at rest: AWS-owned KMS key, AWS-managed KMS key in your account, or a customer-managed KMS key. For data in transit, Amazon Kendra uses the HTTPS protocol to communicate with your client application. API calls to access Amazon Kendra through the network use Transport Layer Security (TLS) that must be supported by the client.

### Can Amazon Kendra Find Answers from the Content of Audio and Video Recordings?

Yes, [MediaSearch solution](https://aws.amazon.com/blogs/machine-learning/make-your-audio-and-video-files-searchable-using-amazon-transcribe-and-amazon-kendra/) combines Amazon Kendra with Amazon Transcribe and enables users to search for relevant answers embedded in audio and video content.