---
title: Routing
devrev_id: ART-21862
parent_directory: Computer+ Support
translation_group: wDr8m54F
modified_date: "2025-12-10T06:56:28.195Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/wDr8m54F"
tags: []
top_category: Computer+ Support
wiki_match: glossary/turing
match_score: 0.615
last_updated: 2026-05-11
---

# Routing

Routing refers to the process of identifying and assigning the appropriate team or individuals to manage a conversation or support ticket. This ensures that inquiries are directed to the most suitable group for prompt and effective resolution. Users can design workflows tailored to various scenarios; the example below illustrates a basic routing use case.

|  |  |
| --- | --- |
| NODE | ACTIVITY |
| Trigger | Ticket created |
| Action | Pick user by group |
| Action | Update ticket |
|  | ID: Ticket created > Output > ID |
|  | Group > Output > ID |
|  | Owned by > Set: Pick user > Output > User |

Orgs can set up pull-based routing by updating the group instead of the user ID in the workflow illustrated above and create a vista for the tickets using the selected group filter.
The following example illustrates spam ticket handling configuration:

|  |  |
| --- | --- |
| NODE | ACTIVITY |
| Trigger | Ticket created |
| Action | Spam checkerID: Ticket created > Output > ID |
| Control | If ElseWhen: Object Spam Checker > Output > Is Spam |
| If true: Action | Update ticketIs frozen: Object Spam Checker > Output > Is Spam |
| If false: Action | Pick user by group > Update ticketID: Ticket created > Output > IDOwned by > Set: Pick user > Output > User |

## Pick user node capabilities

* Object: Selection of ticket or conversation routing type.
* Group: Selection of routing destination group.
* Users: Selection of specific ticket assignment users.
* Strategy: Selection of assignment methodology (round-robin, load balancing, random).
* Agent availability: Assignment filters based on agent status (away or active).

## Additional routing scenarios

* Ticket routing based on customer inquiry keywords.
* Group-specific routing based on customer account assignments.
* Assignment routing based on severity and subtype.
* Custom field and tag-based routing.
* First responder ticket assignment.

## System requirements

* Administrator privileges are required for workflow deployment and execution.
* User status (active/away) is configurable through the profile section.

## Notification behavior

* Group-only routing triggers notifications for all group members.
* Direct user assignment triggers notifications only for the assigned user.
* Combined group and user routing triggers notifications only for the assigned user.
* If a user is assigned as the owner after notifications have been sent to the group members, those notifications are removed for all members and retained only for the assigned owner.
* When a new owner is assigned, the notification associated with the previous owner is deleted.
* Upon adding a new group, notifications are sent to the new group members, while notifications for the previous group members are deleted.
* All notification preferences are manageable through [**Settings** > **Notifications**](https://app.devrev.ai/?setting=user-preferences), including system, agent, and snap-in notifications.

## Source
- DevRev support article [Routing](https://support.devrev.ai/en-US/devrev/article/wDr8m54F) (ART-21862)
