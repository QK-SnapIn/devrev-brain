---
title: DevRev AirSync
devrev_id: ART-22019
parent_directory: AirSync
translation_group: pDAoQ_sS
modified_date: "2026-01-12T13:18:27.655Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/pDAoQ_sS"
tags: []
top_category: Computer by DevRev
wiki_match: glossary/airsync
match_score: 0.85
last_updated: 2026-05-11
related: ['glossary/airsync']
summary: "The DevRev AirSync simplifies migration of objects from one DevRev workspace into another one, supporting both one-time imports and ongoing syncs."
---

# DevRev AirSync

The DevRev [[glossary/airsync|AirSync]] simplifies migration of objects from one DevRev workspace into another one, supporting both one-time imports and ongoing syncs.

## Supported objects

The following is a list of DevRev objects that the user might expect to be successfully imported from the target organization. Those marked as **Supported** are eligible for import.

| DevRev Object | Sync to DevRev |
| --- | --- |
| [[entities/issue|Issue]] | ✅ |
| [[entities/ticket|Ticket]] | ✅ |
| DevUser | ✅ |
| Customer | ✅ |
| Tag | ✅ |
| Product | ✅ |
| Capability | ✅ |
| [[entities/enhancement|Enhancement]] | ✅ |
| Feature | ✅ |
| Runnable | ✅ |
| Links on works | ✅ |
| Timeline Comment | ✅ |
| [[entities/account|Account]] | ✅ |
| Custom [[entities/group|Group]] | ✅ |
| [[entities/article|Articles]] | ✅ |
| [[entities/opportunity|Opportunities]] | ✅ |
| [[entities/task|Tasks]] | ❌ |
| Attachments | ❌ |

## Importing from DevRev

Follow the steps below to import from DevRev:

1. In the Marketplace, [[features/search|search]] for **DevRev ADaaS** under the **Import** category and install.
2. In the snap-in config modal toggle all the object types that are intended to
   be extracted, then save and click on **Install**, then go to the **Import**
   section on your settings left nav.
3. Click **+Import** to start an import, then select the **DevRev ADaaS** option.
4. Create a new connection to your external workspace from which data is
   pulled, or use an existing connection if you already have one. A personal
   access token which has access to that particular org is required.
5. Once the connection is established, select the workspace you want to import and
   specify the DevRev [[entities/part|part]] that should be used for any imported work. This
   initiates a bulk import of the selected site.
6. A pre-defined mapping is provided for all object types to ease on the user's
   required interaction and have them set beforehand. However, you may be
   prompted to manually map certain fields if needed.

The duration of the import depends on the size of the workspace and the data being imported. It can take seconds for an account with only a few dozen [[features/tickets|tickets]] to a few hours for an account with tens of thousands of items with many attachments.

It is recommended to only extract the necessary objects to avoid these long running imports, although it is up to the users' needs.

## Related wiki nodes
- [[glossary/airsync]]

## Source
- DevRev support [[entities/article|article]] [DevRev AirSync](https://support.devrev.ai/en-US/devrev/article/pDAoQ_sS) (ART-22019)
