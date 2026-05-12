---
title: Ticket issue field migrator
devrev_id: ART-21956
parent_directory: Automate
translation_group: BtqQCE8C
modified_date: "2025-12-10T06:57:26.071Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/BtqQCE8C"
tags: []
top_category: Snap-ins
wiki_match: entities/ticket
match_score: 0.85
last_updated: 2026-05-11
related: ['entities/ticket']
summary: "The Ticket issue field migration snap-in automates the transfer of custom field values from tickets to new linked issues in DevRev."
---

# Ticket issue field migrator

The [[entities/ticket|Ticket]] [[entities/issue|issue]] field migration snap-in automates the transfer of custom field values from [[features/tickets|tickets]] to new linked [[features/issues|issues]] in DevRev. It checks for empty or undefined fields and fills them with corresponding ticket values based on the field mappings specified in the configuration input. The process features robust error handling, detailed logging, and appends a summary comment to the timeline for easy update tracking.

## Installation

1. Install the **Ticket Issue Field Migrator** snap-in from the DevRev marketplace.
2. Select the workspace where you want to install the snap-in, confirm your selection, and click **Deploy snap-in**.

## Configuration

1. In DevRev, go to **Settings** > **Snap-ins** > **Ticket Issue Field Migrator** > **Configure**.
2. Specify the **Field Names** to migrate values from the ticket to the issue when fields are empty or undefined.
3. Click **Save** and **Install** to complete the setup.
4. Link an issue to a ticket to begin the migration of values from the ticket fields to the issue fields.
5. After the migration process is complete, you will receive a summary message in the snap-in **Discussion** tab, informing you of the number of fields processed, updated, and not updated. If the fields specified in the configuration are not found, a notification will be provided in the **Discussion** tab.

## Related wiki nodes
- [[entities/ticket]]

## Source
- DevRev support [[entities/article|article]] [Ticket issue field migrator](https://support.devrev.ai/en-US/devrev/article/BtqQCE8C) (ART-21956)
