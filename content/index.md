# Wiki Index
_Last updated: 2026-04-12  ·  Pages: 83_

## Product Drill-Down
- [[overview]] — Product summary, navigation structure, URL routes, settings areas
- [[support-app]] — Computer for Support Teams: tickets, conversations, SLAs, KB, incidents, CSAT
- [[build-app]] — Computer for Builders: issues, sprints, parts, enhancements, code integrations
- [[grow-app]] — Computer for Growth Teams: opportunities, accounts, meetings, CRM
- [[platform]] — Platform services: identity, AI agents, workflows, search, customization, data sync

## Features (40)
- [[features/identity]] — Authentication, SSO/SAML (Okta/Azure/Google/JumpCloud), Groups (static/dynamic), Roles, Access Control (3015 cases)
- [[features/stock-objects]] — Core domain objects: works, conversations, parts, artifacts, chats, approvals, metrics (1916 cases)
- [[features/airdrop]] — Airdrop/AirSync: recipes, sync units, record manager, field mapping, filter-by-value, error handling (1637 cases)
- [[features/agents]] — AI agents (Search, Turing, Computer), Agent Studio (instructions/skills/knowledge/guardrails), testing, deployment (1107 cases)
- [[features/inbox]] — Central hub for conversations: default views (New/Assigned/Awaiting), bulk actions, inline SLA tracking, CSAT via /survey, multi-channel notifications
- [[features/knowledge-base]] — Articles lifecycle, creation, approval, voting/feedback, content blocks, templates, collections, Q&A, 9 surfaces (493 cases)
- [[features/mfz]] — Groups, role sets, roles, access control entries (274 cases)
- [[features/parts]] — Product hierarchy: customer vs builder parts, runnable/linkable, stages, Trails (180 cases)
- [[features/commands]] — Custom command management and execution (131 cases)
- [[features/search]] — Global search: Cmd+K, operators, field types, custom searches, searchable object types
- [[features/slas]] — SLA metrics (First/Next Response, Resolution), policies, publishing, metric stages (95 cases)
- [[features/conversations]] — Conversation types, PLuG, email channels, conversion flow, messaging (80 cases)
- [[features/artifacts]] — File storage, versioning, and content validation (80 cases)
- [[features/customer-portal]] — Support portal: ticket management, KB search, JIT access, customization, login methods
- [[features/customization]] — Object customization: custom fields, subtypes, field types, deprecation (80 cases)
- [[features/vistas]] — Configurable views: list/board/sprint boards/vista reports, filtering, sorting, grouping, RBAC sharing, export
- [[features/commerce]] — SKUs, addon rules, account commerce details (80 cases)
- [[features/analytics]] — Dashboards (stock + custom, SQL-backed widgets), Text2SQL, filters (date/tier/severity/spam), NL query execution (75 cases)
- [[features/chats]] — DMs and channels for internal communication (60 cases)
- [[features/brands]] — Brand management for customer-facing identity (51 cases)
- [[features/accounts]] — Account updates, duplicate detection, CSV support (50 cases)
- [[features/build]] — Code changes from GitHub, GitLab, Bitbucket (40 cases)
- [[features/_minor-features]] — 14 minor features: snap-ins, code sandbox, code changes, support, engage, bot, compliance, AI, works, timeline entries, timeline, reactions, access control, RBAC (~20 cases each)
- [[features/workflows]] — Workflow Builder: 48 triggers, actions, AI nodes, error handling, versioning, dry run, ExecuteCode runtime
- [[features/side-conversations]] — Side threads, comment visibility (external/internal/private), forwarding, SLA/CSAT tracking
- [[features/tickets]] — Ticket lifecycle: creation, stages, merging, follow-ups, Turing Suggests, SLA tracking
- [[features/issues]] — Issue lifecycle: sprints, NNL view, GitHub auto-transitions, parent-child hierarchy
- [[features/conversations-feature]] — Conversation lifecycle: PLuG, email, Slack, routing, Inbox categorization, conversion to ticket
- [[features/slack-integration]] — Slack: setup flow, what syncs, 7 slash commands, notification routing, channel linking
- [[features/github-integration]] — GitHub: setup, PR auto-linking, auto stage transitions, magic commands, autonomous issues
- [[features/jira-integration]] — Jira: setup (Cloud/Data Center), field mapping, sync direction, 12 object types
- [[features/email-integration]] — Email: channel configuration, inbound ticket creation, outbound, threading
- [[features/plug-widget]] — PLuG ("Computer for Your Customers"): widget, AI search, session recording, nudges, push notifications; Web/iOS/Android/React Native SDKs
- [[features/incidents]] — Incident management: creation, stages, severity, on-call, broadcasts, analytics
- [[features/csat]] — Customer satisfaction scoring on conversations and tickets
- [[features/ola]] — Operational-Level Agreement: internal team commitment tracking
- [[features/templates]] — Reusable object templates for tickets, issues, etc.
- [[features/updates-feed]] — Updates hub: feed/notifications for tracking changes (Important/Others tabs)
- [[features/remote-mcp]] — Remote MCP server: expose DevRev actions as tools for external AI agents (Claude, Copilot, Gemini)
- [[features/conversational-workflows]] — Customer-facing conversation automation: buttons, forms, AI agent handoff, nudge triggers

## Flows (5)
- [[flows/client-critical-journeys]] — 6 core journeys (15 scenarios) for the DevRev desktop/web client across platforms
- [[flows/critical-product-flows]] — 14 critical product flows covering authentication, tickets, incidents, integrations, analytics
- [[flows/automation-priority-matrix]] — Coverage matrix mapping 12 modules to 10 flow categories with automation priority levels
- [[flows/workflow-builder-crud]] — Full CRUD lifecycle for Workflow Builder: create, edit, deploy, delete, canvas, AI steps, import/export
- [[flows/side-conversation-flow]] — End-to-end flow for side conversations: forwarding, threads, external collab, SLA/CSAT, analytics

## Scenarios (0)

## Entities (15)
- [[entities/org-types]] — 7 DevRev org tiers (Computer Mini/Pro/Max, Support Pro bundles, Build Pro bundles) and feature availability matrix
- [[entities/ticket]] — Support work item: stock attributes, stages, Turing Suggests AI, attachment management, follow-ups, merging
- [[entities/issue]] — Development work item: P0-P3 priority, hierarchy (parent-child/tasks), Discussion & Events tabs, tags
- [[entities/enhancement]] — Product improvement request: stages (Open/In Progress/Released/Closed)
- [[entities/conversation]] — Communication thread: routing, stages (New/WOU/NR/Hold/Resolved), Inbox categorization, tags, metrics
- [[entities/part]] — Product hierarchy component: customer vs builder parts, runnable/linkable, stages, Trails
- [[entities/article]] — Knowledge base document: lifecycle (Draft/Published/Archived), scope, collections
- [[entities/account]] — Customer organization: fields, actions, relationships
- [[entities/rev-user]] — External customer/contact: lifecycle stages (0-New through 6-Qualified Out)
- [[entities/dev-user]] — Internal team member: types (Regular, Service Account, System User, Shadow User)
- [[entities/group]] — User collection for RBAC: role assignments, customer groups
- [[entities/incident]] — Service disruption object: stages, severity, on-call, broadcasts, analytics
- [[entities/opportunity]] — CRM deal object (Grow app): stages, ACV/TCV, forecast, MEDDPICC
- [[entities/meeting]] — Trackable meeting object: channel types, state, members, sentiment
- [[entities/task]] — Lightweight work item for breaking down work into smaller pieces

## APIs (0)

## Locators (0)

## Bugs (0)

## Glossary (16)
- [[glossary/don]] — DevRev Object Notation: unique ID format for all objects
- [[glossary/plug]] — Customer-facing chat widget (web/mobile SDK)
- [[glossary/turing]] — DevRev's CX AI agent: deflection flow, Suggest/Auto modes, metrics (deflection rate, P90 latency)
- [[glossary/airdrop]] — Data import engine for external systems
- [[glossary/airsync]] — Real-time bidirectional sync engine
- [[glossary/trails]] — Visual product hierarchy map
- [[glossary/nnl]] — Now/Next/Later view for issue planning
- [[glossary/vista]] — Configurable list/board views
- [[glossary/inbox]] — Central hub for managing customer conversations
- [[glossary/shadow-user]] — Non-access tracking users created by AirSync
- [[glossary/incident]] — First-class object for managing service disruptions
- [[glossary/opportunity]] — CRM object in Grow app for tracking sales deals
- [[glossary/csat]] — Customer Satisfaction score on conversations and tickets
- [[glossary/ola]] — Operational-Level Agreement for internal team commitments
- [[glossary/mcp]] — Model Context Protocol: DevRev as remote MCP server and client
- [[glossary/nudge]] — Proactive PLuG widget messages; can trigger conversational workflows
