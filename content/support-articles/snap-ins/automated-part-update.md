---
title: Automated part update
devrev_id: ART-21926
parent_directory: Automate
translation_group: CN6gjQj_
modified_date: "2026-01-15T19:36:35.673Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/CN6gjQj_"
tags: []
top_category: Snap-ins
wiki_match: entities/part
match_score: 0.85
last_updated: 2026-05-11
related: ['entities/part']
summary: "The Automated part update snap-in streamlines the updating of issue or ticket parts based on the initial part and target field defined in its configuration."
---

# Automated part update

The Automated [[entities/part|part]] update snap-in streamlines the updating of [[entities/issue|issue]] or [[entities/ticket|ticket]] [[features/parts|parts]] based on the initial part and target field defined in its configuration. It monitors the creation events of [[features/issues|issues]] and [[features/tickets|tickets]], ensuring that new entries match the part specified in the **Initial Part of Issue/Ticket** input field. Upon successful validation, the snap-in relocates the issue or ticket to the part specified in the **Issue/Ticket - Target Part Field**.

## Installation

1. Open the DevRev marketplace and install the **Automated Part Update** snap-in.
2. Select the workspace where you want to install the snap-in, confirm your
   selection, and click **Deploy snap-in**.
3. Set the following operating parameters.

* **For Initial Part of Issue**: Enter the part to be used as a condition for the issue.
* **For Initial Part of Ticket**: Enter the part to check as a condition for the ticket.
* **For Fallback Part**: Select the Part to move to if the target part field is empty.
* **For Tag**: Select the tag to identify the work is moved to part by this snap-in.
* **Issue - Target Part Field**: Specify the field name that determines the part to which the issue is moved.
* **Ticket - Target Part Field**: Specify the field name that determines the part to which the ticket is moved.

4. Click **Save** and **Install** to complete the setup.

## Related wiki nodes
- [[entities/part]]

## Source
- DevRev support [[entities/article|article]] [Automated part update](https://support.devrev.ai/en-US/devrev/article/CN6gjQj_) (ART-21926)
