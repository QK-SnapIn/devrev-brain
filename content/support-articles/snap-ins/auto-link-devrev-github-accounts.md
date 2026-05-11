---
title: Auto-link DevRev GitHub accounts
devrev_id: ART-21923
parent_directory: Automate
translation_group: lU6Qkrc-
modified_date: "2026-03-26T04:12:55.699Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/lU6Qkrc-"
tags: []
top_category: Snap-ins
wiki_match: entities/account
match_score: 0.85
last_updated: 2026-05-11
related: ['entities/account']
summary: "The Auto-link DevRev GitHub accounts snap-in links GitHub accounts to corresponding DevRev accounts at scale."
---

# Auto-link DevRev GitHub accounts

The [Auto-link DevRev GitHub accounts](https://marketplace.devrev.ai/auto-link-github-accounts) snap-in links GitHub [[features/accounts|accounts]] to corresponding DevRev accounts at scale. The snap-in supports automatic creation of shadow users for inactive DevRev accounts and handles the conversion to active users upon their first login.

## Features

* The system reads a CSV file containing user data.
* For each user, it checks if a DevRev [[entities/account|account]] exists using the provided email (`saml_name_id`).
* If the user exists and is active, the GitHub account is linked directly.
* If the user does not exist or is inactive, a [[glossary/shadow-user|shadow user]] is created and the GitHub account is linked.
* Shadow users automatically convert to active users upon their first login.
* If the user does not exist or is inactive, a shadow user is created and the GitHub account is linked.
* Shadow users automatically convert to active users upon their first login.

## Installation

### Prerequisites

* Obtain the necessary CSV file containing user details.

### Input requirements

The input CSV file should include the following columns. These are case-sensitive, but the order in which they appear is flexible:

|  |  |  |
| --- | --- | --- |
| Column name | Type | Description |
| login | string | GitHub account identifier |
| saml\_name\_id | string | DevRev account email identifier |

### Steps to Install and Configure

1. Download the latest version of the snap-in from the DevRev marketplace.
2. Upload the CSV file containing user details.
3. Run the snap-in to process the file and link accounts.
4. Verify the linked accounts in DevRev.

### How to use the snap-in

1. Use slash [[features/commands|commands]] in the **Events** section.
2. In the **Discussion** tab, type the slash commands.
3. Run the snap-in using the `/link_github_accounts_to_devrev` command in the snap-in discussion thread.
4. The columns `login` and `saml_name_id` can be in any order.

## Related wiki nodes
- [[entities/account]]

## Source
- DevRev support [[entities/article|article]] [Auto-link DevRev GitHub accounts](https://support.devrev.ai/en-US/devrev/article/lU6Qkrc-) (ART-21923)
