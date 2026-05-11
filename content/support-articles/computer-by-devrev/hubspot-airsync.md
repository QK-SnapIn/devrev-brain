---
title: HubSpot AirSync
devrev_id: ART-21995
parent_directory: AirSync
translation_group: 78b5Fv0r
modified_date: "2026-04-12T18:28:59.743Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/78b5Fv0r"
tags: []
top_category: Computer by DevRev
wiki_match: glossary/airsync
match_score: 0.85
last_updated: 2026-05-11
related: ['glossary/airsync']
---

# HubSpot AirSync

DevRev's HubSpot AirSync allows you to seamlessly import your HubSpot companies
and contacts into DevRev.

For more information, refer to the [HubSpot AirSync snap-in](https://marketplace.devrev.ai/hubspot) on the DevRev marketplace.

## Supported objects

The following is a list of HubSpot objects and their corresponding DevRev
equivalent. Those marked as **Supported** are eligible for import.

| HubSpot Object | DevRev Object | Sync to DevRev |
| --- | --- | --- |
| Contact | Contact | ✅ |
| Company | Account | ✅ |
| Deal | Opportunity | ✅ |
| Pipeline of Deal | State/Stage of Opportunity | ✅ |
| Note on Deal | Comment on Opportunity | ✅ |
| Attachment on Note | Attachment on Comment | ✅ |
| User | DevUser | ✅ |
| Ticket | Ticket | ❌ |
| Product | Part | ❌ |
| Timeline | Timeline | ❌ |
| Conversation | Conversation | ❌ |
| Custom Object | Custom Object | ❌ |

## Import from HubSpot

Follow the steps below to import from HubSpot:

For best results, AirSyncs should be done using an administrator account on the external source. This ensures all necessary permissions are available to complete the import successfully.

1. Go to **[Settings](https://app.devrev.ai/?setting=airsyncs)**[ > ](https://app.devrev.ai/?setting=airsyncs)**[Integrations](https://app.devrev.ai/?setting=airsyncs)**[ > ](https://app.devrev.ai/?setting=airsyncs)**[AirSyncs](https://app.devrev.ai/?setting=airsyncs)** and select **AirSync** (or **Start AirSync** if it's your first).
2. Create a new connection to your HubSpot account, or use an existing
   connection if you already have one.
3. Once the connection is established, select the HubSpot site you want to
   import and specify the DevRev part that should be used for any imported work
   (future releases makes use of this). This initiates a bulk import of the
   selected site.
4. Review the automatically mapped fields and manually map any remaining fields if prompted.
   corresponding fields in DevRev. However, you may be prompted to manually map
   certain fields if needed.

The duration of the import depends on the size of the HubSpot account and the
data being imported. It can take seconds for an account with only a few dozen
companies and contacts to a few hours for an account with tens of thousands of
items with many attachments. DevRev honors the HubSpot API rate limits and
back-off and resume automatically.

##

## Related wiki nodes
- [[glossary/airsync]]

## Source
- DevRev support article [HubSpot AirSync](https://support.devrev.ai/en-US/devrev/article/78b5Fv0r) (ART-21995)
