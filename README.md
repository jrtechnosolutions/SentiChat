# Sentiment-Based Chat Agent

## Overview
This repository contains an n8n workflow that implements a sentiment-based chat agent. The agent analyzes the sentiment of incoming user messages and adapts its response style accordingly, creating a more personalized and contextually appropriate conversational experience.

## Components

### 1. Trigger: When Chat Message Received
- **Type:** `@n8n/n8n-nodes-langchain.chatTrigger`
- **Function:** Initiates the workflow when a new chat message is received.
- **Configuration:** Set up as a webhook with public access for external connections.

### 2. Sentiment Analysis
- **Type:** `@n8n/n8n-nodes-langchain.sentimentAnalysis`
- **Function:** Analyzes the emotional tone of the incoming message.
- **Input:** User's chat message.
- **Output:** Categorizes the message as "Positive", "Neutral", or "Negative".
- **Dependencies:** Uses OpenAI Chat Model (GPT-4o-mini) for sentiment classification.

### 3. Edit Fields
- **Type:** `n8n-nodes-base.set`
- **Function:** Dynamically generates a system message based on the detected sentiment.
- **Configuration:**
  - For **Positive** sentiment: Creates a cheerful, urban, and energetic response style using colloquial expressions like "qué bueno, mi rey", "me alegra pila, socio".
  - For **Negative** sentiment: Adopts a firmer, direct tone that maintains respect but doesn't tolerate disrespect, using street-style language.
  - For **Neutral** sentiment: Uses a balanced approach similar to the negative case.

### 4. AI Agent
- **Type:** `@n8n/n8n-nodes-langchain.agent`
- **Function:** Processes the user input with the appropriate system message.
- **Dependencies:**
  - OpenAI Chat Model1 (GPT-4o-mini) for generating responses.
  - Simple Memory for maintaining conversation context.

### 5. OpenAI Chat Models
- **Type:** `@n8n/n8n-nodes-langchain.lmChatOpenAi`
- **Models Used:** gpt-4o-mini
- **Instances:**
  - **OpenAI Chat Model:** Powers the sentiment analysis.
  - **OpenAI Chat Model1:** Powers the main AI agent responses.

### 6. Simple Memory
- **Type:** `@n8n/n8n-nodes-langchain.memoryBufferWindow`
- **Function:** Maintains conversation history and context to ensure coherent, contextually relevant responses throughout the interaction.

## Workflow Logic

1. The workflow begins when a user sends a message through the chat interface.
2. The message is analyzed for sentiment using OpenAI's language model.
3. Based on the detected sentiment (Positive, Neutral, or Negative), a specific system message is generated.
4. The AI Agent receives the user message along with the appropriate system message.
5. The agent, powered by GPT-4o-mini, generates a contextually appropriate response that matches the tone dictated by the detected sentiment.
6. The Simple Memory component maintains conversation history for context in future interactions.

## Requirements

- n8n instance (version compatible with all nodes used)
- OpenAI API key with access to GPT-4o-mini model
- Webhook configuration for receiving chat messages

## Installation

1. Import the JSON workflow file (`My_workflow_3.json`) into your n8n instance.
2. Configure your OpenAI API credentials in n8n.
3. Activate the workflow.
4. Use the provided webhook URL to connect to your chat interface.

## Credentials Configuration

> **IMPORTANT**: The workflow JSON file contains placeholder credentials that must be replaced with your own:
>
> - **OpenAI API**: You will need to replace the credential references in the OpenAI Chat Model nodes with your own API key.
>   - Look for the credential sections in the JSON:
>     ```
>     "credentials": {
>       "openAiApi": {
>         "id": "YOUR_CREDENTIAL_ID_HERE",
>         "name": "YOUR_ACCOUNT_NAME_HERE"
>       }
>     }
>     ```
>   - Either configure these credentials in your n8n instance before importing, or update them after import.
>
> - **Instance ID**: The workflow also contains a unique instance identifier that should be removed or will be automatically generated when imported into your n8n instance.

## Use Cases

- Customer service chatbots that adapt tone based on customer sentiment
- Educational assistants that adjust teaching style to student frustration or excitement
- Entertainment bots that match user enthusiasm or provide support when needed
- Therapeutic conversation partners that recognize emotional states

## Customization

You can modify the system messages in the "Edit Fields" node to change how the agent responds to different sentiments. The current configuration uses colloquial Spanish expressions for a street-smart style, but this can be adapted to any language or tone.

## Limitations

- Sentiment analysis accuracy depends on the quality of the language model
- Response style is limited to three categories (could be expanded)
- Currently optimized for Spanish language conversations

## License

[Include your license information here] 