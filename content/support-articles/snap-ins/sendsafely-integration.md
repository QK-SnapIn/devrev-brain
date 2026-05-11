---
title: SendSafely integration
devrev_id: ART-21989
parent_directory: Integrate
translation_group: 8hgg5ZKd
modified_date: "2025-12-10T06:57:46.569Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/8hgg5ZKd"
tags: []
top_category: Snap-ins
wiki_match: features/email-integration
match_score: 0.769
last_updated: 2026-05-11
related: ['features/email-integration']
---

# SendSafely integration

The SendSafely integration enables secure file sharing. This integration allows both agents and customers to upload files to SendSafely dropzones efficiently. Recipients are notified about file uploads within DevRev. It also offers managing the files and recipients from within the **Discussion** tab.

For more information, refer to the [SendSafely snap-in](https://marketplace.devrev.ai/sendsafely-integration) on the DevRev marketplace.

## Installation

1. Configure dropzones.

   a. In the SendSafely console, go to **Dropzones**.

   b. Create the desired number of dropzones and copy the **Dropzone Id**, **Dropzone Host URL**, and **Dropzone Validation Key**.
2. Generate API Keys.

   a. Go to **Edit Profile** > **API keys** in SendSafely.

   b. Create a new API key and copy the **Organization URL**, **API Key**, and **API Secret**.
3. Install the snap-in in DevRev.

   a. Go to the **Snap-ins** section within your DevRev workspace settings.

   b. Click **Explore Marketplace**.

   c. Search for **SendSafely Integration** and click **Install** next to the SendSafely Integration snap-in.

## Configure the snap-in

1. In the **Configuration** section, enter the default messages for the `Send file upload` and `Request file upload` surfaces.

   a. Enter the default message for the `Send file upload` surface.

   b. Enter the default message for the `Request file upload` surface.
2. For different dropzones per group:

   a. Add the group name or group ID.

   b. Enter the **Dropzone Id**, **Dropzone Host URL**, and **Dropzone Validation Key** for each group.

   If a group name or group ID is not present, the first **Dropzone Id**, **Dropzone Host URL**, and **Dropzone Validation Key** are used.
3. Enter the **Organization URL**, **API Key**, and **API Secret** from the SendSafely console.
4. If you want to save the uploaded files in DevRev, turn off the `Delete file after upload` toggle.
5. If you want to tag work items uniquely, select the desired tag for identification.
6. Click **Save** to apply the configuration, then click **Install**.
7. Copy the generated `webhook URL`.
8. In the SendSafely console, go to **Dropzone Configuration** > **Notification Settings**.
   a. Set it to use a webhook for notifications.
   b. Paste the copied `webhook URL` in the **Webhook URL** field.

## Using the integration

* To upload a file to the SendSafely dropzone, open any work item in DevRev. In the snap-in surfaces, click on **Send File Upload** and upload your file.
* To request a file from a customer, open any work item in DevRev. In the snap-in surfaces, click **Request File Upload**.

## Related wiki nodes
- [[features/email-integration]]

## Source
- DevRev support article [SendSafely integration](https://support.devrev.ai/en-US/devrev/article/8hgg5ZKd) (ART-21989)
