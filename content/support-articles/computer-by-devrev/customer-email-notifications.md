---
title: Customer email notifications
devrev_id: ART-21853
parent_directory: Computer by DevRev
translation_group: bdTvezeR
modified_date: "2025-12-10T06:56:22.762Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/bdTvezeR"
tags: []
top_category: Computer by DevRev
wiki_match: features/csat
match_score: 0.667
last_updated: 2026-05-11
summary: "At DevRev, our commitment is to streamline collaboration and ensure that the teams and their customers are always in the loop."
---

# Customer email notifications

At DevRev, our commitment is to streamline collaboration and ensure that the teams and their customers are always in the loop. To help achieve this, we've established specific email notification rules. This section describes when and how email notifications are triggered within the DevRev platform.

The email senders and subject lines are subject to change based on organizational settings and preferences.

## White-label customer email notifications

Organizations can personalize their email notifications by choosing a customized sender address and by incorporating their own logo, creating a more branded and professional appearance. Moreover, if customers reply to these notification emails, their responses will automatically be added to the relevant [[entities/ticket|ticket]] or [[entities/conversation|conversation]], ensuring seamless and continuous communication.

By default, notifications are sent from [notifications@devrev.ai](mailto:notifications@devrev.ai). However, this setting can be overridden to use the organization’s primary email address as the sender, or notifications can be turned off entirely.

To configure the notifications setting, under [**Settings** > **Snap-ins** > **Email Integration**](https://app.devrev.ai/?setting=snap-ins%2Femail-with-tickets), go to **Configure** > **Notification Sender Email Address** and select the required option.

## Reply to the customer on a conversation

* **Trigger**: When a reply is made to a customer on a conversation and they are not online anymore.
* **Action**: The system sends out a notification to the customer with the recent messages while highlighting the latest message that triggered the email.
* **Sender**: `{Sender_Name}` [support@yourdomain.com](mailto:support@yourdomain.com)
* **Subject**: "You are missing messages from `<Org Name>`"

## Reply to the customer on a ticket

* **Trigger**: When a reply is made to a customer on a ticket.
* **Action**: The system sends out a notification to the customer with the reply message.
* **Sender**: `{Company_Name}` [support@yourdomain.com](mailto:support@yourdomain.com)
* **Subject**: "[`{Company_Name}`] Update on TKT-XXX"

## Ticket linked to a conversation

* **Trigger**: A ticket is linked to an existing conversation.
* **Action**: The system sends out a notification with the linked ticket number.
* **Sender**: `{Company_Name}` [support@yourdomain.com](mailto:support@yourdomain.com)
* **Subject**: "`<customer email subject from Conversation>`"

This email is only sent to the organizations with [Convergence snap-in](https://docs.devrev.ai/automations/converge)

## Change of stage of a ticket/conversation

* **Trigger**: When there's a change of stage in a ticket or conversation.
* **Action**: The system sends out a notification detailing the Ticket/Conversation number and stage change.
* **Sender**: `{Company_Name}` [support@yourdomain.com](mailto:support@yourdomain.com)
* **Subject**:
  - For ticket: "[`{Company_Name}`] Update on TKT-XXX - Ticket Title""`<customer email subject>`"
  - For [[features/conversations-feature|conversations]]: “Update on your Conversation with `{Company_Name}`"

This email is only sent to organizations that have installed [Convergence snap-in](https://docs.devrev.ai/automations/converge).

## CSAT survey for conversation/ticket

* **Trigger**: A [[glossary/csat|CSAT]] survey is sent for a conversation or ticket.
* **Action**: The system sends out a notification with the ticket/conversation number and CSAT form.
* **Sender**: DevRev [no-reply@devrev.ai](mailto:no-reply@devrev.ai)
* **Subject**: "CSAT for TKT-XXX"

This email is only sent to organizations that have installed [CSAT snap-in](https://docs.devrev.ai/automations/csat-conv).

## Auto customer reply

* **Trigger**: A new conversation is initiated from a customer.
* **Action**: An automated reply is sent.
* **Sender**: `{Company_Name}` [support@yourdomain.com](mailto:support@yourdomain.com)
* **Subject**: "`<customer email subject>`"

This email is only sent to organizations that have installed [Auto-reply snap-in](https://docs.devrev.ai/automations/auto-reply).

## Auto reply on email

* **Trigger**: A new email is received from a customer.
* **Action**: An automated reply is sent.
* **Sender**: `{Company_Name}` [support@yourdomain.com](mailto:support@yourdomain.com)
* **Subject**: "`<customer email subject>`"

This email is only sent to organizations that have installed [Auto-reply snap-in](https://docs.devrev.ai/automations/auto-reply).

## Source
- DevRev support [[entities/article|article]] [Customer email notifications](https://support.devrev.ai/en-US/devrev/article/bdTvezeR) (ART-21853)
