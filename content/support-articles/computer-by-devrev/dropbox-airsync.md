---
title: Dropbox AirSync
devrev_id: ART-21994
parent_directory: AirSync
translation_group: -ytHevK0
modified_date: "2026-01-05T06:41:41.937Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/-ytHevK0"
tags: []
top_category: Computer by DevRev
wiki_match: glossary/airsync
match_score: 0.85
last_updated: 2026-05-11
related: ['glossary/airsync']
---

# Dropbox AirSync

The Dropbox AirSync simplifies migration from Dropbox to DevRev, supporting both one-time imports and ongoing syncs.

### Key features

- User profile sync for all team members within a Dropbox Business account.
- Complete file and folder hierarchy sync with directory structure preservation.
- Sync of private folders, team member folders, shared folders, and Dropbox Paper documents (.paper, .papert) for all team members.
- Group and group member data sync with membership details.
- Permission synchronization with granular access controls on files.

## Supported objects

The following is a list of Dropbox objects and their corresponding DevRev equivalents. Those marked as **Sync to DevRev** are eligible for import from Dropbox to DevRev.

| Dropbox object | DevRev object | Sync to DevRev | Sync to Dropbox |
| --- | --- | --- | --- |
| Users | DevUser | ✅ | ❌ |
| Folders | Directory (Article Collection) | ✅ | ❌ |
| File (Meta data) | Article | ✅ | ❌ |
| File Content | Attachment (Article Attachment) | ✅ | ❌ |
| Groups | Group | ✅ | ❌ |
| Group Members | Group Members | ✅ | ❌ |

## Supported document types

The Dropbox AirSync supports importing the following document types as attachments to DevRev Articles:

- Google Workspace documents (.gdoc, .gsheet, .gslides, .gdraw, .gform)
- Microsoft Office documents (.doc, .docx, .ppt, .pptx, .xls, .xlsx)
- PDF documents (.pdf)
- Plain Text files (.txt)
- HTML and Web files (.html, .web)
- Development files (.css, .js, .json, .xml)
- Image formats (.jpg, .jpeg, .png, .gif, .svg)
- Video and Audio files (.mp4, .mov, .mp3)
- ZIP archives (.zip)
- Dropbox Paper documents (.paper, .papert)
- And other common document formats supported by Dropbox.

Dropbox Paper documents (.paper, .papert) are imported as HTML files to preserve formatting and structure.

## Import from Dropbox

1. Go to the **Marketplace** and search for **Dropbox** in the **Import** category and install.
2. In the snap-in config modal, click **Install**.
3. Go to the **Import** section in your settings left nav.
4. Click **+Import** and select the Dropbox logo.
5. Create a new connection to your Dropbox account, or use an existing connection if you already have one.

You must use an admin connection. Non-admin connections are not supported at this time.

1. Once the connection is established, select the Dropbox team you want to import and specify the DevRev part to be used for any imported work. This initiates a bulk import of the selected team.
2. DevRev makes an effort to automatically map the fields from Dropbox to the corresponding fields in DevRev. However, you may be prompted to manually map certain fields if needed.

### Limitations

- Supports sync only with Dropbox Business accounts; personal accounts are not supported at this time.
- An admin connection is required for synchronization; non-admin connections are not currently supported.
- Periodic sync duration may equal or exceed initial import time.
- Folder permissions are not synchronized. Users can see all types of folders belonging to other team members but cannot access files within those folders without proper permissions.

## Related wiki nodes
- [[glossary/airsync]]

## Source
- DevRev support article [Dropbox AirSync](https://support.devrev.ai/en-US/devrev/article/-ytHevK0) (ART-21994)
