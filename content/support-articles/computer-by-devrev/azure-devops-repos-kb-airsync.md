---
title: Azure DevOps Repos KB AirSync
devrev_id: ART-23311
parent_directory: AirSync
translation_group: r_2NCgFb
modified_date: "2026-02-16T11:28:19.408Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/r_2NCgFb"
tags: []
top_category: Computer by DevRev
wiki_match: glossary/airsync
match_score: 0.85
last_updated: 2026-05-11
related: ['glossary/airsync']
summary: "The Azure DevOps Repos KB AirSync simplifies migration of markdown documentation from Azure DevOps repositories to DevRev\"s Knowledge Base."
---

# Azure DevOps Repos KB AirSync

The Azure DevOps Repos KB [[glossary/airsync|AirSync]] simplifies migration of markdown documentation from Azure DevOps repositories to DevRev's [[features/knowledge-base|Knowledge Base]]. This integration enables seamless synchronization of documentation files, folder structures, users, [[entities/group|groups]], and repository permissions, bringing your technical documentation into your DevRev workspace.

### Supported objects

The following is a list of Azure DevOps objects and their corresponding DevRev equivalents. Those marked as **Sync to DevRev** are eligible for import from Azure DevOps to DevRev.

| Azure DevOps object | DevRev object | Sync to DevRev |
| --- | --- | --- |
| Markdown Files | [[entities/article|Article]] | ✅ |
| Folders | Collection (Directory) | ✅ |
| Users | DevUser | ✅ |
| Groups | [[entities/group|Group]] | ✅ |
| Group Members | Object Member | ✅ |
| Repository Permissions | Article Permissions (access\_level, shared\_with) | ✅ |

### Setting up the Azure DevOps connection

To configure the Azure DevOps connection, you need to create a Personal Access Token (PAT) with the following access scopes:

* **Code (Read)** - Read repository files and folder structure
* **Graph (Read)** - Read users and groups from Azure AD
* **Security (Read)** - Read permissions and access control lists
* **Project and Team (Read)** - Read project metadata

To create a Personal Access Token:

1. Go to Azure DevOps: `https://dev.azure.com/{your-organization}`
2. Click **User Settings (profile icon) > Personal Access Tokens**
3. Click **New Token** and configure:

   * **Name:** DevRev Snap-in Integration (or your preferred name)
   * **Organization:** Select your organization
   * **Expiration:** Choose duration (1 year recommended)
   * **Scopes:** Select the required scopes listed above
4. Click **Create** and copy the token immediately (it won't be shown again)

### Importing from Azure DevOps Repos

1. Log in to DevRev.
2. Go to **Settings > Integrations > Snap-ins**, [[features/search|search]] for **Azure DevOps Repos** under **All Snap-ins**.
3. Click **Add and Install Snap-in**.
4. Navigate to **Settings > Integrations > Airsync** in the left-navigation.
5. Click **Airsync** in the top right corner and select **Azure DevOps Repos**.
6. Create a new connection to authenticate with your Azure DevOps organization:

   * Enter a connection name
   * Provide your Azure DevOps organization subdomain
   * Provide your Azure DevOps username
   * Provide your Personal Access Token (PAT)
   * Click **Submit** to authenticate
7. Once the connection is established, configure the import settings:

   * Enter the **Git Branch Name** to sync from, such as, main, master, develop
8. Select the repository you want to import and specify the DevRev [[entities/part|part]] that should be used for any imported content.
9. Click **Start** to trigger the import.

> Import duration varies from minutes to hours based on the number of files, users, and groups in your Azure DevOps organization.

### Configuration options

| Option | Description | Default |
| --- | --- | --- |
| Git Branch Name | The branch name to sync markdown files from (any valid branch) | main |

### Permission mapping

Repository permissions from Azure DevOps are automatically mapped to DevRev article permissions:

| Azure DevOps Permission | DevRev Role |
| --- | --- |
| Manage Permissions, Delete Repository | Owner |
| Generic Write, Generic Contribute, Create Branch, Create Tag | Editor |
| Generic Read | Viewer |

Access level mapping:

* **Private repositories** → Internal access level
* **Public repositories** → External access level

## Limitations

* **Unidirectional sync only**: Data flows from Azure DevOps to DevRev. Changes made in DevRev are not synced back to Azure DevOps.
* **Markdown files only**: Only `.md` and `.markdown` files are extracted. Other file types are not synced.
* **Single branch sync**: Each sync operates on one configured branch at a time.
* **No folder permissions**: DevRev collections (folders) do not support permissions. Only [[entities/article|articles]] receive permission mappings.
* **No transactional guarantees**: If an import fails partway through, partial data may exist in DevRev without automatic rollback.
* **Image link conversion**: Image references in markdown (`![alt](url)`) are converted to regular links (`[alt](url)`) for DevRev compatibility.
* **Group-based permissions only**: Only group permissions from Azure DevOps repository ACLs are mapped to DevRev articles. Individual user permissions set directly on repositories are not imported. Users inherit article access through their group membership in DevRev, which mirrors Azure DevOps' group-based permission model. For more details on Azure DevOps permissions, see [About permissions and security groups](https://learn.microsoft.com/en-us/azure/devops/organizations/security/about-permissions).
* **Nested groups are flattened**: Azure DevOps supports nested groups (groups containing other groups). Since DevRev does not support hierarchical group memberships, the connector automatically flattens nested groups by extracting all users from nested groups and adding them directly to the parent group. This ensures users inherit the correct permissions. For example, if GroupA contains GroupB (which has UserX), UserX will be added as a direct member of GroupA in DevRev.
* **File and folder renames create duplicates**: Articles and collections are identified by their full path. If a file is renamed or moved in Azure DevOps, a new article is created in DevRev. If a folder is renamed or moved, new collections are created for the folder AND new articles are created for ALL markdown files within that folder (since their paths change).

## Post import options

After a successful import, you have the following options available for the imported data:

* **Sync to DevRev**

  This option allows you to synchronize any modifications made in Azure DevOps with the corresponding items previously imported into DevRev. It also creates new items in DevRev for any files, users, or groups added or updated in Azure DevOps after the last sync or import.
* **View Report**

  This option allows you to access detailed information about the initial import and any subsequent syncs performed, including statistics on files synced, users imported, and groups processed.
* **Delete Import**

  If you want to remove the import and all data that were imported from Azure DevOps into DevRev, you can use this option. This will delete all articles, collections, and related metadata.
* **Edit Connection**

  Use this option to change the connection used for any subsequent actions. It can be helpful if a PAT token has expired or needs to be rotated, the user who established the connection is no longer available, or you want to use a different Azure DevOps [[entities/account|account]].

### Sync to DevRev

After a successful import from Azure DevOps, you can choose to sync the imported data with DevRev. This feature imports any new or updated markdown files, users, groups, and permissions, as well as any changes made to previously imported items from Azure DevOps.

The snap-in supports incremental syncs using commit history. When performing a sync after the initial import:

* Only files changed since the last successful sync are processed
* Added, modified, and renamed files are synced
* Deleted files are identified but not removed (DevRev limitation)

To perform a one-time sync to DevRev, follow these steps:

1. Go to **Settings > Integrations > Airsync**.
2. Locate the previously imported Azure DevOps repository.
3. Select the **⋮** > **Sync Azure DevOps to DevRev** option.

> A one-time sync may overwrite fields in previously imported items, even if they were modified in DevRev.

### Historical imports

To view currently running and previous imports from various sources, do the following:

1. Go to **Settings > Integrations > Airsync**.
2. Select the import you want to view.
3. Click on the context menu (⋮) and select **View Report**.

The report includes detailed statistics such as:

* Total number of markdown files synced
* Number of articles created
* Users and groups imported
* Folders (collections) created
* Sync duration and any errors encountered

### Periodic sync

After successfully importing to DevRev, you have the option to enable a periodic sync. This allows for automatic synchronization with DevRev on a regular basis. By default, the sync occurs once an hour.

To configure periodic sync, follow these steps:

1. Go to **Settings > Integrations > Airsync**.
2. Locate the previously imported Azure DevOps repository.
3. Select the **⋮** > **Set Periodic Sync** option.

The Enable automation for synced items setting is optional and can be activated during periodic sync configuration. When enabled, newly created or updated items trigger events, which can initiate webhooks, notifications, snap-ins, and other processes, as if the events originated directly in DevRev.

If this setting is turned off, updates do not trigger any event-driven processes. This behavior applies only to periodic syncs; no events are triggered during a first-time import or manual sync to DevRev.

### Delete import

> This deletes any content created by the import, including articles, collections, users, groups, and related metadata.

An import and all the content it creates can be deleted from DevRev. This can be useful when running POCs or to change the configuration used during the import. Once an import has been deleted, all the content it created gets deleted, even if they were modified in DevRev. It's possible to import the Azure DevOps repository again after its deletion.

To delete an import and all the content it created, go to **Settings > Integrations > Airsync**, find the previously imported Azure DevOps repository, and select **⋮** > **Delete Import**.

## Related wiki nodes
- [[glossary/airsync]]

## Source
- DevRev support article [Azure DevOps Repos KB AirSync](https://support.devrev.ai/en-US/devrev/article/r_2NCgFb) (ART-23311)
