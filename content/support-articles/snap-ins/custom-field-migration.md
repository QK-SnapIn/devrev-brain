---
title: Custom field migration
devrev_id: ART-21965
parent_directory: Automate
translation_group: Oj8u-g0z
modified_date: "2026-02-18T05:45:59.79Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/Oj8u-g0z"
tags: []
top_category: Snap-ins
wiki_match: features/customization
match_score: 0.686
last_updated: 2026-05-11
---

# Custom field migration

The Custom field migration snap-in is designed to facilitate the seamless migration of custom field values across various DevRev objects, including accounts, issues, tickets, opportunities, incidents, and contacts. It efficiently processes data in batches, transferring values from a specified source field to a target field while managing state through cursors for reliable execution.

## Installation

1. Open the DevRev marketplace and install the **Custom Field Migration** snap-in.
2. Select the workspace where you want to install the snap-in, confirm your selection, and click **Deploy snap-in**.

## Configuration

1. Go to **Snap-ins** > **Custom Field Migration** > **Configure**.
2. Fill the configuration for the object and fields.

   If you enable the **Unset source field** option, the values in the source field are permanently deleted after being transferred to the target field.
3. Click **Save** and **Install**.
4. Enter `/start_custom_field_migration` in the `Discussion` section of snap-in to automatically migrate a value from the source field to the respective target field.

   If a value already exists in the target field, it is overwritten with the new value from the source field.

Once the migration starts, you will receive a message in the snap-in **Discussion** section notifying you of its initiation. The progress is updated after every 75 updates. When the migration is completed, you will receive another message in the snap-in **Discussion** section. If there are any failed items, you can re-enter the command to update them.

## Source
- DevRev support article [Custom field migration](https://support.devrev.ai/en-US/devrev/article/Oj8u-g0z) (ART-21965)
