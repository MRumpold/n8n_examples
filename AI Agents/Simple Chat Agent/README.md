# AI Chatbot with n8n and OpenAI

This workflow demonstrates how to build a simple AI-powered chatbot using [n8n](https://n8n.io) and OpenAI. Messages are processed via a webhook trigger and answered by a language model (e.g., GPT-4o). The bot includes short-term memory to handle context between messages – perfect for learning or prototyping AI agents in n8n.

---

## Workflow Structure

The workflow contains four key components:

1. **Chat Trigger**  
   Listens for incoming messages via webhook (e.g., HTTP POST).

2. **OpenAI Chat Model**  
   Sends the user's message to a model like `gpt-4o-mini` or `gpt-3.5-turbo` for a response.

3. **Simple Memory**  
   Maintains chat history so the AI can remember previous interactions and respond more naturally.

4. **AI Agent Node**  
   Connects the model and memory into a conversational agent. Tools (e.g., calculator or web search) can be added later.

---

## Example Request

Send a POST request to the webhook URL (e.g., via Postman or curl):

```bash
curl -X POST http://localhost:5678/webhook/ai-chatbot \
     -H "Content-Type: application/json" \
     -d '{"message": "What is n8n?"}'
