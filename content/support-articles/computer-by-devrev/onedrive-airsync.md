---
title: OneDrive AirSync
devrev_id: ART-21993
parent_directory: AirSync
translation_group: UTMv4dZv
modified_date: "2026-02-16T17:42:32.698Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/UTMv4dZv"
tags: []
top_category: Computer by DevRev
wiki_match: glossary/airsync
match_score: 0.85
last_updated: 2026-05-11
related: ['glossary/airsync']
summary: "The OneDrive AirSync simplifies migration from Microsoft OneDrive to DevRev, supporting both one-time imports and ongoing syncs."
---

# OneDrive AirSync

The OneDrive [[glossary/airsync|AirSync]] simplifies migration from Microsoft OneDrive to DevRev, supporting both one-time imports and ongoing syncs.

## Supported objects

The following is a list of OneDrive objects and their corresponding DevRev equivalents. Those marked as Sync to DevRev are eligible for import from OneDrive to DevRev.

| OneDrive object | DevRev object | Sync to DevRev |
| --- | --- | --- |
| Document | [[entities/article|Article]] | ✅ |
| User | DevUser | ✅ |
| [[entities/group|Group]] | Group | ✅ |
| Group Members | Group Members | ✅ |

## Import from OneDrive

Follow the steps below to import from OneDrive:

1. Go to the **Marketplace**, [[features/search|search]] for **OneDrive** in the **Import** category, and install it.
2. In the **snap-in config modal**, click **Install**.
3. Go to the **Import** section in your **settings left navigation**.
4. Click **+Import** and select the **OneDrive logo**.
5. Create a new connection to your Microsoft [[entities/account|account]] or use an existing connection if you already have one.

The admin must go to the Azure directory and grant permissions for the required scopes so that non-admin users can import user details. If permissions are not granted, you are required to use an admin connection first. This allows all users, [[entities/group|groups]], and members to be imported successfully.

1. Once the connection is established, select the OneDrive directory you want to import and specify the DevRev [[entities/part|part]] that should be used for any imported work. This initiates a bulk import of the selected directory.
2. DevRev attempts to automatically map fields from OneDrive to the corresponding fields in DevRev. However, you may be prompted to manually map certain fields if needed.

## Supported content file types

- Word Documents (.docx, .doc)
- Excel Spreadsheets (.xlsx, .xls)
- PowerPoint Presentations (.pptx, .ppt)
- PDFs (.pdf)
- CSV Files (.csv)
- Text Files (.txt)
- Markdown Files (.md)
- OpenDocument Text (.odt)

##

## Related wiki nodes
- [[glossary/airsync]]

## Source
- DevRev support article [OneDrive AirSync](https://support.devrev.ai/en-US/devrev/article/UTMv4dZv) (ART-21993)
