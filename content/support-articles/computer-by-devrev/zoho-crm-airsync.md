---
title: Zoho CRM AirSync
devrev_id: ART-22479
parent_directory: AirSync
translation_group: cM_UNxOV
modified_date: "2026-01-28T21:44:00.574Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/cM_UNxOV"
tags: []
top_category: Computer by DevRev
wiki_match: glossary/airsync
match_score: 0.85
last_updated: 2026-05-11
related: ['glossary/airsync']
summary: "The Zoho CRM AirSync snap-in simplifies migration from Zoho CRM to DevRev, supporting both one-time imports and ongoing syncs."
---

# Zoho CRM AirSync

The Zoho CRM [[glossary/airsync|AirSync]] snap-in simplifies migration from Zoho CRM to DevRev, supporting both one-time imports and ongoing syncs.

## Supported objects

The following is a list of Zoho CRM objects and their corresponding DevRev equivalents. Those marked as **Sync to DevRev** are eligible for import from Zoho CRM to DevRev.

| Zoho CRM Object | DevRev Object | Sync to DevRev | Sync to Zoho |
| --- | --- | --- | --- |
| Users | DevUser | ✅ | ❌ |
| [[features/accounts|Accounts]] | [[entities/account|Account]] | ✅ | ❌ |
| Contacts | Contact | ✅ | ❌ |
| Leads | Contact | ✅ | ❌ |
| Deals | [[glossary/opportunity|Opportunity]] | ✅ | ❌ |
| Cases | [[features/tickets|Tickets]] | ✅ | ❌ |
| [[entities/task|Tasks]] | [[entities/task|Task]] | ✅ | ❌ |
| Calls | [[entities/meeting|Meeting]] | ✅ | ❌ |
| Events | Meeting | ✅ | ❌ |
| Products | Products | ✅ | ❌ |
| Campaigns | Custom Object | ✅ | ❌ |
| Price Books | Custom Object | ✅ | ❌ |
| Vendors | Custom Object | ✅ | ❌ |
| Quotes | Custom Object | ✅ | ❌ |
| Sales Orders | Custom Object | ✅ | ❌ |
| Purchase Orders | Custom Object | ✅ | ❌ |
| Invoices | Custom Object | ✅ | ❌ |
| Appointments Rescheduled History | Custom Object | ✅ | ❌ |
| Services | Custom Object | ✅ | ❌ |
| Custom Module | Custom Object | ✅ | ❌ |
| Solution | [[entities/article|Articles]] | ✅ | ❌ |
| Emails | DM | ❌ | ❌ |

## Importing from Zoho CRM

1. Log in to DevRev.
2. Navigate to **[Settings > Integrations > Snap-ins](https://app.devrev.ai/?setting=snap-ins)**, [[features/search|search]] for **Zoho CRM** under **All Snap-ins**.
3. Click **Add and Install Snap-in**.
4. Navigate to **[Settings > Integrations > Airsync](https://app.devrev.ai/?setting=airsyncs)** in the left-navigation.
5. Click **Airsync** in the top right corner and select **Zoho CRM**.
6. Create a new connection to authenticate with your Zoho CRM workspace, or use an existing active connection if you already have one.
7. Once the connection is established, select the Zoho CRM you want to import and specify the DevRev [[entities/part|part]] to be used for any imported work. This initiates a bulk import of the selected sync.
8. DevRev makes an effort to automatically map the fields from Zoho CRM to the corresponding fields in DevRev. However, you may be prompted to manually map certain fields if needed.

## Create Zoho CRM Connection

To create a Zoho CRM connection, you must first generate the required credentials from Zoho and then use them while creating the connection in DevRev.

### Step 1: Create a Self Client in Zoho API Console

1. Go to the **Zoho API Console**: [https://api-console.zoho.com/](https://api-console.zoho.com/)
2. Click **+ Add Client** (top-right corner).
3. Select **Self Client**.
4. Zoho will open the **Generate Code** tab. Switch to the **Client Secret** tab.
5. Copy the following details:- **Client ID**
   - **Client Secret**

> These will be required while creating the Zoho CRM connection in DevRev.

### Step 2: Find Your Zoho Organization ID

1. Log in to your **Zoho CRM** account.
2. Click your **profile icon** (top-right).
3. Click on your **Organization Name**.
4. Copy the **Organization ID** displayed on the screen.

### Step 3: Identify Your Zoho Region

Check the URL when you open Zoho CRM in your browser:

- `https://crm.zoho.in/` → Region: **.in**
- `https://crm.zoho.com/` → Region: **.com**
- `https://crm.zoho.eu/` → Region: **.eu**

### Step 4: Create Zoho CRM Connection in DevRev

1. In **DevRev**, navigate to **Airsync**.
2. Select **Zoho CRM**.
3. Click **Add Connection**.
4. Enter the following details:- **Connection Name**
   - **Client ID**
   - **Client Secret**
   - **Zoho Organization ID**
   - **Zoho Region**
5. Click **Next**.
6. On the next screen, select the authenticated Zoho CRM workspace.
7. Specify the DevRev part where the imported content should reside. Click **Start**.
8. This will trigger an import of the authenticated workspace.

> Import duration varies from minutes to hours based on data size.

## Limitations

- Admin user rights are mandatory to perform the import operation.
- Permission handling is only supported for solutions in the current version of the integration.
- Only fields mapped to stock fields of the Account and Contact modules are visible. Other fields will not appear in the records for these modules.
- Records that are updated only with attachments or connected records may not appear in incremental syncs. These records will sync only when the main record itself is updated.
- Attachments are not supported for modules that are imported as custom objects in DevRev.
- Custom fields for Meeting objects are not supported.
- The Meeting object does not support custom links (links to calls and events will not be imported).
- Custom fields that reference multiple object types (for example, the *Connected To* field) are not supported.
- Full stage history from Zoho is not supported; only the latest stage is captured during syncs.

## Related wiki nodes
- [[glossary/airsync]]

## Source
- DevRev support [[entities/article|article]] [Zoho CRM AirSync](https://support.devrev.ai/en-US/devrev/article/cM_UNxOV) (ART-22479)
