---
title: Commands
devrev_id: ART-21866
parent_directory: Computer+ Support
translation_group: 8R9wzoqV
modified_date: "2026-04-10T08:25:45.457Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/8R9wzoqV"
tags: []
top_category: Computer+ Support
wiki_match: features/commands
match_score: 1.0
last_updated: 2026-05-11
related: ['features/commands']
summary: "If your teams repeatedly type the same replies and perform the same actions, commands (also called macros) can unlock significant productivity gains."
---

# Commands

If your teams repeatedly type the same replies and perform the same actions, [[features/commands|commands]] (also called macros) can unlock significant productivity gains. Commands help frontline teams such as support [[features/agents|agents]] manage high volumes of customer queries by providing standard responses and actions in a single click. This reduces response time, maintains consistent communication quality, and improves overall customer satisfaction.

A command is a single-click shortcut that sends a predefined response, executes one or more actions (such as updating a field), or both. Responses can be directed to customers or internal colleagues. They can be personalized with placeholder variables that are dynamically resolved based on the record to which the command is applied.

## Benefits of using commands

**Efficiency and consistency**

Apply commands to perform repetitive actions quickly, reducing clicks and keystrokes while maintaining uniform responses that reflect current policies and communication standards.

**Error reduction**

Minimize manual mistakes by standardizing responses and actions across the team.

**Automated actions**

Enhance saved responses with automated actions for owner or [[entities/group|group]] reassignment, stage updates, tag management, and other field updates, streamlining your workflow.

**Team-specific commands**

Use the **Available to** field to control whether a command is available to all users or only to specific [[entities/group|groups]], tailoring commands to different team needs.

**Flexible access control**

Control who can create and update commands. Admins have this ability by default, and you can assign custom roles to other groups for more flexible command management.

## Create commands

1. Go to [**Settings** > **Commands**](https://app.devrev.ai/?setting=commands) and click **+ Command**.
2. Enter a **Name** for the command and select a **Surface** to specify which object types the command is available on. Supported surfaces include:

   * [[features/tickets|Tickets]]
   * [[features/conversations-feature|Conversations]]
   * [[features/issues|Issues]]
   * [[entities/opportunity|Opportunities]]
   * [[features/accounts|Accounts]]
   * Customers
   > 💡 **Tip**: If you need commands on additional surfaces beyond the defaults, install the [Commands surface expander](https://support.devrev.ai/devrev/article/ART-20847) snap-in.
3. Set the **Status** of the command:

   * **Draft**: The command is saved but not yet available for use. Use this status while reviewing or refining a command before publishing.
   * **Active**: The command is published and available for use on the specified surfaces.
   * **Inactive**: The command is deactivated and cannot be used until changed back to Active.

   ![commands](don:core:dvrv-us-1:devo/0:artifact/4100090)
4. Define the formatted response to send when the command runs. You can insert placeholder variables that auto-fill from the record at execution time. After running the command, you can review and edit the response before sending.

   Common placeholder variables include:

   * `{{ticket.display_id}}`: The [[entities/ticket|ticket]]'s display ID.
   * `{{ticket.title}}`: The ticket's title.
   * `{{owner.display_name}}`: The display name of the current owner.
   * `{{creator.display_name}}`: The display name of the ticket creator.
   * `{{stage.name}}`: The current stage of the record.
   * `{{group.name}}`: The name of the assigned group.

   The available placeholder variables depend on the surface you selected. When you edit the response template, the editor displays the supported variables for that record type.

   ![placeholder](don:core:dvrv-us-1:devo/0:artifact/4100096)
5. Configure predefined **actions** that the command executes. For example, assign a different owner or group, move a ticket or [[entities/conversation|conversation]] to a different stage, or add or remove tags. For user-type fields, select *Current User* to assign the field to whoever runs the command. For example, a support agent can use a command that sets themselves as the ticket owner when the action specifies the owner field as *Current User*.
6. Optionally, set the **Available to** field to restrict the command to one or more specific groups. If you leave **Available to** blank, the command is available to all users in the workspace.
7. Click **Save** to create the command.

## Manage commands

* **View all commands**: Access a centralized list of draft, active, and inactive commands. Sort and filter commands based on their properties or attributes.
* **Edit or clone commands**: Modify existing commands or clone them to reuse a command with minimal changes.
* **Deactivate or delete commands**: Deactivate commands that are no longer needed. Inactive commands remain in the system and can be reactivated. Delete commands permanently only when you are certain they are no longer needed.
* **Share commands with relevant people**: Use the **Available to** field to specify whether a command is available to everyone in the workspace or restricted to one or more specific groups.

## Apply commands

On any supported record, type `/` in the rich-text editor in the internal or external discussion area to open the command selection menu. As you type after `/`, the menu filters to show matching commands. Use the keyboard arrow keys to navigate the list and preview what each command does, then select a command to run it.

After selecting a command, review the generated content before sending. Any placeholder variables that could not be auto-filled appear with distinct formatting so you can fill them in manually and send a correctly formatted response.

![slash command](don:core:dvrv-us-1:devo/0:artifact/4100100)

## Access control

By default, only admins can create, update, delete, and view all commands in the workspace. Grant other user groups access to create, update, read, or delete commands by assigning them custom roles through [[support-articles/computer-by-devrev/user-roles|user role management]].

> 📝 **Note**: Users who are members of groups specified in the **Available to** field for a command automatically have permission to view and use that command, even without a custom role.

## Best practices

Start by creating a few essential commands and gradually expand based on the most frequent query types and [[entities/task|tasks]] your team handles. The goal is to make the support process as streamlined as possible for both your team and your customers.

To help users discover commands quickly, choose names that are easy to remember and follow a consistent structure for categorization and [[features/search|search]]. If you have common themes or categories, standardize a naming convention for your teams.

One possible convention is `Category-Subcategory-Specific command subject`. For example:

* `Rerouting-Reroute to payments-Refund`
* `Rerouting-Reroute to payments-Payment failure`
* `Rerouting-Reroute to Sales`

## Related wiki nodes
- [[features/commands]]

## Source
- DevRev support [[entities/article|article]] [Commands](https://support.devrev.ai/en-US/devrev/article/8R9wzoqV) (ART-21866)
