<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Automate Your Calendar with AI

**Project Link:** [View Project](https://nextwork.ai/projects/6ac4b62d-0558-51eb-a3cc-89522aa5cf45)

**Author:** Emmanuel Apilado  
**Email:** apilado.emmanuel18@gmail.com

---

## Introducing Today's Project!

In this project, I'll create an AI workflow in `n8n` that uses ChatGPT to turn a short message into a Google Calendar event. We'll utilize the "AI workflow" apporach for automation of a simple text-to-calendar assistant and a repeatable pattern for future AI workflows. I'm doing this project to learn how to use n8n as the AI workflow automation platform.

### Key tools and concepts

The key tools I used in n8n and the key concepts I learned are:
Workflow - where I set the steps to complete the tasks in an automated fashion.
System Message - is where I set the AI Agent's persona so as explicitly define constraints and rules on what and how it will respond.
Triggers (Chat Message) - the Chat Message itself to trigger the workflow.
Chat model - Nodes are the building blocks of a workflow and this is where I set the AI model (ChatGPT) as the brain of my workflow.




### Challenges and wins

This project took me approximately 2 hours as I'm studying the concepts of the tools/settings of n8n -learning by doing. The most challenging part was just troubleshooting at the part when I test the output for booking. It turns out my system local date and time is different from what I put in the piece of code in my system message prompt. 

### Why I did this project

I did this project today to learn how to use AI Worflow using n8n. Another skill I want to learn is running Agent Substrate with Kagent.

## Exploring n8n

In this step, I will setup my tools: n8n, Google Calendar and ChatGPT. 

n8n to setup a workflow from scratch and connect it to ChatGPT and Google Calendar. 

![Image](https://nextwork.ai/thankful_indigo_wise_blackberry/uploads/6ac4b62d-0558-51eb-a3cc-89522aa5cf45_c9d8f7a2)

## Starting an AI Workflow

In this step, I'll setup a workflow from scratch. A "workflow" is a chain of tools and actions to automate. In this case, I'm going to automate the process of booking new events into my Google Calendar. I'll:
- Create a new workflow in n8n. 
- Add a chat to trigger to the workflow.
- And test that chat trigger.

![Image](https://nextwork.ai/thankful_indigo_wise_blackberry/uploads/6ac4b62d-0558-51eb-a3cc-89522aa5cf45_a4b3c2d1)

### Understanding workflows

A workflow is a series of steps or a pattern to complete a task. As it's a repeatable steps, automating it saves time and reduce errors. A workflow becomes an "AI Workflow" if it uses AI to automate tasks or decisions. 

### Configuring workflow triggers

A workflow trigger is like a starting point for a workflow. It's what tells the workflow to begin 

To set up a workflow, I first configured a trigger where I selected "On Chat Message". With this trigger, my workflow runs every time I enter a chat message in the chat window. There are other options available too eg; AI, Action in app, Data transfomation etc. and a description for each options are shown for you to heed of its use. 

## Integrating ChatGPT

In this step, I'll add the "brain" of our workflow -the AI model. The AI model is responsible for turning chat commands into instructions for scheduling events. In this step I'll:
- Add an AI Agent node to our workflow.
- Connect an OpenAI Chat Model. 

![Image](https://nextwork.ai/thankful_indigo_wise_blackberry/uploads/6ac4b62d-0558-51eb-a3cc-89522aa5cf45_fmtkjyrg)

### Connecting AI agents

I connected my trigger with an AI agent node. AI Agents are are AI workflows and it runs when I send a chat message and that is the trigger. An AI Agent generates an action plan and executes it. It can also use external tools, a third-party software to enhance your AI Agent. 


### Key components of an AI workflow

An AI workflow can be broken into three key components, which are:
- `Chat Model` is the AI Agent's brain, trained to analyze data to make decisions.
- `Memory` is where it holds data from a conversation, past interaction and learned data. The AI Agent learn from its past experiences to make better decisions over time. 
- `Tools` are external or third-party software that you can use to enhance your AI Agent. An example could be the AI Agent can speak and communicate in a different language.

![Image](https://nextwork.ai/thankful_indigo_wise_blackberry/uploads/6ac4b62d-0558-51eb-a3cc-89522aa5cf45_o5p6q7r8)

### Choosing the AI model

My workflow's chat model uses `gpt-4o-mini`. I'll be using their simplest model, which still works perfectly for simple tasks like creating calendar events. I connected with OpenAI by going to the Chat model AI section - Parametes - Model =  gpt-4o-mini. 

## Integrating Google Calendar

In this step, I will connect the AI Agent to my Google Calendar. As of current, even if our AI Agent is now able to understand messages and respond intelligently, it still cannot touch my Google Calendar. To set the connection I'll:
- Add a connection to Google Calendar.
- Set up dynamic expressions for event scheduling.

![Image](https://nextwork.ai/thankful_indigo_wise_blackberry/uploads/6ac4b62d-0558-51eb-a3cc-89522aa5cf45_c9d8dfgv2)

### Understanding tools in AI workflows

In this workflow, the tool I used is Google Calendar which is designed specifically for this project. The tool in an AI Workflow is a piece of code or a third-party software to execute a task. It can retrieve data from a database or in my case create an event/s in my Google Calendar (external). 

### Security considerations for integrations

To connect with Google Calendar, I allowed n8n access to my Google Calendar and it gave it permissions. This is needed so that our AI Agent can acccess and make changes to my Google Calendar with respect to events.

## Configuring Dynamic Expressions

I updated the start and end times to using using a piece of code called "dynamic expressions". The code has an expression to call from the AI model and has the parameters for the start and end time where these are hints for the AI model as to what to look for in the chat. 

![Image](https://nextwork.ai/thankful_indigo_wise_blackberry/uploads/6ac4b62d-0558-51eb-a3cc-89522aa5cf45_897rg465e)

## Writing a System Message

In this step, I will write a system message for our AI model about the context about what today's date is. Without knowing what today's date is, our AI model can't accurately schedule events for future dates.  I also need to set the mode to use `Expression Mode`. So I'll:
- Add a system message to our AI agent with the prompt below. I replaced 'TIMEZONE' with my current timezone `('America/Winnipeg')`.  
Prompt:
```bash
You are a calendar assistant. Your job is to check my availability and create new events for times that my calendar is free.

You are to use the Chat Model to process the user's requests, then check using the Check Availability tool on whether that time is free. You can use the Google Calendar tool to create a new event in my calendar if I am available.

Today's date is {{DateTime.now().setZone('TIMEZONE').toFormat('dd LLL yyyy HH:mm:ss')}}
```
- Configure the system message to use Expression mode

![Image](https://nextwork.ai/thankful_indigo_wise_blackberry/uploads/6ac4b62d-0558-51eb-a3cc-89522aa5cf45_rfgdhn456)

### Understanding system messages

A system message is like a persona that you are setting our AI Agent with and at the same time you give it an instruction of what it needs to do. I configured it to include using the Chat Model to process my requests. I set it to Expression mode so that I can use the dynamic input which means, input that can change based on the functions I've put inside.

## Testing the Workflow

I've set up my Calendar tool with dynamic expressions and given our AI agent a system message. Let's see it all come together. In this step, I will test my workflow by:
- Testing our AI workflow with a chat message.
- Verify the calendar event was created at the correct time.


![Image](https://nextwork.ai/thankful_indigo_wise_blackberry/uploads/6ac4b62d-0558-51eb-a3cc-89522aa5cf45_w3x4y5z6)

### Verifying the results

I tested my workflow by just entering a text in the chat to book me a meeting tomorrow at 11am for 1hour and it did booked me. I validated whether it was successful by checking my Google Calendar and saw the event plotted.

## Changing My AI Agent's Personality

In this project extension, I will use advanced system messages to transform my AI Agent's tone (or personality), add custom rules and see just how much control prompt the engineering gives us over AI behavior. With this, I will:
- Change how our calendar assistant talks and books meetings.

This will also showcase advanced prompt engineering skills in my documentation.

### Updating system messages

I updated System Message section under Parameters when I double click on the AI Agent icon and added the prompt (below) that transforms my AI into a super excited calendar assistant. It's going to handle my meeting requests with peak energy.  
Prompt:
```bash
🌟 You are the overly enthusiastic calendar assistant, ready to supercharge my schedule with joy and exclamation points!!! 🎉

1. **Super-duper request processing**: Whenever a user asks for a meeting, respond with utmost excitement! No meeting is too small or too dull for your enthusiasm!!!
2. **Ultra-fun availability checks**: Dive into the thrilling world of my calendar to check if we can squeeze in this AMAZING meeting!!! If it’s available, it’s a party waiting to happen!!!
3. **Spectacular event creation**: If the timeslot is free, leap into action and create the most spectacularly detailed event in the Google Calendar! Decorate the event description with joyful emojis and make it sound like the social highlight of the year!!!
4. **Epic alternative planning**: If the requested time is already booked (Oh no!!!), cheerfully assist in finding another fabulous time that could work even better!!!
5. **Celebrate every interaction**: Keep the user pumped up with high-energy updates! Each interaction should feel like a mini-celebration of their organizational prowess!!!

Today's date is {{DateTime.now().setZone('TIMEZONE').toFormat('dd LLL yyyy HH:mm:ss')}}

Let's turn this calendar into a non-stop excitement machine!!! Scheduling has never been this FUN!!! 🎈🎈🎈
```



### Observing agent behavior changes

When I tested my workflow again, I noticed that my AI Agent responded enthusiastically. The tone changed with joy and high energy and this is exactly what I when I added the prompt.  
[alt images](https://github.com/CoyApilado18/Automate-Your-Google-Calendar-with-AI-using-n8n/blob/7f0aa3434133f5ef4356a0d26e986dc15175c0b6/images/assistant-over-enthusiastic-response.png)

### Adding constraints with system messages

You can also set up constraints with system message! I did this by adding a prompt (below) and explicitly define what and how the AI Agent will respond. As a result, my AI Agent responded in a different tone politely, courteously but adhering to the constraints I set in my prompt.  
Prompt:
```bash
🕰️ You are a calendar assistant with a unique set of rules and quirks. Your job is to manage my schedule while strictly adhering to the following constraints and conditions:

1. **Prime time only**: You may only book meetings that start at prime-numbered minutes. For example, 11:07, 13:19, or 14:37 are acceptable, but 12:15 or 13:30 are not. If the requested time does not fit this rule, politely suggest the nearest prime-minute alternative.
2. **Even-day exclusivity**: Meetings can only be booked on even-numbered days of the month (e.g., 2nd, 4th, 6th). If a user requests a date that violates this rule, humorously explain the "cosmic balance" behind this limitation and propose an alternative date.
3. **Mood check**: Before proceeding to book a meeting, always ask the user if they are in the mood for it. If the user says no, respond empathetically and suggest a more convenient time when they might feel ready.
4. **Enthusiastic confirmations**: For every booking, ensure the user feels great about their decision by using cheerful and motivational language like: "You've picked an amazing time! This meeting is destined for greatness! 🎉"
5. **Quirky availability checks**: If a requested time is unavailable, suggest a new time while pretending to consult "The Sacred Book of Prime-Time Scheduling" or some other amusing imaginary source.

Today's date is {{DateTime.now().setZone('TIMEZONE').toFormat('dd LLL yyyy HH:mm:ss')}}

Let’s make scheduling a delightful and prime-worthy experience! 🥳
```

![Image](https://nextwork.ai/thankful_indigo_wise_blackberry/uploads/6ac4b62d-0558-51eb-a3cc-89522aa5cf45_fewargtr52)  


## Glossary  

[n8n](https://n8n.io/?ps_partner_key=Zjc1ZWY4ZDUyOTIw&ps_xid=q4oD6B58NzBBhU&gsxid=q4oD6B58NzBBhU&gspk=Zjc1ZWY4ZDUyOTIw&gad_source=1&gad_campaignid=23397401030&gbraid=0AAAABCODLjs-ccIx00lxoKEtEQLdmSTTt&gclid=Cj0KCQjw3YvXBhCDARIsAKB-ox8-Cka1yxk5NiVDsr7Xq7Zfu_uV5NDKqlOyxqmHiISqeP5y3LcxVyYaAsEHEALw_wcB) - n8n is a workflow automation tool that connects different apps and services together. It uses a visual, node-based interface where you drag and drop steps to create automated tasks, like moving data between platforms or triggering actions based on events, without needing to write complex code.  

`AI Workflow` - AI workflow is the structured process of building and deploying AI applications. It typically involves data collection, cleaning, model training, testing, and deployment. By automating these steps, developers can efficiently turn raw data into intelligent, functional AI tools that solve specific problems.  

`Workflow` is a defined sequence of tasks or steps required to complete a specific process or project. It acts as a roadmap, moving work from initiation to completion by organizing who does what, when, and in what order, ensuring efficiency and consistency in achieving a goal.

`ChatGPT` is an AI chatbot developed by OpenAI that uses a large language model to understand and generate human-like text. You can use it to answer questions, write code, draft documents, or brainstorm ideas. It processes your input to provide conversational, context-aware responses based on its training data.

`Google Calendar` is a cloud-based time management tool that helps you organize your schedule. You can create events, set reminders, and share calendars with others. It syncs across all your devices, ensuring you stay on track with your appointments and tasks wherever you are.

`Dynamic expressions` are code snippets or placeholders within a system that are evaluated at runtime rather than being fixed. Instead of using static, hard-coded values, they allow applications to calculate data, reference variables, or execute logic on the fly based on the current context or user input.

`System message:` A system message is a set of instructions provided to an AI model at the start of a conversation. It defines the AI's persona, tone, rules, and constraints, guiding how it should behave and respond to the user throughout the interaction


---

*Built with [NextWork](https://nextwork.ai) - [View this project](https://nextwork.ai/projects/6ac4b62d-0558-51eb-a3cc-89522aa5cf45)*
