---
title: Ticket linked issues comment sync
devrev_id: ART-21970
parent_directory: Automate
translation_group: rS-fxXX9
modified_date: "2025-12-10T06:57:34.968Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/rS-fxXX9"
tags: []
top_category: Snap-ins
wiki_match: entities/ticket
match_score: 0.85
last_updated: 2026-05-11
related: ['entities/ticket']
---

# Ticket linked issues comment sync

The **Ticket Linked Issues Comment Sync** snap-in automatically synchronizes comments between linked tickets and issues in DevRev. When a comment is added to a ticket, it is automatically replicated to all linked issues, maintaining context and ensuring all stakeholders have access to the same information.

## Key features

* **Comment synchronization**: Comments from tickets are automatically replicated to linked issues with preserved context.
* **Context preservation**: Each synchronized comment includes information about the original author and source ticket.
* **Reduced clutter**: Maintains separate parent comment threads for internal discussions and customer messages.
* **Attachment support**: File attachments in comments are preserved during synchronization.
* **Automatic schema management**: Creates necessary custom fields for tracking comment relationships.

## Installation and configuration

### Prerequisites

* DevRev organization with appropriate permissions.
* Linked tickets and issues that need comment synchronization.
* User's DevRev PAT configured as keyrings under the snap-in services category in the connections page.

### Setup steps

1. Install the **Ticket Linked Issues Comment Sync** snap-in from the DevRev marketplace.
2. Configure your DevRev PAT in the keyrings section under snap-in services in the connections page.
3. The snap-in creates necessary custom fields for tracking comment relationships.

* Comments synchronize only between directly linked items.
* Editing a comment after synchronization does not update the synchronized copies.
* Ticket threads are not fully supported yet. DevRev supports only one level of nesting; threaded comments in tickets are supported as flat items.

## Related wiki nodes
- [[entities/ticket]]

## Source
- DevRev support article [Ticket linked issues comment sync](https://support.devrev.ai/en-US/devrev/article/rS-fxXX9) (ART-21970)
