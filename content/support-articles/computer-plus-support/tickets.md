---
title: Tickets
devrev_id: ART-21861
parent_directory: Computer+ Support
translation_group: WX96DY0b
modified_date: "2026-04-09T09:59:10.988Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/WX96DY0b"
tags: []
top_category: Computer+ Support
wiki_match: features/tickets
match_score: 1.0
last_updated: 2026-05-11
related: ['features/tickets']
summary: "A ticket is a record of a customer\"s request for assistance or support."
---

# Tickets

A *[[entities/ticket|ticket]]* is a record of a customer's request for assistance or support. When a customer contacts a company with a problem or [[entities/issue|issue]], the company creates a ticket to track the request and ensure that it's addressed in a timely and satisfactory manner. For example, if a user calls in and files a ticket for a problem they're facing any progress would be communicated to them through the ticket.

[[features/tickets|Tickets]] are associated with a [[entities/part|part]] (product or service) and can come from both internal and external users. Tickets are also used to communicate progress to the user or other impacted party.

There may be cases where mass communications (broadcast) are necessary in the event of lots of impacted or related parties (such as service status updates). In this scenario, the ticket would be used to broadcast and handle communications among multiple parties, including across multiple workspaces. Broadcast can also be used to engage customers for feedback/ideas (such as new feature ideas). Scoping is important for broadcast tickets as there needs to be a differentiation between broadcast (all revs) vs. multicast (particular revs).

Views of tickets can be found under **Support** in the DevRev app.

![Support tickets](don:core:dvrv-us-1:devo/0:artifact/4099979)

You can export views to CSV or JSON by selecting **Actions** in the upper-right corner and choosing the format.

## Attributes

Tickets have attributes that can be used to filter and [[entities/group|group]] tickets in various views.
You can find all the stock attributes listed under [**Settings** > **Object customization** > **Ticket**](https://app.devrev.ai/?setting=object-customization?type=ticket), go to **Stock fields**.
These are the stock attributes that come with DevRev:

* **Owner**: The person responsible for the ticket. Tickets are assigned to an engineer, PM, designer, or any other team member through the **Owner** attribute.
* **Group**: The group to which the ticket belongs. For more information on [[entities/group|groups]], see [[support-articles/computer-by-devrev/groups|groups]].
* **Severity**: The importance of the ticket. Severity can be set to low, medium, blocker, or high.
* **Stage**: The current state of the issue. The stage attribute is used to track the progress of the issue through its lifecycle. For more information on stages, see stages.
* **Part**: The part of the company or product that the issue is related to. For more information on [[features/parts|parts]], see [[support-articles/computer-by-devrev/parts-trails|parts]].
* **Created by**: The user who created the ticket.
* **Created date**: The date the ticket was created.
* **Modified date**: The date the ticket was last modified.
* **Tags**: Tags are used to categorize tickets.
* **Customer workspace**: The workspace that the ticket pertains to. You can create a new [[entities/account|account]] or workspace if it doesn't exist.
* **Target close date**: The date by which the issue is expected to be resolved.
* **Modified by**: The user who last modified the ticket.
* **Reported by**: Which customer is experiencing the issue. When a ticket is created from an email thread containing multiple customer email IDs, multiple reporters may be added. If a DevRev user adds a new customer while responding from DevRev, or if a new customer responds to the email thread, these new customers are added to the **Reported by** field. In the case of the Portal, there is only one **Reported by**, representing the person who has logged in to the portal to report the issue. Additional reporters can be added from the DevRev app. To select a contact in the **Reported by** field, first choose the corresponding account and workspace in the **Customer** attribute. After this selection, the contact's name will appear in the **Reported by** list.
* **Email members**: Participants in the ongoing email thread, dependent on the last email. This attribute automatically updates based on the last email sent from or received on DevRev.

Adding members to **Email members** also adds them to the **Reported by** field. Removing members from **Email members** does not remove them from the **Reported by** field.

Shadow users can also be subscribers and email members.

* **CCed members in email**: The CCed members in emails will be added to reporters if they are contacts in the workspace to which the ticket belongs. They will be added to email members if they are part of the ongoing email thread, without any workspace restriction.
* **Shadow users**: Users created for tracking and record-keeping purposes that do not have access to the DevRev app. Shadow users are typically created when [[glossary/airsync|AirSync]] imports data from external sources and identifies users without an email address. Tools like AirSync can assign work and attribute comments and actions to them. AirSync can also create **Unassigned** users that serve the same purpose but do have emails.
  Shadow users are considered users (members of the DevRev organization) rather than contacts, although they have no access to the platform. For more information, refer to the [[support-articles/computer-by-devrev/airsync-overview#dev-user-deduplication|import docs]].
* **Close date**: The date the ticket was closed.
* **Source channel**: The channel through which the ticket was created. Customers can create tickets via email, the portal, and various other channels.
* **Channel**: Indicates the medium used for customer communication.
* **Subscribers**: Indicates the group of users who will receive updates about the tickets.External contacts cannot be added as subscribers, so a [[support-articles/customer-support-agent/customer-support-agent-overview|DevRev contact]] must be created first for any emails to be added as subscribers.
* **Needs response**: Set to true whenever a new customer message is received on the ticket to ensure that no customer messages are missed. If a particular customer message does not need a response, the **Needs response** toggle can be turned off by the user. Turning off the **Needs response** toggle does not affect the [[features/slas|SLA]] metrics.

These attributes can be effectively used in filters and **Group** conditions across various [[features/vistas|vistas]] in DevRev to track specific work, capacity, and more.

You can add custom attributes to tickets to track additional information. For more information on custom attributes, see [[support-articles/computer-by-devrev/object-customization|object customization]].

[[features/issues|Issues]] are attached to tickets in order to track efforts with product priorities.

## Create a ticket

1. Go to **Support** > **Tickets** from the sidebar on the left.
2. Click **New Ticket** on the top-right corner of your screen.
3. Add a title and description for your new ticket. You can also attach files related to the ticket in the description.
4. Select which part of the company/product this ticket is related to.

   ![New ticket panel](don:core:dvrv-us-1:devo/0:artifact/4099983)
5. Enter other attributes for the ticket: change the assignee or accept the default; enter the severity; add any relevant tags to help employees identify any relevant traits of the ticket; select the workspace that the ticket pertains to.
6. If there are other tickets or issues that relate to this ticket, click **Link Records** and select the relevant items.
7. If you would like to immediately create another ticket, select **Create multiple**.
8. Click **Create**.

If a ticket is created from an existing [[entities/conversation|conversation]], then the ticket's title and description are populated automatically from the conversation.

![ticket fields](don:core:dvrv-us-1:devo/0:artifact/4099987)

You can create a child issue by clicking **+ Link issue** > **Add a child issue**. You can link the other existing issue as a child issue or create a new one by clicking on **+ New issue**.
Just update the title of the child issue and click enter. All other fields will be populated automatically by DevRev. You can edit them later.

## Stages

This diagram represents the **Ticket Transitions** workflow in DevRev, organized into three main groups:

* **📂 Open**: Initial stage for ticket management (Queued)
* **⚡ In Progress**: Active support stages with various assistance types (Work In Progress, Awaiting Product/Development assistance, In Development, Awaiting Customer Response)
* **🔒 Closed**: Final states for tickets (Resolved, Canceled, Accepted, Archived)

The workflow supports complex support scenarios with multiple assistance types and allows reopening closed tickets through the queue. Tickets can be archived for long-term storage.

![Ticket Transitions Diagram](don:core:dvrv-us-1:devo/0:artifact/4099996)

**Open**

* *Queued* (Q)
  The initial stage for all tickets. When a new ticket is created, it's automatically put into the *queued* stage, which indicates that it needs to be picked up by a customer experience engineer.

**In-progress**

* *Work In Progress* (WIP)

  Work on the concern reported by the user has begun. When a customer experience engineer starts work on a ticket, the ticket's stage changes to *Work In Progress*. When they require more information, they may ask the customer for additional detail (such as logs or context), in which case the stage would change to *Awaiting Customer Response* until the customer responds.

  In certain scenarios, the customer experience engineer may be able to resolve the customer's concern. If that's the case, they would ask the customer if their resolution has resolved their concern and the stage would move to the *Awaiting Customer Response*. Once the concern is resolved and the customer acknowledges the resolution, the stage may move to *Resolved*. If the concern isn't resolved, the stage may change back to *Work In Progress* as the customer experience engineer continues to work on it.
* *Awaiting Product Assist* (APA)

  The customer experience engineer is waiting for a response or feedback from someone internally. They may need to escalate the ticket. There may be a corresponding [[support-articles/computer-plus-build/issues|issue]] created to fix the defect, which would transition the stage to *Awaiting Development*.
* *Awaiting Customer Response* (ACR)

  The customer experience engineer requires more detail or another response from a user. In certain cases where the ticket depends on some fix (issues) the stage may go from *In Development* to *Awaiting Customer Response* when the corresponding issues have been resolved and the fix needs to be validated with the user.

  In certain cases, the customer experience engineer may be able to solve directly (without any required issues) which may change the stage from *Work In Progress* to *Awaiting Customer Response* to validate they have solved the problem. If either has resolved the customer's concern the stage can move to *Resolved*.
* *Awaiting Development* (AD)

  The issues on which the user's concern relies for resolution are planned but not active, when development on the issue begins the stage transitions to *In Development*.
* *In Development* (ID)

  The issues on which the user's concern relies for resolution are actively being worked on. Once the development process begins, the stage may go from *In Development* to *Awaiting Customer Response* to validate the fix with the user and then to *Resolved*. If the user wants to cancel the ticket then the stage moves to *Canceled*.

**Closed**

* *Canceled* (C)

  The ticket is determined to be invalid either by the user or the customer experience engineer. In certain scenarios, a ticket may have been created by accident and may be canceled by the creator. In other scenarios, garbage tickets may be created through automation or because of spam. Automation or the customer experience engineer can directly close and cancel such tickets.
* *Accepted* (A)

  The ticket requires a new feature development on the platform for resolution. However, there is no active work on the ticket but the feature addition required to meet the ticket will be done in the future. This stage is added to ensure that feature requests do not linger in the APA queue and to ensure that the right features are prioritized during roadmap planning.
* *Resolved* (R)

  The goal target stage for tickets. Resolved means that the customer's concerns which led to the ticket have been addressed.
* *Archived*

  The ticket has been archived for long-term storage and historical reference. Archived tickets are no longer active but can be referenced for future work or analysis.

## Subtypes

You can create subtypes for tickets to categorize them based on the type of issue. For example, you can create subtypes for bugs, feature requests, or questions.
A subtype inherits all the attributes of its parent ticket type. You can add custom attributes to a subtype.
To know how to create subtypes and add custom attributes to them, see [[support-articles/computer-by-devrev/object-customization|object customization]].

## Viewing attachments on tickets

You can view all attachments sent via the ticket's description, internal discussion, or a customer message by going to the **Attachments** section on the ticket for easy access.

![ticket attachments](don:core:dvrv-us-1:devo/0:artifact/4100000)

## Turing suggests

[[glossary/turing|Turing]] suggests enables Computer to aid customer experience engineers in resolving current tickets more efficiently. Each time a ticket is viewed, Computer proactively presents a curated selection of similar tickets and related knowledge [[entities/article|articles]].
Additionally, this system includes a feedback mechanism. This allows users to contribute to the continual learning and [[entities/enhancement|enhancement]] of the AI, ensuring an increasingly effective and refined support experience over time.
This advancement is a valuable tool in streamlining your support workflow and enhancing overall service quality.

In case you want it to learn and help you better in the future, [[glossary/don|don]]’t forget to give 👍 on the suggestion if you like it or 👎 to dislike it.

![turing-suggests](don:core:dvrv-us-1:devo/0:artifact/4100003)

## Duplicate ticket merging

Duplicate tickets in a support system pose a significant challenge by creating inefficiencies, increasing the workload for support [[features/agents|agents]], and negatively impacting user experience. These tickets often result from user frustration or misunderstandings of the resolution process, leading to confusion and disrupting the support workflow. This not only wastes time on redundant issues but also slows response times and skews data analysis.

Merging duplicate tickets establishes uniform communication between customers and agents, providing an effective solution to this problem.

**Duplicate ticket**

A duplicate ticket is any ticket identified as a repetition of another existing ticket. These tickets are considered unnecessary for further communication or action, as they pertain to the same problem already raised in the primary ticket. Duplicate tickets often arise from customers submitting multiple requests through different channels (email, portal, Slack). All duplicate tickets become *immutable* after merging.

**Primary ticket**

A primary ticket is the main record that consolidates all relevant information from duplicate tickets. It serves as the primary source of communication for all merged duplicate tickets, ensuring that all customer interactions, updates, and resolutions are centralized in one location. This ticket not only retains the most comprehensive data but also acts as the focal point for tracking the progress of the customer's issue.

### Merging guidelines

To ensure consistency and accuracy in the merging process, apply these guidelines when determining eligible tickets for merging:

* Same workspace: All selected tickets must belong to the same customer workspace or have no workspace.
* Matching reporters: All selected tickets must have the same reporters or no reporters.
* Active status: Only unclosed tickets can be selected as primary or duplicate tickets.
* Channel flexibility: Tickets from any channel can be merged if they share the same reporters.

### Merge settings

You can configure the following options in the ticket preferences page:

* Communication messages for duplicate and primary ticket owners
* Stage of duplicate tickets after merge
* [[features/accounts|Accounts]] to exclude from automated messages

Merge can be enabled only when users configure the post merge stage in the ticket preference settings page.

### Merge tickets

1. Open the primary ticket and select the merge option from the side panel.

   The ticket from which you initiate the merge becomes the primary ticket.
2. In the modal window that appears, review the suggested duplicate tickets based on the pre-filled primary ticket title.
3. Select the appropriate duplicate tickets and confirm the merge action.

   There is no limit on the number of tickets that can be merged.
4. Review the automatic communication sent to primary and duplicate ticket owners (configurable in ticket preferences).

### Post-merge conditions

* The primary ticket retains all key fields (description, part, group, owner, creator, priority, stage), and the SLA remains unchanged.
* Events are updated to reflect all merge actions.
* Subscribers and reporters from duplicate tickets are added to the primary ticket.
* Linked objects from duplicate tickets transfer to the primary ticket.
* The older messages and attachments on the duplicate ticket remains within the duplicate ticket post merge.
* Any new customer message on duplicate tickets post merge sync to the primary ticket.
* Duplicate tickets remain accessible through the **Linked Objects** section of the primary ticket.
* [[glossary/csat|CSAT]] triggers only for the primary ticket resolution.
* Merge actions cannot be reversed, and merged tickets cannot be merged again.

## Follow up tickets

Follow up tickets allow support teams to seamlessly address unresolved issues, recurring problems, or additional concerns without losing context. By linking follow-up tickets to the original ticket(archived/immutable), teams can track ongoing issues more effectively, minimize duplicate work and enhance customer experience. A follow-up ticket is a new ticket that is created and linked when a customer responds in reference to an archived/immutable ticket. The following scenarios can lead to the creation of follow up ticket:

* Customers communicated on an archived/immutable ticket from any channel such as email.
* Customer communicated on a merged ticket and the primary ticket is also archived.

After creation of a follow up ticket the customer messages will reflect only on the new followup ticket and the customer will continue to see response on the same thread in channels like email & slack. The user can continue responding on the new follow up ticket.

The below fields would be copied on the new follow up ticket from the archived/immutable ticket:

* Part
* Channel
* Account
* Workspace
* Reported by
* Description
* Title
* Channel specific custom fields
* Subtype

The follow up trigger is added in the [[features/workflows|workflows]] and admins configure the changes required on new follow up ticket, for example, copying of any other fields.

## Internal Tickets

Internal tickets allow your team to create and manage support tickets on behalf of customers—without granting customers access to these tickets. This feature enables internal collaboration while keeping the ticket invisible to the customer until explicitly made external.

Even if a ticket contains customer-related information (such as the customer workspace or the **Reported by** field), it remains inaccessible to the customer unless it is explicitly converted into an external ticket. The **Customer Messages** tab is unavailable for internal tickets.

To create an internal ticket, click the **Create Ticket** button. At the bottom of the ticket creation panel, click the dropdown menu on **Create external ticket** and select **Create internal ticket**.

You can convert an internal ticket to an external ticket by clicking **Convert to External** within the **Customer Messages** tab. Once a ticket is converted to external, it cannot be reverted back to internal.

## Related wiki nodes
- [[features/tickets]]

## Source
- DevRev support [[entities/article|article]] [Tickets](https://support.devrev.ai/en-US/devrev/article/WX96DY0b) (ART-21861)
