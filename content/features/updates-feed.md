---
title: Updates Feed
type: feature
status: draft
sources: []
related: ["features/inbox"]
last_updated: 2026-04-12
---

# Updates Feed

## What it does
A feed/notification hub for tracking changes across work items. Accessible via the "Updates" entry in the left navigation, with sub-tabs for Important and Others.

## Why it exists
Gives users a centralized place to see relevant changes to items they own, follow, or are mentioned in, without needing to check each item individually.

## Key behaviors

### Update types
- Covers: mentions, assignments, stage changes, and field updates across work items.
- Users can **follow** records to receive updates about them.
- [gap] Are updates grouped by object or chronological?

### Important tab
- [gap] What classifies an update as "Important"?
- [gap] Examples: direct mentions, assignments, state changes on owned items?

### Others tab
- [gap] What falls into "Others"?
- [gap] Is this lower-priority notifications or a catch-all?

### Read/unread state
- Supports **mark-as-read**.
- Supports **snooze**.
- Supports configurable **notification preferences**.
- [gap] Bulk mark-as-read?
- [gap] Badge count behavior

## Entry points
- Left nav: "Updates" item
- Docs: https://docs.devrev.ai/product/updates
- [gap] URL route pattern
- [gap] Keyboard shortcut?

## Related flows
(none yet)

## Related scenarios
(none yet)

## Open questions
- [gap] How does Updates Feed relate to email notifications?
- [gap] Can notification preferences be configured per update type?
- [gap] Is there a "mute" or "unfollow" mechanism (beyond unfollowing a record)?
- [gap] Does the feed support real-time updates (WebSocket)?
