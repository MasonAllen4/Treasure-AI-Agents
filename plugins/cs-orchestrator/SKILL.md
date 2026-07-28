---
name: cs-orchestrator
description: Deploy a Treasure AI Foundry orchestrator agent that triages incoming customer success requests and routes them to specialist agents using agent-to-agent tool wiring
version: 1.0.0
triggers:
  - orchestrator agent
  - multi-agent routing
  - customer success hub
---

# Customer Success Orchestrator Agent

Deploy a Foundry orchestrator that routes customers to the right specialist agent based on whether they are a B2C media subscriber or a B2B SaaS account. Demonstrates the agent-to-agent tool pattern - specialist agents are wired as tools rather than knowledge bases.

## Agent Pattern

- 2 agent-type tools (Subscriber Re-engagement Agent, Churn Risk Intervention Agent)
- output_mode: RETURN on both tools so responses are synthesized before delivery
- reasoning_effort: high for accurate routing decisions
- Structured output capturing specialist used, customer type, resolution, and handoff notes

## Requires

Both specialist agents must be deployed before the orchestrator:
- `agents/media-streaming/` - Subscriber Re-engagement Agent
- `agents/b2b-saas/` - Churn Risk Intervention Agent

## Files

See `agents/customer-success-hub/` in this repository for the complete agent configuration.

## Deploy

```bash
# Deploy specialist agents first
tdx agent push ./agents/media-streaming/
tdx agent push ./agents/b2b-saas/

# Then deploy the orchestrator
tdx agent push ./agents/customer-success-hub/
tdx chat --agent "Customer Success Hub/CS Orchestrator Agent" "I need help with my account"
```

## Test

```bash
tdx agent test ./agents/customer-success-hub/cs-orchestrator-agent/
```
