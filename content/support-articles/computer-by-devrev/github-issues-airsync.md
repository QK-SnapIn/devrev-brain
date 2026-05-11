---
title: GitHub Issues AirSync
devrev_id: ART-22020
parent_directory: AirSync
translation_group: 3VLgFAmj
modified_date: "2025-12-10T06:58:05.112Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/3VLgFAmj"
tags: []
top_category: Computer by DevRev
wiki_match: entities/issue
match_score: 0.85
last_updated: 2026-05-11
related: ['entities/issue']
---

# GitHub Issues AirSync

To ease the transition from GitHub to DevRev, you can import and sync GitHub issues & Markdown files with DevRev.

### Supported objects

|  |  |  |  |
| --- | --- | --- | --- |
| GitHub Object | DevRev Object | Sync to DevRev | Sync to GitHub |
| Issue | Issue | ✅ | ✅ |
| Comment on Issue | Comment on Issue | ✅ | ✅ |
| Label on Issue | Tag on Issue | ✅ | ✅ |
| Attachment on Issue | Attachment on Issue | ❌ | ❌ |
| User | DevUser | ✅ | ❌ |
| Project | Enhancement | ❌ | ❌ |
| Markdown File | Article | ✅ | ❌ |
| Folder | Collection | ✅ | ❌ |

### Import from GitHub

DevRev highly recommends creating a new dedicated GitHub account when setting up GitHub for 2-way sync. All issues and comments created in GitHub will be created using this account.

1. Create a [GitHub PAT token classic](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens) using the account that will be used to set up AirSync.

   The minimum required permissions are "Repo" and "User".

   The GitHub user associated with the PAT must have at least **write** permission to the repositories being imported.
2. Go to [**Settings** > **Integrations** > **Snap-ins**](https://app.devrev.ai/?setting=snap-ins) and install **GitHub AirSync**.
3. Configure the GitHub AirSync snap-in. Follow these steps to complete the installation:

   1. **Open the configuration modal**.
      After selecting **Configure**, a modal will appear prompting you to configure the snap-in settings for your organization.
   2. **Enable Sync Options**.Toggle the following options based on your needs:

      * **Sync Issues**: Import GitHub issues into DevRev.
      * **Sync Markdown files**: Import Markdown files from the selected GitHub branch.
      * **Sync Permissions**: Import repository permissions from GitHub, which will be applied to the Markdown files.

        If enabled, the permissions from GitHub will be applied to the files. If disabled, the imported files will be shared with the DevRev organization.
   3. **Select a Branch**.
      Use the **Select Branch** dropdown to choose between `main` or `master` — the branch from which Markdown files will be fetched.

      This is a required step and determines the source of the Markdown content.
   4. **Click Save**.Once all settings are configured, click **Save** to complete the setup.
4. Go to [**Settings** > **Integrations** > **AirSyncs**](https://app.devrev.ai/?setting=airsyncs) and click **Start AirSync** or **AirSync**.
5. Select **GitHub** under the **Snap-ins** tab.

   * If this isn't available, install the Snap-in as described in step 2.
6. Create a connection by providing the GitHub PAT token and the GitHub organization name in the **subdomain field** when creating a new connection.
7. Choose the repository you want to import.
8. After the extraction is completed, a recipe is presented where you select what data to import and how to map it. The recommended values are preselected.

### Historical AirSyncs

To view currently running and previous AirSyncs from various sources, do the following:

1. Go to [**Settings** > **Integrations** > **AirSyncs**](https://app.devrev.ai/?setting=airsyncs).
2. Select the import you want to view.
3. Select the context menu (⋮) > **View Report**.

### Periodic sync

After successfully importing to DevRev, you have the option to enable a periodic sync. This allows for automatic synchronization with DevRev on a regular basis. By default, the sync occurs once an hour.

To configure periodic sync, follow these steps:

1. Go to [**Settings** > **Integrations** > **AirSyncs**](https://app.devrev.ai/?setting=airsyncs).
2. Locate the previously imported project.
3. Select the ⋮ > **Set Periodic Sync** option.

The **Enable automations for synced items** setting is optional and can be activated during periodic sync configuration. When enabled, newly created or updated items trigger events, which can initiate webhooks, notifications, Snap-ins, and other processes, as if the events originated directly in DevRev.

If this setting is disabled, updates will not trigger any event-driven processes. This behavior applies only to periodic syncs; no events are triggered during a first-time import or manual sync to or from DevRev.

### Delete import

This deletes any content created by the import, including users and works.

An import and all the content it creates can be deleted from DevRev. This can be useful when running POCs or to change the recipe used during the import. Once an import has been deleted, all the content it created gets deleted, even if they were modified in DevRev. It's possible to import the project again after its deletion.

To delete an import and all the content it created, go to [**Settings** > **Integrations** > **AirSyncs**](https://app.devrev.ai/?setting=airsyncs), find the previously imported project, and select ⋮ > **Delete Import**.

## Related wiki nodes
- [[entities/issue]]

## Source
- DevRev support article [GitHub Issues AirSync](https://support.devrev.ai/en-US/devrev/article/3VLgFAmj) (ART-22020)
