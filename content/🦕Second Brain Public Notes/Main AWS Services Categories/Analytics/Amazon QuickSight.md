---
tags:
  - cloud/aws
---
![[Pasted image 20240214170639.png]]  
![[Pasted image 20240214170740.png]]  
![[Pasted image 20240214170854.png]]
# FAQ
## General

### What is Amazon QuickSight?

**QuickSight** is a <mark style="background: #FFB86CA6;">fast, easy-to-use, cloud-powered business analytics service that makes it easier for all employees within an organization to build visualizations, perform ad-hoc analysis, and quickly get business insights from their data, anytime, on any device</mark>.  
Upload CSV and Excel files; connect to SaaS applications like Salesforce; access on-premises databases like SQL Server, MySQL, and PostgreSQL; and seamlessly discover your AWS data sources such as Amazon Redshift, Amazon Relational Database Service (Amazon RDS), Amazon Aurora, Amazon Athena, and Amazon Simple Storage Service (Amazon S3). QuickSight enables organizations to scale their business analytics capabilities to hundreds of thousands of users, and delivers fast and responsive query performance by using a robust in-memory engine (SPICE).

### How is QuickSight Different from Traditional Business Intelligence (BI) Solutions?

Traditional BI solutions often require teams of data engineers to spend months building complex data models before generating a report.  
They typically lack interactive ad-hoc data exploration and visualization, limiting users to canned reports and pre-selected queries.  
Traditional BI solutions also require significant up-front investment in complex and costly hardware and software, and then customers to invest in even more infrastructure to maintain fast query performance as database sizes grow. This cost and complexity makes it difficult for companies to enable analytics solutions across their organizations. 

QuickSight has been designed to solve these problems by bringing the scale and flexibility of the AWS Cloud to business analytics. 

Unlike traditional BI or data discovery solutions, getting started with QuickSight is simple and fast. When you log in, QuickSight seamlessly discovers your data sources in AWS services such as Amazon Redshift, Amazon RDS, Amazon Athena, and Amazon S3.  
 You can connect to any of the data sources discovered by QuickSight and get insights from this data in minutes.  
 <mark style="background: #FFF3A3A6;">You can choose for QuickSight to keep the data in SPICE up to date as the data in the underlying sources change</mark>.  
 SPICE supports rich data discovery and business analytics capabilities to help customers derive valuable insights from their data without worrying about provisioning or managing infrastructure.  
 Organizations pay a low monthly fee for each QuickSight user, eliminating the cost of long-term licenses.  
 With QuickSight, organizations can deliver rich business analytics functionality to all employees without incurring a huge cost upfront.

### What is SPICE?

QuickSight is built with **SPICE**—a <mark style="background: #FF5582A6;">Super-fast, Parallel, In-memory Calculation Engine</mark>.  
Built from the ground up for the cloud,<mark style="background: #FFF3A3A6;"> SPICE uses a combination of columnar storage, in-memory technologies enabled through the latest hardware innovations and machine code generation to run interactive queries on large datasets and get rapid responses</mark>.  
SPICE supports rich calculations to help you derive valuable insights from your analysis without worrying about provisioning or managing infrastructure. Data in SPICE is persisted until it is explicitly deleted by the user. SPICE also automatically replicates data for high availability and enables QuickSight to scale to hundreds of thousands of users who can all simultaneously perform fast interactive analysis across a wide variety of AWS data sources.

### How Can I Get Started with QuickSight?

To get started, sign up to QuickSight, with four authors free in trial for 30 days.

### Are there Any Prerequisites to Use Amazon SageMaker Inferencing in QuickSight?

Your privileged QuickSight account administrator needs to first grant QuickSight IAM permissions to make SageMaker API calls on your behalf. To learn more, see documentation on granting QuickSight IAM permissions.

## Authors and Readers

### Who is a QuickSight Author?

A QuickSight Author is a user who can connect to data sources (within AWS or outside), create visuals and analyze data. Authors can create interactive dashboards using advanced QuickSight capabilities such as parameters and calculated fields, and publish dashboards with other users in the account.

### Who is a QuickSight Reader?

A QuickSight Reader is a user who consumes interactive dashboards. Readers can log in via their organization’s preferred authentication mechanism (QuickSight username/password, SAML portal or AD auth), view shared dashboards, filter data, drill down to details or export data as a CSV file, using a web browser or mobile app. Readers do not have any allocated SPICE capacity.

Individual end-users can be provisioned to access QuickSight as Readers. Reader pricing applies to manual session interactions only. We reserve the right charge for the reader at the higher monthly author rate if, in our discretion, we determine that you are using reader sessions for other types of use (for example, programmatic or automated queries).

### Can I Upgrade a Reader to an Author?

Yes, Readers can be easily upgraded to Authors using the QuickSight user management options.

### I Have a Standard Edition Account. Can I Add Readers?

No, Readers with pay-per-session pricing only exist in Enterprise Edition. If you have a Standard Edition account, you can upgrade to Enterprise Edition using the QuickSight management page.

### Can I Use the QuickSight Reader account for Programmatic Access to QuickSight?

QuickSight Reader user pricing applies to interactive consumption of data by individual users only — for both manual and programmatic access. For sharing of dashboards with multiple end users who are not registered in QuickSight, such as in an embedding scenario, use capacity pricing. See [Service Term](https://aws.amazon.com/service-terms/) 40.4.

### Who is a QuickSight Admin?

A QuickSight Admin is a user who can manage QuickSight users and account-level preferences, as well as purchase SPICE capacity and annual subscriptions for the account. Admins also have all QuickSight authoring capabilities. Admins can also upgrade Standard Edition accounts to Enterprise Edition if needed. For billing purposes, QuickSight Authors and Admins are both recognized as Authors.

### Can I Upgrade a Reader or Author to Admin?

QuickSight Authors and Readers can be upgraded to Admins at any time.

### How long is a Reader Session?

QuickSight Reader sessions are of 30-minute durations each. Each session is charged at $0.30 with maximum charges of $5 per Reader in a month.

### When Does a Reader Session Start and End?

A Reader session starts with a user-initiated action (for example., login, dashboard load, page refresh, drill-down, or filtering) and runs for next 30 minutes. Keeping QuickSight open in a background browser window/tab does not result in active sessions until the Reader initiates action on the page.

### Will a Reader Be Logged out after a 30-minute Session?

No, Reader sessions are transparent to the QuickSight Reader. Reader sessions will be automatically renewed in 30-minute intervals, and time out 30 minutes after start upon inactivity. Readers will only be logged out of QuickSight when their authentication expires, which is dependent on the authentication scheme in place (can be one of QuickSight-only users, SAML/Open ID Connect, or Active Directory).

### Will a Reader Be Charged if QuickSight is Open in a Browser in a Background Tab?

No, having QuickSight open in a background tab will not result in usage charges. A session is only initiated when there is explicit Reader activity on the QuickSight web application. If the QuickSight page is moved to the background or minimized, there will be no additional sessions charged (beyond any sessions initiated when the Reader was active on the window/tab) until the Reader interacts with QuickSight again.

### What Does up to $5/month on Reader Charges Mean?

A Reader will be charged $0.30 a session up to a maximum of $5/month, after which the Reader can access QuickSight at no charge for additional sessions.

### Can QuickSight Authors or Readers Invite More Users?

No, QuickSight Authors and Readers are user types that cannot change account permissions or invite more users. QuickSight offers an Admin user, who can manage QuickSight users and account-level preferences, as well as purchase SPICE capacity and annual subscriptions for the account. Admins also have all QuickSight authoring capabilities. Admins can also upgrade Standard Edition accounts to Enterprise Edition if needed.

### Can I Use the QuickSight Reader account for Display and Scripted Refresh of QuickSight Dashboards on Monitors or Large Screens?

For scripted refresh of QuickSight dashboards intended for monitors or large screens that continuously display data, we recommend use of an Author account. QuickSight Reader user pricing applies to interactive consumption of data by individual end users in an organization. Reader sessions under both user pricing and capacity pricing are also designed to be used in 30-minute intervals. A fair use policy applies, and any abuse of the system will result in the Reader being metered as an Author.

## Mobile and Web Access

### Can I Use Amazon QuickSight on My Mobile Device?

QuickSight mobile apps (available on iOS and Android) gives instant access to your data and insights for you to make decisions on the go. Browse, search and interact with your dashboards. Add dashboards to Favorites for quick and easy access. Explore your data with drill downs, filtering and more. You can also use a web browser on any mobile device to access QuickSight.

### On Which Browsers is QuickSight Supported?

QuickSight supports the latest versions of Mozilla Firefox, Chrome, Safari, Internet Explorer version 10 and above, and Edge.

## Data Management

Close all

### Which Data Sources Does QuickSight Support?

You can connect to AWS data sources including Amazon RDS, Amazon Aurora, Amazon Redshift, Amazon Athena and Amazon S3. You can also upload Excel spreadsheets or flat files (CSV, TSV, CLF, and ELF), connect to on-premises databases like SQL Server, MySQL and PostgreSQL and import data from SaaS applications like Salesforce.

### Can I Connect QuickSight to My Amazon EC2 or On-premises Database?

Yes. To connect QuickSight to an Amazon Elastic Compute Cloud (Amazon EC2) or on-premises database, you need to add the Amazon QuickSight IP range to the authorized list in your hosted database.

### How Do I Upload My Data Files into QuickSight?

You can upload XLSX, CSV, TSV, CLF, XLF data files directly from the QuickSight website. You can also upload them to an Amazon S3 bucket and point QuickSight to the S3 object.

### How Do I Access My Data in AWS Data Sources?

QuickSight seamlessly discovers your AWS data sources that are available in your account with your approval. You can immediately start browsing the data and building visualizations. You can also explicitly connect to other AWS data sources that are not in your account or in a different region by providing connection details for those sources.

### My Source Data is not in a Clean Format. How Do I Format and Transform the Data before Visualizing?

QuickSight lets you prepare data that is not ready for visualization. Select the “Edit/Preview Data” button in the connection dialog. QuickSight supports various functions to format and transform your data. You can alias data fields and change data types. You can subset your data using built in filters and perform database join operations using drag and drop. You can also create calculated fields using mathematical operations and built-in functions such conditional statements, string, numerical and date functions.

### How much Data Can I Analyze with QuickSight?

With QuickSight, you don’t need to worry about scale. You can seamlessly grow your data from a few hundred megabytes to many terabytes of data without managing any infrastructure.

### How Does QuickSight Integration with SageMaker Work?

The first step is to connect the data source from which you want to pull data. Once you’re connected to a data source, select the “Augment with SageMaker” option. From there, you pick the model you want to use from a list of SageMaker models in your AWS account and provide the schema file, which is a JSON-formatted file that contains the input, output, and runtime settings. Review the input schema mapping with the columns in your data set. Once you’re done, you can execute this job and start running the inference.

### Does QuickSight Use SageMaker Models to Perform Inference on Incremental Data or the Full Data Every time it Runs?

QuickSight does inference on the full data every time it refreshes.

## User Management

Close all

### How Do I Manage User Access for QuickSight

When you create a new QuickSight account, you have administrative privileges by default. If you are invited to become an QuickSight user, whoever invites you assigns you either an ADMIN or a USER role. If you have an ADMIN role, you can create and delete user accounts, purchase annual subscriptions and SPICE capacity in addition to using the service. To create a user account, you send an email invitation to the user via an in-application interface, and then the user completes the account creation by specifying a password and signing in.

## Visualization and Analysis

Close all

### How Do I Create an Analysis with QuickSight?

Creating an analysis is simple. QuickSight seamlessly discovers data in popular AWS data repositories within your AWS account. Simply point QuickSight to one of the discovered data sources. To connect to another AWS data source that is not in your AWS account or in a different Region, you can provide the connection details of the source. Then, select a table and start analyzing your data. You can also upload spreadsheets and CSV files and use QuickSight to analyze your files. To create a visualization, start by selecting the data fields you want to analyze, or drag the fields directly on to the visual canvas, or a combination of both actions. QuickSight will automatically select the appropriate visualization to display based on the data you’ve selected.

### How Does QuickSight Select the Right Visualization to Use for My Data?

QuickSight has an innovative technology called AutoGraph that allows it to select the most appropriate visualizations based on the properties of the data, such as cardinality and data type. The visualization types are chosen to best reveal the data and relationships in an effective way.

### How Do I Create a Dashboard?

Dashboards are a collection of visualizations, tables, and other visual displays arranged and visible together. With QuickSight, you can compose a dashboard within an analysis by arranging the layouts and size of visualizations and then publish the dashboard to an audience within your organization.

### What Types of Visualizations Are Supported in QuickSight?

QuickSight supports assorted visualizations that facilitate different analytical approaches: Comparison and distribution Bar charts (several assorted variants) Changes over time Line graphs Area line charts Correlation Scatter plots Heat maps Aggregation Pie graphs Tree maps Tabular Pivot tables

### What is a Suggested Visualization How Does QuickSight Generate Suggestions?

QuickSight comes with a built-in suggestion engine that provides you with suggested visualizations based on the properties of the underlying datasets. Suggestions serve as possible first or next-steps of an analysis and removes the time-consuming task of interrogating and understanding the schema of your data. As you work with more specific data, the suggestions will update to reflect the next steps appropriate to your current analysis.

### What Are Stories?

Stories are guided tours through specific views of an analysis. They are used to convey key points, a thought process, or the evolution of an analysis for collaboration. You can construct them in QuickSight by capturing and annotating specific states of the analysis. When readers of the story select an image in the story, they are then taken into the analysis at that point, where they can explore on their own.

### What Type of Calculations Does QuickSight Enable?

You can perform typical arithmetic and comparison functions; conditional functions such as if,then; and date, numeric, and string calculations.

### How Does QuickSight Integrate with AWS Generated Data?

Today, Billing and Cost Management offers direct integration with QuickSight, which automates creation of the Cost and Usage Dashboard that you can use to gain insights into AWS spend. This dashboard is inspired by the open source project, Cloud Intelligence Dashboards (CID). The Cost and Usage Dashboard brings the benefits of CID to the Billing and Cost Management console as an AWS supported feature and removes the need for maintaining underlying infrastructure like Amazon Athena views or AWS Glue crawlers. You can deploy the Cost and Usage Dashboard from the Data Exports page in the Billing and Cost Management console.

### How Can I Get Sample Data to Explore in QuickSight?

For your convenience, sample analyses are automatically generated when you create an account in Amazon QuickSight. The raw data can also be downloaded from the links below: Business overview People overview Sales pipeline Web and marketing analytics These datasets were created by 47Lining, an AWS Advanced Consulting Partner with Big Data Competency designation.

## Security and Access

Close all

### How is Data Transmitted to QuickSight?

You have several options to get your data into QuickSight: file upload, connect to AWS data sources, connect to external data stores over JDBC/ODBC, or through other API-based data store connectors.

### Can I Choose the AWS Region to Connect to Hosted or On-premises Databases over JDBC/ODBC?

Yes. For better performance and user interactivity, customers are advised to use the region where your data is stored. The QuickSight auto discovery feature detects data sources only within the Region of the QuickSight endpoint to which you are connected. For a list of the supported QuickSight Regions, visit Regional Products and Services for all AWS global infrastructure.

### Does QuickSight Support Multi-factor Authentication?

Yes. You can enable multi-factor authentication (MFA) for your AWS account using the AWS Management Console.

### How Do I Connect My VPC to QuickSight?

If your VPC has been set up with public connectivity, you can add a QuickSight IP address range to your database instances’ security group rules to enable traffic flow into your VPC and database instances.

### What is Row-level Security?

Row-level security (RLS) enables QuickSight dataset owners to control access to data at row granularity based on permissions associated with the user interacting with the data. With RLS, QuickSight users only need to manage a single set of data and apply appropriate row-level dataset rules to it. All associated dashboards and analyses will enforce these rules, simplifying dataset management and removing the need to maintain multiple datasets for users with different data access privileges.

### What Does Private VPC Access in the Context of QuickSight Mean?

If you have data in AWS (perhaps in Amazon Redshift, Amazon RDS, or on EC2) or on-premises in Teradata or SQL Server on servers without public connectivity, this feature is for you. Private VPC (virtual private cloud) Access for QuickSight uses an Elastic Network Interface (ENI) for secure, private communication with data sources in a VPC. It also allows you to use AWS Direct Connect to create a secure, private link with your on-premises resources.

## Sharing

Close all

### How Do I Share an Analysis, Dashboard, or Story in QuickSight?

You can share an analysis, dashboard, or story using the share icon from the QuickSight service interface. You will be able to select the recipients (email address, username or group name), permission levels, and other options before sharing the content with others.

## Upgrades and Downgrades

Close all

### Can I Upgrade from Standard Edition to Enterprise Edition?

Yes, Standard Edition account accounts can be upgraded to Enterprise Edition through the QuickSight management page. Existing authentication details and user data will be seamlessly migrated to Enterprise Edition. Enterprise Edition rates for user and SPICE capacity will apply.

### Can I Downgrade from Enterprise Edition to Standard Edition?

No, you will not be able to downgrade from Amazon QuickSight Enterprise Edition to Standard Edition. Amazon QuickSight Enterprise Edition offers enhanced functionality such as QuickSight Readers, connectivity to data sources in Private VPC, row-level security, hourly refresh of SPICE data as well as AD connectivity and group-based management of assets for AD accounts. Due to the differences in feature set, a downgrade might result in loss of data connectivity and security, and as a result, this option is not supported.