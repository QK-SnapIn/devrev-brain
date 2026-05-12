---
title: Slack Broadcaster
devrev_id: ART-21967
parent_directory: Automate
translation_group: aE1x22U7
modified_date: "2025-12-10T06:57:33.019Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/aE1x22U7"
tags: []
top_category: Snap-ins
wiki_match: features/slack-integration
match_score: 0.529
last_updated: 2026-05-11
summary: "The Slack Broadcaster snap-in is a specialized automation tool designed to streamline the process of posting broadcast messages, both for customers and within your organization."
---

# Slack Broadcaster

The [Slack Broadcaster](https://marketplace.devrev.ai/slack-broadcaster) snap-in is a specialized automation tool designed to streamline the process of posting broadcast messages, both for customers and within your organization. Seamlessly integrated with Slack, it facilitates the dissemination of vital updates and accomplishments.

## Configurations

### Slack Connection

To use the snap-in, you'll need to connect Slack with DevRev. During installation, you'll receive guidance to connect and configure it.
For detailed instructions, refer to the [Slack snap-in docs](https://app.devrev.ai/devrev/settings/knowledge-base/articles/ART-21978).

## Features

* **Customer release notes**: Automatically share release notes with customers via Slack Connect channels.
* **[[entities/account|Account]] linking**: Link Slack channels to [[features/accounts|accounts]] using the `/slack_broadcaster_link <channel_id>` command in the account timeline. To unlink, use `/slack_broadcaster_link invalid`.
* **Bulk account update**: Link multiple accounts using `/slack_broadcaster_upload external` or `/slack_broadcaster_upload internal` and upload a CSV with account display names and Slack channel IDs.
* **Internal release notes**: Share internal updates by uploading a CSV with channel names and IDs using `/slack_broadcaster_upload internal`.
* **Configuration management**: Only authorized users in specific [[entities/group|groups]] can post to Slack channels.

## Slash Commands

The Slack Broadcaster snap-in provides intuitive slash [[features/commands|commands]] to streamline release note posting and management:

* `/slack_broadcaster_link <channel_id>`: Links an account to a Slack channel.
* `/slack_broadcaster_upload internal`: Uploads a CSV for internal broadcasts.
* `/slack_broadcaster_upload external`: Uploads a CSV for private or public customer channels.
* `/slack_broadcaster_show_links`: Displays all linked accounts and internal channels.
* `/slack_broadcast`: Broadcasts updates directly to Slack.
* `/slack_broadcast_by_tags`: Broadcasts updates to accounts filtered by selected tags.
* `/periodic_slack_broadcast`: Periodically broadcasts updates to Slack.
* `/schedule_slack_broadcast`: Schedules a broadcast for a specific date and time.
* `/cancel_all_scheduled_broadcasts`: Cancels all scheduled and periodic broadcasts.

Ensure to run these commands in the **DevRev app snap-in > Events** tab for them to function correctly.

## How to use

1. **Set up Slack Connection**

   * Connect your Slack workspace with DevRev.
   * Invite the DevRev agent to your Slack private and public channels using the `/invite` command in Slack.
2. **Broadcasting messages**

   * Use the `/slack_broadcast` command to broadcast to customers.
3. **Broadcasting by tags**

   * Use the `/slack_broadcast_by_tags` command to broadcast to accounts filtered by tags.
   * Select the desired tags to filter accounts, then write and send your message.
4. **Scheduling a broadcast**

   * Use `/schedule_slack_broadcast` to schedule a message.
   * Select the accounts, write the message, and specify the date and time in UTC.
   * Submit after verifying the details.
5. **Periodic broadcasting**

   * Use `/periodic_slack_broadcast` for recurring messages.
   * Select accounts, write the message, and specify the day and hour.
   * Submit after verifying the details.

## Inputs

* **Internal channels**: Slack channels for internal messages, populated using slash commands.
* **Access groups**: Define who is allowed to send broadcasts.
* **Tag**: Added when account is linked to Slack channel.

## CSV Format

When uploading a CSV to link accounts or channels:

* **External channels**:

  + Column 1: Account display name
  + Column 2: Slack channel ID
* **Internal channels**:

  + Column 1: Channel name
  + Column 2: Slack channel ID

Currently, this snap-in does not support broadcasting to more than 650 channels at a time.

## Source
- DevRev support [[entities/article|article]] [Slack Broadcaster](https://support.devrev.ai/en-US/devrev/article/aE1x22U7) (ART-21967)
