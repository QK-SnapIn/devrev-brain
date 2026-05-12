---
title: ServiceDesk+ AirSync
devrev_id: ART-34620
parent_directory: AirSync
translation_group: mhCzdLve
modified_date: "2026-04-30T21:33:58.989Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/mhCzdLve"
tags: []
top_category: Computer by DevRev
wiki_match: glossary/airsync
match_score: 0.85
last_updated: 2026-05-11
related: ['glossary/airsync']
summary: "Seamlessly import your knowledge base, tickets, and users from ManageEngine ServiceDesk Plus to DevRev."
---

# ServiceDesk+ AirSync

Seamlessly import your [[features/knowledge-base|knowledge base]], [[features/tickets|tickets]], and users from ManageEngine ServiceDesk Plus to DevRev.

## Supported objects

The following is a list of ServiceDesk Plus objects and their corresponding DevRev equivalent. Those marked as Supported are eligible for import.

| ServiceDesk Plus object | DevRev object | Sync to DevRev |
| --- | --- | --- |
| Solution (KB [[entities/article|article]]) | Article | ✅ |
| Topic (KB category) | Directory | ✅ |
| Technician | [[entities/dev-user|Dev user]] | ✅ |
| Attachment | Attachment | ✅ |
| Request | [[entities/ticket|Ticket]] | ✅ |
| User [[entities/group|group]] | Group | ✅ |

## Import from ServiceDesk Plus

Follow the steps below to import from ServiceDesk Plus:

1. In Marketplace, [[features/search|search]] for **ManageEngine ServiceDesk Plus** and install the snap-in.
2. In the snap-in config modal, click **Install**, then go to **Integrations > AirSyncs** in your settings left nav.
3. Click the **[[glossary/airsync|AirSync]]** button and select the ManageEngine ServiceDesk Plus tile in the Start import window.
4. Create a new connection to your ServiceDesk Plus [[entities/account|account]], or use an existing connection if you already have one.
5. While creating the connection, you are required to input the following fields:

   * **API Token** — Zoho OAuth access token with `SDPOnDemand.solutions.ALL` and `SDPOnDemand.general.READ` scopes.
   * **Subdomain** — Full SDP domain for your data center (e.g. `sdpondemand.manageengine.com` for US, `sdpondemand.manageengine.in` for India). This is also used by AirSync as the unique identifier for grouping AirSyncs from the same source system.
   * **Portal Name** — SDP Cloud portal name, found in your SDP URL as `.../app/{portal}/`.
6. Once the connection is established, select the ServiceDesk Plus portal you want to import, and specify the DevRev [[entities/part|part]] that should be used for any imported work. This initiates a bulk import of the selected portal.
7. Click **Map fields** in the import row and configure filters, object mapping, or field mapping as necessary. While DevRev attempts to automatically map fields, you may be prompted to manually map indicated fields. Custom (UDF) fields on Solutions are discovered automatically and surfaced as `cf_udf_*` fields.

The duration of the import depends on the size of the ServiceDesk Plus portal and the amount of data being imported. For a portal with only a few dozen [[entities/article|articles]], it can take seconds, while a portal with tens of thousands of articles may take a few hours. DevRev respects ServiceDesk Plus API rate limits and automatically handles back-off and resume.

## Related wiki nodes
- [[glossary/airsync]]

## Source
- DevRev support article [ServiceDesk+ AirSync](https://support.devrev.ai/en-US/devrev/article/mhCzdLve) (ART-34620)
