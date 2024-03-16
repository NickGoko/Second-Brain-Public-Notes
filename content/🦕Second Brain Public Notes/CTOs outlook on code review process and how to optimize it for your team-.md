---
id: 83cfab1f-1392-4d95-aff5-edd88365df26
---

# CTOs outlook on code review process and how to optimize it for your team?
#Omnivore

[Read on Omnivore](https://omnivore.app/me/ct-os-outlook-on-code-review-process-and-how-to-optimize-it-for--18e478dcad4)
[Read Original](https://www.codegrip.tech/productivity/ctos-outlook-on-code-review-process/)

## Highlights

> Definition: “**Code review** process is an orderly investigation of projects source code, intended to find plausible issues in it and estimate the **code quality**.”  
> The appropriate approach towards the code review process should be very focused and in line with all the project goals. Just like everything else, knowing why we do something, can be an excellent way to do that at its best. The whole exercise of [**reviewing a code**](https://www.codegrip.tech/productivity/best-practices-for-reviewing-code/?utm%5Fsource=website&utm%5Fmedium=blog&utm%5Fcampaign=ctos-outlook-on-code-review-process-and-how-to-optimize-it-for-your-team) should be to promote the environment of sharing responsibilities for improving the overall [**code quality**](https://www.codegrip.tech/productivity/what-is-code-quality-how-to-measure-and-improve-it/?utm%5Fsource=website&utm%5Fmedium=blog&utm%5Fcampaign=ctos-outlook-on-code-review-process-and-how-to-optimize-it-for-your-team). [⤴️](https://omnivore.app/me/ct-os-outlook-on-code-review-process-and-how-to-optimize-it-for--18e478dcad4#584c705e-fe54-4821-a6fa-4b26af6c178c)  ^584c705e

> Learning and adapting the best practices contributes to building and delivering quality software. After all, code quality impacts how dependable, impregnable, and reliable your project is. Providing a high-quality project is critical for all development teams. Especially with web technologies growing safety-critical, building a quality code becomes vital. [⤴️](https://omnivore.app/me/ct-os-outlook-on-code-review-process-and-how-to-optimize-it-for--18e478dcad4#a8395fb2-a73c-4090-b48e-4bd35ec68774)  ^a8395fb2

> The code is classified as a[ **Good-Code or Bad-Code**](https://www.codegrip.tech/productivity/difference-between-good-and-bad-code/). Good-code is of **high quality**, **clean**, **well-written**, and **understandable**. [⤴️](https://omnivore.app/me/ct-os-outlook-on-code-review-process-and-how-to-optimize-it-for--18e478dcad4#b1d92410-57e2-4f0a-a7b6-4d5c22f90218)  ^b1d92410

> Whereas the Bad-code is not so much so, and it won’t last long, it’s bound to fail when it comes to continuous operations. [⤴️](https://omnivore.app/me/ct-os-outlook-on-code-review-process-and-how-to-optimize-it-for--18e478dcad4#55a72382-be0b-4229-ba6c-b24aa2b4bc62)  ^55a72382

> Code quality for most projects is often somewhere in the middle. When a code is understandable, **well-documented**, and tested, it is considered excellent. [⤴️](https://omnivore.app/me/ct-os-outlook-on-code-review-process-and-how-to-optimize-it-for--18e478dcad4#0a1cd40d-091e-4289-90b8-250aae5718d1)  ^0a1cd40d

> To get the code to be good, manual and functional testing isn’t enough, as it does not give any assurance about the program in the longer run. A review process always played a key role in our **development process** and even then based on the reviewer’s preferences, [**duplication**](https://www.codegrip.tech/productivity/what-is-duplicate-code/?utm%5Fsource=website&utm%5Fmedium=blog&utm%5Fcampaign=ctos-outlook-on-code-review-process-and-how-to-optimize-it-for-your-team) and coding standards were easily overlooked or ignored during a [**manual review**](https://www.codegrip.tech/productivity/manual-vs-automated-code-review/?utm%5Fsource=website&utm%5Fmedium=blog&utm%5Fcampaign=ctos-outlook-on-code-review-process-and-how-to-optimize-it-for-your-team). [⤴️](https://omnivore.app/me/ct-os-outlook-on-code-review-process-and-how-to-optimize-it-for--18e478dcad4#f4f70f2c-b321-4c74-a589-c6ba0fd8d0f8)  ^f4f70f2c

> _“A study on “Software Defect Origins and Removal Methods” found that individual programmers are less than 50% efficient at finding bugs in their software. And most forms of testing are only 35% efficient. Studies like these make it difficult to determine quality.”_
> 
> ![Image result for code quality](https://proxy-prod.omnivore-image-cache.app/549x549,spJX24XTGijgTagYpNk9BibPRzoh5J4OKz7QlrvXCTR8/https://assets.codegrip.tech/wp-content/uploads/2020/03/25122310/r_347670_BPUKP-300x300.jpg) [⤴️](https://omnivore.app/me/ct-os-outlook-on-code-review-process-and-how-to-optimize-it-for--18e478dcad4#b265ebe9-a52b-460a-9117-51c726e80a26)  ^b265ebe9

> ## **Common scenario in software companies for code review**
> 
> There are many companies out there that have a **code review process** in play in their software development process. But most often as the **CI/CD(Continuous Integration / Continues Deployment)** environment leans towards progressive development, delivery becomes one of the critical aspects of the software development process. Due to which code review often takes the back seat. Ultimately, leading to a substantial **technical debt** that is going to affect the whole process and projects in the longer run. The ones that have a code review in place can take the various approaches so that the overall process may vary for every company. [⤴️](https://omnivore.app/me/ct-os-outlook-on-code-review-process-and-how-to-optimize-it-for--18e478dcad4#ff74cbaa-21bf-4ffa-bc5b-6eed2f9b80af)  ^ff74cbaa

> For example:-
> 
> * Some companies use ‘git’ extensively and have their pipeline set up in **Master** and **Branch** format so that every **“pull request”** incorporates a **peer code review**.
> * Some other companies, especially startups, don’t opt for a formal code review, and instead, they have a peer-to-peer discussion. Someone from the team casually looks at the code to make sure there’s nothing wrong with it.
> * Many companies use formal code reviews but only as a way of finding bugs that elude QA? [⤴️](https://omnivore.app/me/ct-os-outlook-on-code-review-process-and-how-to-optimize-it-for--18e478dcad4#ea08cbbc-1417-471e-aa53-89eb07e7e95c)  ^ea08cbbc

> All approaches have their **merits** and **demerits**, and it isn’t straightforward to measure the success rate of any code review process. It is most likely an ongoing exercise for a very long duration for every organization. [⤴️](https://omnivore.app/me/ct-os-outlook-on-code-review-process-and-how-to-optimize-it-for--18e478dcad4#55c9dcbe-aaad-4297-8055-ad01603424fc)  ^55c9dcbe

> struggled with things like inappropriate comments made by the reviewer, time invested in the style, non-scalable architecture of the project, and general neglect towards the length and presentation of the code. The way we overcame these issues was by integrating an **automated code review tool** with the team’s existing process. [⤴️](https://omnivore.app/me/ct-os-outlook-on-code-review-process-and-how-to-optimize-it-for--18e478dcad4#e36bfc2b-0792-4935-95ef-a80ec0d19740)  ^e36bfc2b

> Before the **code review process** was pretty much manual. Our team used to write the code for a particular task and submit it for review. The reviewer reviewed all code that was up for review in branches of the assigned project. Only if the code passes the review successfully, was the code merged upstream or launched. But this was a very time-consuming and yet not a **fail-proof method**. [⤴️](https://omnivore.app/me/ct-os-outlook-on-code-review-process-and-how-to-optimize-it-for--18e478dcad4#90478013-a755-4bb5-b30c-0ec02decba33)  ^90478013

> an automated code review tool that allowed us to analyze the code based on particular language standards. [⤴️](https://omnivore.app/me/ct-os-outlook-on-code-review-process-and-how-to-optimize-it-for--18e478dcad4#93450310-71c4-4974-aab3-d987e43663ad)  ^93450310

> This whole exercise drastically reduced the time required for code review and **improved the overall code quality**. Now on every **pull-request**, the reviewer reviews the analysis provided by **Codegrip** and the code written by the author. The code merges upstream only if it passes the review. Embedding automated code review tool, in our review process, allowed us to save time and prevent from populating the master line of the project. High quality should be the goal throughout the software development process. [⤴️](https://omnivore.app/me/ct-os-outlook-on-code-review-process-and-how-to-optimize-it-for--18e478dcad4#b258df78-2ebd-425d-9002-4d0e52801706)  ^b258df78

> ## **What should be the expected mindset while setting up a code review process?**
> 
> The first step should be the author[ **reading their code**](https://www.codegrip.tech/productivity/how-to-format-code-for-maximum-code-readability/?utm%5Fsource=website&utm%5Fmedium=blog&utm%5Fcampaign=how-startups-can-get-a-head-start-with-proper-code-reviews?) even before a review. This notion allows the author to elucidate their code before giving it to the team. So, the reviewer finds fewer issues while reviewing his code. [⤴️](https://omnivore.app/me/ct-os-outlook-on-code-review-process-and-how-to-optimize-it-for--18e478dcad4#be5d1732-016c-4389-b5b2-a9504d32b156)  ^be5d1732

> Often the author doesn’t have an observed and quantitative goal before or after the code is reviewed. Having this clear goal will increase **accountability** among the authors for their code. To set these goals, the best way to start is with proven matrices instead of defining something vague such as “fixing more bugs.” [⤴️](https://omnivore.app/me/ct-os-outlook-on-code-review-process-and-how-to-optimize-it-for--18e478dcad4#bf09cff2-7814-49d6-bb78-91a81e5ae201)  ^bf09cff2

> All the standards that the author follows should be measurable. These observations **good (best practices)** or **bad (mistakes made)** can contribute to improving the code review process across the organizations. There are various benefits like better planning for enough time for a proper or slow review. So, the whole team is aligned on project objectives and the current state. [⤴️](https://omnivore.app/me/ct-os-outlook-on-code-review-process-and-how-to-optimize-it-for--18e478dcad4#2c0ddcaa-6cde-44d9-b4b3-0073c5d692ef)  ^2c0ddcaa

> All these observations, while conducting reviews on development artifacts like **requirements**, **user stories**, and **design documents** is a good way to ensure that your whole team understands the end goals of a project.  
>  It is up to the manager to foster a positive attitude about **finding defects.** Code reviews offer an opportunity for all team members to correct bad habits to learn new tricks and expand capabilities. [⤴️](https://omnivore.app/me/ct-os-outlook-on-code-review-process-and-how-to-optimize-it-for--18e478dcad4#3c49bfe4-80e2-4d75-9c7d-f2d8e46cb6aa)  ^3c49bfe4

> A code review performed for functional verification is different from a code review conducted for quality purposes. [⤴️](https://omnivore.app/me/ct-os-outlook-on-code-review-process-and-how-to-optimize-it-for--18e478dcad4#90eda9ef-2daf-415e-aa66-eaf7e457408d)  ^90eda9ef

> A code review done for **improving the quality** should always have a designated [**automated code review process**](https://www.codegrip.tech/productivity/automated-code-review-some-processes-you-can-automate/?utm%5Fsource=website&utm%5Fmedium=blog&utm%5Fcampaign=ctos-outlook-on-code-review-process-and-how-to-optimize-it-for-your-team). It may be a pull-request on GitHub, a differential revision on, a crucible review on Atlassian, or any number of other review tools. [⤴️](https://omnivore.app/me/ct-os-outlook-on-code-review-process-and-how-to-optimize-it-for--18e478dcad4#3199d4b1-9740-4592-95ea-f3b110f05421)  ^3199d4b1

> A good review is if the author improves the reviewed code and reviews it meticulously! He or she needs to be sure to read the code and concentrate on both the logic and its presentation, and not just skim through the code. It goes hand-in-hand with the idea for conceiving every single change made while reviewing the code, so the same mistakes are not made next time. [⤴️](https://omnivore.app/me/ct-os-outlook-on-code-review-process-and-how-to-optimize-it-for--18e478dcad4#4a0f6e86-e69c-431c-a65e-ee38087a7910)  ^4a0f6e86

> Reviewing the **_“Patch/Update/Enhancement”_** is also as important as the actual production code. It can be shocking just how often such patches and workarounds make it into production and become the correct logic for the project code rather than being replaced. [⤴️](https://omnivore.app/me/ct-os-outlook-on-code-review-process-and-how-to-optimize-it-for--18e478dcad4#9f90c81f-3ffe-4f04-985b-e863546365a6)  ^9f90c81f

> ##### Reviewing the documentation/requirements, test cases, and built files are equally important. While reviewing these documents they should be.
> 
> * **Functional.**
> * **Clean and maintainable.**
> * **Optimized.** [⤴️](https://omnivore.app/me/ct-os-outlook-on-code-review-process-and-how-to-optimize-it-for--18e478dcad4#17538480-85e3-4202-b459-12937421c2fc)  ^17538480

> Reviewing can be intimidating, so it helps to remember that reviewers are not perfect! Issues may slip past the reviewer, and bugs may evade detection, performance flaws may make it to production. So adding multiple layers to a code review process is always a way to go.
> 
> We have always used code review as a **team-building activity** that has helped us find defects before launch and improve our overall software quality during launch. I would suggest doing a certain amount of code review each day, even if it’s not every line that’s fine. [⤴️](https://omnivore.app/me/ct-os-outlook-on-code-review-process-and-how-to-optimize-it-for--18e478dcad4#d5af8c18-ca7d-4c42-8786-7f9af544effb)  ^d5af8c18

> A review process should always have breaks in between review sessions so that incessant code reviews don’t overwhelm the team. Implementing an automated code review tool for even greater efficiency and accuracy helps in optimizing the time teams spend on code reviews. We should always verify that defects are fixed. And lastly, having a **checklist** improves results for both authors and reviewers substantially. Using a list will remind the reviewer as well as the author, to take the time to look for something that might be missing during the code review, as well as helping to improve their coding skills. [⤴️](https://omnivore.app/me/ct-os-outlook-on-code-review-process-and-how-to-optimize-it-for--18e478dcad4#c82fcea0-f0f8-4217-afe2-b221b0c098c3)  ^c82fcea0

> ## **Our observations while setting-up the code review process that works best for us**
> 
> Implementing the automated code review tool in our existing manual code review process allowed us to **enhance the overall process** for **software development in Mindbowser**. It allowed us to plan time for all the projects in the pipeline. Having an automated code review tool helped our team to contribute and collaborate on smarter initiatives. Even the new members of the team started to learning much fasted then before and a drastic difference was noticed in the overall quality of code. Helping us to **limit risk** and **costs simultaneously.**
> 
> ![Infographic for code review process manual vs automated](https://proxy-prod.omnivore-image-cache.app/719x1313,shSvMdSgpSI9A3EnyT3lm0mKFwC8pZ-pKyEVliH8IjJY/https://assets.codegrip.tech/wp-content/uploads/2020/03/25121446/Codegrip_Info_final-1.jpg)
> 
> #### Want [⤴️](https://omnivore.app/me/ct-os-outlook-on-code-review-process-and-how-to-optimize-it-for--18e478dcad4#3281828e-fdd2-4df0-b676-daba34b48163)  ^3281828e

