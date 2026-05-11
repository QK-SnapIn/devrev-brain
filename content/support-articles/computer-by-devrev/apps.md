---
title: Apps
devrev_id: ART-21848
parent_directory: Computer by DevRev
translation_group: EQXyoAPs
modified_date: "2026-05-08T17:57:49.154Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/EQXyoAPs"
tags: []
top_category: Computer by DevRev
wiki_match: entities/task
match_score: 0.5
last_updated: 2026-05-11
---

# Apps

Computer for Support Teams and Computer for Builders enable [[support-articles/computer-plus-support/contacts|customers]] to coordinate with the product or service builders (workspace) and with the different parts of the workspace to coordinate with each other. Between every integration hop and side conversation in traditional fragmented systems, important details that help define the *why* behind work is lost.

By linking work items—conversations and tickets for support, issues and enhancements for build—together, DevRev preserves context. That context defines the problem and requirements for anyone who works on this issue. Moreover, both tickets and issues are always associated with [[support-articles/computer-by-devrev/parts-trails|parts]], tying them to the overall product context.

The following figure shows a high-level view of the relationship between revenue-generating and product-delivery work.

![Apps Workflow Diagram](don:core:dvrv-us-1:devo/0:artifact/4099887)

## Conversations

*Conversations* refer to the communication chains you have with your external users. They begin in the DevRev [[support-articles/customer-support-agent/customer-support-agent-overview|Plug widget]], which enables live chat within customers' apps with just a few lines of code, or through a [[support-articles/snap-ins/snap-ins-overview|snap-in]] for email, WhatsApp, or Slack. Unlike most platforms, customer conversations are no longer siloed to just support, sales, and customer success staff. Instead, they are accessible to everyone in the workspace through the Plug inbox. The service-level metric for a conversation is time to response.

Example: "I have a problem with product X."

You can add a title to your conversations as well as members from your own workspace and other members from the user's workspace without starting a new thread or email chain. Because there can be many tickets attached to a single conversation, there is no need to start a new thread for new topics either.

We recommend closing the conversation whenever you feel the interaction has reached a natural end. Closing the conversation does not close the tickets and your external users are still able to see them in the widget.

## Tickets

A conversation is typically started by an external user. It may be a short interaction, such as a quick question about a sale, that does not require a ticket. If a conversation takes more than 5 mins to close, we recommend that you open one or more tickets. A conversation could also contain one or more items that you would want to capture in a ticket. A ticket is used to capture anything that you may need to follow up on from a conversation, which could be bugs, feature requests, or anything in between. A ticket is associated with a part of the product and can come from either an internal or an external user.

Example: "User reported a problem using product X. They need a workaround for this problem."

When a support ticket is filed, it's a commitment that the concern will be addressed or resolved. The service-level metric for tickets is time to resolution.

You might have seen systems (such as Intercom) that have just conversations or systems (such as Zendesk) that just have tickets. Although a lot of customer problems can just be solved with a conversation, some of them do require more work. Those workflows of solving a customer problem are much better represented in the ticket where customer-facing and product-delivery teams collaborate.

For example, if an external user wrote in and reported a crashing behavior, asked for an enhancement to an existing feature, and asked for entirely new functionality, you would likely create three tickets all linked to the same conversation. This means you do not need to ask your external users to write in separately about each topic they'd like to discuss, while the workspace can still track each item separately.

In the DevRev app, a support engineer can create a ticket based on a conversation they had with someone using the Plug widget. This ticket and conversation are linked.

A ticket should describe what the external user is experiencing in a language that's familiar to them. Developer-specific language is reflected in issues.

## Issues

Later on, a software engineer may start work on this ticket by creating an issue and breaking that issue into smaller pieces with tasks. An issue describes what the developer will work on and is created or accepted by someone who owns or works on the associated part of the product. This distinction allows developers to break up a ticket from an external user into issues as they see fit and delegate the work to other team members as necessary.

Example: "Feature A on product Y exhibited unexpected behavior. This is a defect and needs to be fixed."

Tickets and issues are linked in many-to-many relationships. It may require multiple issues to resolve a ticket, or one issue may resolve multiple tickets if different external users experience and describe the same behavior in different ways.

## Work/state relationships

The following figure shows how the various work object types relate.

![Apps Relationships Diagram](don:core:dvrv-us-1:devo/0:artifact/4099888)

## Work item linkage

Once your organization has implemented a mechanism for customers to start conversations, all customer conversations can be tracked within DevRev and any Conversations can be immediately linked to a ticket, a ticket to an issue and subsequently to a part (product capabilities and features).

| Link | Control |
| --- | --- |
| Conversation → Ticket | Open the conversation and click **Tickets > + Link tickets**. Either create a new ticket or select an existing ticket. |
| Ticket → Issue | Open the ticket and click **Issues > + Link issues**. Either create a new issue or select an existing issue. |
| Issue → Ticket | Open the issue and click **Tickets > + Link tickets**. Either create a new ticket or select an existing ticket. |
| Issue → Issue | Open the issue and click **Issues > + Link issues**. Either create a new issue or select an existing issue. |

| Conversation | Ticket | Issue |
| --- | --- | --- |
| Conversation item | Ticket item | Issue item> |

To delete a ticket or issue, select the work item in the list view and click the **Delete** icon in the taskbar that appears.

![delete ticket](don:core:dvrv-us-1:devo/0:artifact/4099889)

## Source
- DevRev support article [Apps](https://support.devrev.ai/en-US/devrev/article/EQXyoAPs) (ART-21848)
