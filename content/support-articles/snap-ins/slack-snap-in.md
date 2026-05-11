---
title: Slack snap-in
devrev_id: ART-21978
parent_directory: Integrate
translation_group: nDruC5fJ
modified_date: "2026-05-05T13:50:43.464Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/nDruC5fJ"
tags: []
top_category: Snap-ins
wiki_match: features/slack-integration
match_score: 0.552
last_updated: 2026-05-11
summary: "The Slack snap-in lets you scale your customer support in Slack by creating conversations, tickets, and issues, syncing messages bidirectionally and by routing notifications to the right channels."
---

# Slack snap-in

The [Slack snap-in](https://marketplace.devrev.ai/one-slack) lets you scale your customer support in Slack by creating [[features/conversations-feature|conversations]], [[features/tickets|tickets]], and [[features/issues|issues]], syncing messages bidirectionally and by routing notifications to the right channels.

For historical import of Slack data into DevRev, see the [Slack AirSync](https://marketplace.devrev.ai/slack-airdrop) connector, which performs bulk imports rather than real-time sync.

## Slack channel types

The Slack snap-in behaves differently depending on the type of Slack channel. DevRev recognizes three channel types:

* **Connect channels**: Slack Connect channels shared with external organizations. Messages sync to the **Customer Messages** panel in DevRev.
* **External channels**: Channels where external customers or contacts post messages directly. Messages sync to the **Customer Messages** panel in DevRev.
* **Internal channels**: Channels containing only members of your own organization. Messages sync to the **Internal Discussions** panel in DevRev.

## Installation

Before installing the Slack snap-in, verify the following prerequisites:

* You have Slack workspace admin rights, or a Slack workspace admin is available to approve the OAuth connection.
* If you have a Slack Enterprise [[entities/account|account]], contact DevRev Support to be allowlisted before attempting setup. Enterprise workspace support is in limited availability.
* Maintain one public Slack connection per DevRev workspace. Within a workspace, one Slack connection can be used across multiple snap-ins and [[features/workflows|workflows]]. Creating multiple connections may disrupt existing integrations due to Slack's OAuth limitations.
* After installation, invite the DevRev bot to every channel where you want conversations or sync to operate by running `/invite @DevRev` in each channel.

1. [[features/search|Search]] for and open [Slack](https://marketplace.devrev.ai/one-slack) in the DevRev Marketplace, then click **Add** in the top-right corner.
2. In the [snap-in settings](https://app.devrev.ai/?setting=snap-ins), connect your Slack workspace to DevRev by clicking **Sign in with Slack**, which redirects you to Slack's OAuth page.
3. Select the appropriate Slack workspace from the top-right corner of the OAuth page and click **Allow** to complete the connection.
4. Add configurations in the snap-in, click **Save** at the bottom of the configuration page, then click **Install** to activate the snap-in.

> 💡 **Tip**: To see which channels the DevRev app has been added to, open the DevRev app's profile in Slack and view its info panel. Slack lists all channels the app is a member of.

## Available commands

After installation, run `/devrev help` in any Slack channel to display all available [[features/commands|commands]] in a pop-up modal. The key commands include:

* `/devrev create-ticket` — Open a new [[entities/ticket|ticket]] creation form.
* `/devrev create-issue` — Open a new [[entities/issue|issue]] creation form.
* `/devrev link` — Link a Slack channel to a DevRev customer workspace.
* `/devrev view <identifier>` — View a DevRev object by its display ID (for example, `TKT-123` or `ISS-456`), full object ID, or full DevRev URL. Running `/devrev view` without an identifier opens a search modal.
* `/devrev ticket-digest` — Display a paginated list of all open and in-progress tickets.

> ⚠️ **Warning**: Slack does not support slash commands in threads. All `/devrev` commands must be run in a channel, not in a thread reply.

## Message actions vs. commands

When creating work items from Slack, choose between message actions and slash commands based on context:

* **Message actions** are best when creating a ticket or issue from an ongoing thread. Select the message, then choose **Create a new ticket** or **Create a new issue** from the message actions menu. The snap-in uses AI to summarize the thread and pre-populate the title and description fields.
* **Slash commands** are best when starting a new work item that is not tied to an existing thread. Run `/devrev create-ticket` or `/devrev create-issue` in the channel.

## Create DevRev conversations from Slack

The snap-in enables support teams to manage customer interactions directly from DevRev. Enable this feature by toggling the **Sync conversations from Slack to DevRev** setting in the snap-in configuration.

To start creating conversations from a Slack channel:

1. Run `/devrev link` in the channel, search for the DevRev customer workspace in the pop-up modal, select the preferred workspace, and click **Link**. If the channel is already linked, the modal shows the linked workspace details and an option to unlink.
2. Run `/invite @DevRev` in the channel to invite the DevRev app.

Once linking and invitation are complete:

* Messages sent by customers directly to the channel create new conversations.
* Messages in threads or channel messages from members of your own team do not create new conversations.
* Created conversations appear in the **[[features/inbox|Inbox]] [[glossary/vista|vista]]** in your DevRev app.
* If a message is sent to a Slack thread belonging to an archived [[entities/conversation|conversation]], the snap-in creates a new follow-up conversation and syncs all subsequent messages to it.

> 📝 **Note**: A Slack channel can be linked to only one DevRev customer workspace, and vice versa.

### Conversation roll window

To avoid multiple conversations for related customer messages, a **conversation roll window** [[entities/group|groups]] messages together.

* The roll window remains active for five minutes after a conversation is created.
* Any new message sent directly in the channel within this window is appended to the existing conversation, and each new direct customer message resets the timer.
* Messages sent from DevRev sync to the thread of the first message that initiated the conversation.
* Only messages within the thread of the originating message are synced. Messages within Slack threads of follow-up messages sent directly to the channel do not sync to DevRev.

### Conversation notifications

Any new message added to a conversation in your DevRev workspace, regardless of its originating channel or platform, can trigger a notification in a designated Slack channel. This helps your team stay updated on customer interactions. Unicode emoji characters can be included directly in Slack messages to personalize these notifications.

To enable conversation notifications:

1. Turn on **Enable the conversation notification feature** in the [snap-in configuration](https://app.devrev.ai/?setting=snap-ins).
2. Enter a Slack channel ID in the **Channel ID to send conversation notifications** field.

New messages within tickets in the customer messages panel also trigger this automation. Each conversation or ticket is subject to a five-minute cooldown period between notifications to prevent overload. Multiple consecutive messages within this window do not trigger additional notifications.

> 📝 **Note**: Notification threads are not synchronized between DevRev and Slack. Other notification types (such as customer reply notifications) may use different cooldown periods.

### Conversation creation troubleshooting

If conversations are not being created from Slack messages, verify each of the following:

1. Confirm that **Sync conversations from Slack to DevRev** is toggled on in the snap-in configuration.
2. Confirm that the Slack channel is linked to a DevRev customer workspace by running `/devrev link` and checking the modal.
3. Confirm that the DevRev bot has been invited to the channel by running `/invite @DevRev`.
4. Confirm that the Slack snap-in is installed and active in [Settings > Snap-ins](https://app.devrev.ai/?setting=snap-ins).

## Work management using Slack

### Prefill title and description

The snap-in configuration includes a **Prefill title and description for new work item** option. When enabled, using a message action to create a ticket or issue from a Slack thread causes the snap-in to use AI to summarize the thread and pre-populate the title and description fields in the creation form.

### DevRev tickets and Slack

The Slack snap-in allows you to create tickets directly from Slack. There are multiple ways to initiate ticket creation from any channel:

* **Command**: Run `/devrev create-ticket` in the channel.
* **Message action**: Select a message, then choose **Create a new ticket** from the message actions menu. This is recommended when working from an existing thread because the snap-in can pre-populate fields from the thread content.
* **Convert a conversation**: Transform an ongoing conversation into a ticket. This is recommended if you already have a conversation in progress. Configure the snap-in to send or suppress a ticket summary card to the Slack thread using the **Notify on conversation to ticket conversion** setting. The Slack thread syncs with the new ticket instead of the ongoing conversation regardless of this setting.

Choosing either the command or message action option opens a pop-up modal with the new ticket form. Complete the required fields; some fields auto-fill based on the messages.

> 📝 **Note**: Ticket creation dropdowns for [[features/parts|parts]] and customer workspaces display up to 100 items (most recently created). If the item you need does not appear, search by name in the dropdown.

### Ticket sharing options

The new ticket modal in Slack includes a **Share with everyone** checkbox at the bottom:

* **Enabled**: Shares the ticket details with the Slack channel via a summary card.
* **Disabled**: Keeps the ticket internal with no updates to the Slack channel.

Regardless of sharing, the ticket details are visible to the creator in the submission modal.

You can configure the default state of the **Share with everyone** checkbox at the user level through the **Share ticket acknowledgement by default** setting. When enabled, the checkbox is pre-selected each time you create a ticket.

### Syncing details

If sharing is enabled, the type of Slack channel determines the sync location in DevRev:

* **External or Connect channels**: Messages sync with the **Customer Messages** panel.
* **Internal channels**: Messages sync with the **Internal Discussions** panel.

Syncing different panels to separate Slack threads is not supported.

> 📝 **Note**: Only shared tickets are synchronized between DevRev and Slack.

### Follow-up and merged tickets

The Slack snap-in supports follow-up and merged tickets. When two tickets merge and both have syncing Slack threads, all messages from both Slack threads reach only the primary ticket in DevRev, while messages from DevRev sync only to the primary ticket's Slack thread. If only one ticket has a syncing Slack thread, that thread syncs with the primary ticket. No messages from the duplicate ticket sync to Slack.

If a ticket is archived but receives a new customer message in its Slack thread, a follow-up ticket is automatically created for future discussions.

### New ticket notifications

To receive notifications whenever a new ticket is created, regardless of source channel or platform:

1. Enable **Notify on new ticket creation** in the [snap-in configuration](https://app.devrev.ai/?setting=snap-ins).
2. Enter a Slack channel ID in the **Channel ID to send ticket notifications** field.

Notification message threads are not synced between platforms.

### Notifications for ticket state update

Enable **Notify on ticket state update** in the snap-in configuration to send notifications to syncing Slack threads whenever the ticket state changes. This applies only to tickets that are actively syncing with a Slack thread.

> 📝 **Note**: State refers to the ticket's lifecycle status (for example, open, in progress, or closed). Stage changes, which are used for internal workflow purposes, do not trigger these notifications.

### Ticket digest

Run `/devrev ticket-digest` in any Slack channel to open a modal with a paginated list of all open and in-progress tickets.

## DevRev issues and Slack

The Slack snap-in allows issues to be created directly from Slack using the following methods:

* Run `/devrev create-issue` in the channel.
* Select a message, then choose **Create a new issue** from the message actions menu.

Both options open a pop-up modal with a new issue form. Some fields are pre-populated based on the messages in the thread.

The **Share with everyone** functionality operates identically to ticket creation. Only shared issues are synchronized between the platforms. Messages are always synced in the **Internal Discussions** panel with the Slack thread. Creating issues with sync enabled from external channels is not supported.

## Known limitations

* **Slash commands do not work in threads.** Slack does not support slash commands in thread replies. Run all `/devrev` commands in a channel.
* **Dropdown cap of 100 items.** Ticket creation dropdowns for parts and customer workspaces display up to 100 items (most recently created). Search by name if the desired item does not appear.
* **One Slack connection per workspace.** Maintaining more than one public Slack connection per DevRev workspace may disrupt existing integrations.
* **Enterprise workspace support.** Connecting a Slack Enterprise workspace requires allowlisting by DevRev Support.

## Capabilities and limitations

### Channel types

The Slack snap-in distinguishes three channel types:

* **Connect channels**: Slack Connect channels shared with external organizations.
* **Internal channels**: Standard workspace channels used by internal teams.
* **External channels**: Channels designated for customer-facing communication.

Understanding these types is important because sync behavior, summary card visibility, and certain features vary by channel type.

### Custom objects not supported

The Slack snap-in does not support custom objects or related automations. Only stock DevRev objects (tickets, issues, [[features/incidents|incidents]], [[entities/opportunity|opportunities]], and parts) are supported.

### Two-way sync between DevRev and Slack

If two-way sync is enabled on an object, new messages received from non-Slack source channels appear in DevRev but do not sync to the Slack thread.

By default, messages from bots, service [[features/accounts|accounts]], or [[features/agents|AI agents]] in DevRev are not synced to Slack. To change this, enable the **Sync bot messages from DevRev to Slack** option in snap-in configurations.

The snap-in supports syncing of message edits and deletions between platforms. Message attachment sync is supported both ways, with a file size limit of 250 MB.

### Invite the DevRev app to channels

Adding the DevRev app to many Slack channels can be challenging at scale. Use the `/SlackInviteBot` command from the **Slack snap-in event discussions panel** to automatically invite the DevRev app to all public channels. Private channels still require manual addition.

### When sync is not possible

If sync is not possible, the form displays a clear warning. Possible reasons include:

* The thread is already in sync with another DevRev object.
* Sync is not supported for the object in the given Slack channel.
* The DevRev app is not a member of the channel.
* The channel is private or a DM.

> 📝 **Note**: In such cases, the object can still be created, but without two-way sync.

## DevRev incidents and Slack

The Slack snap-in allows [[glossary/incident|incident]] creation directly from Slack using the following methods:

* Use the `/devrev create-incident` command.
* Select **Create a new incident** from the message actions.
* Enable **Auto-create incidents from Slack channels**, which automatically creates an incident for every direct message posted in specified Slack channels.

The first two options open a pop-up modal with a new incident form, with some fields pre-populated based on the context.

### Incident AI agent

The incident AI agent can be invoked directly from Slack by mentioning `@DevRev` in a message. When mentioned, the agent analyzes the conversation context and can assist with incident triage, summarization, and recommended actions. Configure this capability through the **Incident AI agent** snap-in setting.

### Sync options

Incidents support syncing messages both within a dedicated Slack thread and across an entire Slack channel, including all associated threads. The sync target is determined by the **Sync for new incident** snap-in configuration, which offers the following options:

1. **Create a new channel**: Automatically creates a new Slack channel for each new incident, regardless of its source channel or platform. Channel names are prefixed according to the **Prefix for new incident channel** snap-in configuration, with the incident display ID appended to ensure uniqueness. Whenever someone is mentioned or assigned as the owner of the incident, they are auto-invited to the incident channel.
2. **Sync messages with the thread (for incidents created from Slack)**: Works only for incidents created from Slack. Syncs messages with the originating thread, similar to ticket and issue work items.
3. **Sync messages with the notification thread**: Syncs with the thread of the incident notification sent on the channel specified in the **Channel ID to send incident notifications** configuration. Works for all incidents regardless of source channel or platform.
4. **Ask while creating incident**: Only applicable for incidents created from Slack. Adds a dropdown at the end of the incident form, letting the user choose the sync target for each incident individually.
5. **Do not sync**: Incidents remain internal to DevRev without syncing to a new Slack channel or thread.

For incidents that sync with dedicated Slack channels, configure automatic channel archiving when an incident moves to a closed state through the **Incident channel auto-archive interval** snap-in configuration.

If the `/devrev view` command is used in a dedicated incident channel, a pop-up modal opens with a pre-populated incident summary.

## Notify for DevRev object mentions

When a DevRev object link is mentioned in a public Slack channel, the snap-in can post a notification to that object's discussion panel in DevRev. This keeps the DevRev conversation thread informed about relevant Slack discussions. Enable this behavior through the **Notify for DevRev object mentions** snap-in configuration. This feature works only in public channels where the DevRev app is a member.

## Share and view record details

Share or view DevRev record details in Slack using the `/devrev view` command. This lets you search for tickets, issues, incidents, opportunities, and parts directly within Slack.

For example:

* `/devrev view TKT-#`
* `/devrev view ISS-#`

These commands open the specific object mentioned in the command.

## Create custom workflows

Users can configure their own workflows around Slack using DevRev's workflow engine.

| Workflow action | Description | Inputs | Outputs |
| --- | --- | --- | --- |
| Send message on Slack | Sends a message to any Slack channel the DevRev app can access. Private channels are supported only if the DevRev app is a member of the channel. | Slack connection, Slack channel ID, text message to send, objects to mention with message. If any object is added, a summary card of that object is sent with the message. | Slack message ID |
| Create new Slack channel | Creates a new Slack channel. | Slack connection, channel name (must be unique; insert a variable such as object display ID to guarantee uniqueness), toggle for private or public channel, users to invite (list of DevRev users; users are invited only if the Slack snap-in resolves a Slack user for the given DevRev user), groups to invite (list of DevRev groups; all users within the groups are invited after creation). | Channel ID, channel name |
| Get Slack user ID | Gets the Slack user ID for a given DevRev user. Can be used to later send direct messages to the user on Slack using the Send message on Slack node. | Slack connection, DevRev user ID | Slack user ID |
| Start Thread Sync | Sets up two-way message synchronization between a Slack thread and a DevRev object discussion. This node initiates a background sync process and produces no return value. | Slack connection, DevRev object ID, Slack channel ID, Slack thread ID (message ID of parent message, returned by the Send message on Slack node) | None |
| Start Channel Sync | Sets up two-way message synchronization between a complete Slack channel and a DevRev object discussion. This node initiates a background sync process and produces no return value. | Slack connection, DevRev object ID, Slack channel ID | None |

## DevRev object customization support

The Slack snap-in honors DevRev's object customizations, including:

* Custom fields and subtypes
* Stock field overrides
* Slack-specific client overrides
* Summary view card

> ⚠️ **Warning**: Custom objects are not supported by the Slack snap-in. Only stock DevRev objects (tickets, issues, incidents, opportunities, and parts) work with Slack customizations and automations.

The summary view card of all objects can be customized. Only fields marked with **Show in Summary = true** in object [[features/customization|customization]] are shown. Summary cards are static Slack messages and may not reflect real-time data. Use the **Refresh** button at the bottom of the card to update; a timestamp indicates the last update time. To view all fields or update the object, click the **View/Update** button.

The information shown in the summary card differs by channel type:

* In **Internal channels**, all summary fields are shown.
* In **External channels**, summary fields are hidden.

## Slack snap-in user resolution

The Slack snap-in uses email for user resolution between platforms. If a user or organization hides their emails, the integration cannot resolve the user to a DevRev contact and acts on behalf of itself instead. Ask customers to share their emails with your organization so apps, including DevRev, can access them.

If email is unavailable, the snap-in creates a new DevRev contact and attaches the Slack user ID for future reference. For legacy users, run the `/AddSlackUserId` command in DevRev on the contacts to manually add their Slack user ID.

## Deactivate or uninstall the Slack snap-in

To temporarily disable the [[features/slack-integration|Slack integration]] without removing its configuration, deactivate the snap-in:

1. Go to **Settings > Snap-ins** and locate the Slack snap-in.
2. Click the snap-in, then select **Deactivate**. The snap-in stops processing events but retains all configuration and sync history.

To reactivate, return to the same page and select **Activate**.

To permanently remove the Slack snap-in and all its configuration:

1. Go to **Settings > Snap-ins** and locate the Slack snap-in.
2. Click the snap-in, then select **Uninstall**. This removes the snap-in, its configuration, and stops all sync activity. Existing DevRev objects created through the integration are not deleted.

## Troubleshooting

* **Issue**: The DevRev bot does not respond in a Slack channel.

  **Solution**: Verify that the DevRev app has been added to the channel. In Slack, open the channel details and check the **Integrations** section for the DevRev app. For private channels, manually invite the app by typing `/invite @DevRev`. For bulk invitation to public channels, use the `/SlackInviteBot` command from the Slack snap-in event discussions panel.
* **Issue**: Slack connection error during snap-in setup.

  **Solution**: Re-authenticate the Slack connection. Go to the snap-in configuration, remove the existing Slack connection, and add a new one. Ensure the Slack workspace admin has approved the DevRev app and that the required OAuth scopes have not been revoked.
* **Issue**: Messages are not syncing between Slack and DevRev.

  **Solution**: Confirm that two-way sync is enabled for the relevant object type in the snap-in configuration. Check that the DevRev app is a member of the channel where sync is expected. If the channel is private or a DM, sync is not supported. Also verify that the thread or channel is not already in sync with a different DevRev object.
* **Issue**: User resolution fails and messages appear as sent by the DevRev bot instead of the actual user.

  **Solution**: The snap-in resolves users by email. If a Slack user's email is hidden or does not match any DevRev contact, the snap-in cannot map them. Ask the user to make their email visible to your Slack workspace, or manually run the `/AddSlackUserId` command in DevRev to associate the Slack user ID with the correct contact.
* **Issue**: Incident auto-creation does not trigger in a designated Slack channel.

  **Solution**: Verify that the channel is listed in the **Auto-create incidents from Slack channels** snap-in configuration. Ensure the DevRev app is a member of the channel and that the message is a direct post (not a thread reply) if the configuration expects top-level messages.

## Source
- DevRev support [[entities/article|article]] [Slack snap-in](https://support.devrev.ai/en-US/devrev/article/nDruC5fJ) (ART-21978)
