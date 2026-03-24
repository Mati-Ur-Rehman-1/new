n8n Workflow Documentation

Selr AI — Post-Discovery Transcript Revision Workflow

Workflow Diagram

┌─────────────────────────────────────────────┐
│         🔗 Webhook                          │
│   Step 1: Webhook                           │
│   Receives discovery call transcript & JSON │
└─────────────────────┬───────────────────────┘
                      │
                      ▼
┌─────────────────────────────────────────────┐
│         💻 Code Node                        │
│   Step 2: clean webhook data1               │
│   Extracts Transcript, Name, & Shopping List│
└─────────────────────┬───────────────────────┘
                      │
                      ▼
┌─────────────────────────────────────────────┐
│         🤖 OpenAI (GPT-5.2)                 │
│   Step 3: Revise agent1                     │
│   Amends shopping list based on transcript  │
└─────────────────────┬───────────────────────┘
                      │
                      ▼
┌─────────────────────────────────────────────┐
│         💻 Code Node                        │
│   Step 4: Code in JavaScript4               │
│   Fixes AI hallucinations and rebuilds math │
└─────────────────────┬───────────────────────┘
                      │
                      ▼
┌─────────────────────────────────────────────┐
│         💻 Code Node                        │
│   Step 5: Convert Json to HTML              │
│   Generates "Revised" PDF layout template   │
└─────────────────────┬───────────────────────┘
                      │
                      ▼
┌─────────────────────────────────────────────┐
│         📄 PDF.co API                       │
│   Step 6: PDFco Api1                        │
│   Converts HTML to hosted PDF document      │
└─────────────────────┬───────────────────────┘
                      │
                      ▼
┌─────────────────────────────────────────────┐
│         📞 GoHighLevel API                  │
│   Step 7: Create or update a contact        │
│   Saves Revised PDF & updates Audit Status  │
└─────────────────────────────────────────────┘

Step-by-Step Node Documentation

Step 1 — Webhook: Webhook Trigger

App: n8n Core Node
Action: Listen for Event
Type: Trigger
Purpose:
Triggers the revision workflow when an internal team member submits the post-discovery internal form from GoHighLevel. 
Configuration Notes:
Endpoint path: `/zoom-integration`.
Accepts a POST payload containing the original Shopping List JSON, the newly pasted Call Transcript, and the Contact ID.

Step 2 — Code Node: clean webhook data1

App: Code
Action: Run JavaScript
Type: Action
Purpose:
Acts as a data normalizer. It standardizes the incoming payload, handling potential field name variations (e.g., typos like 'Shooping List' vs 'Shopping List'). It safely parses the stringified original JSON and extracts the raw transcript text.
Configuration Notes:
Also extracts the `business_name`, `email`, and `full_name` from the raw GHL form payload for use in the final PDF header.

Step 3 — OpenAI: Revise agent1

App: OpenAI (LangChain)
Action: POST
Type: Action
Purpose:
Acts as the "Revision Agent." It analyzes the discovery call transcript against the original shopping list JSON. It intelligently applies requested changes (adding new items, removing rejected ones, shifting priorities, or adjusting prices based on client feedback) without modifying unchanged items.
Configuration Notes:
Strictly instructed NOT to hallucinate new prices below tier minimums unless explicitly stated by the client in the transcript.
Outputs a structured `changes_from_discovery_call` object logging exactly what was added, removed, or modified.

Step 4 — Code Node: Code in JavaScript4

App: Code
Action: Run JavaScript
Type: Action
Purpose:
A critical safety net. This script scrubs the AI output, extracts the JSON, and performs a "Smart Original Fields Restore". It compares the AI's output with the original JSON and overrides any AI hallucinations (like unauthorized price or tier changes) if the AI didn't explicitly log a reason for changing them. Finally, it dynamically recalculates all financial totals, infrastructure costs, and hours based on the newly adjusted list.
Configuration Notes:
Includes a "Retainer Bleed Fix" to ensure ongoing maintenance items are strictly pushed out of the build automations array.
Rebuilds the Phase 1 roadmap array based on updated priorities and generates mathematical verification summaries.

Step 5 — Code Node: Convert Json to HTML

App: Code
Action: Run JavaScript
Type: Action
Purpose:
Maps the newly validated JSON into the Selr AI HTML template. This node is specifically upgraded for the revision phase, containing new UI blocks for "Changes from Discovery Call" (Added, Removed, Modified items, and Priority Shifts) and "Budget Constraints" notes.

Step 6 — PDF.co: PDFco Api1

App: PDF.co
Action: URL/HTML to PDF
Type: Action
Purpose:
Converts the HTML string from Step 5 into a professional, client-ready PDF document.
Configuration Notes:
Set to name the file with a "Revised" suffix (`= Revised`) to differentiate it from the initial automated audit document.

Step 7 — GoHighLevel API: Create or update a contact

App: HighLevel
Action: Update Contact
Type: Action
Purpose:
Pushes the final, revised proposal back to the client's CRM record so it is ready for final review and contract generation.
Fields Updated:
Post Discovery Call Shopping List: Receives the newly generated PDF.co secure URL.
Audit Status: Updated to "Discovery complete".

Workflow Summary

This n8n workflow automates the amendment of existing proposals after a client discovery call. Triggered by an internal form submission containing the call transcript, it uses an AI Revision Agent to intelligently update the original shopping list JSON based on explicit client feedback. A robust code node then scrubs the AI output to prevent hallucinations and recalculates all financial metrics. The updated data is injected into a revised HTML template, converted into a new PDF via PDF.co, and synced back to the GoHighLevel contact record, ensuring the sales team always has an accurate, client-approved proposal ready to send.

| Step | App | Action | Role |
|---|---|---|---|
| 1 | n8n Webhook | Listen for Event | Trigger — receives transcript & original JSON |
| 2 | Code | Run JavaScript | Normalizes payload and extracts text/JSON |
| 3 | OpenAI | POST | AI Revision Agent — updates list based on call |
| 4 | Code | Run JavaScript | Safety net: Fixes hallucinations & recalculates math |
| 5 | Code | Run JavaScript | Generates updated HTML with "Changes" summary |
| 6 | PDF.co | URL/HTML to PDF | Converts revised HTML to PDF |
| 7 | HighLevel | Update Contact | Updates GHL with new PDF & changes Status |
