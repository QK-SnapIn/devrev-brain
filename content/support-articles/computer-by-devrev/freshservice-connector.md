---
title: Freshservice Connector
devrev_id: ART-34549
parent_directory: AirSync
translation_group: -b76x-5N
modified_date: "2026-04-30T12:03:06.501Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/-b76x-5N"
tags: []
top_category: Computer by DevRev
wiki_match: features/slas
match_score: 0.431
last_updated: 2026-05-11
---

# Freshservice Connector

# Freshservice AirSync Connector

The Freshservice AirSync connector imports your IT service management data from Freshservice into DevRev, making it available for search, linking, and collaboration alongside your product and engineering workflows. This connector supports bidirectional sync — data flows from Freshservice into DevRev, and updates made in DevRev on tickets, problems, and changes are written back to Freshservice.

## What this connector does

The connector reads data from your Freshservice account and creates or updates corresponding records in your DevRev org. It covers Tickets, Problems, Changes, Requesters, Agents, Groups, Departments, Knowledge Base Articles, Releases, Contracts, Vendors, Software, and Service Catalog Items — giving your teams a unified view of ITSM data directly in DevRev.

---

## What data gets synced

The connector fetches the following entity types from Freshservice:

### Work Items

| Entity | Description |
| --- | --- |
| Tickets | Support incidents from Freshservice. Each ticket is created as a DevRev ticket with subject, description, status, priority, assignee, and conversation history. |
| Problems | Root cause analysis items. Created as DevRev tickets with problem-specific fields such as known error flag and analysis notes. |
| Changes | Change request records. Created as DevRev tickets with change-specific fields such as risk, change type, and planned start/end dates. |

### People

| Entity | Description |
| --- | --- |
| Requesters | End users who submitted tickets. Created as DevRev rev-user identities with name and email. |
| Agents | Freshservice IT staff and support agents. Created as DevRev dev-user identities with name and email. |

### Organization

| Entity | Description |
| --- | --- |
| Groups | Freshservice support groups, mapped to DevRev groups. |
| Departments | Organizational departments from Freshservice, mapped to DevRev groups. |

### Knowledge & Assets

| Entity | Description |
| --- | --- |
| Knowledge Base Articles | Solution articles from your Freshservice knowledge base. Synced as DevRev articles with title and body. Requires at least one Solution Folder to exist in Freshservice. |
| Releases | Release management records. Synced as custom objects since they do not map to a standard DevRev type. |

### CMDB Entities (requires Freshservice CMDB plan)

| Entity | Description |
| --- | --- |
| Contracts | Asset and vendor contracts. Synced as custom objects. |
| Vendors | Vendor records from your Freshservice CMDB. Synced as custom objects. |
| Software | Software license records. Synced as custom objects. |
| Service Catalog Items | Service offerings from your Freshservice service catalog. Synced as custom objects. |

> **Note:** CMDB entities require a Freshservice plan that includes CMDB. On free or Starter plans, these entities are skipped automatically with a warning in the sync logs.

---

## Prerequisites

Before you install the connector, make sure you have:

* A DevRev account with permission to install snap-ins
* A Freshservice account with API access enabled
* A Freshservice API key from your profile settings (see How to configure below)
* Agent or Administrator role in Freshservice with read access to the entity types you want to sync

---

## How to install

1. Go to your DevRev org and open **Settings > Snap-ins**.
2. Find **Freshservice** in the snap-in catalog and click **Install**.
3. Follow the prompts to create a new connection (see How to configure below).
4. Once the connection is verified, the snap-in activates and is ready to sync.

---

## How to configure

### Setting up the connection

The connector uses a Freshservice API key to authenticate with the Freshservice REST API.

1. When prompted to create a connection, enter a name for this connection (for example, `Freshservice Production`).
2. In the **Freshservice Subdomain** field, enter your subdomain. For `acme.freshservice.com`, enter `acme` — do not include `.freshservice.com`.
3. In the **API Key** field, paste the API key from your Freshservice profile settings.

   * To find your API key: log in to Freshservice → click your profile picture → **Profile Settings** → scroll to the **API Key** section.
4. Click **Verify**. DevRev calls the Freshservice API to confirm the credentials are valid.
5. If verification succeeds, the connection is saved and your Freshservice subdomain is identified as the sync unit.

### Connection fields

| Field | Description |
| --- | --- |
| Connection Name | A label for this connection, such as `Freshservice Production`. |
| Freshservice Subdomain | The prefix of your Freshservice URL (e.g., `acme` for `acme.freshservice.com`). |
| API Key | Your Freshservice API key. Retrieved from your Freshservice profile settings. |

### Permissions the connector requires

The snap-in uses a DevRev service account with the following scopes:

| Scope | Purpose |
| --- | --- |
| `sync_unit:read` | Reads the Freshservice subdomain scope to determine what to sync |
| `sync_mapper_record:read` | Reads entity mappings to support incremental sync |
| `sync_mapper_record:write` | Writes entity mappings as Freshservice records are imported |
| `sync_snap_in:all` | Manages the extraction lifecycle and connector state |

---

## How the sync works

### Sync direction

This connector is primarily forward — data flows from Freshservice into DevRev. For tickets, problems, and changes, the connector also supports reverse sync: updates made to those records in DevRev are written back to Freshservice.

### Sync phases

Each sync run goes through four phases in order:

1. **Sync unit discovery** — The connector identifies your Freshservice subdomain as the sync scope.
2. **Metadata extraction** — The connector pushes the field schema for all entity types into DevRev so it knows what fields to expect.
3. **Data extraction** — The connector fetches all records for each entity type from the Freshservice REST API and imports them into DevRev. Pagination is handled automatically in batches of 100 records.
4. **Attachment extraction** — File attachments from tickets and knowledge base articles are downloaded and transferred to DevRev.

### Incremental sync

After the initial full sync, the connector supports incremental syncs for entities where Freshservice provides a timestamp filter. Only records modified since the last successful sync are re-fetched.

| Entity | Incremental support |
| --- | --- |
| Tickets | Yes — fetches only records updated since last sync |
| Problems | Yes — fetches only records updated since last sync |
| Changes | Yes — fetches only records updated since last sync |
| Releases | Yes — fetches only records updated since last sync |
| Requesters | No — full re-fetch every run |
| Agents | No — full re-fetch every run |
| Groups | No — full re-fetch every run |
| Departments | No — full re-fetch every run |
| Articles | No — full re-fetch every run |
| Contracts, Vendors, Software, Service Items | No — full re-fetch every run |

### Resumable syncs

If a sync run is interrupted (for example, due to a timeout), the connector saves its position after each page of data. When the next run starts, it resumes from where it left off rather than starting over. You do not need to take any action for this to happen.

---

## How records map to DevRev objects

| Freshservice entity | DevRev representation |
| --- | --- |
| Tickets | DevRev tickets |
| Problems | DevRev tickets |
| Changes | DevRev tickets |
| Requesters | DevRev rev-user identities |
| Agents | DevRev dev-user identities |
| Groups | DevRev groups |
| Departments | DevRev groups |
| Knowledge Base Articles | DevRev articles |
| Releases | Custom objects (`fresh_custom`) |
| Contracts, Vendors, Software, Service Items | Custom objects (`fresh_custom`) |

---

## Field reference

### Ticket fields synced to DevRev

| Freshservice field | DevRev field |
| --- | --- |
| Subject | Title |
| Description | Body |
| Status | Stage |
| Priority | Severity |
| Urgency | Urgency |
| Impact | Impact |
| Source | Source channel |
| Requester | Reported by |
| Assigned agent | Owned by |
| Group | Group |
| Tags | Tags |
| Created at | Created date |
| Updated at | Modified date |
| Due by | Target close date |
| Custom fields (`cf_*`) | Custom fields |
| Freshservice URL | Link to item |

### Status and priority mappings

**Status → Stage**

| Freshservice status | DevRev stage |
| --- | --- |
| Open | Queued |
| Pending | Awaiting customer response |
| Resolved | Resolved |
| Closed | Resolved |

**Priority → Severity**

| Freshservice priority | DevRev severity |
| --- | --- |
| Low | Low |
| Medium | Medium |
| High | High |
| Urgent | Blocker |

### Requester and agent fields synced to DevRev

| Freshservice field | DevRev field |
| --- | --- |
| Email | Email |
| Name | Display name, Full name |
| First name | First name |
| Last name | Last name |
| Phone | Phone |
| Job title | Job title (Requesters only) |
| Freshservice URL | Link to item |

---

## Reverse sync (DevRev → Freshservice)

When reverse sync is enabled, changes made to tickets, problems, and changes in DevRev are automatically written back to Freshservice.

### Supported operations

| Entity | Create | Update | Delete |
| --- | --- | --- | --- |
| Tickets | Yes | Yes | No |
| Problems | Yes | Yes | No |
| Changes | Yes | Yes | No |

Deletion is not supported. Deleting a record in DevRev does not delete it in Freshservice.

### Fields written back to Freshservice

Changes to the following DevRev fields trigger a write-back to Freshservice:

* Title (maps to Subject)
* Body (maps to Description)
* Stage (maps to Status)
* Severity (maps to Priority)
* Owned by (maps to Assigned agent)
* Custom fields prefixed with `cf_`

---

## Best practices

**Sync agents and requesters alongside tickets** — If you sync tickets without syncing agents or requesters, ticket assignments will show as "Unassigned." Sync all three together to preserve ownership and reporting relationships.

**Make HR changes in Freshservice first** — For entities synced forward-only (agents, requesters, groups, departments), any changes you make to those records in DevRev will be overwritten on the next sync. Update these records in Freshservice.

**Use incremental sync for ongoing updates** — Schedule incremental syncs hourly or every few hours rather than triggering manual full syncs. The manual "Sync Now" button always runs a full sync, which is slower and uses more API quota.

**Ensure agent emails match DevRev users** — The connector resolves ticket ownership by matching the Freshservice agent's email to a DevRev user. If emails don't match, tickets will appear unassigned. Keep email addresses consistent across both systems.

**Set up Solution Folders before syncing articles** — The Freshservice Articles API requires at least one Solution Folder to exist. Create a folder in Freshservice before running the sync if you want articles to be imported.

---

## Troubleshooting

### The sync is not starting

* Confirm the snap-in is in **Active** state in **Settings > Snap-ins**.
* Verify the connection by editing it in Settings and clicking **Verify** again.
* Check that your Freshservice API key is still valid and belongs to an active agent account.

### Records are missing from DevRev

* Check that the sync has fully completed all four phases. Metadata extraction must finish before data records are created.
* If a particular entity type is missing, the connector may have received a 403 error from Freshservice for that endpoint. Check the snap-in logs for warnings about skipped entities and confirm your API key has access to those modules.
* CMDB entities (Contracts, Vendors, Software, Service Items) are only available on Freshservice plans that include CMDB. These are skipped on free or Starter plans.

### Tickets show "Unassigned" as owner

The connector matches Freshservice agent emails to DevRev users. If an agent's email in Freshservice does not match any DevRev user, the ticket owner will appear as "Unassigned." Ensure agents in Freshservice share the same email addresses as their DevRev user accounts.

### Articles are not syncing

Freshservice's Articles API requires at least one Solution Folder to exist in your account. Create a Solution Folder in Freshservice and re-run the sync.

### Authentication errors

* Confirm your API key is valid by testing it directly:

  ```
  curl -u YOUR_API_KEY:X https://YOUR_SUBDOMAIN.freshservice.com/api/v2/agents/me
  ```
* Make sure the subdomain field contains only the prefix — do not include `.freshservice.com`.

### Reverse sync is not writing back to Freshservice

* Confirm reverse sync is enabled in the AirSync configuration.
* Check that custom fields you expect to sync back are prefixed with `cf_` in DevRev.

---

## Related resources

* [DevRev AirSync overview](https://developer.devrev.ai/airsync)
* [Managing snap-ins in DevRev](https://developer.devrev.ai/snapin-development/concepts)
* [Freshservice API documentation](https://api.freshservice.com/)

## Source
- DevRev support article [Freshservice Connector](https://support.devrev.ai/en-US/devrev/article/-b76x-5N) (ART-34549)
