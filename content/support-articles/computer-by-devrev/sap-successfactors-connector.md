---
title: SAP SuccessFactors Connector
devrev_id: ART-30228
parent_directory: AirSync
translation_group: aU5kKfE7
modified_date: "2026-04-14T05:29:45.217Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/aU5kKfE7"
tags: []
top_category: Computer by DevRev
wiki_match: features/csat
match_score: 0.407
last_updated: 2026-05-11
summary: "The SAP SuccessFactors connector for DevRev (powered by Airdrop) syncs your HR data from SAP SuccessFactors into DevRev."
---

# SAP SuccessFactors Connector

The SAP SuccessFactors connector for DevRev (powered by [[glossary/airdrop|Airdrop]]) syncs your HR data from SAP SuccessFactors into DevRev. It brings employee profiles, organizational units, and company data into DevRev so you can [[features/build|build]] [[features/workflows|workflows]], reports, and automations on top of your people data.

---

## What this connector does

The connector reads data from your SAP SuccessFactors tenant using the OData V2 API and creates or updates the corresponding objects in DevRev. It supports both a full initial sync and ongoing incremental syncs to keep DevRev up to date as your HR data changes.

The connector is **read-only** — it does not write back to SAP SuccessFactors.

---

## What data it syncs

The connector syncs four types of objects into DevRev:

### Users

Active SuccessFactors user [[features/accounts|accounts]] are mapped to DevRev native user objects.

| Field | Description |
| --- | --- |
| Display name | Full name of the user |
| Email | Primary email address |

### Employee Profiles

Employee profiles are the richest entity. The connector consolidates data from multiple SuccessFactors entity sets (User, PerPersonal, PerEmail, EmpEmployment, EmpJob, EmpJobRelationships) into a single unified profile.

| Field | Description |
| --- | --- |
| First name, Last name, Middle name | Personal name fields |
| Gender | Gender |
| Date of birth | Date of birth |
| Nationality | Nationality |
| Marital status | Marital status |
| Primary email | Primary contact email |
| Job title | Current job title |
| Department | Department assignment |
| Division | Division assignment |
| Location | Office location |
| Cost center | Cost center assignment |
| Manager | Direct manager reference |
| Employee class | Classification type |
| Employment start date | Employment start date |
| Employment end date | Employment end date (for terminated employees) |
| Status | Active or terminated |

> **Note:** The connector includes terminated employees in the sync. If an employee no longer has an active user [[entities/account|account]] in SuccessFactors, their profile is still synced using employment records as the source of truth.

### Companies

Company records are synced along with their primary location data.

| Field | Description |
| --- | --- |
| Company name | Legal entity name |
| Country | Country of registration |
| Currency | Base currency |
| Location name | Primary office location name |
| Address | Physical address |
| Status | Active or inactive |

### Organizational Units

Organizational units represent the hierarchy of your organization. Four sub-types are synced and labeled with a `unit_type` field:

* **Department** — teams and functional [[entities/group|groups]]
* **Division** — business divisions
* **Business Unit** — top-level business units
* **Cost Center** — financial cost centers

| Field | Description |
| --- | --- |
| Unit name | Name of the org unit |
| Unit code | External identifier code |
| Unit type | Department, Division, BusinessUnit, or CostCenter |
| Head of unit | Person leading the unit |
| Parent unit | Reference to the parent unit (for hierarchy) |
| Status | Active or inactive |

---

## Prerequisites

Before you install the connector, make sure you have:

1. **A SAP SuccessFactors tenant** — either a production instance or a sandbox environment via the [SAP Business Accelerator Hub](https://api.sap.com/).
2. **An API Key** — obtain this from the SAP Business Accelerator Hub or your SuccessFactors Admin Console.
3. **Your SuccessFactors subdomain URL** — for example, `https://sandbox.api.sap.com/successfactors` for sandbox or your production tenant URL.
4. **DevRev admin access** — you need permission to install snap-ins and create connections.

---

## How to install

1. Go to your DevRev organization settings and open the **Snap-ins** section.
2. Find **SuccessFactors** in the snap-in catalog and click **Install**.
3. Follow the prompts to create a new connection (see [How to configure](https://github.com/DevRev-Labs/airsync-sap-successfactors-snap-in/blob/main/sap-successfactors-documentation.mdx#how-to-configure) below).
4. Once the connection is verified, the snap-in is installed and ready to use.

---

## How to configure

### Creating a connection

The connector uses an **API Key** to authenticate with SAP SuccessFactors.

1. During installation (or from the **Connections** settings page), select **SuccessFactors API Key Connection**.
2. Enter your **SuccessFactors subdomain**
3. Enter your **API Key** in the token field.
4. Click **Verify** — DevRev tests the connection by making a live request to the SuccessFactors API.
5. Save the connection.

---

## How to run a sync

### Initial sync

The initial sync fetches all available data from SuccessFactors and loads it into DevRev. It runs in four sequential phases:

1. **Users** — fetches all active SuccessFactors user accounts.
2. **Employee Profiles** — fetches employment records, personal info, job assignments, email addresses, and manager relationships, then joins them into unified profiles.
3. **Companies** — fetches company records and joins them with their location data.
4. **Organizational Units** — fetches departments, divisions, business units, and cost centers in parallel.

To start the initial sync:

1. Open the **Imports** section of your DevRev settings.
2. Find the **SuccessFactors** import and click **Start sync**.
3. Monitor progress from the sync status page.

The duration of the initial sync depends on the size of your SuccessFactors tenant. Large tenants with many employees may take several minutes.

### Incremental sync

After the initial sync completes, subsequent syncs are incremental. The connector only fetches records that have changed since the last successful sync, using the `lastModifiedDateTime` field on each SuccessFactors entity.

Incremental syncs run automatically on a schedule. You can also trigger one manually from the **Imports** settings page.

> **Fallback behavior:** If the incremental filter is rejected by the SuccessFactors API for a given entity type, the connector automatically falls back to a full sync for that entity. This is non-destructive and the rest of the sync continues normally.

### Sync resume on timeout

If a sync run exceeds the time limit, the connector saves its progress and DevRev resumes it automatically from where it left off. You do not need to restart the sync manually.

---

## Data refresh and pagination

* The connector fetches data in pages of **1,000 records** at a time.
* It retries automatically on server errors (5xx) with exponential backoff — up to 3 retries.
* It respects SAP SuccessFactors rate limits. If the API signals a rate limit, the connector pauses and retries automatically.

---

## Best practices

* **Run the initial sync during off-peak hours.** For large tenants, the initial sync makes a high volume of API calls. Running it outside business hours reduces the risk of hitting rate limits.
* **Keep your API Key secure.** Rotate your API Key periodically and update the connection in DevRev when you do.
* **Use sandbox for testing.** Use the SAP Business Accelerator Hub sandbox environment to validate the connector configuration before pointing it at your production tenant.
* **Do not modify synced objects manually.** Objects created by the connector are owned by the sync. Manual edits may be overwritten on the next sync run.
* **Monitor terminated employees.** The connector intentionally includes terminated employees. If you build automations or filters on employee profiles, account for records with `status = terminated`.
* **Org unit hierarchy.** Organizational units reference their parent unit via the `parent_unit` field. Use this to reconstruct the org hierarchy in DevRev queries and reports.

---

## Troubleshooting

| Symptom | Likely cause | What to do |
| --- | --- | --- |
| Connection verification fails | Invalid API Key or wrong subdomain URL | Double-check both fields; ensure the URL starts with `https://` |
| Sync shows no data | API Key lacks read access to required entity sets | Verify the API Key has access to User, PerPersonal, EmpEmployment, FOCompany, and related OData entity sets |
| Employees missing from profiles | Terminated employees with no User record | This is expected — terminated employees are included via EmpEmployment records |
| Incremental sync fetches all data | First run after a failed sync | Normal — the connector falls back to full sync when no valid timestamp is available |
| Sync times out and resumes | Large tenant or slow API | Normal — the connector saves progress and resumes automatically |

---

## Supported SuccessFactors API version

This connector uses the **OData V2 API** for SAP SuccessFactors. It is compatible with both production instances and sandbox environments on the SAP Business Accelerator Hub.

## Source
- DevRev support [[entities/article|article]] [SAP SuccessFactors Connector](https://support.devrev.ai/en-US/devrev/article/aU5kKfE7) (ART-30228)
