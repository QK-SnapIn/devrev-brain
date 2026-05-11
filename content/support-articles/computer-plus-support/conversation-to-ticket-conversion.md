---
title: Conversation to ticket conversion
devrev_id: ART-21913
parent_directory: Conversations
translation_group: sYVCWaPV
modified_date: "2025-12-10T06:56:58.597Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/sYVCWaPV"
tags: []
top_category: Computer+ Support
wiki_match: entities/ticket
match_score: 0.85
last_updated: 2026-05-11
related: ['entities/ticket']
---

# Conversation to ticket conversion

You can convert conversations from Plug and Slack directly into tickets. Previously, conversations were only linked to tickets. This update streamlines workflows and enhances the customer experience.

For conversations originating from Plug or Slack, the **Link to Ticket** functionality is replaced with a new **Convert to Ticket** feature. Currently, the conversion feature is available only for Plug and Slack conversations. Other channels still use the traditional **Link Ticket** functionality.

Conversion cannot be undone. Once a conversation is converted to a ticket, this action is permanent and the conversation remains archived.

## Conversation conversion process

When you convert a conversation to a ticket, the following happens automatically:

* The original conversation moves to *Archived* stage and cannot be reopened.
* A new ticket is created with:

  + All internal discussions and customer messages copied from the conversation
  + Equivalent metadata as the conversation, including source channel, customer account information, and external members added as **reported by** on the ticket
  + An AI-generated ticket title and description based on customer messages

## Convert conversations to tickets

**Manual conversion**

Go to the conversation record pane and select **Convert to Ticket** to create a new ticket from the conversation.

![convert ticket](don:core:dvrv-us-1:devo/0:artifact/4100490)

**Automated conversion via workflows**

Set up automated [[support-articles/computer-by-devrev/workflows-overview|workflows]] to convert conversations to tickets based on specific triggers:

* When a conversation meets defined criteria
* When the AI agent identifies an issue requiring escalation
* According to custom business rules

Workflows enable seamless handovers from automated conversations to your support teams when necessary.

## Plug widget end-user experience

When a conversation is converted to a ticket in the Plug widget:

* The ticket number and basic details appear in the same conversation pane.
* Users can click **Details** to view complete ticket information.
* If the **Tickets** tab is enabled in Plug, users can track their ticket status there.

![create conversation](don:core:dvrv-us-1:devo/0:artifact/4100492)

## Slack end-user experience

When a conversation is converted to a ticket in Slack:

* Ticket information appears within the same thread.
* All subsequent messages sync with the newly created ticket.
* The transition is seamless for the end user.

## Conversation conversion scenarios

Consider converting a conversation to a ticket in these scenarios:

* Complex issues requiring in-depth investigation
* Cross-team collaboration needs
* Escalation requirements
* Feature requests
* Bug reports
* SLA tracking requirements
* Documentation needs
* Resource allocation requirements
* AI capability limitations
* Extended troubleshooting needs

## Support workflows

* **CSAT surveys**: CSAT surveys are not sent when a conversation is converted to a ticket. Surveys are only triggered when a conversation is resolved, not when it's archived through conversion.
* **SLA handling**: Conversation and ticket SLAs operate independently. When converting:

  + The new ticket starts with its own response and resolution SLA timers
  + All active SLA metrics on the original conversation are marked as completed

## Related wiki nodes
- [[entities/ticket]]

## Source
- DevRev support article [Conversation to ticket conversion](https://support.devrev.ai/en-US/devrev/article/sYVCWaPV) (ART-21913)
