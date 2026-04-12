---
title: Jira Integration
type: feature
status: draft
sources: [raw/docs/devrev-agent-dump-integrations.md]
related: ["features/airdrop"]
last_updated: 2026-04-12
---

# Jira Integration

## What it does
The Jira integration uses AirSync to provide bidirectional sync between Jira (Cloud and Data Center) and DevRev. It imports Jira projects as sync units, maps issue types and fields between systems, and supports one-way or bidirectional periodic sync. Jira Service Management (JSM) is also supported with additional object types.

## Why it exists
Many teams migrating to or co-existing with DevRev have existing Jira projects. This integration ensures issues, comments, labels, attachments, and statuses stay synchronized between both systems without manual re-entry.

## Setup flow (step-by-step)

1. Go to **Settings -> Integrations -> AirSyncs**.
2. Select **AirSync** (or **Start AirSync** if first time).
3. Create a new connection to your Jira site (or use an existing one).
   - **Jira Cloud:** Uses OAuth for authentication.
   - **Jira Data Center:** Uses PAT-based connection (only supported type).
4. Select the Jira project to import (each project becomes a sync unit).
5. Configure the import recipe (see field mapping below).
6. DevRev recommends using a **dedicated Jira administrator account** for the connection to avoid individual users receiving excessive Jira notifications.

## Field mapping (Jira -> DevRev)

DevRev auto-maps Jira fields to DevRev fields where possible, but prompts for manual mapping when needed. Key mapping decisions:

- **Issue type mapping:** Jira issues -> DevRev issues (default) or DevRev tickets. Jira epics -> DevRev enhancements (optional).
- **Custom fields:** Imported and mapped; can be imported as tags or custom fields.
- **Enum values:** e.g. Jira priority "Critical" can be mapped to DevRev "P0". In the reverse direction, only values that were mapped in the forward direction are available as targets (prevents round-trip inconsistencies).
- **Comments:** Synced bidirectionally. Reverse-synced comments are created in the name of the Jira user who authorized the connection, with a prefix indicating the original DevRev author and timestamp.

## Supported object types

### Jira Software (Cloud and Data Center)

| Jira object | DevRev object | Sync to DevRev | Sync to Jira |
|---|---|---|---|
| Issue | Issue/Ticket | Yes | Yes |
| Epic | Issue/Ticket/Enhancement | Yes | Yes |
| Comment on Issue | Comment on Issue/Ticket | Yes | Yes |
| Label on Issue | Tag on Issue/Ticket | Yes | Yes |
| Link between Issues | Link between Issues/Tickets | Yes | Yes |
| Attachment on Issue | Attachment on Issue/Ticket | Yes | Yes |
| Status/States | Stage of Issue/Ticket | Yes | Yes |
| Workflow | Stage Transition Diagram | Yes | No |
| User | DevUser | Yes | No |
| Sprint | Sprint | No | No |
| Filter | Vista | No | No |
| Automation | Snap-in | No | No |

### Jira Service Management (additional)

JSM additionally supports: Tickets (mapped from JSM Issues), Private/Public Comments, Customer records, Organizations (mapped to Accounts), App Users (mapped to SysUsers).

## Sync direction

**Both one-way and bidirectional are supported:**

- **One-way (Jira -> DevRev):** Import a Jira project once, then optionally re-sync to pull in new changes.
- **One-way (DevRev -> Jira):** Write back DevRev changes to previously imported Jira issues.
- **Bidirectional (periodic sync):** Enabled via **Settings -> AirSync -> ... -> Set Periodic Sync**. Runs hourly by default. Changes on either side are reflected on the other.

**How AirSync knows what to sync in 2-way mode:** When issues are imported from Jira, AirSync creates a subtype in DevRev for each Jira issue type (e.g. `Jira Project 1/Bug`). Only DevRev work items with one of these subtypes are synced back to Jira. New DevRev issues without a Jira subtype are not synced unless explicitly marked.

## Key behaviors
- OAuth for Jira Cloud, PAT for Jira Data Center.
- Auto-mapping with manual override for fields, issue types, and enums.
- Reverse-direction enum values constrained to forward-mapped values only.
- Bidirectional comment sync with author attribution prefix.
- Hourly periodic sync by default when bidirectional mode is enabled.
- Dedicated admin account recommended to avoid notification floods.
- Subtypes created per Jira issue type to control reverse sync scope.

## Entry points
- **Settings -> Integrations -> AirSyncs** (primary)
- **Marketplace:** search "Jira AirSync"

## Related flows
- [gap] Jira initial import flow
- [gap] Jira bidirectional periodic sync flow
- [gap] Jira field mapping configuration flow

## Related scenarios
- [gap] Scenarios to be created

## Open questions
- [gap] What is the exact behavior for Jira Data Center-specific nuances?
- [gap] How are Jira workflows mapped to DevRev stage transition diagrams?
- [gap] What happens when a Jira issue type has no corresponding DevRev type?
