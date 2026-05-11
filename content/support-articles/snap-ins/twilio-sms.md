---
title: Twilio SMS
devrev_id: ART-22934
parent_directory: Integrate
translation_group: ILdKGQ7j
modified_date: "2026-02-12T04:25:40.441Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/ILdKGQ7j"
tags: []
top_category: Snap-ins
wiki_match: glossary/trails
match_score: 0.5
last_updated: 2026-05-11
---

# Twilio SMS

To establish a single source of truth for all customer issues, DevRev has integrated with Twilio to capture support requests made via phone. Customers can now share their concerns by sending an SMS to the designated Twilio support number. Each SMS automatically creates a support conversation and caller identity, allowing the support team to maintain complete context around the customer's issue.

## Prerequisites

Before installing the Twilio SMS snap-in, ensure you have the following:

1. A Twilio account.
2. Twilio account SID and the authentication token.

   These details can be found on the [Twilio Console](https://console.twilio.com/) dashboard under **Account Info**.

## Installing the Twilio SMS snap-in

Follow these steps to install the Twilio SMS snap-in:

1. In DevRev, go to **Settings > Integrations > Snap-ins**.
2. In the All Snap-ins, find **Twilio-sms** and click **Add**.

## Configure the Twilio SMS snap-in

Follow these steps to ensure that the customer SMS received via Twilio are synced with DevRev conversation.

1. **Configure the connection**  
   On the **Snap-ins** > **Connections** tab, either add an existing connection or create a new connection by clicking **+ Connection** and providing a name.
2. **Provide credentials**  
   Provide the Twilio account SID and the authentication token.
3. **Fill in configuration details**  
   In the Configurations tab, fill in the following details:

   * **Twilio Phone number**: The phone number to send the reply back to the contact via Twilio from DevRev Conversation.
   * **Default Part**: Select the default part that will be assigned to the conversation that is created by SMS received on the configured phone number.
4. **Configure Twilio webhook**  
   After configuring, an Instruction Page will appear. Follow the steps below:

   1. Log in to your [Twilio Console](https://console.twilio.com/) and go to **Phone Numbers** > **Manage** > **Active Numbers**.
   2. Select the phone number registered for this Snap-in.
   3. On the Configure page, scroll to the **Messaging Configuration** section.
   4. Under **A Message Comes In**, select **Webhook** from the dropdown.
   5. Copy the Source URL and paste it into the URL input field.
   6. Set the HTTP Method to **POST** and click **Save Configuration**.

Once the Snap-in configuration is complete, any user who sends an SMS to the configured Twilio phone number will automatically create a support conversation in DevRev. The support team can then respond directly to the user through the same Twilio phone number.

## Limitations

* From DevRev to Twilio, only **plaintext** and **hyperlink** formats are supported for agent messages.
* Editing existing comments is not supported and will not be reflected in Twilio.

## Source
- DevRev support article [Twilio SMS](https://support.devrev.ai/en-US/devrev/article/ILdKGQ7j) (ART-22934)
