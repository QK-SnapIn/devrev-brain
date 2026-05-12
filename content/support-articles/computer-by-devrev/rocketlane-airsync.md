---
title: Rocketlane AirSync
devrev_id: ART-22000
parent_directory: AirSync
translation_group: 7OPmGfqK
modified_date: "2026-01-05T06:20:58.442Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/7OPmGfqK"
tags: []
top_category: Computer by DevRev
wiki_match: glossary/airsync
match_score: 0.85
last_updated: 2026-05-11
related: ['glossary/airsync']
summary: "DevRev\"s Rocketlane AirSync allows you to perform a sync from Rocketlane to DevRev."
---

# Rocketlane AirSync

DevRev's Rocketlane [[glossary/airsync|AirSync]] allows you to perform a sync from Rocketlane to DevRev. The snap-in extracts the data needed from Rocketlane projects to create DevRev [[features/accounts|accounts]].

## Supported objects

The following is the Rocketlane object and its DevRev equivalent.

| Rocketlane Object | DevRev | Sync to DevRev |
| --- | --- | --- |
| Organization | [[entities/account|Account]] | ✅ |

## Importing from Rocketlane

Follow the steps below to import from Rocketlane:

For best results, AirSyncs should be done using an administrator account on the external source. This ensures all necessary permissions are available to complete the import successfully.

1. Go to **[Settings](https://app.devrev.ai/?setting=airsyncs)**[ > ](https://app.devrev.ai/?setting=airsyncs)**[Integrations](https://app.devrev.ai/?setting=airsyncs)**[ > ](https://app.devrev.ai/?setting=airsyncs)**[AirSyncs](https://app.devrev.ai/?setting=airsyncs)** and select **AirSync** (or **Start AirSync** if it's your first).
2. Create a new connection to your Rocketlane account, or use an existing connection if you already have one.
3. Once the connection is established, select the Rocketlane workspace you want to import and specify the DevRev [[entities/part|part]] where the imported [[features/tickets|tickets]] should be created. This initiates a bulk import of the selected workspace.
4. Review and map fields manually if prompted.

The duration of the import depends on the size of the Rocketlane account. It can take seconds for an account with only a few tickets to a few hours for an account with tens of thousands of tickets with many attachments. DevRev honors the Rocketlane API rate limits and back-off and resume automatically.

## Related wiki nodes
- [[glossary/airsync]]

## Source
- DevRev support [[entities/article|article]] [Rocketlane AirSync](https://support.devrev.ai/en-US/devrev/article/7OPmGfqK) (ART-22000)
