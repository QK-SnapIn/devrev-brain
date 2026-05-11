---
title: Datadog
devrev_id: ART-21975
parent_directory: Integrate
translation_group: hsqoeCOm
modified_date: "2025-12-10T06:57:37.808Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/hsqoeCOm"
tags: []
top_category: Snap-ins
wiki_match: features/updates-feed
match_score: 0.421
last_updated: 2026-05-11
---

# Datadog

This automation creates a link between Datadog and DevRev. When a new incident
is created on Datadog or an existing incident is updated, the webhook is
triggered and a payload is sent over to DevRev. Using this payload, a new
incident is created and the existing incident is updated on DevRev. Similarly,
when a new incident is created or an existing incident is updated in DevRev,
DevRev webhook is triggered and corresponding changes are reflected in Datadog.
Timeline entries are synced one-way—from DevRev to Datadog.

## Installation

1. Open the DevRev marketplace and install the **Datadog** snap-in.
2. Select the workspace where you want to install the snap-in, confirm your
   selection, and click **Deploy snap-in**.
3. In DevRev app, setup the connection in **Settings** > **Snap-ins** >
   **Connections** on top.

   * Search and choose an existing connection or create a new one by clicking
     **+ Connection**.
   * Select **Datadog** from the dropdown list.
   * Give it a connection name and paste your Datadog **API Key**, **Application
     Key** and **Environment** (production or development) in their respective fields.

## Configuration

1. Go to **Snap-ins** > **All Snap-ins** > **Datadog** > **Configure**.
2. In the **Connections** tab, select the connection that you created.

This connection is necessary if you wish to bring stage and custom
fields to DevRev.

3. Select the part, and default severity value for incidents. This default
   incident value is used when the Datadog incident has `UNKNOWN` severity.
4. Include the desired severity mapping from Datadog to DevRev and vice versa.
5. Include the desired stage mapping from Datadog to DevRev and vice versa.

Multiple DevRev stages can be mapped to single state in Datadog. In such
cases, please provide comma separated values.

6. Include the custom fields that you wish to bring to DevRev from Datadog and
   vice versa. For multiple fields, provide comma-separated values.

The custom fields included in the input field while configuration must
be created in DevRev. The field type must be either `textbox` or `dropdown` in
Datadog.

7. If you wish to sync incidents from DevRev back to Datadog, click the **Enable Reverse Sync** button.
8. Click **Save** and **Install**.
9. Copy the webhook URL and follow the below steps to connect it to Datadog via
   webhook integration.

   a. Go to **Integrations** > **Webhooks** and click **Install** or
   **Configure**.

   b. On the **Configuration** tab, enter a **Name** for the webhook and the
   webhook **URL**.

   c. Add the following payload in the **Payload** section.

   ```
   {
     "aggreg_key": "$AGGREG_KEY",
     "alert_metric": "$ALERT_METRIC",
     "alert_query": "$ALERT_QUERY",
     "alert_scope": "$ALERT_SCOPE",
     "alert_status": "$ALERT_STATUS",
     "alert_transition": "$ALERT_TRANSITION",
     "alert_type": "$ALERT_TYPE",
     "alert_url": "$LINK",
     "event_id": "$ID",
     "event_message": "$EVENT_MSG",
     "event_title": "$EVENT_TITLE",
     "event_type": "$EVENT_TYPE",
     "hostname": "$HOSTNAME",
     "incident_commander": "$INCIDENT_COMMANDER",
     "incident_message": "$INCIDENT_MSG",
     "incident_title": "$INCIDENT_TITLE",
     "logs_sample": "$LOGS_SAMPLE",
     "public_id": "$INCIDENT_PUBLIC_ID",
     "snapshot_url": "$SNAPSHOT",
     "tags": "$TAGS",
     "timestamp": "$DATE"
   }
   ```

   d. Click **Install Integration** or **Update Configuration**.

   e. Go to **Incidents** > **Settings** > **Notification Rules** and click **Add New Rule**.

   f. Choose **Declared or Updated** to notify the webhook when the incident is
   both declared and updated.

   g. Add the webhook **Name** followed by **@webhook-** in the **Notify**
   field.

   h. Select the fields that needs to be updated when the notification is sent,
   in the **Renotify on updates to** field.

   i. Click **Save** to enable the notification rule.

Once the above setup is complete, file a support ticket with DevRev to enable
the Incident object in your workspace.

## Source
- DevRev support article [Datadog](https://support.devrev.ai/en-US/devrev/article/hsqoeCOm) (ART-21975)
