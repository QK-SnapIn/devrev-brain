---
title: CSAT on ticket
devrev_id: ART-21934
parent_directory: Automate
translation_group: iaG7eVAQ
modified_date: "2025-12-10T06:57:12.115Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/iaG7eVAQ"
tags: []
top_category: Snap-ins
wiki_match: entities/ticket
match_score: 0.85
last_updated: 2026-05-11
related: ['entities/ticket']
---

# CSAT on ticket

[CSAT on ticket](https://devrev.ai/marketplace/csat_on_ticket_dwx7b2bp) offers a simplified approach to measure customer satisfaction level for the ticket resolved with the help of surveys which can be utilized to enhance the overall customer experience.

This snap-in displays a customer satisfaction survey to customers after their ticket gets resolved. The questions can be customized to align with their requirements.

To manually request CSAT feedback without having to wait until the ticket is resolved, use the `/survey` command in **Tickets** > **Customer messages**.

## Installation

1. Install the [CSAT on ticket](https://devrev.ai/marketplace/csat_on_ticket_dwx7b2bp) from the DevRev marketplace.
2. Select the workspace to install the snap-in, confirm installation, and click **Deploy snap-in**.

## Configuration

1. Go to **Snap-ins** > **CSAT on ticket** > **Configure**.
2. Select the channel you want to send the survey on in **Survey channel**.
3. Write introductory text for the survey in **Survey introductory text**.

   To include the customer's name in the CSAT survey emails, add a key `{{customer_name}}` to the introductory text configuration of the CSAT.
4. Customize your survey response scale which is shown to the customers to select from in **Survey response scale**.
5. To collect additional feedback from the customer along with the scale rating, ensure that the toggle for **Additional Feedback Request** configuration is enabled.
6. Write a query for the customers after the survey is populated in **Survey query**.
7. Write a message for the customers after the survey response is submitted in **Survey response message**.
8. Specify the time for the survey to expire (in minutes) in **Survey expires after**.

   ![csat on ticket](don:core:dvrv-us-1:devo/0:artifact/4100640)
9. If you want to send the survey only once, enable the **Send survey only once per ticket** toggle.
10. If you want to automatically send CSAT surveys when tickets reach the *Resolved* stage, keep the **Trigger the CSAT survey based on configured rules** toggle turned off.
11. If you want to send CSAT at a specific ticket stage, turn the **Trigger the CSAT survey based on configured rules** toggle on and set up a custom workflow with the following configuration:

|  |  |
| --- | --- |
| **Component** | **Details** |
| Trigger | Update Ticket |
| Stage Control | If Else |
| Condition | When: Ticket Updated / Output > Stage > Name (Make sure that the stage name is in snake case.) |
| Action | Update Ticket |
| ID | Ticket Updated > Output > Id |
| List of Integrations | CSAT |
| Integrations | App CSAT Send Survey > Yes |

12. Click **Save** > **Next** and deploy the snap-in.

## Related wiki nodes
- [[entities/ticket]]

## Source
- DevRev support article [CSAT on ticket](https://support.devrev.ai/en-US/devrev/article/iaG7eVAQ) (ART-21934)
