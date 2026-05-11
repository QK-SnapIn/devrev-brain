---
title: Instabug
devrev_id: ART-21984
parent_directory: Integrate
translation_group: -bgE7TbV
modified_date: "2025-12-10T06:57:43.071Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/-bgE7TbV"
tags: []
top_category: Snap-ins
wiki_match: glossary/vista
match_score: 0.615
last_updated: 2026-05-11
---

# Instabug

Seamlessly bring user feedback from Instabug into DevRev. DevRev's Instabug
integration enables you to create tickets or issues automatically when an
Instabug user creates a report, linking it to a specific part of your product,
assigning a default owner and optional tags.

For more information, refer to the [Instabug snap-in](https://devrev.ai/marketplace/instabug) on the DevRev marketplace.

## Let's set up Instabug for you

### Installation

1. Go to the **Snap-ins** section within your DevRev workspace settings.
2. Click **Explore Marketplace**.
3. Search for **Instabug** and click **Install** next to the **Instabug**
   snap-in.
4. In the DevRev app, configure the snap-in in **Settings** > **Snap-ins** >
   **Instabug**.

   * Optionally select the default owner for Instabug work items.
   * Select the default part for Instabug work items.
   * Optionally add default tags for Instabug work items.
   * Select the DevRev work item type (issue or ticket) for Instabug reports.
   * Click **Save** > **Install**
5. Go to the **Instructions** tab.

   * Copy the webhook URL found here.
6. Connect the DevRev webhook with Instabug.

   * Go to [Instabug](https://instabug.com) and login.
   * Select your application and environment.
   * In the left nav, click on **Settings**.
   * Click on **Integrations**.
   * Find **Webhook** and click on **Create**.
   * Enter the DevRev webhook URL which you copied in the previous step in the
     URL field.

## Source
- DevRev support article [Instabug](https://support.devrev.ai/en-US/devrev/article/-bgE7TbV) (ART-21984)
