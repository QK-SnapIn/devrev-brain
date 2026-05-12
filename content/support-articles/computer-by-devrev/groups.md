---
title: Groups
devrev_id: ART-21893
parent_directory: Access control
translation_group: s1klL8Gq
modified_date: "2026-05-06T19:33:23.517Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/s1klL8Gq"
tags: []
top_category: Computer by DevRev
wiki_match: entities/group
match_score: 0.909
last_updated: 2026-05-11
related: ['entities/group']
summary: "A group is a collection of members used to organize access and permissions within a workspace."
---

# Groups

A [[entities/group|group]] is a collection of members used to organize access and permissions within a workspace. Only administrators can create and manage [[entities/group|groups]].

[[support-articles/computer-by-devrev/roles|Roles]] can be assigned to groups, granting the associated permissions to all members of that group.

## User groups and customer groups

**User groups** contain the workspace's internal users (team members, [[features/agents|agents]], platform users). Manage user groups at [Settings > Groups](https://app.devrev.ai/?setting=groups). Default user groups include **Admins**, **Platform Users**, and **All Users**.

For further details, refer to [[support-articles/computer-by-devrev/user-management|User groups]].

**Customer groups** contain external customers who interact with your product or support channels. Manage customer groups at [Settings > Customer groups](https://app.devrev.ai/?setting=customer-groups). Default customer groups include **Customer Admins** and **Verified Customers**.

For further details, refer to see [[support-articles/computer-by-devrev/customer-management|Customer groups]].

## Static groups and dynamic groups

**Static groups** are manually managed collections where administrators explicitly add and remove members. Static groups are ideal when you need precise control over group membership or when the criteria for membership cannot be automated.

**Dynamic groups** automatically manage membership based on predefined rules or expressions that evaluate member attributes such as email domain, role, or custom properties. Unlike static groups, dynamic groups are self-maintaining: members are automatically added when they meet the group's criteria and automatically removed when they no longer qualify. This automation eliminates the need for manual membership management and ensures groups stay current as attributes change over time.

## Related wiki nodes
- [[entities/group]]

## Source
- DevRev support [[entities/article|article]] [Groups](https://support.devrev.ai/en-US/devrev/article/s1klL8Gq) (ART-21893)
