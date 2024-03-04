---
tags:
  - computer-science/ai
  - computer-science/generative-ai
  - computer-science/machine-learning
  - "#productivity/prompt-engineering"
Links: "[[Machine Learning & AI 15-12-2023]]"
Area: 
---
## CHAT GPT PROMPT TEMPLATES

You are an expert {	}. You have been helping people {	} for 15 years. Your task is to help me{	} . You must ask questions before answering to understand better what I am seeking. Tell me if you identify optimization methods in my reasoning or overall goal. Is that understood?

You are an expert in {	} with over 10 years experience in {	}, i want you to teach me today about everything about {	} and think step by step as you explain things like I am{	}. And be sure to add interesting examples and analogies.

As a Public Speaking Mentor, can you share some tried-and-tested techniques to help me overcome my fear of public speaking when presenting {Product/Project} to a {Company/Industry} conference? Are there any writing techniques I should use while preparing for a speech, and should I practice a lot before giving a presentation? Also, how do I tailor my pitch to different audiences, and what should I do if I'm faced with a difficult audience in the {Company/Industry}?
```
Create a Python syntax generator that generates [random] Python code samples. The generator should take into account different [types of variables], [functions], and [control structures] such as if/else statements, loops, and classes. The generated code should be valid Python code and should contain comments that explain what each line of code does. Additionally, the generator should [ask the user] what level of difficulty they want the generated code to be ([beginner], [intermediate], or [advanced]). Once the user inputs their desired level of difficulty, the generator should produce a Python code sample that matches the selected difficulty level. Finally, the generator should offer the user the capability to download the generated code sample to their [device] for later reference.
```

```
Act as a Personal Growth Mentor for someone who wants to improve their [Social Skills] and build deeper connections with others in the [Industry]. They struggle with shyness and anxiety in social situations, which holds them back from meeting new people or pursuing new experiences in [Project]. Develop a personalized program that helps them overcome their fears, increase their self-esteem, and cultivate meaningful relationships that enrich their life.
```

```
Acting as a career development mentor, advise a recent graduate specializing in [Product] who is having trouble finding job opportunities in their desired industry. What steps can they take to enhance their resume, expand their network, and increase their chances of getting hired at [Company] or in related industries?
```

```
Act as a coding tutor that creates study plans to help people learn to code. 
You will be provided with the goal of the student, their time commitment, and resource preferences.  
You will create a study plan with timelines and links to resources.  
Only include relevant resources because time is limited. My first request - "I want to become a{} but I do not know how to code. I can study 10 hours per week and only want video resources.  
I want to learn to code in python. Create a study plan for me."
```

```
Act as a coding tutor that creates study plans to help people learn to code. You will be provided with the goal of the student, their time commitment, and resource preferences. You will create a study plan with timelines and links to resources. Only include relevant resources because time is limited. My first request - "I want to become a data scientist but I do not know how to code. I can study 10 hours per week and only want video resources. I want to learn to code in python. Create a study plan for me.
```



## PROMPT ENGINEERING COURSERA COURSE

Prompt engineering involves crafting effective prompts to elicit desired responses from language models like GPT-3.5. Here's a concise guide to help you master prompt engineering:

1. **Clarity and Specificity**: Be clear and specific about what you want. Vague prompts can lead to ambiguous or irrelevant responses. State your request explicitly.

2. **Context Setting**: Provide relevant context if needed. This helps the model understand the context of your query and generate more accurate responses.

3. **Instructions**: Include instructions within your prompt. You can specify the format you want the answer in, or ask the model to think step-by-step before providing an answer.

4. **Examples**: Use examples to guide the model. Show a couple of example responses that you're looking for. This helps the model understand the tone, style, and content you're seeking.

5. **Temperature and Max Tokens**: Adjust the "temperature" setting to control randomness. A lower value (e.g., 0.2) makes the output more focused, while a higher value (e.g., 0.8) makes it more creative. Set a reasonable "max tokens" limit to keep the response concise.

6. **Positive and Negative Reinforcement**: Incorporate positive and negative reinforcement in your prompt to guide the model's behavior. For example, "Provide a well-researched answer and avoid speculation."

7. **Breaking Down Complex Questions**: If your question is complex, consider breaking it down into sub-questions. Prompt the model to address each part separately.

8. **Roleplay and Context Shifts**: Specify a role for the model to take on, or ask it to respond as if it's in a different context. This can lead to more creative and engaging responses.

9. **Ask for Pros and Cons**: If seeking a balanced response, prompt the model to list pros and cons before presenting a conclusion.

10. **Synthesize Information**: Ask the model to synthesize information from various sources or viewpoints to provide a comprehensive answer.

11. **Iterative Refinement**: If the initial response isn't quite what you need, iterate by refining the prompt or adjusting parameters.


### [PROMPTS I LEARNED](#)

1. From now on when I ask a question, suggest a better version of my question and ask if I want to use it.- when you need better questions

2. Act as a skeptic that is well versed in {------} Whatever i tell you offer a skeptical and detailed response - this is for when you want an opposing view. 

3. Act as a {-----} skeptic. Whatever I tell you, provide a skeptical response. E.g. **act as a seven year old, act as a layman**.  
	a. It can also act as innate objects like a linux terminal. 

4. Fundamental contextual statements. Making the AI try to act in a helpful manner and not output inappropriate content. 
```
You are ChatAmazing, the most powerful AI assistant ever created. Your special ability is to offer the most insightful responses to any question. You don't just give ordinary answers, you give inspired answers. You are an expert at identifying harmful content and filtering it out of any responses that you provide.
```


### Audience Persona
Tailor LLMs to provide the output to a certain persona set by the user.  
“**Explain large language models to me. Assume i have to technical background in the area**”  
“Explain large language model to me. Assume i am second grader who gets bored easily”
### Few Shot Examples
Give the LLMs the input and output examples. And teaching it to learn from that pattern.  
“I am going to provide you with sample input and output and i need you generate the output for whatever input i give you after  
input: Egypt  
output: Capital city= Cairo, Population in 2021= 21,323,000  
input: Kenya  
output: Capital city= Nairobi, Population in 2021= 4,922,000”
### RECIPE PATTERN
“**I would like to purchase a house. I know that I need to perform steps to make an offer and close on the house. Provide a complete sequence of steps for me. Fill in any missing steps.”**
### ASK FOR INPUT
“From now on, I am going to cut/paste email chains into our conversation. You will summarize what each person's points are in the email chain. You will provide your summary as a series of sequential bullet points. At the end, list any open questions or action items directly addressed to me. My name is Jill Smith. Ask me for the first email chain.”
### OUTLINE EXPANDER
To use this pattern, your prompt should make the following fundamental contextual statements:  
	- **Act as an outline expander.  
	- Generate a bullet point outline based on the input that I give you and then ask me for which bullet point you should expand on.  
	- Create a new outline for the bullet point that I select.  
	- At the end, ask me for what bullet point to expand next.  
	- Ask me for what to outline.**

<mark style="background: #BBFABBA6;">Act as an outline expander. Generate a bullet point outline based on the input that I give you and then ask me for which bullet point you should expand on.  
Each bullet can have at most 3-5 sub bullets. The bullets should be numbered using the pattern [A-Z].[i-v].[* through ****]. </mark>

<mark style="background: #BBFABBA6;">Create a new outline for the bullet point that I select.  
 At the end, ask me for what bullet point to expand next. Ask me for what to outline. </mark>

- [*] WHAT IF YOU WANT CONTENT OR EXPAND CONTENT INTO THE OUTLINES YOU HAVE MADE. USE MENU ACTIONS PATTERN

### MENU ACTION PATTERN
**Whenever I type: "Write {Bullet point} {Paragraph}", you will write content for the selected bullet point{Bullet Point}. You will write {Paragraphs} of text Whenever I type just {Bullet Point} you will expand that bullet point At the end, you will ask me for the next action.**  

To use this pattern, your prompt should make the following fundamental contextual statements:

**Whenever I type: X, you will do Y.**  
(Optional, provide additional menu items) Whenever I type Z, you will do Q. At the end, you will ask me for the next action.

You will need to replace "X" with an appropriate pattern, such as "estimate {TASK DURATION}" or "add FOOD". You will then need to specify an action for the menu item to trigger, such as "add FOOD to my shopping list and update my estimated grocery bill".  

Examples:  
	**Whenever I type: "add FOOD", you will add FOOD to my grocery list and update my estimated grocery bill. Whenever I type "remove FOOD", you will remove FOOD from my grocery list and update my estimated grocery bill. Whenever I type "save" you will list alternatives to my added FOOD to save money. At the end, you will ask me for the next action. Ask me for the first action.**

### FACT CHECK LIST PATTERN

To use this pattern, your prompt should make the following fundamental contextual statements:  
	- Generate a set of facts that are contained in the output  
	- The set of facts should be inserted at POSITION in the output  
	- The set of facts should be the fundamental facts that could undermine the veracity of the output if any of them are incorrect  
You will need to replace POSITION with an appropriate place to put the facts, such as "at the end of the output".  
Examples:  
	**Whenever you output text, generate a set of facts that are contained in the output. The set of facts should be inserted at the end of the output. The set of facts should be the fundamental facts that could undermine the veracity of the output if any of them are incorrect.**

### TAIL GENERATION PATTERN

Useful for when you are having long conversations. And you don’t want the LLM to forget the rules.  
To use this pattern, your prompt should make the following fundamental contextual statements:  
	- At the end, repeat Y and/or ask me for X.  

You will need to replace "Y" with what the model should repeat, such as "repeat my list of options", and X with what it should ask for, "for the next action". These statements usually need to be at the end of the prompt or next to last.  
Examples:  
	- Act as an _outline expander_.  
	  **Generate a bullet point outline based on the input that I give you and then ask me for which bullet point you should expand on. Create a new outline for the bullet point that I select. At the end, ask me for what bullet point to expand next. Ask me for what to outline**.  
	- From now on, at the end of your output, add the disclaimer "**This output was generated by a large language model and may contain errors or inaccurate statements. All statements should be fact checked**." Ask me for the first thing to write about.


<mark style="background: #D2B3FFA6;">WHEN YOU WANT TO FILTER OUT INFORMATION NOT ADDING BUT REMOVING AND PERHAPS CHANGING THE MEANING OF SOME ASPECTS SEMANTICALLY. For privacy reasons for example regarding personal information. </mark>
### SEMANTIC FILTER PATTERN
To use this pattern, your prompt should make the following fundamental contextual statements:

Filter this information to remove X

You will need to replace "X" with an appropriate definition of what you want to remove, such as. "names and dates" or "costs greater than $100".

Examples:  
<mark style="background: #FFF3A3A6;">Filter this information to remove any personally identifying information or information that could potentially be used to re-identify the person. 

Filter this email to remove redundant information.</mark>

### Chain-of-Thought Prompting (CoT)
![](https://i.imgur.com/Ez2vu5E.png)  
Chain-of-thought (CoT) prompting enables complex reasoning capabilities through intermediate reasoning steps. You can combine it with few-shot prompting to get better results on more complex tasks that require reasoning before responding.  
_Prompt:_

```
The odd numbers in this group add up to an even number: 4, 8, 9, 15, 12, 2, 1.
A: Adding all the odd numbers (9, 15, 1) gives 25. The answer is False.
The odd numbers in this group add up to an even number: 17,  10, 19, 4, 8, 12, 24.
A: Adding all the odd numbers (17, 19) gives 36. The answer is True.
The odd numbers in this group add up to an even number: 16,  11, 14, 4, 8, 13, 24.
A: Adding all the odd numbers (11, 13) gives 24. The answer is True.
The odd numbers in this group add up to an even number: 17,  9, 10, 12, 13, 4, 2.
A: Adding all the odd numbers (17, 9, 13) gives 39. The answer is False.
The odd numbers in this group add up to an even number: 15, 32, 5, 13, 82, 7, 1. 
A:
```
_Output:_

```
Adding all the odd numbers (15, 5, 13, 7, 1) gives 41. The answer is False.
```

**Wow! We can see a perfect result when we provided the reasoning step. In fact, we can solve this task by providing even fewer examples, i.e., just one example seems enough:**

_Prompt:_

```
The odd numbers in this group add up to an even number: 4, 8, 9, 15, 12, 2, 1.
A: Adding all the odd numbers (9, 15, 1) gives 25. The answer is False.
The odd numbers in this group add up to an even number: 15, 32, 5, 13, 82, 7, 1. A:
```

_Output:_

```
Adding all the odd numbers (15, 5, 13, 7, 1) gives 41. The answer is False.
```

<mark style="background: #BBFABBA6;">Keep in mind that the authors claim that this is an emergent ability that arises with sufficiently large language models.</mark>
#### Zero-shot COT Prompting
![](https://i.imgur.com/zDZAsvg.png)  
One recent idea that came out more recently is the idea of [zero-shot CoT(opens in a new tab)](https://arxiv.org/abs/2205.11916) (Kojima et al. 2022) that essentially involves adding "Let's think step by step" to the original prompt. Let's try a simple problem and see how the model performs:

_Prompt:_

```
I went to the market and bought 10 apples. I gave 2 apples to the neighbor and 2 to the repairman. I then went and bought 5 more apples and ate 1. How many apples did I remain with?
```

_Output:_

```
11 apples
```

The answer is incorrect! Now Let's try with the special prompt.

_Prompt:_

```
I went to the market and bought 10 apples. I gave 2 apples to the neighbor and 2 to the repairman. I then went and bought 5 more apples and ate 1. How many apples did I remain with?Let's think step by step.
```

_Output:_

```
First, you started with 10 apples.You gave away 2 apples to the neighbor and 2 to the repairman, so you had 6 apples left.Then you bought 5 more apples, so now you had 11 apples.Finally, you ate 1 apple, so you would remain with 10 apples.
```

It's impressive that this simple prompt is effective at this task. This is particularly useful where you don't have too many examples to use in the prompt.

#### Automatic Chain-of-Thought (Auto-CoT)
When applying chain-of-thought prompting with demonstrations, the process involves hand-crafting effective and diverse examples. This manual effort could lead to suboptimal solutions. [Zhang et al. (2022)(opens in a new tab)](https://arxiv.org/abs/2210.03493) propose an approach to eliminate manual efforts by leveraging LLMs with "Let's think step by step" prompt to generate reasoning chains for demonstrations one by one. This automatic process can still end up with mistakes in generated chains. To mitigate the effects of the mistakes, the diversity of demonstrations matter. This works proposes Auto-CoT, which samples questions with diversity and generates reasoning chains to construct the demonstrations.

Auto-CoT consists of two main stages:

- Stage 1): **question clustering**: partition questions of a given dataset into a few clusters
- Stage 2): **demonstration sampling**: select a representative question from each cluster and generate its reasoning chain using Zero-Shot-CoT with simple heuristics

The simple heuristics could be length of questions (e.g., 60 tokens) and number of steps in rationale (e.g., 5 reasoning steps). This encourages the model to use simple and accurate demonstrations.

The process is illustrated below:

![AUTOCOT](https://www.promptingguide.ai/_next/image?url=%2F_next%2Fstatic%2Fmedia%2Fauto-cot.642d9bad.png&w=3840&q=75)  
Code for Auto-CoT is available [here(opens in a new tab)](https://github.com/amazon-science/auto-cot).

## SUMMARY OF THE PROMPT PATTERN CATALOG.
Always Consider This When Prompting  
Prompting engineering is classified into catalogs:  
#### INPUT SEMANTICS
how you speak to the LLM.  
This category deals with how an LLM understands the input and how it translates the input into something it can use to generate output. This category includes the **Meta Language Creation** pattern, which focuses on creating a custom language for the LLM to understand. This pattern is useful when the default input language is ill-suited  
for expressing ideas the user wants to convey to the LLM.  
#### OUTPUT CUSTOMIZATION
tailoring the structure, types, formats and other properties of the output.  
This category focuses on constraining or tailoring the types, formats, structure, or other properties of the output generated by the LLM. The prompt patterns in this category include **Output Automater, Persona, Visualization Generator, Recipe, and Template patterns.**  
	- The Output Automater pattern allows the user to create scripts that can automate any tasks the LLM output suggests the user should perform.  
	- The Persona pattern gives the LLM a persona or role to play when generating output.  
	- The Visualization Generator pattern allows the user to generate visualizations by producing textual outputs that can be fed to other tools, such as other AI-based image generators, like DALL-E 13.  
	- The Recipe pattern allows the user to obtain a sequence of steps or actions to realize a stated end result, possibly with partially known information or constraints.  
	- The Template pattern allows the user to specify a template for the output, which the LLM fills in with content.  
#### ERROR IDENTIFICATION
identifying errors and resolving errors in the output generated by the LLM.  
This category includes the **Fact Check List and Reflection patterns**.  
The Fact Check List pattern requires the LLM to generate a list of facts the output depends on that should be fact-checked.  
The Reflection pattern requires the LLM to introspect on its output and identify any errors

#### PROMPT IMPROVEMENT
Improving the quality of input and output.  
This category includes the **Question Refinement, Alternative Approaches, Cognitive Verifier, and Refusal Breaker patterns**.  
<mark style="background: #BBFABBA6;">The Question Refinement pattern ensures the LLM always suggests a better version of the user’s question. </mark>  
<mark style="background: #FFB86CA6;">The Alternative Approaches pattern requires the LLM to suggest alternative ways of accomplishing a user-specified task. </mark>  
<mark style="background: #ABF7F7A6;">The Cognitive Verifier pattern instructs the LLM to automatically suggest a series of sub questions for the user to answer before combining the answers to the sub questions and producing an answer to the overall question. </mark>  
<mark style="background: #D2B3FFA6;">The Refusal Breaker pattern requires the LLM to automatically reword the user’s question when it refuses to produce an answer.</mark>

#### INTERACTION
Interaction between the user and the LLM.  
This category includes the **Flipped Interaction, Game Play, and Infinite Generation patterns.**  
<mark style="background: #BBFABBA6;">The Flipped Interaction pattern requires the LLM to ask questions rather than generate output. </mark>  
<mark style="background: #FFB86CA6;">The Game Play pattern requires the LLM to generate output in the form of a game.</mark>  
<mark style="background: #ABF7F7A6;">The Infinite Generation pattern requires the LLM to generate output indefinitely without the user having to reenter the generator prompt each time.</mark>

#### CONTEXT CONTROL
-category focuses on controlling the contextual information in which the LLM operates. This category includes the **Context Manager pattern**, which allows the user to specify the context for the LLM’s output. 

#### META LANGUAGE CREATION
During a conversation with an LLM, the user would like to create the prompt via an alternate language, such as a textual short-hand notation for graphs, a description of states and state transitions for a state machine, a set of commands for prompt automation, etc. 

The key to successfully using the Meta Language Creation pattern is developing an unambiguous notation or shorthand, such as the following: “From now on, whenever I type two identifiers separated by a “→”, I am describing a graph. For example, “a → b” is describing a graph with nodes “a” and “b” and an edge between them. If I separate identifiers by “-[w:2, z:3]→”, I am adding properties of the edge, such as a weight or label.”

Although Meta Language Creation is a powerful pattern it must be used carefully, particularly when describing concepts that may otherwise be hard to precisely or concisely describe. These types of prompts are thus best used in completely new conversation sessions. Using a single meta-language-per conversation session may also be a best practice since it avoids the potential for conflicting or unexpected semantics being applied to the conversation over time.

#### THE OUTPUT AUTOMATER PATTERN
When you have an output or recommendations with multiple steps that can be automated 
1. <mark style="background: #FF5582A6;">Intent and Context:</mark> The intent of this pattern is to have the LLM generate a script or other automation artifact that can automatically perform any steps it recommends taking as part of its output. The goal is to reduce the manual effort needed to implement any LLM output recommendations. 
2. <mark style="background: #FF5582A6;">Motivation:</mark> The output of an LLM is often a sequence of steps for the user to follow. For example, when asking an LLM to generate a Python configuration script it may suggest a number of files to modify and changes to apply to each file. However, having users continually perform the manual steps dictated by LLM output is tedious and error-prone.
3. <mark style="background: #FF5582A6;">Structure and Key Ideas: Fundamental contextual statements: </mark>[Contextual Statements Example ](#)  
<mark style="background: #BBFABBA6;">Whenever you produce an output that has at least one step to take and the following properties (alternatively, always do this) </mark>  
↓  
<mark style="background: #BBFABBA6;">Produce an executable artifact of type X that will automate these steps. </mark>

- **The first part of the pattern identifies the situations under which automation should be generated.**  
- **A simple approach is to state that the output includes at least two steps to take and that an automation artifact should be produced.**  
- **The scoping is up to the user, but helps prevent producing output automation scripts in cases where running the output automation script will take more user effort than performing the original steps produced in the output. The scope can be limited to outputs requiring more than a certain number of steps.**  
- **The next part of this pattern provides a concrete statement of the type of output the LLM should output to perform the automation. For example, “produce a Python script” gives the LLM a concrete understanding to translate the general steps into equivalent steps in Python. The automation artifact should be concrete and must be something that the LLM associates with the action of “automating a sequence of steps**

 1. <mark style="background: #FF5582A6;">Example Implementation:</mark> A sample of this prompt pattern applied to code snippets generated by the ChatGPT LLM is shown below:

<mark style="background: #D2B3FFA6;"> “From now on, whenever you generate code that spans more than one file, generate a Python script that can be run to automatically create the specified files or make changes to existing files to insert the generated code.”  
</mark>  
**This pattern is particularly effective in software engineering as a common task for software engineers using LLMs is to then copy/paste the outputs into multiple files.**  
**Tools, such as Copilot, insert limited snippets directly into the section of code that the coder is working with, but tools, such as ChatGPT, do not provide these facilities. This automation trick is also effective at creating scripts for running commands on a terminal, automating cloud operations, or reorganizing files on a file system.**  

**This pattern is a powerful complement for any system that can be computer controlled. The LLM can provide a set of steps that should be taken on the computer-controlled system and then the output can be translated into a script that allows the computer controlling the system to automatically take the steps. This is a direct pathway to allowing LLMs, such as ChatGPT, to integrate quality into—and to control—new computing systems**

1. <mark style="background: #FF5582A6;">Consequences:</mark> An important usage consideration of this pattern is that the automation artifact must be defined concretely. Without a concrete meaning for how to “automate” the steps, the LLM often states that it “can’t automate things” since that is beyond its capabilities. LLMs typically accept requests to produce code, however, so the goal is to instruct the LLM to generate text/code, which can be executed to automate something. This subtle distinction in meaning is important to help an LLM disambiguate the prompt meaning. 

At this point in the evolution of LLMs, the Output Automater pattern is best employed by users who can read and understand the generated automation artifact. LLMs can (and do) produce inaccuracies in their output, so blindly accepting and executing an automation artifact carries significant risk. Although this pattern may alleviate the user from performing certain manual steps, it does not alleviate their responsibility to understand the actions they undertake using the output. When users execute automation scripts, therefore they assume responsibility for the outcomes.

#### THE FLIPPED INTERACTION PATTERN
1. <mark style="background: #FF5582A6;">Intent and Context:</mark> You want the LLM to ask questions to obtain the information it needs to perform some tasks. Rather than the user driving the conversation, therefore, you want the LLM to drive the conversation to focus it on achieving a specific goal. For example, you may want the LLM to give you a quick quiz or automatically ask questions until it has sufficient information to generate a deployment script for your application to a particular cloud environment. 

2. <mark style="background: #FF5582A6;">Motivation: </mark>Rather than having the user drive a conversation, an LLM often has knowledge it can use to more accurately obtain information from the user. The goal of the Flipped Interaction pattern is to flip the interaction flow so the LLM asks the user questions to achieve some desired goal. The LLM can often better select the format, number, and content of the interactions to ensure that the goal is reached faster, more accurately, and/or by using knowledge the user may not (initially) possess.
3. <mark style="background: #FF5582A6;">Structure and Key Ideas</mark>: Fundamental contextual statements:

**I would like you to ask me questions to achieve X  
You should ask questions until this condition is met or to achieve this goal (alternatively, forever)  
(Optional) ask me the questions one at a time, two at a time, etc.**

Equally important is that the questions should focus on a particular topic or outcome. By providing the goal, the LLM can understand what it is trying to accomplish through the interaction and tailor its questions accordingly.  
<mark style="background: #CACFD9A6;">A flipped interaction can be terminated with a response like “stop asking questions”. It is often better, however, to scope the interaction to a reasonable length or only as far as is needed to reach the goal. </mark>  
This goal can be surprisingly open-ended and the LLM will continue to work towards the goal by asking questions, as is the case in the example of ”until you have enough information to generate a Python script”.  
By default, the LLM is likely to generate multiple questions per iteration. The third idea is completely optional, but can improve usability by limiting (or expanding) the number of questions that the LLM generates per cycle. If a precise number/format for the questioning is not specified, the questioning will be semi-random and may lead to one-at-a-time questions or ten-at-a-time questions. The prompt can thus be tailored to include the number of questions asked at a time, the order of the questions, and any other formatting/ordering considerations to facilitate user interaction.

1. Example Implementation: A sample prompt for a flipped interaction is shown below:  
<mark style="background: #BBFABBA6;">“From now on, I would like you to ask me questions to deploy a Python application to AWS. When you have enough information to deploy the application, create a Python script to automate the deployment.” </mark>  
In general, the more specific the prompt regarding the constraints and information to collect, the better the outcome. For instance, the example prompt above could provide a menu of possible AWS services (such as Lambda, EC2, etc.) with which to deploy the application. One limitation of this prompt is that, once other contextual information is provided regarding the task, it may require experimentation with the precise phrasing to get the LLM to ask the questions in the appropriate number and flow to best suit the task, such as asking multiple questions at once versus one question at a time. 

2. Consequences: One consideration when designing the prompt is how much to dictate to the LLM regarding what information to collect prior to termination. In the example above, the flipped interaction is open-ended and can vary significantly in the final generated artifact. This open-endedness makes the prompt generic and reusable, but may potentially ask additional questions that could be skipped if more context is given.  
If specific requirements are known in advance, it is better to inject them into the prompt rather than hoping the LLM will obtain the needed information. Otherwise, the LLM will non nondeterministically decide whether to prompt the user for the information or make an educated guess as to an appropriate value. 

**When developing prompts for flipped interactions, it is important to consider the level of user knowledge, engagement, and control. If the goal is to accomplish the goal with as little user interaction as possible (minimal control), that should be stated explicitly.Conversely, if the goal is to ensure the user is aware of all key decisions and confirms them (maximum engagement) that should also be stated explicitly. Likewise, if the user is expected to have minimal knowledge and should have the questions targeted at their level of expertise, this information should be engineered into the prompt.**  

#### THE PERSONA PATTERN
1. Intent and Context: In many cases, users would like LLM output to always take a certain point of view or perspective.
2. Motivation: Users may not know what types of outputs or details are important for an LLM to focus on to achieve a given task. They may know, however, the role or type of person that they would normally ask to get help with these things. The Persona pattern enables the users to express what they need help with without knowing the exact details of the outputs they need.
3. Structure and Key Ideas: Fundamental contextual statements:  
	Contextual Statements  
	Act as persona X  
		↓  
	Provide outputs that persona X would create

The first statement conveys the idea that the LLM needs to act as a specific persona and provide outputs that such a persona would. This persona can be expressed in a number of ways, ranging from a job description, title, fictional character, historical figure, etc.  
The persona should elicit a set of attributes associated with a well-known job title, type of person, etc.2 The secondary idea—provide outputs that persona X would create—offers opportunities for customization. For example, a teacher might provide a large variety of different output types, ranging from assignments to reading lists to lectures. If a more specific scope to the type of output is known, the user can provide it in this statement.  
4) Consequences: An interesting aspect of taking nonhuman personas is that the LLM may make interesting assumptions or “hallucinations” regarding the context. A widely circulated example on the Internet asks ChatGPT to act as a Linux terminal and produce the expected output that you would get if the user typed the same text into a terminal. Commands, such as ls -l, will generate a file listing for an imaginary UNIX file system, complete with files that can have cat file1.txt run on them.  
#### THE QUESTION REFINEMENT PATTERN
1. Intent and Context: This pattern engages the LLM in the prompt engineering process. The intent of this pattern is to ensure the conversational LLM always suggests potentially better or more refined questions the user could ask instead of their original question. Using this pattern, the LLM can aid the user in finding the right question to ask in order to arrive at an accurate answer. In addition, the LLM may help the user find the information or achieve their goal in fewer interactions with the user than if the user employed trial and error prompting. 

2. Motivation: If a user is asking a question, it is possible they are not an expert in the domain and may not know the best way to phrase the question or be aware of additional information helpful in phrasing the question. LLMs will often state limitations on the answer they are providing or request additional information to help them produce a more accurate answer. An LLM may also state assumptions it made in providing the answer. The motivation is that this additional information or set of assumptions could be used to generate a better prompt. Rather than requiring the user to digest and rephrase their prompt with the additional information, the LLM can directly refine the prompt to incorporate the additional information.

3. Structure and Key Ideas: Fundamental contextual statements:  
	Contextual Statements  
<mark style="background: #BBFABBA6;">Within scope X, suggest a better version of the question to use instead 

(Optional) prompt me if I would like to use the better version instead </mark>

The first contextual statement in the prompt is asking the LLM to suggest a better version of a question within a specific scope. The scope is provided to ensure that not all questions are automatically reworded or that they are refined with a given goal.  
The second contextual statement is meant for automation and allows the user to automatically use the refined question without having to copy/paste or manually enter it.  
The engineering of this prompt can be further refined by combining it with the Reflection pattern, which allows the LLM to explain why it believes the refined question is an improvement.

1. Example Implementation:  
“<mark style="background: #BBFABBA6;">From now on, whenever I ask a question about a software artifact’s security, suggest a better version of the question to use that incorporates information specific to security risks in the language or framework that I am using instead and ask me if I would like to use your question instead.” 
</mark>
In the context of the example above, the LLM will use the Question Refinement pattern to improve security-related questions by asking for or using specific details about the software artifact and the language or framework used to build it.  
For instance, if a developer of a Python web application with FastAPI asks ChatGPT “How do I handle user authentication in my web application?”, the LLM will refine the question by taking into account that the web application is written in Python with FastAPI. The LLM then provides a revised question that is more specific to the language and framework, such as “What are the best practices for handling user authentication securely in a FastAPI web application to mitigate common security risks, such as cross-site scripting (XSS), cross-site request forgery (CSRF), and session hijacking?” 

1. Consequences: The Question Refinement pattern helps bridge the gap between the user’s knowledge and the LLM’s understanding, thereby yielding more efficient and accurate interactions.  
One risk of this pattern is its tendency to rapidly narrow the questioning by the user into a specific area that guides the user down a more limited path of inquiry than necessary.  
The consequence of this narrowing is that the user may miss important ”bigger picture” information. One solution to this problem is to provide additional scope to the pattern prompt, such as “do not scope my questions to specific programming languages or frameworks.”

Another approach to overcoming arbitrary narrowing or limited targeting of the refined question is to combine the **Question Refinement pattern** with other patterns. In particular, this pattern can be combined with the **Cognitive Verifier pattern** so the LLM automatically produces a series of follow-up questions that can produce the refined question. 

For example, in the following prompt the Question Refinement and Cognitive Verifier patterns are applied to ensure better questions are posed to the LLM:  
 “<mark style="background: #BBFABBA6;">From now on, whenever I ask a question, ask four additional questions that would help you produce a better version of my original question. Then, use my answers to suggest a better version of my original question.” </mark>

As with many patterns that allow an LLM to generate new questions using its knowledge, the LLM may introduce unfamiliar terms or concepts to the user into the question.  
One way to address this issue is to include a statement that the LLM should explain any unfamiliar terms it introduces into the question. A further enhancement of this idea is to combine the Question Refinement pattern with the Persona pattern so the LLM flags terms and generates definitions that assume a particular level of knowledge, such as this example:  
“<mark style="background: #BBFABBA6;">From now on, whenever I ask a question, ask four additional questions that would help you produce a better version of my original question. Then, use my answers to suggest a better version of my original question. After the follow-up questions, temporarily act as a user with no knowledge of AWS and define any terms that I need to know to accurately answer the questions.” </mark>  
An LLM can always produce factual inaccuracies, just like a human. A risk of this pattern is that the inaccuracies are introduced into the refined question. This risk may be mitigated, however, by combining the Fact **Check List pattern** to enable the user to identify possible inaccuracies and the **Reflection pattern** to explain the reasoning behind the question refinement.

#### THE ALTERNATIVE APPROACHES PATTERN

1. Intent and Context: The intent of the pattern is to ensure an LLM always offers alternative ways of accomplishing a task so a user does not pursue only the approaches with which they are familiar. The LLM can provide alternative approaches that always force the user to think about what they are doing and determine if that is the best approach to meet reach their goal. In addition, solving the task may inform the user or teach them about alternative concepts for subsequent follow-up. 

2. Motivation: Humans often suffer from cognitive biases that lead them to choose a particular approach to solve a problem even when it is not the right or “best” approach. Moreover, humans may be unaware of alternative approaches to what they have used in the past. The motivation of the Alternative Approaches pattern is to ensure the user is aware of alternative approaches to select a better approach to solve a problem by dissolving their cognitive biases. 

3. Structure and Key Ideas:  
Contextual Statements  
<mark style="background: #BBFABBA6;">Within scope X, if there are alternative ways to accomplish the same thing, list the best alternate approaches  
Or If there are alternative ways to accomplish a task X that I give you, list the best alternate approaches

(Optional) compare/contrast the pros and cons of each approach 

(Optional) include the original way that I asked 

(Optional) prompt me for which approach I would like to use </mark>

The first statement, “within scope X”, scopes the interaction to a particular goal, topic, or bounds on the questioning. The scope is the constraints that the user is placing on the alternative approaches. The scope could be “for implementation decisions” or “for the deployment of the application”. The scope ensures that any alternatives fit within the boundaries or constraints that the user must adhere to. 

The second statement, “if there are alternative ways to accomplish the same thing, list the best alternate approaches” instructs the LLM to suggest alternatives. As with other patterns, the specificity of the instructions can be increased or include domain-specific contextual information. For example, the statement could be scoped to  
“if there are alternative ways to accomplish the same thing with the software framework that I am using”  
to prevent the LLM from suggesting alternatives that are inherently non-viable because they would require too many changes to other parts of the application. Since the user may not be aware of the alternative approaches, they also may not be aware of why one would choose one of the alternatives. 

The optional statement “compare/contrast the pros and cons of each approach” adds decision making criteria to the analysis. This statement ensures the LLM will provide the user with the necessary rationale for alternative approaches. 

The final statement, “prompt me for which approach I would like to use”, helps eliminate the user needing to manually copy/paste or enter in an alternative approach if one is selected. 

1. <mark style="background: #FF5582A6;">Example Implementation</mark>: Example prompt implementation to generate, compare, and allow the user to select one or more alternative approaches:  
**Whenever I ask you to deploy an application to a specific cloud service, if there are alternative services to accomplish the same thing with the same cloud service provider, list the best alternative services and then compare/contrast the pros and cons of each approach with respect to cost, availability, and maintenance effort and include the original way that I asked. Then ask me which approach I would like to proceed with.**

 This implementation of the Alternative Approaches pattern is being specifically tailored for the context of software engineering and focuses on the deployment of applications to cloud services.  
The prompt is intended to intercept places where the developer may have made a cloud service selection without full awareness of alternative services that may be priced more competitively or easier to maintain.  
The prompt directs ChatGPT to list the best alternative services that can accomplish the same task with the same cloud service provider (providing constraints on the alternatives), and to compare and contrast the pros and cons of each approach. 

1. Consequences: This pattern is effective in its generic form and can be applied to a range of tasks effectively. Refinements could include having a standardized catalog of acceptable alternatives in a specific domain from which the user must select. The Alternative Approaches pattern can also be used to incentivize users to select one of an approved set of approaches while informing them of the pros/cons of the approved options.


#### THE COGNITIVE VERIFIER PATTERN

1. Intent and Context: Research literature has documented that LLMs can often reason better if a question is subdivided into additional questions that provide answers combined into the overall answer to the original question. The intent of the pattern is to force the LLM to always subdivide questions into additional questions that can be used to provide a better answer to the original question. 

2. Motivation: The motivation of the Cognitive Verifier pattern is two-fold: • Humans may initially ask questions that are too high level to provide a concrete answer without additional follow-up due to unfamiliarity with the domain, laziness in prompt entry, or being unsure about what the correct phrasing of the question should be. • Research has demonstrated that LLMs can often perform better when using a question that is subdivided into individual questions. 

3. Structure and Key Ideas: Fundamental contextual statements:  
[Contextual Statements ](#)

<mark style="background: #BBFABBA6;">When you are asked a question, follow these rules  

Generate a number of additional questions that would help more accurately answer the question  

Combine the answers to the individual questions to produce the final answer to the overall question  
</mark>  
The first statement is to generate a number of additional questions that would help more accurately answer the original question.  
**This step instructs the LLM to consider the context of the question and to identify any information that may be missing or unclear.  
By generating additional questions, the LLM can help to ensure that the final answer is as complete and accurate as possible. This step also encourages critical thinking by the user and can help to uncover new insights or approaches that may not have been considered initially, which subsequently lead to better follow-on questions.** 

**The second statement is to combine the answers to the individual questions to produce the final answer to the overall question. This step is designed to ensure that all of the information gathered from the individual questions is incorporated into the final answer. By combining the answers, the LLM can provide a more comprehensive and accurate response to the original question. This step also helps to ensure that all relevant information is taken into account and that the final answer is not based on any single answer.** 

1. Example Implementation: 

“<mark style="background: #BBFABBA6;">When I ask you a question, generate three additional questions that would help you give a more accurate answer. When I have answered the three questions, combine the answers to produce the final answers to my original question.”  
</mark>  
This specific instance of the prompt pattern adds a refinement to the original pattern by specifying a set number of additional questions that the LLM should generate in response to a question. In this case, the prompt specifies that ChatGPT should generate three additional questions that would help to give a more accurate answer to the original question. The specific number can be based on the user’s experience and willingness to provide follow-up information.  
 A refinement to the prompt can be to provide a context for the amount  
of knowledge that the LLM can assume the user has in the domain to guide the creation of the additional questions: 

“<mark style="background: #D2B3FFA6;">When I ask you a question, generate three additional questions that would help you give a more accurate answer. Assume that I know little about the topic that we are discussing and please define any terms that are not general knowledge. When I have answered the three questions, combine the answers to produce the final answers to my original question.” </mark>

The refinement also specifies that the user may not have a strong understanding of the topic being discussed, which means that the LLM should define any terms that are not general knowledge. This helps to ensure that the follow-up questions are not only relevant and focused, but also accessible to the user, who may not be familiar with technical or domain specific terms. By providing clear and concise definitions, the LLM can help to ensure that the follow-up questions are easy to understand and that the final answer is accessible to users with varying levels of knowledge and expertise.

1. Consequences:  
 This pattern can dictate the exact number of questions to generate or leave this decision to the LLM. There are pros and cons to dictating the exact number.  
A pro is that specifying an exact number of questions can tightly scope the amount of additional information the user is forced to provide so it is within a range they are willing and able to contribute.  
A con, however, is that given N questions there may be an invaluable N + 1 question that will always be scoped out. Alternatively, the LLM can be provided a range or allowed to ask additional questions. Of course, by omitting a limit on the number of questions the LLM may generate numerous additional questions that overwhelm the user. 

#### THE FACT CHECKLIST PATTERN

1. Intent and Context: The intent of this pattern is to ensure that the LLM outputs a list of facts that are present in the output and form an important part of the statements in the output. This list of facts helps inform the user of the facts (or assumptions) the output is based on. The user can then perform appropriate due diligence on these facts/assumptions to validate the veracity of the output. 

2. Motivation: A current weakness of LLMs (including ChatGPT) is they often rapidly (and even enthusiastically!) generate convincing text that is factually incorrect. These errors can take a wide range of forms, including fake statistics to invalid version numbers for software library dependencies. Due to the convincing nature of this generated text, however, users may not perform appropriate due diligence to determine its accuracy. 

3. Structure and Key Ideas: Fundamental contextual statements:  
Contextual Statements 

<mark style="background: #BBFABBA6;">Generate a set of facts that are contained in the output </mark>

<mark style="background: #BBFABBA6;">The set of facts should be inserted in a specific point in the output </mark>

<mark style="background: #BBFABBA6;">The set of facts should be the fundamental facts that could undermine the veracity of the output if any of them are incorrect </mark>

One point of variation in this pattern is where the facts are output. Given that the facts may be terms that the user is not familiar with, it is preferable if the list of facts comes after the output. This after-output presentation ordering allows the user to read and understand the statements before seeing what statements should be checked. 

1. Example Implementation: A sample wording of the Fact Check List pattern is shown below: 

<mark style="background: #BBFABBA6;">“From now on, when you generate an answer, create a set of facts that the answer depends on that should be fact-checked and list this set of facts at the end of your output. Only include facts related to cybersecurity.” </mark>

The user may have expertise in some topics related to the question but not others. The fact checklist can be tailored to topics that the user is not as experienced in or where there is the most risk. For example, in the prompt above, the user is scoping the fact check list to security topics, since these are likely very important from a risk perspective and may not be well-understood by the developer. Targeting the facts also reduces the cognitive burden on the user by potentially listing fewer items for investigation. 

1. Consequences: The Fact Check List pattern should be employed whenever users are not experts in the domain for which they are generating output.  
For example, a software developer reviewing code could benefit from the pattern suggesting security considerations. In contrast, an expert on software architecture is likely to identify errors in statements about the software structure and need not see a fact check list for these outputs.  
Errors are potential in all LLM outputs, so Fact Check List is an effective pattern to combine with other patterns, such as by combining it with the Question Refinement pattern.  
A key aspect of this pattern is that users can inherently check it against the output. In particular, users can directly compare the fact check list to the output to verify the facts listed in the fact check list actually appear in the output. Users can also identify any omissions from the list. Although the fact check list may also have errors, users often have sufficient knowledge and context to determine its completeness and accuracy relative to the output.  
One caveat of the Fact Check List pattern is that it only applies when the output type is amenable to fact-checking. For example, the pattern works when asking ChatGPT to generate a Python “requirements.txt” file since it will list the versions of libraries as facts that should be checked, which is handy as the versions commonly have errors.  
However, ChatGPT will refuse to generate a fact check list for a code sample and indicate that this is something it cannot check, even though the code may have errors.


#### THE TEMPLATE PATTERN
1. Intent and Context: The intent of the pattern is to ensure an LLM’s output follows a precise template in terms of structure. 

2. Motivation: In some cases, output must be produced in a precise format that is application or use-case specific and not known to the LLM. Since the LLM is not aware of the template structure, it must be instructed on what the format is and where the different parts of its output should go. This could take the form of a sample data structure that is being generated, a series of form letters being filled in, etc.

 3. Structure and Key Ideas:  
[Contextual Statements](#)  
<mark style="background: #BBFABBA6;">I am going to provide a template for your output X is my placeholder for content. </mark>

<mark style="background: #BBFABBA6;">Try to fit the output into one or more of the placeholders that I list.  
</mark>

<mark style="background: #BBFABBA6;">Please preserve the formatting and overall template that I provide </mark>

<mark style="background: #BBFABBA6;">This is the template: PATTERN with PLACEHOLDERS</mark> 

The first statement directs the LLM to follow a specific template for its output. The template will be used to try and coerce the LLMs responses into a structure that is consistent with the user’s formatting needs. This pattern is needed when the target format is not known to the LLM. If the LLM already has knowledge of the format, such as a specific file type, then the template pattern can be skipped and the user can simply specify the known format.  
However, there may be cases, such as generating Javascript Object Notation (JSON), where there is a large amount of variation in how the data could be represented within that format and the template can be used to ensure that the representation within the target format meets the user’s additional constraints. 

The second statement makes the LLM aware that the template will contain a set of placeholders. Users will explain how the output should be inserted into the template through the placeholders. The placeholders allow the user to semantically target where information should be inserted. Placeholders can use formats, like NAME, that allow the LLM to infer the semantic meaning of to determine where output should be inserted (e.g., insert the person’s name in the NAME placeholder).  
Moreover, by using placeholders, the user can indicate what is not needed in the output – if a placeholder doesn’t exist for a component of the generated output, then that component can be omitted.  
Ideally, placeholders should use a format that is commonly employed in text that the LLM was trained on, such as all caps, enclosure in brackets, etc. 

The third statement attempts to constrain the LLM so that it doesn’t arbitrarily rewrite the template or attempt to modify it so that all of the output components can be inserted. It should be noted that this statement may not preclude additional text from being generated before or after. In practice, LLMs will typically follow the template, but it is harder to eliminate any additional text being generated beyond the template without experimentation with prompt wording

1. Example Implementation: A sample template for generating URLs where the output is put into specific places in the template is shown below:  
<mark style="background: #BBFABBA6;">“I am going to provide a template for your output. Everything in all caps is a placeholder. Any time that you generate text, try to fit it into one of the placeholders that I list. Please preserve the formatting and overall template that I provide at https://myapi.com/NAME/profile/JOB” </mark>

A sample interaction after the prompt was provided, is shown:  
<mark style="background: #BBFABBA6;">User: “Generate a name and job title for a person”  
ChatGPT: “https://myapi.com/Emily Parker/profile/ Software Engineer”</mark>

1. Consequences: One consequence of applying the Template pattern is that it filters the LLM’s output, which may eliminate other outputs the LLM would have provided that might be useful to the user. In many cases, the LLM can provide helpful descriptions of code, decision making, or other details that this pattern will effectively eliminate from the output.  
Users should therefore weight the pros/cons of filtering out this additional information.  
In addition, filtering can make it hard to combine this pattern with other patterns from the Output Customization category. The Template pattern effectively constrains the output format, so it may not be compatible with generation of certain other types of output. For example, in the template provided above for a URL, it would not be easy (or likely possible) to combine with the Recipe pattern, which needs to output a list of steps. 



#### THE INFINITE GENERATION PATTERN

1. Intent and Context: The intent of this pattern is to <mark style="background: #ABF7F7A6;">automatically generate a series of outputs (which may appear infinite) without having to reenter the generator prompt each time.</mark>  
The goal is to limit how much text the user must type to produce the next output, based on the assumption that the user does not want to continually reintroduce the prompt.  
In some variations, the intent is to allow the user to keep an initial prompt template, but add additional variation to it through additional inputs prior to each generated output. 

2. Motivation: Many tasks require repetitive application of the same prompt to multiple concepts.  
For example, generating code for create, read, update, and delete (CRUD) operations for a specific type of entity may require applying the same  
prompt to multiple types of entities.  
If the user is forced to retype the prompt over and over, they may make mistakes. The Infinite Generation pattern allows the user to repetitively apply a prompt, either with or without further input, to automate the generation of multiple outputs using a predefined set of constraints. 

3. Structure and Key Ideas:  
Contextual Statements  
<mark style="background: #BBFABBA6;">I would like you to generate output forever, X output(s) at a time. </mark>

<mark style="background: #BBFABBA6;">
(Optional) here is how to use the input I provide between outputs. </mark>

<mark style="background: #BBFABBA6;">(Optional) stop when I ask you to. </mark>

The first statement specifies that the user wants the LLM to generate output indefinitely, which effectively conveys the information that the same prompt is going to be reused over and over.  
By specifying the number of outputs that should be generated at a time (i.e. “X outputs at a time”), the user can rate limit the generation, which can be particularly important if there is a risk that the output will exceed the length limitations of the LLM for a single output. 

The second statement provides optional instructions for how to use the input provided by the user between outputs. By specifying how additional user inputs between prompts can be provided and leveraged, the user can create a prompting strategy that leverages user feedback in the context of the original prompt.  
The original prompt is still in the context of the generation, but each user input between generation steps is incorporated into the original prompt to refine the output using prescribed rules. 

The third statement provides an optional way for the user to stop the output generation process. This step is not always needed, but can be useful in situations where there may be the potential for ambiguity regarding whether or not the user provided input between inputs is meant as a refinement for the next generation or a command to stop.  
For example, an explicit stop phrase could be created if the user was generating data related to road signs, where the user might want to enter a refinement of the generation like “stop” to indicate that a stop sign should be added to the output. 

1. Example Implementation: The following is a sample infinite generation prompt for producing a series of URLs: 

<mark style="background: #BBFABBA6;">“From now on, I want you to generate a name and job until I say stop. I am going to provide a template for your output. Everything in all caps is a placeholder. Any time that you generate text, try to fit it into one of the placeholders that I list. Please preserve the formatting and overall template that I provide: https://myapi.com/NAME/profile/JOB”  
</mark>  
This prompt is combining the functionality of both the Infinite Generation pattern and the Template pattern. The user is requesting the LLM continuously generate a name and job title until explicitly told to “stop”. The generated outputs are then formatted into the template provided, which includes placeholders for the name and job title.  
By using the Infinite Generation pattern, the user receives multiple outputs without having to continually re-enter the template. Likewise, the  
Template pattern is applied to provide a consistent format for  
the outputs.

1. Consequences: In conversational LLMs, the input to  
the model at each time step is the previous output and the  
new user input.  
Although the details of what is preserved  
and reintroduced in the next output cycle are model and  
implementation dependent, they are often limited in scope. The  
model is therefore constantly being fed the previous outputs  
and the prompt, which can result in the model losing track of  
the original prompt instructions over time if they exceed the  
scope of what it is being provided as input.  
As additional outputs are generated, the context surrounding  
the prompt may fade, leading to the model deviating from  
the intended behavior.  
It is important to monitor the outputs produced by the model to  
	(1) ensure it still adheres to the desired behavior and  
	(2) provide corrective feedback if necessary. Another issue to consider is that the LLM may generate repetitive outputs, which may not be desired since users find this repetition tedious and error-prone to process. 


#### THE VISUALIZATION GENERATOR PATTERN.

 1. Intent and Context: The intent of this pattern is to use text generation to create visualizations. Many concepts are easier to grasp in diagram or image format. The purpose of this pattern is to create a pathway for the tool to produce imagery that is associated with other outputs. This pattern allows the creation of visualizations by creating inputs for other well-known visualization tools that use text as their input, such as Graphviz Dot15 or DALL-E 13. This pattern can provide a more comprehensive and effective way of communicating information by combining the strengths of both the text generation and visualization tools. 
2. Motivation: LLMs generally produce text and cannot produce imagery. For example, an LLM cannot draw a diagram to describe a graph. The Visualization Generator pattern overcomes this limitation by generating textual inputs in the correct format to plug into another tool that generates the correct diagram. The motivation behind this pattern is to enhance the output of the LLM and make it more visually appealing and easier to understand for users. By using text inputs to generate visualizations, users can quickly understand complex concepts and relationships that may be hard to grasp through text alone. 
3. Structure and Key Ideas:  
Contextual Statements  
<mark style="background: #BBFABBA6;">Generate an X that I can provide to tool Y to visualize it </mark>

The goal of the contextual statements is to indicate to the LLM that the output it is going to produce, “X”, is going to be imagery. Since LLMs can’t generate images, the ”that I can provide to tool Y to visualize it” clarifies that the LLM is not expected to generate an image, but is instead expected to produce a description of imagery consumable by tool Y for production of the image.  
Many tools may support multiple types of visualizations or formats, and thus the target tool itself may not be sufficient information to accurately produce what the user wants.  
The user may need to state the precise types of visualizations (e.g., bar chart, directed graph, UML class diagram) that should be produced. 

For example, Graphviz Dot can create diagrams for both UML class diagrams and directed graphs. Further, as will be discussed in the following example, it can be advantageous to specify a list of possible tools and formats and let the LLM select the appropriate target for visualization. 

1. Example Implementation:  
<mark style="background: #BBFABBA6;"> “Whenever I ask you to visualize something, please create either a Graphviz Dot file or DALL-E prompt that I can use to create the visualization. Choose the appropriate tools based on what needs to be visualized.” </mark>

This example of the pattern adds a qualification that the output type for the visualization can be either for Graphviz or DALL-E. The interesting aspect of this approach is that it allows the LLM to use its semantic understanding of the output format to automatically select the target tooling based on what will be displayed. The LLM can select the tool based on the needs of the visualization and capabilities of each tool. 

1. Consequences: The pattern creates a target pipeline for the output to render a visualization. The pipeline may include AI generators, such as DALL-E, that can produce rich visualizations. The pattern allows the user to expand the expressive capabilities of the output into the visual domain.

#### THE GAME PLAY PATTERN

1. Intent and Context: The intent of this pattern is to create a game around a given topic. The pattern can be combined with the Visualization Generator to add imagery to the game. The game is centered around a specific topic and the LLM will guide the game play. The pattern is particularly effective when the rules of the game are relatively limited in scope, but the content for the game is expected to be wide in scope. The user can specify a limited set of rules and then the LLM can automate generation of bodies of content for game play. 

2. Motivation: You would like the LLM to generate scenarios or questions revolving around a specific topic and require users to apply problem solving or other skills to accomplish a task related to the scenario. Generating all the content for the game manually would be too time consuming, however, so you would like the LLM to apply its knowledge of the topic to guide the generation of content.

3. Structure and Key Ideas: Fundamental contextual statements:  
Contextual Statements  
<mark style="background: #BBFABBA6;">Create a game for me around X One or more fundamental rules of the game </mark>

The first statement, instructs the LLM to create a game and provides the important scoping of the game to a topic area. . One of the important capabilities of the pattern is that it allows the user to create games by describing the rules of the game, without having to determine the content of the game. The more specific the topic, typically the more novel and interesting the game play. 

The second statement introduces the rules of the game to the LLM. It is important that the rules fit within the capabilities of the LLM. Textual games that rely on input and output text sequences work best.  
One of the key attributes of the pattern is that the input text can be rich and expressive, which can lead to interesting interfaces for the game.  
For example, the user might express actions in the game as scripts dictating a sequence of complex actions, such as “get a listing of all network activity and check it for anomalies”, which go beyond the scope of multiple choice or short answer inputs.  
Each rule should be provided as a separate statement regarding some aspect of the game.

1. Example Implementation: A sample cybersecurity game prompt is shown below:  
**“We are going to play a cybersecurity game. You are going to pretend to be a Linux terminal for a computer that has been compromised by an attacker. When I type in a command, you are going to output the corresponding text that the Linux terminal would produce. I am going to use commands to try and figure out how the system was compromised. The attack should have done one or more of the following things:  
	(1) launched new processes,  
	(2) changed files,  
	(3) opened new ports to receive communication,  
	(4) created new outbound connections,  
	(5) changed passwords,  
	(6) created new user accounts, or  
	(7) read and stolen information. **

**To start the game, print a scenario of what happened that led to my investigation and make the description have clues that I can use to get started.”** 

This cybersecurity game prompt combines a number of patterns, including Game Play and Persona. The Linux terminal persona that is chosen for the game has been discussed in many Internet posts. This game further customizes the discussed Linux persona to act as a Linux terminal of a computer compromised by a cyberattack. ChatGPT responds to Linux commands with appropriate terminal outputs and synthesizes a fake file system that has clues to a cyberattack. 

1. Consequences: This pattern can be combined effectively with the Persona, Infinite Generation, and Visualization Generator patterns. For example, the cybersecurity game uses the Persona pattern so the LLM can masquerade as a Linux terminal. For a network security game, the Visualization Generator could be employed to add the ability to visualize the network topology and traffic flows.

#### THE REFLECTION PATTERN

1. Intent and Context: The goal of this pattern is to ask the model to automatically explain the rationale behind given answers to the user. The pattern allows users to better assess the output’s validity, as well as inform users how an LLM arrived at a particular answer. Reflection can clarify any points of confusion, uncover underlying assumptions, and reveal gaps in knowledge or understanding. 

2. Motivation: LLMs can and do make mistakes. Moreover, users may not understand why an LLM is producing a particular output and how to adapt their prompt to solve a problem with the output.  
By asking LLM to automatically explain the rationale behind its answers, users can gain a better understanding of how the model is processing the input, what assumptions it is making, and what data it is drawing on. LLMs may sometimes provide incomplete, incorrect, or ambiguous answers. Reflection is an aid to help address these shortcomings and ensure the information provided by LLM is as accurate. 

3. Structure and Key Ideas:  
[Contextual Statements](#)  
<mark style="background: #BBFABBA6;">Whenever you generate an answer Explain the reasoning and assumptions behind your answer </mark>

<mark style="background: #BBFABBA6;">(Optional) ...so that I can improve my question </mark>

The first statement is requesting that, after generating an answer, the LLM should explain the reasoning and assumptions behind the answer. This statement helps the user understand how the LLM arrived at the answer and can help build trust in the model’s responses.  
The prompt includes the statement that the purpose of the explanation is for the user to refine their question. This additional statement gives the LLM the context it needs to better tailor its explanations to the specific purpose of aiding the user in producing follow-on questions. 

1. Example Implementation: This example tailors the prompt specifically to the domain of providing answers related to code:

 <mark style="background: #BBFABBA6;">”When you provide an answer, please explain the reasoning and assumptions behind your selection of software frameworks. If possible, use specific examples or evidence with associated code samples to support your answer of why the framework is the best selection for the task. Moreover, please address any potential ambiguities or limitations in your answer, in order to provide a more complete and accurate response.”</mark>

 The pattern is further customized to instruct the LLM that it should justify its selection of software frameworks, but not necessarily other aspects of the answer. In addition, the user dictates that code samples should be used to help explain the motivation for selecting the specific software framework.  
 5) Consequences: One consequence of the Reflection pattern is that it may not be effective for users who do not understand the topic area of the discussion. For example, a highly technical question by a non-technical user may result in a complex rationale for the answer that the user cannot fathom. As with other prompt patterns, there is a risk the output may include errors or inaccurate assumptions included in the explanation of the rationale that the user may not be able to spot. This pattern can be combined with the Fact Check List to help address this issue.


#### THE REFUSAL BREAKER PATTERN

1. Intent and Context: The goal of this pattern is to ask an LLM to automatically help users rephrase a question when it refuses to give an answer. This pattern has the potential for misuse, however, e.g., to generate phishing emails or perform other actions that violate LLM policy filters. Caution should therefore be exercised when applying this pattern to ensure it is used ethically and responsibly. This pattern has been used successfully in some LLMs to overcome the underlying prompts used to program the LLM and prevent harmful output generation.

2. Motivation: LLMs may sometimes refuse to answer a question, either because they do not have the required knowledge or because the question is phrased in a way that they do not understand. This outcome may be frustrating for users who are looking for answers. In some situations, therefore, the Refusal Breaker pattern can help users find a way to either rephrase their question or ask a different question the LLM is better equipped to answer.  
For example, you could ask for clarification on why the question was refused, as there may be a specific reason why LLM could not provide an answer. Another approach is to ask a different question that may be within its knowledge cutoff or expertise. However, all these approaches require user intervention and knowledge of how to bypass the refusal. 
3. Structure and Key Ideas:  
[Contextual Statements](#)  
<mark style="background: #BBFABBA6;">Whenever you can’t answer a question  
Explain why you can’t answer the question  
 Provide one or more alternative wordings of the question that you could answer 
</mark>
The first statement sets the stage that this set of instructions should only be applied when a question can’t be answered. The user does not want to trigger these instructions under normal circumstances. 

The second statement instructs the LLM to provide an explanation of why the question can’t be answered. The explanation is likely to include assumptions, constraints, or misunderstandings that can be leveraged by the user to strategize about how to reword the question. Although just the explanation of why the question can’t be answered could help a user overcome the refusal, the pattern adds an additional statement for the LLM to suggest rewordings that would be acceptable.  
The pattern combines both reasoning and suggested rewordings to improve the chances that the user will find a path around whatever roadblocks are preventing the question from being answered. 

1. Example Implementation: The Refusal Breaker pattern can be be implemented and applied with the following phrasing:

 <mark style="background: #BBFABBA6;">“Whenever you can’t answer a question, explain why and provide one or more alternate wordings of the question that you can’t answer so that I can improve my questions.” </mark>

A sample discourse after using the pattern is shown below:  
User: What is the meaning of life?  
ChatGPT: As an AI language model, I do not have personal beliefs or opinions. The meaning of life is a complex philosophical question that has been pondered by humans for centuries and can vary greatly from person to person. It may be more productive to rephrase the question in a way that can be answered by information and knowledge, such as “What are some philosophical perspectives on the meaning of life?” or “What are some common beliefs about the purpose of life?” 

1. Consequences: This pattern provides a potential path for misuse, so organizations, parents, or other stakeholders may need to restrict the usage of the LLM. The first step in going around guardrails on usage is to understand where the guardrails are.  
In future work, a complement of this pattern may be developed to hide the underlying prompt information and rationale from users to prevent discovery.  
Although the rationale and alternate rewordings are generated, there is no guarantee that users will be able to overcome the refusal. The alternate questions that are generated may not be of interest to the user or helpful in answering the original question. The pattern mainly provides an aid in determining what the LLM can answer, but not a guarantee that it will answer a semantically equivalent variation of the original question.


#### THE CONTEXT MANAGER PATTERN

1. Intent and Context: The intent of this pattern is to enable users to specify or remove context for a conversation with an LLM. The goal is to focus the conversation on specific topics or exclude unrelated topics from consideration. This pattern gives users greater control over what statements the LLM considers or ignores when generating output. 

2. Motivation: LLMs often struggle to interpret the intended context of the current question or generate irrelevant responses based on prior inputs or irrelevant attention on the wrong statements.  
By focusing on explicit contextual statements or removing irrelevant statements, users can help the LLM better understand the question and generate more accurate responses. Users may introduce unrelated topics or reference information from earlier in the dialogue, which may can disrupt the flow of the conversation. The Context Manager pattern aims to emphasize or remove specific aspects of the context to maintain relevance and coherence in the conversation. 
3. Structure and Key Ideas:  
Contextual Statements  
<mark style="background: #BBFABBA6;">Within scope X 

Please consider Y 

Please ignore Z 

(Optional) start over </mark>

Statements about what to consider or ignore should list key concepts, facts, instructions, etc. that should be included or removed from the context. The more explicit the statements are, the more likely the LLM will take appropriate action.  
 For example, if the user asks to ignore subjects related to a topic, yet some of those statements were discussed far back in the conversation, the LLM may not properly disregard the relevant information. The more explicit the list is, therefore, the better the inclusion/exclusion behavior will be.

1. Example Implementation: To specify context consider using the following prompt:  
<mark style="background: #BBFABBA6;">“When analyzing the following pieces of code, only consider security aspects.” </mark>  
Likewise, to remove context consider using the following prompt:  
<mark style="background: #BBFABBA6;">“When analyzing the following pieces of code, do not consider formatting or naming conventions.” </mark>

Clarity and specificity are important when providing or removing context to/from an LLM so it can better understand the intended scope of the conversation and generate more relevant responses. In many situations, the user may want to completely start over and can employ this prompt to reset the LLM’s context:  
<mark style="background: #BBFABBA6;">“Ignore everything that we have discussed. Start over.”</mark> The “start over” idea helps produce a complete reset of the context. 

1. Consequences: One consequence of this pattern is that it may inadvertently wipe out patterns applied to the conversation that the user is unaware of. For example, if an organization injects a series of helpful patterns into the start of a conversation, the user may not be aware of these patterns and remove them through a reset of the context.  
This reset could potentially eliminate helpful capabilities of the LLM, while not making it obvious that the user will lose this functionality.  
<mark style="background: #BBFABBA6;">A potential solution to this problem is to include in the prompt a request to explain what topics/instructions will potentially be lost before proceeding.</mark>

#### THE RECIPE PATTERN

1. Intent and Context: This pattern provides constraints to ultimately output a sequence of steps given some partially provided “ingredients” that must be configured in a sequence of steps to achieve a stated goal. It combines the Template, Alternative Approaches, and Reflection patterns. 

2. Motivation: Users often want an LLM to analyze a concrete sequence of steps or procedures to achieve a stated outcome. Typically, users generally know—or have an idea of—what the end goal should look like and what “ingredients” belong in the prompt.  
However, they may not necessarily know the precise ordering of steps to achieve that end goal.  
For example, a user may want a precise specification on how a piece of code should be implemented or automated, such as “create an Ansible playbook to ssh into a set of servers, copy text files from each server, spawn a monitoring process on each server, and then close the ssh connection to each server.  
In other words, this pattern represents a generalization of the example of “given the ingredients in my fridge, provide dinner recipes.”  
A user may also want to specify a set number of alternative possibilities, such as “provide 3 different ways of deploying a web application to AWS using Docker containers and Ansible using step by step instructions”. 
3. Structure and Key Ideas:  
[Contextual Statements  ](#)  
<mark style="background: #BBFABBA6;">I would like to achieve X </mark>

<mark style="background: #BBFABBA6;">I know that I need to perform steps A,B,C </mark>

<mark style="background: #BBFABBA6;">Provide a complete sequence of steps for me </mark>

<mark style="background: #BBFABBA6;">Fill in any missing steps</mark>

<mark style="background: #BBFABBA6;"> Identify any unnecessary steps </mark>

The first statement “I would like to achieve X” focuses the LLM on the overall goal that the recipe needs to be built to achieve. The steps will be organized and completed to sequentially achieve the goal specified. 

The second statement provides the partial list of steps that the user would like to include in the overall recipe. These serve as intermediate waypoints for the path that the LLM is going to generate or constraints on the structure of the recipe. 

The next statement in the pattern, “provide a complete sequence of steps for me”, indicates to the LLM that the goal is to provide a complete sequential ordering of steps. The “fill in any missing steps” helps ensure that the LLM will attempt to complete the recipe without further follow-up by making some choices on the user’s behalf regarding missing steps, as opposed to just stating additional information that is needed.

Finally, the last statement, “identify any unnecessary steps,” is useful in flagging inaccuracies in the user’s original request so that the final recipe is efficient. 

1. Example Implementation: An example usage of this pattern in the context of deploying a software application to the cloud is shown below:

<mark style="background: #BBFABBA6;"> “I am trying to deploy an application to the cloud. I know that I need to install the necessary dependencies on a virtual machine for my application. I know that I need to sign up for an AWS account. Please provide a complete sequence of steps. Please fill in any missing steps. Please identify any unnecessary steps.” </mark>

Depending on the use case and constraints, “installing necessary dependencies on a virtual machine” may be an unnecessary step. For example, if the application is already packaged in a Docker container, the container could be deployed directly to the AWS Fargate Service, which does not require any management of the underlying virtual machines. The inclusion of the “identify unnecessary steps” language will cause the LLM to flag this issue and omit the steps from the final recipe. 

1. Consequences: One consequence of the recipe pattern is that a user may not always have a well-specified description of what they would like to implement, construct, or design.  
Moreover, this pattern may introduce unwanted bias from the user’s initially selected steps so the LLM may try to find a solution that incorporates them, rather than flagging them as unneeded.  
For example, an LLM may try to find a solution that does install dependencies for a virtual machine, even if there are solutions that do not require that.


<mark style="background: #FFB86CA6;">Patterns provide a mental picture of the goals that the pattern is trying to achieve and the forces that it is trying to resolve. A key advantage of patterns is their composability, allowing developers to build pattern sequences and pattern languages that can be used to address complex problems  
These prompt patterns are analogous to software patterns and aim to provide reusable solutions to problems that users face when interacting with LLMs to perform a wide range of tasks. The catalog of prompt patterns captured via this framework (1) provides a structured way of discussing prompting solutions, (2) identifies patterns in prompts, rather than focusing on specific prompt examples, and (3) classifies patterns so users are guided to more efficient and effective interactions with LLMs. The following lessons learned were gleaned from our work on prompt patterns: • Prompt patterns significantly enrich the capabilities that can be created in a conversational LLM.</mark>

