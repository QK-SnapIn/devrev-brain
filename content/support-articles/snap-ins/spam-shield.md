---
title: Spam Shield
devrev_id: ART-21953
parent_directory: Automate
translation_group: LAK75G01
modified_date: "2025-12-11T08:05:52.116Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/LAK75G01"
tags: []
top_category: Snap-ins
wiki_match: entities/issue
match_score: 0.375
last_updated: 2026-05-11
summary: "The Spam Shield snap-in checks for spam from users."
---

# Spam Shield

The Spam Shield snap-in checks for spam from users. This snap-in marks or suggests [[features/conversations-feature|conversations]], [[features/tickets|tickets]], and contacts as spam. It analyzes the first customer message and determines whether a [[entities/ticket|ticket]] or [[entities/conversation|conversation]] is spam. It uses advanced algorithms to identify patterns indicative of spam content, ensuring that customer support teams can focus their efforts on genuine customer interactions.

For more information, refer to the [Spam Shield snap-in](https://marketplace.devrev.ai/spam-snap) on the DevRev marketplace.

## Installation

1. In DevRev, go to **Settings** > **Snap-ins** and click **Explore Marketplace** in the top-right corner.
2. In the DevRev marketplace, find **Spam Shield** and click **Install**.

## Configuration

In **Snap-ins** > **Spam Shield** > **Configure**, the following configuration options are available:

* **Objects for spam detection:** Choose the DevRev objects (tickets, conversations) that the spam detection algorithm should work on.
* **Primary action:** Choose the action to be performed when spam is detected.
* **Check for spam from verified users (DevRev app users and customers added as Contacts)**: If enabled, the spam detection algorithm will also consider the tickets and conversations created by DevRev app users and customer Contacts on DevRev as inputs.

Click **Install snap-in** to deploy the snap-in.

![spam shield](don:core:dvrv-us-1:devo/0:artifact/4100749)

## Source
- DevRev support [[entities/article|article]] [Spam Shield](https://support.devrev.ai/en-US/devrev/article/LAK75G01) (ART-21953)
