---
title: User management
devrev_id: ART-21894
parent_directory: Access control
translation_group: uNlA_ZjU
modified_date: "2026-05-06T19:44:53.608Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/uNlA_ZjU"
tags: []
top_category: Computer by DevRev
wiki_match: features/incidents
match_score: 0.706
last_updated: 2026-05-11
related: ['features/incidents']
---

# User management

User groups contain your internal team members – the people inside your organization who build, support, and sell your product. They control what your internal team can do; that is, permissions for accessing and acting on objects like tickets, issues, and parts within the DevRev app.

## Default user groups

The following are the default user groups in a workspace:

* **Admins:** All workspace admins.
* **All Users:** A dynamic group containing all users in the workspace. Because this group is dynamic, its membership is managed automatically and cannot be manually edited.
* **Platform Users:** All internal members of the workspace. Any new member is added to this group by default.
* **Support:** All members of the support team, which may include customer success and sales. Only members of this group receive updates about conversations in the Plug inbox.
* **Agent and Automations Admin:** This group includes privileges to manage agents, workflows, snap-ins, commands, and related automation resources.

## Dynamic and static groups

Admins can add or remove members from any static group. A dynamic group determines membership automatically based on rules and expressions rather than manual assignment. Members are added or removed as they meet or stop meeting the defined criteria. You cannot manually edit the member list of a dynamic group.

For a detailed explanation of how dynamic groups work, including expression syntax and use cases, see [[support-articles/computer-by-devrev/groups|Groups]].

## User group management

### Create a new user group

You must be an admin to create a group.

1. In [**Settings** > **User Management** > **Groups**](https://app.devrev.ai/?setting=groups), click **+ Create new**.
2. Fill in the group details such as name and description and select the method for adding customers.
3. For a static group, add users by email or name.
4. For a dynamic group, define the filter rules or expressions that determine which users are automatically included (for example, filtering by department, role, or custom attribute).

![group creation](don:core:dvrv-us-1:devo/0:artifact/4100358)

### Update a user group

The name, type, and description of default groups cannot be edited. However, you can add or remove members from default static groups such as Support and Agent and Automations Admin.

1. In [**Settings** > **User Management** > **Groups**](https://app.devrev.ai/?setting=groups), select the group you want to update.
2. Click **Edit**.
3. Make your changes and save.

![update group](don:core:dvrv-us-1:devo/0:artifact/4100361)

### Modify membership of a static group

1. In [**Settings** > **User Management** > **Groups**](https://app.devrev.ai/?setting=groups), select the static group.
2. To add a user, click **Add Users** and enter the email addresses or names of the customers to add.
3. To remove a user, find the member you want to remove in the list view and click the cross button (⨯) next to the member's name.

## User invitations

Only admins can invite users to the workspace. If you are not an admin, the **Invite** button is not displayed.

For organizations using SSO or identity provider (IDP) provisioning, users can be provisioned automatically without manual invitation. Contact your workspace admin for details on configuring IDP-based provisioning.

### Invite users to the workspace

1. In [**Settings** > **User Management** > **Invitations**](https://app.devrev.ai/?setting=invitations), click **+ Invite**.
2. In the **To** field, enter the email addresses of the users to invite.
3. In the **Add to groups** field, add the required group. **Platform Users** is pre-filled by default.
4. Click **Send Invite** to dispatch the invitation emails.

![invite users](don:core:dvrv-us-1:devo/0:artifact/4100365)

### Manage invitations

After sending invitations, you can review their status and take further action from [**Settings** > **User Management** > **Invitations**](https://app.devrev.ai/?setting=invitations).

* **Check pending invitations:** The Invitations page lists all outstanding invitations along with their status (pending, accepted, or expired).
* **Resend an invitation:** If a recipient has not accepted their invitation, select the pending invitation and click **Resend** to send a new email.
* **Revoke an invitation:** To cancel a pending invitation before it is accepted, select the invitation and click **Revoke**. The invitation link becomes invalid immediately.

## Related wiki nodes
- [[features/incidents]]

## Source
- DevRev support article [User management](https://support.devrev.ai/en-US/devrev/article/uNlA_ZjU) (ART-21894)
