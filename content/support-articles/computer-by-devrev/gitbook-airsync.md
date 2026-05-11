---
title: GitBook AirSync
devrev_id: ART-22018
parent_directory: AirSync
translation_group: vUAojt_p
modified_date: "2026-01-05T05:37:31.483Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/vUAojt_p"
tags: []
top_category: Computer by DevRev
wiki_match: glossary/airsync
match_score: 0.85
last_updated: 2026-05-11
related: ['glossary/airsync']
summary: "Seamlessly import your articles from GitBook to DevRev."
---

# GitBook AirSync

Seamlessly import your [[entities/article|articles]] from GitBook to DevRev.

## Supported objects

The following is a list of GitBook objects and their corresponding DevRev
equivalent. Those marked as **Supported** are eligible for import.

| GitBook object | DevRev object | Sync to DevRev |
| --- | --- | --- |
| Collection | [[entities/article|Article]] collection | ✅ |
| Space | Article collection | ✅ |
| Page | Article | ✅ |
| User [[entities/group|group]] | Group | ❌ |
| Attachment | Attachment | ❌ |

## Import from GitBook

Follow the steps below to import from GitBook:

1. In **Marketplace**, [[features/search|search]] for **GitBook** and install the snap-in.
2. In the snap-in config modal, click **Install** then go to **Integrations** >
   **AirSyncs** in your settings left nav.
3. Click the **[[glossary/airsync|AirSync]]** button and select the GitBook tile in the **Start
   import** window.
4. Create a new connection to your GitBook [[entities/account|account]], or use an existing.
   connection if you already have one.While creating the connection, you are required to input a **Subdomain**
   field. This is a mandatory unique identifier used by AirSync to group
   together AirSyncs from the same source system.It is recommended to use the name of the GitBook workspace you want to import
   as the value of **Subdomain**.
5. Once the connection is established, select the GitBook workspace you want to
   import, and specify the DevRev [[entities/part|part]] that should be used for any imported work.
   This initiates a bulk import of the selected site.
6. Click **Map fields** in the import row and configure filters, object mapping,
   or field mapping as necessary.While DevRev attempts to automatically map fields, you may be prompted to
   manually map indicated fields.

The duration of the import depends on the size of the GitBook workspace and the
amount of data being imported. For a workspace with only a few dozen items, it
can take seconds, while a workspace with tens of thousands of items may take a
few hours. DevRev respects GitBook API rate limits and automatically handles
back-off and resume.

##

## Related wiki nodes
- [[glossary/airsync]]

## Source
- DevRev support article [GitBook AirSync](https://support.devrev.ai/en-US/devrev/article/vUAojt_p) (ART-22018)
