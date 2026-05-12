---
title: Task tracker
devrev_id: ART-21959
parent_directory: Automate
translation_group: wKEL5T9d
modified_date: "2025-12-10T06:57:27.971Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/wKEL5T9d"
tags: []
top_category: Snap-ins
wiki_match: entities/task
match_score: 0.85
last_updated: 2026-05-11
related: ['entities/task']
summary: "The Task tracker snap-in helps streamline task management by tagging users with open tasks every Monday through Friday allowing them to keep track of pending tasks."
---

# Task tracker

The **[[entities/task|Task]] tracker** snap-in helps streamline task management by tagging users with open [[entities/task|tasks]] every Monday through Friday allowing them to keep track of pending tasks. These messages are logged every day at 9 AM IST within the work item.

For more information, refer to the [Task tracker snap-in](https://marketplace.devrev.ai/...) on the DevRev marketplace.

## Installation

1. In DevRev, go to **Settings** > **Snap-ins** and click **Explore Marketplace** in the top-right corner.
2. In the DevRev marketplace, find **`Task Tracker`** and click **Install**.

## Configuration

In **Settings** > **...**, the following configuration options are available:

* **[[entities/part|Part]] to Render:**Select the part where messages should be logged. For example, if you wish to log messages within a Capability and its associated [[features/parts|parts]], choose "Capability" from the dropdown menu.
* **Number of Levels Deep Within the Parent:**Define how many levels under the selected part should include logged messages. Setting this to "0" restricts logging to the selected part only. Increase the value to include additional sub-levels.
* **Custom Message:**Create a personalized message and include placeholders to tag users and tasks. Use the following keywords within square brackets `[ ]`:

  1. `[owner]` - Tags the owners of the tasks within the work item.
  2. `[task_list]` - Lists all open tasks in the work item, grouped by each owner.
     If you prefer, you can leave this field as is to use the default message template.

## Related wiki nodes
- [[entities/task]]

## Source
- DevRev support [[entities/article|article]] [Task tracker](https://support.devrev.ai/en-US/devrev/article/wKEL5T9d) (ART-21959)
