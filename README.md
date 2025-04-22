# 🧠 Sentiment-Based Chat Agent

[![n8n](https://img.shields.io/badge/Built%20with-n8n-0D1117?style=flat&logo=n8n)](https://n8n.io/)
[![OpenAI](https://img.shields.io/badge/OpenAI-GPT--4o--mini-4B8BBE?style=flat&logo=openai)](https://platform.openai.com/)
[![Langchain](https://img.shields.io/badge/Powered%20by-LangChain-EC4E4E.svg)](https://www.langchain.com/)
[![License](https://img.shields.io/badge/license-MIT-green.svg)](LICENSE)

---

## 📋 Description

This project implements a **sentiment-based message analysis agent** using `n8n` and OpenAI's GPT-4o-mini.  
⚠️ Unlike traditional chatbots, this agent is **not meant for sustained conversation**. Instead, it analyzes individual user messages and provides a **single, context-aware, emotionally-aligned response**.

It's ideal for use cases where identifying and responding to a user's emotional tone is more important than maintaining ongoing chat sessions.

---

## ✨ Key Features

- 🔍 **Sentiment Analysis**: Classifies input messages as *Positive*, *Neutral*, or *Negative* using OpenAI.
- 🧠 **Tone-Adaptive Responses**: Generates a structured, empathetic response aligned with the detected sentiment.
- 🧰 **Non-Conversational Agent**: Responds once per input message—does not continue chatting.
- 💡 **Structured Outputs**: Clearly presents emotional insights, tailored replies, and suggested actions.
- 🌍 **Multilingual Adaptability**: Currently optimized for Spanish, easily extendable to other languages.

---

## 🛠️ Workflow Components

| Component             | Description                                                                 |
|-----------------------|-----------------------------------------------------------------------------|
| **Trigger**           | Starts the workflow when a message is received (`chatTrigger` webhook).     |
| **Sentiment Analysis**| Classifies sentiment using `OpenAI Chat Model` via LangChain node.          |
| **Edit Fields**       | Generates a dynamic system prompt based on detected sentiment.              |
| **AI Agent**          | Produces the final output using OpenAI + memory context.                    |
| **OpenAI Models**     | GPT-4o-mini used for both sentiment analysis and final message generation.  |
| **Simple Memory**     | Stores minimal context if future expansion is needed.                       |

---

## 🧠 Workflow Logic

1. **Trigger**: Activated via webhook when a user sends a chat message.
2. **Sentiment Detection**: Analyzes emotional tone (positive, neutral, negative).
3. **System Prompt Generation**: Builds a structured instruction for the AI agent based on sentiment.
4. **Response Generation**: AI agent returns a well-structured, emotionally aligned reply.
5. *(Optional)*: Memory module stores context for future expansion (currently not used in loops).

---

## 🚀 Installation

```bash
# Step 1: Import the workflow into n8n
Upload the file `My_workflow_3.json` to your n8n instance.

# Step 2: Configure OpenAI credentials
Go to your n8n credentials and add your API key with GPT-4o access.

# Step 3: Activate the workflow
Enable the webhook trigger to start receiving messages.

# Step 4: Connect your frontend or external service
Use the webhook URL provided to connect a chat UI, form, or integration.
```

---

## 🔐 Credentials

Before using the workflow, update the following:

- **OpenAI API Key**: Replace the placeholder credentials in the workflow JSON with your own.
- **Webhook Access**: Ensure the trigger node is publicly accessible or protected as needed.

```json
"credentials": {
  "openAiApi": {
    "id": "YOUR_CREDENTIAL_ID",
    "name": "YOUR_ACCOUNT_NAME"
  }
}
```

---

## 📌 Use Cases

- Customer service tools that adjust tone based on emotional input  
- Educational platforms that identify student frustration or motivation  
- Therapy apps that offer support or reflection based on mood  
- Human-computer interaction demos for sentiment-aware systems

---

## ⚙️ Customization

You can modify:
- 🎭 **Tone and language style** in the `Edit Fields` node
- 🧠 **Prompt template** to change formatting or content emphasis
- 🌐 **Language adaptation** to English, Spanish, or multilingual use

---

## 🚫 Limitations

- Currently handles only 3 sentiment types (positive, neutral, negative)
- Response quality depends on OpenAI's interpretation accuracy
- Not a conversation bot — does not handle multi-turn interactions

---

## 📄 License

[MIT License](LICENSE)

---

## 🙏 Acknowledgements

- [n8n](https://n8n.io/) for the visual automation platform  
- [OpenAI](https://openai.com/) for language models  
- [LangChain](https://www.langchain.com/) for seamless model chaining  
- The open-source community for continued inspiration
