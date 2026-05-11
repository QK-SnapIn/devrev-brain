---
title: Ticket immutability
devrev_id: ART-21957
parent_directory: Automate
translation_group: 8qJ46S4f
modified_date: "2026-05-06T02:54:35.382Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/8qJ46S4f"
tags: []
top_category: Snap-ins
wiki_match: entities/ticket
match_score: 0.85
last_updated: 2026-05-11
related: ['entities/ticket']
---

# Ticket immutability

The [Ticket Immutability](https://devrev.ai/marketplace/followup) snap-in enables automatic enforcement of immutability on closed tickets. Organizations use this snap-in to maintain compliance with data governance policies, prevent accidental edits on resolved tickets, and preserve audit integrity. Once activated, tickets are marked as immutable after a defined number of days in a closed state, excluding those in the *Accepted* stage. After this period, no further modifications are permitted. This includes restrictions on rich-text editor access, field updates, object linking, and other changes, ensuring ticket integrity.

This snap-in requires workspace admin privileges to install and configure.

## Behavior

**Immutability enforcement**

When a ticket has remained in a closed state (other than *Accepted*) for the configured number of days, the snap-in marks it as immutable. Once immutable, agents and customers cannot modify any fields, link objects, or edit the ticket's content.

> 📝 **Note**: To apply immutability to tickets, this snap-in runs about once per hour. On each run it can mark up to 50 tickets immutable. If there are a lot of tickets that meet the criteria for immutability, it can take multiple cycles to mark them all.

**Follow-up ticket creation**

When a customer responds to an immutable ticket, the snap-in automatically creates a follow-up ticket. This ensures that customer inquiries are never lost while preserving the integrity of the original closed ticket. For more details, see [Follow-up Ticket](https://support.devrev.ai/devrev/article/ART-2012).

**Automatic archiving**

Tickets are automatically archived 180 days after becoming immutable.

**AirSync ticket exemption**

Tickets imported through AirSync are exempt from being set as immutable. This prevents conflicts with synchronization workflows that may need to update ticket data after import.

## Installation

1. In DevRev, go to **Settings > Snap-ins** and click **Explore Marketplace** in the top-right corner.
2. In the DevRev Marketplace, find **Ticket Immutability** and click **Install**.
3. Configure the immutability period in the configuration settings (see below).
4. Click **Save**, then click **Install** to activate the snap-in.

## Configuration

In the **Configuration Settings**, specify the number of days (1–365) after which a closed ticket becomes immutable. The default value is 365 days. A ticket must remain in a closed state (excluding *Accepted*) for this entire period before immutability is enforced.

## Related wiki nodes
- [[entities/ticket]]

## Source
- DevRev support article [Ticket immutability](https://support.devrev.ai/en-US/devrev/article/8qJ46S4f) (ART-21957)
