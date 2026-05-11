---
title: Snowflake AirSync
devrev_id: ART-25907
parent_directory: AirSync
translation_group: 8AJRfbiU
modified_date: "2026-04-16T14:43:58.11Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/8AJRfbiU"
tags: []
top_category: Computer by DevRev
wiki_match: glossary/airsync
match_score: 0.85
last_updated: 2026-05-11
related: ['glossary/airsync']
---

# Snowflake AirSync

The Snowflake AirSync simplifies migration from Snowflake to DevRev, supporting both one-time imports and ongoing syncs.

# Supported objects

The following is a list of Snowflake objects and their corresponding DevRev equivalents. Those marked as **Sync to DevRev** are eligible for import from Snowflake to DevRev.

| Snowflake object | DevRev object | Sync to DevRev |
| --- | --- | --- |
| Table (rows) | Custom Object | ✅ |

Each Snowflake table selected for sync is mapped as a DevRev custom object type. All table columns are automatically mapped as fields on the custom object. In addition, the following stock fields are populated for every record:

| Field | Description |
| --- | --- |
| Snowflake Record Status | Indicates whether the record is **ACTIVE** or **DELETED** in Snowflake. During incremental syncs, rows deleted in Snowflake are marked as `DELETED`; all other rows are marked `ACTIVE`. |

# Import from Snowflake

1. Log in to DevRev.
2. Navigate to **Settings > Integrations > Snap-ins**, search for **Snowflake** under **All Snap-ins**.
3. Click **Add and Install Snap-in**.
4. Navigate to **Settings > Integrations > Airsync** in the left-navigation.
5. Click **Airsync** in the top right corner and select **Snowflake**.
6. Create a new connection to your Snowflake account using key-pair authentication. You will need to provide:

* **Sub Domain** — This is the **Account Identifier** from Snowflake (e.g., `org-account`). You can find it under **Admin > Accounts** in the Snowflake web app, or by running `SELECT CURRENT_ORGANIZATION_NAME() || '-' || CURRENT_ACCOUNT_NAME();` in a Snowflake worksheet.
* **Username** — This is the **Login Name** of the user in Snowflake. You can verify it by running `DESC USER <username>;` and checking the `LOGIN_NAME` property.
* **Private Key** — Your RSA private key in PEM format (including the `-----BEGIN` and `-----END` header/footer). See ***Key-pair authentication setup*** below.
* **Private Key Passphrase** *(optional)* — If your private key is encrypted, provide the passphrase. Must be at least **8 characters** long.
* **Account Identifier** — Same as the Sub Domain value above your Snowflake account identifier.
* **Warehouse Name** — The Snowflake virtual warehouse to use for compute.
* **Role** — The Snowflake role to assume for the connection.

7. Once the connection is established, select the Snowflake tables you want to import and specify the DevRev part to be used for any imported work. This initiates a bulk import of the selected tables.

   DevRev makes an effort to automatically map fields from Snowflake to the corresponding fields in DevRev. However, you may be prompted to manually map certain fields if needed.

## Key-pair authentication setup

The Snowflake connector uses key-pair authentication with JWT tokens. Follow the steps below to generate the required key pair and configure it in Snowflake.

For more information, refer to the Snowflake documentation on [Key-pair authentication](https://docs.snowflake.com/en/user-guide/key-pair-auth).

**Step 1: Generate a private key**

Generate an RSA private key. You can choose to create either an **unencrypted** or **encrypted** key.

**Unencrypted key:**

```
openssl genrsa 2048 | openssl pkcs8 -topk8 -inform PEM -out rsa_key.p8 -nocrypt
```

**Encrypted key (recommended for production):**

```
openssl genrsa 2048 | openssl pkcs8 -topk8 -inform PEM -v2 aes-256-cbc -out rsa_key.p8
```

You will be prompted to set a passphrase. The passphrase **must be at least 8 characters** long — this is required when configuring the connection in DevRev.

**Step 2: Generate the public key**

Extract the public key from the private key:

```
openssl rsa -in rsa_key.p8 -pubout -out rsa_key.pub
```

**Step 3: Assign the public key to your Snowflake user**

Log in to Snowflake as an `ACCOUNTADMIN` (or a role with `MANAGE GRANTS` privileges) and assign the public key to the user that the connector will use:

```
ALTER USER <username> SET RSA_PUBLIC_KEY='MIIBIjANBgkqh...';
```

> Copy the public key value from `rsa_key.pub`, removing the `-----BEGIN PUBLIC KEY-----` and `-----END PUBLIC KEY-----` header/footer and any newlines.

You can verify the key was assigned correctly:

```
DESC USER <username>;
```

Look for the `RSA_PUBLIC_KEY_FP` property in the output.

**Step 4: Provide the private key in DevRev**

When configuring the connection in DevRev, paste the **full contents** of your private key file (`rsa_key.p8`) into the **Private Key** field, **including** the `-----BEGIN ENCRYPTED PRIVATE KEY-----` / `-----END ENCRYPTED PRIVATE KEY-----` (or `-----BEGIN PRIVATE KEY-----` / `-----END PRIVATE KEY-----` for unencrypted keys) header and footer.

If you generated an encrypted key, also provide the passphrase in the **Private Key Passphrase** field.

## Snowflake permissions

The Snowflake user (and role) used for the connection must have the following permissions:

| Permission | Scope | Purpose |
| --- | --- | --- |
| `USAGE` | Database, Schema | Discover and access databases and schemas |
| `SELECT` | Table | Read table data during extraction |
| `CREATE STAGE` | Schema | Create temporary internal stages for bulk data export (dropped after extraction) |
| `CREATE` and `MODIFY` | Streams | Create streams for incremental (change-based) sync |
| `USAGE` | Warehouse | Execute queries using the specified virtual warehouse |

> It's mandatory for tables to have `PRIMARY KEYS`. The user must also have the ability to run `SHOW DATABASES`, `SHOW PRIMARY KEYS`, and `DESC TABLE` on the tables being synced.

**For example, granting minimum required permissions:**

```
-- Grant database and schema access
GRANT USAGE ON DATABASE <database> TO ROLE <role>;
GRANT USAGE ON SCHEMA <database>.<schema> TO ROLE <role>;

-- Grant table access
GRANT SELECT ON TABLE <database>.<schema>.<table> TO ROLE <role>;

-- Grant stage creation in the schema
GRANT CREATE STAGE ON SCHEMA <database>.<schema> TO ROLE <role>;

-- Grant stream creation for incremental sync
GRANT CREATE STREAM ON SCHEMA <database>.<schema> TO ROLE <role>;

-- Grant warehouse usage
GRANT USAGE ON WAREHOUSE <warehouse> TO ROLE <role>;
```

## Enable change tracking

Change tracking must be enabled on each table before it can be synced. The connector checks for this and will report an error if change tracking is not enabled.

To enable change tracking on a table:

```
ALTER TABLE <database>.<schema>.<table> SET CHANGE_TRACKING = TRUE;
```

> Change tracking is required for both the initial import and incremental syncs. It allows the connector to create Snowflake Streams on your tables, which track row-level changes (inserts, updates, deletes) between syncs.

## Limitations

* **Only base tables are supported.** Views, external tables, materialized views, and other object types cannot be synced.
* **Tables must have a primary key.** The connector requires a defined primary key to uniquely identify rows. Tables without primary keys will be skipped with an error.
* **Change tracking must be pre-enabled.** Change tracking must be turned on for each table before initiating a sync. See [Enabling change tracking](https://docs.snowflake.com/en/sql-reference/constructs/changes).
* **The user must have permissions to create and modify streams.** The connector creates Snowflake Streams on tables for incremental sync. If the user lacks `MODIFY` or `OWNERSHIP` privileges on the table, stream creation will fail and incremental sync will not be available (full extraction will be used on every sync).
* **System databases are excluded.** The following databases are automatically skipped during sync unit discovery: `SNOWFLAKE`, `SNOWFLAKE_SAMPLE_DATA`, `SNOWFLAKE_LEARNING_DB`.
* **The** `INFORMATION_SCHEMA` **schema is excluded** from each database.
* **File deletion in Snowflake (row deletion) is tracked only when using incremental sync.** If a stream goes stale or is missing, the connector falls back to a full extraction which does not capture deletes.
* **Only key-pair authentication is supported.** OAuth and username/password authentication are not available.
* **Deleting records in DevRev is not supported.** When a record is deleted in Snowflake, it is not removed from DevRev. Instead, the **Snowflake Record Status** field is marked as `DELETED`. Refer to this field to identify records that have been deleted in the external system.
* **Incremental sync depends on streams for CDC (change data capture).** DDL operations (such as adding or dropping columns) are not reflected until a DML operation (insert, update, or delete) is performed on the table's rows.
* **Time scope filters are not supported.** You cannot restrict syncs to a specific time range; each sync processes all available data (or all changes since the last sync when using incremental mode).

## How it works

At a high level, each sync cycle consists of two phases:

1. **Extraction** — The connector queries your Snowflake tables, stages the results, and downloads the data. This is the only phase that consumes your Snowflake virtual warehouse credits and may incur data egress fees. Temporary internal stages created during extraction are automatically dropped once extraction completes, so they do not persist in your account.
2. **Transformation and Loading** — The extracted data is transformed and loaded into DevRev. Both transformation and loading run entirely within DevRev, so your Snowflake warehouse compute is not used during this phase.

Because warehouse compute is limited to the extraction phase, the window of active Snowflake resource consumption is typically much shorter than the overall sync duration.

### Managing Snowflake costs

We recommend setting up a [resource monitor](https://docs.snowflake.com/en/user-guide/resource-monitors) on the warehouse used for Snowflake AirSync. A good starting point is to align the monitor's credit quota with your periodic sync interval (for example, if you sync every hour, set a quota that covers the expected hourly extraction cost). As a preventive measure, consider also adding a **daily** credit quota to guard against unexpected spikes across multiple sync runs.

### 

> **Disclaimer**  
> **Data Egress and Compute Charges:** Use of the Snowflake connector may incur additional charges beyond your standard platform subscription. These costs include, but are not limited to:
>
> * **Data Egress fees** — for transferring data out of your Snowflake region or cloud provider.
> * **Virtual Warehouse credits** — for compute resources utilized during data extraction (queries, `COPY INTO` operations, stage file downloads, etc.). Warehouse compute is consumed only during the extraction phase of each sync.
>
> Please review your Snowflake account's pricing and usage policies before enabling this connector. DevRev is not responsible for any Snowflake charges incurred through the use of this integration.

## Post import options

After a successful import, you have the following options available for the imported data:

* **Sync to DevRev** This option allows you to synchronize any modifications made in Snowflake with the corresponding items previously imported into DevRev. It also creates new items in DevRev for any rows added in Snowflake after the last sync or import.
* **View Report** This option allows you to access detailed information about the initial import and any subsequent syncs performed.
* **Delete Import** If you want to remove the import and all data that were imported from Snowflake into DevRev, you can use this option.
* **Edit Connection** Use this option to change the connection used for any subsequent actions. It can be helpful if a connection becomes inactive or the user who established it is no longer available.

### Sync to DevRev

After a successful import from Snowflake, you can choose to sync the imported data with DevRev. This feature imports any new rows and changes made to previously imported items from Snowflake.

To perform a one-time sync to DevRev, follow these steps:

1. Go to **Settings > Integrations > Airsync**.
2. Locate the previously imported project.
3. Select the **⋮** > **Sync Snowflake to DevRev** option.

> A one-time sync may overwrite fields in previously imported items, even if they were modified in DevRev.

### Historical imports

To view currently running and previous imports from various sources, do the following:

1. Go to **Settings > Integrations > Airsync**.
2. Select the import you want to view.
3. Click on the context menu (⋮) and select **View Report**.

### Periodic sync

After successfully importing to DevRev, you have the option to enable a periodic sync. This allows for automatic synchronization with DevRev on a regular basis. By default, the sync occurs once an hour.

To configure periodic sync, follow these steps:

1. Go to **Settings > Integrations > Airsync**.
2. Locate the previously imported project.
3. Select the **⋮** > **Set Periodic Sync** option.

The Enable automation for synced items setting is optional and can be activated during periodic sync configuration. When enabled, newly created or updated items trigger events, which can initiate webhooks, notifications, snap-ins, and other processes, as if the events originated directly in DevRev.

If this setting is turned off, updates do not trigger any event-driven processes. This behavior applies only to periodic syncs; no events are triggered during a first-time import or manual sync to or from DevRev.

### Delete import

> This deletes any content created by the import, including custom objects and their associated data.

An import and all the content it creates can be deleted from DevRev. This can be useful when running POCs or to change the configuration used during the import. Once an import has been deleted, all the content it created gets deleted, even if they were modified in DevRev. It's possible to import the project again after its deletion.

To delete an import and all the content it created, go to **Settings > Integrations > Airsync**, find the previously imported project, and select **⋮** > **Delete Import**.

## Related wiki nodes
- [[glossary/airsync]]

## Source
- DevRev support article [Snowflake AirSync](https://support.devrev.ai/en-US/devrev/article/8AJRfbiU) (ART-25907)
