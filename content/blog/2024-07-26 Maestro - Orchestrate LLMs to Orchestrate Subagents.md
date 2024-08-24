---
title: Maestro - Orchestrate LLMs to Orchestrate Subagents
description: LLM Orchestrator
authors: niclasedge
images: null
tags:
- AI
toc_max_heading_level: 5
created: 26.07.2024
---
## Setup

`git clone https://github.com/Doriandarko/maestro`

get free Tavly Account: https://app.tavily.com/
- needed for Web Search API
- 1000 Searches Free per Month

### Setup API Key in its own file:
```bash
# .env_variables file
export ANTHROPIC_API_KEY="api key"
export OPENAI_API_KEY="api key"
export GROQ_API_KEY="api key"
export HUGGINGFACE_API_TOKEN="api key"
export TAVLY_API_KEY="api key"
export TOGETHER_API_KEY="api key"

# load the file in .bashr file:
if [ -f ~/.env_variables ]; then
    source ~/.env_variables
fi

# reload the changes
source .bashrc
```

### change the maestro.py files to use os env variables

```python
import os
client = Anthropic(api_key=os.environ["ANTHROPIC_API_KEY"])
```

### install pip packages
`pip install tavily-python anthropic rich`

## run maestro:

```bash
python maestro.py # or maester-gpt4o.py for openai only

# impot your prompt
# maestro will use orchestration engine to create the files
```
