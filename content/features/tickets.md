---
title: Tickets
type: feature
status: stable
sources: [raw/docs/devrev-docs-tickets-issues-conversations.md, raw/docs/devrev-agent-dump-part2.md]
related: [[entities/ticket]], [[features/stock-objects]], [[features/slas]], [[features/conversations]], [[flows/critical-product-flows]]
last_updated: 2026-04-12
---

# Tickets

## What it does
Tickets are the core support work item in DevRev's [[support-app]] (Computer for Support Teams). They track customer requests for assistance across multiple channels (email, PLuG widget, Slack, customer portal, API) and manage the resolution lifecycle from creation through closure.

## Why it exists
Provides a unified system for tracking, triaging, and resolving customer support requests with SLA enforcement, AI-assisted routing, and cross-team collaboration.

## Key behaviors
- Created via UI, conversation conversion, email, PLuG widget, customer portal, Slack, API, or workflow automation
- Route through stages: Queued → WIP/ACR/APA/AD/ID → Resolved/Canceled/Accepted/Archived
- Support internal tickets (invisible to customers) and external tickets
- Duplicate detection and merging with AI-suggested matches
- Follow-up tickets auto-created when customers respond to archived tickets
- "Turing Suggests" shows similar tickets and KB articles on each ticket view
- SLA timers (First Response, Resolution) tracked per stage transitions
- Linking to issues (is_dependent_on), conversations (is_related_to), and other tickets
- Export to CSV or JSON via Actions menu

## Entry points
- **UI:** Support > Tickets > "New Ticket" button
- **Quick Create:** `+` button or `Cmd+K` → Ticket
- **From Conversation:** Convert conversation to ticket
- **URL:** `app.devrev.ai/<org>/works` (filtered to tickets)
- **API:** `POST /works.create` with `type: ticket`
- **Workflow:** `CreateTicket` action node

## Detailed entity reference
See [[entities/ticket]] for complete field list, stages, priorities, creation flow, merging rules, and follow-up behavior.

## Related flows
- [[flows/critical-product-flows]] — Ticket Creation & Management (Critical priority)

## Related scenarios
[gap] Scenarios to be generated from test cases

## Open questions
- [gap] What are the exact routing rules for auto-assignment?
- [gap] How does the "Needs response" toggle interact with SLA timers?
