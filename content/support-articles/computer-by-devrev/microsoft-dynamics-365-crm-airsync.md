---
title: Microsoft Dynamics 365 CRM AirSync
devrev_id: ART-23314
parent_directory: AirSync
translation_group: pOtNOMwk
modified_date: "2026-02-09T05:02:06.85Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/pOtNOMwk"
tags: []
top_category: Computer by DevRev
wiki_match: glossary/airsync
match_score: 0.85
last_updated: 2026-05-11
related: ['glossary/airsync']
---

# Microsoft Dynamics 365 CRM AirSync

The Microsoft Dynamics 365 CRM AirSync simplifies migration from Dynamics 365 to DevRev, supporting both one-time imports and ongoing syncs. This integration brings your CRM data including accounts, contacts, opportunities, cases, and activities into your DevRev workspace. This AirSync specifically supports data from the Customer Service and Sales Hub modules.

### Supported objects

The following is a list of Microsoft Dynamics 365 CRM objects and their corresponding DevRev equivalents. Those marked as **Sync to DevRev** are eligible for import from Dynamics 365 to DevRev.

| Dynamics 365 Object | DevRev Object | Sync to DevRev |
| --- | --- | --- |
| System User | DevUser | ✅ |
| Account | Account | ✅ |
| Contact | Contact | ✅ |
| Lead | Contact | ✅ |
| Opportunity | Opportunity | ✅ |
| Incident (Case) | Ticket | ✅ |
| Task | Issue | ✅ |
| Knowledge Article | Article | ✅ |
| Annotation (Note) | Comment | ✅ |
| Product | Product | ✅ |
| Appointment | Meeting | ✅ |
| Activities | Custom Object | ✅ |
| Quote | Custom Object | ✅ |
| Quote Detail | Custom Object | ✅ |
| Order | Custom Object | ✅ |
| Sales Order Detail | Custom Object | ✅ |
| Invoice | Custom Object | ✅ |
| Price Level | Custom Object | ✅ |
| Unit of Measure | Custom Object | ✅ |
| Unit Group | Custom Object | ✅ |
| Opportunity Product | Custom Object | ✅ |
| Campaign | Custom Object | ✅ |
| Marketing List | Custom Object | ✅ |
| Goal | Custom Object | ✅ |
| Metric | Custom Object | ✅ |
| Competitor | Custom Object | ✅ |
| Territory | Custom Object | ✅ |
| Sales Literature | Custom Object | ✅ |
| Discount | Custom Object | ✅ |
| Transaction Currency | Custom Object | ✅ |
| Entitlement | Custom Object | ✅ |
| SLA | Custom Object | ✅ |
| SLA Item | Custom Object | ✅ |
| SLA KPI | Custom Object | ✅ |
| Subject | Custom Object | ✅ |
| Bookable Resource | Custom Object | ✅ |
| Timezone Definition | Custom Object | ✅ |
| Email | — | ❌ |

### Create Microsoft Dynamics 365 Connection

The Microsoft Dynamics 365 CRM snap-in uses OAuth 2.0 for secure authentication.

### Create Connection in DevRev

1. In **DevRev**, go to **Airsync**.
2. Select **Microsoft Dynamics 365 CRM**.
3. Click **Add Connection**.
4. Enter the following details:

   * Connection Name
   * Subdomain
5. Click **Sign in with Snap-ins**.
6. On the next screen, the Microsoft login portal will pop up. Authenticate with your login credentials.

   * Admin consent is required for non-admin users.
7. Upon successful authentication, click **Connect and Install Snap-in**.

### Importing from Microsoft Dynamics 365 CRM

1. Log in to DevRev.
2. Go to **Settings > Integrations > Snap-ins**, search for **Microsoft Dynamics 365 CRM** under **All Snap-ins**.
3. Click **Add and Install Snap-in**.
4. Navigate to **Settings > Integrations > Airsync** in the left-navigation.
5. Click **Airsync** in the top right corner and select **Microsoft Dynamics 365 CRM**.
6. Create a new connection to authenticate with your Dynamics 365 organization, or use an existing active connection if you already have one.
7. Once the connection is established and the snap-in is installed, click **Start AirSync**, select **Dynamics 365 AirSync**, then select the organization you want to import and specify the DevRev part to be used for any imported work. This initiates a bulk import of the selected organization.
8. DevRev automatically maps fields from Dynamics 365 to the corresponding fields in DevRev. However, it is advised to manually review the mapping and update certain fields if needed.

**Note**: Import duration varies from minutes to hours based on the volume of data in your Dynamics 365 organization.

## Supported activities

The Activities object in the supported objects table includes the following activity types from Microsoft Dynamics 365.

**Note**: Tasks are mapped separately to a DevRev issue, and email activities are not supported.

| Activity Type | Description |
| --- | --- |
| Phone Call | Phone call records and metadata |
| Appointment | Appointment and meeting records |
| Letter | Letter correspondence records |
| Fax | Fax activity records |
| Campaign Response | Marketing campaign response records |
| Service Appointment | Service scheduling records |
| Opportunity Close | Opportunity closure activity records |
| Order Close | Sales order closure records |
| Quote Close | Quote closure records |
| Incident Resolution | Case resolution records |

## Limitations

While Microsoft Dynamics 365 CRM AirSync supports importing a wide range of content and metadata, the following are not imported or supported:

* **Unidirectional sync only** — Data flows from Dynamics 365 to DevRev. Changes made in DevRev are not synced back to Dynamics 365 (reverse sync is not supported).
* **Limited to Customer Service and Sales Hub** — Only data from Customer Service and Sales Hub modules is imported. Other Dynamics 365 apps such as Field Service, Marketing, or Finance are not supported.
* **Email activities are not supported** — Email records from Dynamics 365 are not imported. Only the activity types listed above are supported.
* **Email attachments are not supported** — Email attachments from Dynamics 365 are not imported. Only the activity types listed above are supported.
* **Not all activities are exported** — Only the specific activity types documented in the "Supported activities" section are imported. Other activity types such as custom activities or social activities are not supported.
* **Permission handling not supported** — Dynamics 365 security roles and field-level security are not mapped to DevRev permissions. All imported data follows DevRev's permission model.
* **No transactional guarantees** — If an import fails partway through, partial data may exist in DevRev without automatic rollback.
* **Attachment size limits** — Large attachments may be subject to size limits during import.
* **Related entity references** — Some lookup field references may not resolve if the related entity is not part of the import scope.
* **Picklist/OptionSet mappings** — Custom picklist values are imported but may require manual mapping to DevRev enum fields.
* **Custom link warnings** — Some custom links may throw warnings during import. This is typically due to associations with unsupported entities.

## Post import options

After a successful import, you have the following options available for the imported organization:

* **Sync to DevRev**

  This option allows you to synchronize any modifications made in Dynamics 365 with the corresponding items previously imported into DevRev. It also creates new items in DevRev for any records added or updated in Dynamics 365 after the last sync or import.
* **View Report**

  This option allows you to access detailed information about the initial import and any subsequent syncs performed, including statistics on records synced and any errors encountered.
* **Delete Import**

  If you want to remove the import and all data that were imported from Dynamics 365 into DevRev, you can use this option. This will delete all accounts, contacts, opportunities, cases, activities, and related data.
* **Edit Connection**

  Use this option to change the connection used for any subsequent actions. It can be helpful if:

  + An OAuth connection needs to be re-authorized (e.g., token expired or permissions changed)
  + Client credentials need to be rotated for security compliance
  + The user who established the connection is no longer available
  + You want to connect to a different Dynamics 365 organization

### Sync to DevRev

After a successful import from Dynamics 365, you can choose to sync the imported data with DevRev. This feature imports any new or updated accounts, contacts, opportunities, cases, activities, and other records, as well as any changes made to previously imported items.

To perform a one-time sync to DevRev, follow these steps:

1. Go to **Settings > Integrations > Airsync**.
2. Locate the previously imported Dynamics 365 organization.
3. Select the **⋮** > **Sync Dynamics 365 to DevRev** option.

**Note**: A one-time sync may overwrite fields in previously imported items, even if they were modified in DevRev.

### Historical imports

To view currently running and previous imports from various sources, do the following:

1. Go to **Settings > Integrations > Airsync**.
2. Select the import you want to view.
3. Click on the context menu (⋮) and select **View Report**.

The report includes detailed statistics such as:

* Total number of records synced by entity type
* Number of attachments processed
* Users and contacts imported
* Sync duration and any errors encountered

### Periodic sync

After successfully importing to DevRev, you have the option to enable a periodic sync. This allows for automatic synchronization with DevRev on a regular basis. By default, the sync occurs once an hour.

To configure periodic sync, follow these steps:

1. Go to **Settings > Integrations > Airsync**.
2. Locate the previously imported Dynamics 365 organization.
3. Select the **⋮** > **Set Periodic Sync** option.

The Enable automation for synced items setting is optional and can be activated during periodic sync configuration. When enabled, newly created or updated items trigger events, which can initiate webhooks, notifications, snap-ins, and other processes, as if the events originated directly in DevRev.

If this setting is turned off, updates do not trigger any event-driven processes. This behavior applies only to periodic syncs; no events are triggered during a first-time import or manual sync to DevRev.

### Delete import

> This deletes any content created by the import, including accounts, contacts, opportunities, cases, activities, products, knowledge articles, and all related data.

An import and all the content it creates can be deleted from DevRev. This can be useful when running POCs or to change the configuration used during the import. Once an import has been deleted, all the content it created gets deleted, even if they were modified in DevRev. It's possible to import the Dynamics 365 organization again after its deletion.

To delete an import and all the content it created, go to **Settings > Integrations > Airsync**, find the previously imported Dynamics 365 organization, and select **⋮** > **Delete Import**.

## Related wiki nodes
- [[glossary/airsync]]

## Source
- DevRev support article [Microsoft Dynamics 365 CRM AirSync](https://support.devrev.ai/en-US/devrev/article/pOtNOMwk) (ART-23314)
