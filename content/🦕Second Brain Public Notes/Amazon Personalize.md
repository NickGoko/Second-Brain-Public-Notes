---
tags:
  - cloud/aws
---


![](https://i.imgur.com/sIpOTfW.png)

# FAQ
## General

Close all

### What is Amazon Personalize?

Amazon Personalize is a fully managed machine learning (ML) service that uses your data to generate product and content recommendations for your users. You provide data about your end-users (e.g., age, location, device type), items in your catalog (e.g., genre, price) and interactions between users and items (e.g., clicks, purchases). Personalize uses this data to train custom, private models that generate recommendations which can be surfaced via an API.

The service uses algorithms to analyze customer behavior and recommend products, content, and services that are likely to be of interest to them. This enhanced customer experience approach can increase customer engagement, loyalty, and sales, which can lead to increases in revenue and profitability. Personalize is powered by the same ML technology used by [Amazon.com](https://amazon.com/) and allows any developer to easily add personalization to existing applications, websites, push notifications, marketing communications, and more – all without any ML experience required. Personalize uses real-time data insights to deliver recommendations that are personalized instantaneously depending on the user’s behavior. You can get started quickly with use-case optimized recommenders for your business domain, or you can create your own configurable custom resources.

### What Are the Benefits of Using Amazon Personalize?

Here are some reasons why businesses choose Amazon Personalize for personalization:

- <u>Improve user engagement and conversion rates:</u> Users are more likely to interact with products and services that are tailored to their preferences, thus businesses can boost user engagement and conversion rates by offering personalized recommendations.
- <u>Increase customer satisfaction:</u> Businesses can offer a better customer experience by using personalization to surface products and services that are more relevant to their needs and interests.
- <u>Scale personalization in a cost-effective manner:</u> Amazon Personalize is a cloud-based, ML service that can handle massive volumes of user data to produce tailored recommendations for millions of users. It is thus an effective solution for companies with user bases that are large or expanding quickly.
- <u>Save time and resources:</u> Amazon Personalize automates the process of generating tailored suggestions, deploying recommendation models in days, not months. This can help organizations save valuable resources and time that would otherwise be used for manual analysis and recommendation generation.

### How Are Companies Using Amazon Personalize?

Amazon Personalize can be used to personalize the end-user experience over any digital channel. Examples include product recommendations for e-commerce, news articles, publications, media and social networks, hotel recommendations for travel websites, credit card recommendations for banks, and match recommendations for dating sites. Amazon Personalize can also be used to customize the user experience when user interaction is over a physical channel; for example, a meal delivery company could personalize weekly meals to users in a subscription plan. Additional use case examples include the following. See our [customer references](https://aws.amazon.com/personalize/customers/) for real customer success stories.

- <u>Personalize a video streaming app:</u> Add multiple types of personalized video recommendations to your streaming app. For example, _Top picks for you_, _More like X_, and _Most popular_ video recommendations.
- <u>Add product recommendations to an e-commerce app:</u> Add a range of personalized product recommendations to your retail app. For example, _Recommended for you_, _Frequently bought together_, and _Customers who viewed X also viewed_ product recommendations.
- <u>Create personalized emails:</u> Generate batch recommendations for all users on an email list. You can then use an <u>AWS service</u> or <u>third-party service</u> to send users personalized emails recommending items in your catalog.
- <u>Create a targeted marketing campaign:</u> You can use Amazon Personalize to generate segments of users who will most likely interact with items in your catalog. Then you can use an <u>AWS service</u> or <u>third-party service</u> to create a targeted marketing campaign that promotes different items to different user segments.

### How Can I Quickly Try out Amazon Personalize?

Check out the Magic Movie Machine, a short, interactive game where you are looking for movie recommendations that match your personal interests. See first-hand how Amazon Personalize learns what you like and then tunes your recommendations in real-time. [Demo now.](https://dohy8sp8i3s5p.cloudfront.net/)

## Using Amazon Personalize

Close all

### How Does Amazon Personalize Work?

Amazon Personalize has a simple, three-step process, which only takes a few clicks in the AWS Management Console, or a set of simple API calls. First, point Amazon Personalize to your user interaction data (historical log of views, clicks, purchases, etc.) in Amazon S3, upload the data using an easy API call, or use SageMaker Data Wrangler to prep and import your data. Optionally, you can provide an items or users dataset that contains additional information about your catalog and customer base. Second, with just a few clicks in the console or an API call, train a custom private recommendation model for your data. Third, retrieve personalized recommendations. [Watch this Amazon Personalize Deep Dive video series to learn more.](https://www.youtube.com/watch?v=3gJmhoLaLIo&t=1s)

### How Do I Get Started Using Amazon Personalize?

Get started by creating an account and accessing the Amazon Personalize developer console, which walks you through an intuitive set-up wizard. You have the option of using a JavaScript API and Server-Side SDKs to send real-time activity stream data to Amazon Personalize or bootstrapping the service using a historical log of user events. You can also import your data via Amazon Simple Storage Service (S3) or by using SageMaker Data Wrangler. Then, with only a few API calls, you can train a personalization model, either by letting the service choose the right algorithm for your dataset with AutoML or manually choosing one of the several algorithm options available. Once trained, the models can be deployed with a single API call and can then be used by production applications. When deployed, call the service from your production services to get real-time recommendations, and Amazon Personalize will automatically scale to meet demand.

### What Data Do I Have to provide to Amazon Personalize?

Users should provide the following data to Amazon Personalize:

- <u>User activity stream or event data</u>: A historical log of users’ interactions on the website/application is captured in the form of events and is sent to Amazon Personalize via an integration that involves a single line of code. This includes key events such as click, buy, watch, add-to-shopping cart, like, etc. When onboarding to the service, you can also provide a historical log of all event/activity stream data, if available.
- <u>Catalog (item) data:</u> This can be any type of catalog including books, videos, news articles, or products. This involves item ids and metadata associated with each item.
- <u>User data:</u> User profile data including user demographic data such as gender and age. This data is optional.

Amazon Personalize will train and deploy a model based on this data. You can then use a simple inference API to get individualized recommendations at run-time and generate a personalized experience for end-users according to the type of personalization model (for example, user personalization, related items, or personalized reranking).

The following data can help improve your recommendation relevance and is strongly encouraged to include:

- Event type (required for all Domain dataset group use cases)
- Event value
- Contextual metadata
- Item and user metadata

For more information on the types of data Amazon Personalize can use, see [Types of data you can import into Amazon Personalize](https://docs.aws.amazon.com/personalize/latest/dg/data.html).

### How Can I Import and Prepare My Data Using SageMaker DataWrangler?

Amazon Personalize makes it easy for you to import and prepare your data through [Amazon SageMaker Data Wrangler](https://aws.amazon.com/sagemaker/data-wrangler) before using it in Amazon Personalize. With SageMaker Data Wrangler, you can to import data from 40+ supported data sources and perform end-to-end data preparation (including data selection, cleansing, exploration, visualization, and processing at scale) in a single user interface using little to no code. This allows you to rapidly prepare user, item, or interaction datasets using Amazon SageMaker Data Wrangler by leveraging Amazon Personalize-specific transformations and over 300 general built-in data transformations, retrieving data insights, and quickly iterating by fixing data issues. Simply visit the [Amazon Personalize console](https://signin.aws.amazon.com/signin?redirect_uri=https%3A%2F%2Fconsole.aws.amazon.com%2Fpersonalize%2Fhome%3FhashArgs%3D%2523%26isauthcode%3Dtrue%26state%3DhashArgsFromTB_us-east-2_b24b204e230ef3ef&client_id=arn%3Aaws%3Asignin%3A%3A%3Aconsole%2Fconcierge&forceMobileApp=0&code_challenge=xkRQIOf8skojLGzTpH-5jqdVvyFUxtohMB6aG1ntoPQ&code_challenge_method=SHA-256) , open a Dataset from within your Dataset groups, select “Import and Prepare Your Data,” and then choose “Prepare Data with Data Wrangler.” Please note that customers using Amazon SageMaker Data Wrangler will incur additional charges as per their usage. Check out their pricing page.

### Can I Surface Items without Interactions in My Recommendations?

Yes. Amazon Personalize allows you to help your users discover new products and items by allowing you to specify a “new item exploration weight.” This input is then used by Amazon Personalize to automatically strike the right balance between exposing new content to users and offering the most relevant recommendations. Amazon Personalize also considers data about which items users have been exposed to, but chose not to interact with. 

### How Can I Optimize My Data for Amazon Personalize?

Amazon Personalize provides analysis on your data to make getting started easy. It can analyze the data you provide and offers suggestions to assist in improving your data preparation. The performance of personalization systems depends on providing models with high quality data about users and their interactions with items in your catalog. By identifying potential data deficiencies and providing suggestions to assist customers with remediation, Amazon Personalize makes training performant models easier and reduces the need for troubleshooting.

### Can I Personalize My search Results Using Amazon Personalize?

Amazon Personalize has launched an integration with self-managed OpenSearch that enables you to personalize search results for each user and assists in predicting your search needs. The Amazon Personalize Search Ranking plugin within OpenSearch helps you to leverage the deep learning capabilities offered by Amazon Personalize and apply personalized re-ranking to OpenSearch search results, without any ML expertise. With personalized search, you can go beyond the traditional keyword matching approach and boost relevant items in a specific user's search results based on their interests, context, and past interactions in real-time. You can also fine tune the level of personalization for every search query to have greater control over your search experience, improving the end-user engagement and conversion from their search. 

### How Can I Personalize My search Results Using Amazon Personalize and OpenSearch?

The Amazon Personalize Search Ranking plugin is available for both self-managed and Amazon OpenSearch. If you are using Amazon OpenSearch, to get started, simply [setup](https://docs.aws.amazon.com/personalize/latest/dg/opensearch-install.html) an OpenSearch domain, then [setup](https://docs.aws.amazon.com/personalize/latest/dg/setup.html) Amazon Personalize campaign with AWS-personalized-ranking recipe. Next, associate the Amazon Personalize Search Ranking plugin with your domain, and finally configure the plugin. You can also use OpenSearch dashboard to compare your search results.

If you are using self-managed OpenSearch, to get started, simply [setup](https://opensearch.org/docs/latest/install-and-configure/install-opensearch/index/) an OpenSearch cluster, then [setup](https://docs.aws.amazon.com/personalize/latest/dg/setup.html) Amazon Personalize campaign with AWS-personalized-ranking recipe, and finally, [install and configure](https://github.com/opensearch-project/search-processor) the Amazon Personalize Search Ranking plugin within OpenSearch. You can use OpenSearch dashboard to compare your search results.

To learn more, visit our [documentation](https://docs.aws.amazon.com/personalize/latest/dg/personalize-opensearch.html).

### Can Amazon Personalize Help Me to Recommend Actions for My Users?

With the Amazon Personalize Next-Best-Action (aws-next-best-action) recipe, you can determine the next best action to recommend to each individual user based on their preferences, interests and history in real-time. You can recommend actions such as an add-on service, joining a customer loyalty program, subscribing to a newsletter, etc. that encourage conversion. This allows you to improve each user’s experience by nudging them to take certain actions across their user journey that will help in promoting long-term brand engagement. It also enables you to improve return on marketing investment by recommending actions that have a high degree of relevance to the user, thereby resulting in increased revenue and loyalty. [Learn more.](https://aws.amazon.com/blogs/machine-learning/build-brand-loyalty-by-recommending-actions-to-your-users-with-amazon-personalize-next-best-action/)

### How Does Next Best Action Recipe Work

Amazon Personalize Next Best Action (NBA) allows brands to recommend the best action that their individual users should take to increase loyalty and conversion with their brand in real-time. Customers start by defining a list of actions and uploading the required datasets. Next, they train their custom NBA model. They will then integrate recommendations into their applications or marketing technology tools via an API. When an end user triggers a real-time recommendation, Personalize NBA model will return a ranked list of actions for each user along with their propensity scores. Because actions may only be relevant for a specific period of time (e.g. sign up for holiday travel deals), or customers may want to limit the number of actions surfaced to end users (e.g. do not show the same action more than X times in Y days), customers will be able to impose constraints on their action recommendations (e.g. filters). 

### How Do I apply/export Amazon Personalize Recommendations to My Business Workflows or Applications?

Amazon Personalize provides customers two inference APIs: getRecommendations and getPersonalizedRanking. These APIs return a list of recommended itemIDs for a user, a list of similar items for an item, or a reranked list of items for a user. The itemID can be a product identifier, videoID, etc. You are then expected to use these itemIDs to generate the end-user experience through steps, such as fetching image and description, and then rendering a display. In some cases, you might integrate with AWS services, third-party email delivery services, or notification services etc. to generate the end-user experience you desire.

### How Should I Integrate Amazon Personalize with My Existing Applications?

Check out the [Personalization APIs](https://github.com/aws-samples/personalization-apis) solution that explains the real-time low latency API framework that sits between your applications and recommender systems such as Amazon Personalize. The solution also provides best practice implementations of response caching, API gateway configurations, A/B testing with [Amazon CloudWatch Evidently](https://docs.aws.amazon.com/cloudwatchevidently/latest/APIReference/Welcome.html) , inference-time item metadata, automatic contextual recommendations, and more.

### How Do I Know if Amazon Personalize is providing Good Recommendations?

There are a few features built within Amazon Personalize that serve as checkpoints to help you ensure you are optimizing for high quality recommendations.

- <u>Online testing (A/B testing):</u> This is always going to be the best measure of the impact of a model on business metrics. It is also the most common method. You should evaluate your recommendations against business metrics. If you do not have an A/B testing tool already in place, consider using Amazon CloudWatch Evidently. The Personalization APIs project provides a deployable solution and reference architecture.
- <u>Offline metrics:</u> Amazon Personalize computes offline metrics for each solution version and recommender that measure the accuracy of predictions from the model. You can use these metrics to provide a directional sense of the quality of a solution version against other versions. Offline metrics are calculated by splitting the Personalize datasets into a training and testing set. It allows you to view the effects of modifying hyperparameters and algorithms used to train your models, calculated against historical data.
- <u>Online metrics:</u> These are empirical results observed in your user’s interactions with real-time recommendations provided in a live environment. When you are comparing Amazon Personalize models against an existing recommendation system, the historical data is initially biased towards the existing approach. Therefore, running an online test for a few weeks before actually starting a test to measure results is recommended so that the model is trained and evaluated on interactions data that has been generated by seeing recommendations by Amazon Personalize.

### Can Amazon Personalize Help Me Measure the Impact of Recommendations?

You can measure the business outcome of any Amazon Personalize recommendation with any event sent to the system. You can then visualize and evaluate the impact of one or multiple recommendations to develop a more data-driven personalization strategy. From either the Amazon Personalize console or API, define a “metric attribution,” which is a list of interactions (event types) that you want to evaluate and report on. For example, you may want to track two metrics: the click-through rate (CTR) for recommendations and total number of purchases. For each event type, a you simply define the metric and function you want to evaluate (sum or count), and Amazon Personalize performs the calculation and sends reports to your CloudWatch or S3 account.

### Will My Data Be Secure and Private?

All Amazon Personalize models are unique to the customers’ data set, and are not shared across other AWS accounts or with Amazon Retail, Amazon Prime, or any other business unit. No data is used to train or propagate models for other customers; the customer’s model inputs and outputs are entirely owned by the account. Every interaction customers have with Amazon Personalize is protected by encryption. Any user, items, or interactions data processed by Amazon Personalize can be further encrypted with customer keys through AWS Key Management Service, and encrypted at rest and in transit in the AWS Region where the customer is using the service. Administrators can also control access to Amazon Personalize through an [AWS Identity and Access Management](https://aws.amazon.com/iam/) (IAM) permissions policy, ensuring that sensitive information is kept secure and confidential.

## Use Cases

Close all

### What Are the Most Common Use Cases Supported by Amazon Personalize?

- <u>User personalization:</u> Recommendations tailored to a user’s profile, behavior, preferences, and history. This is most commonly used to boost customer engagement and satisfaction. It can also drive higher conversion rates.
- <u>Personalized ranking:</u> Items re-ranked in a category or search response based on user preference or history. This use case is used to surface relevant items or content to a specific user ensuring a better customer experience. Amazon Personalize supports re-ranking while optimizing for business priorities such as revenue, promotions, or trending items.
- <u>Similar items:</u> Recommended related items to encourage exploration, upsell and cross-sell opportunities. Similar item recommendations help users discover new content or compare existing items in your catalog.
- <u>Next Best Action</u>: Recommend the right actions to the right user in real-time based on their individual behavior and needs. This will allow you to maximize user engagement and lead to greater conversion rates.
- <u>Trending Now</u>: Recommend items gaining popularity at the fastest pace among your users, such as breaking news articles, popular social content or newly released movies.
- <u>User segmentation:</u> Targeted messaging and notifications to the users most interested in an item or category. This can help companies drive higher engagement with marketing campaigns and increase retention rates through hyper-targeted messaging.

### What Are the top Features and Capabilities of Amazon Personalize?

Amazon Personalize is constantly being improved based on customer feedback and long-term roadmap objectives as we strive to optimize for easy onboarding and use. Listed here you will find several impactful Amazon Personalize features that go beyond basic ML practices. For a full list of features check out our [Features page](https://aws.amazon.com/personalize/features/).

- <u>User segmentation</u>: Segment end-users intelligently based on their preferences and create targeted messages that resonate with specific customer groups. [Watch this demo to learn more](https://www.youtube.com/watch?v=Fy9_Narfpf0).
- <u>Domain optimized recommenders:</u> Accelerate time-to-market using pre-built recommenders for common business use cases. [Check out this demo to learn more](https://www.youtube.com/watch?v=NN6sM0Dj_Cg).
- <u>New item recommendations:</u> Create quality recommendations for new products and content when data on user preference is scarce.
- <u>Real-time or batch recommendations</u>: Respond to changing intent in real-time or feed mass recommendations to batch-oriented workflows.
- <u>Action recommendations</u>: Increase your user loyalty and conversion by expanding your recommendations beyond items or content. Determine the best action to suggest to individual user based on their preferences, needs, and past behavior.
- <u>Personalized search</u>: Improve user search experience by surfacing relevant search results based on their unique interests, preferences, and past interactions in real-time.
- <u>Unstructured text support:</u> Natural Language Processing and attention-based modeling to automatically extract key information.
- <u>Contextual recommendations:</u> Improve recommendations by generating them with a context such as user segment, device type, location, or time of day.
- <u>Business rules:</u> Apply business rules including filters and promotions that control the percentage of promoted content for each user.
- <u>Trending recommendations:</u> Recommend items gaining popularity at the fastest pace among your users
- <u>Recommendation impact:</u> Measure total business impact of any event such as a page view, video start, click, add to cart, purchase, etc.

## Pricing

Close all

### How much Does Amazon Personalize Cost?

Please see the [Amazon Personalize Pricing page](https://aws.amazon.com/personalize/pricing/) for current pricing information.

### How Can I Optimize My Amazon Personalize Costs?

With Amazon Personalize, you only pay for what you use, and there are no minimum fees and no upfront commitments. Here are some tips on how to manage costs.

Consider caching results based on your needs for real-time updates

 Re-train based on business requirements only

Rely heavily on auto-scaling by setting the minimum provisioned TPS low unless it negatively impacts your throughput / latency targets

Consider using batch recommendations when the use case aligns with a downstream batch process such as email marketing. Since batch recommendations run against a solution version, they do not require a campaign. Note: Batch recommendations are only available in custom recommendation datasets.

The [Amazon Personalize Monitor project](https://github.com/aws-samples/amazon-personalize-monitor) provides some cost optimization features for optimizing campaign provisioning as well as alerting and deleting idle/abandoned campaigns.