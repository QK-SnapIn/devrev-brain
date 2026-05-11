---
title: CSAT on conversation
devrev_id: ART-21933
parent_directory: Automate
translation_group: 8hsIAD6w
modified_date: "2026-02-23T18:38:49.831Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/8hsIAD6w"
tags: []
top_category: Snap-ins
wiki_match: entities/conversation
match_score: 0.85
last_updated: 2026-05-11
related: ['entities/conversation']
summary: "CSAT on conversation offers a simplified approach to measure customer satisfaction level for the conversation resolved with the help of surveys which can be utilized to enhance the overall customer experience."
---

# CSAT on conversation

[CSAT on conversation](https://marketplace.devrev.ai/csat_on_conversation_68rj7531) offers a simplified approach to measure customer satisfaction level for the [[entities/conversation|conversation]] resolved with the help of surveys which can be utilized to enhance the overall customer experience.

This snap-in displays a customer satisfaction survey to customers after their conversation gets resolved. The questions can be customized to align with their requirements.

To manually request [[glossary/csat|CSAT]] feedback without having to wait until the conversation is resolved, use the `/survey` command in **[[features/inbox|Inbox]]** > **Customer messages**.

## Installation

1. Install the [CSAT on conversation](https://marketplace.devrev.ai/csat_on_conversation_68rj7531) from the DevRev marketplace.
2. Select the workspace to install the snap-in, confirm installation, and click **Deploy snap-in**.

## Configuration

1. Go to **Snap-ins** > **CSAT on conversation** > **Configure**.
2. Select the channel you want to send the survey on in **Survey channel**.
3. Write introductory text for the survey in **Survey introductory text**.To include the customer's name in the CSAT survey emails, add a key `{{customer_name}}` to the introductory text configuration of the CSAT.
4. Customize your survey response scale which is shown to the customers to select from in **Survey response scale**.
5. To collect additional feedback from the customer along with the scale rating, ensure that the toggle for **Additional Feedback Request** configuration is enabled.
6. Write a query for the customers after the survey is populated in **Survey query**.
7. Write a message for the customers after the survey response is submitted in **Survey response message**.
8. Specify the time for the survey to expire (in minutes) in **Survey expires after**.![csat on conv](don:core:dvrv-us-1:devo/0:artifact/4100634)
9. Click **Save** > **Next** and deploy the snap-in.

## Related wiki nodes
- [[entities/conversation]]

## Source
- DevRev support [[entities/article|article]] [CSAT on conversation](https://support.devrev.ai/en-US/devrev/article/8hsIAD6w) (ART-21933)
