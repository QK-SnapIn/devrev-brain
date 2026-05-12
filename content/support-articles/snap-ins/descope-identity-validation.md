---
title: Descope identity validation
devrev_id: ART-21938
parent_directory: Automate
translation_group: XrGz1dw4
modified_date: "2025-12-10T06:57:14.79Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/XrGz1dw4"
tags: []
top_category: Snap-ins
wiki_match: features/identity
match_score: 0.85
last_updated: 2026-05-11
related: ['features/identity']
summary: "Creating delightful customer journeys starts with having reliable, validated user identities at every step."
---

# Descope identity validation

Creating delightful customer journeys starts with having reliable, validated user identities at every step. The [Descope snap-in for DevRev](https://devrev.ai/marketplace/descope-identity-validation) provides user email validation through OTP authentication right within your [[features/plug-widget|Plug widget]]. Authenticating users in context without any redirects provides a native experience.

This snap-in enables several use cases across teams such as:

* Providing clean, accurate lead data for marketing teams
* Routing qualified [[features/conversations-feature|conversations]] to sales teams
* Having consistent user identities across pre and post-signup processes

Ensuring your users are who they say they are helps streamline operations, save
time on frivolous conversations, and provide a secure and frictionless user
experience.

### User email validation

Authenticate users with the “possession factor” of their email [[entities/account|account]] with
one-time password (OTP) validation. Request the user for their email and have
them input the OTP within the [[glossary/plug|Plug]] widget.

## Make a new connection

1. Open the settings on your DevRev app and go to **Integrations** >
   **Snap-ins** > **Connections**.
2. This page shows all your existing integrations. In the top-right corner,
   Select **+ Connection**.
3. Create and select your Descope connection.

   * Follow the steps below to get your Descope Project ID

     + Sign Up on [Descope](https://www.descope.com/sign-up)
     + Go to **Settings > Projects**
     + Copy the **Project ID**

     ![Descope Project ID](don:core:dvrv-us-1:devo/0:artifact/4100653)

## Installing the Descope identity validation snap-in

1. Install the [Descope identity validation](https://devrev.ai/marketplace/descope-identity-validation) from the DevRev marketplace.
2. Select the workspace to install the snap-in, confirm installation, and click
   **Deploy snap-in**.
3. Update the snap-in configurations as needed.

   * Configure the initial message which would be shown to the user when they
     are asked for their email.
   * Customize the message that is shown to the user during OTP collection.
   * Customize the message that is shown to the user on successful verification
     of email.
   * You can trigger this either for all new conversations from an unverified
     user or when Computer is unable to deflect a [[entities/conversation|conversation]].

     + To activate the automation for every new conversation, toggle on **Send
       on Create**.
     + If you prefer the automation to only be triggered when Computer is unable
       to deflect a conversation, make sure you have selected the appropriate
       `turing_undeflected` tag, and toggle off **Send on Create**.

![Descope identity validation](don:core:dvrv-us-1:devo/0:artifact/4100658)

4. Click **Save** > **Next** and deploy the snap-in.

## Related wiki nodes
- [[features/identity]]

## Source
- DevRev support [[entities/article|article]] [Descope identity validation](https://support.devrev.ai/en-US/devrev/article/XrGz1dw4) (ART-21938)
