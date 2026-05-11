---
title: Tasks
devrev_id: ART-21851
parent_directory: Computer by DevRev
translation_group: UR_DDUpg
modified_date: "2026-04-22T08:14:51.325Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/UR_DDUpg"
tags: []
top_category: Computer by DevRev
wiki_match: entities/task
match_score: 0.889
last_updated: 2026-05-11
related: ['entities/task']
summary: "Tasks are lightweight work items (like personal to-dos) that DevRev offers in addition to the more complex and richer work management records like issues, tickets, and opportunities."
---

# Tasks

[[entities/task|Tasks]] are lightweight work items (like personal to-dos) that DevRev offers in addition to the more complex and richer work management records like [[features/issues|issues]], [[features/tickets|tickets]], and [[entities/opportunity|opportunities]]. Unlike the mentioned work objects, tasks have been designed purposefully to be very simple.
You can break down any work item in DevRev into a bunch of tasks to track your daily progress on it.
Tasks may be owned by the owner of the work item or by someone else. They may be created automatically from GitHub or by a user.

You can also create personal tasks under **My Tasks** that are not linked to any work item and live outside independently like studying some topic, setting up a [[entities/meeting|meeting]], or following up with someone.

![Tasks](don:core:dvrv-us-1:devo/0:artifact/4099901)

You can use this to get your job done, organize your day, and ensure the highest priority work items are always front and center for you. The page has two tabs to show all your open tasks and completed/closed tasks.

Use tasks to:

* Set due dates for tasks if needed to denote deadlines by when they should be completed.
* Maintain a checklist of tasks inside a work record or outside and mark the checkbox next to them to denote that they are completed.

For example, if your [[entities/issue|issue]] is tracking the work of adding a new API in a service, your tasks linked to that issue can be:

* Read up on the code of the service
* Clarify doubts with the tech lead
* Write the core logic
* Write unit tests for it
* Raise a PR

You cannot assign personal tasks to others. Tasks associated with a work record can be assigned to others.

Use child issues and dependency issues for more heavy work assignments to others that are related to your work. Use tasks only for lightweight things like reviewing your work.

You cannot see the linked work item (issue, [[entities/ticket|ticket]], or [[glossary/opportunity|opportunity]]) for a [[entities/task|task]] and can navigate to it directly from there.

## Stages

This diagram represents the **Task Transitions** workflow in DevRev, organized into three main [[entities/group|groups]]:

* **📂 Open**: Initial stage for new tasks (Open)
* **⚡ In Progress**: Active development stage (In Development)
* **🔒 Closed**: Final state for completed tasks (Resolved)

Tasks can transition flexibly between all states, allowing for reopening and moving back to development as needed.

![Task Transitions Diagram](don:core:dvrv-us-1:devo/0:artifact/4099902)

## Related wiki nodes
- [[entities/task]]

## Source
- DevRev support [[entities/article|article]] [Tasks](https://support.devrev.ai/en-US/devrev/article/UR_DDUpg) (ART-21851)
