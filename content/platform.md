---
title: Platform
type: feature
status: stable
last_updated: 2026-04-12
---

# DevRev Platform

Core platform services powering all three apps. Identity, AI, automation, extensibility, and data management.

## Identity & Access
- [[features/identity]] — User types, SSO/SAML, SCIM, tokens
- [[features/mfz]] — Groups, role sets, access control entries
- [[entities/dev-user]] — Internal users (Regular, Service Account, System User, Shadow)
- [[entities/group]] — User collections for RBAC

## AI & Agents
- [[features/agents]] — Search Agent, Turing AI agent, Computer, Agent Studio
- [[glossary/turing]] — CX AI agent: deflection flow, Suggest/Auto modes

## Automation
- [[features/workflows]] — 48 triggers, actions, AI nodes, error handling, versioning
- [[features/conversational-workflows]] — Customer-facing conversation automation: buttons, forms, AI agent handoff, nudge triggers
- [[features/commands]] — Extensible command framework

## MCP & External AI
- [[features/remote-mcp]] — Remote MCP server (`api.devrev.ai/mcp/v1`): expose DevRev actions as tools for external AI agents
- [[glossary/mcp]] — Model Context Protocol glossary entry

## Data & Sync
- [[features/airdrop]] — Airdrop import engine: recipes, sync units, record manager
- [[glossary/airsync]] — Real-time bidirectional sync
- [[features/slack-integration]] — Slack connector
- [[features/github-integration]] — GitHub connector
- [[features/jira-integration]] — Jira connector
- [[features/email-integration]] — Email channels

## Customization
- [[features/customization]] — Custom fields, subtypes, schema fragments, stages
- [[features/stock-objects]] — Core work object types
- [[entities/org-types]] — 7 org tiers and feature availability

## UI & Navigation
- [[features/search]] — Global search (Cmd+K)
- [[features/vistas]] — Configurable views (list/board/Gantt)
- [[features/inbox]] — Unified conversation hub
- [[features/updates-feed]] — Notification feed (Important/Others)
- [[features/plug-widget]] — In-app widget SDK
- [[features/analytics]] — Dashboards, Text2SQL, export

## Extensibility
- [[features/artifacts]] — File storage and versioning
- [[features/templates]] — Reusable object templates
