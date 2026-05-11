---
title: StageFlow Automator
devrev_id: ART-21948
parent_directory: Automate
translation_group: dkZfjJqW
modified_date: "2025-12-10T06:57:21.425Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/dkZfjJqW"
tags: []
top_category: Snap-ins
wiki_match: glossary/shadow-user
match_score: 0.467
last_updated: 2026-05-11
summary: "The StageFlow Automator is a custom snap-in that allows you to configure custom stages between tickets and issues/enhancements."
---

# StageFlow Automator

The StageFlow Automator is a custom snap-in that allows you to configure custom stages between [[features/tickets|tickets]] and [[features/issues|issues]]/[[entities/enhancement|enhancements]]. You can also configure the stage transition whenever a message is given by a customer or a support team member.
It also sends notifications to the [[entities/ticket|ticket]] owner based on its stage changes.

For more information, refer to the
[StageFlow Automator snap-in](https://marketplace.devrev.ai/custom-covergence) on the DevRev marketplace.

## Installation

1. In DevRev, go to **Settings** > **Snap-ins** and click **Explore Marketplace** in the top-right corner.
2. In the DevRev marketplace, find **StageFlow Automator** and click **Install**.

## Configuration

You need to create a mapping between the tickets and issues/[[entities/enhancement|enhancement]] stages so that when the stage of an [[entities/issue|issue]] changes then the changes are also reflected accordingly in issues/enhancements.

1. Create the mapping in the CSV file in the format given below. The CSV file should contain the following columns:

   * `Ticket Subtype`
   * `Issue Stage` or `Enhancement Stage`
   * `Ticket Stage`

   Refer to the default stages documentation for each product feature:

   * [[support-articles/computer-plus-build/issues#stages|Issue stages]]
   * [[support-articles/computer-plus-support/tickets#stages|Ticket stages]]
   * [[support-articles/computer-plus-build/enhancements#stages|Enhancement stages]]

You can only create either ticket-issue mapping or ticket-enhancement mapping in a single CSV file.

Custom stages and subtypes are organization-specific.

1. In the snap-in **Discussions** tab, enter `/UploadCSV` and upload the CSV file you created for mapping before.
2. Go to the **Configuration** tab and view the mapping that was created using the CSV file.
3. Configure what stage the ticket must go to depending on the message given by a discussion participant.

   Enter `/StageConfig` in the snap-in **Discussions** tab and select the values from the dropdown for the stage transition whenever a message is given by a discussion participant.
4. Go to **Issues** or **Roadmap** and make updates. The tickets that were linked to the issue or enhancement reflect the changes you configured in the CSV file, notifying the ticket owner.

## Source
- DevRev support [[entities/article|article]] [StageFlow Automator](https://support.devrev.ai/en-US/devrev/article/dkZfjJqW) (ART-21948)
