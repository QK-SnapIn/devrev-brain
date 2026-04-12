---
title: DevRev Brain
---

# DevRev Product Knowledge Wiki

> **83 pages** of structured product knowledge — features, entities, flows, glossary. Built for QA, engineering, and product teams.

---

## Product Apps

| App | Description | Key Pages |
|-----|-------------|-----------|
| **[[support-app]]** | Customer support: tickets, conversations, SLAs, KB, incidents | [[features/tickets]], [[features/slas]], [[features/knowledge-base]] |
| **[[build-app]]** | Product development: issues, sprints, parts, code integration | [[features/issues]], [[features/parts]], [[features/workflows]] |
| **[[grow-app]]** | CRM & revenue: opportunities, accounts, meetings | [[entities/opportunity]], [[features/accounts]] |
| **[[platform]]** | Core services: identity, AI agents, search, customization | [[features/identity]], [[features/agents]], [[features/search]] |

---

## Core Objects

| Object | Stages | Key Detail |
|--------|--------|------------|
| [[entities/ticket]] | Queued → WIP/ACR/APA → Resolved/Archived | 4 severities, P0-P4, 8 creation methods |
| [[entities/issue]] | Triage → In Dev/Review/Test → Completed | P0-P3, parent-child, sprint boards |
| [[entities/conversation]] | New → WOU/NR/Hold → Resolved | Primary/Guest/Spam routing |
| [[entities/enhancement]] | Ideation → Development → GA | Epic-level, groups issues |
| [[entities/part]] | Ideation → Deployed → Deprecated | Product → Capability → Feature |
| [[entities/incident]] | Detection → Resolution | On-call, broadcasts, alerts |
| [[entities/article]] | Draft → Published → Archived | 9 surfaces, multi-language |

---

## AI & Automation

| Feature | What it does |
|---------|-------------|
| [[features/agents]] | Search Agent, Turing AI agent, Computer + Agent Studio |
| [[features/workflows]] | 48 triggers, AI nodes, error handling, versioning |
| [[features/conversational-workflows]] | Customer-facing button/form flows + AI handoff |
| [[features/remote-mcp]] | Expose DevRev as MCP server for Claude, Copilot, Gemini |

---

## Integrations

| Integration | Sync Type |
|-------------|-----------|
| [[features/slack-integration]] | Conversations, tickets, 7 slash commands |
| [[features/github-integration]] | PR auto-link, stage transitions, magic commands |
| [[features/jira-integration]] | Bidirectional, 12 object types |
| [[features/email-integration]] | Inbound ticket creation, threading |
| [[features/airdrop]] | Bulk import + periodic sync (recipes, sync units) |

---

## Customer Experience

| Feature | Description |
|---------|-------------|
| [[features/plug-widget]] | In-app widget: chat, AI search, session recording, nudges |
| [[features/customer-portal]] | Self-service portal with KB, tickets, SSO |
| [[features/csat]] | 5-point satisfaction surveys via snap-ins |
| [[features/inbox]] | Unified support workspace with SLA tracking |

---

## Configuration & Admin

| Area | Key Pages |
|------|-----------|
| Identity & RBAC | [[features/identity]], [[entities/group]], [[features/mfz]] |
| Customization | [[features/customization]], [[features/templates]] |
| SLA / OLA | [[features/slas]], [[features/ola]] |
| Analytics | [[features/analytics]], [[features/vistas]] |
| Navigation | [[features/search]], [[features/updates-feed]] |

---

## Quick Reference

| Term | Definition |
|------|-----------|
| [[glossary/don]] | DevRev Object Notation — unique ID format |
| [[glossary/turing]] | CX AI agent for ticket deflection |
| [[glossary/airdrop]] | Data import engine |
| [[glossary/airsync]] | Real-time bidirectional sync |
| [[glossary/mcp]] | Model Context Protocol server |
| [[glossary/plug]] | Customer-facing chat widget |
| [[glossary/trails]] | Visual product hierarchy |
| [[glossary/nnl]] | Now/Next/Later issue planning |
| [[glossary/vista]] | Configurable views |
| [[glossary/csat]] | Customer satisfaction score |
| [[glossary/ola]] | Operational-Level Agreement |
| [[glossary/nudge]] | Proactive PLuG widget messages |

---

## Browse All

- **[[overview]]** — Full product overview with navigation, URLs, settings
- **Flows:** [[flows/critical-product-flows]], [[flows/automation-priority-matrix]], [[flows/workflow-builder-crud]], [[flows/client-critical-journeys]], [[flows/side-conversation-flow]]
- **Org Tiers:** [[entities/org-types]] — Feature availability by plan (Mini/Pro/Max)
