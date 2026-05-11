---
title: Updates
devrev_id: ART-21852
parent_directory: Computer by DevRev
translation_group: knFZaYQO
modified_date: "2026-05-08T18:08:39.165Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/knFZaYQO"
tags: []
top_category: Computer by DevRev
wiki_match: features/updates-feed
match_score: 0.85
last_updated: 2026-05-11
related: ['features/updates-feed']
---

# Updates

Updates help you stay on top of all your activity on DevRev.

Conversations, tickets, and issues where you are an owner, member, or creator, or where comments are made or you are @mentioned, are automatically shown in your updates. A group can also be mentioned here which will send a notification to all the members of the group. For other tickets and issues, you can follow them to receive some or all updates through the bell icon 🔔 on the work item. You can unfollow work items to stop updates by unchecking all or some update types.

Both discussions and field updates show up as participation updates. Participation updates are the most frequent. You can unfollow them to reduce noise in your updates.

The **Updates** page features two main tabs:

* **Important**: Displays critical updates requiring immediate attention.
* **Others**: Shows less critical updates for informational purposes.

By default, all Important notifications are delivered via email and mobile push notifications.

## Triage of updates

### Notification handling

DevRev helps you efficiently manage and triage updates with the following features:

* Auto-mark as read: Notifications are marked as read when clicked, and the record opens in the right pane.
* Automatic archiving: Notifications are archived after 30 days; only the last 30 days are viewable.
* Deduplication: Except for mentions, notifications are reduced to the latest comment and field update.
* Clustering: Notifications are clustered by record, appearing in a single row. Records can appear in both the **Important** and **Others** tabs if they have updates of both types.
* Notification count: The badge reflects the total number of **Important** notification records, not individual updates.

### Filters and tools for triaging

DevRev provides several tools to help you manage your notifications.

* Unread vs All: Toggle between **Unread** and **All** updates, with **Unread** as the default to achieve inbox zero.
* Subscription management: Unsubscribe using the bell icon on hover if a specific record is no longer relevant.
* Mark as read: Use the check mark icon on hover to mark notifications as read.
* Filters: Filter notifications by record type (such as ticket or Issue), notification type (mentions, comments, assignments, etc.), or notified by (select from your colleagues or bots).
* Bulk actions: Select any notification and a new option to **Select All** will appear, allowing you to take bulk actions or mark all as read. It selects all updates on the current page, not all available updates.

### Notification priorities and channels

Notifications are prioritized and sent through different channels based on their importance.

**Important notifications**:

* Sent via all channels (in-app, email, push notifications, and integrations).
* Trigger a badge and bell sound on the **Updates** page.
* Show a toast notification in the app.

**Other notifications**:

* Sent only in-app to reduce noise.

### Email and push notifications

* Email notifications: Sent after a five-minute delay if the notification is unread.
* Push notifications: Sent immediately and marked as stale if read on the web.

By using these features, DevRev helps you efficiently manage updates, focus on critical tasks, and maintain a streamlined workflow.

## Personalizing notifications

DevRev allows users to personalize their notification preferences to ensure they receive only relevant updates. Follow these steps to personalize your notifications.

1. Go to [**Settings > Notifications**](https://app.devrev.ai/?setting=user-preferences) page.
2. Under the **General** panel, enable the following options as required:

   * Reminders: Set notifications for reminders.
   * Assignments: Enable notifications for new assignments.
   * Group Mentions: Enable notifications for mentions involving your affiliated groups.
   * Mentions: Enable alerts when you're mentioned.
   * Comments: Enable updates for comments on your subscribed records.
   * Attribute Updates: Enable notifications for attribute updates in records to which you subscribe.
3. Select the priority level (*Important*, *Others*, *Muted*) for each notification type. This determines the destination tab on the **Updates** page.
4. Under the **Bots and Snap-ins Notification** panel, manage bots and snap-ins notifications. These override default notifications.

> Currently, all customer messages are treated as comments and share the same priority.

## Collision and prioritization

DevRev prioritizes actions (comments, mentions, assignments, etc.) over actors (bots) to ensure efficiency and reduce noise. This means that the priority and channel of notifications are determined by the type of action, rather than solely by the actor performing the action.

Examples:

* If mentions are set to **Important** and a bot's notifications are set to **Others**, then bot mentions will only appear in the **Others** tab.
* If mentions are set to **Important** and a bot's notifications are also set to **Important**, then bot mentions will appear in the **Important** tab.
* If mentions are set to **Others** and a bot's notifications are set to **Important**, then bot mentions will still appear in the **Others** tab.

## Follow conversations

To receive updates about conversations in the Plug inbox, you must be a member of the support group. To manage membership of the support group go to [**Settings** > **Groups**](https://app.devrev.ai/?setting=groups).

For more information about groups, refer to [[support-articles/computer-by-devrev/groups|Groups]].

## Daily email digest

DevRev sends a daily email digest with a summary of unread updates. The updates in the email are not comprehensive but give you a snapshot of what you might have missed. Clicking the link in the email takes you to the **Updates** page in DevRev where you can see all the latest items.

## Related wiki nodes
- [[features/updates-feed]]

## Source
- DevRev support article [Updates](https://support.devrev.ai/en-US/devrev/article/knFZaYQO) (ART-21852)
