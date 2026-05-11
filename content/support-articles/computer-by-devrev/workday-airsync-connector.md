---
title: Workday AirSync Connector
devrev_id: ART-30224
parent_directory: AirSync
translation_group: G3qXTXDm
modified_date: "2026-04-14T04:54:35.955Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/G3qXTXDm"
tags: []
top_category: Computer by DevRev
wiki_match: glossary/airsync
match_score: 0.85
last_updated: 2026-05-11
related: ['glossary/airsync']
---

# Workday AirSync Connector

# Workday AirSync Connector

The Workday AirSync connector imports your HR data from Workday into DevRev, making it available for search, linking, and collaboration alongside your product and engineering workflows. This connector performs a one-way sync — data flows from Workday into DevRev only.

---

## What this connector does

The connector reads data from your Workday tenant and creates or updates corresponding records in your DevRev org. It covers Workers, Organizations, Recruiting, Absence, Compensation, Payroll, Time Tracking, Talent, and Benefits — giving your teams a unified view of people and HR data directly in DevRev.

---

## What data gets synced

The connector fetches the following entity types from Workday:

### People

| Entity | Description |
| --- | --- |
| **Workers** | All active and inactive workers from your Workday tenant. Each worker is created as a DevRev user identity with name and email. |
| **Worker Profiles** | Extended HR record for each worker, including job title, department, manager, location, hire date, compensation group, and personal details. |
| **Candidates** | Job candidates from Workday Recruiting, created as DevRev rev-user identities. |
| **Candidate Profiles** | Extended profile for each candidate with application details and recruiting-specific fields. |

### Organization

| Entity | Description |
| --- | --- |
| **Organizations** | Workday organizations (Supervisory, Cost Center, Region, Company), mapped to DevRev groups. |
| **Organization Members** | Membership records that link workers to their organizations, preserving your org chart structure. |

### HR Modules

| Entity | Sub-types synced |
| --- | --- |
| **Staffing** | Job Profiles, Positions |
| **Recruiting** | Job Postings, Job Applications |
| **Absence** | Time Off Requests, Leave Requests |
| **Compensation** | Compensation Grades, Compensation Plans |
| **Payroll** | Pay Groups, Pay Periods |
| **Time Entries** | Worker time tracking records |
| **Talent** | Goals, Performance Reviews |
| **Benefits** | Benefit Plans, Benefit Enrollments |

> **Note:** For entities that have multiple sub-types (such as Staffing and Recruiting), a `*_type` field on each record tells you which sub-type it represents so you can filter or group them in DevRev.

---

## Prerequisites

Before you install the connector, make sure you have:

* A DevRev account with permission to install snap-ins
* A Workday bearer token issued by your Workday tenant administrator
* Access to the Workday REST API for your tenant

---

## How to install

1. Go to your DevRev org and open **Settings > Snap-ins**.
2. Find **Workday** in the snap-in catalog and click **Install**.
3. Follow the prompts to create a new connection (see [How to configure](https://github.com/DevRev-Labs/airsync-workday-snap-in/blob/main/workday-documentation.mdx#how-to-configure) below).
4. Once the connection is verified, the snap-in activates and is ready to sync.

---

## How to configure

### Setting up the connection

The connector uses a bearer token to authenticate with the Workday REST API.

1. When prompted to create a connection, enter a name for this connection (for example, `Workday Production`).
2. In the **API Token** field, paste the bearer token provided by your Workday administrator.

   > You do not need to include the `Bearer` prefix — the connector adds it automatically.
3. Click **Verify**. DevRev calls the Workday health endpoint to confirm the token is valid and to detect your tenant name.
4. If verification succeeds, the connection is saved and your Workday tenant is identified as the sync unit.

### Connection fields

| Field | Description |
| --- | --- |
| **API Token** | The bearer token for your Workday REST API. Provided by your Workday administrator. |

### Permissions the connector requires

The snap-in uses a DevRev service account with the following scopes:

| Scope | Purpose |
| --- | --- |
| `sync_unit:read` | Reads the Workday tenant scope to determine what to sync |
| `sync_mapper_record:read` | Reads entity mappings to support incremental sync |
| `sync_mapper_record:write` | Writes entity mappings as Workday records are imported |
| `sync_snap_in:all` | Manages the extraction lifecycle and connector state |

---

## How the sync works

### Sync direction

This connector is **forward-only**: data flows from Workday into DevRev. Changes made in DevRev are not written back to Workday.

### Sync phases

Each sync run goes through four phases in order:

1. **Sync unit discovery** — The connector identifies your Workday tenant as the sync scope.
2. **Metadata extraction** — The connector pushes the field schema for all 14 entity types into DevRev so it knows what fields to expect.
3. **Data extraction** — The connector fetches all records for each entity type from the Workday REST API and imports them into DevRev. Pagination is handled automatically in batches of 100 records.
4. **Attachments extraction** — This phase completes immediately; the Workday REST API does not expose binary file attachments.

### Sync frequency

The connector performs a **full sync** on every run. All records for all entity types are re-fetched and updated in DevRev each time the sync runs.

### Resumable syncs

If a sync run is interrupted (for example, due to a timeout), the connector saves its position after each page of data. When the next run starts, it resumes from where it left off rather than starting over. You do not need to take any action for this to happen.

### How records map to DevRev objects

| Workday entity | DevRev representation |
| --- | --- |
| Workers | DevRev user identities (`devu`) + Worker Profile custom objects |
| Candidates | DevRev rev-user identities (`revu`) + Candidate Profile custom objects |
| Organizations | DevRev groups |
| Organization Members | Group membership records linking workers to organizations |
| All other HR entities | Custom objects with the relevant fields from Workday |

Workers and Candidates use a **dual-object pattern**: one object holds the DevRev identity (used for mentions, assignments, and linking) and a second custom object holds all the Workday HR fields. This preserves references across all related records.

---

## Field reference

### Worker fields synced to DevRev

| Workday field | DevRev field |
| --- | --- |
| Legal name (full) | Display name, Full name |
| Primary email | Email |
| Worker type | Worker Type |
| Worker status | Worker Status |
| Organization | Organization (name + ID) |
| Position | Position (name + ID) |
| Business title | Business Title |
| Start date | Start Date |
| Hire date | Hire Date |
| End employment date | End Employment Date |
| Location | Location |
| Job profile | Job Profile (name + ID) |
| Department | Department (name + ID) |
| Manager | Manager (name + ID) |
| Pay group | Pay Group |
| Time type | Time Type |
| First name, Last name | First Name, Last Name |
| Date of birth | Date of Birth |
| Gender | Gender |
| Country of birth | Country of Birth |
| Primary phone | Primary Phone |
| Home address | Address Line 1, City, State, Postal Code, Country, Address Type |
| Workday profile URL | Workday URL |

### Organization fields synced to DevRev

| Workday field | DevRev field |
| --- | --- |
| Descriptor (name) | Name |
| Organization type | Description, Organization Type |
| Organization code | Organization Code |
| Superior organization | Superior Organization (name + ID) |
| Top-level organization | Top Level Organization |
| Manager | Manager (name + ID) |
| Member count | Member Count |
| Inactive flag | Inactive |
| Workday profile URL | Workday URL |

---

## Best practices

* **Use the Worker Profile custom object for HR searches** — Worker identity objects hold name and email for linking purposes. The Worker Profile custom object holds all HR fields and is the right place to search for job titles, departments, and org details.
* **Filter combined entities by sub-type** — Entities like Staffing, Recruiting, and Benefits contain multiple sub-types in a single custom object. Use the `*_type` field (for example, `staffing_type`) to filter records by Job Profile vs. Position or Job Posting vs. Job Application.
* **Check Organization Members for org chart structure** — The Organization Members entity records each worker-to-organization relationship. Use this to navigate your org hierarchy in DevRev.
* **Do not edit synced records directly in DevRev** — Since this connector does not write back to Workday, any changes you make to synced records in DevRev are overwritten on the next sync. Make HR changes in Workday first.
* **Verify your bearer token regularly** — If the Workday API token expires, the connector fails authentication and the sync stops. Refresh the token in the connection settings before expiry to avoid gaps in your data.

---

## Troubleshooting

### The sync is not starting

* Confirm the snap-in is in **Active** state in **Settings > Snap-ins**.
* Verify the connection by editing it in Settings and clicking **Verify** again.
* Check that your Workday API token has not expired.

### Workers or organizations are missing

* Check that the sync has fully completed all four phases. Metadata extraction must finish before data records are created.
* If a particular entity type is missing, the connector may have received a permissions error (HTTP 403) from Workday for that endpoint. Check the snap-in logs for warnings about skipped entities and ensure your token has access to those Workday modules.

### Custom object fields are empty or missing

* For combined entity types (Staffing, Recruiting, Absence, Compensation, Payroll, Talent, Benefits), ensure the `*_type` enum custom field is installed correctly. Check the snap-in logs for field mapping errors.

### Authentication errors

* Confirm your token is valid by testing it against your Workday API.
* Make sure you are entering the raw token value without a `Bearer` prefix — the connector prepends it automatically.

---

## Related resources

* [DevRev AirSync overview](https://devrev.ai/docs/airsync)
* [Managing snap-ins in DevRev](https://devrev.ai/docs/snap-ins)

## Related wiki nodes
- [[glossary/airsync]]

## Source
- DevRev support article [Workday AirSync Connector](https://support.devrev.ai/en-US/devrev/article/G3qXTXDm) (ART-30224)
