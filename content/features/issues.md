---
title: Issues
type: feature
status: stable
sources: [raw/docs/devrev-docs-tickets-issues-conversations.md, raw/docs/devrev-agent-dump-part2.md]
related: ["entities/issue", "features/stock-objects", "features/parts", "features/build", "flows/critical-product-flows"]
last_updated: 2026-04-12
---

# Issues

## What it does
Issues are the core development work item in DevRev's [[build-app]] (Computer for Builders). They track product development tasks, support parent-child hierarchies, integrate with sprint boards, and auto-link to code changes from GitHub/GitLab.

## Why it exists
Provides a structured system for planning, tracking, and completing engineering work with sprint management, priority-based planning (Now/Next/Later), and automatic stage transitions from code activity.

## Key behaviors
- Created via UI, from tickets (child issue), API, workflow, or GitHub integration
- Route through stages: Triage/Backlog/Prioritized → In Development/Review/Testing/Deployment → Completed/Won't Fix/Duplicate
- Parent-child hierarchy: one parent, multiple children; tasks break down further
- Sprint management: sprint boards, backlog, burndown charts, Smart Sprint snap-in
- NNL (Now/Next/Later) view: Now = In Progress, Next = Prioritized, Later = Backlog
- GitHub auto-transitions: branch created → In Development, PR opened → In Review
- Priority levels: P0 (highest) through P3 (lowest)
- Linked to tickets via `is_dependent_on` — when issue closes, linked tickets can auto-update
- Discussion tab for collaboration, Events tab for change history
- Export to CSV (max 5,000) or JSON

## Entry points
- **UI:** Work > Issues > "+ Issue" button
- **Quick Create:** `+` button or `Cmd+K` → Issue
- **From Ticket:** "+ Link issue" > "Add a child issue"
- **Sprint Board:** Add from Backlog tab
- **URL:** `app.devrev.ai/<org>/works` (filtered to issues)
- **API:** `POST /works.create` with `type: issue`
- **Workflow:** `CreateIssue` action node

## Detailed entity reference
See [[entities/issue]] for complete field list, stages, sprint details, hierarchy, and GitHub integration behavior.

## Related flows
- [[flows/critical-product-flows]] — Issue lifecycle (High priority)

## Related scenarios
[gap] Scenarios to be generated from test cases

## Open questions
- [gap] What are the exact auto-transition rules for GitLab and Bitbucket (vs GitHub)?
- [gap] How does the Smart Sprint snap-in decide which issues to carry forward?
