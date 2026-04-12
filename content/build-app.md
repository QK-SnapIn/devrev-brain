---
title: Build App
type: feature
status: stable
last_updated: 2026-04-12
---

# Computer for Builders

Product development tool. Issue tracking, sprint management, product hierarchy, code integration, and enhancement planning.

## Core Objects
- [[entities/issue]] — Development work items (P0-P3 priority)
- [[entities/enhancement]] — Product improvements (epic-level)
- [[entities/part]] — Product hierarchy (Product → Capability → Feature)
- [[entities/task]] — Lightweight work breakdown items

## Features
- [[features/issues]] — Issue lifecycle, sprints, NNL view, parent-child hierarchy
- [[features/parts]] — Product hierarchy, Trails visualization, customer vs builder parts
- [[features/build]] — Code changes tracking
- [[features/analytics]] — Sprint insights, burndown charts

## Code Integrations
- [[features/github-integration]] — PR auto-linking, stage transitions, magic commands
- [[features/jira-integration]] — Bidirectional sync, field mapping, 12 object types

## Automation
- [[features/workflows]] — Issue routing, stage automation, AI classification
- [[features/commands]] — Extensible command framework
