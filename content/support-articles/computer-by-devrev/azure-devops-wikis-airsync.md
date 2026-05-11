---
title: Azure DevOps Wikis AirSync
devrev_id: ART-22014
parent_directory: AirSync
translation_group: yYohvsGz
modified_date: "2026-02-16T11:49:55.624Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/yYohvsGz"
tags: []
top_category: Computer by DevRev
wiki_match: glossary/airsync
match_score: 0.85
last_updated: 2026-05-11
related: ['glossary/airsync']
summary: "The Azure DevOps Wikis AirSync simplifies the migration of Wiki content from Azure DevOps to DevRev, supporting both one-time imports and ongoing syncs."
---

# Azure DevOps Wikis AirSync

The Azure DevOps Wikis [[glossary/airsync|AirSync]] simplifies the migration of Wiki content from Azure DevOps to DevRev, supporting both one-time imports and ongoing syncs.

### configure the Azure DevOps Connection

To configure the Azure DevOps connection, ensure the Azure DevOps token includes the following access scopes:

* Code - Read
* Graph - Read
* [[features/identity|Identity]] - Read
* Member Entitlement Management - Read
* Project and Team - Read
* Security - Manage
* Wiki - Read

### Supported objects

The following is a list of Azure DevOps Wiki objects and their corresponding DevRev equivalents. Those marked as **Sync to DevRev** are eligible for import from Azure DevOps to DevRev.

| Azure Wikis Object | DevRev Object | Sync to DevRev |
| --- | --- | --- |
| Code Wikis | [[entities/article|Articles]] | ✅ |
| Project Wikis | Articles | ✅ |
| Users | Identities | ✅ |
| [[entities/group|Groups]] | Groups | ✅ |

### Import from Azure DevOps Wikis

1. Go to **Marketplace** and [[features/search|search]] for **Azure DevOps Wikis** in the **Airsync** category.
2. Install the snap-in and configure it in the **Airsync** section of your settings.
3. Click **+Import** and select the Azure DevOps Wikis logo.
4. Create a new connection to your Azure DevOps [[entities/account|account]] or use an existing one.
5. Once the connection is established, select the Azure DevOps organization and Wiki repositories to import.
6. DevRev automatically maps fields from Azure DevOps Wikis to DevRev articles. You may be prompted to manually map certain fields if needed.

The duration of the import depends on the size of the Azure DevOps Wikis content. DevRev respects API rate limits and resumes automatically if necessary.

## Limitations

> ⚠️ **Mermaid Diagram Support**: DevRev currently does not support Mermaid diagrams. Any Mermaid syntax included in Azure DevOps Wikis will not render as expected in DevRev and may appear as raw text in the final articles.

## Post import options

After a successful import, you have the following options available:

* **Sync to DevRev**

  This option keeps your Azure DevOps Wikis content synchronized with DevRev, ensuring that new articles and updates are continuously reflected.
* **View Report**

  Access detailed information about the initial import and any subsequent syncs.
* **Delete Import**

  Remove the import and all imported items from DevRev.
* **Edit Connection**

  Modify the connection settings if needed.

### Sync to DevRev

After importing from an Azure DevOps Wikis account, you can enable sync to keep your content updated in DevRev. This feature ensures that any new or modified Wiki content in Azure DevOps is reflected in DevRev.

To perform a one-time sync to DevRev, follow these steps:

1. Go to **Settings > Integrations > Airsync**.
2. Locate the previously imported project.
3. Select the **⋮** > **Sync Azure DevOps Wikis to DevRev** option.

> ⚠️ A one-time sync may overwrite fields in previously imported articles, even if they were modified in DevRev.

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

> ⚠️ This deletes any content created by the import, including users, groups, and articles.

An import and all the content it creates can be deleted from DevRev. This can be useful when running POCs or to change the configuration used during the import. Once an import has been deleted, all the content it created gets deleted, even if they were modified in DevRev. It's possible to import the project again after its deletion.

To delete an import and all the content it created, go to **Settings > Integrations > Airsync**, find the previously imported project, and select **⋮** > **Delete Import**.

## Related wiki nodes
- [[glossary/airsync]]

## Source
- DevRev support [[entities/article|article]] [Azure DevOps Wikis AirSync](https://support.devrev.ai/en-US/devrev/article/yYohvsGz) (ART-22014)
