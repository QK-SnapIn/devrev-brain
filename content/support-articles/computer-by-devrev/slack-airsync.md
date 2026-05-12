---
title: Slack AirSync
devrev_id: ART-22936
parent_directory: AirSync
translation_group: FEt-OfgM
modified_date: "2026-04-27T21:41:28.676Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/FEt-OfgM"
tags: []
top_category: Computer by DevRev
wiki_match: glossary/airsync
match_score: 0.85
last_updated: 2026-05-11
related: ['glossary/airsync']
summary: "Slack AirSync imports and syncs public channel conversations from Slack into DevRev."
---

# Slack AirSync

Slack [[glossary/airsync|AirSync]] imports and syncs public channel [[features/conversations-feature|conversations]] from Slack into DevRev. It supports one-time imports, time-scoped imports, and ongoing periodic syncs, ensuring that knowledge from Slack is accessible and searchable within DevRev.

For general information about how AirSync works, see the [[support-articles/computer-by-devrev/airsync-overview|AirSync overview]]. If you want to sync live Slack conversations with DevRev [[features/tickets|tickets]] and [[features/issues|issues]] in real time rather than importing historical data, see the [[support-articles/snap-ins/slack-snap-in|Slack snap-in article]] instead.

## Supported objects

The following is a list of Slack objects and their corresponding DevRev equivalents. Those marked as **Sync to DevRev** are eligible for import from Slack to DevRev.

| Slack Object | DevRev Object | Sync to DevRev |
| --- | --- | --- |
| Public Channel | Chat | ✅ |
| Public Channel Messages/Threads | Comments | ✅ |
| User Details | DevUser | ✅ |
| Channel Members | [[entities/group|Group]] Members | ✅ |

## Prerequisites

Before setting up Slack AirSync, ensure the following:

* **Slack admin access**: You need administrator permissions in the Slack workspace to authorize the connection and create Slack apps.
* **Public channels only**: Slack AirSync imports messages from public channels only. Private channels, direct messages, and group DMs are not supported.
* **One connection per workspace**: Each Slack workspace can have one active AirSync connection to a DevRev workspace at a time.
* **DevRev admin role**: You must have an admin role in your DevRev workspace to install snap-ins and configure AirSync.

## Connections

Establish an OAuth connection between Slack and DevRev before starting the import.

> 📝 **Note**: When selecting a connection during setup, the dropdown may display both **Slack** and **Slack AirSync** options. Select **Slack AirSync** for this integration.

1. Use Slack's OAuth flow to authenticate and generate a bot token.
2. Open Slack and navigate to the target public channel. In the message box, type `/invite @DevRev` and press **Enter**.
3. Confirm the bot has been added to the channel. Repeat for each public channel you want included in the import.

## Set up the import

1. Go to [Settings > Integrations > Snap-ins](https://app.devrev.ai/?setting=snap-ins) and [[features/search|search]] for **Slack AirSync** under **All Snap-ins**.
2. In the snap-in configuration modal, configure attachment import settings:

   * **Enable Extract attachments**: All files and attachments from Slack conversations are imported to DevRev.
   * **Disable Extract attachments**: Only [[entities/conversation|conversation]] messages are imported, with no files or attachments.
   > ⚠️ **Warning**: Attachment settings cannot be changed after the import begins. The import process starts immediately upon confirmation and cannot be re-run with different attachment settings without deleting the import and starting over. Ensure your configuration reflects what you want to import before proceeding.
3. In the **My Settings** section of the configuration page, toggle **Enable** to **true**. This activates the AirSync data extraction for your user [[entities/account|account]] and is required for the import to run. Save your changes.
4. Click **Install** to install the snap-in.
5. Go to [Settings > Integrations > AirSync](https://app.devrev.ai/?setting=airsyncs) and select the Slack logo to begin configuring the import.
6. Create a new connection to your Slack workspace or select an active existing connection. If prompted, choose the **Slack AirSync** option from the connection dropdown.
7. Select the import scope. You can import the entire Slack workspace or select specific public channels. You can also choose a time-scoped import (for example, messages from the last 7 days) rather than importing full history.

   > 📝 **Note**: If you perform a time-scoped import and later want to import the full history, you must delete the existing import and re-import with the broader time range. There is no way to extend the scope of an existing import incrementally.
8. DevRev automatically maps fields from Slack to DevRev. Review the mapping and adjust manually if prompted, then confirm to start the import.

Import duration depends on the volume of Slack messages and data. Small workspaces may complete in seconds, while large-scale imports can take several hours.

## Post-import options

After a successful import, the following options are available for the imported account at [Settings > Integrations > AirSync](https://app.devrev.ai/?setting=airsyncs) under the **⋮** context menu:

**Sync to DevRev**

Synchronize Slack messages and updates with the corresponding items in DevRev. This ensures continuous data syncing after the initial import.

**View report**

Access detailed reports of imported Slack conversations and subsequent syncs.

**Delete import**

Remove all imported Slack data from DevRev, including conversations, users, and [[entities/group|groups]].

**Edit connection**

Modify the existing connection settings for future imports and syncs.

### Sync to DevRev

After a successful import, you can perform a one-time sync to pull the latest Slack messages into DevRev:

> ⚠️ **Warning**: A one-time sync may overwrite fields that were modified in DevRev after the initial import. For details on how AirSync handles modifications, see [AirSync modification restrictions](https://support.devrev.ai/devrev/article/ART-8447).

1. Go to [Settings > Integrations > AirSync](https://app.devrev.ai/?setting=airsyncs) and locate the previously imported Slack workspace.
2. Select **⋮** > **Sync Slack to DevRev**.

### Historical imports

To view running and previous imports:

1. Go to [Settings > Integrations > AirSync](https://app.devrev.ai/?setting=airsyncs) and select the import you want to view.
2. Click the context menu (**⋮**) and select **View Report**.

### Periodic sync

After a successful import, you can enable periodic sync to automatically synchronize Slack data with DevRev on a recurring schedule:

1. Go to [Settings > Integrations > AirSync](https://app.devrev.ai/?setting=airsyncs) and locate the imported workspace.
2. Click **⋮** > **Set Periodic Sync**.
3. Configure the following options:

   * **Slack → DevRev**: Enable this option to sync data from Slack into DevRev on the selected schedule.
   * **DevRev → Slack**: Syncing from DevRev to Slack is not supported.
   * **Automation option**: Enable automation to trigger webhooks, snap-ins, and DevRev-native events for synced items. If disabled, periodic syncs do not trigger any events or automations.
4. Select the frequency and start date, then click **Schedule** to activate the periodic sync.

### Delete import

An import and all the content it creates can be deleted from DevRev. This is useful when running proofs of concept or when you need to change the configuration used during the import. Once deleted, all content created by the import is removed, even if items were modified in DevRev after import. You can import the workspace again after deletion.

> ⚠️ **Warning**: Deleting an import permanently removes all imported content, including users, groups, members, and messages.

To delete an import, go to [Settings > Integrations > AirSync](https://app.devrev.ai/?setting=airsyncs), find the previously imported workspace, and select **⋮** > **Delete Import**.

## Limitations

* **Public channels only**: Slack AirSync imports messages from public channels only. Private channels, direct messages, and group DMs are not imported.
* **Attachment size limit**: Attachments larger than 250 MB are not transferred. For more details on general AirSync constraints, see [[support-articles/computer-by-devrev/airsync-scope|AirSync scope and limitations]].
* **No deleted message sync**: Messages deleted in Slack after import are not removed from DevRev. AirSync does not propagate deletions.
* **No DevRev-to-Slack sync**: Data flows only from Slack to DevRev. Changes made in DevRev are not pushed back to Slack.
* **Time-scoped imports cannot be extended**: If you perform a time-scoped import, you cannot later extend it to include older messages. You must delete the import and re-import with the broader scope.

## Troubleshooting

* **[[entities/issue|Issue]]**: The connection dropdown shows both **Slack** and **Slack AirSync** and it is unclear which to select.

  **Solution**: Select **Slack AirSync**. The **Slack** option is for the real-time Slack snap-in integration, not for AirSync imports.
* **Issue**: The import completes but no messages appear for certain channels.

  **Solution**: Ensure the DevRev bot has been added to each public channel you want to import. In Slack, type `/invite @DevRev` in each target channel and confirm the bot is listed as a member.
* **Issue**: The snap-in shows an "invalid" or error state after installation.

  **Solution**: Go to [Settings > Integrations > Snap-ins](https://app.devrev.ai/?setting=snap-ins), uninstall the Slack AirSync snap-in, and reinstall it. Verify that your Slack OAuth token has all required scopes and has not expired.
* **Issue**: The import runs but does not include attachments.

  **Solution**: Confirm that **Extract attachments** was enabled during the snap-in configuration before the import started. Attachment settings cannot be changed after the import begins. If needed, delete the import and re-import with attachments enabled.

## Related wiki nodes
- [[glossary/airsync]]

## Source
- DevRev support [[entities/article|article]] [Slack AirSync](https://support.devrev.ai/en-US/devrev/article/FEt-OfgM) (ART-22936)
