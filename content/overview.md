---
title: Product Overview
type: overview
status: stable
sources: [raw/docs/devrev-developer-docs.md, raw/test-cases/summary.md, raw/docs/devrev-agent-dump-settings.md]
last_updated: 2026-04-12
---

# Product Overview

## What it is

DevRev is an AI-powered platform that unifies product development, customer support, and business operations. Its core product, **Computer**, acts as an AI teammate that connects all business data (tickets, issues, knowledge base articles, customer records) and provides intelligent automation through specialized AI agents.

## Who uses it

- **Dev users** (`devu`) — Internal developers and team members who build, manage, and operate the product. They interact via the Build app, APIs, and snap-ins.
- **Rev users** (`revu`) — External customers and end-users who interact via the Support widget (Plug SDK), portals, and conversations.
- **System users** (`sysu`) — Automated services and integrations acting on behalf of the organization.

## Main modules / features

### [[support-app]] — Computer for Support Teams
Tickets, conversations, SLAs, knowledge base, incidents, CSAT, AI-powered resolution.

### [[build-app]] — Computer for Builders
Issues, sprints, parts & trails, enhancements, code integrations (GitHub/Jira).

### [[grow-app]] — Computer for Growth Teams
Opportunities, accounts, contacts, meetings, CRM integrations.

### [[platform]] — Platform Services
Identity & RBAC, AI agents, workflows, search, customization, data sync, extensibility.

## Glossary highlights

- **DON** — DevRev Object Notation, the unique ID format: `don:identity:dvrv-us-1:devo/0:devu/30`
- **Work** — Umbrella term for actionable items: tickets, issues, conversations, enhancements
- **Part** — Product hierarchy node: Product → Capability → Feature (features can be nested)
- **Snap-in** — A plugin/extension built on the DevRev extensibility framework
- **Airdrop** — DevRev's data import/sync pipeline for ingesting external data
- **PAT** — Personal Access Token, used for API authentication
- **Plug** — The customer-facing support widget (web/mobile SDK)

See [[glossary/don]], [[glossary/turing]], [[glossary/airdrop]], [[glossary/plug]], [[glossary/mcp]] and other entries under Glossary.

## Key user flows

1. [[features/tickets]] — Ticket created → triaged → resolved → closed
2. [[features/issues]] — Issue created → assigned → developed → verified → closed
3. [[features/airdrop]] — External data synced into DevRev via airdrop snap-ins
4. [[features/identity]] — Create/invite users, assign roles, manage groups
5. [[features/agents]] — AI agent auto-resolves customer tickets using KB
6. [[flows/critical-product-flows]] — 14 critical product flows with automation priorities
7. [[flows/client-critical-journeys]] — Desktop/web client critical user journeys

## Navigation Structure

| Section | Purpose |
|---------|---------|
| Work | Issues, tickets, tasks |
| Product | Parts, trails, enhancements, roadmap |
| Customer | Accounts, contacts, conversations, inbox |
| People | Users, groups |

> **Note:** The official product framing is organized around three apps: **Computer for Support Teams**, **Computer for Builders**, and **Computer for Growth Teams (Grow)**. The nav sections above (Work, Product, Customer, People) are the top-level labels within the UI, but the three-app model is how DevRev positions the platform externally.

## Quick Create Objects
From the `+` button (or `Cmd+K` / `Ctrl+K`), users can create:
Ticket, Issue, Conversation, Enhancement, Account, Contact, Opportunity, Incident, Meeting, Article.

## Key URL Routes

| Page | URL pattern |
|------|-------------|
| App root / Updates | `app.devrev.ai/<org-slug>` |
| Tickets | `app.devrev.ai/<org>/works` (filtered to tickets) |
| Issues | `app.devrev.ai/<org>/works` (filtered to issues) |
| Settings | `app.devrev.ai/<org>/settings` |
| Workflows | `app.devrev.ai/<org>/settings/workflows` |
| Object customization | `app.devrev.ai/?setting=object-customization?type=ticket` |
| User roles | `app.devrev.ai?setting=user-roles` |
| Customer roles | `app.devrev.ai?setting=customer-roles` |
| Agent settings | `app.devrev.ai/<org>/settings/agent` |
| Knowledge base | `app.devrev.ai/<org>/settings/knowledge-base` |

## Settings Sub-sections

| Settings area | Notes |
|---------------|-------|
| General | Profile, preferences, org settings, language & region |
| Account | Users, invitations, connections to external apps |
| Security | Auth, SSO/SAML, access control |
| Agent | AI agent preferences, analytics, content |
| Support | PLuG widget, email channel, customer portal, auto-responses |
| SLA | SLA policy creation, business hours, assignment rules |
| Workflows | Workflow builder |
| Object customization | Custom fields, stages, subtypes, schema fragments |
| User Management > Roles | User role creation and assignment |
| User Management > Groups | Static and dynamic group management |
| Customer Management > Roles | Customer role management |
| Integrations > Snap-ins | Install/manage snap-ins from marketplace |
| Integrations > AirSync | Data import/sync management (Jira, Zendesk, Salesforce, etc.) |
| Knowledge Base | Articles, Q&A, collections, content blocks, templates |

## API Architecture

- **Base URL:** `https://api.devrev.ai`
- **Auth:** Bearer token (PAT, AAT, SUT, or Session Token)
- **Format:** REST, JSON responses, OpenAPI 3.0 spec
- **Versioning:** `X-Devrev-Version: 2022-10-20` (default), `X-Devrev-Scope: beta` for beta APIs
