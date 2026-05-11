---
title: Zendesk AirSync
devrev_id: ART-21997
parent_directory: AirSync
translation_group: MX2y9R9A
modified_date: "2026-02-27T08:22:15.301Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/MX2y9R9A"
tags: []
top_category: Computer by DevRev
wiki_match: glossary/airsync
match_score: 0.85
last_updated: 2026-05-11
related: ['glossary/airsync']
---

# Zendesk AirSync

DevRev's Zendesk AirSync allows you to perform a bulk import, ongoing 1-way sync, or ongoing 2-way syncs. A bulk import is a prerequisite to setting up a sync.

For more information, refer to the [Zendesk AirSync snap-in](https://marketplace.devrev.ai/zendesk) on the DevRev marketplace.

## Supported objects

The following is a list of Zendesk objects and their corresponding DevRev equivalent. Those marked as **Sync to DevRev** are eligible for import/sync to DevRev from Zendesk. Those marked as **Sync to Zendesk** are eligible to be synced to Zendesk from DevRev.

| Zendesk Object | DevRev Object | Sync to DevRev | Sync to Zendesk |
| --- | --- | --- | --- |
| Ticket | Ticket | ✅ | ✅ |
| Comment on Ticket | Comments | ✅ | ✅ |
| Category/Status of Ticket | State/Stage of Ticket | ✅ | ✅ |
| Attachments on Ticket | Attachments on Ticket | ✅ | ✅ |
| Tag on Ticket | Tag on Ticket | ✅ | ❌ |
| Organization | Account | ✅ | ❌ |
| Agent | DevUser | ✅ | ❌ |
| End User | Contact | ✅ | ❌ |
| Chat | Conversation | ❌ | ❌ |
| Conversation | Conversation | ❌ | ❌ |
| SLA | SLA | ❌ | ❌ |
| Article | Article | ✅ | ❌ |
| Categories | Collections | ✅ | ❌ |
| Sections | Collections | ✅ | ❌ |
| Automation | Snap-in | ❌ | ❌ |
| Macro | Command | ❌ | ❌ |
| Custom Object | Custom Object | ❌ | ❌ |

## Importing from Zendesk

Follow the steps below to import from Zendesk:

User performing the AirSync should have administrator permissions on external side. Zendesk incremental endpoints which are heavily used in AriSync are not accessible for non-admin users thus sync won't work as expected.

1. Go to **[Settings](https://app.devrev.ai/?setting=airsyncs)**[ > ](https://app.devrev.ai/?setting=airsyncs)**[Integrations](https://app.devrev.ai/?setting=airsyncs)**[ > ](https://app.devrev.ai/?setting=airsyncs)**[AirSyncs](https://app.devrev.ai/?setting=airsyncs)** and select **AirSync** (or **Start AirSync** if it's your first).
2. Create a new connection to your Zendesk account, or use an existing connection if you already have one.
3. Once the connection is established, select the Zendesk workspace you want to import and specify the DevRev part where the imported tickets should be created. This initiates a bulk import of the selected workspace.
4. DevRev makes an effort to automatically map the fields from Zendesk to corresponding fields in DevRev. However, you may be prompted to manually map certain fields if needed.

DevRev supports importing Zendesk organization custom fields. When importing organizations, AirSync will display Zendesk organization custom fields under **Select Custom Fields**. Selecting them will create them as DevRev account custom fields with corresponding values filled in.

The duration of the import depends on the size of the Zendesk account. It can take seconds for an account with only a few tickets to a few hours for an account with tens of thousands of tickets with many attachments. DevRev honors the Zendesk API rate limits and back-off and resumes automatically.

### Sync to Zendesk

After a successful import from a Zendesk account, you can sync changes made in DevRev to the previously imported supported items back to Zendesk. Additionally, any new DevRev tickets marked for sync are created as new Zendesk items.

To perform a one-time sync to Zendesk, follow these steps:

1. Go to **[Settings](https://app.devrev.ai/?setting=airsyncs)**[ > ](https://app.devrev.ai/?setting=airsyncs)**[Integrations](https://app.devrev.ai/?setting=airsyncs)**[ > ](https://app.devrev.ai/?setting=airsyncs)**[AirSyncs](https://app.devrev.ai/?setting=airsyncs)**.
2. Locate the previously imported project.
3. Select ⋮ > **Sync DevRev to Zendesk**.

This may override fields in Zendesk of previously imported items, even if they were modified in Zendesk.

#### Mark a DevRev ticket for syncing

Using the Sync to Zendesk feature, it's possible to sync DevRev tickets to Zendesk. In order to sync a DevRev ticket to a specific Zendesk type, it must be marked for syncing. Marking a DevRev ticket for syncing can only be done during the creation of a new ticket. During ticket creation, open the dropdown **Select Subtype**, set it to the type the ticket should be synced to. The format is as follows: `Zendesk / tickets / {type}`.

For example, if you want to sync a new ticket of type question to Zendesk, this would show as `Zendesk / tickets / question`.

After a DevRev work item has been marked for syncing, it's created in Zendesk the next time the Sync from DevRev to Zendesk runs. This can be triggered manually or automatically through a Periodic Sync. Future sync keeps this item updated on both sides after it has been created in Zendesk.

## Zendesk Help Center AirSync

DevRev supports the import of Zendesk help center (Categories, Sections, and KB Articles) using AirSync.

The mapping of Zendesk items to their counterparts in DevRev is as follows:

| Zendesk | DevRev |
| --- | --- |
| Categories | Collections |
| Sections | Collections |
| Articles | Articles |
| Content Tags | Tags |
| Permission Groups | Tags |
| User Segments | Tags |

During import, any fields without equivalence in DevRev are excluded. For information about DevRev articles, click [[support-articles/computer-plus-support/articles|here]].

### Importing Help Center items into DevRev

The help center import process is integrated into your overall Zendesk import. If you already have an ongoing import of tickets and want to include articles as well, reach out to our customer experience team.

### Features

- Imported articles will be editable within DevRev.
- Inline and block attachments associated with each article will be imported.
- References to other Zendesk articles within article content will be managed, redirecting to articles on DevRev. Note that only article references created through Zendesk official reference creation tool. Any links that do not follow the Zendesk article reference format (minified links etc.) will not be detected as references to internal articles. 
- Permission groups and user segments will be imported as tags and added to the relevant articles.
- Content Tags are currently not being synced.
- Each synchronization will generate a new version of the article on DevRev if changes were made in Zendesk since the last sync, ensuring content is not overwritten. Users can edit articles within DevRev.

### Help center item translations

DevRev supports bringing in translations of articles, sections and categories from Zendesk.

- Tree structure of directories is kept as it was in Zendesk - sections are nested under the same categories and articles under the same sections.
- The directory structure can be viewed **per locale** on UI under 'Collections' tab in Knowledge Base  (only directories form the same locale are shown on UI on the same view)
- Same applies to articles which can be viewed under 'Articles' tab
- Brands are not imported as directories as they don't have translations (described in the limitations)
- Multi-language portals are currently not available but can be enabled on request.
- References to other articles are resolved in a way that they point to other articles in the same locale as the article they are placed. If a referenced article in the same locale does not exist, reference points to the english version of the article.
- Inline attachments are synced and are placed in the same place as in original article. Attachments can differ among different translations which is the same as in source system.
- Block attachments are also synced. Those are multiplied so that every translations gets its own copy of block attachment. As a result, block attachments can be changed per translation which is different from Zendesk where block attachments can only be changed for all translations together.

Syncing of translations has certain **limitations**:

- articles or sections that don't have a parent section/category translated into the same locale are synced to DevRev and can be found under list of all articles but will not be bound to any directory as DevRev can't link items with different locales. Note that so articles will not be visible in a customer portal. 
- To mitigate above issue the corresponding translation of parent should be created in Zenesk beforehand or later on in DevRev. Note that in the later case the article has to be linked manually to this parent translation.
- Note that there are multiple locales for the same language in Zendesk (for ex. `pl` and `pl-pl` both represent polish). For mapping of child objects to their parents this have to be set accordingly (`pl` parrent for `pl` child and `pl-pl` parent for `pl-pl` child).
- Articles with similar locales as above will be synced as the same translation into DevRev - both with locale `pl-PL`.
- References to other knowledge base articles will point to the article with the same locale as article that contains the reference. In case referenced article does not have the corresponding translation the reference will default to `en-us`. In case there is no `en-us` version the link will not be parsed.
- When enabling translations, the brands form Zendesk are not synced anymore due to lack of translations for those (those may be synced for en-us but will appear empty, not containing any sub-items). Categories will appear top level in directory structure. If you need brands in your DevRev portal, contact customer experience team. Overall brand support is coming in the near future.
- If you currently have ongoing article sync without translations, contact customer experience team to add support for this feature.

### Limitations

- While Zendesk's API provides article content in *HTML*, DevRev articles are in a custom *JSON* format. We've made a best-effort conversion between the two formats, which may result in errors. If any errors are detected, a `Review Required` tag will be added, and the article status will be switched to *draft*. While our converter supports Zendesk's native editor tags, we cannot guarantee compatibility with all user-added HTML, potentially resulting in rendering issues and disruptions to the editing experience.
- The ordering of articles and collections during the initial import and subsequent syncs is not assured. This is because of limitations in how Zendesk transmits positions in its response and how we internally store the rank of articles and collections.
- Syncing from DevRev to Zendesk for help center items is not supported.
- For large AirSyncs, the data processing may take some time, which is why it remains in the extraction phase for an extended period.

## AirSync Zendesk scope and limitations

The following is a list of AirSync Zendesk scopes and limitations to keep in mind when performing a Zendesk AirSync. In addition to these Zendesk-specific limitations, there are also some generic [[support-articles/computer-by-devrev/airsync-overview#airsync-scope-and-limitations|AirSync scopes and limitations]].

### Comments

Inline email replies may be omitted when importing Zendesk ticket responses into DevRev. These replies include and update the contents of previous emails within the same message. This omission occurs due to limitations in the Zendesk API.

### Updates

- Changes to the description field in DevRev are not properly transferred since the description isn’t a first-class field in Zendesk.
- If a Zendesk public note is changed to private after being synced to DevRev, it will remain a public comment in DevRev.

## Related wiki nodes
- [[glossary/airsync]]

## Source
- DevRev support article [Zendesk AirSync](https://support.devrev.ai/en-US/devrev/article/MX2y9R9A) (ART-21997)
