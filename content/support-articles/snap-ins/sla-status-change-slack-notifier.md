---
title: SLA status change Slack notifier
devrev_id: ART-21951
parent_directory: Automate
translation_group: RdtItDkh
modified_date: "2025-12-10T06:57:23.16Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/RdtItDkh"
tags: []
top_category: Snap-ins
wiki_match: features/csat
match_score: 0.379
last_updated: 2026-05-11
---

# SLA status change Slack notifier

Get alerted on your ticket's SLAs. This snap-in sends a notification through Slack to user configured channels, tagging the ticket's owner and subscribers, when a ticket's resolution time SLA changes into the *Warning* or *Breached* stage.

For more information, refer to the [SLA status change Slack notifier snap-in](https://devrev.ai/marketplace/sla-status-change-slack-notifier) on the DevRev
marketplace.

## Installation

1. Create a Slack app for your workspace in <https://api.slack.com/apps>.
2. In App features, generate bot token in **OAuth & Permissions**.
3. Grant the app bot the following permissions: `channel-read`, `groups-read`, `user.profile:read`, `users:read`, `users.read:email`, `chat-write`, and `userGroup-read`.
4. Invite the bot to the workspace.
5. Save the bot access token as connection (snap-in secret) in DevRev app.
6. Invite the bot to the channels where the messages will be sent.
7. In the DevRev app, setup the connection in **Settings** > **Snap-ins** > **Connections** on top.

   * Search and choose an existing connection or create a new one by clicking **+ Connection**.
   * Select **Slack** from the dowpdown list.
   * Give it a name and sign in with Slack. Ensure to toggle on **Make public** to make the connection public for your organization.

## Configure the snap-in

1. In the **Configuration** tab, the first input field to set is *filters*. Here you can declare for which tickets to track the SLA status and to which channels to send notifications.

   Set the ticket subtype, severity, and part; the support heads you would like to tag on the message (the ticket owner gets tagged automatically); and the target Slack channel. The channel's ID can be found by going to the channel details. Refer to the placeholder value on the input to see an example of how this looks.
2. Decide if notifications should go out even if the ticket has a target end date set. Set the toggle to the desired behavior.
3. Decide if a ticket should pass the check if it's part is a descendant of the filter part. For example, if a ticket with part set as "Feature 1" should trigger a notification when the filter is set to "Capability 1" and this is a parent part of that feature. Set the toggle to the desired behavior.
4. Check the default message body and change it if you would like a different phrasing.

## Source
- DevRev support article [SLA status change Slack notifier](https://support.devrev.ai/en-US/devrev/article/RdtItDkh) (ART-21951)
