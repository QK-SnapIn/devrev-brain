---
title: AirSync overview
devrev_id: ART-21842
parent_directory: AirSync
translation_group: i96Xvth5
modified_date: "2026-05-07T03:51:41.862Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/i96Xvth5"
tags: []
top_category: Computer by DevRev
wiki_match: glossary/airsync
match_score: 0.85
last_updated: 2026-05-11
related: ['glossary/airsync']
---

# AirSync overview

AirSync imports and synchronizes data between Computer and external platforms. You can perform a one-time import, set up a one-way sync from an external source to Computer, or establish a two-way sync that keeps both systems updated. AirSync preserves context, relationships, and permissions for every record, unifying structured and unstructured data into Computer's [[support-articles/computer-by-devrev/airsync-scope|Memory]].

AirSync supports near-real-time, bidirectional synchronization through periodic sync runs (by default, once per hour). By connecting tickets, conversations, product backlogs, documents, and more, AirSync consolidates scattered information into a single source of truth for both your teams and AI agents.

For details on what AirSync does and does not synchronize, including attachment size limits and schema change behavior, see [[support-articles/computer-by-devrev/airsync-scope|AirSync scope and limitations]].

> 📝 **Note**: AirSync was previously known as *DevRev Airdrop*. If you encounter references to "Airdrop" elsewhere, they refer to this same feature.

## AirSync features

The AirSync features available vary per external source but support one or more of these:

* **One-time import**: Migrate data from an external source to DevRev.
* **One-way sync**: Keep data synchronized from an external source to DevRev on an ongoing basis.
* **Two-way sync**: Synchronize data bidirectionally between DevRev and an external source. Changes made in DevRev propagate back to the external system and vice versa.
* **Recipe manager**: Select the object types and fields you want to AirSync from an external source.

## Prerequisites

Before setting up an AirSync, install the appropriate AirSync snap-in from the [DevRev Marketplace](https://marketplace.devrev.ai). Each external source has its own snap-in (for example, Jira, Zendesk, Salesforce). The snap-in must be installed and active in your workspace before you can configure an import.

For a full list of supported connectors, browse the AirSync category in the [DevRev Marketplace](https://marketplace.devrev.ai).

## General process

### Set up a new AirSync

> 📝 **Note**: Use an administrator account on the external source to ensure all necessary permissions are available.

Whether you want to perform only a one-time import or set up an ongoing sync, performing an initial import is required.

1. Go to [Settings > Integrations > AirSyncs](https://app.devrev.ai/?setting=airsyncs) and select **AirSync** (or **Start AirSync** if this is your first).
2. Select the external platform (for example, Jira, Zendesk) from which you want to import data, then authenticate with the external source.
3. Initiate the import process, which brings in enough data and metadata to allow you to configure the rest of the process.
4. Configure the import settings, such as selecting specific objects and mapping fields using the recipe manager.

## Post-import options

After a successful import, you have the following options available:

* **Sync to DevRev**: Triggers a one-time sync that pulls new and updated content from the external source into DevRev.
* **View report**: Access detailed information about the initial import and any subsequent syncs.
* **Delete import**: Remove the import and all imported items from DevRev.
* **Edit connection**: Modify the connection settings, such as updating credentials or changing the connected account. This is useful when authentication tokens expire or when you need to switch to a different service account.

### Sync to DevRev

After importing, you can trigger a sync to pull the latest content into DevRev. This feature ensures that any new or modified content is reflected in DevRev.

To perform a one-time sync to DevRev:

1. Go to [Settings > Integrations > AirSyncs](https://app.devrev.ai/?setting=airsyncs) and locate the previously imported project.
2. Select ⋮ > **Sync to DevRev**.

> ⚠️ **Warning**: A one-time sync may overwrite fields in previously imported items, even if they were modified in DevRev. For details on which fields are protected from overwriting, see [AirSync modification restrictions](https://support.devrev.ai/devrev/article/ART-8447).

### Historical AirSyncs

To view running and previous AirSyncs from various sources:

1. Go to [Settings > Integrations > AirSyncs](https://app.devrev.ai/?setting=airsyncs) and select the import you want to view.
2. Select ⋮ > **View Report** to see sync history and details.

### Periodic sync

After successfully importing to DevRev, you can enable a periodic sync for automatic synchronization on a regular basis. By default, the sync occurs once per hour.

To configure periodic sync:

1. Go to [Settings > Integrations > AirSyncs](https://app.devrev.ai/?setting=airsyncs) and locate the previously imported project.
2. Select ⋮ > **Set Periodic Sync** and configure the desired interval.

The **Enable automations for synced items** setting is optional and can be activated during periodic sync configuration. When enabled, newly created or updated items trigger events, which can initiate webhooks, notifications, snap-ins, and other processes, as if the events originated directly in DevRev.

If this setting is disabled, updates do not trigger any event-driven processes. This behavior applies only to periodic syncs; no events are triggered during a first-time import or manual sync to or from DevRev.

### Delete import

Deleting an import removes all content created by that import from DevRev, including users and work items. Deletion does not propagate to the external system; records in the external source remain unchanged.

> ⚠️ **Warning**: All imported content is deleted even if it was modified in DevRev after import. This action cannot be undone. For more information on how data deletion works, see [Understanding data deletion options](https://support.devrev.ai/devrev/article/ART-20486).

This can be useful when running POCs or when you need to change the recipe used during the import. After deletion, you can re-import the project.

To delete an import and all the content it created, go to [Settings > Integrations > AirSyncs](https://app.devrev.ai/?setting=airsyncs), find the previously imported project, and select ⋮ > **Delete Import**.

## Filter AirSynced records

After an import, you can view the sync status of imported items. The sync status indicates whether an item is in sync with the external source or if there are discrepancies. You can apply the following sync status filters to records:

* **Succeeded**: The import was successful, and the record is in sync with the external source.
* **Modified**: Minor modifications were made to the record after sync, but no constraints were violated.
* **Staged**: Data model constraints were violated and the record requires attention before it can fully sync. For example, a contact is linked to an account that does not exist in DevRev, or a required field mapping is missing. Review staged records and resolve the constraint issue to move them to a synced state.
* **Failed**: The record was not synced due to an error.

**Other sync metadata**

* **Sync date**: Filter to records that were synced in or out at a specific time.
* **Sync origin status**: Filter to records synced in or out from a specific external source (for example, items synced from Jira, Zendesk, or Salesforce Service).
* **Sync unit**: Filter to records synced from a specific sync unit in the origin system, such as a specific project in Jira.

## Record view

AirSynced items display an icon at the top of the record, next to the display ID and subtype, which indicates:

* Source system
* Sync status
* Sync date
* A link back to this item in the external source

You can identify imported items by the identifier next to the display ID in the vista view without opening the record. Sync filters are also available in vista view. AirSynced records may also have a custom tag applied that can be used for filtering.

## Related wiki nodes
- [[glossary/airsync]]

## Source
- DevRev support article [AirSync overview](https://support.devrev.ai/en-US/devrev/article/i96Xvth5) (ART-21842)
