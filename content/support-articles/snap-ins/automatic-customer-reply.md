---
title: Automatic customer reply
devrev_id: ART-21924
parent_directory: Automate
translation_group: qW8nBHfZ
modified_date: "2026-01-15T19:35:53.964Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/qW8nBHfZ"
tags: []
top_category: Snap-ins
wiki_match: features/customer-portal
match_score: 0.564
last_updated: 2026-05-11
summary: "The automatic customer reply snap-in provides the following functionalities:"
---

# Automatic customer reply

The [automatic customer reply](https://devrev.ai/marketplace/auto-reply) snap-in provides the following functionalities:

* Automatically reply on your behalf in the [[features/plug-widget|Plug Widget]].
* Send a custom button along with the automatic message.
* Collect the visitor's email address, if it does not exist in the system.

Depending on the requirement, these functionalities can be enabled or disabled.

## Installation

1. Install the [automatic customer reply snap-in](https://devrev.ai/marketplace/auto-reply) from the DevRev marketplace.
2. Select the workspace to install the snap-in, confirm installation, and click **Deploy snap-in**.
3. If you want to enable automatic customer response, turn on the **Enable automated reply** toggle.

   * In the **Automated reply** field, enter the text you want to send as an automated reply.
4. To define business hours, turn on the **Set business hours** toggle.

   * In the **Automated messages after business hours** field, enter the text you want to send as an automated reply.
   * Define **Business start hours**, **Business end hours**, **UTC offset**, and **Business days** in the respective fields.
5. To send a button, turn on the **Enable a custom button** toggle.

   * In the **Text displayed on custom button** field, enter the text to be displayed on the button. For example, Book a Demo, Meet with Us!, Let's Chat.
   * In the **Target URL for the custom button** field, enter the website you'd like to redirect to, such as Calendly, HubSpot [[entities/meeting|meetings]], Microsoft Bookings, or another site.
6. To collect unregistered email IDs, turn on the **Enable email collector** toggle.

   * In the **Placeholder text for email collector** field, enter the text to display in the email collector.
   * In the **Email collector submit button text** field, enter the text to display on the submit button.
7. Click **Save**.

If [[glossary/turing|Turing]] in your workspace is in Auto-response mode, [[glossary/don|don]]'t enable auto-customer reply or you'll send two messages to your customer. By using this snap-in, you can still request email addresses for enriching customer data, as well as contacting customers through the right channel if they drift off your website.

## Source
- DevRev support [[entities/article|article]] [Automatic customer reply](https://support.devrev.ai/en-US/devrev/article/qW8nBHfZ) (ART-21924)
