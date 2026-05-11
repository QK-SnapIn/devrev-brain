---
title: Jira Service Management AirSync
devrev_id: ART-22023
parent_directory: AirSync
translation_group: IBvW-Z2E
modified_date: "2026-01-28T21:42:59.863Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/IBvW-Z2E"
tags: []
top_category: Computer by DevRev
wiki_match: glossary/airsync
match_score: 0.85
last_updated: 2026-05-11
related: ['glossary/airsync']
---

# Jira Service Management AirSync

The Jira Service Management AirSync simplifies migration from Jira Service
Management to DevRev, supporting both one-time imports and ongoing syncs.

For more information, refer to the
[Jira Service Management AirSync snap-in](https://devrev.ai/marketplace/jsm) on
the DevRev marketplace.

## Supported objects

The following is a list of Jira Service Management objects and their
corresponding DevRev equivalent. Those marked as **Sync to DevRev** are eligible
for import/sync to DevRev from Jira Service Management.

|  |  |  |
| --- | --- | --- |
| Jira Object | DevRev Object | Sync to DevRev |
| Issue | Ticket | ✅ |
| Private Comment on Issue | Internal Comment on Ticket | ✅ |
| Public Comment on Issue | Customer Comment on Ticket | ✅ |
| Label on Issue | Tag on Ticket | ✅ |
| Link between Issues | Link between Tickets | ✅ |
| Attachment on Issue | Attachment on Ticket | ✅ |
| Status Category/States of Issue | State/Stage of Ticket | ✅ |
| Workflow of Issue | Stage Transition Diagram of Ticket | ✅ |
| User | DevUser | ✅ |
| Customer | Customer | ✅ |
| Organization | Account | ✅ |
| App User | SysUser | ✅ |
| Sprint | Sprint | ❌ |
| Filter | Vista | ❌ |
| Automation | Snap-in | ❌ |

## Migrate from Jira Service Management to DevRev

In this scenario, the intention is to replace Jira Service Management with
DevRev. Once the migration is complete, the work that was normally done in Jira
Service Management would continue in DevRev. This can also be used to evaluate
DevRev with real data.

To migrate from Jira Service Management to DevRev:

1. Perform a project import to migrate over an entire Jira
   Service Management project.
2. (Optionally) Perform a sync from Jira to DevRev
   to bring over changes made after the initial import. This step can be
   repeated as needed.

## Project import

To ease the transition from Jira Service Management to DevRev, you can import
your Jira Service Management projects into DevRev. The project import is a
1-time bulk import of a Jira project into DevRev. Once this import is complete,
further incremental syncs can also be made.

To import a Jira Service Management project, go to **Settings** >
**Integrations** > **AirSyncs** then select **AirSync** (or **Start AirSync** if it's your first).
From there, create a new connection to a Jira Service Management site or use an
existing connection if you already have one.

To create a new connection:

1. Choose the visibility (private/public).
2. Enter a connection name.
3. Input the subdomain from your Jira instance URL:
   `example-subdomain.atlassian.net/jira/servicedesk` >
   `example-subdomain`.
4. Enter the email address from an administrator of the Jira instance.
5. Enter an
   [Atlassian API token](https://id.atlassian.com/manage-profile/security/api-tokens)
   from the same administrator of the Jira instance.

Imports should be done using an administrator account on the external
source. This ensures all necessary permissions are available to complete the
import successfully.

Once the connection is established, select the project you wish to import. At
this point you are prompted to configure how to import the Jira Service
Management project.

### Set up the import recipe

A Jira Service Management project import is highly configurable, and the
configurations for a specific project import are referred to as the recipe.
DevRev tries to automatically and sensibly map your Jira Service Management
fields to corresponding fields in DevRev, but it may prompt you on how you want
to map certain fields.

Typically Jira Service Management projects contain multiple types: epics,
stories, bugs, and tasks are common; you can configure which types to import
from Jira Service Management.

### Sync from Jira Service Management to DevRev

After a successful import of a Jira Service Management project, you have the sync from Jira Service Management to DevRev option. This feature replicates any new issues and any new changes to previously imported issues.

To perform a one-time sync from Jira Service Management to DevRev, go to
**Settings** > **Integrations** > **AirSyncs**, find the previously imported
project, and select the ⋮ > **Sync to DevRev** option.

If the Jira Service Management project is created as **Private**, the
global Jira Service Management administrator can access its settings but can't
see the issues or most of the data (which can be checked by logging in and
trying to see the issues). To be able to access the issues, set the global Jira
Service Management administrator as a project administrator for that particular
project.

This overrides work's fields, even if they were changed in DevRev.

### Historical AirSyncs

To view currently running and previous AirSyncs from various sources, do the following:

1. Go to [**Settings** > **Integrations** > **AirSyncs**](https://app.devrev.ai/?setting=airsyncs).
2. Select the import you want to view.
3. Select the context menu (⋮) > **View Report**.

### Periodic sync

After successfully importing to DevRev, you have the option to enable a periodic sync. This allows for automatic synchronization with DevRev on a regular basis. By default, the sync occurs once an hour.

To configure periodic sync, follow these steps:

1. Go to [**Settings** > **Integrations** > **AirSyncs**](https://app.devrev.ai/?setting=airsyncs).
2. Locate the previously imported project.
3. Select the ⋮ > **Set Periodic Sync** option.

The **Enable automations for synced items** setting is optional and can be activated during periodic sync configuration. When enabled, newly created or updated items trigger events, which can initiate webhooks, notifications, Snap-ins, and other processes, as if the events originated directly in DevRev.

If this setting is disabled, updates will not trigger any event-driven processes. This behavior applies only to periodic syncs; no events are triggered during a first-time import or manual sync to or from DevRev.

### Delete import

This deletes any content created by the import, including users and works.

An import and all the content it creates can be deleted from DevRev. This can be useful when running POCs or to change the recipe used during the import. Once an import has been deleted, all the content it created gets deleted, even if they were modified in DevRev. It's possible to import the project again after its deletion.

To delete an import and all the content it created, go to [**Settings** > **Integrations** > **AirSyncs**](https://app.devrev.ai/?setting=airsyncs), find the previously imported project, and select ⋮ > **Delete Import**.

## AirSync Jira Service Management scope and limitations

The following is a list of AirSync Jira Service Management scopes and
limitations to keep in mind when performing a Jira Service Management AirSync.
In addition to these Jira-specific limitations, there are also some generic
[[support-articles/computer-by-devrev/airsync-overview#airsync-scope-and-limitations|AirSync scopes and limitations]].

### Attachments

* Attachments to comments in Jira Service Management are not transferred as
  attachments to comments in DevRev. They are transferred as attachments to the
  issues.

### Customers and organizations

* Tickets in DevRev can only be attached to a single customer, so if multiple
  organizations are linked to a Jira Service Management issue, the DevRev ticket
  is only linked to the first of them.
* Customers in DevRev can only belong to a single account, so if a customer is a
  part of multiple organizations in Jira Service Management, he will only be
  linked to one of them in DevRev.

### Connection

* The Jira Service Management user who authorizes the connection to Jira Service
  Management must be a site admin or the organization admin for AirSync to be
  able to collect the email addresses of users. Otherwise, Jira users are
  collected but they are created with generated email addresses. The DevRev
  admin can [[support-articles/computer-by-devrev/airsync-overview#manual-dev-user-merging|merge the user accounts manually]].

## Related wiki nodes
- [[glossary/airsync]]

## Source
- DevRev support article [Jira Service Management AirSync](https://support.devrev.ai/en-US/devrev/article/IBvW-Z2E) (ART-22023)
