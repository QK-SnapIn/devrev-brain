---
title: Conversations Overview
devrev_id: ART-21838
parent_directory: Conversations
translation_group: C48RPDJK
modified_date: "2025-12-10T06:56:14.228Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/C48RPDJK"
tags: []
top_category: Computer+ Support
wiki_match: entities/conversation
match_score: 0.85
last_updated: 2026-05-11
related: ['entities/conversation']
---

# Conversations Overview

A conversation is an object type that's used to track any synchronous or near-synchronous discussions. A conversation maybe started by a customer, a builder, or a system (auto-created).

A new conversation is routed to the customer org's default owner unless it matches keywords in the support routing snap-in configuration.

Conversations from new or unidentified customer orgs have lower priority than existing customer orgs.

**Tags** [*values*]

* Stalled
* Priority/Escalated
* Fast/Slow Moving
* Blocked
* Resolution: [*value*]

## Stages

The following figure shows the state machine for conversations.

![Conversation State Machine Diagram](don:core:dvrv-us-1:devo/0:artifact/4099843)

**Open**

* *New*

  The initial stage for all valid conversations. In certain cases, spam may get past the filter and end up in *new* which would be moved to *suspended*. When someone from the support team responds, the status changes to *waiting on user* as they need a response from the user to take the next step towards addressing the user's concern.
* *Suspended*

  The initial stage for all invalid conversations, which may include spam or otherwise suspicious inquiries. This stage is used to minimize noise in the support inbox. If, upon review, the *suspended* item is deemed valid, it's transitioned to the *new* stage.

**In-progress**

* *Waiting on user* (WOU)

  Someone from the support team has responded and is waiting on a response from the user. For the initial response, the stage transitions from *new* to *waiting on user*. When a customer responds back to support, the stage transitions to *needs response*.

  Towards the end of the conversation when the resolution is expected to be valid, the customer experience engineer asks the customer to acknowledge their concerns have been resolved. When the customer experience engineer asks this question the stage transitions to *waiting on user*, and if they validate it moves to *needs response* for the customer experience engineer to verify resolution. Once verified the customer experience engineer moves the stage to *resolved*. If the user does not validate the resolution, the customer experience engineer responds back to the user and the process continues.

  To calculate the time to initial response you can look at the duration between the conversation created timestamp and the time the stage transitions from *new* to *waiting on user*. Another method is to see how long the conversation was in the *new* stage.
* *Needs response* (NR)

  The customer has responded; the customer experience engineer needs to review the item and respond or resolve the issue if the user requests or validates the fix. When a customer experience engineer responds the stage transitions to *waiting on user*.

  In certain cases it may be necessary to escalate the item internally where the conversation may depend on tickets, issues, or a response from someone other than themselves. In this case the stage transitions to *hold* since the customer experience engineer is blocked by a dependent item.

  Conversations which need a response from the customer experience engineer shows a **Reply** button in the inbox.
* *Hold* (H)

  The resolution is waiting on some dependent item. Dependencies may include review from someone other than the customer experience engineer (for example, SME, manager, PM, developer) or the completion of other work items (tickets or issues).

  When the dependencies have been completed the stage transitions to *needs response* to bring to the customer experience engineer's attention. Upon review they may put the conversation back on *hold* to re-escalate the item. If the dependencies seem to be resolved the customer experience engineer responds to the customer and the stage transitions to *waiting on user*.

**Closed**

* *Resolved* (R)

  The final target stage for conversations. It means that the customer's concerns which led to the conversation have been addressed.

  A conversation set to *resolved* still shows in the end-user's widget. If they respond again, it reopens the conversation and set the status to *needs response*.
* *Archived*

  The final stage for conversation.

## Related wiki nodes
- [[entities/conversation]]

## Source
- DevRev support article [Conversations Overview](https://support.devrev.ai/en-US/devrev/article/C48RPDJK) (ART-21838)
