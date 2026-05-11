---
title: DevRev Brain
---

# DevRev Product Knowledge Wiki

> **459 pages** of structured product knowledge — features, entities, flows, glossary. Built for QA, engineering, and product teams.

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


---

## Support Documentation Mirror

| Category | Articles |
|---------|---------|
| [[support-articles/computer-by-devrev/index|Computer by DevRev]] | 109 |
| [[support-articles/snap-ins/index|Snap-ins]] | 73 |
| [[support-articles/computer-plus-support/index|Computer+ Support]] | 34 |
| [[support-articles/computer-plus-build/index|Computer+ Build]] | 8 |
| [[support-articles/changelog/index|Changelog]] | 7 |
| [[support-articles/computer-plus-observe/index|Computer+ Observe]] | 5 |
| [[support-articles/customer-support-agent/index|Customer Support Agent]] | 3 |

Full crawl of [support.devrev.ai](https://support.devrev.ai/en-US/devrev/directories) (239 articles, 22 directories) cross-linked with existing wiki nodes. Entry point: [[support-articles/index]].


---

## Developer Documentation Mirror

| Category | Pages |
|---|---|
| [[developer-docs/snapin-development/index|Snap-in development]] | 33 |
| [[developer-docs/sdks/index|SDKs]] | 29 |
| [[developer-docs/airsync/index|AirSync (for developers)]] | 25 |
| [[developer-docs/changelog/index|Developer changelog]] | 9 |
| [[developer-docs/about/index|About]] | 6 |
| [[developer-docs/guides/index|Guides]] | 4 |

Curated mirror of [developer.devrev.ai](https://developer.devrev.ai/) (107 pages, 6 categories) — skips the auto-generated API reference. Entry point: [[developer-docs/index]].

## Browse All

- **[[overview]]** — Full product overview with navigation, URLs, settings
- **Flows:** [[flows/critical-product-flows]], [[flows/automation-priority-matrix]], [[flows/workflow-builder-crud]], [[flows/client-critical-journeys]], [[flows/side-conversation-flow]]
- **Org Tiers:** [[entities/org-types]] — Feature availability by plan (Mini/Pro/Max)
