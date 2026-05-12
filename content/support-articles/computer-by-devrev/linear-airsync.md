---
title: Linear AirSync
devrev_id: ART-22015
parent_directory: AirSync
translation_group: 8eMG410c
modified_date: "2026-03-27T11:07:05.039Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/8eMG410c"
tags: []
top_category: Computer by DevRev
wiki_match: glossary/airsync
match_score: 0.85
last_updated: 2026-05-11
related: ['glossary/airsync']
summary: "To ease the transition from Linear issues to DevRev, you can import and sync Linear issues with DevRev."
---

# Linear AirSync

# Linear AirSync

To ease the transition from Linear [[features/issues|issues]] to DevRev, you can import and sync Linear issues with DevRev.

> For more information, refer to the [Linear AirSync snap-in](https://marketplace.devrev.ai/) on the DevRev marketplace.

### Supported objects

The table below lists Linear object types and their DevRev equivalents. Objects marked **Sync to DevRev** or **Sync to Linear** are eligible for import and synchronization.

| Linear object | DevRev object | Sync to DevRev | Sync to Linear |
| --- | --- | --- | --- |
| [[entities/issue|Issue]] | Issue | ✅ | ✅ |
| Comment on Issue | Comment on Issue | ✅ | ✅ |
| Label on Issue | Tag on Issue | ✅ | ✅ |
| Attachment on Issue | Attachment on Issue | ✅ | ✅ |
| User | DevUser | ✅ | ❌ |
| View | [[glossary/vista|Vista]] | ❌ | ❌ |
| Project | [[entities/enhancement|Enhancement]] | ✅ | ✅ |
| Project Milestones | Tag on Enhancement | ✅ | ❌ |
| Team | [[entities/group|Group]] | ✅ | ❌ |

> **Note:** Empty teams are also imported to maintain organizational structure, even when they contain no members or issues.

## Limitations

The following objects have sync limitations:

- **Team Members.** Not supported due to rate-limit limitations. Empty [[entities/group|groups]] are imported to support reverse sync.
- **Views.** Cannot be imported or synced.
- **Project Milestones.** Can be imported from Linear to DevRev as custom objects but cannot be synced back to Linear.

### Importing from Linear

For best results, AirSyncs should be done using an administrator [[entities/account|account]] on the external source. This ensures all necessary permissions are available to complete the import successfully.

1. Go to **Settings > Snap-ins** and install **Linear**.

> There may be an existing **Linear Issues** snap-in already added. If so, **Add** the other.

1. Go to **Settings > Integrations > AirSyncs** and click **[[glossary/airsync|AirSync]]**.
2. Under the **Snap-ins** tab, select **Linear**.
3. Follow the prompt to create a connection, then click **Authorize** and select the organization once authorization is complete.
4. A recipe is presented where you select what data to import and how to map it. The recommended values are preselected.

### Troubleshooting Linear Connection

If you see **"Manage"** instead of **"Connection"** when setting up the Linear AirSync, this indicates the OAuth app is already installed in your Linear workspace.

To resolve this issue:

1. Go to your Linear workspace **Settings**.
2. Navigate to the **API** section.
3. Find the existing DevRev OAuth application.
4. Click **"Revoke"** to remove the existing authorization.
5. Return to DevRev and attempt to authorize the connection again.
6. The connection should now properly establish.

> This typically occurs when a previous connection attempt was made or if the OAuth app was previously installed.

## Related wiki nodes
- [[glossary/airsync]]

## Source
- DevRev support [[entities/article|article]] [Linear AirSync](https://support.devrev.ai/en-US/devrev/article/8eMG410c) (ART-22015)
