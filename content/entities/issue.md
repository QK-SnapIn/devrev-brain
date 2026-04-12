---
title: Issue
type: entity
status: stable
sources: [raw/docs/devrev-agent-dump-part2.md, raw/docs/devrev-docs-tickets-issues-conversations.md, raw/docs/devrev-agent-dump-part1.md]
related: ["features/stock-objects", "entities/ticket", "entities/enhancement", "entities/part"]
last_updated: 2026-04-12
---

# Issue

## Description
An issue is an internal work item representing a development task, bug fix, or feature implementation. Issues are the primary object in the [[build-app]] (Computer for Builders).

## Issue Hierarchy
Issues support parent-child relationships. An issue can have one parent but multiple children. **Tasks** further break down work into smaller pieces within an issue.

## Stages

| Group | Stage | Description |
|-------|-------|-------------|
| Open | Triage | Newly created, requires categorization |
| Open | Backlog | Accepted but not planned for immediate cycles |
| Open | Prioritized | Planned for current/upcoming development cycle |
| In Progress | In Development | Owner actively working |
| In Progress | In Review | Solution under evaluation |
| In Progress | In Testing | Validation phase |
| In Progress | In Deployment | CD lifecycle active |
| Closed | Completed | Deployment finished |
| Closed | Won't Fix | Cannot be addressed |
| Closed | Duplicate | Redundant with another issue |

## Core Attributes

| Field | Type | Notes |
|-------|------|-------|
| Title | Text | Required |
| Description | Rich text | Supports attachments |
| Owner | User reference | Person responsible for the issue |
| Priority | Dropdown | P0 (highest) through P3 (lowest) |
| Stage | Dropdown | See stages above |
| Part | Part reference | Related product/company section (see [[entities/part]]) |
| Created date | Timestamp | Auto-populated |
| Modified date | Timestamp | Auto-populated |
| Tags | Multi-select | Categorization labels |
| Target close date | Date | Expected resolution deadline |
| Reported by | User reference | Original reporter |
| Close date | Timestamp | Completion timestamp |
| Sprint | Sprint reference | Assigned sprint |
| Display ID | String | Auto-generated |
| Subtype | Dropdown | Custom issue categories (bugs, features) |

Custom attributes can be added via object customization settings (see [[features/customization]]).

## Discussion & Events
The **Discussion tab** enables cross-functional collaboration on issues. The **Events tab** logs key changes: owner assignments, stage transitions, and dependency updates.

## Tags
Common tags: Stalled, Priority/Escalated, Fast/Slow Moving, Blocked, Resolution, Impact, and Reason categories. Autonomous issues created from external events carry the `autonomous` tag.

## Creation Methods
- **UI:** Work > Issues > + Issue button, or from a sprint board backlog
- **From ticket:** Click + Link issue > Add a child issue on a ticket
- **Quick Create:** `+` button or `Cmd+K`
- **API:** `works.create` with issue type
- **Workflow action:** `CreateIssue`
- **GitHub integration:** Automatically creates issues when branches are created
- **Airdrop/AirSync import**

## Sprint Management
- Issues are assigned to sprints.
- **NNL view (Now/Next/Later):** Maps issues to time horizons. See [[glossary/nnl]].
- **Smart Sprint snap-in:** Auto-moves open/in-progress issues to next sprint when current sprint ends.
- **Sprint insights:** Burndown chart, issues by stage/owner/priority/part, sprint health, average time per stage.

## GitHub Integration Auto-Transitions
Issues linked to GitHub PRs auto-transition stages based on PR status:
- New branch created -> issue moves to "In Development"
- PR opened -> issue moves to "In Review"
- Default flow: Triage -> In Development -> In Review -> Completed

## Issue-Ticket Relationship
Issues linked to tickets via `is_dependent_on`. When an issue closes, linked tickets can be automatically updated (via StageFlow Automator snap-in or workflow). All linked customer tickets are visible on every issue.

## Relationship to Enhancements
Issues can be linked to [[entities/enhancement]] objects. Enhancements represent higher-level feature requests; issues represent the development work to implement them.

## List View Filters
Owner, Group, Severity, Stage, Part, Tags, Priority, Sprint, Created date, Target close date.
