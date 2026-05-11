---
title: Confluence AirSync
devrev_id: ART-22001
parent_directory: AirSync
translation_group: BOVjni26
modified_date: "2026-04-27T10:40:36.541Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/BOVjni26"
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

### Supported objects

The following is a list of Confluence objects and their corresponding DevRev equivalents. Those marked as **Sync to DevRev** are eligible for import from Confluence to DevRev.

| Confluence Object | DevRev Object | Sync to DevRev |
| --- | --- | --- |
| Pages | [[entities/article|Articles]] | ✅ |
| Blogs | Articles | ✅ |
| Users | Identities | ✅ |
| Attachments | [[features/artifacts|Artifacts]] on [[entities/article|Article]] | ✅ |
| Folders | Directories | ✅ |

### Importing from Confluence

1. Log in to DevRev.
2. Navigate to **[Settings > Integrations > Snap-ins](https://app.devrev.ai/?setting=snap-ins)**, [[features/search|search]] for **Confluence **under **All Snap-ins**.
3. Click **Add and Install Snap-in**.
4. Navigate to **[Settings > Integrations > Airsync](https://app.devrev.ai/?setting=airsyncs)** in the left-navigation.
5. Click **Airsync** in the top right corner and select **Confluence**.
6. Create a new connection to authenticate with your Confluence workspace, or use an existing active connection if you already have one.
7. Once the connection is established, select the Confluence spaces you want to import and specify the DevRev [[entities/part|part]] to be used for any imported work. This initiates a bulk import of the selected spaces.
8. DevRev makes an effort to automatically map the fields from Confluence to the corresponding fields in DevRev. However, you may be prompted to manually map certain fields if needed.

### Create Confluence Connection

To create a Confluence connection, you must first generate a Personal Access Token (PAT) from your Atlassian [[entities/account|account]] and then use it while creating the connection in DevRev.

### Step 1: Create a Personal Access Token

1. Go to your [Atlassian Account Settings](https://id.atlassian.com/manage-profile).
2. Navigate to **Security** > **API tokens**.
3. Click **Create API token**.
4. Enter a label for your token and click **Create**.
5. Copy the generated token.

> This token will be required while creating the Confluence connection in DevRev.

### Step 2: Set Email Visibility

To successfully import users and their associated articles, you must set email visibility to "Anyone" in your Confluence account settings:

1. Navigate to your [Atlassian Account Settings](https://id.atlassian.com/manage-profile).
2. In the left-hand menu, select **Profile and Visibility**.
3. Scroll down to the **Contact** section.
4. Locate the **Email** field and set its visibility to **Anyone**.

### Step 3: Create Confluence Connection in DevRev

1. In **DevRev**, navigate to **Airsync**.
2. Select **Confluence**.
3. Click **Add Connection**.
4. Enter the following details:- **Connection Name**
   - **Email**: Enter the email used in your Confluence account
   - **Subdomain**: Enter only the domain part from your Confluence URL (e.g., "[yourdomain.atlassian.net](http://yourdomain.atlassian.net)")
   - **PAT Token**: Enter your Personal Access Token
5. Click **Next**.
6. On the next screen, select the Confluence spaces you want to import.
7. Specify the DevRev part where the imported content should reside. Click **Start**.
8. This will trigger an import of the selected spaces.

> Import duration varies from minutes to hours based on data size. Small spaces might complete in seconds, while larger spaces with thousands of pages and attachments may take hours.

## Limitations

While Confluence AirSync supports importing a wide range of content and metadata, the following are not imported or supported:

- Comments on pages and blogs
- Page reactions (likes or other emoji responses)
- Inline attachments indexing
- Table sorting — tables imported from Confluence will appear as static content and cannot be sorted within DevRev
- Email visibility requirement — users must explicitly set their email visibility to** Anyone** in their Confluence profile settings; otherwise, user associations and [[features/identity|identity]] mapping may fail
- Shared public Confluence links — any publicly shared Confluence links cannot be tracked or mapped; no user or content association will be pulled from such links

These limitations exist due to differences in feature support between Confluence and DevRev.

## Related wiki nodes
- [[glossary/airsync]]

## Source
- DevRev support article [Confluence AirSync](https://support.devrev.ai/en-US/devrev/article/BOVjni26) (ART-22001)
