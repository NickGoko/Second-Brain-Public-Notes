---
id: 82510c19-2f04-48e6-ab0f-df2531385208
---

# A Deep Dive into OpenTelemetry. Part 1: An in-depth exploration into… | by Eromosele Akhigbe | Mar, 2024 | AWS in Plain English
#Omnivore

[Read on Omnivore](https://omnivore.app/me/a-deep-dive-into-open-telemetry-part-1-an-in-depth-exploration-i-18e47469962)
[Read Original](https://aws.plainenglish.io/opentelemetry-deep-dive-part-1-6ebbd2362bd3)

## Highlights

> Across the tech horizon, apps are getting more complicated, and keeping an eye on them is becoming more tedious. Finding your way around the different services offered by apps is like trying to find your way through a big maze filled with errors that are hard to identify. [⤴️](https://omnivore.app/me/a-deep-dive-into-open-telemetry-part-1-an-in-depth-exploration-i-18e47469962#d9412003-5377-42ed-b058-74594ceef021)  ^d9412003

> For a while, it was tough to monitor these complex apps. The usual methods just couldn’t keep up with how much these apps were growing. It created a situation where problems stayed hidden, causing a lot of confusion for digital operations. [⤴️](https://omnivore.app/me/a-deep-dive-into-open-telemetry-part-1-an-in-depth-exploration-i-18e47469962#fff2be7c-3edf-4d6a-b27b-fcb362c10c81)  ^fff2be7c

> observability software [⤴️](https://omnivore.app/me/a-deep-dive-into-open-telemetry-part-1-an-in-depth-exploration-i-18e47469962#8782c4cd-40d8-4761-905a-58830223ca8a)  ^8782c4cd

> showed up and changed the game. It takes on the tough job of keeping an eye on things, breaking down the complicated parts, and showing us a clear picture of what’s going on in the applications. [⤴️](https://omnivore.app/me/a-deep-dive-into-open-telemetry-part-1-an-in-depth-exploration-i-18e47469962#6a8169f4-b964-4f89-a19c-d83566b6f02f)  ^6a8169f4

> Observability is the ability to understand the internal state of a system by examining its outputs. [⤴️](https://omnivore.app/me/a-deep-dive-into-open-telemetry-part-1-an-in-depth-exploration-i-18e47469962#7b2ea50e-9ac1-45ba-8dd5-f4122bdd0370)  ^7b2ea50e

> Usually, people mistake monitoring for observability, but there is a clear difference. In simple terms, monitoring is used for accessing the health of the application while observability is doing something about that assessment. [⤴️](https://omnivore.app/me/a-deep-dive-into-open-telemetry-part-1-an-in-depth-exploration-i-18e47469962#84ba83f4-f52d-4e7c-89f1-c22becdbff8b)  ^84ba83f4

> “three pillars of observability” — metrics, logs, and traces [⤴️](https://omnivore.app/me/a-deep-dive-into-open-telemetry-part-1-an-in-depth-exploration-i-18e47469962#50ea39bb-a3b9-482a-88d2-941ed738ccde)  ^50ea39bb

> introduced a broader framework called TEMPLE, which stands for traces, events, metrics, profiles, logs, and exceptions. [⤴️](https://omnivore.app/me/a-deep-dive-into-open-telemetry-part-1-an-in-depth-exploration-i-18e47469962#fc6d24c1-ac55-4b49-9c8e-6cf7479900a0)  ^fc6d24c1

> **OpenTelemetry is an observability framework designed to help developers and operators better understand the behavior and performance of their software applications.** It provides a set of APIs, libraries, agents, instrumentation, and instrumentation standards to enable the collection of telemetry data such as traces, metrics, and logs. [⤴️](https://omnivore.app/me/a-deep-dive-into-open-telemetry-part-1-an-in-depth-exploration-i-18e47469962#81240a5c-c95a-4a67-a8b4-d5ac0e19a605)  ^81240a5c

> ## History of OpenTelemetry
> 
> OpenTelemetry came about as a convergence of two projects, _OpenTracing_ and _OpenCensus_.
> 
> OpenTracing was an open-source project developed by Ben Sigelman and some other contributors, their primary goal was to create a standard for distributed tracing, allowing developers to instrument their code to capture and visualize traces across microservices.
> 
> OpenCensus on the other hand, was created by Google and some other companies to provide a standardized approach to collect metrics and traces from applications.
> 
> In 2019 they decided to merge and form OpenTelemetry, after realizing their goals were the same. From then on, OpenTelemetry has experienced rapid growth in terms of community contributions, with support from major cloud providers, observability vendors, and individual developers. [⤴️](https://omnivore.app/me/a-deep-dive-into-open-telemetry-part-1-an-in-depth-exploration-i-18e47469962#2c8e263f-d05f-4aca-8cc2-c3b30c5832a9)  ^2c8e263f

> ## Let’s look at some Concepts of OpenTelemetry:
> 
> 1. **Observability**: Observability refers to the ability to gain insights into the internal state, behavior, and performance of applications by collecting and analyzing telemetry data. Here’s how observability functions as a core component within OpenTelemetry:
> * **_Data Collection Across Multiple Signals:_** OpenTelemetry aims to provide a holistic view of a system by collecting data from various signals or telemetry types. These include traces, metrics, logs, events, profiles, and exceptions. Each of these signals contributes unique information about the application’s behavior.
> * T**_races for Distributed Tracing:_** Traces, a significant component of observability in OpenTelemetry, enable the visualization and tracking of a request or transaction as it traverses through different services and components in a distributed system. Traces provide a chronological sequence of events, allowing developers and operators to identify performance bottlenecks, latency issues, and the overall flow of requests.
> * **_Metrics for Quantitative Measurements:_** OpenTelemetry captures metrics, which are quantitative measurements representing various aspects of the application’s performance and behavior. Metrics offer a numerical view of resource usage, error rates, and other critical indicators. These metrics contribute to the overall observability by providing insights into the application’s health and efficiency.
> * **_Logs for Detailed Information:_** Logs in OpenTelemetry provide detailed information about events and activities within the application. While traces and metrics offer structured and quantitative data, logs provide a more in-depth, contextual understanding of specific events, errors, or activities. This helps in detailed troubleshooting and investigation.
> * **_Events for External Changes:_** Events, as part of OpenTelemetry’s observability framework, capture external changes that can impact the system, such as deployments, configuration changes, or experiments. These events, when integrated into the observability platform, contribute to a more comprehensive understanding of the system’s behavior in response to external stimuli.
> * **_Profiles for In-Depth Analysis:_** OpenTelemetry introduces profiles, a telemetry type that focuses on in-depth analysis and optimization of application performance. Profiles consist of stack traces associated with specific metrics, providing a powerful tool for developers dealing with performance and efficiency optimizations.
> * **_Exceptions for Error Analysis:_** Exceptions, another crucial component of observability in OpenTelemetry, capture and analyze errors within the application. Exception telemetry includes stack traces, error messages, and contextual information, aiding in the rapid identification and resolution of issues. [⤴️](https://omnivore.app/me/a-deep-dive-into-open-telemetry-part-1-an-in-depth-exploration-i-18e47469962#bc4b6c35-f6f7-4297-89a9-f637276b6d65)  ^bc4b6c35

> 2\. **Span:** In OpenTelemetry, a “span” is a fundamental unit of work or operation within a distributed system, essential for understanding and monitoring the flow of requests or transactions. Spans encapsulate specific activities, such as an HTTP request, database query, or any meaningful operation, and are organized in a hierarchical structure to represent parent-child relationships. [⤴️](https://omnivore.app/me/a-deep-dive-into-open-telemetry-part-1-an-in-depth-exploration-i-18e47469962#edd24fc2-d150-4c6b-80ce-0990648840b4)  ^edd24fc2

> 3\. **Context Propagation:** To explain this concept allow me to use an analogy, Imagine planning a surprise party with friends. Each friend has a job — decorations, cake, invitations. You send a special message (context) with the plan details. As friends work on their tasks, they pass along this message. Even though they only know their part, the message ensures everyone is on the same page, making it easier to coordinate. In tech, this is context propagation — passing information as tasks move through different parts of a system. [⤴️](https://omnivore.app/me/a-deep-dive-into-open-telemetry-part-1-an-in-depth-exploration-i-18e47469962#f272a5cd-5e9a-4d47-822a-9f2a464d7718)  ^f272a5cd

> 5\. **Instrumentation:** To introduce observability into a system or process, it must be first instrumented. Code from the system components should produce metrics, traces, and logs. [⤴️](https://omnivore.app/me/a-deep-dive-into-open-telemetry-part-1-an-in-depth-exploration-i-18e47469962#21020ee5-5379-49c6-bedb-a1e1273f6b93)  ^21020ee5

> 8\. S**ampling:** Sampling in OpenTelemetry refers to the process of selecting a subset of telemetry data for collection and analysis, rather than capturing every single event or trace. Sampling helps manage the volume of telemetry data generated by applications, reducing overhead and storage costs while still providing meaningful insights into system behavior. [⤴️](https://omnivore.app/me/a-deep-dive-into-open-telemetry-part-1-an-in-depth-exploration-i-18e47469962#34ab4393-24c3-4c2e-88b5-f6afa4f78c46)  ^34ab4393

