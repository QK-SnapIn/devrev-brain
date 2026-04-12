---
title: Templates
type: feature
status: draft
sources: []
related: ["features/tickets", "features/issues", "features/customization"]
last_updated: 2026-04-12
---

# Templates

## What it does
Provides reusable object templates for creating tickets, issues, and other work items with pre-filled fields and configurations.

## Why it exists
Reduces repetitive data entry and enforces consistency when creating common types of work items.

## Key behaviors
- Available for **tickets**, **issues**, and **workflows**.
- **Workflow templates**: a library of pre-built automation patterns, for example:
  - Suggest ticket severity
  - Disable needs-response on close
  - Send regional notifications
- Workflows support **structured output templates** for AI nodes.
- [gap] What fields can a ticket/issue template pre-fill?
- [gap] Can templates set default assignees, parts, tags, custom fields?
- [gap] How are templates selected during object creation?

## Template management
- [gap] Where are templates created and managed?
- [gap] Who can create/edit templates? (Roles/permissions)
- [gap] Can templates be shared across teams or org-wide?
- [gap] Versioning of templates?

## Entry points
- [gap] Where do templates appear in the creation flow?
- [gap] Are templates available via API?
- Docs: https://docs.devrev.ai/product/template

## Related flows
(none yet)

## Related scenarios
(none yet)

## Open questions
- [gap] How do templates interact with subtypes and custom fields?
- [gap] Are there system-provided default templates beyond the workflow template library?
