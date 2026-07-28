---
name: automotive-lead-qualification
description: Deploy a Treasure AI Foundry agent that qualifies automotive leads using high reasoning effort, scores intent across five dimensions, and routes buyers to the right next step
version: 1.0.0
triggers:
  - lead qualification agent
  - automotive agent
  - car dealership agent
---

# Automotive Lead Qualification Agent

Deploy a Foundry agent that qualifies inbound automotive leads through natural conversation. The agent matches buyers to inventory, identifies financing and trade-in intent, and outputs a five-field qualification score (hot/warm/cold/unqualified) that integrates with CRM and journey workflows.

## Agent Pattern

- 2 table-based KBs (Lead Profiles, Vehicle Inventory)
- 1 text-based KB (Sales & Finance FAQ)
- reasoning_effort: high for accurate qualification decisions
- Structured output with qualification score, purchase timeline, vehicle interest, and recommended next action

## Files

See `agents/automotive/` in this repository for the complete agent configuration.

## Deploy

```bash
tdx agent push ./agents/automotive/
tdx chat --agent "Automotive/Lead Qualification Agent" "I'm looking for a family SUV under $45k"
```
