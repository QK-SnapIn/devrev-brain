---
title: Send customized emails
devrev_id: ART-21947
parent_directory: Automate
translation_group: oiSCboZz
modified_date: "2025-12-10T06:57:20.845Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/oiSCboZz"
tags: []
top_category: Snap-ins
wiki_match: features/customization
match_score: 0.571
last_updated: 2026-05-11
---

# Send customized emails

The [**send customized emails**](https://marketplace.devrev.ai/marketplace/send-emails) snap-in automates email sending. Once activated, this operation becomes available in the Workflow builder, enabling the delivery of personalized messages.

## Configuration

1. Create a **SendGrid** account.
2. Generate an **API key**.
3. Create a SendGrid connection:
   a. Go to **Settings** > **Snap-ins** > **+ Connection**
   b. Select **SendGrid**.
   c. Add the **API key** and click **Save**.

## Installation

1. Install the [**send customized emails**](https://marketplace.devrev.ai/marketplace/send-emails) from the DevRev marketplace.
2. Open the Workflow Builder and locate the **send customized emails** action node.
3. Configure the node by selecting the SendGrid connection and providing inputs such as:

   * **Sender email**
   * **Recipient emails**
   * **Email body or email template name (use only one)**
   * **Fields to replace in the email template** for dynamic content substitution

   Use either the email body or the email template name, but not both. The email template name must match a template created in SendGrid. The **Fields to replace in the email template** allows dynamic value substitution. For example, if the HTML template contains `<p>{{Name}}</p>`, specifying `Name=ABC` in the field replaces `<p>{{Name}}</p>` with `<p>ABC</p>`.

## Limitations

* The total size of an email, including attachments, must be less than 30 MB.
* Each email can have a maximum of 1,000 recipients.
* The SendGrid API has a rate limit of 600 requests per minute per account or more (depending on the account subscription). Exceeding this limit results in rate limiting, where requests are delayed or rejected.

## Source
- DevRev support article [Send customized emails](https://support.devrev.ai/en-US/devrev/article/oiSCboZz) (ART-21947)
