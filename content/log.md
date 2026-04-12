# Wiki Log

## [2026-04-12 00:00] init | Wiki scaffold created
- Directory structure created: raw/, wiki/, automation/
- CLAUDE.md schema installed
- No sources ingested yet
- pages touched: [[index]], [[overview]]

## [2026-04-12 12:00] ingest | Bulk feature page creation from JSONL test case files
- Created 18 individual feature pages under wiki/features/ from by-feature JSONL files
- Created 1 combined minor features page for 14 small features (~20 cases each)
- Updated index.md with all 19 feature entries and page count
- All pages are status: draft with [gap] markers for unknowns
- Total test cases covered: ~9,800+ across all feature tags
- pages touched: [[features/identity]], [[features/stock-objects]], [[features/airdrop]], [[features/agents]], [[features/knowledge-base]], [[features/mfz]], [[features/parts]], [[features/commands]], [[features/slas]], [[features/conversations]], [[features/artifacts]], [[features/customization]], [[features/commerce]], [[features/analytics]], [[features/chats]], [[features/brands]], [[features/accounts]], [[features/build]], [[features/_minor-features]], [[index]]

## [2026-04-12 14:00] ingest | Bulk ingest of 5 raw export files into flows, features, and entities
- Ingested 5 source files from raw/exports/:
  1. DevRev Computer Client – Critical User Journeys.md (15 client test scenarios, 6 core journeys)
  2. DevRev Legacy Critical Flows.md (14 critical product flows + coverage matrix)
  3. Org Types and Limitations.md (7 org tiers with feature availability)
  4. Sample.md (Workflow Builder manual test cases: CRUD, canvas, AI steps, import/export)
  5. Side Conversations<>PRD.md (24 test cases for side conversations)
- Created 8 new wiki pages:
  - 2 feature pages: [[features/workflows]], [[features/side-conversations]]
  - 5 flow pages: [[flows/client-critical-journeys]], [[flows/critical-product-flows]], [[flows/automation-priority-matrix]], [[flows/workflow-builder-crud]], [[flows/side-conversation-flow]]
  - 1 entity page: [[entities/org-types]]
- Updated [[index]] with new pages; page count now 28
- All new pages are status: draft with [gap] markers for unknowns
- HTML tables from raw sources converted to clean markdown
- pages touched: [[features/workflows]], [[features/side-conversations]], [[flows/client-critical-journeys]], [[flows/critical-product-flows]], [[flows/automation-priority-matrix]], [[flows/workflow-builder-crud]], [[flows/side-conversation-flow]], [[entities/org-types]], [[index]]

## [2026-04-12 18:00] ingest | Product knowledge dump part 2 (sections 5-14)
- Source: raw/docs/devrev-agent-dump-part2.md (sections 5-14: Conversations, KB, Workflows, Agents, Identity, Integrations, Analytics, Settings, Search, Notifications)
- Updated 11 feature pages with new structured data:
  - [[features/identity]]: user types table, RBAC model, SSO/SAML, token types, role creation steps
  - [[features/knowledge-base]]: article lifecycle, Q&A objects, surfacing methods, collections
  - [[features/workflows]]: complete triggers list, all action categories, AI nodes, utility ops, variable selector, workflow states
  - [[features/agents]]: out-of-box agents, Agent Studio components, testing methods, ticket resolution flow
  - [[features/slas]]: SLA timer types, stage-based start/stop, dashboards
  - [[features/analytics]]: dashboards table, Text2SQL, export options
  - [[features/conversations]]: conversation types, PLuG, email channels, conversion flow, messaging features
  - [[features/side-conversations]]: comment visibility options (external/internal/private)
  - [[features/customization]]: custom field types, schema fragments, dependent fields
  - [[features/airdrop]]: Airdrop vs AirSync distinction, integrations list, connection methods
  - [[features/stock-objects]]: ticket/issue/enhancement stages tables, part hierarchy, Trails view
- Updated [[overview]] with navigation structure, Quick Create list, URL routes, Settings sub-sections
- Created 9 new entity pages: [[entities/ticket]], [[entities/issue]], [[entities/enhancement]], [[entities/conversation]], [[entities/article]], [[entities/account]], [[entities/rev-user]], [[entities/dev-user]], [[entities/group]]
- Created 8 new glossary pages: [[glossary/don]], [[glossary/plug]], [[glossary/turing]], [[glossary/airdrop]], [[glossary/airsync]], [[glossary/trails]], [[glossary/nnl]], [[glossary/vista]]
- Updated [[index]] with all new entries; page count now 46
- Resolved several [gap] markers across feature pages where source provided answers
- pages touched: [[overview]], [[features/identity]], [[features/knowledge-base]], [[features/workflows]], [[features/agents]], [[features/slas]], [[features/analytics]], [[features/conversations]], [[features/side-conversations]], [[features/customization]], [[features/airdrop]], [[features/stock-objects]], [[entities/ticket]], [[entities/issue]], [[entities/enhancement]], [[entities/conversation]], [[entities/article]], [[entities/account]], [[entities/rev-user]], [[entities/dev-user]], [[entities/group]], [[glossary/don]], [[glossary/plug]], [[glossary/turing]], [[glossary/airdrop]], [[glossary/airsync]], [[glossary/trails]], [[glossary/nnl]], [[glossary/vista]], [[index]]

## [2026-04-12 22:00] ingest | Official DevRev docs (scraped) + tickets/issues/conversations deep dive + agent dump part 1
- Sources:
  1. raw/docs/devrev-docs-scraped.md (14 doc pages: Parts, Inbox, Vistas, Workflows, SLA, KB, Articles, SSO, Groups, Roles, Access Control, Object Customization, Customer Portal, Search)
  2. raw/docs/devrev-docs-tickets-issues-conversations.md (Tickets, Issues, Conversations deep dive)
  3. raw/docs/devrev-agent-dump-part1.md (Agent knowledge dump sections 1-5)
- Updated 3 entity pages with official docs content:
  - [[entities/ticket]]: full stock attributes list, CCed members, shadow users, severity levels, Turing Suggests AI, attachment management, follow-up trigger scenarios/messaging, creation UI flow
  - [[entities/issue]]: priority corrected to P0-P3 (not P4), issue hierarchy (parent-child/tasks), stages corrected (Triage/Completed/Duplicate), Discussion & Events tabs, tags list, creation methods expanded
  - [[entities/conversation]]: routing behavior, full stage enumeration (New/Suspended/WOU/NR/Hold/Resolved/Archived), Inbox categorization (Primary/Guest/Spam), tags, time-to-initial-response metric
- Updated 5 feature pages:
  - [[features/parts]]: two part categories (customer/builder), runnable vs linkable, hierarchy levels, stages, stock fields, Trails features
  - [[features/slas]]: three core metrics (first/next response, resolution), creation process, publishing/assignment, metric stages, troubleshooting
  - [[features/knowledge-base]]: article creation methods, required settings, approval workflow, visibility control, content formatting, content blocks, templates, version management, analytics, bulk operations
  - [[features/identity]]: SSO/SAML expanded (JumpCloud added, SP-only, connection naming), Groups (static/dynamic), Roles (actors, scope), Access Control (4-step verification, MFZ policies, Vista privileges)
  - [[features/customization]]: customizable objects list, access/permissions, full field type table (13 types), adding/managing fields, creating/deprecating subtypes
- Created 4 new feature pages:
  - [[features/inbox]]: conversation sources, organization (Primary/Guest/Spam), response management, slash commands
  - [[features/vistas]]: creating/saving/sharing views, toolbar controls, filtering, sorting, view types (List/Board/Gantt), export
  - [[features/search]]: Cmd+K access, operators, field types, custom searches, searchable object types
  - [[features/customer-portal]]: ticket management, KB search, login methods, roles, customization, JIT access, subscriptions
- Created 1 new entity page:
  - [[entities/part]]: hierarchy, customer vs builder parts, stages, stock fields, Trails
- Created 2 new glossary pages:
  - [[glossary/inbox]]: central hub for customer conversations
  - [[glossary/shadow-user]]: non-access tracking users created by AirSync
- Updated [[index]] with all new entries; page count now 54
- Resolved multiple [gap] markers: ticket severity levels, ticket fields, ticket creation UI flow, conversation stages, issue GitHub auto-transitions, SLA metrics/actions, KB article details, identity SSO details, customization field types
- pages touched: [[entities/ticket]], [[entities/issue]], [[entities/conversation]], [[entities/part]], [[features/parts]], [[features/slas]], [[features/knowledge-base]], [[features/identity]], [[features/customization]], [[features/inbox]], [[features/vistas]], [[features/search]], [[features/customer-portal]], [[glossary/inbox]], [[glossary/shadow-user]], [[index]]

## [2026-04-12 23:00] ingest | Feature pages for tickets, issues, conversations
- Created 3 new feature pages to resolve dangling [[links]] in graph view:
  - [[features/tickets]]: ticket lifecycle, creation methods, entry points, links to entities/ticket
  - [[features/issues]]: issue lifecycle, sprints, NNL, GitHub integration, links to entities/issue
  - [[features/conversations-feature]]: conversation lifecycle, routing, Inbox, PLuG/email/Slack, links to entities/conversation
- Fixed [[overview]] links: features/conversations → features/conversations-feature, features/code-changes → features/_minor-features
- Updated [[index]]; page count now 57

## [2026-04-12 23:30] ingest | Deep dive dumps: KB, Workflows, Agents, Settings, Integrations
- Sources:
  1. raw/docs/devrev-agent-dump-kb.md (KB deep dive: article voting, brands, help center, collections)
  2. raw/docs/devrev-agent-dump-workflows.md (Workflows: 48 triggers, error handling, versioning, dry run)
  3. raw/docs/devrev-agent-dump-agents.md (Agents: Turing deflection flow, bulk tests, guardrails, deployment)
  4. raw/docs/devrev-agent-dump-settings.md (Settings: SSO/SAML, SLA, customization, SCIM)
  5. raw/docs/devrev-agent-dump-integrations.md (Integrations: Slack, GitHub, Jira, Airdrop internals)
- Updated 10 existing feature pages:
  - [[features/knowledge-base]]: article voting/feedback, content blocks, templates, version management, 9 article surfaces table, collections deep dive, help center enablement
  - [[features/workflows]]: expanded to 48 triggers, trigger filter conditions, control steps (If/Else + Router), delay steps, ExecuteCode (Python runtime, 30s/120s timeout), Http action, error handling (per-step error paths, Temporal retry), dry run, versioning (semantic, Draft/Published/Paused states, rollback)
  - [[features/agents]]: Search Agent (capabilities, search types, architecture), Turing (deflection flow, modes), Computer (surfaces, capabilities), Instructions/Skills/Knowledge/Guardrails detail, bulk test CSV format, analytics scoring, deployment/versioning, session data
  - [[features/brands]]: multi-brand status, collection-per-brand workaround, portal appearance settings
  - [[features/customer-portal]]: help center configuration, domain setup, multi-language 6-step setup
  - [[features/identity]]: customer portal SSO, SCIM provisioning, session policies, email domain auto-join
  - [[features/slas]]: 9-step creation walkthrough, business hours/org schedules, holiday rules
  - [[features/customization]]: API-based subtype creation, schema fragment types, stage modification API, dependent field conditions
  - [[features/airdrop]]: recipes (pipeline stages), sync units (namespace isolation), record manager, snap-in manager, field mapping UI, filter-by-value, error handling, 8-step setup
  - [[overview]]: settings sub-sections enriched
- Updated 3 entity/glossary pages:
  - [[entities/article]]: dual-dimension lifecycle, 18-field table, content blocks, version management, analytics
  - [[glossary/turing]]: deflection flow (search -> suggest article -> suggest answer -> create ticket), modes (Suggest/Auto), metrics (deflection rate, P90 latency)
  - [[flows/workflow-builder-crud]]: error handling, versioning/rollback, dry run test steps
- Created 4 new integration feature pages:
  - [[features/slack-integration]]: 7-step setup, what syncs, 7 slash commands, notification routing, channel linking
  - [[features/github-integration]]: 5-step setup, PR auto-linking (4 methods), 5 auto stage transitions, magic commands, autonomous issues
  - [[features/jira-integration]]: 6-step setup (Cloud/Data Center), field mapping, 12 object types, sync direction
  - [[features/email-integration]]: channel configuration (gaps noted, ready for enrichment)
- Updated [[index]]; page count now 61
- Resolved numerous [gap] markers across all updated pages
- pages touched: [[features/knowledge-base]], [[features/workflows]], [[features/agents]], [[features/brands]], [[features/customer-portal]], [[features/identity]], [[features/slas]], [[features/customization]], [[features/airdrop]], [[overview]], [[entities/article]], [[glossary/turing]], [[flows/workflow-builder-crud]], [[features/slack-integration]], [[features/github-integration]], [[features/jira-integration]], [[features/email-integration]], [[index]]

## [2026-04-12 23:45] refactor | Product expert review corrections
- **Part hierarchy**: Removed "sub-feature" as a formal hierarchy level across all pages. The official hierarchy is Product -> Capability -> Feature (features can be nested). Fixed in 6 files.
- **Navigation framing**: Added note to overview.md that the official framing is around three apps: Computer for Support Teams, Computer for Builders, and Computer for Growth Teams (Grow).
- **Turing naming**: Changed "Turing" to "Turing AI agent" throughout. Replaced the numbered 7-step deflection model with the correct flow: search -> suggest article -> suggest answer -> create ticket. Fixed in 2 files.
- pages touched: [[entities/part]], [[features/parts]], [[glossary/trails]], [[entities/enhancement]], [[features/stock-objects]], [[features/_minor-features]], [[overview]], [[glossary/turing]], [[features/agents]], [[log]]

## [2026-04-12 24:30] gap-fill | Product detail enrichment for PLuG, Vistas, Analytics, Inbox
- [[features/plug-widget]]: Added sub-components (Widget, AI search, Session recording, Nudges, Push notifications), SDKs table (Web/iOS/Android/React Native), user identity types (Anonymous/Unverified/Verified), branding ("Computer for Your Customers"), docs URL. Removed 8 [gap] markers.
- [[features/vistas]]: Added sub-types table (List/Board/Sprint boards/Vista reports), updated Finding Views to reference Explore (Stock/My/Shared), noted pin-to-nav, RBAC sharing (org-wide or specific people), docs URL.
- [[features/analytics]]: Added Dashboards vs Vistas distinction table, stock dashboards list (7 dashboards), custom dashboards section, dashboard filters (date/tier/severity/spam), docs URL. Removed confusing "Custom dashboards via Vistas" line.
- [[features/inbox]]: Added default views (New-Unassigned/Assigned to me/Open awaiting follow-up), bulk actions (assign/close/link to ticket), inline SLA tracking, CSAT via /survey command, notification channels (in-app/email/browser push/Slack), docs URL.
- Updated [[index]] descriptions for all 4 features.
- pages touched: [[features/plug-widget]], [[features/vistas]], [[features/analytics]], [[features/inbox]], [[index]]

## [2026-04-12 24:00] gap-fill | Product expert review — missing entities, features, and glossary
- Created 4 new entity pages: incident, opportunity, meeting, task
- Created 6 new feature pages: plug-widget, incidents, csat, ola, templates, updates-feed
- Created 4 new glossary pages: incident, opportunity, csat, ola
- All 14 pages are status: draft with extensive [gap] markers — no source docs ingested yet
- Updated [[index]] with all new entries; page count now 75
- pages touched: [[entities/incident]], [[entities/opportunity]], [[entities/meeting]], [[entities/task]], [[features/plug-widget]], [[features/incidents]], [[features/csat]], [[features/ola]], [[features/templates]], [[features/updates-feed]], [[glossary/incident]], [[glossary/opportunity]], [[glossary/csat]], [[glossary/ola]], [[index]]

## [2026-04-12 24:30] gap-fill | New feature and glossary pages for Remote MCP and Conversational Workflows
- Created 2 new feature pages:
  - [[features/remote-mcp]]: DevRev as remote MCP server and client, supported AI clients, OAuth/PAT auth
  - [[features/conversational-workflows]]: Customer-facing conversation automation, buttons/forms/carousels, AI agent handoff, nudge triggers
- Created 2 new glossary pages:
  - [[glossary/mcp]]: Model Context Protocol definition
  - [[glossary/nudge]]: PLuG widget proactive messages
- Updated [[features/workflows]]: added "Conversational Workflows" section linking to the new page
- Updated [[platform]]: added "MCP & External AI" section with remote-mcp; added conversational-workflows under Automation
- Updated [[index]]: page count 79 -> 83, added 2 feature entries and 2 glossary entries
- All new pages are status: draft (features) or stable (glossary) with [gap] markers for unknowns
- pages touched: [[features/remote-mcp]], [[features/conversational-workflows]], [[glossary/mcp]], [[glossary/nudge]], [[features/workflows]], [[platform]], [[index]]
