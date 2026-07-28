---
name: cpg-loyalty-insights
description: Deploy a Treasure AI Foundry agent that helps CPG shoppers understand their loyalty status, discover rewards, and engage with the brand using tier-aware messaging and live web search
version: 1.0.0
triggers:
  - loyalty agent
  - cpg shopper agent
  - rewards agent
---

# CPG Loyalty & Shopper Insights Agent

Deploy a Foundry agent that makes loyalty tangible for CPG shoppers - showing exactly what their points are worth, surfacing relevant rewards, and adapting messaging based on tier status. Includes a web search tool for retailer availability and brand news beyond static KB content.

## Agent Pattern

- 2 table-based KBs (Shopper Profiles, Rewards Catalog)
- 1 text-based KB (Brand & Product FAQ)
- Web search tool for live retailer and brand queries
- Tier-aware messaging logic (Bronze, Silver, Gold)
- Structured output capturing intent, points discussed, offer surfaced, and brand sentiment

## Files

See `agents/cpg-loyalty/` in this repository for the complete agent configuration.

## Deploy

```bash
tdx agent push ./agents/cpg-loyalty/
tdx chat --agent "CPG Loyalty/Loyalty & Shopper Insights Agent" "How many points do I have?"
```
