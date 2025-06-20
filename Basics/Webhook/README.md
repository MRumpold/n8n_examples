# 🔄 Simple Webhook Echo Workflow (n8n)

This n8n workflow demonstrates how to:
- Receive data via a **Webhook Trigger**
- Process the data (e.g., extract `name`)
- Respond directly to the request with a message

---

## 📋 Overview

**Flow:**

1. **Webhook**: Listens for incoming POST requests  
2. **Set Response**: Prepares a confirmation message  
3. **Respond to Webhook**: Sends the response back to the requester

---

## 🌐 Webhook URL

- In **test mode**, your URL will look like:
  ```
  http://localhost:5678/webhook-test/hello-webhook
  ```

- When **active**, it becomes:
  ```
  http://localhost:5678/webhook/hello-webhook
  ```

> You can find both URLs in the **Webhook Trigger node**.

---

## ⚙️ Example Request (PowerShell)

To test the workflow locally on Windows using PowerShell:

```powershell
curl -X POST http://localhost:5678/webhook-test/hello-webhook `
     -H "Content-Type: application/json" `
     -d '{ "name": "Michael" }'
```

Or using `Invoke-RestMethod`:

```powershell
$body = @{ name = "Michael" } | ConvertTo-Json
Invoke-RestMethod -Method POST -Uri "http://localhost:5678/webhook-test/hello-webhook" -Body $body -ContentType "application/json"
```

---

## ✅ Expected Response

```json
{
  "message": "Hello Michael! Your message was received."
}
```

> The response is generated dynamically based on the `name` value from the request.

---

## 📝 Notes

- This workflow is useful to learn:
  - How webhooks work in n8n
  - How to extract and use data from incoming requests
  - How to return a JSON response using `Respond to Webhook`

- You can easily extend it to:
  - Validate inputs
  - Forward to another system (e.g., database, email, API)
  - Create your own lightweight API endpoint

---

## 🔗 Related Docs

- [Webhook Trigger Docs](https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-base.webhook/)
- [Respond to Webhook Docs](https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-base.respondtowebhook/)
