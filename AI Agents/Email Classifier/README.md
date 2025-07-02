# Email Classifier (n8n Workflow)

This workflow demonstrates how to classify incoming emails using an AI agent (LLM) and automatically forward them to appropriate recipients based on the content. It's useful for automating email triage in business environments such as shared inboxes, contact forms, or helpdesks.

## Features

- Fetches emails using IMAP
- Uses OpenAI GPT (via LangChain Agent) to categorize each email
- Classifies into one of the following categories:
  - `Spam`
  - `AppointmentRequest`
  - `Invoice`
  - `RequestForQuotation`
  - `NotAssignable`
- Automatically forwards the email (including attachments) via SMTP to a predefined recipient based on its category

## Setup

1. **Credentials**
   - Create the following credentials in your n8n instance:
     - **IMAP Email** (named `Your IMAP Credentials`)
     - **SMTP Email** (named `Your SMTP Credentials`)
     - **OpenAI API** (named `Your OpenAI API Key`)

2. **Mail Server Configuration**
   - The workflow fetches unread messages from the default inbox.
   - Messages are marked as read after processing.

3. **Category to Recipient Mapping**
   - In the `Code` node, you can define which recipient receives which category.
   - Example:
     ```js
     const config = {
       Spam: { targetEmail: 'spam' },
       AppointmentRequest: { targetEmail: 'appointments' },
       Invoice: { targetEmail: 'invoices' },
       RequestForQuotation: { targetEmail: 'sales' },
     };
     const TargetServer = 'example.com';
     ```

4. **LLM Prompt**
   - The LangChain Agent receives a structured prompt with sender, subject, and message content.
   - Output is validated using a structured output parser for reliability.

## Example Flow

1. A new email arrives in the inbox.
2. The AI agent classifies the email content.
3. A recipient is assigned based on the classification.
4. The email is forwarded via SMTP to the appropriate recipient.

## Notes

- Emails that do not clearly match a category will be marked as `NotAssignable`.
- Attachments are preserved and forwarded with the email.
- You can customize categories and recipients by adjusting the prompt and `Code` node logic.
