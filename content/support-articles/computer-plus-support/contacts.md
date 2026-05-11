---
title: Contacts
devrev_id: ART-21881
parent_directory: Customer records
translation_group: V75TgHpU
modified_date: "2025-12-10T06:56:39.336Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/V75TgHpU"
tags: []
top_category: Computer+ Support
wiki_match: features/accounts
match_score: 0.625
last_updated: 2026-05-11
---

# Contacts

Contacts in DevRev identify your customers which are a crucial part of the DevRev offering and ecosystem. Conversations on DevRev rely on customer identity to capture information about the customer initiating the conversation. Similarly, tickets on DevRev can capture who the ticket was reported by (or reported for).

## Concepts

Customer identity in DevRev includes the following important constructs:

* **External User/contact**: Your end user or customer or users associated with organization Accounts or Workspaces.
* **Account/workspace**: Any logical grouping that an external user is part of. It could represent a customer account for your B2B product (for example Stripe as a customer of Slack) or a workspace in your software product (such as a Slack workspace).

## Create a new customer contact

1. Go to [**Explore** > **Contacts**](https://app.devrev.ai/?vista=vista-def-contacts), and click **+ Contact**.
2. Fill in the following fields as **Add Display Name, Description, Domains, Tags, Tiers**.
3. Click **Create**.

While creating new customer records, be sure to specify the **External Reference** so customer information coming from other channels (like Plug, email, and WhatsApp) can be matched to the right customer record.

![Creating a new customer](don:core:dvrv-us-1:devo/0:artifact/4100323)

You can create a contact using DevRev's `rev-users.create` API. Follow the [Create accounts and contacts in DevRev](https://developer.devrev.ai/beta/guides/create-accounts-and-contacts-in-dev-rev#create-a-contact) tutorial.

### Bulk import customer records

To bulk import customer records, see [[support-articles/computer-plus-support/account-and-contact-import|Account and contact import]].

You can also use [AirSync]([[support-articles/computer-by-devrev/airsync-overview|AirSync overview]]#contact-deduplication) to migrate your customer contacts from various platforms such as HubSpot, Salesforce, Zendesk, Jira, Linear, ServiceNow, and more.

Customer records offer a place to do the following:

* Find all conversations and tickets linked to a customer in one view.
* Have internal discussions related to a customer.
* Add description or notes about a customer.
* Assign an owner or tags to the customer.

![Customer view](don:core:dvrv-us-1:devo/0:artifact/4100324)

Apart from customer records that get automatically created from your [[support-articles/customer-support-agent/customer-support-agent-overview|Plug integration]], new customer records can be created through the app.

### Contact attributes

Contacts have attributes that can be used to filter them.
You can find all the stock attributes listed under [**Settings** > **Object customization** > **Contact**](https://app.devrev.ai/?setting=object-customization?type=revu), and click > **Stock fields**.
These are the stock attributes that come with DevRev:

* **Email**: The email address associated with the contact.
* **External reference ID**: Identifier for this company from your primary customer record, for example, company domain or account\_id. This is used to match customer identity across channels to one record.
* **Created date**: The date the contact was created.
* **Verified**: Indicates whether the contact has been verified.
* **Phone numbers**: The phone number associated with the contact.
* **Customer**: Account or workspace this contact is associated with.
* **Tags**: Tags are used to categorize contacts.

These attributes can be effectively used in filters and **Group** conditions across various vistas in DevRev to track specific work, capacity, and more.

You can add custom attributes to opportunities to track additional information. For more information on custom attributes, see [[support-articles/computer-by-devrev/object-customization|object customization]].

### External reference

While ingesting customer identity into DevRev, customer information coming across channels must be matched to the same record.For example, a customer record created by you using APIs should get resolved and matched when the same customer engages with you on the Plug widget for a support interaction.

This is achieved by using the *external reference* provided by you when creating customer identity.

**External reference for a customer**
A unique identifier for an end user from your primary customer record. The system uses this to resolve a newly created customer with customers already in the system.If none is available, a good alternative is the email address or phone number that could uniquely identify the user.If none is specified, a system-generated identifier is assigned to the user.

For ingestion channels where providing an external reference isn't possible, the system relies on custom logic to identify and match incoming customer identity.

Example: The Slack and Email integration uses a combination of the customer `email` and workspace `domain_name` values. WhatsApp uses the WhatsApp number and associated name.

### Identity ingestion

The identity of your customers can be brought to the DevRev system in multiple ways.

**Plug**Your Plug integration automatically brings customer identity to DevRev with each widget conversation.

Workspace and external user information provided as part of the [Plug integration](https://developer.devrev.ai/sdks/web/user-identity) identifies or creates corresponding customer identity in the DevRev system and links it to Plug conversations.

**Integrations**DevRev's integrations like [Slack](https://devrev.ai/marketplace/slack), [Email for conversations](https://marketplace.devrev.ai/marketplace/devrev-plug-with-email), [WhatsApp](https://devrev.ai/marketplace/whatsapp) are additional channels available with DevRev's omnichannel support offering.
Integrating these channels automatically brings customer identity to DevRev.

## Source
- DevRev support article [Contacts](https://support.devrev.ai/en-US/devrev/article/V75TgHpU) (ART-21881)
