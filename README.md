# AI Automation Portfolio

**Josefina Giannelli Bozzini** · AI Automation Specialist · Argentina

I build AI-powered workflows with **n8n** that connect real business tools: Gmail, Google Sheets, Google Drive, HubSpot, Tally, Airtable, WhatsApp and Telegram, with Google Gemini, OpenAI, Pinecone and ElevenLabs.

My background is in **legal administration and customer service**, so I design automations around how a business actually works: clear steps, a human approving what matters, and no lost data when something fails.

Each project folder includes the exported **n8n workflows**, **screenshots** and its own **README**.

---

## Projects

### ⚖️ [UK Legal Intake, Conflict Check & Client Care Letter](uk-legal-intake-client-care) · *New*
End-to-end system for a law firm in England & Wales, from first enquiry to engagement letter, built as three connected workflows.
- AI checks each enquiry for **conflicts of interest** against the firm's client database and prepares a case brief.
- The solicitor **accepts or declines with one click**, and the contact is saved in **HubSpot CRM**.
- After the consultation, AI drafts the **Client Care Letter**. Fees, complaints and SRA wording come from fixed templates, and the solicitor approves it before it is sent.
- Data validation, retries, no-duplicate audit logs and a shared **error workflow** with email alerts.

`n8n` `Google Gemini` `Tally` `Gmail` `HubSpot` `Google Sheets` · 🎥 [Demo video](https://drive.google.com/file/d/1ryQE05HFwn3VLweZoAONkBYVY3zTIoVx/view?usp=sharing)

### 🎙️ [Voice AI Assistant](voice-ai-assistant)
Voice-to-voice customer assistant for a coffee shop on Telegram: transcribes voice notes, answers with a natural voice and keeps per-customer memory. Built with privacy by design: no audio is stored.

`n8n` `Whisper` `GPT-4o-mini` `ElevenLabs` `Telegram`

### 💬 [NovaTech Support Bot](novatech-support-bot)
Telegram support agent that answers questions with **RAG** over a company knowledge base indexed from Google Drive.

`n8n` `AI Agent` `Pinecone` `Google Drive` `Telegram`

### 🎾 [AI Padel Booking Assistant](padel-booking-assistant)
WhatsApp AI agent that checks court availability and books or cancels slots in natural language.

`n8n` `Google Gemini` `WhatsApp Cloud API` `Google Sheets`

### 🧾 [Invoice Processor](invoice-processor)
Extracts data from supplier invoices received by email, validates required fields, totals and duplicates, and saves valid invoices to a spreadsheet. Invalid ones go to review with an email alert.

`n8n` `AI` `Gmail` `Google Sheets`

### 🏠 [Real Estate Lead Management](real-estate-lead-management)
Four connected workflows that process leads from a Tally form, manage property and lead data in Airtable, and include an error handler and human approval before key actions.

`n8n` `Tally` `Airtable` `Sub-workflows` `Human-in-the-loop`

---

## What these projects show

- **AI agents** with tools, memory and structured outputs
- **RAG** with vector databases
- **Voice AI** (speech-to-text and text-to-speech)
- **Document processing** and data validation
- **CRM automation** with HubSpot
- **Human-in-the-loop** approvals for decisions that matter
- **Reliable workflow design:** sub-workflows, retries, error handlers and audit logs
- **Privacy by design:** least-privilege credentials and no unnecessary data storage

---

## Contact

- LinkedIn: [linkedin.com/in/josefina-giannelli-bozzini](https://www.linkedin.com/in/josefina-giannelli-bozzini)
- Email: josefina.giannellibozzini@gmail.com

*All projects are built on simulated business scenarios with test data.*
