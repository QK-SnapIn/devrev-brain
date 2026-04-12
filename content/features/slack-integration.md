---
title: Slack Integration
type: feature
status: draft
sources: [raw/docs/devrev-agent-dump-integrations.md]
related: [[features/airdrop]]
last_updated: 2026-04-12
---

# Slack Integration

## What it does
The Slack integration connects DevRev with Slack workspaces, enabling bidirectional message syncing, work item creation from Slack, notification routing, and channel-level linking to DevRev customer workspaces. It is installed as a snap-in from the DevRev Marketplace.

## Why it exists
Support and engineering teams live in Slack. This integration lets them create tickets, issues, and incidents without leaving Slack, while keeping DevRev conversations and threads synchronized in both directions.

## Setup flow (step-by-step)

1. Open the DevRev Marketplace and search for **Slack** (or "Slack for Support").
2. Click **Add** in the top-right corner.
3. In snap-in settings, click **Sign in with Slack** -- this redirects to Slack's OAuth page.
4. Select the appropriate Slack workspace and click **Allow** to complete the connection.
5. Add configurations in the snap-in and click **Save**.
6. Click **Install** to activate.
7. To confirm: go to your Slack workspace and run `/devrev help` -- a modal will display all available commands.

**Important notes:**
- Maintain **one public connection per DevRev organization** due to Slack OAuth limitations. Multiple connections can disrupt existing integrations.
- Slack Enterprise workspace support is in limited availability -- contact DevRev Support to be whitelisted first.

## What syncs between Slack and DevRev

- **Conversations:** Customer messages in linked Slack channels create DevRev conversations. Messages in threads sync bidirectionally.
- **Tickets:** Created from Slack, synced bidirectionally (if "Share with everyone" is enabled). External/Connect channels sync to the Customer Messages panel; internal channels sync to Internal Discussions.
- **Issues:** Created from Slack, synced in the Internal Discussions panel. Creating issues with sync from external channels is not supported.
- **Incidents:** Can be created from Slack; sync options include dedicated new channel, thread sync, or notification thread sync.
- **Message edits and deletions** are synced both ways. File attachments up to 250 MB are supported.

## Slash commands

After installation, run `/devrev help` in Slack to see all commands. Key commands:

| Command | Description |
|---------|-------------|
| `/devrev create-ticket` | Opens a new ticket form |
| `/devrev create-issue` | Opens a new issue form |
| `/devrev create-incident` | Opens a new incident form |
| `/devrev link` | Links a Slack channel to a DevRev customer workspace |
| `/devrev view TKT-#` / `/devrev view ISS-#` | View a specific DevRev object |
| `/devrev ticket-digest` | Shows all open and in-progress tickets in a paginated modal |
| `/SlackInviteBot` | (from snap-in event discussions panel) auto-invites the DevRev app to all public channels |

## Notification routing

- **Conversation notifications:** Enable via "Enable the conversation notification feature" in snap-in config. Provide a Slack Channel ID. A 5-minute cooldown prevents notification overload.
- **New ticket notifications:** Enable via "Notify on new ticket creation". Provide a target Slack Channel ID. Fires for all new tickets regardless of source.
- **Ticket state update notifications:** Enable via "Notify on ticket state update". Applies only to tickets already syncing with a Slack thread.
- **Incident notifications:** Configurable to create a new dedicated Slack channel per incident, sync with a thread, or sync with a notification thread.

## Channel linking

- Run `/devrev link` in any Slack channel to link it to a DevRev customer workspace.
- A channel can be linked to **only one** DevRev account workspace, and vice versa.
- Once linked: new contacts identified via Slack are automatically added to the associated workspace; when creating work items, the linked workspace is pre-selected.
- A **conversation roll window** of 5 minutes prevents duplicate conversations for related messages.

## Custom workflow nodes

- Send message on Slack.
- Create new Slack channel.
- Get Slack User ID.
- Start Thread Sync (2-way message sync between a Slack thread and a DevRev object).
- Start Channel Sync (2-way sync between an entire Slack channel and a DevRev object).

## Key behaviors
- One public Slack connection per DevRev org (OAuth limitation).
- Bidirectional message/thread sync with edits and deletions.
- File attachments up to 250 MB.
- 5-minute conversation roll window to prevent duplicates.
- 5-minute cooldown on conversation notifications.
- Slack Enterprise workspace support is limited availability only.

## Entry points
- **Marketplace:** Settings -> Snap-ins -> Explore Marketplace -> search "Slack"
- **Slack side:** `/devrev` slash commands in any channel

## Related flows
- [gap] Slack channel linking flow
- [gap] Ticket creation from Slack flow
- [gap] Incident creation and channel sync flow

## Related scenarios
- [gap] Scenarios to be created

## Open questions
- [gap] What happens when a linked channel is archived in Slack?
- [gap] How are Slack user identities mapped to DevRev users?
- [gap] What is the behavior when the 250 MB attachment limit is exceeded?
