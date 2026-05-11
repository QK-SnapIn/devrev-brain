---
title: Document360 AirSync
devrev_id: ART-27324
parent_directory: AirSync
translation_group: jgJymbfI
modified_date: "2026-03-27T05:36:37.796Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/jgJymbfI"
tags: []
top_category: Computer by DevRev
wiki_match: glossary/airsync
match_score: 0.85
last_updated: 2026-05-11
related: ['glossary/airsync']
---

# Document360 AirSync

# Document360 AirSync

Document360 AirSync enables migration from Document360 to DevRev, including one-time imports and ongoing syncs.

### Supported objects

The table below lists Document360 object types and their DevRev equivalents. Objects marked **Sync to DevRev** may be imported from Document360 into DevRev.

| Document360 object | DevRev object | Sync to DevRev |
| --- | --- | --- |
| Article | Article | ✅ |
| Category | Directory | ✅ |
| Category page | Article | ✅ |
| Team account (user) | DevUser | ✅ |
| Permission group | Group | ✅ |

**Permission groups.** Document360 and DevRev groups are not mapped one-to-one. Document360 does not provide permission-group entities for direct import. AirSync derives access from **team users**, then creates **static** DevRev groups (with associated membership) so articles can be shared in DevRev. Each group name is prefixed with `DOC360__` and corresponds to scope in this order: **project → version → language → category**. User groups defined under **Teams** in Document360 are not imported as separate DevRev groups; access is represented solely through this derived static-group model.

### Disclaimer — Article sharing and category access

> **Permissions:** When an article in Document360 is shared with specific users or groups, AirSync may grant those principals access to the **entire parent category (directory)** in DevRev, not to that article alone. The Document360 API does not expose article-level permissions in a form that supports a more granular mapping in DevRev. Plan DevRev permissions accordingly.

### Configurations

In the Document360 AirSync flow, use the **Configurations** tab (or equivalent configuration step) to set the following **before** completing connection setup and import:

* **Region** — Select **Global**, **EU**, or **US** to target the Document360 data region where the account is hosted. This value must align with the Document360 workspace region.
* **Allow External Hyperlinks In Article Content** — With this option **enabled**, external URLs in article and category page content remain clickable in DevRev. With it **disabled**, only DevRev URLs (for example `devrev.ai`) remain clickable; all other external URLs are rendered as plain text.

### Importing from Document360

1. Sign in to DevRev.
2. Go to **Settings > Integrations > Snap-ins**, locate **Document360** under **All Snap-ins**.
3. Select **Add and Install Snap-in**.
4. Open **Settings > Integrations > Airsync** from the left navigation.
5. Select **Airsync** in the upper-right corner, then choose **Document360**.
6. On the **Configurations** tab, configure **Region** and **Allow External Hyperlinks In Article Content** as described in **Configurations** above. Create a new connection with your Document360 **API token** and workspace details, or select an existing active connection.

> The API token must be authorized for the project versions to be imported. Tokens with insufficient permissions may result in partial import failures (users, groups, or content).

7. After the connection is active, select the Document360 **project version** (knowledge base version) to import and specify the DevRev **part** for imported work. This starts a bulk import of the selected version.
8. Field mapping from Document360 to DevRev is performed automatically where possible. Manual mapping may be required for certain fields.

### Supported content file types

* Knowledge base articles delivered as **rich text (HTML)** (including content produced in Document360’s Markdown, WYSIWYG, and block editors).
* **Attachments** linked from article and category page content (for example images, PDFs, and Microsoft Office documents), subject to size limits described under **Limitations**.

## Limitations

* Only **forward sync** supported. (Document360 → DevRev): changes in DevRev are not written back to Document360. Imported articles are **read-only** in DevRev for all users **except** article owners.
* **Languages.** AirSync imports content only for locales that DevRev supports. Additional languages configured in Document360 are omitted from extraction. What can be imported per locale is also bounded by the Document360 APIs in use. Supported languages and **BCP 47** identifiers are:

| Language | BCP 47 |
| --- | --- |
| English (United States) | `en-US` |
| Spanish | `es-ES` |
| Japanese | `ja-JP` |
| Dutch | `nl-NL` |
| Portuguese (Brazil) | `pt-BR` |
| Chinese (Simplified) | `zh-CN` |
| Chinese (Traditional) | `zh-TW` |
| French | `fr-FR` |
| German | `de-DE` |
| Hindi | `hi-IN` |
| Portuguese | `pt-PT` |
| Spanish (Argentina) | `es-AR` |
| Slovene | `sl-SI` |

* **Article status.** Under current Document360 API constraints, only **Draft** and **Published** statuses are supported. All other statuses are unsupported for sync.
* **Article settings.** Attributes such as **deprecated** state in Document360 are **not** synchronized to DevRev via AirSync.
* **Article metadata.** Changes to metadata (for example **description** or **moving an article to a different category**) appear in DevRev only when the article **body content** is updated as well, owing to Document360 API constraints.
* Attachments larger than **250 MB** are not imported.
* Deleting articles, categories, or related content in Document360 does **not** automatically delete the corresponding records in DevRev.

## Post import options

After a successful import, you have the following options available for the imported data:

* **Sync to DevRev**

  This option allows you to synchronize any modifications made in Document360 with the corresponding items previously imported into DevRev. It also creates new items in DevRev for any document in Document360 after the last sync or import.
* **View Report**

  This option allows you to access detailed information about the initial import and any subsequent syncs performed.
* **Delete Import**

  If you want to remove the import and all data that were imported from Document360 into DevRev, you can use this option.
* **Edit Connection**

  Use this option to change the connection used for any subsequent actions. It can be helpful if a connection becomes inactive or the user who established it is no longer available.

### Sync to DevRev

After a successful import from Document360, you can choose to sync the imported data with DevRev. This feature imports any files and users, and any changes made to previously imported items from Document360.

To perform a one-time sync to DevRev, follow these steps:

1. Go to **Settings > Integrations > Airsync**.
2. Locate the previously imported project.
3. Select the **⋮** > **Sync Document360 to DevRev** option.

> A one-time sync may overwrite fields in previously imported items, even if they were modified in DevRev.

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

The Enable automation for synced items setting is optional and can be activated during periodic sync configuration. When enabled, newly created or updated items trigger events, which can initiate webhooks, notifications, snap-ins, and other processes, as if the events originated directly in DevRev.

If this setting is turned off, updates do not trigger any event-driven processes. This behavior applies only to periodic syncs; no events are triggered during a first-time import or manual sync to or from DevRev.

### Delete import

> This deletes any content created by the import, including users, groups, members, and articles.

An import and all the content it creates can be deleted from DevRev. This can be useful when running POCs or to change the configuration used during the import. Once an import has been deleted, all the content it created gets deleted, even if they were modified in DevRev. It's possible to import the project again after its deletion.

To delete an import and all the content it created, go to **Settings > Integrations > Airsync**, find the previously imported project, and select **⋮** > **Delete Import**.

## Related wiki nodes
- [[glossary/airsync]]

## Source
- DevRev support article [Document360 AirSync](https://support.devrev.ai/en-US/devrev/article/jgJymbfI) (ART-27324)
