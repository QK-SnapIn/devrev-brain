---
title: Minor Features (Combined)
type: feature
status: draft
sources:
  - raw/test-cases/by-feature/fe_snap-ins.jsonl
  - raw/test-cases/by-feature/fe_code_sandbox.jsonl
  - raw/test-cases/by-feature/fe_code_changes.jsonl
  - raw/test-cases/by-feature/fe_support.jsonl
  - raw/test-cases/by-feature/fe_engage.jsonl
  - raw/test-cases/by-feature/fe_bot.jsonl
  - raw/test-cases/by-feature/fe_compliance.jsonl
  - raw/test-cases/by-feature/fe_ai.jsonl
  - raw/test-cases/by-feature/fe_works.jsonl
  - raw/test-cases/by-feature/fe_timeline_entries.jsonl
  - raw/test-cases/by-feature/fe_timeline.jsonl
  - raw/test-cases/by-feature/fe_reactions.jsonl
  - raw/test-cases/by-feature/fe_access_control.jsonl
  - raw/test-cases/by-feature/fe_rbac.jsonl
related: []
last_updated: 2026-04-12
---

# Minor Features (Combined)

This page covers features with approximately 20 or fewer test cases each. These are either small standalone features or cross-cutting concerns that tag a small number of test cases.

---

## Snap-ins (fe_snap-ins)
**~20 cases** | Endpoint: `commands.get`

Snap-ins are DevRev's extensibility mechanism allowing third-party integrations to plug into the platform. The test cases under this tag exercise the `commands.get` endpoint for retrieving snap-in command definitions. [gap] Full snap-in lifecycle (install, configure, uninstall) is not visible from this tag alone -- likely covered under fe_commands and fe_airdrop.

---

## Code Sandbox (fe_code_sandbox)
**~20 cases** | Endpoint: `code-sandboxes.execute`

Code Sandbox provides a secure execution environment for running code snippets within DevRev, likely used by snap-ins or automation workflows. The `code-sandboxes.execute` endpoint runs code in a sandboxed environment and returns results. [gap] What languages/runtimes are supported? What are the execution limits (timeout, memory)?

---

## Code Changes (fe_code_changes)
**~20 cases** | Endpoint: `code-changes.get`

A subset of the Build feature focused specifically on retrieving code change objects. The `code-changes.get` endpoint retrieves a single code change by ID. See [[features/build]] for the full code changes feature.

---

## Support (fe_support)
**~20 cases** | Endpoint: `conversations.group`

The Support tag covers the grouping of support conversations, specifically the `conversations.group` endpoint that groups conversations by stage. This endpoint has a hardcoded `ConversationType: ["support"]` filter -- it exclusively returns support-type conversations regardless of filters. See [[features/conversations]] for related coverage.

---

## Engage (fe_engage)
**~20 cases** | Endpoint: `chats.delete`

The Engage tag covers chat deletion functionality via the `chats.delete` endpoint. This complements the Chats feature with the ability to remove DMs and channels. The backend service is `us_engage`. See [[features/chats]] for related coverage.

---

## Bot (fe_bot)
**~20 cases** | Endpoint: `bot.update`

The Bot feature manages bot configuration within DevRev. The `bot.update` endpoint updates bot properties. [gap] What bot types exist? How do bots relate to AI agents? What properties can be updated?

---

## Compliance (fe_compliance)
**~20 cases** | Endpoint: `audit-logs.fetch`

The Compliance feature provides audit logging capabilities. The `audit-logs.fetch` endpoint retrieves audit log entries for compliance and governance purposes. [gap] What events are logged? What filter/query options are available? What is the retention period?

---

## AI (fe_ai)
**~20 cases** | Endpoint: `metis.respond-to-object`

The AI feature covers the Metis AI response engine, which generates AI-powered responses to objects (likely conversations or tickets). The `metis.respond-to-object` endpoint takes an object reference and returns an AI-generated response. [gap] What object types does Metis support? How does this relate to AI Agents?

---

## Works (fe_works)
**~20 cases** | Endpoint: `works.group`

A subset of the Stock Objects feature focused on work item grouping. The `works.group` endpoint groups work items by specified dimensions. See [[features/stock-objects]] for full works coverage.

---

## Timeline Entries (fe_timeline_entries)
**~20 cases** | Endpoint: `reactions.list`

Timeline entries tag covers listing reactions on timeline entries. The `reactions.list` endpoint retrieves reactions associated with timeline entries. [gap] What timeline entry types exist? How do reactions relate to the timeline data model?

---

## Timeline (fe_timeline)
**~20 cases** | Endpoint: `reactions.update`

The Timeline tag covers updating reactions on timeline items via the `reactions.update` endpoint. [gap] What reaction types are supported (emoji, thumbs up, etc.)? Can reactions be removed?

---

## Reactions (fe_reactions)
**~20 cases** | Endpoint: `reactions.list`

The Reactions feature manages reaction objects on timeline entries and other entities. Overlaps with fe_timeline_entries in using the `reactions.list` endpoint. [gap] Is this a standalone feature or a child feature of Timeline?

---

## Access Control (fe_access_control)
**~20 cases** | Endpoint: `access-control-entries.count`

The Access Control tag covers counting access control entries. The `access-control-entries.count` endpoint returns the number of ACEs matching given filters. See [[features/identity]] and [[features/mfz]] for broader access control coverage.

---

## RBAC (fe_rbac)
**~20 cases** | Endpoint: `roles.create`

The RBAC (Role-Based Access Control) tag covers role creation. The `roles.create` endpoint creates new roles in the system. See [[features/identity]] and [[features/mfz]] for broader role management coverage.

---

## Open questions
- [gap] Should any of these minor features be promoted to full feature pages as more test cases are added?
- [gap] What is the relationship between fe_timeline, fe_timeline_entries, and fe_reactions -- are they one feature or three?
- [gap] How does fe_bot differ from fe_agents conceptually?
