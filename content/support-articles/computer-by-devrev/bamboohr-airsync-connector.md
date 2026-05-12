---
title: BambooHR AirSync Connector
devrev_id: ART-27919
parent_directory: AirSync
translation_group: OG12XyE2
modified_date: "2026-04-07T05:03:36.787Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/OG12XyE2"
tags: []
top_category: Computer by DevRev
wiki_match: glossary/airsync
match_score: 0.85
last_updated: 2026-05-11
related: ['glossary/airsync']
summary: "The BambooHR AirSync connector imports your HR data from BambooHR into DevRev."
---

# BambooHR AirSync Connector

# BambooHR AirSync Connector

The BambooHR [[glossary/airsync|AirSync]] connector imports your HR data from BambooHR into DevRev. It keeps employee records, departments, time-off requests, and other HR entities in sync so your team can work with up-to-date HR data directly in DevRev.

---

## What this connector does

The connector reads data from your BambooHR [[entities/account|account]] and creates corresponding records in DevRev. After the initial full import, it runs incremental syncs that only pull in records that have changed since the last run—keeping your data fresh without redundant transfers.

The connector also supports **two-way sync for employees**: changes made to employee records in DevRev can be written back to BambooHR.

---

## What data gets synced

The connector imports the following entities from BambooHR:

### Core entities

| Entity | Description |
| --- | --- |
| **Employees** | Employee profiles including name, work email, job title, department, hire date, and all standard and custom fields |
| **Departments** | Department records derived from employee data |

### Employee child records

These records are linked to individual employees:

| Entity | Description |
| --- | --- |
| **Job History** | Historical job role and compensation changes per employee |
| **Training Records** | Training completions and certifications |
| **Performance Goals** | Goals set for employees in BambooHR performance management |
| **Emergency Contacts** | Emergency contact information per employee |
| **Dependents** | Dependent records associated with each employee |
| **Employee Files** | File attachments uploaded to employee profiles (imported as DevRev attachments when enabled) |

### Optional entities

| Entity | Description |
| --- | --- |
| **Time Off Requests** | Employee time-off requests and approvals |
| **ATS Jobs** | Job postings from BambooHR Applicant Tracking |
| **ATS Applications** | Candidate applications linked to job postings |
| **Benefits** | Company benefit plans and employee benefit enrollments |
| **Timesheet Entries** | Time tracking entries from BambooHR Time Tracking |

> **Note:** Optional entities such as ATS, Benefits, and Time Tracking are only synced if your BambooHR plan includes access to those modules. If your account does not have access to a module, the connector skips it gracefully and continues syncing other data.

---

## Prerequisites

Before you install the connector, make sure you have:

* A BambooHR account with **admin access** (required to generate an API key)
* Your **BambooHR subdomain** (the [[entities/part|part]] before `.bamboohr.com` in your account URL — for example, if your URL is `https://acme.bamboohr.com`, your subdomain is `acme`)
* A DevRev account with permission to install snap-ins

### How to get your BambooHR API key

1. Log in to BambooHR as an admin.
2. Click your name in the top-right corner and select **API Keys**.
3. Click **Add New Key**, give it a name (for example, `DevRev AirSync`), and click **Generate Key**.
4. Copy the API key — you need it during connector setup.

---

## How to install the connector

1. Go to the [DevRev Marketplace](https://app.devrev.ai/marketplace) and [[features/search|search]] for **BambooHR AirSync**.
2. Click the connector listing and select **Install**.
3. Follow the on-screen prompts to complete installation.

Once installed, the connector appears in your DevRev snap-ins list.

---

## How to configure the connector

After installation, you connect the snap-in to your BambooHR account and set sync preferences.

### Step 1: Create a connection

1. In DevRev, navigate to **Settings > Integrations > BambooHR AirSync**.
2. Click **Add Connection**.
3. Enter:

   * **BambooHR Subdomain** — your subdomain (for example, `acme`)
   * **API Key** — the API key you generated in BambooHR
4. Click **Save**. DevRev verifies the credentials against your BambooHR account.

### Step 2: Set sync preferences

Once the connection is saved, you configure what gets imported:

| Setting | Default | Description |
| --- | --- | --- |
| **Historical start date** | `2020-01-01` | The earliest date from which records are imported. Use `YYYY-MM-DD` format. Cannot be set to a future date. |
| **Import attachments** | Enabled | When enabled, employee file attachments from BambooHR are imported as DevRev attachments. Disable this if you do not need files or want to reduce sync time. |
| **Include terminated employees** | Disabled | When enabled, employees who have left the organization are also imported. Enable this if you need a complete historical record. |

Click **Save** after updating your preferences.

---

## How to run a sync

### Initial sync

After configuration, click **Start Sync** to begin the first full import. The initial sync fetches all records from BambooHR going back to your configured historical start date. Depending on the size of your organization and the number of entities, this may take several minutes to complete.

You can monitor sync progress from the connector's status panel.

### Incremental sync

After the initial sync completes, the connector automatically runs incremental syncs. Each incremental run only fetches records that have changed in BambooHR since the last sync — so subsequent syncs are significantly faster than the initial import.

### Manual sync

You can trigger a manual sync at any time by clicking **Sync Now** in the connector settings. This is useful after bulk updates in BambooHR or when you want to pull in changes immediately rather than waiting for the next scheduled run.

---

## Two-way sync for employees

The connector supports writing employee changes from DevRev back to BambooHR. When you update an employee record in DevRev, the connector pushes those changes to the corresponding BambooHR employee profile.

Two-way sync applies to the **Employees** entity only. All other entities are read-only (imported from BambooHR into DevRev).

---

## Best practices

* **Set a meaningful historical start date.** If you only need data from the past two years, set the start date accordingly. Importing many years of history increases initial sync time and storage.
* **Enable terminated employees selectively.** Include terminated employees only if your use case requires historical records. Keeping this disabled reduces noise in DevRev.
* **Disable attachment import if not needed.** Employee file attachments can be large and increase sync duration. If your team does not use employee files in DevRev, disable this option.
* **Keep your API key secure.** Regenerate your BambooHR API key immediately if it is ever exposed. Update the connection in DevRev after regenerating.
* **Do not share API keys across integrations.** Generate a dedicated API key in BambooHR specifically for the DevRev connector. This makes it easier to revoke access without affecting other integrations.
* **Verify BambooHR module access before expecting optional entities.** If ATS, Benefits, or Time Tracking data does not appear in DevRev after a sync, check that your BambooHR plan includes those modules.

---

## Troubleshooting

### The connection fails during setup

* Confirm your API key is correct and has not been revoked in BambooHR.
* Verify your subdomain is entered without `https://` or `.bamboohr.com` — enter only the subdomain portion.
* Make sure your BambooHR account is active and accessible.

### Some entities are missing after a sync

* Optional entities (ATS, Benefits, Timesheet) only sync if your BambooHR plan includes those modules. Check your BambooHR subscription.
* If terminated employees are missing, enable the **Include terminated employees** setting and re-run the sync.

### Attachments are not appearing in DevRev

* Confirm **Import attachments** is enabled in sync preferences.
* Verify that employee files exist in BambooHR (navigate to an employee profile and check the **Files** tab).
* Re-run the sync after enabling the setting — attachments from past syncs are not retroactively imported.

### Employee changes in DevRev are not reflected in BambooHR

* Two-way sync requires that the employee record was originally created via the connector. Records created manually in DevRev are not written back to BambooHR.
* Confirm that the API key used for the connection has write permissions in BambooHR.

### The sync takes a long time

* The initial sync is expected to take longer than subsequent incremental syncs, especially for large organizations or long historical date ranges.
* If incremental syncs are slow, consider whether a large number of records changed in BambooHR since the last run (for example, after a bulk import or update in BambooHR).

---

## Frequently asked questions

**Does the connector sync custom fields?** Yes. The connector automatically discovers custom fields configured in your BambooHR account and imports them alongside standard fields.

**How often does the connector sync?** Incremental syncs run on a schedule managed by DevRev. You can also trigger a manual sync at any time from the connector settings.

**Can I sync only specific departments or employee [[entities/group|groups]]?** The current connector imports all employees (and optionally terminated employees) from your BambooHR account. Department or [[entities/group|group]] filtering is not supported at this time.

**What happens if BambooHR is temporarily unavailable?** The connector retries failed requests automatically. If BambooHR is rate-limiting requests, the connector waits and resumes. The sync state is preserved so the connector picks up where it left off rather than restarting from scratch.

**Is employee data encrypted in transit?** Yes. All communication between DevRev and BambooHR uses HTTPS.

## Related wiki nodes
- [[glossary/airsync]]

## Source
- DevRev support [[entities/article|article]] [BambooHR AirSync Connector](https://support.devrev.ai/en-US/devrev/article/OG12XyE2) (ART-27919)
