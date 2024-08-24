---
title: Azure Infrastructure Update July 12, 2024
description: A summary of recent Azure infrastructure updates and announcements
authors: niclasedge
images: null
tags:
- AI
toc_max_heading_level: 5
created: 06.07.2024
---

## Was ist Aide Chat?

### Welche Modelle werden untertstützt?


## Master Promts
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
Es sollte gute Beispiele mitgeliefert werden, sodass klar wird was genau gewünscht wird.

```
# aider starten und das gewünschte model angeben

# bestes model (teuer)
aider --model openrouter/anthropic/claude-3.5-sonnet

# guter coder (preiswert)
aider --model openrouter/deepseek/deepseek-coder

#free via groq
- groq/llama-3.1-405b-reasoning
- groq/llama-3.1-70b-versatile
- groq/llama-3.1-8b-instant
- groq/mixtral-8x7b-32768

## Aider im browser
aider --browser --model openrouter/deepseek/deepseek-coder
```

#### Aider In-Chat comands

|                  |                                                                                         |
| ---------------- | --------------------------------------------------------------------------------------- |
| **/add**         | Add files to the chat so GPT can edit them or review them in detail                     |
| **/ask**         | Ask questions about the code base without editing any files                             |
| **/chat-mode**   | Switch to a new chat mode                                                               |
| **/clear**       | Clear the chat history                                                                  |
| **/clipboard**   | Add image/text from the clipboard to the chat (optionally provide a name for the image) |
| **/code**        | Ask for changes to your code                                                            |
| **/commit**      | Commit edits to the repo made outside the chat (commit message optional)                |
| **/diff**        | Display the diff of changes since the last message                                      |
| **/drop**        | Remove files from the chat session to free up context space                             |
| **/exit**        | Exit the application                                                                    |
| **/git**         | Run a git command                                                                       |
| **/help**        | Ask questions about aider                                                               |
| **/lint**        | Lint and fix provided files or in-chat files if none provided                           |
| **/ls**          | List all known files and indicate which are included in the chat session                |
| **/map**         | Print out the current repository map                                                    |
| **/map-refresh** | Force a refresh of the repository map                                                   |
| **/model**       | Switch to a new LLM                                                                     |
| **/models**      | Search the list of available models                                                     |
| **/quit**        | Exit the application                                                                    |
| **/read-only**   | Add files to the chat that are for reference, not to be edited                          |
| **/reset**       | Drop all files and clear the chat history                                               |
| **/run**         | Run a shell command and optionally add the output to the chat (alias: !)                |
| **/test**        | Run a shell command and add the output to the chat on non-zero exit code                |
| **/tokens**      | Report on the number of tokens used by the current chat context                         |
| **/undo**        | Undo the last git commit if it was done by aider                                        |
| **/voice**       | Record and transcribe voice input                                                       |
| **/web**         | Scrape a webpage, convert to markdown and add to the chat                               |

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


