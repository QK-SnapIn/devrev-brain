---
title: Slash commands
devrev_id: ART-21952
parent_directory: Automate
translation_group: JhW1DLGe
modified_date: "2025-12-10T06:57:23.74Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/JhW1DLGe"
tags: []
top_category: Snap-ins
wiki_match: features/commands
match_score: 0.85
last_updated: 2026-05-11
related: ['features/commands']
---

# Slash commands

The [Slash commands snap-in](https://marketplace.devrev.ai/marketplace/slash-commands) helps you with tasks that are taking up your time and increasing your workload.
By using the Slash commands snap-in, you gain direct access to the capabilities of Computer within any text field. This integrates into your workflow, regardless of whether you're engaged in customer support interactions or immersed in building projects.

## Commands

Slash commands are available through text fields such as:

* **Inbox** > **Conversation** > **Customer chat/Discussions**
* **Tickets** > **Customer chat/Discussions**
* **Issues** > **Discussions**

![slash commands](don:core:dvrv-us-1:devo/0:artifact/4100739)

Entering `/` in a text field allows you to execute commands, revealing a comprehensive list of available options. Respond to customers or participate in discussions, all without the need to exit your ongoing conversations.

### Remind

Using the remind command, you can set a reminder for yourself or another user in the context of the source. You must specify a time and add messages to set the reminder.

For example:`/remind @user Please follow up on this. 1d`

### Rephrase

The rephrase command helps you reply professionally when communicating with clients or colleagues.

For example:`/rephrase can't help now... ask again in 5d`

Sample response:

I am unable to assist you at the moment, however please reach out to me again in five days and I will be happy to help you.

### Summarize

Using the summarize command, you can sum up the entire conversation. It applies to the following:

* Conversation
* Tickets
* Issues
* Part
* Workspace
* Customer
* Account

Sample response:

**Summary:**

* Rahul from DummyOrg is having difficulty installing the Plug Widget.
* Rohan suggests checking the setup instructions.
* When this doesn't work, Rohan asks for more information on the error.
* Rahul shares a recording of the error.
* Rohan thanks the user, and they get on call to fix it.

### Clone

Using the clone command, a copy of the selected issue or ticket is created. All attributes of the issue/ticket are copied, along with [CLONE] prefixed to the title. It also comments on:

* Source issue/ticket. For example, "ISS-0123 was cloned and ISS-0123 was created."
* Cloned issue/ticket. For example, "TKT was cloned from TKT-0123."

## Installation

The Slash commands snap-in is installed automatically in new workspaces.

## Related wiki nodes
- [[features/commands]]

## Source
- DevRev support article [Slash commands](https://support.devrev.ai/en-US/devrev/article/JhW1DLGe) (ART-21952)
