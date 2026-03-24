# Selr AI Audit Automation System

This documentation outlines the complete start-to-end automated pipeline for generating priced "Automation Shopping Lists" for Selr AI clients.

## Overview

The system automates the manual analysis of client onboarding data. It transforms raw form responses into a professional, accurately priced PDF proposal within minutes. The high-level flow is:

1. **Trigger:** Client submits the Deep Onboarding Form in GoHighLevel (GHL).
2. **Orchestration:** n8n fetches the data and routes it through a 3-agent AI pipeline.
3. **Intelligence:** AI Agents identify opportunities, assess complexity, and apply pricing based on Google Sheets reference data.
4. **Delivery:** A professional PDF is generated via PDF.co and synced back to the GHL contact record.
5. **Revision:** Discovery call transcripts can be used to automatically update the proposal.

## Workflows

The system is composed of interconnected workflows. Detailed documentation for each component can be found below:

### 1. GHL Audit Trigger Workflow
The entry point that captures form submissions and initiates the automation.
* [GHL Audit Trigger Documentation](./GHL_Audit_Trigger.md)

### 2. n8n Initial Generation Pipeline
The core engine that processes data through AI agents and generates the initial PDF.
* [n8n Initial Generation Documentation](./n8n_Initial_Generation.md)

### 3. n8n Transcript Revision Workflow
The secondary flow that amends proposals based on discovery call insights.
* [n8n Transcript Revision Documentation](./n8n_Transcript_Revision.md)

### 4. Reference Data (Google Sheets)
The dynamic "database" for pricing tiers, adjustment factors, and patterns.
* [Reference Data Documentation](./Audit_Reference_Data.md)
