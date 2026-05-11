---
title: Search Node
devrev_id: ART-21943
parent_directory: Automate
translation_group: Nu9tvhiJ
modified_date: "2025-12-10T06:57:17.84Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/Nu9tvhiJ"
tags: []
top_category: Snap-ins
wiki_match: features/search
match_score: 0.85
last_updated: 2026-05-11
related: ['features/search']
---

# Search Node

The [Search Node](https://marketplace.devrev.ai/search-node) snap-in includes the custom operation Get Relevant Objects, which is available in the Workflow Builder upon activation. This automation gets the list of relevant objects for the given search query.

## Installation

1. In DevRev, go to **Settings** > **Snap-ins** and click **All Snap-ins**.
2. Search for **Search Node** and click **Configure**.
3. Confirm the installation.

## Input Parameters

1. **Account ID**:

   * Description: Filters and retrieves tickets or conversations associated with a specific user account.
   * Requirement: Required only when the Namespace is `ticket`/`conversation`.
2. **Search Query**:

   * Description: A search term or phrase used to locate relevant objects within the system.
   * Requirement: Mandatory.
3. **Namespace**:

   * Description: Defines the category under which the search should be conducted.
   * Requirement: Mandatory.
   * Allowed Values: `ticket`, `dev-user`, `conversation`, `part`.

## Output Parameters

1. **List of Relevant Object IDs**:

   * Returns a list of IDs corresponding to objects that meet the provided search criteria.

## Related wiki nodes
- [[features/search]]

## Source
- DevRev support article [Search Node](https://support.devrev.ai/en-US/devrev/article/Nu9tvhiJ) (ART-21943)
