# ReByte User Guide

## Available Platform

[Desktop](https://rebyte.ai) | [Mobile]("https://apps.apple.com/app/rebyte-your-team-assistant/id6466730972")

## Unified Assistant Interface For Your Team

**Revia** is our codename for universal user interface that can be used by all team members to interact with the AI assistant. This interface is designed to handle various types of tasks, such as data retrieval, question and answer, document generation, and data analysis, and more advanced tasks such as interactive chart and table, form filling and more.

Besides Revia, team admin can build other assistants specific to some use cases, for example, a customer support assistant, a sales assistant, a marketing assistant, etc.

The relationship between **Super Assistant** and **Other Assistants** is like the relationship between **Team ChatGPT** and **Team Specific Gpts**.

In terms of functionality, **Super Assistant** is no different from other assistants, the only difference is that **Super Assistant** is always shown on the top of the assistant list, and it's available for all team members.

## For Team Builder and Admin


### Configure Team Assistant
Only builders or admin in your team can configure the team assistant. 

Each assistant, including **Revia**, contains:
* **Planner**: can plan and execute a sequence of tools to achieve a specific goal.
* **Code Sandbox**: Handle arbitrary code execution, such as data analysis, data visualization, etc. 
* **List of ReByte Tools**: a list of ReByte Tools that can be used by the assistant. Tool can be built by your team or by other tool builders, or by ReByte team.

**Planner** and **Code Sandbox** can be optional. In that case, user has to ask specific tool to perform a specific task.


## For Team Member

### Interacts with Revia

* **Directly Ask Questions**: You can ask questions to Revia, such as "What is the sales number of last year?" or "How many employees do we have in the company?"
* **@specific tool**: A noval way to interact with ReByte, you can @mention a specific tool to perform a specific task, for example, "@image_generator generates an image of a cat."
* **/command**: You can use slash commands to invoke other assistants, for example, "/customer_support"

### Attachment files
* You can attach files to your message, we support various file types, such as csv, xlsx, PDF, docx, png, jpg, etc. ReByte will automatically parse the file and extract the content for further processing.

### Reasoning Steps
Hallucination is a common issue in AI assistants,
ReByte tries to solve this issue by providing reasoning steps as detail as possible,
user can see the reasoning steps of each tool.
Builder can also see the actual tool running log to debug if there's any issue.

### Code Sandbox
ReByte planner iteratively writes/executes code in the code sandbox to achieve the goal.
This is super useful to do things like data analysis, numerical computation, etc. Code execution environment is isolated for each user iteration.

### Language that the assistant uses
You can control the language that the assistant uses to communicate with you.  
go to 'user settings' -> 'language' to change the language.

## Hallucination
Hallucination is a common issue in AI assistants. In our system, we try to solve these issues in the following ways:

* **Automate small steps**: We're **NOT** planning to do giant multiple steps reasoning, we do small steps planning at one time, and achieve the final goal iteratively under the guidance of the user.
* **Reasoning Steps**: We show the reasoning steps on Assistant UI, so user can see how the assistant comes up with the answer. 
* **Tool Run logs**: Builder can see the actual tool running log to debug if there's any issue. Tool run contains the input data, the output data, and every step that the tool takes to achieve the goal.
* **Show original data**: We show the original data that the tool uses to generate the answer, so user can see if the data is correct. This is particularly useful for structured data. We will show exact data coming from user's database, so user knows if LLM provides the correct answer based on the data.