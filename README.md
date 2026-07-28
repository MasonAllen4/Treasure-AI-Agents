# Treasure AI Foundry - Agent Portfolio

A portfolio of five AI agents built using knowledge from the [Treasure AI Foundry](https://docs.treasure.ai/products/ai-studio), demonstrating the range of use cases an AI Deployment Consultant would design and deploy across various Fortune 1000 clients.

Each agent is production-ready configuration - push to a live Treasure AI environment and it works.

---

## Agents

| Vertical | Agent | Use Case | Key Pattern |
|---|---|---|---|
| **Media** | Subscriber Re-engagement | Re-engage at-risk subscribers before churn | Text KB + 2 table KBs, CDP output loop |
| **Retail** | Abandoned Cart Recovery | Remove purchase barriers, recover lost revenue | Promotions FAQ KB, barrier-detection logic |
| **CPG** | Loyalty & Shopper Insights | Surface rewards, drive repeat purchase | Web search tool, tier-aware messaging |
| **Automotive** | Lead Qualification | Qualify buyer intent, route to right next step | High reasoning effort, 5-field scoring output |
| **B2B SaaS** | Churn Risk Intervention | Diagnose at-risk accounts, escalate to CSM | Success playbook KB, root cause classification |

---

## Folder Structure

Each vertical is a self-contained Treasure AI project:

```
agents/{vertical}/
├── tdx.json                        # Links to the Treasure AI project by name
├── {agent-name}/
│   ├── agent.yml                   # Model, tools, and output schema
│   └── prompt.md                   # Agent behavior rules and guardrails
└── knowledge_bases/
    ├── {name}.yml                  # Table-based KB - queries a live TD database
    └── {name}.md                   # Text-based KB - static reference content
```

### The three file types

**`agent.yml`** - the wiring layer. Defines which LLM model to use, which knowledge bases to connect, how to query them, and what structured data to write back to the CDP at the end of each conversation.

**`prompt.md`** - the behavior layer. Defines how the agent responds, what it should and shouldn't do, how it handles edge cases, and when to escalate to a human.

**Knowledge bases** - the data layer. Table-based KBs (`.yml`) run `td_query` against live Treasure Data databases - customer profiles, inventory, product catalogs. Text-based KBs (`.md`) store static content - FAQs, playbooks, policies - that the agent can read and reference.

---

## How It Works

```
User message
    ↓
Agent reads prompt.md → decides what to do
    ↓
Agent calls a tool (lookup_customer, search_inventory, etc.)
    ↓
Tool queries the knowledge base (live TD table or text file)
    ↓
Agent uses that data to respond
    ↓
Agent calls record_outcome → structured output written back to CDP
```

The `outputs` section in `agent.yml` closes the loop - every conversation produces structured data (intent, action taken, recommendations) that flows back into Treasure Data to update customer profiles, refine segments, and trigger downstream journeys.

---

## Deploy & Test

```bash
# Install and authenticate
npm install -g @treasure-data/tdx
tdx auth setup

# Push an agent to Treasure AI
tdx agent push ./agents/media-streaming/

# Preview changes without deploying
tdx agent push --dry-run ./agents/media-streaming/

# Test with a live conversation
tdx chat --agent "Media Streaming/Subscriber Re-engagement Agent" "I haven't watched in weeks"

# Start a fresh conversation
tdx chat --new --agent "Media Streaming/Subscriber Re-engagement Agent" "Hello"

# Run automated test suite
tdx agent test ./agents/media-streaming/subscriber-reengagement-agent/
```

---

## Why Each Agent Is Different

Each agent was designed to demonstrate a distinct pattern - not just swap the prompt and repeat.

**Media - Subscriber Re-engagement**
Three knowledge bases (one text, two table-based), structured output that captures subscriber intent and feeds it back into the CDP for segment refinement.

**Retail - Abandoned Cart Recovery**
Barrier-detection logic in the prompt - the agent diagnoses *why* the customer didn't purchase before offering a solution. Promotions are only surfaced when price sensitivity is confirmed, not by default.

**CPG - Loyalty & Shopper Insights**
Web search tool wired in alongside knowledge bases - the agent can reach beyond static data to find current retailer availability or brand news. Tier-aware messaging adapts tone and offers by loyalty level.

**Automotive - Lead Qualification**
`reasoning_effort: high` - this agent thinks harder before responding because qualification decisions have downstream consequences (routing to sales, triggering nurture journeys). Output schema captures a five-field lead score that integrates directly with CRM workflows.

**B2B SaaS - Churn Risk Intervention**
Uses a Success Playbooks knowledge base - a text KB containing intervention sequences by risk level. The agent doesn't just respond to the customer; it consults the playbook to determine the right intervention, then records root cause and CSM escalation flag for the CS team.

---

## Built With

- [Treasure AI Foundry](https://docs.treasure.ai/products/ai-studio)
- [Treasure AI CLI (tdx)](https://tdx.treasuredata.com)
- [Treasure AI Studio](https://docs.treasure.ai)
