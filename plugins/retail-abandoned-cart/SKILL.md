---
name: retail-abandoned-cart
description: Deploy a Treasure AI Foundry agent that recovers abandoned carts by diagnosing purchase barriers and surfacing targeted promotions only when price sensitivity is confirmed
version: 1.0.0
triggers:
  - abandoned cart agent
  - cart recovery
  - retail ecommerce agent
---

# Retail Abandoned Cart Recovery Agent

Deploy a Foundry agent that helps ecommerce customers complete purchases they started but didn't finish. The agent diagnoses why the customer stopped before suggesting a solution - promotions are only offered when price sensitivity is explicitly confirmed, not by default.

## Agent Pattern

- 2 table-based KBs (Customer Profiles, Product Catalog)
- 1 text-based KB (Promotions FAQ)
- Variables block to pre-load customer context and active promotions on conversation start
- Structured output capturing outcome, barrier identified, and whether a promotion was offered

## Files

See `agents/retail-ecommerce/` in this repository for the complete agent configuration.

## Deploy

```bash
tdx agent push ./agents/retail-ecommerce/
tdx chat --agent "Retail Ecommerce/Abandoned Cart Recovery Agent" "I left something in my cart"
```
