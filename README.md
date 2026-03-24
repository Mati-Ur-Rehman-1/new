# Selr AI Audit Automation

This documentation outlines the workflow for the Selr AI Audit Automation system.

## Overview

This automated process is designed to generate a priced "Automation Shopping List" for Selr AI audit clients. The top-level flow is:

1. Client data and form responses are fetched from the GoHighLevel (GHL) Deep Onboarding Form.
2. The data is processed through a multi-agent AI pipeline in n8n to assess complexity and pricing.
3. A professional PDF is generated, pushed back to GHL, and the team gets notified.

## Workflows

The system is composed of interconnected workflows and reference data. Detailed documentation for each can be found in the links below:

### 1. n8n Initial Shopping List Workflow

Fetches form data from GHL, processes it through AI agents, and generates the initial PDF.

- [AI Audit Initial Generation Workflow](./AI_Audit_Initial_Generation.md)

### 2. n8n Transcript Revision Workflow

Triggered by an internal form to revise the existing shopping list based on a discovery call transcript.

- [AI Audit Transcript Revision Workflow](./AI_Audit_Transcript_Revision.md)

### 3. Google Sheets Reference Data

Stores the pricing tiers, adjustment factors, and automation patterns used by the AI pipeline.

- [AI Audit Reference Data](./AI_Audit_Reference_Data.md)

### 4. GHL Configuration Setup

Handles the initial webhook triggers, custom fields, and internal team notifications in GoHighLevel.

- [AI Audit GHL Configuration](./AI_Audit_GHL_Configuration.md)
