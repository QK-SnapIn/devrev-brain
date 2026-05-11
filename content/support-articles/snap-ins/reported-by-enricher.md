---
title: Reported by enricher
devrev_id: ART-21968
parent_directory: Automate
translation_group: GKhQcRGb
modified_date: "2026-01-02T22:59:05.547Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/GKhQcRGb"
tags: []
top_category: Snap-ins
wiki_match: features/remote-mcp
match_score: 0.486
last_updated: 2026-05-11
---

# Reported by enricher

The [Reported by Enricher](https://marketplace.devrev.ai/ticket-reported-by) snap-in automatically updates the **Reported By** field on tickets created with an email entered in a custom field. It verifies if the email belongs to an existing customer of the configured account and either links to that customer or creates a new one.

## Installation

Install the [Reported by Enricher](https://marketplace.devrev.ai/ticket-reported-by) from DevRev marketplace.

## Configuration

In the **Configuration** tab, the following settings are available:

* **Custom Email Field**: Specify the backend name of the custom field where the email is entered when creating a ticket.
* **Default Account**: Select the account to which new customers should be linked if they do not already exist in the system.

After configuring these settings, the snap-in automatically processes new tickets and enriches their **Reported By** fields based on the provided email addresses.

## Source
- DevRev support article [Reported by enricher](https://support.devrev.ai/en-US/devrev/article/GKhQcRGb) (ART-21968)
