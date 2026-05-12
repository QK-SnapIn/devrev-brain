---
title: SharePoint AirSync
devrev_id: ART-22011
parent_directory: AirSync
translation_group: QV3VNmJ5
modified_date: "2026-02-17T04:21:44.014Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/QV3VNmJ5"
tags: []
top_category: Computer by DevRev
wiki_match: glossary/airsync
match_score: 0.85
last_updated: 2026-05-11
related: ['glossary/airsync']
summary: "The SharePoint AirSync simplifies migration from SharePoint to DevRev, supporting both one-time imports and ongoing syncs."
---

# SharePoint AirSync

The SharePoint [[glossary/airsync|AirSync]] simplifies migration from SharePoint to DevRev, supporting both one-time imports and ongoing syncs.

SharePoint AirSync is a tool that lets you migrate your team's documents and knowledge from SharePoint into DevRev. It's like building a bridge between the two platforms, allowing you to:

* Transfer your site pages and content
* Keep your document organizational structure intact
* Bring over important file attachments
* Maintain user associations and relationships

Use the SharePoint AirSync if you need to:

* Import documents and [[features/knowledge-base|knowledge base]] [[entities/article|articles]] from SharePoint into DevRev platform
* Import libraries and their contents as per user requirements
* Maintain user identities and relationships between platforms
* Preserve organizational structures and hierarchies

# Supported objects

The following is a list of SharePoint objects and their corresponding DevRev equivalents. Those marked as **Sync to DevRev** are eligible for import from SharePoint to DevRev.

| SharePoint Object | DevRev Object | Sync to DevRev |
| --- | --- | --- |
| Pages (Site Pages, Web [[entities/part|Part]] Pages, Wiki Pages, Space) | [[entities/article|Article]] (URL), Article (Content) | ✅ |
| Library | Collection | ✅ |
| Attachment on Page / Library | [[features/artifacts|Artifacts]] on Article | ✅ |
| User | DevUser | ✅ |

# First time import overview

When using SharePoint AirSync for the first time:

1. **Admin Consent**: First, your organization's administrator needs to give consent to DevRev and establish the initial connection. After this is done, other organization members can create their own connections.
2. **Preparation**: Ensure you have appropriate access to your SharePoint [[entities/account|account]].
3. **Installation and Setup**: Follow the steps in the "Importing from SharePoint" section below.
4. **Connection Process**: You'll need to authenticate with your Microsoft account to establish a secure connection between SharePoint and DevRev.
5. **Selection Process**: You'll have the [[glossary/opportunity|opportunity]] to choose specific SharePoint sites to import, allowing you to be selective about what data moves to DevRev.
6. **Processing Time**: The import duration depends on the volume of data. Small sites might complete in seconds, while larger sites with thousands of pages and attachments may take hours.
7. **Results and Verification**: After completion, review the import report to confirm that all pages, libraries, users, and attachments were properly transferred.

> * Syncing from SharePoint to DevRev is one-way only. Changes made in DevRev won't reflect back in SharePoint, and syncing may overwrite DevRev customizations with SharePoint data.
> * Due to a known delay in the SharePoint API, changes made in SharePoint may take up to **1 hour** to reflect in DevRev after syncing.

## Set up SharePoint connection

To configure the SharePoint connection, you'll need to use OAuth authentication. Access to a SharePoint account with appropriate permissions is required.

### Import from SharePoint

1. Go to **Settings > Integrations > Snap-ins**.
2. Navigate to **All snap-ins** and [[features/search|search]] for **SharePoint AirSync**.
3. Open the snap-in and click the **Add** button located in the top-right corner.
4. Click **Install**.
5. Once installed, click on **Config**.
6. In the configuration screen, you will see an option for **Communication Site**. This allows you to choose whether to import its content as **Public** or **Restricted to Owner Only**.

> By default, the setting is **Restricted to Owner Only**. Toggle it according to your requirements.

7. Go to the **Airsync** option under **Integrations**.
8. Click the **Start Airsync** button and select **SharePoint**.
9. Click **Add Connection**, enter a connection name, then authenticate using **OAuth** to establish the connection.
10. After the connection is successfully established, select it to view a list of SharePoint sites.
11. Choose the sites and the corresponding **DevRev part** for import, then start the extraction.
12. Review the pre-configured field mappings and click **Next** to proceed through each step until the mapping process is complete.
13. The extraction will begin, and after some time, the import will be completed.
14. Click on the completed import to view a detailed report, including imported **Users**, **Pages**, **Libraries**, and **Attachments**.

## Supported site types

SharePoint AirSync supports both project and communication [[entities/group|group]] sites.

**Project group sites**

* Designed for team collaboration
* Integrated with Microsoft 365 [[entities/group|Groups]] and Teams
* Includes libraries, lists, wiki pages, and attachments
* Best for importing structured content and documents

**Communication group sites**

* Designed for broad announcements and info sharing
* Not connected to Microsoft Teams
* Focused on site pages and web part layouts
* Best for importing content as Article (URL)

## Post import options

After a successful import, you have the following options available for the imported site:

* **Sync to DevRev**

  This option allows you to synchronize any modifications made in SharePoint with the corresponding items previously imported into DevRev. It also creates new items in DevRev for any new content in SharePoint after the last sync or import.
* **View Report**

  This option allows you to access detailed information about the initial import and any subsequent syncs performed.
* **Delete Import**

  If you wish to remove the import and all items that were imported from SharePoint into DevRev, you can use this option.
* **Edit Connection**

  Use this option to change the connection used for any subsequent actions. It can be helpful if a connection becomes inactive or the user who established it is no longer available.

### Sync to DevRev

After a successful import from a SharePoint site, you can choose to sync the imported data with DevRev. This feature syncs any new pages, libraries, attachments, users, and any changes made to previously imported items from SharePoint.

To perform a one-time sync to DevRev, follow these steps:

1. Go to **Settings > Integrations > Airsync**.
2. Locate the previously imported site.
3. Select the **⋮** > **Sync SharePoint to DevRev** option.

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

> ⚠️ This deletes any content created by the import, including users, libraries, pages, and articles.

An import and all the content it creates can be deleted from DevRev. This can be useful when running POCs or to change the configuration used during the import. Once an import has been deleted, all the content it created gets deleted, even if they were modified in DevRev. It's possible to import the project again after its deletion.

To delete an import and all the content it created, go to **Settings > Integrations > Airsync**, find the previously imported project, and select **⋮** > **Delete Import**.

## Related wiki nodes
- [[glossary/airsync]]

## Source
- DevRev support article [SharePoint AirSync](https://support.devrev.ai/en-US/devrev/article/QV3VNmJ5) (ART-22011)
