---
title: Account deduplication
devrev_id: ART-21921
parent_directory: Automate
translation_group: WY9H5fw_
modified_date: "2025-12-10T06:57:03.413Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/WY9H5fw_"
tags: []
top_category: Snap-ins
wiki_match: entities/account
match_score: 0.85
last_updated: 2026-05-11
related: ['entities/account']
---

# Account deduplication

The Account Deduplication snap-in streamlines account management by merging duplicates imported from various external sources. It consolidates the primary account, which remains synced with the external source, and the secondary account, which ceases syncing.

For more information, refer to the [Account Deduplication snap-in](https://marketplace.devrev.ai/account-deduplication) on the DevRev marketplace.

## Installation

1. Open the DevRev marketplace and install the **Account Deduplication** snap-in.
2. Select the workspace where you want to install the snap-in, confirm your selection, and click **Deploy snap-in**.

## Configure

1. Go to **Snap-ins** > **Account Deduplication** > **Configure**.
2. Fill the configuration with the primary and secondary external sources, the primary and secondary import tags, and the account type for entries that include **Source ID:XXXXX** in their display name.

   If both the primary and secondary accounts have the source ID appended to their display names, run the script twice. First, set the type to 'primary' in the configuration, add tags, and merge accounts. Then, run the script again, set the type to 'secondary' in the configuration, add tags, and merge the accounts.

   Providing incorrect information in the configuration may lead to the merging of incorrect accounts, an irreversible action. The primary account continues syncing after the merge, while the secondary account no longer syncs with the external source. Field updates to the secondary account are ignored. When accounts are merged, the values of single-value stock fields from the secondary account, as well as any **common** custom field values of the secondary account, are lost.
3. Click **Save** and **Install**.

## Deduplicate accounts

1. Enter `/add_tags` in the `Discussion` section of snap-in to start adding tags
   to primary and secondary account.

   If the timeline entry remains unchanged for an extended period, use `/add_tags stop` to change the status from "running" to "stop". To reset the script completely, use `/add_tags reset`, which removes the checkpoints that allow the script to continue from a specific point. After adding the tags, you can verify by filtering Vista using the **duplicate-account** and **original-account** tags. You can remove a tag from an account to prevent the merging of specific accounts. If there are multiple duplicates, merge them manually. The link to the account is available in the timeline entry under **Discussions**.
2. Verify the duplicate accounts.
3. Enter `/merge_duplicates` to merge secondary account into primary account.

   If the timeline entry remains unchanged for an extended period, use `/merge_duplicates stop` to change the status from "running" to "stop".

## Related wiki nodes
- [[entities/account]]

## Source
- DevRev support article [Account deduplication](https://support.devrev.ai/en-US/devrev/article/WY9H5fw_) (ART-21921)
