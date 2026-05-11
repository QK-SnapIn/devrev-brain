---
title: Azure Boards AirSync
devrev_id: ART-22017
parent_directory: AirSync
translation_group: pIFPpCr4
modified_date: "2026-02-16T11:43:41.926Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/pIFPpCr4"
tags: []
top_category: Computer by DevRev
wiki_match: glossary/airsync
match_score: 0.85
last_updated: 2026-05-11
related: ['glossary/airsync']
summary: "The Azure Boards AirSync simplifies migration from Azure Boards to DevRev, supporting both one-time imports and ongoing syncs."
---

# Azure Boards AirSync

The Azure Boards [[glossary/airsync|AirSync]] simplifies migration from Azure Boards to DevRev, supporting both one-time imports and ongoing syncs.

### Configure the Azure Boards Connection

To configure the Azure Boards connection, ensure the Azure Boards token includes the following access scopes:

* Member Entitlement Management - Read
* Project and Team - Read
* Work Items - Read

### Supported objects

The following is a list of Azure Boards objects and their corresponding DevRev equivalents. Those marked as **Sync to DevRev** are eligible for import from Azure Boards to DevRev and marked as **Sync to Azure Boards** are eligible for import from DevRev to Azure Boards.

| Azure Boards Object | DevRev Object | Sync to DevRev | Sync to Azure Boards |
| --- | --- | --- | --- |
| Work Item | [[entities/issue|Issue]]/[[entities/ticket|Ticket]] | ✅ | ✅ |
| Comment on Work Item | Comments on Issue/Ticket | ✅ | ✅ |
| Tag on Work Item | Tags on Issue/Ticket | ✅ | ✅ |
| Attachment on Work Item | Attachment on Issue/Ticket | ✅ | ✅ |
| User | DevUser | ✅ | ❌ |
| Stage on Work Item | State/Stage on Issue/Ticket | ✅ | ✅ |
| Filter | [[glossary/vista|Vista]] | ❌ | ❌ |
| Extensions | Snap-in | ❌ | ❌ |

### Import from Azure Boards

1. Log in to DevRev.
2. Go to **Settings** and [[features/search|search]] for **Integrations**.
3. In the snap-in config, click on **All Snap-ins**, search for **Azure Boards**, Click **Add** and **Install Snap-in**.
4. Go to **Settings > Airsync** in the left-navigation.
5. Click **Airsync** in top right corner and select the **Azure Boards**.
6. Create a new connection to authenticate with your Azure Boards workspace, or use an existing active connection.
7. Once the connection is successfully established:

   * In DevRev, navigate to **Settings > Airsync**, then click **Airsync** in the top-right corner.
   * Select **Azure Boards**.
   * Select the connection you just created. Click on **Next**.
   * On the next screen the list of projects will be displayed. Choose the project you wish to import.
   * Specify the **DevRev [[entities/part|part]]** where the imported content should reside, then click on **Start**. This will trigger a bulk import of the selected content.
8. DevRev makes an effort to automatically map the fields from Azure Boards to the corresponding fields in DevRev. However, you may be prompted to manually map certain fields if needed.

> The duration of the import depends on the size of the Azure Boards [[entities/account|account]] and the data being imported. It can take seconds for an account with only a few dozen work items to a few hours for an account with tens of thousands of items with many attachments. DevRev honors the Azure Boards API rate limits and back-off and resumes automatically.

### Creating an Azure Boards Connection

1. In Azure Boards home, select the workspace.
2. Click on **User settings** and select the **Personal access tokens**.
3. Click on **+New Token** on the top right corner.

   * Give a name to the connection.
   * Select the organization.

> If the expiration time is set for the token, ensure that once it expires, create a new connection to authenticate with the workspace.

4. In **Scope**, select the **Custom defined** radio button. Choose the following scopes:

   * **Work Item** – Read & Write
   * **Member Entitlement Management** – Read

   Then, click on **Create**.
5. On the next screen, the token will be visible. Copy it and use it to establish the connection in DevRev.

## Limitations

* Links between [[features/issues|Issues]] and [[features/tickets|Tickets]], and between Tickets, are not supported.
* Deep hierarchies (multiple levels of linked work items) are not supported.
* If a work item has a missing or invalid priority or severity value, a default value will be assigned to the corresponding issue or ticket in DevRev.
* Some work item stages may require manual mapping if they are of different project type or having custom stages.
* Syncing of reactions on comments is not supported.
* In forward sync, if the field (priority/severity) is blank in ADO but it's required in DevRev, DevRev will assign a default value, and during two-way sync, this default will be pushed back to ADO.

### Import from DevRev to Azure Boards (Reverse Sync)

After a successful import of an Azure Boards project, you have the sync from DevRev to Azure Boards option. This feature writes back any changes made in DevRev to previously imported issues from Azure Boards. Additionally, any new DevRev work marked for sync to this project is created in Azure Boards.

To perform a one-time sync to Azure Boards, go to **Settings > Integrations > Airsync**, find the previously imported project, and select the **⋮** > **Sync DevRev to Azure Boards** option.

> ⚠️ This overrides the workitem's fields, even if they were changed in Azure Board.

### Supported Objects for Reverse Sync

During reverse sync from DevRev to Azure Boards, the following DevRev objects and their Azure Boards equivalents are supported. Objects marked as Sync to Azure Boards are available for import from DevRev to Azure Boards.

| DevRev Object | Azure Boards Object | Sync to Azure Boards |
| --- | --- | --- |
| Issue/Ticket | Work Item | ✅ |
| Comments on Issue/Ticket | Comment on Work Item | ✅ |
| Tags on Issue/Ticket | Tag on Work Item | ✅ |
| Attachment on Issue/Ticket | Attachment on Work Item | ✅ |
| DevUser | User | ❌ |
| State/Stage on Issue/Ticket | Stage on Work Item | ✅ |

### Sync to Azure Boards

This feature enables synchronization of updates made in DevRev to the corresponding items imported through forward sync. Additionally, it creates new work items in Azure Boards whenever a new issue or ticket is created in DevRev.

> To sync newly created or modified issues/tickets from DevRev back to Azure Boards, the project subtype must be selected beforehand. Using the Sync from DevRev to Azure Boards feature, it's possible to sync DevRev work items to Azure Boards projects that have been imported to DevRev. In order to sync a DevRev work item to Azure Boards, it must be marked for syncing. Marking a DevRev work item for syncing can be done during the creation of a work item. During work creation, open the dropdown Select Subtype, set it to the Azure Boards project, and type the work item that should be synced. The display format is as follows: {Azure Boards project name} / issues / {type}. For example, if you want to sync to a Bug to a Azure Boards project called Sample, this would show as Sample / issues / Bug.

### Reverse Sync Limitations

* Syncing users from DevRev to Azure Boards is not supported.
* Comments can only be posted by the user who set up the connection. To address this, each comment is prefixed with the original DevRev user's name.
* Stages of work items that were mapped to DevRev stock stages during forward sync need to be mapped appropriately during reverse sync.
* If a work item's owner does not exist in Azure Boards:

  + If "Assigned To" is optional, the owner will be set as "Unassigned".
  + If "Assigned To" is mandatory, the owner will default to the user who established the connection.
* If a comment is created by a user who exists in DevRev but not in Azure Boards, the comment will be created in Azure Boards on behalf of the user who established the connection.
* Threaded comments created in DevRev are not synced to Azure Boards, as Azure Boards does not support threaded or hierarchical comments. Syncing them as flat comments would lose context and may cause confusion.

## Post import options

After a successful import, you have the following options available for the imported account:

* **Sync to DevRev**

  This option allows you to synchronize any modifications made in Azure Boards with the corresponding items previously imported into DevRev. It also creates new items in DevRev for any new work items in Azure Boards after the last sync or import.
* **View Report**

  This option allows you to access detailed information about the initial import and any subsequent syncs performed.
* **Delete Import**

  If you want to remove the import and all items that were imported from Azure Boards into DevRev, you can use this option.
* **Edit Connection**

  Use this option to change the connection used for any subsequent actions. It can be helpful if a connection becomes inactive or the user who established it is no longer available.

### Sync to DevRev

After a successful import from an Azure Boards account, you can choose to sync the imported data with DevRev. This feature syncs any new work items and users, and any changes made to previously imported items from Azure Boards.

To perform a one-time sync to DevRev, follow these steps:

1. Go to **Settings > Integrations > Airsync**.
2. Locate the previously imported project.
3. Select the **⋮** > **Sync Azure Boards to DevRev** option.

> ⚠️ A one-time sync may overwrite fields in previously imported items, even if they were modified in DevRev.

### Historical imports

To view currently running and previous imports from various sources, do the following:

1. Go to **Settings > Integrations > Airsync**.
2. Select the import you want to view.
3. Click on the context menu (⋮) and select **View Report**.

### Periodic sync

After successfully importing to DevRev, you have the option to enable a periodic sync. This allows for automatic synchronization with DevRev on a regular basis.

To configure periodic sync, follow these steps:

1. Go to **Settings > Integrations > Airsync**.
2. Locate the imported project.
3. Click on **⋮** > **Set Periodic Sync**.

You'll see three periodic sync options:

* **Azure Boards → DevRev**

  Enable this option to sync data from Azure Boards into DevRev.
* **DevRev → Azure Boards**

  Data from DevRev will be synced to Azure Boards.
* **Automation Option**

  Enable automation to trigger webhooks, Snap-ins, and DevRev-native events for synced items. If disabled, periodic syncs will **not** trigger any events or automations.

Select the frequency:

1. Enter a number (e.g., 1, 2, 3) in the Repeat every box.
2. Choose a time unit (Hours, Days, Weeks, or Months) from the dropdown.
3. Click **Schedule** to activate periodic sync.

### Delete import

> ⚠️ This deletes any content created by the import, including users and [[entities/article|articles]].

An import and all the content it creates can be deleted from DevRev. This can be useful when running POCs or to change the configuration used during the import. Once an import has been deleted, all the content it created gets deleted, even if they were modified in DevRev. It's possible to import the project again after its deletion.

To delete an import and all the content it created, go to **Settings > Integrations > Airsync**, find the previously imported project, and select **⋮** > **Delete Import**.

### Mark a DevRev Work Item for Syncing

Using the Sync from DevRev to Azure Boards feature, it's possible to sync DevRev work items to Azure Boards projects that have been imported to DevRev. In order to sync a DevRev work item to Azure Boards, it must be marked for syncing. Marking a DevRev work item for syncing can be done during the creation of a work item. During work creation, open the dropdown Select Subtype, set it to the Azure Boards project, and type the work item that should be synced. The display format is as follows: `{Azure Boards project name} / {type}`. For example, if you want to sync to a Bug to a Azure Boards project called Maple, this would show as Maple / Bug.

## Related wiki nodes
- [[glossary/airsync]]

## Source
- DevRev support [[entities/article|article]] [Azure Boards AirSync](https://support.devrev.ai/en-US/devrev/article/pIFPpCr4) (ART-22017)
