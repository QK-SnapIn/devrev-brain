---
title: Marker.io
devrev_id: ART-21983
parent_directory: Integrate
translation_group: v5fbKQXS
modified_date: "2025-12-10T06:57:42.479Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/v5fbKQXS"
tags: []
top_category: Snap-ins
wiki_match: features/airdrop
match_score: 0.533
last_updated: 2026-05-11
---

# Marker.io

Seamlessly bring user feedback from Marker.io into DevRev. DevRev's Marker.io
integration enables you to create tickets or issues automatically when a
Marker.io issue is created, linking it to a specific part of your product,
assigning a default owner, and adding tags.

Additionally, if you include the reporter's email in the Marker.io issues custom
data, and create DevRev tickets from Marker.io issues, you can configure the
snap-in to use this email to auto-fill the **Reported By** and **Customer
Workspace** fields in tickets. If no contact or accounts match the email, they
are automatically created.

## Installing the Marker.io integration snap-in

1. Install the [Marker.io](https://devrev.ai/marketplace/marker-io) from the
   DevRev Marketplace.
2. Configure the snap-in as needed.

   * (Optional) Select the default owner for Marker.io work items.
   * Select the default part for Marker.io work items.
   * Optionally add default tags for Marker.io work items.
   * Select the DevRev work item type (issue or ticket) for Marker.io reports.
   * Optionally add the reporter email field from Marker.io issues custom data.
   * Click **Save** > **Install**
3. Go to the **Instructions** tab.

   * Copy the webhook URL found here.
4. Connect the DevRev webhook with Marker.io.

   * Go to [Marker.io](https://app.marker.io) and log in.
   * Click on the project you want to integrate with DevRev.
   * Click on the settings icon.
   * Click on the **Webhooks** tab.
   * Enter the DevRev webhook URL that you copied in the previous step in the
     URL field.

## Source
- DevRev support article [Marker.io](https://support.devrev.ai/en-US/devrev/article/v5fbKQXS) (ART-21983)
