# Sentiment-Based Chat Agent Installation Guide

This guide will help you configure, import, and correctly run the sentiment-based chat agent on your own n8n instance.

## Prerequisites

Before starting, make sure you have the following:

1. **n8n Instance**: A functional n8n installation. You can install it following the [official instructions](https://docs.n8n.io/hosting/).
2. **OpenAI Account**: You'll need an OpenAI account with API access and sufficient credits.
3. **OpenAI API Key**: You must generate an API key in your OpenAI account.

## Step 1: Setting Up Credentials in n8n

### Configure OpenAI Credentials

1. Log in to your n8n instance.
2. Navigate to **Settings** (gear icon) → **Credentials**.
3. Click the **+ Add Credential** button.
4. Search for and select **OpenAI API**.
5. Complete the following fields:
   - **Name**: Choose a descriptive name (e.g., "My OpenAI Account")
   - **API Key**: Paste your OpenAI API key
   - Click **Save**

## Step 2: Import the Workflow

1. In your n8n instance, navigate to the main workflow page.
2. Click the **+ Import from File** button.
3. Select the `My_workflow_3.json` file you downloaded from this repository.
4. Once imported, the workflow will open in the editor.

## Step 3: Update Credential References

After importing the flow, you need to update the credential references:

1. In the flow editor, click on the **OpenAI Chat Model** node.
2. In the configuration panel on the right, click on the credentials field.
3. Select the OpenAI credential you created in Step 1.
4. Repeat the same process for the **OpenAI Chat Model1** node.

## Step 4: Activate the Workflow

1. Once the credentials are configured, click the **Activate** button in the top right of the editor.
2. Confirm the activation in the dialog that appears.

## Step 5: Get the Webhook URL

To interact with your agent, you'll need the webhook URL:

1. Click on the **When chat message received** node.
2. In the configuration panel, you'll find the webhook URL under the "Webhook URL" section.
3. Click the copy button to copy this URL.

## Step 6: Test the Agent

There are several ways to test your agent:

### Option 1: Using the n8n Test Panel

1. While the flow is activated, click on **Test Webhook** in the left sidebar.
2. Configure a POST request to the webhook URL with the following JSON body:
   ```json
   {
     "chatInput": "I'm very happy with the result of my project"
   }
   ```
3. Send the request and observe the agent's response.

### Option 2: Using cURL

You can test the agent from the command line using cURL:

```bash
curl -X POST -H "Content-Type: application/json" -d '{"chatInput":"I'm very frustrated with these errors"}' YOUR_WEBHOOK_URL
```

### Option 3: Integrating with a Chat Interface

For a more complete experience, you can integrate this webhook with:

1. **Web applications** using JavaScript to send requests to the webhook.
2. **Telegram, Discord, Slack bots**, etc., by configuring these services to redirect messages to your webhook.
3. **Custom chat interfaces** developed specifically to interact with this agent.

## Test Message Examples

Test the agent with messages expressing different sentiments:

### Positive Message
```json
{
  "chatInput": "I'm so happy! I finally finished my project and everything turned out perfect."
}
```

### Negative Message
```json
{
  "chatInput": "I'm tired of nothing working as it should, this is very frustrating."
}
```

### Neutral Message
```json
{
  "chatInput": "I need information on how to properly configure this service."
}
```

## Troubleshooting

### The agent doesn't respond
- Verify that the workflow is activated.
- Check that the OpenAI credentials are valid.
- Make sure you're correctly sending the `chatInput` parameter in your request.

### OpenAI Errors
- If you receive API limit errors, check your balance and limits in your OpenAI account.
- If the model is unavailable, edit the OpenAI Chat Model nodes to use a different model available in your account.

### Webhook Error
- If the webhook is not accessible, check the network configuration of your n8n instance.
- Verify that the "When chat message received" node is configured as public.

## Customization

To customize the agent's behavior:

1. Edit the **Edit Fields** node to modify responses based on the detected sentiment.
2. Change the OpenAI models in the corresponding nodes if you want to use other models.
3. Adjust the memory configuration in the **Simple Memory** node to control how much context the agent retains.

## Additional Notes

- This agent is optimized to respond in Spanish with an urban colloquial style.
- Sentiment analysis works best with clear and direct messages.
- To use this agent in a production environment, consider implementing additional security measures and input validation. 