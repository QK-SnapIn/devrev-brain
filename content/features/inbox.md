---
title: Inbox
type: feature
status: draft
sources: [raw/docs/devrev-docs-scraped.md]
related: [[entities/conversation]], [[features/conversations]], [[glossary/plug]], [[features/slas]], [[features/csat]]
last_updated: 2026-04-12
docs_url: https://docs.devrev.ai/product/inbox
---

# Inbox

## What it does
DevRev's Inbox ([[glossary/inbox]]) feature is accessible at **Support > Inbox** and serves as a central hub for managing customer conversations. It aggregates conversations from multiple channels and organizes them for efficient response management.

## Why it exists
Support teams need a single place to view and respond to all customer conversations regardless of origin channel. The Inbox provides this unified view with intelligent categorization.

## Conversation Sources
Customers can initiate conversations through multiple channels:
- **Computer widget** (PLuG, embedded on websites/apps) -- see [[glossary/plug]]
- **Email integration**
- **Slack integration**

## Inbox Organization
The system sorts conversations into three categories:

1. **Primary** -- Conversations started by verified customers
2. **Guest** -- Conversations started by a user that is not verified as a customer
3. **Spam** -- Conversations that appear to be malicious, fraudulent, or otherwise invalid

Users can mark erroneously categorized spam as "Not spam."

## Response Management
Customer experience engineers respond to conversations through the same channel the customer used initially. Responses are sent back through the originating channel.

## Default Views
The Inbox provides three default views:
1. **New / Unassigned** — conversations with no owner, awaiting triage
2. **Assigned to me** — conversations owned by the current user
3. **Open awaiting follow-up** — conversations that need further action

## Bulk Actions
From the Inbox list, users can select multiple conversations and perform:
- **Assign** — assign to a team member or group
- **Close** — close selected conversations
- **Link to ticket** — associate conversations with existing or new tickets

## SLA Tracking
SLA timers are shown **inline** on each conversation in the Inbox. This provides at-a-glance visibility into response/resolution deadlines without opening individual conversations. See [[features/slas]].

## CSAT Surveys
CSAT surveys can be **manually triggered** via the `/survey` slash command typed in the conversation response box. See [[features/csat]].

## Slash Commands
Users can access available commands by typing "/" in the response text box within conversations. These commands assist with conversation management. Known commands include:
- `/survey` — triggers a CSAT survey to the customer
- [gap] Full list of other available slash commands

## Notifications
Inbox supports multiple notification channels:
- **In-app** — notifications within the DevRev application
- **Email** — email alerts for conversation activity
- **Browser push** — browser push notifications
- **Slack** — Slack integration notifications (see [[features/slack-integration]])

## Entry points
- **URL:** Support > Inbox in left navigation
- Default pinned view in left nav sidebar
- Docs: https://docs.devrev.ai/product/inbox

## Related flows
- [gap] Inbox triage and response flow

## Related scenarios
- [gap] Scenarios to be defined

## Open questions
- [gap] Full list of slash commands beyond `/survey`
- [gap] What are the sorting/filtering options within Inbox?
- [gap] Can custom Inbox views be created beyond the 3 defaults?
