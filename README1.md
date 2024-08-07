# Welcome to ReByte

<figure><img src=".gitbook/assets/1.png" alt=""><figcaption></figcaption></figure>

## What is ReByte?

ReByte is your team assistant that helps you to create your own AI-powered applications without needing too much coding skills. On ReByte, you can create various types of applications and publish them for your own personal use, or for the team to use.

ReByte is a platform that allows everyone to quickly develop their AI-powered applications without needing too much coding skill. On ReByte, anyone with or without programming experiences, can create various types of applications and publish them for their own personal use, or for the team to use.

## Rationale behind ReByte

Previously, software development is a process that requires a lot of coding skills. But with the rise of **Language Models** \(LMs\), we are able to build software tools that can understand human intentions and generate code automatically. This is a huge step forward in software development, because it allows us to build software tools without needing to write too much code.

This will open the hood of software development to a much larger group of people. Everyone can use their personal computers to create their **personal** software tools. Every company can use their private data to create their **personal** software tools for internal or external uses.

**ReByte** is built with one mission: to give everyone the ability to create their own software tools without needing too much coding skills.

In terms of functionality, **ReByte** has some core components:

* Language Model Tool: A serverless function that can be executed on cloud. Those functions usually use LLMs to perform some tasks, but it's not required.
* Knowledge: Private data ingestion pipeline that feed data to ReByte system, later can be used by LLM tools.
* App Builder: User interface builder that allows developers to wire up LLM tools and knowledge to create their own tools.

Also, **ReByte** is built to solve the following problems in LLM application development:

1. **Predicable LLM application**: It works on the principle of treating each LLM interaction as a single step or functional transformation on working memory, offering a predictable and manageable way to guide the thought process of a LLM. This approach results in consistent, easier-to-follow interaction flows.
2. **Iterative Nature of LLM Development**: Creating tools on top of modern LLM models can be quite challenging, due to the nature of LLMs. LLMs' output are not deterministic, and their performance can vary from time to time. We want ReByte's LLM agent builder to make this process as easy as possible.
   * We provide a unified interface for users to build, test and deploy their LLM application.
   * We also keep logs of the application, so that users can easily fix the bugs when things go wrong.
3. **Painless Private Data integration**: Today's LLM tools heavily rely on private data. Frameworks such as Langchain and LlamaIndex, together with various vector databases, provide the necessary pieces for private data embedding and search. But even for someone experiences in coding and engineering, it's hard to get the system running the first time, and usually takes hours to debug. That's why we want to make this data integration process as easy and painless as possible.
   * We provide a hosted solution for users to import data from popular data sources, such as Notion, Google, GitHub, etc., as well as from user's local computers.
   * We handle data source synchronization automatically, so users don't need to worry about data consistency.
4. **Production Serving Ready**: Provide a robust runtime ready for immediate deployment and scalable growth.
   * It's rather hard to scale LLM applications, because of its unpredictable and asynchronous nature.
   * Being inspired by serverless functions, we provide a scalable runtime for users to scale their LLM applications without having to know the details of the underlying infrastructure.
5. **Deliver Tool instead of Prompt**: LLM applications are meant to be ready-to-use tools, not just prompts. We make sure that users can deliver their LLM applications as actual tools, instead of prompts.

At its core, ReByte defines an **Tool DSL** as an intermediate representation of any LLM application, and provides a hosted runtime for users to execute their LLM applications. Introduction to Tool DSL has obvious benefits:

* can be used to build a GUI builder for users to create their own LLM application.
* can be generated by fine-tuned models
* can be edited by human