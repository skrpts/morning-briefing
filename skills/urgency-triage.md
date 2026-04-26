---
type: skill
id: urgency-triage
title: Urgency Triage
description: "Classifies emails by urgency — action required, needs reply, FYI, or skippable"
tags: [Production, Email]
connections:
  - target: llm-service
    type: runs_on
context_params:
  urgency_sensitivity:
    label: "Urgency Sensitivity"
    description: "How aggressively to flag items as urgent — Relaxed, Standard, or Aggressive"
    default: "Standard"
    required: false
---

## Capability

Takes the fetched email set and classifies each email by urgency, considering sender importance, subject content, time sensitivity, and whether a reply is expected.

## What It Does

1. **Action required** — emails needing a response or decision today: direct requests, questions from your manager, deadline-related items, escalations
2. **Needs reply** — emails expecting a reply but not time-critical: colleague questions, meeting follow-ups, information requests
3. **FYI** — useful to read but no action needed: announcements, status updates, newsletters
4. **Skippable** — safe to ignore in the briefing: automated notifications, marketing, social media alerts

## Outputs

Structured triage map: emails grouped by urgency level with a brief reason for each classification.
