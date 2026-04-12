---
title: CSAT (Customer Satisfaction)
type: feature
status: draft
sources: []
related: ["features/conversations-feature", "features/tickets", "features/side-conversations"]
last_updated: 2026-04-12
---

# CSAT (Customer Satisfaction)

## What it does
Tracks customer satisfaction ([[glossary/csat]]) scores on conversations and tickets. Enables measurement of support quality through customer feedback.

## Why it exists
Allows support teams to measure and improve the quality of customer interactions by collecting structured satisfaction feedback.

## Key behaviors

### Scoring mechanism
- 5-point survey scale (button labels are customizable).
- Survey timing, expiry, and introductory text are all configurable.
- [gap] What are the default button labels?

### Survey channels
- Surveys can be delivered via the **portal** or **email**.
- Manual trigger: agents can send a survey using the `/survey` command in Inbox.

### Available on conversations
- Enabled by the **"CSAT on conversation"** snap-in.
- [gap] Exact trigger point in conversation flow (on close? on resolution?).

### Available on tickets
- Enabled by the **"CSAT on ticket"** snap-in.
- [gap] Exact trigger point in ticket lifecycle.

### Alerting
- **CSAT Slack Notifier** snap-in alerts the team when a score is below 4.

### Reporting
- [gap] CSAT dashboards and metrics
- [gap] Agent-level CSAT scores
- [gap] Trend analysis

## Entry points
- [gap] Where is CSAT configured in Settings?
- [gap] Where are CSAT results visible?
- Docs: no specific URL noted.

## Related flows
(none yet)

## Related scenarios
(none yet)

## Open questions
- [gap] Is CSAT tracked on side conversations? (referenced in [[features/side-conversations]])
- [gap] Can CSAT be customized per brand?
- [gap] Integration with analytics dashboards?
