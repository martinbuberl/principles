# Trustpilot's Engineering Principles

- **[Code Review Everything](#code-review-everything)**
- **[Services First](#services-first)**
- **[Serverless First](#serverless-first)**
- **[Build smaller things](#build-smaller-things)**
- **[Encapsulate in contexts and expose APIs](#encapsulate-in-contexts-and-expose-apis)**
- **[Aim to Open Source](#aim-to-open-source)**
- **[Measure it and you can improve it](#measure-it-and-you-can-improve-it)**


> **Breaking the Rules**
> *Remember that all principles are generally meant as rules of Trustpilot Tech. If a particular principles isn’t appropriate to your situation - escalate it to your manager to explore alternatives, but this shouldn’t be the norm. Always use your common sense and best judgement.*

## Code Review Everything

All production code must be reviewed, even the most trivial. Commits should be optimized for code reviews and tell a story. “Pre-review” your code before requesting a review from your peers. Review requests should be handled promptly. Pairing for infrastructure or configuration changes is recommended. While the reviewer’s input is welcomed, in the end the author decides what suggestions to implement.

*We do this because we believe that code reviews are an imperative tool to ship quality code. This includes finding issues with the code, but also sharing alternative approaches and learning new practices. It is also great to share knowledge, so that always more than just one person knows what happened. Simple changes usually require very little reviewing effort so try to take “everything” literally. And even small changes can have very negative impacts.*

## Services First

If there are 3rd party services (SaaS) that solve a problem - or most of it, we prefer using those.
If those services are not good enough - or too expensive, we will research and use appropriate open source libraries. Only if that option doesn’t exist either, we build it ourselves.

*We do this because we don’t want to reinvent the wheel every time we need a new service or library - focusing on our core business. On top of that, those service providers are experts in their domain and their services are battle tested by multiple customers. We usually can’t outperform them on multiple levels (e.g. cost, features, quality, time to market). Consider extending an existing open source library before building it from scratch yourself if parts are missing.*

## Serverless First

If Serverless is not available or practical, containers are recommended.
Virtual servers are considered legacy and should be avoided.

*We do this because we strongly believe that Serverless (FaaS, BaaS, DBaaS) is the future of the cloud and we’d like to be on the forefront of that movement. Serverless might not necessarily be the right choice for everything today, but start your architecture discussions there. We’re in the process of fading out virtual servers and want to avoid creating new ones. The benefits of Serverless and containers over virtual servers are diverse: simplified and faster autoscaling, better service orchestration, reduction of cloud service costs, reduction of operational costs and modernizing our cloud stack.*

## Build smaller things

Generally consider making smaller rather than larger systems, services, repositories, etc.

*When building small, the project is easier to reason about, and the responsibility of a service is more clearly defined. It is easier to fix bugs, and easier to deploy.*
*While there may be an overhead by making things too small, we have generally found that it’s much easier to combine things that are too small, than to take things apart that are too large. Combining is easier than splitting.*
*It is perfectly fine to have multiple services and projects from the same context be in multiple repositories.*

## Encapsulate in contexts and expose APIs

We divide ownership into contexts. The context concept encapsulates one or more services that are closely connected. The context is also the boundary of data ownership. This means that only services inside the context can directly work with the data it owns. The context exposes REST APIs to be be used by other contexts as well as our customers and third party services. For any API endpoint, consider first if it can be public, if not can it be private and only make it internal if none of the first two are possible.

*We believe that the context concept gives a good abstraction level of coherent services, that allows for full ownership, while allowing ownership to change. At the same time it’s more practical than having individual services as the isolation level. By exposing REST APIs we allow other teams or third parties to interact with and combine our products in new and interesting ways. At the same time we retain control over the underlying data for flexibility of implementation and data storage.*

## Aim to Open Source

Always apply open source best practices to all repositories, public and private ([Inner Source](https://en.wikipedia.org/wiki/Inner_source)). That typically includes a clear documentation (README) and code that isn’t tightly coupled to anything internally. Consider which pieces could be pulled out and open sourced (e.g. a general purpose library without any dependencies is a prime candidate to be open source).

*We do this because code written with open source on mind, is usually cleaner, better documented and not tightly coupled to anything internally. Generally it’s a good sanity check that we’re not doing anything too weird internally. Additionally, open source is a great recruiting tool for us to display our engineering culture.*

## Measure it and you can improve it

We monitor our services, we define service level indicators, objectives and setup alerting if objectives is violated. We react promptly to these alerts when they happen, to improve our service quality or adjust the alerting threshold to reflect reality. Through monitoring and alerting we strive to maintain a high service quality.

*We do this to have factual knowledge that our services works as intended, rather than just a gut feeling or if no customers complains. These measures is a baseline for every change we do to our systems, either to improve performance or adding new features with no quality degradation.*

## Observe your services

Keep a pulse on the services you own. 

*Sometimes generic metrics are enough, sometimes you would need something specific. Too many alerts triggered for your services? Is time to take action. Focus on self-healing and architect with soft dependencies between services.*
