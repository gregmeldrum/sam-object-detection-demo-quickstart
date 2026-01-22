---
sidebar_position: 1
---

import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

# Getting Started

Get up and running with Solace Agent Mesh in just a few steps.

This guide uses **SAM Community**, the free and open-source version of Solace Agent Mesh.

## Supported Platforms

- **macOS** (Apple Silicon)
- **Windows WSL** (Debian-based distributions like Ubuntu)

## Prerequisites

- Python 3.10 or higher
- A terminal/command prompt

## Installation

First, create and activate a Python virtual environment, then install Solace Agent Mesh:

```bash
python -m venv .venv
source .venv/bin/activate  # On Windows: .venv\Scripts\activate
pip install solace-agent-mesh
```

## Initialize Your Project

Choose your setup path based on your LLM provider:

<Tabs>
  <TabItem value="paid" label="Paid Provider (OpenAI, etc.)" default>

If you're using a paid LLM provider like OpenAI, Anthropic, or Azure OpenAI, use the interactive GUI setup:

```bash
sam init --gui
```

This launches a web-based configuration interface on port 5002. When the page loads:

1. Choose the **"Get Started Quickly"** path
2. Enter your AI model credentials (API endpoint, key, and model)
3. Continue to the next step

  </TabItem>
  <TabItem value="free" label="Free Provider (Cerebras, Mistral)">

If you want to try Solace Agent Mesh with a free (rate-limited) LLM provider, use the development mode setup:

```bash
sam init --skip --dev-mode
```

This creates a project with a local broker container and generates a `.env` file with placeholder LLM configuration:

```bash
LLM_SERVICE_ENDPOINT="YOUR_LLM_SERVICE_ENDPOINT_HERE"
LLM_SERVICE_API_KEY="YOUR_LLM_SERVICE_API_KEY_HERE"
LLM_SERVICE_PLANNING_MODEL_NAME="YOUR_LLM_SERVICE_PLANNING_MODEL_NAME_HERE"
LLM_SERVICE_GENERAL_MODEL_NAME="YOUR_LLM_SERVICE_GENERAL_MODEL_NAME_HERE"
```

Replace these values with your chosen free provider's configuration:

<Tabs>
  <TabItem value="cerebras" label="Cerebras" default>

[Cerebras](https://cerebras.ai) offers free API access with rate limits.

**Get your API key:**
1. Go to [cerebras.ai](https://cerebras.ai) and log in
2. Click **API Keys** in the left sidebar
3. Click **Generate API Key**
4. Copy the generated key

**Update your `.env` file:**

```bash
LLM_SERVICE_ENDPOINT="https://api.cerebras.ai/v1"
LLM_SERVICE_API_KEY="csk-xxxx-your-cerebras-api-key-xxxxxx"
LLM_SERVICE_PLANNING_MODEL_NAME="openai/zai-glm-4.7"
LLM_SERVICE_GENERAL_MODEL_NAME="openai/zai-glm-4.7"
```

  </TabItem>
  <TabItem value="mistral" label="Mistral">

[Mistral AI](https://mistral.ai) also offers free API access with rate limits. This is a good backup if you hit Cerebras rate limits.

**Get your API key:**
1. Go to [Mistral AI Studio](https://console.mistral.ai/)
2. Click **API Keys**
3. Click **Create new key**
4. Copy the generated key

**Update your `.env` file:**

```bash
LLM_SERVICE_ENDPOINT="https://api.mistral.ai/v1"
LLM_SERVICE_API_KEY="xxxx-your-mistral-api-key-xxxx"
LLM_SERVICE_PLANNING_MODEL_NAME="openai/magistral-medium-latest"
LLM_SERVICE_GENERAL_MODEL_NAME="openai/magistral-medium-latest"
```

  </TabItem>
</Tabs>

  </TabItem>
</Tabs>

## Run Your Agent Mesh

Once configured, start your agent mesh:

```bash
sam run
```

The web interface will be available at `http://localhost:8000` (configurable via `FASTAPI_PORT` in your `.env` file).

## Next Steps

Now that you have Solace Agent Mesh running, proceed to [Installing Agents](./installing-agents) to set up the agents needed for the demo.
