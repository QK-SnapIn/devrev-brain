---
title: Intercom AirSync
devrev_id: ART-22006
parent_directory: AirSync
translation_group: PkxZOkjf
modified_date: "2026-02-16T12:07:29.84Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/PkxZOkjf"
tags: []
top_category: Computer by DevRev
wiki_match: glossary/airsync
match_score: 0.85
last_updated: 2026-05-11
related: ['glossary/airsync']
summary: "The Intercom AirSync simplifies migration from Intercom to DevRev, supporting both one-time imports and ongoing syncs."
---

# Intercom AirSync

The Intercom [[glossary/airsync|AirSync]] simplifies migration from Intercom to DevRev, supporting both one-time imports and ongoing syncs.

# Supported objects

The following is a list of Intercom objects and their corresponding DevRev equivalents. Those marked as **Sync to DevRev** are eligible for import from Intercom to DevRev.

| Intercom Object | DevRev Object | Sync to DevRev |
| --- | --- | --- |
| [[features/conversations-feature|Conversations]] | Conversations | ✅ |
| [[entities/conversation|Conversation]] [[features/parts|Parts]] (comments) | Conversation comments | ✅ |
| Tags | Tags | ✅ |
| Attachment in conversation/comments | Attachment in conversation/comments | ✅ |
| Admins | DevUser | ✅ |
| Companies | [[features/accounts|Accounts]] | ✅ |
| Contacts | Contacts | ✅ |
| Collections | Collections | ✅ |
| [[entities/article|Articles]] | Articles | ✅ |
| Attachment in Articles | Attachment in Articles | ❌ |

## Import from Intercom

1. Log in to DevRev.
2. Go to **Settings** and [[features/search|search]] for **Integrations**.
3. In the snap-in config, click on **All Snap-ins**, search for **Intercom AirSync Snap-in**, and click **Add**. The snap-in configuration component will be displayed.
4. Do the following:

   **4a**. In the snap-in config, **Enable** the toggle to **Import all conversations**, as per requirement:

   * **Enable**: Imports both **open and closed conversations**.
   * **Disable**: Imports only **closed conversations**.

   Helps maintain a **complete history** of customer interactions.

   **4b**. Configure the **External Reference as a Custom Field in Intercom** toggle:

   Used to map Intercom contacts to DevRev contacts.

   * **Enable**: Use a custom field from Intercom (e.g., `phone_user_id`). Enter the custom field name in the required field **Reference Field Name**. This field will be used as the **external reference ID** in DevRev.
   * **Disable**: Intercom's `user_id` will be used as the external reference ID.

   **4c**. Click on save to apply the configuration settings.
5. Click **Install Snap-in**.
6. Go to **Airsync** from the left navigation in your settings.
7. Click **Airsync** in the top-right corner and select the **Intercom AirSync Snap-in** logo.
8. Create a new connection to your **Intercom** [[entities/account|account]], or use an existing active connection if you already have one.

### **Choose a Connection Type**

There are two types of connections. You can choose either one to authenticate with your Intercom workspace:

**Option 1: Intercom API Key Connection**

* To get the API key, in intercom click on Settings in left nav search for Integration > **Intercom Developer Hub**.
* Select the workspace you want to import from.
* Go to the **Authentication** tab.
* Copy the API token and paste it into the **API Key** field in the DevRev connection setup.

**Option 2: Intercom OAuth Connection**

* Give a name to connection and Click on Sign-in.
* You will be redirected to Intercom to authorize access to your workspace. Select the workspace from the top right dropdown and click on authorize access.

8. After successfully creating the connection. Click **Airsync** in the top-right corner and select the created connection.

### Sync Units

A list of sync units will be displayed. Select the sync unit as per required and **DevRev [[entities/part|part]]** that should be used for any imported work. *(Future releases will enhance this functionality.)* This initiates a **bulk import** of the selected sync unit.

* `[org_name] Article & Collections`: Imports only **articles and collections**.
* `[org_name] Recent 3 Months All Entities`: Imports **all entities** (users, contacts, accounts, conversations, tags, attachments, comments, articles, and collections) from the **last 3 months**.
* `[org_name] Recent 3 Months Conversation & Contacts`: Imports only **conversations and contacts** from the **last 3 months**.
* `[org_name] Recent 6 Months All Entities`: Imports **all entities** from the **last 6 months**.
* `[org_name] Recent 6 Months Conversation & Contacts`: Imports only **conversations and contacts** from the **last 6 months**.

The duration of the import depends on the size of the Intercom conversations and the data being imported. It can take seconds for an account with only a few dozen conversations or a few hours for an account with tens of thousands of conversations and many attachments. DevRev honors the Intercom API rate limits and automatically handles back-off and resumption.

## Post import options

After a successful import, you have the following options available for the imported account:

* **Sync to DevRev**

  This option allows you to synchronize any modifications made in Intercom with the corresponding items previously imported into DevRev. It also creates new items in DevRev for any new modification in items of Intercom after the last sync or import.
* **View Report**

  This option allows you to access detailed information about the initial import and any subsequent syncs performed.
* **Delete Import**

  If you wish to remove the import and all items that were imported from Intercom into DevRev, you can use this option.
* **Edit Connection**

  Use this option to change the connection used for any subsequent actions. It can be helpful if a connection becomes inactive or the user who established it is no longer available.

### Sync to DevRev

After a successful import from an Intercom account, you can choose to sync the imported data with DevRev. This feature imports any new data and applies any changes made to previously imported items from Intercom.

To perform a one-time sync to DevRev, follow these steps:

1. Go to **Settings > Integrations > Airsync**.
2. Locate the imported project.
3. Click on **⋮**.
4. Select the **Sync Intercom to DevRev** option.

> ⚠️ A one-time and periodic sync may overwrite fields in previously imported items, even if they were modified in DevRev.

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
3. Click **⋮** > **Set Periodic Sync**.

You'll see three periodic sync options:

* **Intercom → DevRev**

  Enable this option to sync data from Intercom into DevRev.
* **DevRev → Intercom**

  *Note: Syncing from DevRev to Intercom is currently not supported.*
* **Automation Option**

  Enable automation to trigger webhooks, Snap-ins, and DevRev-native events for synced items. If disabled, periodic syncs will **not** trigger any events or automations.

Select the frequency:

1. Enter a number (e.g., 1, 2, 3) in the Repeat every box.
2. Choose a time unit (Hours, Days, Weeks, or Months) from the dropdown.
3. Click **Schedule** to activate periodic sync.

### Delete import

> ⚠️ This deletes all content created by the import.

An import and all the content it creates can be deleted from DevRev. This can be useful when running POCs or to change the configuration used during the import. Once an import has been deleted, all the content it created gets deleted, even if they were modified in DevRev. It's possible to import the project again after its deletion.

To delete an import and all the content it created, go to **Settings > Integrations > Airsync**, find the imported sync, and select **⋮** > **Delete**.

## Related wiki nodes
- [[glossary/airsync]]

## Source
- DevRev support [[entities/article|article]] [Intercom AirSync](https://support.devrev.ai/en-US/devrev/article/PkxZOkjf) (ART-22006)
