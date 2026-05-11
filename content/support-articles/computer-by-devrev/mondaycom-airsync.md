---
title: Monday.com AirSync
devrev_id: ART-22005
parent_directory: AirSync
translation_group: Ulrl_ER7
modified_date: "2026-04-06T07:07:31.318Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/Ulrl_ER7"
tags: []
top_category: Computer by DevRev
wiki_match: glossary/airsync
match_score: 0.85
last_updated: 2026-05-11
related: ['glossary/airsync']
summary: "The Monday.com AirSync simplifies migration from Monday.com to DevRev, supporting both one-time imports and ongoing sync."
---

# Monday.com AirSync

The Monday.com [[glossary/airsync|AirSync]] simplifies migration from Monday.com to DevRev, supporting both one-time imports and ongoing sync.

## Supported Objects

The following is a list of Monday.com objects and their corresponding DevRev equivalents. Those marked as Sync to DevRev are eligible for import from Monday.com to DevRev.

| **Monday.com object** | **DevRev object** | **Sync to DevRev** |
| --- | --- | --- |
| Workspaces | [[entities/part|Part]] | ✅ |
| User | DevUser | ✅ |
| Items | [[entities/issue|Issue]] | ✅ |
| Updates | comments | ✅ |
| Reply | Threads | ✅ |
| Assets | Attachments | ✅ |
| Tags | Tags | ✅ |

## Importing from Monday.com

Follow the steps below to import from Monday.com:

1. **Install the ****[DevRev App](https://auth.monday.com/oauth2/authorize?client_id=212704ea280506d48d3a0a8957e34e4c&response_type=install))**** on ****[Monday.com](http://Monday.com)****.** 
Before creating a connection, you must install the DevRev app in your [Monday.com](http://Monday.com) [[entities/account|account]] to authorize the required OAuth scopes.

Click the link below and select **Install**:

Install [DevRev App](https://auth.monday.com/oauth2/authorize?client_id=212704ea280506d48d3a0a8957e34e4c&response_type=install)) on [Monday.com](http://Monday.com)
If the link above does not work, copy and paste the following URL into your browser:
`https://auth.monday.com/oauth2/authorize?client_id=212704ea280506d48d3a0a8957e34e4c&response_type=install`

 **Note:** Skipping this step may result in a scope authorization error while establishing the OAuth connection.

2. Go to the **Marketplace** and [[features/search|search]] for **[Monday.com](http://Monday.com)** in the **Import** category and install it.
3. In the snap-in configuration modal, click **Install**.
4. Go to **Settings > Integrations > AirSyncs** from the left navigation panel.
5. Click **AirSync** and select the **[Monday.com](http://Monday.com)** connection.
6. Create a new connection to your [Monday.com](http://Monday.com) account, or use an existing connection if you already have one.
7. Once the connection is established, select [Monday.com](http://Monday.com) and specify the DevRev part that should be used for the imported work. This initiates a bulk import of the selected account.
8. DevRev attempts to automatically map fields from [Monday.com](http://Monday.com) to the corresponding fields in D

## Related wiki nodes
- [[glossary/airsync]]

## Source
- DevRev support [[entities/article|article]] [Monday.com AirSync](https://support.devrev.ai/en-US/devrev/article/Ulrl_ER7) (ART-22005)
