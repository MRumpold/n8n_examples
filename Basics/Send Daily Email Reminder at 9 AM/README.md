# Daily Email Reminder (n8n Workflow)

This workflow sends a **daily email reminder at 9:00 AM** using the built-in `Schedule Trigger` and `Send Email` nodes in n8n.

---

## Overview

- **Trigger Time:** Every day at 09:00
- **Steps:**
  1. `Schedule Trigger`: Starts the workflow at 9:00 AM
  2. `Edit Fields`: Sets the sender, recipient, subject, and body of the email
  3. `Send Email`: Sends the email using an SMTP server

---

## Setup Instructions

### 1. Configure Email Addresses
In the `Edit Fields` node:
- Replace the value of `emailFrom` with your **sender email**
- Replace the value of `emailTo` with your **recipient email**

### 2. Add SMTP Credentials
In the `Send Email` node:
- Add or select your SMTP credentials under the **"SMTP account"** field

> If you haven't created credentials yet:
> - You can go to `Credentials` in the n8n sidebar and add your mail server configuration (e.g., Gmail, Outlook, or your SMTP server)
> - **Alternatively**, click on **"+ Create New Credential"** directly in the `Send Email` node to add it on the spot

---

## Testing the Workflow

To test the workflow manually:
- Click the **arrow button next to the "Schedule Trigger"** node
- This allows you to manually trigger the workflow without waiting for 9:00 AM

---

## Production Usage

Once you **activate** the workflow (toggle top right corner in the editor), it will automatically:
- Run every day at **9:00 AM**
- Send an email to the specified recipient

---

## Notes

- The email body is plain text or HTML (editable in the `body` field).
- If needed, you can expand the workflow to include CC, attachments, or conditional logic.