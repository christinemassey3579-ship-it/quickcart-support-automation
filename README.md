# QuickCart Customer Support Automation

An automated support-request system for **QuickCart**, an online store. Customers submit a request through a Google Form, the answers are saved in Google Sheets, and an **n8n** workflow sorts each request by issue type and sends it on by email.

**Built by:** Christine Massey · **Tools:** Google Forms, Google Sheets, n8n, Gmail

## How it works

```
Google Form  →  Google Sheet  →  n8n workflow  →  Switch (by issue type)  →  Gmail
(customer      (responses        (reads the        Payment / Delivery /       (one email
 submits)       saved)            rows)             Technical / General        per type)
```

1. **Google Form – "QuickCart Support":** customers enter their name, email, issue category and a message.
2. **Google Sheet – "QuickCart (Responses)":** every form submission is saved as a new row automatically.
3. **n8n workflow – "QuickCart workflow":**
   - **When clicking 'Execute workflow'** starts the run.
   - **Get row(s) in sheet** reads the support requests from the Google Sheet.
   - **Switch** checks the *Issue Category* and routes each request into one of four paths.
   - **Four Gmail nodes** send an email for each category: Payment Issues, Delivery Issues, Technical Issues and General Issues.

## Issue categories

| Category | Example request | Email sent by |
| --- | --- | --- |
| Payment Issues | "Unable to make payment through the website" | Email for Payment Issues |
| Delivery Issues | "My delivery is delayed" | Email for Delivery Issues |
| Technical Issues | "Unable to add items to my cart" | Email for Technical Issues |
| General Issues | "When is your next end of season sale?" | Email for General Issues |

## Files

| File | What it is |
| --- | --- |
| `QuickCart workflow.json` | The n8n workflow. Import it into n8n with **⋯ → Import from file**. |
| `quickcart-responses-sample.csv` | 24 test support requests from the Google Sheet. Names and emails are replaced with test values. |
| `README.md` | This description |

## How to reuse it

1. Create a Google Form with the fields **Name**, **Email**, **Issue Category** (Payment Issues, Delivery Issues, Technical issues, General Issues) and **Message**, and link it to a Google Sheet.
2. In n8n, import `QuickCart workflow.json`.
3. Connect your own Google Sheets and Gmail accounts in n8n. No passwords or keys are stored in this repository.
4. Point the **Get row(s) in sheet** node at your own response sheet.
5. Click **Execute workflow**.

## Possible next steps

- Run automatically whenever a new form response arrives, instead of clicking Execute.
- Send an acknowledgement email to the customer.
- Use AI to categorise the message when the customer picks the wrong category.
