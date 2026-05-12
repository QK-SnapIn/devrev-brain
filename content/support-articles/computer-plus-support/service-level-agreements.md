---
title: Service-level agreements
devrev_id: ART-21867
parent_directory: Computer+ Support
translation_group: gjimnW9H
modified_date: "2026-05-06T03:19:50.416Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/gjimnW9H"
tags: []
top_category: Computer+ Support
wiki_match: features/slas
match_score: 0.885
last_updated: 2026-05-11
related: ['features/slas']
summary: "A service-level agreement (SLA) is a contract between you and your customers that sets the expectations for your service level."
---

# Service-level agreements

A service-level agreement ([[features/slas|SLA]]) is a contract between you and your customers that sets the expectations for your service level. [[features/slas|SLAs]] help ensure that your customers receive timely responses and resolutions to inquiries. SLAs are configured in [Settings > SLA](https://app.devrev.ai/?setting=slas).

Admins and users with SLA policy permissions can set breach and warning targets for three time metrics: **First response**, **Next response**, and **Full resolution**. Each metric has its own breach and warning target. You can specify whether metrics are calculated using calendar hours or business hours while defining breach and warning targets.

> 📝 **Note**: SLA metrics respect the org schedule configured for your workspace. To configure business hours, go to [Settings > Org schedules](https://app.devrev.ai/?setting=org-schedule). For related operational-level agreements, see [[support-articles/computer-plus-support/operational-level-agreements|Operational-level agreements]].

## SLA metrics

### Conversation metrics

**First response time**

* **Default conditions**: A customer sends the first message in the [[entities/conversation|conversation]].
* **Start event**: Conversation created.
* **End event**: The agent replies to the conversation, the conversation moves to *Waiting on User* or *Resolved*, or the conversation is marked as spam.

**Next response time**

* **Default conditions**: A customer sends a new message after the support engineer replied.
* **Start event**: A new message on the conversation from the customer after the support engineer replied.
* **End event**: The agent replies to the conversation, the conversation moves to *Waiting on User* or *Resolved*, or the conversation is marked as spam.

**Full resolution time**

* **Default conditions**: Conversation created.
* **Start event**: Conversation created.
* **End event**: The conversation moves to *Resolved* or *Archived*, or the conversation is marked as spam.
* **Pause event**: The conversation moves to *Waiting on User*.
* **Resume event**: The conversation moves to any stage except *Waiting on User*.

### Ticket metrics

**First response time**

* **Default conditions**: [[entities/ticket|Ticket]] created by a customer, or by a support engineer on behalf of a customer.
* **Start event**: Ticket created.
* **End event**: The agent adds a comment to the customer chat, the ticket moves to *Awaiting Customer Response*, or the ticket is *Closed*.

**Next response time**

* **Default conditions**: Ticket created by a customer, or created by a support engineer but reported by a customer.
* **Start event**: A new comment on the ticket by the customer after the support engineer replied.
* **End event**: The agent adds a comment to the customer chat, the ticket moves to *Awaiting Customer Response*, or the ticket is *Closed*.

**Full resolution time**

* **Default conditions**: Ticket created by a customer, or created by a support engineer but reported by a customer.
* **Start event**: Ticket created.
* **End event**: The ticket moves to the *Closed* state.
* **Pause event**: The ticket moves to *Awaiting Customer Response*.
* **Resume event**: The ticket moves to any state except *Closed*.

### SLA metric calculation

SLA metrics are calculated based on the policy applied to the conversation or ticket. One or more SLA metrics can be active on a given conversation or ticket, with each tracked separately.

An SLA metric can be in one of the following stages:

* *Active*: The metric is being tracked on the conversation or ticket.
* *Close to breach*: The time spent by the SLA metric is greater than or equal to the close-to-breach target defined in the policy.
* *Breached*: The time spent by the SLA metric is greater than or equal to the breach target defined in the policy.
* *Paused*: The metric is paused based on certain conditions, for example when a ticket moves to *Awaiting Customer Response*.
* *Completed*: The conversation or ticket has reached the completion condition.

Based on business hours defined in your org schedule, *Active*, *Close to breach*, and *Breached* metrics can move out of schedule. Time spent out of schedule is not included in the calculation.

> ⚠️ **Warning**: If the customer [[entities/account|account]] is updated after the ticket is created, all SLA metrics are recalculated based on the updated customer account information. Any previous SLA breaches or achievements are discarded, and new calculations are applied according to the updated SLA.

> 📝 **Note**: The [Operational SLA Metrics snap-in](https://devrev.ai/marketplace/operational-sla-metrics) adds three additional metrics to ticket and conversation SLA policies.

## SLA notifications

SLA breach and close-to-breach events can trigger notifications to assignees and other stakeholders. Configure notification rules in your workspace settings to ensure the right team members are alerted when an SLA metric approaches or exceeds its target.

## View SLAs

The SLA targets applied to a particular conversation appear in the **[[features/inbox|Inbox]]** and the **Conversation Detailed** view. For [[features/tickets|tickets]], SLA targets appear in any ticket [[glossary/vista|vista]].

When two metrics are active, the vista displays the one closest to breach. For example, in a conversation where both the first response and full resolution metrics are active and the first response is due in five minutes while the full resolution is due in one day, the vista displays five minutes. If the first response is not provided within five minutes, the timer displays negative values (such as -10m), indicating that 10 minutes have passed since the first response was due. [[features/conversations-feature|Conversations]] or tickets can also be grouped by SLA stages.

In the **Detailed View**, all metrics applied to the ticket or conversation are visible along with their current stage.

To filter tickets based on SLA, use the **Next SLA Target** filter. The filter options work as follows:

* **All**: Returns all tickets that have an SLA applied. Tickets where the SLA has already completed are excluded.
* **Breached since**:

  + *Any*: Returns all tickets that have breached SLA, regardless of when the breach occurred.
  + *Over an hour*: Returns all tickets that have been in breach for more than one hour.
  + *Over a day*: Returns all tickets that have been in breach for more than one day.
  + *Custom*: Returns all tickets that have been in breach since a specified date.
* **Will breach in**:

  + *Any*: Returns all tickets that are not in breach.
  + *Over an hour*: Returns all tickets with less than one hour remaining before breach.
  + *Over a day*: Returns all tickets with less than one day remaining before breach.
  + *Custom*: Returns all tickets that will breach by the selected date.

## SLA management

### Create an SLA

1. Go to [Settings > SLA](https://app.devrev.ai/?setting=slas) and click **+ Create**.
2. In the **Create SLA** dialog, provide a name and description, then click **Create**. After creating the SLA, assign policies to it.

### Create policies within an SLA

Multiple policies can exist within an SLA. Each policy has a priority order, so if a ticket meets the conditions of two or more policies, the policy with the highest priority is applied. SLA metrics are only applied to tickets or conversations that meet the policy's conditions.

1. Click **+ Policy** and select either *Ticket Policy* or *Conversation Policy*.
2. In the policy pane, under **Conditions**, select the ticket or conversation attribute values for **Tag**, **[[entities/part|Part]]**, and **Severity**.
3. Under **Metrics**, enable or disable **First response**, **Next response**, and **Resolution time**, and set the breach and warning targets for each enabled metric.
4. Click **Save**.

### Publish an SLA

Publish an SLA after all policies are created. Published SLAs cannot be edited. You cannot change the policies or priority order of a published SLA. To modify a published SLA, clone it (see below), make changes to the clone, and publish the new version.

### Clone an SLA

Cloning allows you to create a copy of an existing SLA, including all its policies and priority order. This is useful when you need to modify a published SLA, since published SLAs cannot be edited directly.

1. Go to [Settings > SLA](https://app.devrev.ai/?setting=slas) and select the SLA you want to clone.
2. Click the **Clone** option. A new draft SLA is created with the same policies and settings.
3. Edit the cloned SLA as needed, then publish it.
4. Reassign customers from the original SLA to the cloned SLA if necessary.

### Assign customers

SLAs can only be assigned to customers after they are published. If no customers are added, the SLA is not applied to any tickets or conversations.

**Assignment rules**

Assignment rules define conditions that automatically assign a particular SLA to matching customer [[features/accounts|accounts]]. You can manage assignment rules from within an individual SLA or from the dedicated assignment rules view. Under [Settings > SLA](https://app.devrev.ai/?setting=slas), the **Assignment rules** top-level tab displays assignment rules across all published SLAs in one place. From this view you can create, edit, or delete assignment rules for any published SLA and review the priority order that determines which SLA applies when multiple rules match the same account.

1. Go to the **Assignment rules** tab of a published SLA and click **+ Create Rule**.
2. In the **New SLA assignment rule** pane, select the account attributes and their values to match against.
3. Click **Save and Apply**.

Once an assignment rule is created, you can edit or delete it. Changes to assignment rules only affect tickets where the SLA is applied after the change; there is no immediate impact on tickets where the SLA is already running.

**Exceptions**

Exceptions allow you to assign specific customer accounts to an SLA regardless of assignment rules.

1. Go to the **Exceptions** tab of a published SLA and click **+ Customer**.
2. Add all customer accounts you want to assign to the SLA.
3. Click **Assign**.

> 📝 **Note**: Setting an SLA as default automatically assigns it to all accounts that do not already have an SLA. When an SLA is set as default, its assignment rules and exceptions are bypassed — every unassigned account receives this SLA. Only one SLA can be the default at a time.

### View SLA policies

To see all active ticket and conversation SLA policies in a single view, go to [Settings > SLA](https://app.devrev.ai/?setting=slas). Each published SLA lists its policies, conditions, and assigned customers. You can filter by policy type (ticket or conversation) to quickly locate the relevant policy.

## Troubleshooting

* **[[entities/issue|Issue]]**: You have created and published an SLA, but no SLA is running on the ticket.

  **Solution**:

  1. Check the **SLA Name** attribute on the ticket. If it is empty, the customer account selected on the ticket is not assigned any SLA. Review your SLA assignment rules or add the customer as an exception to one of your SLAs.

     > 📝 **Note**: The **SLA Name** is never empty if your workspace has a default SLA.
  2. If the **SLA Name** is populated but no SLA metrics are running, the ticket does not satisfy the conditions of any policy within that SLA. Review the policies defined for the SLA listed under **SLA Name**. For example, if you have two policies — one with the condition Severity = Blocker and another with Severity = High — a ticket with medium severity still carries the SLA name but has no running metrics because it does not meet either severity condition.

  If the issue persists, review your SLA assignment rules and policies or contact support for further assistance. The ticket should have an SLA running when the **SLA Name** is populated and the ticket satisfies the conditions of at least one policy within that SLA.
* **Issue**: Your SLA timer runs continuously—including nights, weekends, or holidays—even though you expected it to pause outside working hours. SLA metrics use calendar hours by default; business-hours tracking only applies when a policy is explicitly linked to an Org Schedule.

  **Solution**:

  1. Go to [Settings > SLA](https://app.devrev.ai/?setting=slas) and open the relevant SLA.
  2. Select the policy and, under **Metrics**, check the schedule setting for each metric (First response, Next response, Resolution time).
  3. If the setting shows **Calendar hours**, change it to **Business hours** and select the correct Org Schedule.
  4. Click **Publish** to create a new version of the SLA.
  > 📝 **Note**: Publishing creates a new SLA version. The updated schedule applies to tickets created after publishing; existing open tickets continue under the previous version until their policy is next updated. For details on configuring business hours and holiday rules, refer to [[support-articles/computer-plus-support/org-schedules|Org schedules]].
* **Issue**: SLA breach history or progress on a ticket has been cleared, and the metrics appear to have restarted from zero. This is expected if the customer account on the ticket was updated after the ticket was created: all SLA metrics are recalculated based on the new account's SLA assignment, and any previous breach records or completed metrics are discarded.

  **Solution**:

  Verify whether the customer account field on the ticket was recently changed (check the ticket's activity timeline). If the reset was unintentional, reassign the correct customer account to restore the intended SLA.

  To prevent accidental resets, consider using **Assignment rules** under [Settings > SLA](https://app.devrev.ai/?setting=slas) so that the correct SLA is applied automatically at ticket creation, reducing the need for manual account updates later.
* **Issue:** An SLA metric not visible after completion.

  **Solution:** Go to [Settings > Support > Org Schedule](https://app.devrev.ai/?setting=org-schedule), find the expired schedule, and click **Edit**. Update the validity period (end date) to cover the current and future period, then save and publish.

  Publishing creates a new version of the schedule. Existing tickets will continue using the previous version; the new version applies to tickets created after publishing. For tickets where the SLA policy is updated, the latest schedule version will be applied.

## Related wiki nodes
- [[features/slas]]

## Source
- DevRev support [[entities/article|article]] [Service-level agreements](https://support.devrev.ai/en-US/devrev/article/gjimnW9H) (ART-21867)
