---
title: Paligo AirSync
devrev_id: ART-22021
parent_directory: AirSync
translation_group: lREOYzMO
modified_date: "2026-01-05T05:34:54.705Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/lREOYzMO"
tags: []
top_category: Computer by DevRev
wiki_match: glossary/airsync
match_score: 0.85
last_updated: 2026-05-11
related: ['glossary/airsync']
---

# Paligo AirSync

Seamlessly import your articles from Paligo to DevRev.

## Supported objects

The following is a list of Paligo objects and their corresponding DevRev
equivalent. Those marked as **Supported** are eligible for import.

| Paligo object | DevRev object | Sync to DevRev |
| --- | --- | --- |
| Folder | Article collection | ✅ |
| Document | Article | ✅ |
| User group | Group | ❌ |

## Import from Paligo

Follow the steps below to import from Paligo:

1. In **Marketplace**, search for Paligo under the **Import** category and
   select the option for the **Paligo**.
2. In the snap-in config modal, click **Install** then go to **Integrations** >
   **Imports** in your settings left nav.
3. Click the **Import** button and select the Paligo tile in the **Start
   import** window.
4. Create a new connection to your Paligo account, or use an existing.
   connection if you already have one.While creating the connection, you are required to input a **Subdomain**
   field. This is a mandatory unique identifier used by AirSync to group
   together imports from the same source system.It is recommended to use the **Instance** of the Paligo workspace you want to import
   as the value of **Subdomain**.
5. Once the connection is established, select the Paligo publication you want to
   import, and specify the DevRev part that should be used for any imported work.
   This initiates a bulk import of the selected site.
6. Click **Map fields** in the import row and configure filters, object mapping,
   or field mapping as necessary.While DevRev attempts to automatically map fields, you may be prompted to
   manually map indicated fields.

The duration of the import depends on the size of the Paligo workspace and the
amount of data being imported. For a workspace with only a few dozen items, it
can take seconds, while a workspace with tens of thousands of items may take a
few hours.

## Related wiki nodes
- [[glossary/airsync]]

## Source
- DevRev support article [Paligo AirSync](https://support.devrev.ai/en-US/devrev/article/lREOYzMO) (ART-22021)
