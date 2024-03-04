---
tags:
  - cloud/aws
---


![](https://i.imgur.com/yIdeHr8.png)



# FAQ
**Q: What are the usability improvements offered in the V2 enhanced console and APIs?**

Lex V2 console and APIs use an updated information architecture (IA) to deliver simplified versioning, support for multiple languages in a bot, and streaming capabilities. Additional improvements include the saving of partially completed bot configurations, renaming of resources, simplified navigation, bulk upload of utterances, and granular debugging.

**Q: How can I use the streaming capability?**

<mark style="background: #ADCCFFA6;">You can use the streaming API to conduct a continually streaming conversation with a Lex bot</mark>. With streaming conversation, the bot continuously listens and can be designed to respond proactively to user interruptions and pauses. For example, you can configure the bot to keep a conversation going when a user needs more time to respond by sending periodic messages such as “Take your time. Let me know once you are ready.”

**Q: What are the pricing details for the V2 APIs?**

Amazon Lex bots are designed for a request and response interaction or a continuous streaming conversation. With the request and response interaction, each user input (voice or text) is processed as a separate API call. In a streaming conversation, all user inputs across multiple turns are processed in one streaming API call. Please refer to the [Amazon Lex pricing page](https://aws.amazon.com/lex/pricing/) for more details.

**Q: Can I integrate bots created using V2 APIs with Amazon Connect contact flows?**

Yes, Amazon Connect contact flows work with both Lex V2 and V1 APIs. You can use the Lex V2 console to create and integrate bots with Amazon Connect.

**Q: Can I take advantage of V2 API features for my existing bots?**  

No. If you want to take advantage of V2 features, you will need to recreate your bot with V2 APIs. The Lex V1 APIs are not compatible because V2 APIs use an updated information architecture to enable simplified resource versioning and support for multiple languages within a bot. Converting to V2 APIs is easy, so get started with this step by step migration guide.

**Q: Which regions and languages do the V2 APIs support?**

The Amazon Lex V2 APIs and enhanced console experience is available in all existing 8 regions and languages including US English, Spanish, French, German, Italian, Japanese, Australian English, British English, Canadian French, Latin American Spanish, and US Spanish. For a list of the supported Amazon Lex AWS regions, please visit the [AWS Region Table.](https://aws.amazon.com/about-aws/global-infrastructure/regional-product-services/)

**Q: Will the support for new features such as simplified versioning and multiple languages in a bot be available in the existing APIs?**

No. These features are only available in the V2 APIs. If you want to take advantage of these features, you can migrate to V2 APIs by following this [migration guide](https://docs.aws.amazon.com/lexv2/latest/dg/migration.html).

**Q: Will I be able to access the V1 console?**

Yes, you can access the V1 console in the [AWS Management Console](https://console.aws.amazon.com/lex/). Once in the Lex console, you can navigate between the V1 and V2 console. The bots created in the V1 console will only be visible within the V1 Console. You will not be able to access your V1 bots in the V2 console until you recreate them in the V2 console. Migrating your bots to V2 is easy, here is a step by step [migration guide](https://docs.aws.amazon.com/lexv2/latest/dg/migration.html).

**Q: How do I access the V2 console?**

You can click on the link in the left navigation bar to choose V1 or V2 as your console.

**Q: Can I still use Lex V1 APIs?**

Yes. The existing Lex V1 APIs are still supported. You can continue to use them to build and conduct your bot conversations.