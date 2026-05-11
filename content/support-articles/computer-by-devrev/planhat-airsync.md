---
title: Planhat AirSync
devrev_id: ART-22022
parent_directory: AirSync
translation_group: xQ3SygZ-
modified_date: "2026-03-23T12:54:44.425Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/xQ3SygZ-"
tags: []
top_category: Computer by DevRev
wiki_match: glossary/airsync
match_score: 0.85
last_updated: 2026-05-11
related: ['glossary/airsync']
---

# Planhat AirSync

The PlanHat AirSync simplifies migration from PlanHat to DevRev, supporting both one-time imports and periodic sync.

### Supported objects

The following is a list of PlanHat objects and their corresponding DevRev equivalents. Those marked as **Sync to DevRev** are eligible for import from PlanHat to DevRev.

| PlanHat object | DevRev object | Sync to DevRev | Sync to PlanHat |
| --- | --- | --- | --- |
| User | DevUser | ✅ | ❌ |
| Company | Account | ✅ | ❌ |
| EndUser | Contact | ✅ | ❌ |
| Comments | Comments | ✅ | ❌ |
| Licenses | Custom Object | ✅ | ✅ |
| Task | Conversation | ✅ | ❌ |
| Conversation | Conversations | ✅ | ❌ |
| Conversation.Ticket | Ticket | ✅ | ✅ |
| Conversation.Chat | DM | ❌ | ❌ |
| Conversation.Meeting | Custom Object | ✅ | ✅ |
| ProductUsage | Custom field in Account | ✅ | ❌ |

### Importing from PlanHat

1. Log in to DevRev.
2. Navigate to [**Settings > Integrations > Snap-ins**](https://app.devrev.ai/?setting=snap-ins), search for **PlanHat** under **All Snap-ins**.
3. Click **Add and Install Snap-in**.
4. Navigate to [**Settings > Integrations > AirSync**](https://app.devrev.ai/?setting=airsyncs) in the left-navigation.
5. Click AirSync in the top right corner and select **PlanHat**.
6. Create a new connection to authenticate with your PlanHat workspace, or use an existing active connection.

   * To create a PlanHat connection, provide a name to the connection. In the **Subdomain** field, enter your PlanHat domain, which can be found in the PlanHat browser URL. For example, from `https://app.planhat.com/`, `app.planhat.com` is the Subdomain. Then enter your token.

**Note**: Ensure that the token has full access with the following permissions: **Portfolio:** Full access. **Data Module:** Company (View), End Users (View), Conversations (View, Create, Update), Tasks (View), Licenses (View, Create, Update), Users (View), Custom Fields (View, Create, Update), Comments (View, Create, Update).

7. On the next screen, select the authenticated PlanHat workspace.
8. Specify the DevRev part where the imported content should reside. Click on **Start**. This initiates a bulk import of the selected workspace.

The duration of the import depends on the size of the PlanHat workspace and the data being imported. It can take minutes to hours based on data size.

## Limitations

* PlanHat does not support OAuth for API authentication.
* Conversation-level or comment-level attachments are not supported.
* User roles and permissions are not supported.
* Reverse sync is only supported for tickets and custom objects.
* Tags are not supported.
* When creating a custom object (e.g., License) in DevRev during reverse sync, the CompanyId, FromDate & ToDate are required.
* In incremental sync, all data is extracted first and then filtered, which can cause the sync process to take longer than expected.
* Conversation type changes are not supported during Incremental Sync, which may result in duplicate data and missing comments.

## Post import options

After a successful import, you have the following options available for the imported account:

* **Sync to DevRev**

  This option allows you to synchronize any modifications made in PlanHat with the corresponding items previously imported into DevRev. It also creates new items in DevRev for any data in PlanHat after the last sync or import.
* **View Report**

  This option allows you to access detailed information about the initial import and any subsequent syncs performed.
* **Delete Import**

  If you want to remove the import and all data that were imported from PlanHat into DevRev, you can use this option.
* **Edit Connection**

  Use this option to change the connection used for any subsequent actions. It can be helpful if a connection becomes inactive or the user who established it is no longer available.

### Sync to DevRev

After a successful import from PlanHat, you can choose to sync the imported data with DevRev. This feature imports any company, users, and any changes made to previously imported items from PlanHat.

To perform a one-time sync to DevRev, follow these steps:

1. Go to **Settings > Integrations > Airdrops**.
2. Locate the previously imported project.
3. Select the **⋮** > **Sync PlanHat to DevRev** option.

To perform a reverse sync from DevRev to PlanHat, follow these steps:

1. Go to **Settings > Integrations > Airdrops**.
2. Locate the previously imported project.
3. Select the **⋮** > **Sync DevRev to PlanHat** option.

> A one-time sync may overwrite fields in previously imported items, even if they were modified in DevRev.

### Historical imports

To view currently running and previous imports from various sources, do the following:

1. Go to **Settings > Integrations > Airdrops**.
2. Select the import you want to view.
3. Click on the context menu (⋮) and select **View Report**.

### Periodic sync

After successfully importing to DevRev, you have the option to enable a periodic sync. This allows for automatic synchronization with DevRev on a regular basis. By default, the sync occurs once an hour.

To configure periodic sync, follow these steps:

1. Go to **Settings > Integrations > Airdrops**.
2. Locate the previously imported project.
3. Select the **⋮** > **Set Periodic Sync** option.

You'll see periodic sync options:

* **PlanHat → DevRev**: Enable this option to sync data from PlanHat into DevRev.
* **DevRev → PlanHat**: Enable this option for reverse sync to PlanHat (only supported for tickets and custom objects).

The Enable automation for synced items setting is optional and can be activated during periodic sync configuration. When enabled, newly created or updated items trigger events, which can initiate webhooks, notifications, snap-ins, and other processes, as if the events originated directly in DevRev.

If this setting is turned off, updates do not trigger any event-driven processes. This behavior applies only to periodic syncs; no events are triggered during a first-time import or manual sync to or from DevRev.

### Delete import

> This deletes any content created by the import, including users, accounts, contacts, and conversations.

An import and all the content it creates can be deleted from DevRev. This can be useful when running POCs or to change the configuration used during the import. Once an import has been deleted, all the content it created gets deleted, even if they were modified in DevRev. It's possible to import the project again after its deletion.

To delete an import and all the content it created, go to **Settings > Integrations > Airdrops**, find the previously imported project, and select **⋮** > **Delete Import**.

## Related wiki nodes
- [[glossary/airsync]]

## Source
- DevRev support article [Planhat AirSync](https://support.devrev.ai/en-US/devrev/article/xQ3SygZ-) (ART-22022)
