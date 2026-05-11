---
title: BrowserStack AirSync
devrev_id: ART-22024
parent_directory: AirSync
translation_group: QktEkl3h
modified_date: "2025-12-12T20:26:54.597Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/QktEkl3h"
tags: []
top_category: Computer by DevRev
wiki_match: glossary/airsync
match_score: 0.85
last_updated: 2026-05-11
related: ['glossary/airsync']
---

# BrowserStack AirSync

Import your test cases, test runs, and test results from BrowserStack to DevRev.

## Supported objects

The following is a list of BrowserStack objects and their corresponding DevRev equivalent. Those marked as supported are eligible for import.

| BrowserStack object | DevRev object | Sync to DevRev |
| --- | --- | --- |
| Test Cases | Test Cases | ✅ |
|  | (Custom Object) |  |
| Test Runs | Test Runs | ✅ |
|  | (Custom Object) |  |
| Test Results | Test Results | ✅ |
|  | (Custom Object) |  |

## Import from BrowserStack

Follow the steps below to import from BrowserStack:

1. In **Marketplace**, search for **BrowserStack** under the **Import** category
   and select it.
2. In the snap-in config modal, click **Install** then go to **Integrations** >
   **Imports** in your settings left nav.
3. Click the **Import** button and select the BrowserStack tile in the **Start
   import** window.
4. Create a new connection to your BrowserStack account or use an existing one.To create the connection, you'll need to enter a **Subdomain**. This field is mandatory for AirSync to group imports from the same source system.It is recommended to use the instance of the BrowserStack workspace you want
   to import as the value of **Subdomain**.
5. Once the connection is established, select the BrowserStack project you want to
   import, and specify the DevRev part that should be used for any imported work.
   This initiates a bulk import of the selected site.
6. Click **Map fields** in the import row and configure filters, object mapping, or field
   mapping as necessary.While DevRev attempts to automatically map fields, you may be prompted to manually
   map indicated fields.

The duration of the import depends on the size of the BrowserStack workspace and the amount
of data being imported. For a workspace with only a few dozen items, it can take seconds,
while a workspace with hundreds of thousands of items may take a few days.

## Related wiki nodes
- [[glossary/airsync]]

## Source
- DevRev support article [BrowserStack AirSync](https://support.devrev.ai/en-US/devrev/article/QktEkl3h) (ART-22024)
