---
title: Ticket tagger
devrev_id: ART-21960
parent_directory: Automate
translation_group: TKQV--P6
modified_date: "2026-01-26T17:03:06.193Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/TKQV--P6"
tags: []
top_category: Snap-ins
wiki_match: entities/ticket
match_score: 0.85
last_updated: 2026-05-11
related: ['entities/ticket']
summary: "The Ticket Tagger is an automation tool designed to streamline ticket management."
---

# Ticket tagger

The **[[entities/ticket|Ticket]] Tagger** is an automation tool designed to streamline ticket
management. It automatically assigns appropriate tags to [[features/tickets|tickets]] based on the
tags of the contact or their [[entities/account|account]].

## Key features

* Automatically tags tickets created by specific users (customer users).
* Ignores tickets created by other user types.
* Allows multiple tags to be assigned based on predefined rules.
* Can be triggered via [[features/commands|commands]] or automatically when tickets are created.

## Configuration

Follow these steps to set up the Ticket Tagger:

1. Go to **Snap-ins** > **Ticket Tagger** > **Configure**.
2. Fill in the configuration settings.

   * **[[features/search|Search]] for Tags**: Select the tags to check for on the contact or
     account. If multiple tags are selected, only one needs to match.
   * **Search for tags on**: Specify where to search for tags—on the contact,
     the account, or both.
   * **Assign tags if found**: Choose the tags to add to the ticket if matching
     tags are found.
   * (Optional) **Assign tags if not found**: Choose tags to add if no matching
     tags are found.
3. Click **Save**.
4. Click **Install** to activate the snap-in.

## How to use

Once the snap-in is installed, it automatically checks all newly created tickets
and assigns tags based on the configuration.

### Triggering tag checks for existing tickets

To apply tags to tickets that were created before the snap-in was installed:

1. Go to the **Events/Discussions** section in the snap-in.
2. Enter the command: `/tag_existing_tickets`.
3. Allow time for the process to complete—this may vary depending on the number
   of existing tickets.

## Related wiki nodes
- [[entities/ticket]]

## Source
- DevRev support [[entities/article|article]] [Ticket tagger](https://support.devrev.ai/en-US/devrev/article/TKQV--P6) (ART-21960)
