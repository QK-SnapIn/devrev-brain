---
title: Calendly
devrev_id: ART-21973
parent_directory: Integrate
translation_group: YCcMHZL_
modified_date: "2025-12-10T06:57:36.705Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/YCcMHZL_"
tags: []
top_category: Snap-ins
wiki_match: features/commands
match_score: 0.5
last_updated: 2026-05-11
---

# Calendly

## Integrate Calendly with DevRev

Streamline your scheduling process and optimize customer engagement with DevRev's powerful Calendly snap-in. It's designed to capture all your Calendly bookings and seamlessly integrate them into DevRev's system of record, ensuring no leads or appointments are missed.

## Let's set up Calendly for you

For more information, refer to the [Calendly](https://marketplace.devrev.ai/calendly) on the DevRev marketplace.

For the DevRev Calendly snap-in to work, you must have a Professional, Teams, or Enterprise plan.

### Install

1. Go to [**Settings** > **Integrations** > **Snap-ins**](https://app.devrev.ai/?setting=snap-ins).
2. Click **Explore Marketplace**.
3. Search for **Calendly** and click **Install** next to the Calendly snap-in.
4. In DevRev app, setup the connection in **Settings** > **Snap-ins** > **Connections** on top.

   * Search and choose an existing connection or create a new one by clicking **+ Connection**.
   * Select **Snap-In Secret** from the dowpdown list.
   * Give it a name and paste your Calendly personal access token in the **Secret** field. Toggle on **Make public** if you want to make the connection public for your organization.
5. Update the snap-in configurations as needed.
6. Deploy the snap-in.
7. Enter **/calendly register-webhook** in the snap-in's **Discussions** tab on the right.
8. In the **Discussions** tab, you see a message `Calendly integration completed` on successful start.

### How to uninstall

1. In the **Discussion** tab, enter **/calendly unregister-webhook** to unregister the webhook. A message is displayed **Calendly integration removed**.
2. Remove the snap-in.

## Source
- DevRev support article [Calendly](https://support.devrev.ai/en-US/devrev/article/YCcMHZL_) (ART-21973)
