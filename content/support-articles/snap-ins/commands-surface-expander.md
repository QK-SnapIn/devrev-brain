---
title: Commands surface expander
devrev_id: ART-21930
parent_directory: Automate
translation_group: VOY3CHs0
modified_date: "2025-12-10T06:57:09.367Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/VOY3CHs0"
tags: []
top_category: Snap-ins
wiki_match: features/commands
match_score: 0.85
last_updated: 2026-05-11
related: ['features/commands']
summary: "The Commands surface expander snap-in is an automation tool designed to expand commands availability across DevRev surfaces."
---

# Commands surface expander

The **[[features/commands|Commands]] surface expander** snap-in is an automation tool designed to
expand commands availability across DevRev surfaces.

## Configuration

Follow these steps to set up the Commands Surface Expander:

1. Go to **Snap-ins** > **Commands Surface Expander** > **Configure**.
2. Fill in the configuration settings.

   * **Command Names**: List command names that exist in the organization. Enter
     one per text box (to add more text boxes, click '**+**').
   * **Customer Chat Surfaces**: Select surfaces where the commands should be
     available in the "Customer messages".
   * **Discussions Surfaces**: Select surfaces where the commands should be
     available in internal [[features/chats|chats]].
3. Click **Save**.
4. Click **Install** to activate the snap-in.

## Trigger commands surface expansion

To update commands surfaces:

1. Go to the **Events/Discussions** section in the snap-in.
2. Enter the command: `/expand_commands_surfaces`.
3. Allow time for the process to complete—this may vary depending on the number
   of commands listed.

## Related wiki nodes
- [[features/commands]]

## Source
- DevRev support [[entities/article|article]] [Commands surface expander](https://support.devrev.ai/en-US/devrev/article/VOY3CHs0) (ART-21930)
