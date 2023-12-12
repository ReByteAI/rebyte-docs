# Chatbot


## Introduction
ReByte provide a universal protocal for ChatBot UI. This protocal is flexible and scalable, which is why it is suitable to build UI for various ChatBots.

## Feature
- Multi-round conversation, a.k.a. Long-term-memory. ChatBot UI can track chat history and use it to provide more content information.

Chat will send the messages along with other information to the Agent, using this format:

| parameter          | description                                                  |
|--------------------|--------------------------------------------------------------|
| role               | "user" for user's messages, "assistant" for agent's response |
| content            | the message content                                          |
| context            | environmental variables(if there is any)                     |
| context.files      | files uploaded by user                                       |
| context.files.uuid | id of the uploaded file                                      |
| context.files.name | name of the uploaded file                                    |


```json
{
"message":[
  {
    "role": "user",
    "content": "content",
    "context": {
      "files": [
        {
          "uuid": "f3610fef-f490-4675-81fe-df04735f5058",
          "name": "resume.pdf"
        },
        {
          "uuid": "59986165-bead-485c-a453-30b03e366a39",
          "name": "bp.pdf"
        }
      ]
    }
  }
]
}
```

- Rich UI styles - You can use various styles to build ChatBot UI, for example: input, toggle list, drag down menu and so on.
Please use this format:

```json
input type: use to genearte html input
example json: 
{
    type: "input",
    title: "Username",
    field: "username",
    value: "",
    props: {
      placeholder: "hi",
    }
}

radio type: use to generae html radio button
example json:
{

    type: "radio",
    title: "Notify me about...",
    field: "type",
    value: "all",
    options: [
      { value: "all", label: "All new messages" },
      { value: "mentions", label: "Direct messages and mentions" },
      { value: "none", label: "Nothing" },
    ],
}

checkbox type: use for multiple select
example json:
 {
    type: "checkbox",
    title: "Items",
    field: "items",
    value: ["recents", "home"],
    options: [
      { value: "recents", label: "Recents" },
      { value: "home", label: "Home" },
      { value: "applications", label: "Application" },
    ],
  },
  
  select type: select from one many options
  {
    type: FormFieldTypes.SELECT,
    title: "Email",
    field: "email",
    value: "m@example.com",
    options: [
      { value: "m@example.com", label: "m@example.com" },
      { value: "m@google.com", label: "m@google.com" },
      { value: "m@support.com", label: "m@gsupport.com" },
    ],
    props: {
      placeholder: "Select a verified email to displa",
    },
  },
  ```