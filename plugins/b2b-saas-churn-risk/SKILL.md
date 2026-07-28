---
name: b2b-saas-churn-risk
description: Deploy a Treasure AI Foundry agent that intervenes on at-risk B2B SaaS accounts, diagnoses churn root cause using a success playbook KB, and escalates to CSM when thresholds are met
version: 1.0.0
triggers:
  - churn risk agent
  - b2b saas agent
  - customer success agent
---

# B2B SaaS Churn Risk Intervention Agent

Deploy a Foundry agent that works within Customer Success to identify why accounts are struggling and take targeted action before they churn. The agent consults a Success Playbooks KB to determine the right intervention sequence by risk level, and outputs root cause classification and CSM escalation flags.

## Agent Pattern

- 2 table-based KBs (Account Profiles, Product Documentation)
- 1 text-based KB (Success Playbooks - intervention sequences by risk level)
- reasoning_effort: high for accurate root cause diagnosis
- Structured output with churn risk level, root cause, intervention taken, CSM escalation flag, and renewal at risk flag

## Files

See `agents/b2b-saas/` in this repository for the complete agent configuration.

## Deploy

```bash
tdx agent push ./agents/b2b-saas/
tdx chat --agent "B2B SaaS/Churn Risk Intervention Agent" "Our team hasn't been using the platform much lately"
```

## Test

```bash
tdx agent test ./agents/b2b-saas/churn-risk-agent/
```
