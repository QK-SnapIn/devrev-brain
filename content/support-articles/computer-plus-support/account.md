---
title: Account
devrev_id: ART-21879
parent_directory: Customer records
translation_group: x368dZAr
modified_date: "2026-01-01T12:01:48.613Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/x368dZAr"
tags: []
top_category: Computer+ Support
wiki_match: entities/account
match_score: 1.0
last_updated: 2026-05-11
related: ['entities/account']
summary: "An account represents a customer organization, and it holds information about the company, including its name, address, industry, domain, and website address."
---

# Account

An [[entities/account|account]] represents a customer organization, and it holds information about the company, including its name, address, industry, domain, and website address.

[[features/accounts|Accounts]] are associated with a workspace. An account can be a [[entities/part|part]] of multiple workspaces at the same time. An account can also be linked to multiple [[entities/opportunity|opportunities]]. Accounts help you keep track of your customer contacts. Contacts are always linked to a workspace or an account.

## Create an account

You can create accounts in the following ways:

### Using the DevRev app

1. Go to[**Explore > Accounts**](https://app.devrev.ai/?vista=vista-def-accounts), and click \*\*+ Account\*\*.
2. Fill in the details like account name, description, websites, domains, type, annual revenue, forecast category, tags, and tier.
3. Fill in the required fields like external references and owner of the account.
4. Click \*\*Create\*\*.

### Bulk import accounts

To bulk import accounts, see [[support-articles/computer-plus-support/account-and-contact-import|Account and contact import]].

You can also use [[support-articles/computer-by-devrev/airsync-overview#account-deduplication|AirSync]] to migrate your accounts from various platforms such as HubSpot, Salesforce, Zendesk, Jira, Linear, ServiceNow, and more.

### Using DevRev APIs

You can create an account using the `accounts.create` API. Follow the [Create accounts and contacts in DevRev](https://developer.devrev.ai/beta/guides/create-accounts-and-contacts-in-dev-rev) tutorial.

### Account attributes

Accounts have attributes that can be used to filter them. You can find all the stock attributes listed under [**Settings** > **Object customization** > **Account**](https://app.devrev.ai/?setting=object-customization?type=account), and click > **Stock fields**.

These are the stock attributes that come with DevRev:

* **Domains**: Domain names associated with the company to help map contacts to accounts when a contact isn't already linked. Use the format: '[subdomain].domain.com'
* **External references**: Identifier for this company from your primary customer record, for example, company domain or account ID. This is used to match customer [[features/identity|identity]] across channels to one record.
* **Created by**: The user who created the account.
* **Created date**: The date the account was created.
* **Modified by**: The user who last modified the account.
* **Modified date**: The date the account was last modified.
* **Owners**: The users who are responsible for the account.
* **Tags**: Tags are used to categorize accounts.
* **Tier**: You can add Tier 1, Tier 2, and Tier 3 to classify accounts.
* **Subscribers**: Users who are notified of changes to the account.

### External reference

While ingesting accounts into DevRev, account information coming across channels must be matched to the same record.For example, an account created by you using APIs should get resolved and matched when a customer contact is created under the account and it should not create a duplicate account.

This is achieved by using the *external reference* provided by you when creating an account.

**External reference for an account**
A unique identifier for the account from your primary customer record. If none is available, a good alternative is the customer’s company domain. If none is specified, a system-generated identifier is assigned to the account.

For ingestion channels where providing an external reference isn't possible, the system relies on custom logic to identify and match incoming customer identity.

Example: The Slack and [[features/email-integration|Email integration]] uses a combination of the customer `email` and workspace `domain_name` values. WhatsApp uses the WhatsApp number and associated name.

## Add a workspace

To add a workspace to an account, go to **Account** > **Workspace** and select **New workspace**.

## Related wiki nodes
- [[entities/account]]

## Source
- DevRev support [[entities/article|article]] [Account](https://support.devrev.ai/en-US/devrev/article/x368dZAr) (ART-21879)
