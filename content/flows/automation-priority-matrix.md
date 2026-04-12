---
title: "DevRev Platform Critical Test Coverage & Automation Priority Matrix"
type: flow
status: draft
sources: [raw/exports/DevRev Legacy Critical Flows.md]
related: [[flows/critical-product-flows]], [[features/identity]], [[features/stock-objects]], [[features/airdrop]], [[features/analytics]]
last_updated: 2026-04-12
---

# DevRev Platform Critical Test Coverage & Automation Priority Matrix

## Goal
Map which product modules intersect with which flow categories, and assign automation priority levels to guide test automation investment.

## Coverage Matrix

| Module | Login & Access | Ticket Lifecycle | Incident Management | Customer Portal | Search | Integrations | Analytics | Notifications | User & Access Mgmt | Automation Priority |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Authentication | x | | | | | | | | x | High |
| Workspace / Dashboard | x | x | x | | x | | x | x | | High |
| Tickets | | x | | x | x | | | x | | **Critical** |
| Incident Management | | x | x | | x | x | x | x | | **Critical** |
| Customer Portal | | x | | x | x | | | x | | High |
| Search | | x | x | x | x | | | | | High |
| Analytics Dashboard | | x | x | | | | x | | | Medium |
| Notifications / Alerts | | x | x | x | | x | | x | | **Critical** |
| Integrations (Slack, Jira, Salesforce, etc.) | | x | x | | | x | | x | | **Critical** |
| User Groups / Access Control | x | | | | | | | | x | High |
| Help Center / Knowledge Base | | x | | x | x | | | | | Medium |
| Computer / Desktop Client | x | x | x | | x | x | x | x | | High |

## Priority Summary

| Priority | Modules |
| --- | --- |
| **Critical** | Tickets, Incident Management, Notifications / Alerts, Integrations |
| **High** | Authentication, Workspace / Dashboard, Customer Portal, Search, User Groups / Access Control, Computer / Desktop Client |
| **Medium** | Analytics Dashboard, Help Center / Knowledge Base |

## Interpretation Notes
- An "x" indicates the module is exercised by that flow category.
- **Critical** modules touch the highest number of flow categories and represent core product value.
- Modules touching 5+ flow categories should be prioritized for end-to-end automation.
- The Computer / Desktop Client touches 8 of 9 flow categories, making it a high-priority cross-cutting concern.

## Open questions
- [gap] Are there additional modules (e.g., Workflow Builder, Side Conversations) that should be added to this matrix?
- [gap] What is the target automation coverage percentage per priority level?
