---
title: Okta AirSync Connector
devrev_id: ART-27918
parent_directory: AirSync
translation_group: mKHCupBE
modified_date: "2026-04-07T04:59:25.631Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/mKHCupBE"
tags: []
top_category: Computer by DevRev
wiki_match: glossary/airsync
match_score: 0.85
last_updated: 2026-05-11
related: ['glossary/airsync']
---

# Okta AirSync Connector

# Okta AirSync Connector

The Okta AirSync connector syncs identity and access management (IAM) data from your Okta organization into DevRev. This connector helps you centralize your identity data, track user access patterns, and maintain visibility into your organization's security posture.

## Overview

The Okta connector imports users, groups, applications, access policies, devices, and audit logs from Okta into DevRev. It supports both initial full synchronization and incremental updates, ensuring your DevRev data stays current with minimal API overhead.

### What This Connector Does

* **Imports identity data** from Okta into DevRev as external records
* **Syncs user profiles** including standard and custom attributes
* **Tracks group memberships** and administrative role assignments
* **Monitors application access** including user and group assignments
* **Captures security policies** for sign-on, MFA, and password requirements
* **Imports audit logs** for compliance and security monitoring
* **Discovers managed devices** and their enrollment status
* **Supports incremental sync** to minimize API calls and stay within rate limits

## Entities Synced

The connector extracts the following entity types from Okta:

### Core Identity Entities

| Entity | Description | Incremental Sync |
| --- | --- | --- |
| **Users** | User profiles with standard and custom attributes | ✓ Yes |
| **Groups** | Security groups and distribution lists | ✓ Yes |
| **Group Members** | User-to-group membership relationships | Full sync only |

### Access Management Entities

| Entity | Description | Incremental Sync |
| --- | --- | --- |
| **IAM Roles** | Administrative roles (Super Admin, Org Admin, etc.) | Full sync only |
| **IAM Role Members** | User-to-role assignments | Full sync only |
| **Applications** | SAML, OIDC, SWA, and other integrated applications | Full sync only |
| **App User Assignments** | Direct user-to-application access grants | Full sync only |
| **App Group Assignments** | Group-based application access grants | Full sync only |

**IAM Roles Extraction**: The connector extracts IAM roles from two sources: custom IAM Governance roles via `/api/v1/iam/roles` (requires IAM Governance license) and assigned administrator roles from user assignments via `/api/v1/users/{userId}/roles`. Only roles that are actually assigned to users are extracted from the user assignments endpoint.

**IAM Role Descriptions**: Okta's Management API does not provide descriptions for standard built-in administrator roles (e.g., Super Admin, Org Admin, App Admin). The API response for these roles returns a null description field. To provide meaningful information in DevRev, the connector generates descriptive fallback text for roles without descriptions (e.g., "SUPER\_ADMIN IAM role: Super Administrator with administrative access"). Only custom IAM roles created through IAM Governance may include actual descriptions from Okta. Similarly, group descriptions are provided by Okta API when available, but if missing, a fallback description is generated.

### Security Entities

| Entity | Description | Incremental Sync |
| --- | --- | --- |
| **Policies** | Security policies (sign-on, MFA, password, OAuth) | Full sync only |
| **System Logs** | Audit log events for compliance and monitoring | ✓ Yes (time-windowed) |
| **Devices** | Managed devices enrolled in Okta | ✓ Yes |
| **Factors** | Multi-factor authentication methods per user | Full sync only |

### Metadata

| Entity | Description | Usage |
| --- | --- | --- |
| **Custom Field Schema** | Dynamically discovered custom user attributes | Metadata extraction |
| **Organization Profile** | Okta org details and contact information | Sync unit discovery |

### Incremental Sync Details

The connector performs incremental syncs for the following entities using Okta's `lastUpdated` filters:

* **Users**: Fetches only users modified since the last sync
* **Groups**: Fetches groups where the group profile or membership changed
* **Devices**: Fetches devices with updated attributes
* **System Logs**: Fetches audit events within a specific time window

For entities without incremental support, the connector performs a full sync each time but only updates records that changed.

### Shadow User Filtering

Users with `status = "shadow"` are automatically excluded. Shadow users are incomplete placeholder accounts created during automated provisioning and do not represent real users.

## Prerequisites

Before installing the connector, ensure you have:

1. **Okta Administrator Access**: You need permissions to create API tokens
2. **DevRev Account**: An active DevRev organization with AirSync enabled
3. **DevRev Admin Role Permissions**:

   * Grant **full privileges** for all **custom objects** in DevRev, including subtypes
   * Navigate to **Settings → Roles & Permissions → Admin Role**
   * Enable **read, write, and manage permissions** for all custom object types that will store Okta data
   * This ensures the connector can create and update records for users, groups, applications, and other entities
4. **API Token Permissions**: The Okta token must have read access to:

   * Users
   * Groups
   * Applications
   * Roles
   * Policies
   * System logs
   * Devices
   * Factors (optional, for MFA data)

## Installation

### Step 1: Configure DevRev Permissions

Before connecting to Okta, ensure your DevRev admin role has the necessary permissions:

1. Log in to your **DevRev account** as an administrator
2. Navigate to **Settings → Roles & Permissions**
3. Select the **Admin Role** (or the role that will manage the connector)
4. Scroll to the **Custom Objects** section
5. Enable **full privileges** (Create, Read, Update, Delete) for:

   * All custom object types
   * All subtypes within each custom object
6. This ensures the connector can properly sync and map Okta entities to DevRev records
7. Click **Save Changes**

**Important**: Without these permissions, the connector may fail to create or update records in DevRev, resulting in sync errors or incomplete data.

---

### Step 2: Create an Okta API Token

1. Log in to your **Okta Admin Console**
2. Navigate to **Security → API → Tokens**
3. Click **Create Token**
4. Enter a descriptive name (e.g., "DevRev AirSync Connector")
5. Click **Create Token**
6. **Copy the token immediately** — it is shown only once and cannot be retrieved later
7. Store the token securely (you will use it in the next step)

### Step 3: Install the Connector in DevRev

1. Log in to your **DevRev account**
2. Navigate to **Settings → Integrations**
3. Search for **Okta** in the connector marketplace
4. Click **Install** on the Okta AirSync connector
5. The connector is now added to your DevRev organization

### Step 4: Configure a Connection

1. After installation, click **Configure** on the Okta connector
2. Click **Add Connection** to create a new Okta connection
3. Provide the following information:

   * **Connection Name**: A friendly name for this connection (e.g., "Okta Production")
   * **Okta Subdomain**: Your Okta organization subdomain (e.g., if your Okta URL is `https://mycompany.okta.com`, enter `mycompany`)
   * **API Token**: Paste the API token you created in Step 1
4. Click **Test Connection** to verify the credentials
5. If the test succeeds, click **Save**

### Step 5: Configure Sync Settings

1. After saving the connection, configure the sync behavior:

   * **System Log Start Date**: (Optional) Enter the date from which to start importing audit logs

     + Format: `YYYY-MM-DD` (e.g., `2026-02-15`)
     + Default: 30 days ago
     + Tip: Use a recent date for the initial sync to avoid importing large volumes of historical logs
2. Click **Save Configuration**

## Running a Sync

### Initial Sync

The first sync performs a full import of all entities:

1. Navigate to the Okta connector configuration
2. Click **Run Sync**
3. The connector fetches all users, groups, applications, policies, devices, and logs
4. Depending on your Okta organization size, the initial sync can take several minutes to several hours
5. You can monitor progress in the **Sync History** tab

**Note**: The initial sync imports all audit logs starting from the configured **System Log Start Date** (default: 30 days ago). Adjust this date if you need a longer or shorter log history.

### Incremental Sync

After the initial sync, subsequent syncs fetch only changes:

1. Schedule automatic syncs or trigger them manually
2. The connector uses the last successful sync timestamp to fetch incremental updates
3. Incremental syncs are significantly faster and use fewer API calls

### Sync Frequency Recommendations

* **Hourly**: For organizations requiring near-real-time identity data
* **Daily**: For most organizations (recommended)
* **Weekly**: For small organizations with infrequent changes

Consider your Okta API rate limits when setting sync frequency. The connector automatically handles rate limiting by pausing and retrying when limits are reached.

## Configuration Options

### System Log Start Date

This setting controls the starting point for audit log imports. It is only used during the initial sync.

* **Format**: `YYYY-MM-DD`
* **Default**: 30 days ago
* **Recommendations**:

  + Use a recent date (1-7 days) for initial testing to reduce sync time
  + Use 30-90 days for production to capture a meaningful audit trail
  + Avoid setting dates older than 90 days to prevent long sync times

After the initial sync, the connector automatically tracks log events incrementally using time-windowed queries.

## Authentication

The connector uses **SSWS API tokens** for authentication. The token format is:

```
SSWS <token_value>
```

The connector automatically adds the `SSWS` prefix — you only need to provide the token value from the Okta Admin Console.

### Token Security

* API tokens are stored securely in DevRev's keyring service
* Tokens are encrypted at rest and in transit
* Token values are never logged or displayed in the UI after initial configuration
* Rotate tokens periodically following your organization's security policies

### Token Verification

When you save a connection, DevRev verifies the token by calling:

```
GET https://{subdomain}.okta.com/api/v1/users/me
```

If this call succeeds, the token is valid and has sufficient permissions.

## Error Handling and Resilience

The connector is designed to handle transient errors gracefully:

### Rate Limiting (HTTP 429)

When Okta rate limits are reached:

1. The connector reads the `X-Rate-Limit-Reset` header to determine the wait time
2. The sync pauses automatically and resumes after the rate limit resets
3. No data is lost or skipped during the pause

**Tip**: If you encounter frequent rate limiting, reduce your sync frequency or contact Okta to review your rate limit tier.

### Permission Errors (HTTP 403/405)

If the API token lacks permissions for a specific entity:

1. The connector skips that entity type with a warning
2. Other entity types continue to sync normally
3. The sync completes with a summary of skipped entities

**Solution**: Ensure your API token has read permissions for all required scopes.

### Server Errors (HTTP 500/502/503/504)

Transient server errors are retried automatically:

* **Attempt 1**: Immediate retry after 1 second
* **Attempt 2**: Retry after 2 seconds
* **Attempt 3**: Error is logged and reported

### Incremental Sync Fallback

If an incremental sync filter fails (HTTP 400):

1. The connector automatically falls back to a full sync for that entity
2. This ensures no data is missed due to unsupported filter syntax
3. Future syncs continue to attempt incremental mode

## Best Practices

### Initial Setup

1. **Start with a recent log date**: Set the System Log Start Date to 7-14 days ago for your first sync
2. **Test the connection**: Always use the Test Connection feature before saving
3. **Monitor the first sync**: Watch the initial sync closely to identify any permission issues
4. **Review skipped entities**: Check the sync logs for any entities that were skipped due to permissions

### Ongoing Operations

1. **Schedule regular syncs**: Set up hourly or daily syncs based on your needs
2. **Monitor rate limits**: Review sync logs for rate limit warnings and adjust frequency if needed
3. **Rotate API tokens**: Replace API tokens every 90-180 days following security best practices
4. **Review sync history**: Periodically check the Sync History tab for errors or warnings

### Performance Optimization

1. **Use incremental sync**: Always allow the connector to complete the initial sync before scheduling frequent syncs
2. **Limit log history**: Avoid setting System Log Start Date too far in the past (30-90 days is ideal)
3. **Respect rate limits**: Space out syncs to stay within Okta's API rate limits
4. **Monitor sync duration**: If syncs take too long, consider reducing the number of entities synced

### Security

1. **Limit token permissions**: Grant only the read permissions required for the entities you want to sync
2. **Use dedicated tokens**: Create a separate API token for DevRev (do not reuse tokens across integrations)
3. **Monitor token usage**: Review Okta system logs for API token activity
4. **Revoke unused tokens**: If you disable the connector, revoke the API token in Okta

## Custom Field Support

The connector automatically discovers and syncs custom user profile attributes defined in your Okta user schema.

### How It Works

1. During metadata extraction, the connector fetches your Okta user schema
2. Custom attributes are identified in the `definitions.custom.properties` section
3. Each custom field is added to the DevRev schema dynamically
4. Custom fields are synced alongside standard user attributes

### Supported Custom Field Types

| Okta Type | DevRev Type | Description |
| --- | --- | --- |
| `string` | `text` | Text fields and strings |
| `number` | `float` | Floating-point numbers |
| `integer` | `int` | Whole numbers |
| `boolean` | `bool` | True/false values |
| `array` | `text` | Arrays (serialized as JSON strings) |

**Note**: Custom fields are read-only. The connector does not write data back to Okta.

## Troubleshooting

### Connection Test Fails

**Error: HTTP 401 Unauthorized**

* **Cause**: The API token is invalid or expired
* **Solution**: Generate a new API token in the Okta Admin Console and update the connection

**Error: HTTP 404 Not Found**

* **Cause**: The Okta subdomain is incorrect
* **Solution**: Verify your subdomain (e.g., `mycompany` for `mycompany.okta.com`) and update the connection

### Sync Fails or Is Incomplete

**Symptom: Rate limit errors (HTTP 429)**

* **Cause**: Sync frequency exceeds your Okta API rate limits
* **Solution**: Reduce sync frequency or contact Okta to review your rate limit tier

**Symptom: Entities are skipped**

* **Cause**: API token lacks required permissions
* **Solution**: Ensure the token has read access to: users, groups, apps, roles, policies, logs, factors, and devices

**Symptom: Users are missing after sync**

* **Cause**: Users with `status = "shadow"` are filtered out automatically
* **Solution**: Confirm the user has an active status in Okta (not "shadow")

### Sync Takes Too Long

**Solution 1**: Reduce the System Log Start Date to a more recent date (e.g., 7 days ago)

**Solution 2**: Verify that incremental sync is working (check that "Incremental" appears in the sync logs)

**Solution 3**: Increase the sync interval to allow each sync to complete before the next one starts

### Custom Fields Not Appearing

**Symptom**: Custom user attributes are not synced

**Solution**:

1. Verify that custom attributes are defined in your Okta user schema (Admin Console → Directory → Profile Editor → User)
2. Ensure the API token has read access to user schema metadata
3. Check that the field names do not conflict with system fields (`id`, `created_date`, `modified_date`)
4. Re-run metadata extraction by triggering a new sync

## API Rate Limits

Okta enforces API rate limits based on your organization tier:

| Okta Tier | Rate Limit | Notes |
| --- | --- | --- |
| **Developer** | 1,000 requests/min | Suitable for testing only |
| **Production** | 3,000-10,000 requests/min | Varies by license tier |
| **Enterprise** | 10,000+ requests/min | Contact Okta for custom limits |

The connector uses pagination and incremental sync to minimize API calls. Monitor the `X-Rate-Limit-Remaining` header in Okta system logs to track your usage.

## Data Privacy and Compliance

### Data Stored

The connector imports the following data into DevRev:

* User profile attributes (first name, last name, email, etc.)
* Group names and descriptions
* Application names and settings (no application secrets)
* Policy configurations (no sensitive credentials)
* Audit log events (user actions, login events, etc.)
* Device metadata (device type, status, enrollment date)

### Data NOT Stored

The connector does NOT import:

* User passwords or password hashes
* MFA secrets or recovery codes
* API tokens or client secrets
* Social Security Numbers or other PII not in standard Okta fields

### Compliance Considerations

* **GDPR**: Ensure your data processing agreements cover DevRev as a data processor
* **HIPAA**: Okta audit logs may contain PHI — review your BAA requirements
* **SOC 2**: DevRev maintains SOC 2 Type II compliance for data handling

## Support

For issues with the Okta AirSync connector:

1. **Check sync logs**: Review the Sync History tab for error messages and warnings
2. **Review documentation**: Consult this guide and the troubleshooting section
3. **Contact DevRev Support**: Open a support ticket in DevRev with:

   * Connection name
   * Sync timestamp
   * Error messages from sync logs
   * Steps you have already tried

For issues with Okta API tokens or permissions, contact Okta Support.

## Limitations

* **One-way sync**: Data flows from Okta to DevRev only (no write-back)
* **Read-only custom fields**: Custom user attributes are synced but cannot be modified from DevRev
* **Policy rules**: Policy rules and mappings are included but may not render in the DevRev UI
* **Attachment support**: Not applicable (Okta IAM entities do not support attachments)
* **Real-time sync**: The connector uses polling-based sync (no webhooks)

## Changelog

### Version 1.0.0 (Initial Release)

* Full sync support for all major Okta entities
* Incremental sync for users, groups, devices, and system logs
* Custom user field discovery and mapping
* Automatic rate limit handling with pause/resume
* Permission-denied graceful skip for restricted entities
* Retry logic for transient server errors
* Timeout-resumable extraction with cursor-based pagination

---

**Last Updated**: April 2026  
**Connector Version**: 1.0.0  
**Supported Okta API Version**: v1

## Related wiki nodes
- [[glossary/airsync]]

## Source
- DevRev support article [Okta AirSync Connector](https://support.devrev.ai/en-US/devrev/article/mKHCupBE) (ART-27918)
