---
title: Notion AirSync
devrev_id: ART-22010
parent_directory: AirSync
translation_group: lFhx-4bm
modified_date: "2026-02-03T17:25:43.887Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/lFhx-4bm"
tags: []
top_category: Computer by DevRev
wiki_match: glossary/airsync
match_score: 0.85
last_updated: 2026-05-11
related: ['glossary/airsync']
---

# Notion AirSync

The Notion AirSync simplifies migration from Notion to DevRev, supporting both
one-time imports and ongoing syncs.

## Supported objects

The following is a list of Notion objects and their corresponding DevRev
equivalents. Those marked as **Sync to DevRev** are eligible for import from
Notion to DevRev.

| **Notion Object** | **DevRev Object** | **Sync to DevRev** |
| --- | --- | --- |
| Page | Article | ✅ |
| User | DevUser | ✅ |
| Database (collection of pages) | Article (Single) | ✅ |

## Import from Notion

Follow these steps to install the Notion AirSync snap-in:

1. In the **Snap-in Config Modal**, search for **Notion** under **All snap-ins**.
2. Click **Add** and **Install snap-in**.
3. Go to **[Settings](https://app.devrev.ai/?setting=airsyncs)**[ > ](https://app.devrev.ai/?setting=airsyncs)**[Integrations](https://app.devrev.ai/?setting=airsyncs)**[ > ](https://app.devrev.ai/?setting=airsyncs)**[AirSyncs](https://app.devrev.ai/?setting=airsyncs)** in the left-hand navigation.
4. Click **AirSync** in the top-right corner and select **Notion**.
5. Create a new connection to your Notion account or use an existing one. See Choose a Connection Type
6. Once the connection is established:
   a. In DevRev, go to **[Settings](https://app.devrev.ai/?setting=airsyncs)**[ > ](https://app.devrev.ai/?setting=airsyncs)**[Integrations](https://app.devrev.ai/?setting=airsyncs)**[ > ](https://app.devrev.ai/?setting=airsyncs)**[AirSyncs](https://app.devrev.ai/?setting=airsyncs)**, then click **AirSync** in the top-right corner.
   b. Select **Notion**.
   c. Select the connection you just created. Click **Next**.
   d. On the next screen, select **Notion workspace**.
   e. Specify the **DevRev part** where the imported content should reside. This triggers a bulk import of the selected content.

DevRev automatically maps Notion properties to corresponding fields. You may be prompted for manual mapping in some cases.

Import duration depends on the volume of Notion data — from a few seconds to several hours.

You have two options to authenticate with your Notion workspace.

## Option 1: Notion OAuth Connection

1. Provide a name for the connection and click **Sign-in**.
2. You are redirected to Notion to authorize access to your workspace.
3. A pop-up appears for workspace access authorization. Select the workspace from the drop-down in the top-right corner and click **Select pages**.
4. On the next screen, select the required pages to import and click **Allow access**.
5. After successfully creating the connection, click **+AirSync** in the top-right corner and select the created connection.

Only pages selected during the OAuth connection are imported in the incremental sync (Sync to DevRev).

### Import additional pages

Update the access manually:

1. Go to **Notion Home**.
2. Click **Settings** (bottom-left panel).
3. Under **Accounts > Connections**, find the DevRev integration.
4. Click the menu (•••) > **Access selected pages**.
5. Select additional pages and **Save**.

You can use the same connection in DevRev to import more Notion pages.

When setting up a new connection for the same workspace, reselect all pages that were linked in the previous connection to maintain continuity.

## Option 2: Notion API Key Connection

Create an internal integration in Notion for the workspace you want to import:

1. In Notion, go to **Settings** from the left navigation.
2. Click Connections, then select **Develop or Manage Integrations** or click [here](https://www.notion.so/profile/integrations).
3. Click **Create New Integration**.
4. Choose the **workspace** from which you want to import pages.
5. Set the **Integration Type** to **Internal**.
6. Click **Save**.
7. In the pop-up, click Configure Integration Settings and enable the following scopes:
   a. Under **Content Capabilities**, enable **Read content**.
   b. Under **User Capabilities**, enable **Read user information, including email addresses**.
8. After saving the integration, copy the **Internal Integration Secret** and use it to establish the connection in DevRev.

Only pages connected to the integration can be imported. You must explicitly link the desired pages to the integration before starting the import.

### Connect pages to the integration

To link a Notion page to your integration:

1. Open the page in Notion.
2. Click the ••• (More) menu in the top-left corner.
3. Select **Connections**.
4. Choose the integration you created.

## 

---

## Related wiki nodes
- [[glossary/airsync]]

## Source
- DevRev support article [Notion AirSync](https://support.devrev.ai/en-US/devrev/article/lFhx-4bm) (ART-22010)
