---
type: service
id: llm-service
title: LLM Service
description: "Language model service for email triage, briefing synthesis, and language polish"
tags: [Production, Tested]
connections: []
metadata:
  serviceType: llm
  auth_type: api_key
---

## LLM Service

This skrpt uses a language model for analytical and generative tasks. The LLM handles urgency triage, briefing synthesis, and language polish.

### Configuration

- **Temperature:** 0.3 for triage, 0.5 for briefing synthesis
- **Max tokens:** 4,000 per analysis step, 6,000 for synthesis
- **Context window:** The triage step receives both email and calendar data. The synthesis step receives triage output.

### Requirements

- A configured LLM provider in skrptiq settings
- Sufficient token quota for the full pipeline
- No external network access required beyond your AI provider's endpoint
