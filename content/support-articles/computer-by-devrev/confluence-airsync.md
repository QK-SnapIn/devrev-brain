---
title: Confluence AirSync
devrev_id: ART-22482
parent_directory: AirSync
translation_group: 4VufOIBg
modified_date: "2026-04-29T07:15:02.395Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/4VufOIBg"
tags: []
top_category: Computer by DevRev
wiki_match: glossary/airsync
match_score: 0.85
last_updated: 2026-05-11
related: ['glossary/airsync']
summary: "The Confluence AirSync snap-in simplifies migration from Confluence to DevRev, supporting both one-time imports and ongoing syncs."
---

# Confluence AirSync

The Confluence [[glossary/airsync|AirSync]] snap-in simplifies migration from Confluence to DevRev, supporting both one-time imports and ongoing syncs.

Confluence AirSync is a tool that lets you migrate your team's [[features/knowledge-base|knowledge base]] from Confluence into DevRev. It allows you to:

* Transfer your pages, blogs, and content
* Keep your content organizational structure intact
* Bring over important file attachments
* Maintain user associations and relationships

Use the Confluence AirSync if you need to:

* Import pages, blogs, and knowledge base [[entities/article|articles]] from Confluence into DevRev
* Import spaces and their contents as per user requirements
* Maintain user identities and relationships between platforms
* Preserve organizational structures and hierarchies

## Supported objects

The following is a list of Confluence objects and their corresponding DevRev equivalents. Those marked as **Sync to DevRev** are eligible for import from Confluence to DevRev.

| Confluence Object | DevRev Object | Sync to DevRev |
| --- | --- | --- |
| Pages | Articles | ✅ |
| Blogs | Articles | ✅ |
| Users | Users | ✅ |
| Attachments | [[features/artifacts|Artifacts]] on [[entities/article|Article]] | ✅ |
| Folders | Directories | ✅ |

## First time import overview

When using Confluence AirSync for the first time:

1. **Preparation**: Ensure you have appropriate access to your Confluence [[entities/account|account]] and choose your preferred authentication method (OAuth, Scoped Token, or Classic Token).
2. **Installation and Setup**: Follow the steps in the `Importing from Confluence` section below.
3. **Connection Process**: Authenticate using one of the three supported methods to establish a secure connection between Confluence and DevRev.
4. **Selection Process**: You'll have the [[glossary/opportunity|opportunity]] to choose specific Confluence spaces to import, allowing you to be selective about what data moves to DevRev.
5. **Processing Time**: The import duration depends on the volume of data. Small spaces might complete in seconds, while larger spaces with thousands of pages and attachments may take hours.
6. **Results and Verification**: After completion, review the import report to confirm that all pages, blogs, users, and attachments were properly transferred.

> Syncing from Confluence to DevRev is one-way only. Changes made in DevRev won't reflect back in Confluence, and syncing may overwrite DevRev customizations with Confluence data.

## Importing from Confluence

1. Log in to DevRev.
2. Navigate to **Settings > Integrations > Snap-ins**, [[features/search|search]] for **Confluence** under **All Snap-ins**.
3. Open the snap-in and click the **Add** button located in the top-right corner.
4. Click **Install**.
5. Once installed, click on **Config** to configure the snap-in settings. See `Snap-in configuration` for details on the available options.
6. Go to the **AirSyncs** option under **Integrations**.
7. Click the **AirSync** button and select **Confluence**.
8. Click **Add Connection**, enter a connection name, and select your preferred authentication method. See `Set up Confluence connection` for details on each method.
9. After the connection is successfully established, select it to view a list of Confluence spaces.
10. Choose the spaces and the corresponding **DevRev [[entities/part|part]]** for import, then start the extraction.
11. DevRev makes an effort to automatically map the fields from Confluence to the corresponding fields in DevRev. Review the pre-configured field mappings and click **Next** to proceed through each step until the mapping process is complete. You may be prompted to manually map certain fields if needed.
12. The extraction will begin, and after some time, the import will be completed.
13. Click on the completed import to view a detailed report, including imported **Users**, **Pages**, **Blogs**, and **Attachments**.

> Import duration varies from minutes to hours based on data size. Small spaces might complete in seconds, while larger spaces with thousands of pages and attachments may take hours.

## Set up Confluence connection

Confluence AirSync supports three authentication methods to connect your Confluence workspace with DevRev:

| Method | Description | Best for |
| --- | --- | --- |
| **OAuth** | Authenticate via Atlassian's OAuth 2.0 flow with granular scopes | Organizations that prefer delegated authorization and token auto-refresh |
| **Scoped Token** | Use a fine-grained API token with specific permission scopes | Teams that need precise control over API permissions |
| **Classic Token** | Use a Personal Access Token (PAT) generated from your Atlassian account | Quick setup with broad account-level access |

### Required scopes (OAuth and Scoped Token)

Both OAuth and Scoped Token authentication require the following Confluence scopes:

* `read:content-details:confluence`
* `read:space:confluence`
* `read:space.permission:confluence`
* `read:page:confluence`
* `read:attachment:confluence`
* `read:user:confluence`
* `read:group:confluence`
* `readonly:content.attachment:confluence`
* `offline_access`

### Option 1: OAuth authentication

OAuth allows you to authenticate through Atlassian's standard OAuth 2.0 authorization flow. DevRev will request only the scopes listed above, ensuring minimal and well-defined access to your Confluence data.

When selecting **OAuth** as the authentication method in step 8 of the `import process`:

1. You will be redirected to Atlassian's authorization page.
2. Review the requested scopes and authorize DevRev.
3. After authorization, the connection is established and you can proceed with the import.

### Option 2: Scoped Token authentication

Scoped tokens provide fine-grained API access with the same permission scopes as OAuth, but are managed manually via your Atlassian account settings.

Create a Scoped Token

1. Go to your [Atlassian Account API Tokens](https://id.atlassian.com/manage-profile/security/api-tokens) page.
2. Select the option to create a new token with scopes.
3. Enter a name for the token based on its intended purpose.
4. Set the token expiration (between 1 and 365 days).
5. Select **Confluence** as the app.
6. Select the required scopes listed in the [Required scopes](https://#required-scopes-oauth-and-scoped-token) section above.
7. Click **Create** to generate the token.
8. Copy the generated token immediately. The token cannot be recovered after this step.

> Store this token securely. It will be required while creating the Confluence connection in DevRev.

When selecting **Scoped Token** as the authentication method in step 8 of the `import process`, enter the following details:

* **Connection Name**
* **Email**: Enter the email used in your Confluence account
* **Subdomain**: Enter only the domain part from your Confluence URL (e.g., `yourdomain.atlassian.net`)
* **Scoped Token**: Enter the token generated above

### Option 3: Classic Token (PAT) authentication

Classic tokens use a Personal Access Token (PAT) generated from your Atlassian account. This method provides broad account-level access and is the simplest way to get started.

Create a Personal Access Token

1. Go to your [Atlassian Account API Tokens](https://id.atlassian.com/manage-profile/security/api-tokens) page.
2. Navigate to **Security** > **API tokens**.
3. Click **Create API token**.
4. Enter a label for your token and click **Create**.
5. Copy the generated token.

> This token will be required while creating the Confluence connection in DevRev.

When selecting **Classic Token (PAT)** as the authentication method in step 8 of the `import process`, enter the following details:

* **Connection Name**
* **Email**: Enter the email used in your Confluence account
* **Subdomain**: Enter only the domain part from your Confluence URL (e.g., `yourdomain.atlassian.net`)
* **PAT Token**: Enter your Personal Access Token

## Email visibility

To successfully import users and their associated articles, you must set email visibility to **Anyone** in your Confluence account settings. This is required for both Scoped Token and Classic Token authentication methods. Without this setting, user associations and [[features/identity|identity]] mapping may fail.

To set email visibility:

1. Navigate to your [Atlassian Account Settings](https://id.atlassian.com/manage-profile/profile-and-visibility).
2. In the left-hand menu, select **Profile and Visibility**.
3. Scroll down to the **Contact** section.
4. Locate the **Email** field and set its visibility to **Anyone**.

## Snap-in configuration

After installing the Confluence AirSync snap-in, the following configuration options are available under **Config**. These settings control how imported content is handled in DevRev.

| Option | Description |
| --- | --- |
| **Article Visibility** | Enabling this toggle will make the imported articles accessible to all the [[entities/dev-user|dev users]] in your organization. If disabled, the original Confluence permissions will be preserved. |
| **Import as External** | Import all Confluence pages with external scope. This is generally intended only for PLuG-related use cases. |
| **Allow External Hyperlinks In Article Content** | Allow external hyperlinks in article content. When disabled, only internal DevRev links (devrev.ai) are preserved as clickable hyperlinks; all other external URLs will be rendered as plain text. |

## Post import options

After a successful import, you have the following options available for the imported space:

* **Sync to DevRev** -- This option allows you to synchronize any modifications made in Confluence with the corresponding items previously imported into DevRev. It also creates new items in DevRev for any new content in Confluence after the last sync or import.
* **View Report** -- This option allows you to access detailed information about the initial import and any subsequent syncs performed.
* **Delete Import** -- If you wish to remove the import and all items that were imported from Confluence into DevRev, you can use this option.
* **Edit Connection** -- Use this option to change the connection used for any subsequent actions. It can be helpful if a connection becomes inactive or the user who established it is no longer available.

### Sync to DevRev

After a successful import from a Confluence space, you can choose to sync the imported data with DevRev. This feature syncs any new pages, blogs, attachments, users, and any changes made to previously imported items from Confluence.

To perform a one-time sync to DevRev, follow these steps:

1. Go to **Settings > Integrations > Airsync**.
2. Locate the previously imported space.
3. Select the **...** > **Sync Confluence to DevRev** option.

> A one-time sync may overwrite fields in previously imported items, even if they were modified in DevRev.

### Historical imports

To view currently running and previous imports from various sources, do the following:

1. Go to **Settings > Integrations > Airsync**.
2. Select the import you want to view.
3. Click on the context menu (...) and select **View Report**.

### Periodic sync

After successfully importing to DevRev, you have the option to enable a periodic sync. This allows for automatic synchronization with DevRev on a regular basis. By default, the sync occurs once an hour.

To configure periodic sync, follow these steps:

1. Go to **Settings > Integrations > Airsync**.
2. Locate the previously imported space.
3. Select the **...** > **Set Periodic Sync** option.

The Enable automation for synced items setting is optional and can be activated during periodic sync configuration. When enabled, newly created or updated items trigger events, which can initiate webhooks, notifications, Snap-ins, and other processes, as if the events originated directly in DevRev.

If this setting is disabled, updates will not trigger any event-driven processes. This behavior applies only to periodic syncs; no events are triggered during a first-time import or manual sync to or from DevRev.

### Delete import

> This deletes any content created by the import, including users, pages, blogs, and articles.

An import and all the content it creates can be deleted from DevRev. This can be useful when running POCs or to change the configuration used during the import. Once an import has been deleted, all the content it created gets deleted, even if they were modified in DevRev. It's possible to import the space again after its deletion.

To delete an import and all the content it created, go to **Settings > Integrations > Airsync**, find the previously imported space, and select **... > Delete Import**.

## Limitations

While Confluence AirSync supports importing a wide range of content and metadata, the following are not imported or supported:

* Comments on pages and blogs
* Page reactions (likes or other emoji responses)
* Inline attachments indexing
* Table sorting -- tables imported from Confluence will appear as static content and cannot be sorted within DevRev
* Shared public Confluence links -- any publicly shared Confluence links cannot be tracked or mapped; no user or content association will be pulled from such links

These limitations exist due to differences in feature support between Confluence and DevRev.

## Related wiki nodes
- [[glossary/airsync]]

## Source
- DevRev support article [Confluence AirSync](https://support.devrev.ai/en-US/devrev/article/4VufOIBg) (ART-22482)
