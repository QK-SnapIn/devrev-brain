---
title: WhatsApp
devrev_id: ART-21979
parent_directory: Integrate
translation_group: UdY1CsSV
modified_date: "2025-12-10T06:57:40.099Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/UdY1CsSV"
tags: []
top_category: Snap-ins
wiki_match: features/chats
match_score: 0.615
last_updated: 2026-05-11
---

# WhatsApp

Using DevRev, you can connect with your customers through WhatsApp. This new communication channel allows your customers to reach out with their questions and concerns directly on WhatsApp. The messages from WhatsApp seamlessly appear in your DevRev Inbox, making it easy for you to manage all your customer conversations in one place. By adding WhatsApp to DevRev, you can streamline your support and offer a smoother experience to your customers.

For detailed information about WhatsApp for Business, refer to [WhatsApp Business Platform - Documentation](https://developers.facebook.com/docs/whatsapp/overview#about-the-platform)

## Prerequisites

1. **Create a business account:** Ensure you have a [Business Account](https://business.facebook.com/overview) in Meta Business Manager. For detailed information, refer to [creating a Business Account](https://m.facebook.com/help/1710077379203657) in Meta Business Manager.
2. **Number compatibility:** Ensure the designated number isn't linked to another WhatsApp account. If it is, either delete that account or [migrate your number](https://developers.facebook.com/docs/whatsapp/cloud-api/get-started/migrate-existing-whatsapp-number-to-a-business-account/) to a business account.
3. **Partner integration:** We work with 360dialog for WhatsApp Integration. If you have an existing WhatsApp for Business Account, follow the steps to [migrate to 360dialog](https://docs.360dialog.com/partner/account-setup/migrating-phone-numbers).

## Installing the WhatsApp snap-in

To use this snap-in, you'll need to connect your WhatsApp with Business API with DevRev.

1. Install [WhatsApp](https://devrev.ai/marketplace/whatsapp) from the DevRev marketplace.
2. Select the workspace to install the snap-in, confirm installation, and click **Deploy snap-in**.

## Limitations

* Group Conversations are not supported by WhatsApp for Business API.
* If you do not respond to the customer’s message within 24 hours, you can only respond to the conversation using Meta-approved template messages.

## Set up the snap-in

Follow these steps to ensure WhatsApp messages sent to your business are synced with the DevRev Inbox.

1. **Install the snap-in:** Install the WhatsApp snap-in from the marketplace as mentioned above.
2. **Create a connection:** In the **Connections** tab, add your existing connection or create a new connection.

   * Give your connection a name, and ensure that you completed the required steps in the prerequisites.
   * Click **Connect**.
   * ![whatsapp](don:core:dvrv-us-1:devo/0:artifact/4100835)

     Open the dialog and follow the process to finish creating a connection.
3. **Configure business phone number:** In the **Configuration** tab, enter the business phone number to sync WhatsApp messages sent to the business with DevRev Inbox.
4. **Register for WhatsApp webhook:** In the **Discussion** tab, enter **/whatsapp** to register to the WhatsApp webhook URL to receive WhatsApp messages in the DevRev Inbox.
5. **Use template messages:** As per WhatsApp policies, template messages are required to communicate with customers once 24 hours have passed since their last message. To ensure continuity in customer conversations, the following template messages are sent for Meta approval:

   * **Reinitiate missed conversation:** "Hi, sorry for not responding earlier. (Custom Message)"
   * **Share an update with the customer:** "Hi, here is an update (Custom Message)"

## Source
- DevRev support article [WhatsApp](https://support.devrev.ai/en-US/devrev/article/UdY1CsSV) (ART-21979)
