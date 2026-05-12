---
title: Asana AirSync (Beta)
devrev_id: ART-22648
parent_directory: AirSync
translation_group: hxBLyPqQ
modified_date: "2026-04-07T13:46:13.749Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/hxBLyPqQ"
tags: []
top_category: Computer by DevRev
wiki_match: glossary/airsync
match_score: 0.85
last_updated: 2026-05-11
related: ['glossary/airsync']
summary: "The Asana AirSync simplifies migration between Asana and DevRev, supporting one-time imports, forward syncs, and reverse syncs."
---

# Asana AirSync (Beta)

The Asana [[glossary/airsync|AirSync]] simplifies migration between Asana and DevRev, supporting one-time imports, forward syncs, and reverse syncs.

# Supported objects

The following is a list of Asana objects and their corresponding DevRev equivalents. Those marked as **Sync to DevRev** are eligible for import from Asana to DevRev, and those marked as **Sync to Asana** are eligible for sync from DevRev back to Asana.

| Asana object | DevRev object | Sync to DevRev | Sync to Asana |
| --- | --- | --- | --- |
| [[entities/task|Task]] | [[entities/issue|Issue]] | ✅ | ✅ |
| Attachment | Attachment | ✅ | ✅ |
| User | DevUser | ✅ | ❌ |

## 

# Import from Asana

To perform a one-time import from Asana to DevRev:

1. Go to [Settings > Integrations > AirSyncs](https://app.devrev.ai/?setting=airsyncs).

2. Click **+Import** and select **Asana**.

3. Connect your Asana [[entities/account|account]] and select the project to import.

Asana [[entities/task|tasks]] are imported as DevRev [[features/issues|issues]] with automatic field mapping.

# Sync from Asana to DevRev

After the initial import, you can sync updates made in Asana to the previously imported issues in DevRev. Only tasks and attachments that were [[entities/part|part]] of the imported project are synced.

To perform a one-time sync from Asana to DevRev:

1. Go to [Settings > Integrations > AirSyncs](https://app.devrev.ai/?setting=airsyncs).

2. Locate the imported Asana project.

3. Select ⋮ > **Sync Asana to DevRev**.

# Sync from DevRev to Asana

After a successful import from an Asana project, you can sync changes made in DevRev back to Asana. Additionally, any new DevRev issues marked for sync are created as new Asana tasks.

To perform a one-time sync from DevRev to Asana:

1. Go to [Settings > Integrations > AirSyncs](https://app.devrev.ai/?setting=airsyncs).

2. Locate the previously imported Asana project.

3. Select ⋮ > **Sync DevRev to Asana**.

# Limitations

- DevRev issues require `priority` and `stage`. Asana tasks do not provide these by default.

- All imported issues are created with priority *P0* and stage *Backlog*.

- Asana custom fields are not supported.

## Related wiki nodes
- [[glossary/airsync]]

## Source
- DevRev support [[entities/article|article]] [Asana AirSync (Beta)](https://support.devrev.ai/en-US/devrev/article/hxBLyPqQ) (ART-22648)
