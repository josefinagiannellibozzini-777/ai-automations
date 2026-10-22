# 🧾 AI Supplier Invoice Processor

An n8n workflow that reads supplier invoices from email, extracts their data with AI, validates it, and loads it into Google Sheets automatically. Invoices with errors or duplicates are flagged for human review.

Built for **Chías**, a coffee shop that receives invoices from its dairy, coffee and bakery suppliers every week.

<!-- Demo GIF: add images/demo.gif and uncomment the line below -->
<!-- ![Demo](images/demo.gif) -->

## The problem

Small businesses still type supplier invoices into spreadsheets by hand. It takes time, it's easy to make mistakes, and the same invoice can end up being registered (and paid) twice.

## The solution

Suppliers keep sending invoices by email as usual. The workflow takes it from there:

1. **Intake:** watches the inbox for emails with PDF attachments and extracts the text.
2. **AI extraction:** GPT-4o-mini turns the unstructured text into structured data (supplier, tax ID, invoice number, dates, subtotal, VAT, total, currency) using a strict JSON schema.
3. **Validation:** checks that no field is missing, that subtotal + VAT matches the total, and that the invoice hasn't been registered before.
4. **Routing:** valid invoices go to the **Invoices** sheet. Invalid ones go to the **Review** sheet with the reason, and an email alert is sent.

![Workflow](images/workflow.png)

## Key design decisions

- **No guessing:** the AI is instructed to return `null` for any missing field instead of inventing or calculating values. A hallucinated number would pass validation silently; a `null` is always caught.
- **Math check:** subtotal + VAT must equal the total (with a 1-unit tolerance for rounding). This catches typos in the invoice and extraction errors.
- **Duplicate detection:** invoices are matched by invoice number **and** supplier tax ID, since two suppliers can use the same invoice number.
- **Human in the loop:** nothing is discarded. Every invoice that fails a check lands in the Review sheet with a clear reason, so a person can decide what to do.
- **Error handling:** a separate error workflow catches unexpected failures (unreadable PDF, API outage) and emails the failed node, the error message and a link to the execution.

## Results

**Invoices sheet** (valid invoices):

![Invoices sheet](images/sheet-invoices.png)

**Review sheet** (flagged invoices with reason):

![Review sheet](images/sheet-review.png)

**Email alerts:**

| Invoice needs review | Workflow error |
|---|---|
| ![Review alert](images/alert-review.png) | ![Error alert](images/alert-error.png) |

## Test cases

Four sample invoices are included in [`sample-invoices/`](sample-invoices/), one for each path of the workflow:

| File | Expected result |
|---|---|
| `01_valid_dairy.pdf` | Saved to Invoices |
| `02_valid_coffee.pdf` | Saved to Invoices |
| `03_error_total_mismatch.pdf` | Sent to Review: subtotal + VAT doesn't match the total |
| `04_duplicate_dairy.pdf` | Sent to Review: same invoice as #01 |

## Tech stack

- **n8n** (workflow automation)
- **Gmail** (trigger and alerts)
- **OpenAI GPT-4o-mini** via n8n's Information Extractor (structured output)
- **Google Sheets** (invoice register and review queue)
- **JavaScript** (validation logic in a Code node)

## How to use it

1. Import `workflow.json` and `error-handler.json` into n8n.
2. Create a Google Sheet with two tabs, **Invoices** and **Review**, using these headers:
   `processed_at | supplier | supplier_tax_id | invoice_number | issue_date | due_date | subtotal | vat | total | currency | file_name`
   (the Review tab also has a `reason` column at the end).
3. Connect your Gmail, Google Sheets and OpenAI credentials.
4. Replace the alert email address with your own.
5. Publish the error handler, select it in the main workflow's settings (**Settings → Error Workflow**), and publish the main workflow.
6. Send yourself an email with one of the sample invoices attached.

## Possible improvements

- OCR for scanned invoices and photos taken with a phone.
- Line-item extraction to track supplier prices over time.
- Approval step in Slack or Telegram before an invoice is marked as ready to pay.
