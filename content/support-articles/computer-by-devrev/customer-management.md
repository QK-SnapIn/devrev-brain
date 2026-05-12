---
title: Customer management
devrev_id: ART-21895
parent_directory: Access control
translation_group: Dsq2x-V4
modified_date: "2026-05-06T19:42:40.139Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/Dsq2x-V4"
tags: []
top_category: Computer by DevRev
wiki_match: features/incidents
match_score: 0.684
last_updated: 2026-05-11
summary: "Customer groups contain your external customers – contacts who interact with your product via the customer portal."
---

# Customer management

Customer [[entities/group|groups]] contain your external customers – contacts who interact with your product via the [[features/customer-portal|customer portal]]. They control what your customers can see and access on the customer portal, such as [[entities/article|article]] visibility, [[entities/ticket|ticket]] permissions, and portal features.

## Default customer groups

The following are the default customer groups in a workspace:

* **Customers:** All external members (customers) of the workspace. Any new customer is added to this [[entities/group|group]] by default. This group also governs public portal access when the public portal is enabled, allowing visitors to view [[entities/article|articles]] without signing in. See [[support-articles/computer-plus-support/customer-portal-setup-and-administration|Portal settings]] for details on how this group affects article visibility.
* **Customer Admins:** Users who can manage customer inquiries and view all [[features/tickets|tickets]] belonging to the [[features/accounts|accounts]] they are members of. Workspace admins and other customer admins can add customers to this group.
* **Verified Customers:** All verified external members (customers) of the workspace.

## Dynamic and static groups

Admins can add or remove members from any static group. A dynamic group determines membership automatically based on rules and expressions rather than manual assignment. Members are added or removed as they meet or stop [[entities/meeting|meeting]] the defined criteria. You cannot manually edit the member list of a dynamic group.

For a detailed explanation of how dynamic groups work, including expression syntax and use cases, see [[support-articles/computer-by-devrev/groups|Groups]].

## Customer group management

### Create a new customer group

You must be an admin to create a group.

1. In [**Settings > Customer management > Groups**](https://app.devrev.ai/?setting=customer-groups), click **+ Create new** and select the type of group you want to create (static or dynamic).
2. Fill in the group details such as name and description and select the method for adding customers.
3. For a static group, add customers by email or name.
4. For a dynamic group, define the filter rules or expressions that determine which users are automatically included (for example, filtering by email, association, or tags).

![group creation](don:core:dvrv-us-1:devo/0:artifact/4100374)

### Update a customer group

Default groups cannot be updated.

1. In [**Settings > Customer management > Groups**](https://app.devrev.ai/?setting=customer-groups), select the group you want to update and click **Edit**.
2. Make your changes — such as updating the group name, description, or membership rules (for dynamic groups) — and save.

![update group](don:core:dvrv-us-1:devo/0:artifact/4100380)

### Modify membership of a static customer group

1. In [**Settings > Customer management > Groups**](https://app.devrev.ai/?setting=customer-groups), select the static group.
2. To add a user, click **Add Customers** and enter the email addresses or names of the customers to add.
3. To remove a user, find the member you want to remove in the list view and click the cross button (⨯) next to the member's name.

## Source
- DevRev support article [Customer management](https://support.devrev.ai/en-US/devrev/article/Dsq2x-V4) (ART-21895)
