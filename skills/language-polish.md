---
type: skill
id: language-polish
title: Language Polish
description: "Spelling, grammar, punctuation, sentence clarity, and minor wording cleanup"
tags: [Production, Quality]
connections:
  - target: llm-service
    type: runs_on
context_params:
  voice_profile:
    label: "Voice Profile"
    description: "Creator's writing style, vocabulary, sentence patterns, and banned words"
    required: false
  grammar_strictness:
    label: "Grammar Strictness"
    description: "How strict to be with grammar rules — Casual, Conversational, Professional, or Academic"
    default: "Professional"
    required: false
---

## Capability

Corrects spelling, grammar, and punctuation errors. Improves sentence clarity by simplifying convoluted phrasing, fixing awkward constructions, and tightening verbose passages.

This is a surface-level polish — it does NOT rewrite for tone, restructure arguments, or reposition content for a different audience.

## What It Does

1. **Spelling and grammar** — corrects errors, including context-dependent ones
2. **Punctuation** — fixes missing or misplaced commas, full stops, semicolons, and quotation marks
3. **Sentence clarity** — simplifies unnecessarily complex sentences without changing meaning
4. **Word choice** — replaces jargon or vague phrasing with clearer alternatives where unambiguous
5. **Consistency** — standardises British English spelling throughout

## Outputs

Polished text with corrections applied.
