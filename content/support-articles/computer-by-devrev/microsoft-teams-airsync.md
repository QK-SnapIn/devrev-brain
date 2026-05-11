---
title: Microsoft Teams AirSync
devrev_id: ART-22013
parent_directory: AirSync
translation_group: -e6ab1x4
modified_date: "2026-02-17T04:35:07.2Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/-e6ab1x4"
tags: []
top_category: Computer by DevRev
wiki_match: glossary/airsync
match_score: 0.85
last_updated: 2026-05-11
related: ['glossary/airsync']
summary: "The Microsoft Teams AirSync simplifies migration from MS Teams to DevRev, supporting both one-time imports and ongoing syncs."
---

# Microsoft Teams AirSync

The Microsoft Teams [[glossary/airsync|AirSync]] simplifies migration from MS Teams to DevRev, supporting both one-time imports and ongoing syncs.

Microsoft Teams AirSync is a tool that lets you migrate your team's communication from Microsoft Teams into DevRev. It's like building a bridge between the two platforms, allowing you to:

* Transfer your team's [[entities/conversation|conversation]] history
* Keep your organizational structure intact
* Bring over important file attachments
* Maintain user associations and relationships

Use the Microsoft Teams AirSync if you need to:

* Import chat messages from channels of Microsoft Teams into DevRev platform
* Import attachments from messages as per user requirements
* Maintain user identities and relationships between platforms
* Sync channels with their corresponding DevRev [[features/chats|chats]]

# Supported objects

The following is a list of Microsoft Teams objects and their corresponding DevRev equivalents. Those marked as **Sync to DevRev** are eligible for import from Microsoft Teams to DevRev.

| Microsoft Teams Object | DevRev Object | Sync to DevRev |
| --- | --- | --- |
| User | [[features/identity|Identity]]/DevUser | ✅ |
| Channel | Chat | ✅ |
| Attachments in Message/Thread | [[features/artifacts|Artifacts]] on Comment | ✅ |
| Message | Comment | ✅ |

# First time import overview

When using Microsoft Teams AirSync for the first time:

1. **Preparation**: Ensure you have admin access to your Microsoft Teams [[entities/account|account]] (Only Professional/Organizational account). Also Admin has to give permission before the non admin uses the account.
2. **Installation and Setup**: Follow the steps in the "Importing from Microsoft Teams" section below.
3. **Attachment Consideration**: Decide whether to import attachments based on your storage needs and migration timeline.
4. **Connection Process**: When establishing your connection, you'll need to authenticate with Microsoft. This creates a secure link between your Teams account and DevRev.
5. **Selection Process**: You'll have the [[glossary/opportunity|opportunity]] to choose specific channels to import, allowing you to be selective about what data moves to DevRev.
6. **Processing Time**: The import duration depends on the volume of data. Small teams might complete in minutes, while larger organizations with extensive history may take hours.
7. **Results and Verification**: After completion, review the import report to confirm that all users, channels, messages, and attachments were properly transferred.

> Syncing from Teams to DevRev is one-way only. Changes made in DevRev won't reflect back in Teams, and syncing may overwrite DevRev customizations with Teams data.

## Set up Microsoft Teams connection

To configure the Microsoft Teams connection, you'll need to use OAuth authentication. Access to a Microsoft Teams admin account is required.

### Import from Microsoft Teams

1. Go to **Settings > Integrations > Snap-ins**.
2. Navigate to **All snap-ins** and [[features/search|search]] for **MS Teams AirSync**.
3. Open the snap-in and click the **Add** button located in the top-right corner.
4. While installing, you'll see a toggle for importing attachments. Enable or disable this toggle based on your requirements, then click save button to save the configuration and click **Install**.
5. Go to the **Airsync** option under **Integrations**.
6. Click the **Start Airsync** button and select Microsoft Teams.
7. Click **Add Connection**, or enter a connection name, then click **Sign in with Snap-ins** to establish the connection.
8. After successfully establishing the connection, select that connection to view the list of channels from Teams.
9. Select the channels and the DevRev [[entities/part|part]] for import, then start the extraction.
10. You'll be presented with field mappings which are already configured. Review these mappings and click **Next** until you finish the mapping process.
11. The extraction will begin and after some time, the import will be completed.
12. Click on the completed import to view a detailed report showing imported Users, Channels, Attachments, and Messages.

# Post import options

After a successful import, you have the following options available for the imported account:

* **Sync to DevRev**

  This option allows you to synchronize any modifications made in Microsoft Teams with the corresponding items previously imported into DevRev. It also creates new items in DevRev for any new data in Microsoft Teams after the last sync or import.
* **View Report**

  This option allows you to access detailed information about the initial import and any subsequent syncs performed.
* **Delete Import**

  If you wish to remove the import and all items that were imported from Microsoft Teams into DevRev, you can use this option.
* **Edit Connection**

  Use this option to change the connection used for any subsequent actions. It can be helpful if a connection becomes inactive or the user who established it is no longer available.

### Sync to DevRev

After a successful import from a Microsoft Teams team, you can choose to sync the imported data with DevRev. This feature syncs any new channels, messages, users, [[entities/task|tasks]], and any changes made to previously imported items from Microsoft Teams.

To perform a one-time sync to DevRev, follow these steps:

1. Go to **Settings > Integrations > Airsync**.
2. Locate the previously imported team.
3. Select the **⋮** > **Sync Microsoft Teams to DevRev** option.

> ⚠️ A one-time sync may overwrite fields in previously imported items, even if they were modified in DevRev.

### Historical imports

To view currently running and previous imports from various sources, do the following:

1. Go to **Settings > Integrations > Airsync**.
2. Select the import you want to view.
3. Click on the context menu (⋮) and select **View Report**.

### Periodic sync

After successfully importing to DevRev, you have the option to enable a periodic sync. This allows for automatic synchronization with DevRev on a regular basis. By default, the sync occurs once an hour.

To configure periodic sync, follow these steps:

1. Go to **Settings > Integrations > Airsync**.
2. Locate the previously imported project.
3. Select the **⋮** > **Set Periodic Sync** option.

The Enable automation for synced items setting is optional and can be activated during periodic sync configuration. When enabled, newly created or updated items trigger events, which can initiate webhooks, notifications, Snap-ins, and other processes, as if the events originated directly in DevRev.

If this setting is disabled, updates will not trigger any event-driven processes. This behavior applies only to periodic syncs; no events are triggered during a first-time import or manual sync to or from DevRev.

### Delete import

> ⚠️ This deletes any content created by the import, including users, channels, messages, and attachments.

An import and all the content it creates can be deleted from DevRev. This can be useful when running POCs or to change the configuration used during the import. Once an import has been deleted, all the content it created gets deleted, even if they were modified in DevRev. It's possible to import the project again after its deletion.

To delete an import and all the content it created, go to **Settings > Integrations > Airsync**, find the previously imported project, and select **⋮** > **Delete Import**.

## Related wiki nodes
- [[glossary/airsync]]

## Source
- DevRev support [[entities/article|article]] [Microsoft Teams AirSync](https://support.devrev.ai/en-US/devrev/article/-e6ab1x4) (ART-22013)
