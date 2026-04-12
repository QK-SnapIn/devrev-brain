---
title: Stock Objects
type: feature
status: draft
sources: [raw/test-cases/by-feature/fe_stock_objects.jsonl, raw/docs/devrev-developer-docs.md]
related: []
last_updated: 2026-04-12
---

# Stock Objects

## What it does
Stock Objects is a cross-cutting feature that covers the core domain objects in DevRev: works (issues, tickets, tasks), conversations, parts (features, capabilities, enhancements), artifacts, chats, approvals, metrics/SLAs, code changes, and atoms. With 1916 test cases, it exercises the CRUD and query operations across these fundamental object types, including export, grouping, counting, clustering, batch operations, and complex filtering. This feature represents the backbone data model of DevRev.

## Why it exists
DevRev is built around a unified data model where product development (works, parts, code changes) and customer support (conversations, tickets) coexist. Stock Objects ensures these core entities can be reliably created, retrieved, listed, updated, deleted, exported, and queried with complex filters, pagination, and grouping. Every higher-level feature depends on these operations working correctly.

## Key behaviors
- **Works**: Full CRUD, export (sync/async), grouping, counting, merging, clustering (list, gather, describe), suggest-info
- **Conversations**: CRUD, export (sync/async), grouping, counting; hardcoded to `support` type for group operations; rev user filter override behavior (silently replaces filters with member-based)
- **Parts**: CRUD, mutate (promote types e.g. enhancement to capability), export (sync/async), grouping, counting, contributors/customers/supporters listing, descendant-links traversal
- **Artifacts**: Prepare, create-from-content, copy, get, list, locate, download, versions management (prepare, create-from-content, list, delete), content extraction/validation
- **Chats**: Create DMs and channels, get, list with type filtering, invite users, update; tombstone behavior for deleted users; title silently ignored for default DMs
- **Approvals**: Config CRUD, start/cancel approval flows, tracker management, register user actions, available approvals listing
- **Metrics/SLAs**: Metric definition CRUD, metric workflow CRUD, metric tracker management, metric action execution
- **Code changes**: CRUD with multi-source support (GitHub, GitLab, Bitbucket)
- **Atoms**: Get and summary retrieval
- **Batch**: Apply batch operations across objects
- **Addon rules**: CRUD with associativity filtering (mandatory/optional)

## Entry points
- **Base URL**: `https://api.devrev.ai/internal/`
- All endpoints require `Authorization: Bearer $TOKEN` header
- Both GET (query params) and POST (JSON body) variants for many endpoints

## API endpoints

| Endpoint | Methods | Description |
|----------|---------|-------------|
| `works.create` | POST | Create work item |
| `works.get` | GET, POST | Get work item |
| `works.list` | GET, POST | List work items |
| `works.update` | POST | Update work item |
| `works.delete` | POST | Delete work item |
| `works.count` | GET, POST | Count work items |
| `works.export` | GET, POST | Export works |
| `works.export.async` | POST | Async export works |
| `works.group` | GET, POST | Group work items |
| `works.merge` | POST | Merge work items |
| `works.suggest-info` | GET, POST | Suggest info for works |
| `works.clusters.list` | GET, POST | List work clusters |
| `works.clusters.gather` | GET, POST | Gather work clusters |
| `works.clusters.describe` | POST | Describe work clusters |
| `conversations.get` | GET, POST | Get conversation |
| `conversations.list` | GET, POST | List conversations |
| `conversations.count` | GET, POST | Count conversations |
| `conversations.export` | GET, POST | Export conversations |
| `conversations.export.async` | POST | Async export |
| `conversations.group` | GET, POST | Group conversations |
| `parts.get` | GET, POST | Get part |
| `parts.list` | GET, POST | List parts |
| `parts.count` | GET, POST | Count parts |
| `parts.export` | POST | Export parts |
| `parts.export.async` | POST | Async export parts |
| `parts.group` | GET, POST | Group parts |
| `parts.contributors.list` | GET, POST | List part contributors |
| `parts.customers.list` | GET, POST | List part customers |
| `parts.supporters.list` | GET, POST | List part supporters |
| `parts.descendant-links.traverse` | GET | Traverse descendant links |
| `artifacts.get` | GET, POST | Get artifact |
| `artifacts.list` | GET, POST | List artifacts |
| `artifacts.locate` | GET, POST | Locate artifact |
| `artifacts.download` | GET, POST | Download artifact |
| `artifacts.copy` | POST | Copy artifact |
| `artifacts.contents.extract` | POST | Extract artifact contents |
| `artifacts.contents.prepare` | POST | Prepare artifact contents |
| `artifacts.versions.create-from-content` | POST | Create version from content |
| `artifacts.versions.delete` | POST | Delete artifact version |
| `chats.get` | POST | Get chat |
| `chats.list` | POST | List chats |
| `chats.invite` | POST | Invite to chat |
| `chats.update` | POST | Update chat |
| `approvals.configs.create` | POST | Create approval config |
| `approvals.configs.list` | GET, POST | List approval configs |
| `approvals.configs.update` | POST | Update approval config |
| `approvals.start` | POST | Start approval flow |
| `approvals.cancel` | POST | Cancel approval |
| `approvals.available.list` | GET, POST | List available approvals |
| `approvals.last-tracker.get` | GET, POST | Get last tracker |
| `approvals.trackers.register-user-action` | POST | Register user action |
| `approvals.trackers.update` | POST | Update tracker |
| `metric-definitions.get` | GET, POST | Get metric definition |
| `metric-definitions.list` | GET, POST | List metric definitions |
| `metric-definitions.delete` | POST | Delete metric definition |
| `metric-trackers.get` | GET, POST | Get metric tracker |
| `metric-workflows.create` | POST | Create metric workflow |
| `metric-workflows.get` | GET, POST | Get metric workflow |
| `metric-workflows.list` | GET, POST | List metric workflows |
| `metric-workflows.update` | POST | Update metric workflow |
| `metric-action.execute` | POST | Execute metric action |
| `code-changes.list` | GET, POST | List code changes |
| `code-changes.update` | POST | Update code change |
| `code-changes.delete` | POST | Delete code change |
| `atoms.get` | GET, POST | Get atom |
| `atoms.summary` | GET | Get atom summary |
| `addon-rules.get` | GET, POST | Get addon rule |
| `addon-rules.list` | GET, POST | List addon rules |
| `addon-rules.create` | POST | Create addon rule |
| `addon-rules.update` | POST | Update addon rule |
| `batch.apply` | POST | Batch apply operations |

## Related flows
- [gap] Work item lifecycle flow
- [gap] Conversation support flow
- [gap] Approval workflow flow
- [gap] Artifact upload/download flow

## Related scenarios
- [gap] Scenarios to be created from 1916 test cases

## Ticket Stages

| Group | Stage | Code |
|-------|-------|------|
| Open | Queued | Q |
| In Progress | Work In Progress | WIP |
| In Progress | Awaiting Product Assist | APA |
| In Progress | Awaiting Customer Response | ACR |
| In Progress | Awaiting Development | AD |
| In Progress | In Development | ID |
| Closed | Canceled | C |
| Closed | Accepted | A |
| Closed | Resolved | R |
| Closed | Archived | -- |

See [[entities/ticket]] for full field list and behaviors.

## Issue Stages

| Group | Stage |
|-------|-------|
| Open | Backlog, Prioritized |
| In Progress | In Development, In Review, In Testing, In Deployment |
| Closed | Resolved, Won't Fix (Never), Cancelled |

See [[entities/issue]] for full field list and behaviors.

## Enhancement Stages

| Group | Stages |
|-------|--------|
| Open | Ideation, Prioritized |
| In Progress | UX Design, In Development, In Testing |
| Released | Limited Availability, General Availability |
| Closed | Deprecated, Won't Do, Deprioritized |

See [[entities/enhancement]] for details.

## Part Hierarchy
Product → Capability → Feature (features can be nested)

**Trails view** ([[glossary/trails]]): Visual product hierarchy map showing parts and their relationships.

## Open questions
- [gap] How does the `batch.apply` endpoint work across different object types?
- [gap] How do work clusters relate to individual work items?
- [gap] What triggers metric-action.execute and what side effects does it have?
