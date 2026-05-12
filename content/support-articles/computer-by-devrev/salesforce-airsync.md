---
title: Salesforce AirSync
devrev_id: ART-21996
parent_directory: AirSync
translation_group: i5UHGPEt
modified_date: "2026-04-15T10:54:10.85Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/i5UHGPEt"
tags: []
top_category: Computer by DevRev
wiki_match: glossary/airsync
match_score: 0.85
last_updated: 2026-05-11
related: ['glossary/airsync']
summary: "DevRev\"s Salesforce AirSync allows you to perform a bulk migration, ongoing 1-way sync, or ongoing 2-way syncs."
---

# Salesforce AirSync

DevRev's Salesforce [[glossary/airsync|AirSync]] allows you to perform a bulk migration, ongoing 1-way sync, or ongoing 2-way syncs. A bulk import is a prerequisite to setting up a sync.

For more information, refer to the [Salesforce AirSync snap-in](https://marketplace.devrev.ai/salesforce) on the DevRev marketplace.

## Supported objects

The following is a list of Salesforce objects and their corresponding DevRev equivalent. Those marked as **Sync to DevRev** are eligible for import/sync to DevRev from Salesforce. Those marked as **Sync to Salesforce** are eligible to be synced to Salesforce from DevRev.

| Salesforce Object | DevRev Object | Sync to DevRev | Sync to Salesforce |
| --- | --- | --- | --- |
| Case | [[entities/ticket|Ticket]] | ✅ | ✅ |
| Problem | Ticket | ✅ | ✅ |
| [[glossary/incident|Incident]] | Ticket | ✅ | ✅ |
| Comment on Case/[[entities/task|Task]]/Problem/Incident | Comment on Ticket | ✅ | ✅ |
| Attachment on Case/Task/Problem/Incident | Attachment on Ticket | ✅ | ❌ |
| Product | Product | ✅ | ❌ |
| [[entities/account|Account]] | Account | ✅ | ❌ |
| Contact | Contact | ✅ | ❌ |
| [[glossary/opportunity|Opportunity]] | Opportunity | ✅ | ✅ |
| Lead | Contact | ❌ | ❌ |
| Knowledge [[entities/article|Article]] | Article | ✅ | ❌ |
| Custom Object | Custom Object | ✅ | ❌ |
| Business Hours | Custom Object | ✅ | ❌ |
| Asset | Custom Object | ✅ | ❌ |
| Order | Custom Object | ✅ | ❌ |
| Quote | Custom Object | ✅ | ❌ |
| Event | Custom Object |  |  |
| Opportunity History | Custom Object | ✅ | ❌ |
| Task | Custom Object | ✅ | ❌ |
| Opportunity Contact Role | Custom Object | ✅ | ❌ |
| Messaging Session | Custom Object | ✅ | ❌ |
| Messaging End User | Custom Object | ✅ | ❌ |

## Importing from Salesforce

Follow the steps below to import from Salesforce:

Only [Salesforce editions with API access](https://help.salesforce.com/s/articleView?id=000385436&type=1) are supported. Supported editions include **Enterprise**, **Unlimited**, **Developer**, and **Performance**. Additionally, the **Professional** edition is supported if API access has been purchased as an add-on. Both sandbox and production instances are supported.

Since early September 2025, [Salesforce has started restricting the use of uninstalled connected apps](https://help.salesforce.com/s/articleView?id=005132365&type=1). Only highly trusted users with certain permissions can use uninstalled connected apps. The required permissions depend on whether **API Access Control** is enabled.
To enable API Access Control, follow these instructions:1. Open a case with Salesforce support and ask to have the API access control feature enabled.
2. Once enabled, go to the system user in SFDC and select the appropriate profle/permission set and go to **System Permissions**.
3. Check the box that says **Use Any API client**. This is a setting that isn't available without the API access control feature.

1. Go to **[Settings](https://app.devrev.ai/?setting=airsyncs)**[ > ](https://app.devrev.ai/?setting=airsyncs)**[Integrations](https://app.devrev.ai/?setting=airsyncs)**[ > ](https://app.devrev.ai/?setting=airsyncs)**[AirSyncs](https://app.devrev.ai/?setting=airsyncs)** and select **AirSync** (or **Start AirSync** if it's your first).
2. Create a new connection to your Salesforce account, or use an existing connection if you already have one.
3. Once the connection is established, select the Salesforce account you want to import and specify the DevRev [[entities/part|part]] that should be used for any imported cases without a product. This initiates a bulk import of the selected account.
4. DevRev makes an effort to automatically map the fields from Salesforce to corresponding fields in DevRev. However, you may be prompted to manually map certain fields if needed. You can track the migration and perform any required mapping under **[Settings](https://app.devrev.ai/?setting=airsyncs)**[ > ](https://app.devrev.ai/?setting=airsyncs)**[Integrations](https://app.devrev.ai/?setting=airsyncs)**[ > ](https://app.devrev.ai/?setting=airsyncs)**[AirSyncs](https://app.devrev.ai/?setting=airsyncs)**.

To ensure a successful import, it's important to verify that the Salesforce user has **View All Data** permissions, not to be confused with the **View All** permissions for individual objects. If this permission is missing, the **FeedComment** object will not be extracted. 

The duration of the import depends on the size of the Salesforce account and the data being imported. It can take seconds for an account with only a few dozen cases to a few hours for an account with tens of thousands of cases with many attachments. DevRev honors the Salesforce API rate limits and back-off and resumes automatically.

### Sync to Salesforce

After a successful import from a Salesforce account, you can sync changes made in DevRev to the previously imported cases back to Salesforce. Additionally, any new DevRev [[features/tickets|tickets]] marked for sync is created as new Salesforce items.

To perform a one-time sync to Salesforce, follow these steps:

1. Go to **[Settings](https://app.devrev.ai/?setting=airsyncs)**[ > ](https://app.devrev.ai/?setting=airsyncs)**[Integrations](https://app.devrev.ai/?setting=airsyncs)**[ > ](https://app.devrev.ai/?setting=airsyncs)**[AirSyncs](https://app.devrev.ai/?setting=airsyncs)**.
2. Locate the previously imported project.
3. Select ⋮ > **Sync DevRev to Salesforce Service**.

This may override fields in Salesforce of previously imported items, even if they were modified in Salesforce.

#### Mark a DevRev ticket for syncing

Using the Sync to Salesforce feature, it's possible to sync DevRev tickets to Salesforce. In order to sync a DevRev ticket to a specific Salesforce type, it must be marked for syncing. Marking a DevRev ticket for syncing can only be done during the creation of a new ticket. During ticket creation, open the dropdown **Select Subtype**, set it to the type the ticket should be synced to. The format is as follows: `SalesforceService / {type}`.

For example, if you want to sync a new ticket in DevRev to a case type in Salesforce, this would show as **SalesforceService / cases**.

After a DevRev work item has been marked for syncing, it's created in the specified Salesforce account the next time the Sync from DevRev to Salesforce runs. This can be triggered manually or automatically through a Periodic Sync. Future syncs keeps this item updated on both sides after it has been created in Salesforce.

## AirSync Salesforce scope and limitations

The following is a list of AirSync Salesforce scopes and limitations to keep in mind when performing a Salesforce AirSync. In addition to these Salesforce-specific limitations, there are also some generic [[support-articles/computer-by-devrev/airsync-overview#airsync-scope-and-limitations|AirSync scopes and limitations]].

### Comments

- Threaded case comments are not synced back to Salesforce.

### Updates

- Updates to `Picklist_MultiSelect` fields from DevRev are not loaded/synced back to Salesforce.

### Knowledge articles

- Only published [[entities/article|articles]] in the master language are imported from Salesforce to DevRev.
- If the article has multiple rich text content fields, the article will be split into multiple DevRev articles, one for each rich text content field.

### Sync groups as owners of tickets

- Articles with multiple rich text content fields are split into multiple DevRev articles, one for each rich text content field.
- If a case in Salesforce is owned by a queue or a [[entities/group|group]], the case is imported into DevRev with a fallback service account owner, and the **Group** field in DevRev is set to the name of the queue or group in Salesforce.
- For syncing back to Salesforce, to assign the case to a queue or group, the **Group** field in DevRev must be set to the name of the queue or group in Salesforce, and the **Owner** field must be set to a fallback service account.

## Related wiki nodes
- [[glossary/airsync]]

## Source
- DevRev support article [Salesforce AirSync](https://support.devrev.ai/en-US/devrev/article/i5UHGPEt) (ART-21996)
