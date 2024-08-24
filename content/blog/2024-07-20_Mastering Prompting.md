---
title: USEFUL Agentic Workflow
description: AUTO-Updating Blog with Claude 3.5 Sonnet
authors: niclasedge
images: null
tags:
- AI
toc_max_heading_level: 5
created: 20.07.2024
---

# Master Promts
### 1 Model
Das Model enscheided wie man das Prompt schreiben muss

### 2 Purpouse
Der Zweck muss klar definiert sein.

### 3 Variablen
Static Variables
Dynamic Variable
- werden geupdated, wenn man das prompt ausführen möchte
- TOPIC

### 4 Examples
Es sollte gute Beispiele mitgeliefert werden, sodass klar wird was genau egwünscht wird.

### 5 Output
Hängt eng mit Beispielen zusammen.
JSON ist ein gutes format um strukturiere Ausgaben zu erhalten.

For Chains, the output of the previous task defines the input variables for the next agent.

![[Pasted image 20240719145614.png]]

![[Pasted image 20240719145840.png]]


# When to use Prompt Chains. DITCHING LangChain. ALL HAIL Claude 3.5 Sonnet
https://www.youtube.com/watch?v=UOcYsrnSNok&t=74s

## When to use Prompt Chain
1. Your tasks are complex for a single prompt
	- Am I asking my LLM to accomplish 2 or more tasks that are distantly related in one prompt? If Yes → Build a prompt chain?
		- *Why: Prompt chaining can help break down complex tasks into manageable chunks, improving clarity and accuracy.*
2. Increase prompt performance and reduce, errors
	- Do I want to increase prompt performance to the max, and reduce errors to the minimum? If Yes → Build a prompt chain?
		- *Why: Prompt chaining allows you to guide the LLM's reasoning process, reducing the likelihood of irrelevant or nonsensical responses.*
3. Use output of previous prompt as input
	- Do I need the output of a previous prompt to be the input (variable) of this prompt? If Yes → Build a prompt chain?
		- *Why: Prompt chaining is essential for tasks where subsequent prompts need to use information generated in previous steps.*
4. Adaptive workflow based on prompt flow
- Do I need an adaptive workflow that changes based on the flow of the prompt? If yes •→ Build a prompt chain
	- *Why: Prompt chaining allowed you to interject and respond to the flow of your


# USEFUL Agentic Workflow: AUTO-Updating Blog with Claude 3.5 Sonnet
https://www.youtube.com/watch?v=F0eOYrA6ggY

- https://schedule.readthedocs.io/en/stable/
	- auto schedule via python library
- https://ntfy.sh/ - for free notofications from worflows etc 
	- with ios app

## Sequential Agentic Workflow
- predetermined steps how this should work
- What should happen, when certain info is retrieved via llm
- act on it, if something appeared

### step 1 trigger
- hit api endpoint
- scheduler
- cli
- UI  triggered

### step 2 retrieve
- API
- Database
- Local File
- Message
- Web Scraping

### Agentics
Run your prompt(s) that solve your problem
- Prompt
- Prompt Chain
- AI Agents
- Assistant API
- Tool Calling

### Act
Act on the data retrieved.
Can occur i 'prompt' step via tooling.
completes the task at hand
- Update Files
- Update database
- update api
- update UI

### Learn
Learn from data retrieved.
Allows your Workflow to improve over time.
- Update LLM files
- Update LLM database
- Update LLM API
- Update LLM UI

### Notify
Let the owner (you) know about the result of the workflow, if somethin was triggered and retrieved something new
- Slack
- Email
- SMS
- Push
- Logging
- System Metrics

## 5 Tips for builing 
1. be incremental
	1. bare minimal promt, then slowly become more complex
2. use great logging & notifications
	1. Great monitoring leads to great debugging and system level understanding
3. SOTA model first
	1. Start with the state of the art models first, then slowly replace it with cheaper models IF they can do the job
4. LLMs a "just" function
	1. Remember LLMs are 'just' string in, string out functions. Engineer your agentics as you would any other function
5. Build for tomorrow
	1. over time you should be givin your agents more abilities + autonomy and writing less code
