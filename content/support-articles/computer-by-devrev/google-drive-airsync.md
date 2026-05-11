---
title: Google Drive AirSync
devrev_id: ART-22003
parent_directory: AirSync
translation_group: 5vSOrzHF
modified_date: "2026-05-05T12:31:36.134Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/5vSOrzHF"
tags: []
top_category: Computer by DevRev
wiki_match: glossary/airsync
match_score: 0.85
last_updated: 2026-05-11
related: ['glossary/airsync']
---

# Google Drive AirSync

The Google Drive AirSync simplifies migration from Google Drive to DevRev, supporting both one-time imports and ongoing syncs.

## Supported objects

The following is a list of Google Drive objects and their corresponding DevRev equivalents. Those marked as **Sync to DevRev** are eligible for import from Google Drive to DevRev.

| Google Drive object | DevRev object | Sync to DevRev |
| --- | --- | --- |
| Document | Article (Attachment) | ✅ |
| User | DevUser | ✅ |
| Group | Group | ✅ |
| Group Members | Group Members | ✅ |

## Supported document types

The Google Drive AirSync supports importing the following document types as attachments to DevRev Articles:

- Google Docs (docs, sheets, slides)
- Microsoft Docs (.docx, .doc, .pptx, .xlsx)
- PDF (.pdf)
- Plain Text (.txt)
- Rich Text Format (.rtf)
- Other common document formats supported by Google Drive.

## Import from Google Drive

Follow the steps below to import from Google Drive:

1. Go to the **Marketplace** and search for **Google Drive** in the **Import** category and install.
2. In the snap-in config modal, click **Install**.
3. Go to the **Import** section in your settings left nav.
4. Click **+Import** and select the Google Drive logo.
5. Create a new connection to your Google account, or use an existing connection if you already have one.You are required to use an admin connection first. So it imports all the users, groups with members successfully.
6. Once the connection is established, select the Google Drive you want to import and specify the DevRev part that should be used for any imported work (future releases make use of this). This initiates a bulk import of the selected drive.
7. DevRev makes an effort to automatically map the fields from Google Drive to the corresponding fields in DevRev. However, you may be prompted to manually map certain fields if needed.

The duration of the import depends on the size of the Google Drive and the data being imported. It can take seconds for an account with only a few dozen documents to a few hours for an account with tens of thousands of documents.

For a Google file to be imported into the knowledge base with AirSync, it must have **Can find in search results** in the sharing settings.

![Google sharing settings](don:core:dvrv-us-1:devo/0:artifact/4100957)

 **NOTE**: Due to API limitations, the Google Drive connector cannot modify permissions if the user who initially synced a document has their access revoked. Because the connector relies on that user's credentials to fetch the permission list, any loss of access prevents the system from syncing further permission changes.

## Related wiki nodes
- [[glossary/airsync]]

## Source
- DevRev support article [Google Drive AirSync](https://support.devrev.ai/en-US/devrev/article/5vSOrzHF) (ART-22003)
