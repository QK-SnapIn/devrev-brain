---
title: ServiceNow KB AirSync
devrev_id: ART-22009
parent_directory: AirSync
translation_group: MoQxlpFG
modified_date: "2026-01-05T05:51:05.94Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/MoQxlpFG"
tags: []
top_category: Computer by DevRev
wiki_match: glossary/airsync
match_score: 0.85
last_updated: 2026-05-11
related: ['glossary/airsync']
---

# ServiceNow KB AirSync

The ServiceNow KB AirSync simplifies migration from ServiceNow to DevRev, supporting both one-time imports and Periodic Sync.

## Supported objects

| ServiceNow KB Object | DevRev Object | Sync to DevRev |
| --- | --- | --- |
| User | DevUser | ✅ |
| Knowledge Base | Collection | ✅ |
| Knowledge Category | Tag | ✅ |
| Tag | Tag | ✅ |
| User Criteria | Group | ✅ |
| User Criteria User | Group member | ✅ |
| Knowledge Article | Article | ✅ |
| Article Attachment | Attachment on Article | ✅ |

### Importing from ServiceNow KB

1. Login to DevRev.
2. Go to **Settings > Integrations > Snap-ins**, search for **ServiceNow KB** under **All Snap-ins**.
3. Click **Add** and **Install Snap-in**.
4. Go to **[Settings](https://app.devrev.ai/?setting=airsyncs)**[ > ](https://app.devrev.ai/?setting=airsyncs)**[Integrations](https://app.devrev.ai/?setting=airsyncs)**[ > ](https://app.devrev.ai/?setting=airsyncs)**[AirSyncs](https://app.devrev.ai/?setting=airsyncs)** in the left navigation.
5. Click **AirSync** in top-right corner and select the **ServiceNow KB** connection.
6. Create a new connection to authenticate with your ServiceNow workspace, or use an existing active connection.

### Create ServiceNow connection

1. Provide a name to the connection.
2. In the **Subdomain** field, enter your ServiceNow workspace ID, which can be found in the ServiceNow browser URL. For example, from [https://dev190970.service-now.com/](https://dev190970.service-now.com/), dev190970 is the workspace ID.
3. Enter ServiceNow username and password, then click **Next**.
4. On the next screen, select the authenticated **ServiceNow workspace**.
5. Specify the **DevRev part** where the imported content should reside. Click **Start**.
   This triggers an import of the authenticated workspace.

The import duration can vary from minutes to hours depending on the size of the data.

### Key highlights

- **Structure Preservation**: Maintains ServiceNow knowledge bases as collections in DevRev.
- **Basic Permissions**: Preserves knowledge base and article permissions in DevRev's articles. Only can read and can contribute permissions are imported from the knowledge base and articles.
- **Content & Metadata**: Imports published articles, including content, titles, dates, authors, and source URLs.
- **Version History**: Keeps track of published article versions.
- **Attachments**: Transfers files attached to articles and links them correctly.
- **User Criteria**: Imports users and group rules from ServiceNow.

### Limitations

- **Access Requirements**: The connecting user must have read rights for users and criteria in ServiceNow.
- **Advanced Permissions**: Complex scripts and custom ACL rules in ServiceNow may not transfer; only basic access settings are moved.
- **Excluded Features**: Custom widgets, workflows, and scripted criteria are not imported.
- **Permission Removals**: Removing access in ServiceNow after import isn’t reflected on sync; only new additions are sync.
- **Language Tags**: All imported articles default to English in DevRev, regardless of the original language.
  If a user in ServiceNow belongs to two different criteria—one allowing read and contribute access, and the other denying it—they may still have access in DevRev. However, if the same criteria appear in both the allow and deny lists for read and contribute access, the user is restricted in DevRev.

## Related wiki nodes
- [[glossary/airsync]]

## Source
- DevRev support article [ServiceNow KB AirSync](https://support.devrev.ai/en-US/devrev/article/MoQxlpFG) (ART-22009)
