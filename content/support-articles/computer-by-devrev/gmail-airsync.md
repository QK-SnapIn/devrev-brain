---
title: Gmail AirSync
devrev_id: ART-22004
parent_directory: AirSync
translation_group: 6xVVbQpB
modified_date: "2026-01-05T05:56:36.653Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/6xVVbQpB"
tags: []
top_category: Computer by DevRev
wiki_match: glossary/airsync
match_score: 0.85
last_updated: 2026-05-11
related: ['glossary/airsync']
summary: "The Gmail AirSync enables seamless migration of emails from Gmail into DevRev, offering both one-time imports and ongoing sync capabilities."
---

# Gmail AirSync

The Gmail [[glossary/airsync|AirSync]] enables seamless migration of emails from Gmail into DevRev,
offering both one-time imports and ongoing sync capabilities.

## Supported objects

The following is a list of Gmail objects and their corresponding DevRev
equivalents. Those marked as Sync to DevRev are eligible for import from Gmail
to DevRev.

| **Gmail Object** | **DevRev Object** | **Sync to DevRev** |
| --- | --- | --- |
| Attachments | Attachments | ✅ |
| Labels | Tags | ✅ |
| Users | Identities | ✅ |
| Threads | [[features/chats|Chats]] | ✅ |
| Customers | Customers | ✅ |
| Messages | Comments | ✅ |

## Import from Gmail

Follow the steps below to import from Gmail:

1. Go to the **Marketplace**, [[features/search|search]] for **Gmail** in the **Import**
   category, and install.
2. Go to the **Import** section in your settings left nav.
3. Click **+Import** and select the Gmail logo.
4. In the **Select Connection** dropdown, choose **Gmail**.If a connection already exists, you can reuse it; otherwise, click **Add
   Connection**.In the connection modal, click **Sign in with snap-in** (with the Gmail
   icon), enter a connection name, and proceed to **authorize via your Google
   [[entities/account|account]] using OAuth**.Provide the necessary permissions and click **Continue** to complete the
   setup.
5. Once the connection is established, select the email labels/folders you want
   to import and specify the DevRev [[entities/part|part]] where imported emails should reside.
   This starts the bulk import.

DevRev attempts to automatically map email metadata and participants to DevRev
fields. Some fields might require manual mapping.

The import time depends on the volume of emails being brought in and could range
from seconds to hours. Once the import is complete, your emails will become part
of Computer's Memory and be available in search context.

## Related wiki nodes
- [[glossary/airsync]]

## Source
- DevRev support [[entities/article|article]] [Gmail AirSync](https://support.devrev.ai/en-US/devrev/article/6xVVbQpB) (ART-22004)
