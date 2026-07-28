---
name: media-subscriber-reengagement
description: Deploy a Treasure AI Foundry agent that re-engages at-risk media streaming subscribers using personalized content recommendations and subscription data
version: 1.0.0
triggers:
  - subscriber reengagement
  - media streaming agent
  - churn prevention agent
---

# Media Subscriber Re-engagement Agent

Deploy a Foundry agent that helps at-risk media streaming subscribers rediscover value before they cancel. The agent looks up subscriber profiles, searches a content catalog for personalized recommendations, and references a subscriber FAQ for billing and account questions.

## Agent Pattern

- 1 text-based KB (Subscriber FAQ)
- 2 table-based KBs (Subscriber Profiles, Content Catalog)
- Variables block to pre-load subscriber context before conversation starts
- Structured output capturing intent, action taken, and recommended titles

## Files

See `agents/media-streaming/` in this repository for the complete agent configuration.

## Deploy

```bash
tdx agent push ./agents/media-streaming/
tdx chat --agent "Media Streaming/Subscriber Re-engagement Agent" "I haven't watched in weeks"
```

## Test

```bash
tdx agent test ./agents/media-streaming/subscriber-reengagement-agent/
```
