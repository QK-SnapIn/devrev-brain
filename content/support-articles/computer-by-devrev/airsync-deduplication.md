---
title: AirSync deduplication
devrev_id: ART-21891
parent_directory: AirSync
translation_group: dscRaUbH
modified_date: "2025-12-10T06:56:45.494Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/dscRaUbH"
tags: []
top_category: Computer by DevRev
wiki_match: glossary/airsync
match_score: 0.85
last_updated: 2026-05-11
related: ['glossary/airsync']
---

# AirSync deduplication

## User deduplication

When migrating data, ensuring the accuracy and consistency of the data is paramount. This section describes how AirSync handles potential duplicates and the processes that can be used to clean up duplicates.

[Users]([[support-articles/computer-by-devrev/core-concepts|Core concepts]]#identity) are team members, specifically, they're considered members of the DevRev organization. Examples of AirSync-created users include engineers working on imported Jira issues, support agents who own imported Zendesk tickets, and account owners for imported HubSpot accounts.

When importing external users, the email address is used as a means of deduplication.

### Scenarios

# User has no email or it's not accessible

A new user is created in DevRev. This user is marked as *Unassigned*. Unassigned users can't log in and have no access to DevRev. All work, comments, and assignments imported from the external source and associated with the external user are associated with the unassigned DevRev user.

This user can be manually merged with an existing user.

# User has an email but doesn't match any existing DevRev user email

A new user is created in DevRev. This user is marked as *Shadow*. Shadow users cannot log in and have no access to DevRev. All work, comments, and assignments imported from the external source and associated with the external user are associated with the shadow DevRev user.

If a new user joins DevRev and that user's email matches the email of the shadow user, the person joining assumes the existing shadow user. The shadow user is marked as active and can access DevRev. All the work, comments, and assignments remain with the now-active user.

This user can be manually merged with an existing user.

# User has an email that matches an existing DevRev email

No new user is created in DevRev. All work, comments, and assignments imported from the external source are associated with the existing DevRev user with the matching email.

### Merge users manually

There are cases where the automatic AirSync user deduplication logic doesn't catch duplicates. This can happen when an imported user has no email address or the email address doesn't match that of an existing user in DevRev. In these cases, a DevRev admin can manually resolve these duplicate entries after the AirSync import.

To do this, find the duplicated AirSync-created user and merge it with the desired active DevRev user.

1. Be a DevRev admin.
2. Find the duplicated AirSync-created user.
3. Merge the duplicated AirSync-created user with the desired active DevRev user.

# Find duplicated AirSync-created user

You can find AirSync-created users that weren't deduplicated into an existing user with a few different methods.

To find users, perform a user search (CMD-K/Ctrl-K). You can search by name or email and in some cases by unique external ID (such as Jira user ID). From there, you can either:

* Select the user in imported records. Select users on records, such as an imported issue they own.
* Find the user in the users list. Go to **Settings** > **User Management** > **Users** and filter by *Unassigned* and *Shadow* users.

# Merge duplicated user

The merge user option is only available from *Unassigned* and *Shadow* users with *Active* users and must be performed by a DevRev admin. The merge option will move all records owned by the unassigned/shadow user to the active user. The unassigned/shadow user will be deactivated, and any future imported items will be assigned to the active user.

Timeline events, such as comments made or actions taken in existing records, aren't updated and continue to reference the now-deactivated user.

To perform a merge:

1. Open the list of *Unassigned* or *Shadow* users.
2. Select the action ⋮ menu > **Merge User**.
3. Find the *Active* user you wish to merge with.

## Account deduplication

DevRev accounts help you keep track of your [customers](https://app.devrev.ai/devrev/settings/knowledge-base/articles/ART-21881). AirSync can import accounts from various external sources. Accounts from external sources can have varying names, such as companies in HubSpot, organizations in Zendesk, or accounts in Salesforce.

An AirSync doesn't deduplicate imported accounts; rather, it modifies them so that new accounts don't violate DevRev constraints. These accounts can be merged after the import has been completed. Since DevRev has several constraints on the uniqueness of different DevRev account fields, AirSync avoids breaking these constraints by following these rules when another account is already using the unique value:

|  |  |
| --- | --- |
| Account Field | Rule |
| Display Name | The imported account display name is appended with a unique external ID. |
| External Reference(s) | Conflicting imported account external reference dropped. |
| Domain(s) | Conflicting imported account domain dropped. |
| Website(s) | Conflicting imported account website dropped. |

### Merge accounts manually

Accounts, whether natively created in DevRev or migrated via AirSync, can be merged by a DevRev administrator.

To perform a merge:

1. Open the account you want to merge from. This account will be the one that will be deleted.
2. Select **Merge** from the account action menu (⋮).
3. In the **Merge** dialog, select the account to merge into.

   * All associated discussions with the account you want to merge from will be deleted.
   * All associated users, conversations, tickets, and workspaces are preserved in the account to be merged with.
   * Any future items synced via AirSync (such as new users or tickets) associated with the account you want to merge from will be associated with the account to be merged with.
4. Click **Merge**.

## Contact deduplication

DevRev contacts help you keep track of your [customers](https://app.devrev.ai/devrev/settings/knowledge-base/articles/ART-21881). Contacts are the individual users, which may or may not be associated with an account. DevRev contacts aren't globally unique. The same user may have multiple contact records.

AirSync imported contacts are deduplicated against existing contacts. The user email is used as the deduplication field. The deduplication happens at the account level. Contacts without an account are treated as being in the same pseudo-account. When a contact is deduplicated, the records and comments of the incoming contact are associated with the existing contact.

The following scenarios illustrate how this AirSync contact deduplication mechanism works:

|  |  |  |
| --- | --- | --- |
| Existing Contact | Incoming Contact | Result |
| email: [a@example.com](mailto:a@example.com) account: **None** | email: [a@example.com](mailto:a@example.com) account: **None** | Existing contact used |
| email: [a@example.com](mailto:a@example.com) account: "Example" | email: [a@example.com](mailto:a@example.com) account: "Example" | Existing contact used |
| email: [a@example.com](mailto:a@example.com) account: "Example" | email: [a@example.com](mailto:a@example.com) account: **None** | New contact created |
| email: [a@example.com](mailto:a@example.com) account: **None** | email: [a@example.com](mailto:a@example.com) account: "Example" | New contact created |

### Work deduplication

AirSync doesn't deduplicate work objects (issues, tickets, opportunities). Unlike identity objects (users, accounts), these objects do not typically have duplicates in other systems.

## Related wiki nodes
- [[glossary/airsync]]

## Source
- DevRev support article [AirSync deduplication](https://support.devrev.ai/en-US/devrev/article/dscRaUbH) (ART-21891)
