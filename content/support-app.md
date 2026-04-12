---
title: Support App
type: feature
status: stable
last_updated: 2026-04-12
---

# Computer for Support Teams

Customer support command center. AI-powered ticket resolution, multi-channel conversations, SLA enforcement, and knowledge base management.

## Core Objects
- [[entities/ticket]] — Customer support requests with lifecycle stages
- [[entities/conversation]] — Real-time discussions across channels
- [[entities/incident]] — Service disruptions with on-call and broadcasts
- [[entities/article]] — Knowledge base documents

## Features
- [[features/tickets]] — Ticket creation, stages, merging, follow-ups, Turing Suggests
- [[features/conversations-feature]] — Multi-channel conversations (PLuG, email, Slack)
- [[features/inbox]] — Unified conversation management (Primary/Guest/Spam)
- [[features/incidents]] — Incident management, on-call, broadcasts
- [[features/knowledge-base]] — Articles, Q&A, collections, 9 surfaces
- [[features/slas]] — SLA policies, First Response & Resolution timers
- [[features/ola]] — Operational-Level Agreements for internal teams
- [[features/csat]] — Customer satisfaction scoring ([[glossary/csat]])
- [[features/side-conversations]] — Side threads for external collaboration
- [[features/customer-portal]] — Self-service portal for customers
- [[features/brands]] — Brand management for customer-facing identity
- [[features/templates]] — Reusable ticket/conversation templates
- [[features/chats]] — Internal DMs and channels

## AI & Automation
- [[features/agents]] — Turing AI agent for deflection and auto-resolution
- [[features/workflows]] — Automated ticket routing, classification, notifications

## Channels
- [[features/plug-widget]] — In-app chat widget (PLuG SDK)
- [[features/email-integration]] — Email channel configuration
- [[features/slack-integration]] — Slack integration for support

## Key Flows
- [[flows/critical-product-flows]] — Ticket lifecycle, incident escalation, customer portal
- [[flows/automation-priority-matrix]] — Module automation priorities
