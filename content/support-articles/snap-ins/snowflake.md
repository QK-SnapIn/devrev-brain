---
title: Snowflake
devrev_id: ART-21991
parent_directory: Integrate
translation_group: M69kzanW
modified_date: "2025-12-10T06:57:47.693Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/M69kzanW"
tags: []
top_category: Snap-ins
wiki_match: features/knowledge-base
match_score: 0.522
last_updated: 2026-05-11
---

# Snowflake

The [Snowflake](https://devrev.ai/marketplace/snowflake) allows you to import account, contact data, and opportunity data from Snowflake to DevRev.

## Installation

1. In DevRev, go to **Settings** > **Snap-ins** and click **Explore Marketplace** in the top-right corner.
2. In the DevRev marketplace, find **Snowflake** and click **Install**.
3. Set-up the snap-in's configurations.
4. Fill in the following fields:

   * **Username**: Your Snowflake account username
   * **Password**: Your Snowflake account password
   * **Account**: Your Snowflake account identifier
   * **Database**: Name of the Snowflake database to import data
   * **Schema**: Schema in Snowflake containing your data
   * **Account Table**: Table for account data
   * **Contact Table**: Table for contact data
   * **Opportunity Table**: Table for opportunity data
   * **Sync Contacts**: Set to `true` if you want to import contacts.
   * Set Sync Opportunities to `true` if you want to import opportunities.
5. Click **Save**.
6. Execute the `/initialize_mapping` command in the snap-in **Discussions** tab. This step ensures that custom fields from Snowflake map correctly to the DevRev schema.
7. Once the mapping step is completed then every day at **12 UTC** the snap-in would start importing the accounts, contacts and opportunities object from Snowflake to DevRev.
8. One can also manually turn on the import by executing the `/initialize_snowflake_import` command in the snap-in **Discussions** tab.

## Source
- DevRev support article [Snowflake](https://support.devrev.ai/en-US/devrev/article/M69kzanW) (ART-21991)
