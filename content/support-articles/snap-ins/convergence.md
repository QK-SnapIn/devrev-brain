---
title: Convergence
devrev_id: ART-21931
parent_directory: Automate
translation_group: qR1VuAs7
modified_date: "2025-12-10T06:57:10.054Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/qR1VuAs7"
tags: []
top_category: Snap-ins
wiki_match: features/commerce
match_score: 0.632
last_updated: 2026-05-11
summary: "Converge support and build by bringing together conversations, tickets, and issues."
---

# Convergence

Converge support and [[features/build|build]] by bringing together [[features/conversations-feature|conversations]], [[features/tickets|tickets]], and [[features/issues|issues]].

Once the convergence snap-in is installed, tickets and issues automatically change states when related tickets and issues do. These state changes are visible in the **Discussions** and **Events** tabs of tickets and issues.

![DevRev bot updates on a ticket](don:core:dvrv-us-1:devo/0:artifact/4100627)

## Workflows

The [[features/workflows|workflows]] present in the Convergence snap-in do the following [[entities/task|tasks]] for you automatically:

* [[entities/ticket|Ticket]] owners are added to the watchers list of the [[entities/enhancement|enhancement]] on which the ticket was created.
* If the enhancement is in-progress state and there are no issues linked to it, post a message in the enhancement timeline.
* Post message to enhancement timeline if not issues have been linked.
* Post message to enhancement timeline if issues are in *Triage* stage.
* Post in enhancement timeline if enhancement is *Prioritized* but no issues are linked.
* Post to ticket's timeline mentioning its owners when it is moved to *Product Assist* stage.
* Post to linked ticket's timelines when enhancement changes stage.
* Notify target close date to ticket, [[entities/issue|issue]], tasks, [[glossary/opportunity|opportunity]] and enhancement owners.
* Notify enhancement owners for linking PRD and design docs.
* Post a message on [[entities/part|part]] timeline tagging part owners when a new ticket is linked to that part.
* Post in the linked [[entities/conversation|conversation]] when a ticket is closed or reopened.
* Post in the linked conversation when a ticket is linked.
* Post in child issue timeline when parent issue is closed.
* Post in parent issue timeline when child issue is closed.
* Post to issue's timeline when linked ticket's severity is changed.
* Post in ticket's timeline when an issue linked to it is closed.
* Post in enhancement's timeline when any linked issue is *In Development*.
* Update ticket's stage when linked issue's state changes.
* Update ticket's stage when linked issue is linked or unlinked.
* Close pending tickets if they have remained in the *Awaiting customer response* stage for longer than x days.
* Update ticket's stage to waiting on user when user reverts on new conversation.
* Update ticket's stage to *Accepted* and notify owner and customers when an enhancement in ideation stage is linked.
* Update a spam conversation's stage to *Suspended*.
* Update a spam ticket's stage to *Canceled*.

## Installation

The Convergence snap-in is installed automatically in new workspaces.

## Configuration

While the defaults aim at balance, your environment may call for other settings. You can change the snap-in settings at any time under **Settings** > **Snap-ins**.

## Source
- DevRev support [[entities/article|article]] [Convergence](https://support.devrev.ai/en-US/devrev/article/qR1VuAs7) (ART-21931)
