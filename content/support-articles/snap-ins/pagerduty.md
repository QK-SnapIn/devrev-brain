---
title: PagerDuty
devrev_id: ART-21990
parent_directory: Integrate
translation_group: cRJBvgPG
modified_date: "2025-12-10T06:57:47.13Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/cRJBvgPG"
tags: []
top_category: Snap-ins
wiki_match: entities/part
match_score: 0.615
last_updated: 2026-05-11
---

# PagerDuty

The PagerDuty snap-in integrates DevRev's incident management with the PagerDuty
platform. Synchronize the DevRev incident object with PagerDuty incidents using
the **PagerDuty** incident subtype. Create, update, and escalate incidents
seamlessly between the two.

This feature is currently in limited availability. If you would like to use it, please contact DevRev support.

## Installation

1. In DevRev, go to **Settings** > **Snap-ins** and click **Explore
   Marketplace** in the top-right corner.
2. In the DevRev marketplace, find **PagerDuty** and click **Install**.
3. Set-up the snap-in's configurations.
4. Click **Save** > **Install snap-in**.
5. Execute the `/pagerduty register-webhook` command in the snap-in
   **Discussions** tab. Upon successful start, you will see the message
   **Successfully registered DevRev webhook.**.

## Configuration

In **Configure**, the following configuration options are available:

* **PagerDuty API Token**: Set up the PagerDuty API connection: create or select
  your **Snap-in Service** connection with a **PagerDuty API Access Key**.
  Ensure that the API Access Key has a **Full** access level.

  If the configured API key has a **Read-only** access level, the PagerDuty snap-in will not be able to make changes on your PagerDuty instance. The DevRev webhook will also have to be manually set up on [PagerDuty Generic Webhooks - v3](https://support.pagerduty.com/main/docs/webhooks#add-a-v3-webhook-subscription-on-the-generic-webhooks-page).
  Make sure to select the desired scope and event subscriptions.
* **PagerDuty Services Rev Part**: Select the customer part that all your
  PagerDuty services serve when first created as DevRev runnables.

  + The snap-in creates and maps your PagerDuty services as runnable builder parts
    in DevRev. Builder parts always serve (are linked to) a specific customer
    part.
  + After snap-in installation, you can update each runnable builder part to serve a
    different customer part.
* **Default PagerDuty User Email** (optional): Specify a default PagerDuty user
  email to synchronize DevRev changes from non-PagerDuty users.

  + You will need a default PagerDuty user email for workflows and other
    automations to make changes in PagerDuty on behalf of this user.
  + A default email is required for non-PagerDuty users since all PagerDuty API
    calls need to contain a valid PagerDuty user email address.
* **Update PagerDuty Incident Priority**: Toggle whether the DevRev incident
  severity field should synchronize with the PagerDuty incident priority field.

  If toggled on, the PagerDuty priority name mapping for each DevRev severity
  value 0-4 must be provided.
* **Synchronize Incident Discussions and Notes**: Toggle whether the DevRev
  incident discussions should synchronize with the PagerDuty incident notes.
* **Update PagerDuty Incident Name**: Toggle whether PagerDuty incident titles
  should be updated with the respective DevRev incident's ID.

  The format is: **[INC-XXX] - Original Incident Title**.
* **Default PagerDuty Service Runnable Part** (optional): Specify the default
  runnable part to be used when no impacted part is selected on incident
  creation.

  Select a runnable part that is mapped to a PagerDuty service.
* **Default PagerDuty Escalation Policy ID** (optional): Specify the default
  selected escalation policy when delegating through the `/delegate` command.

  Enter the PagerDuty escalation policy ID.

## Removal

1. Execute the `/pagerduty unregister-webhook` command in the snap-in
   **Discussions** tab. Upon successful removal, you will see the message
   **Successfully unregistered DevRev webhook.**
2. **Remove** or **Deactivate** the snap-in.

## Source
- DevRev support article [PagerDuty](https://support.devrev.ai/en-US/devrev/article/cRJBvgPG) (ART-21990)
