---
title: Microsoft Intune AirSync connector
devrev_id: ART-32873
parent_directory: AirSync
translation_group: sWtjszWM
modified_date: "2026-04-27T05:58:48.95Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/sWtjszWM"
tags: []
top_category: Computer by DevRev
wiki_match: glossary/airsync
match_score: 0.85
last_updated: 2026-05-11
related: ['glossary/airsync']
summary: "The Microsoft Intune AirSync connector imports your Intune endpoint management data into DevRev."
---

# Microsoft Intune AirSync connector

The Microsoft Intune [[glossary/airsync|AirSync]] connector imports your Intune endpoint management data into DevRev. It syncs managed devices, compliance policies, device configurations, and enrollment configurations so your team has full hardware lifecycle visibility — directly inside DevRev.

Use this connector to:

* View device inventory, compliance status, and encryption state alongside support [[features/tickets|tickets]]
* Look up which policies and configurations apply to a device or [[entities/group|group]]
* Track device provisioning, reassignment, and decommissioning [[features/workflows|workflows]]
* Answer fleet-wide questions like "How many devices are noncompliant?" without switching to the Intune portal

## What gets synced

The connector imports four entity types from Microsoft Intune and maps them to DevRev **Configuration Item** objects.

### Managed Devices

Every device enrolled in your Intune tenant is synced as a Configuration Item with CI class `hardware`. This includes laptops, desktops, phones, and tablets across Windows, macOS, iOS, and Android.

**Fields synced for each device:**

| Intune field | DevRev field | Description |
| --- | --- | --- |
| Device Name | Title / Name | The name of the device as it appears in Intune |
| Serial Number | Serial Number | Hardware serial number assigned by the manufacturer |
| Model | Model | Device model (e.g., ThinkPad X1 Carbon, iPhone 15 Pro) |
| Manufacturer | Manufacturer | Hardware manufacturer (e.g., Lenovo, Apple, Samsung) |
| User Principal Name | Assigned To | The email address of the user the device is assigned to |
| Compliance State | Compliance State | Whether the device meets policy requirements: Compliant, Noncompliant, In Grace Period, Error, Conflict, Unknown, or Not Evaluated |
| Is Encrypted | Encryption Status | Whether device storage encryption (BitLocker, FileVault) is active: Encrypted, Not Encrypted, or Unknown |
| Managed Device Owner Type | Ownership Type | Whether the device is Company-owned or Personal (BYOD) |
| Last Sync Date Time | Last Check In | When the device last contacted Intune |
| Operating System | CI Subclass | The OS determines the device subclass: `windows_device`, `ios_device`, `android_device`, or `macos_device` |

Additional device properties — such as OS version, storage capacity, MAC addresses, jailbreak status, Azure AD device ID, enrollment profile, and threat state — are stored in the **Class Attributes** field as structured data.

### Compliance Policies

Compliance policies define the rules a device must meet (e.g., require encryption, minimum OS version, password complexity). Each policy is synced as a Configuration Item with CI class `service` and subclass `compliance_policy`.

**Fields synced for each policy:**

| Intune field | DevRev field | Description |
| --- | --- | --- |
| Display Name | Title / Name | The name of the compliance policy |
| Description | Notes | Administrator description of the policy |
| Assigned [[entities/group|Groups]] | Assigned Group IDs | Which Azure AD groups this policy targets |
| Policy Rules | Class Attributes | Platform-specific compliance rules (e.g., password required, encryption required) |
| Scheduled Actions | Class Attributes | Automated responses when a device becomes noncompliant (e.g., block access after 72 hours) |

### Device Configurations

Device configuration profiles define settings pushed to devices (e.g., Wi-Fi profiles, VPN settings, email configurations). Each profile is synced as a Configuration Item with CI class `logical` and subclass `configuration_profile`.

**Fields synced for each configuration:**

| Intune field | DevRev field | Description |
| --- | --- | --- |
| Display Name | Title / Name | The name of the configuration profile |
| Description | Notes | Administrator description of the configuration |
| Assigned Groups | Assigned Group IDs | Which Azure AD groups receive this configuration |
| Configuration Settings | Class Attributes | Platform-specific settings (e.g., SSID, proxy, certificate) |

### Enrollment Configurations

Enrollment configurations control how devices enroll into Intune. This includes device limits per user, platform restrictions (e.g., block personal Android), and Windows Hello for Business settings. Each is synced as a Configuration Item with CI class `logical`.

The subclass is automatically determined:

* **enrollment\_limit** — for device count limit configurations
* **enrollment\_restriction** — for platform restriction configurations
* **enrollment\_configuration** — for all other enrollment types

**Fields synced for each enrollment configuration:**

| Intune field | DevRev field | Description |
| --- | --- | --- |
| Display Name | Title / Name | The name of the enrollment configuration |
| Description | Notes | Administrator description |
| Priority | Class Attributes | Evaluation priority when multiple configurations apply |
| Assigned Groups | Assigned Group IDs | Which Azure AD groups this configuration targets |
| Settings | Class Attributes | Enrollment-specific rules (e.g., device limit count, allowed platforms) |

## Prerequisites

Before you install the connector, make sure the following requirements are met.

### In Microsoft Azure

1. **An Azure AD application registration** with the following Microsoft Graph **application permissions** (not delegated permissions):

   * `DeviceManagementManagedDevices.ReadWrite.All` — Read device properties and execute remote actions
   * `DeviceManagementConfiguration.Read.All` — Read compliance policies and device configurations
   * `DeviceManagementServiceConfig.Read.All` — Read enrollment configurations and device categories
   * `User.Read.All` — Resolve device-to-user associations
2. **Admin consent granted** for the above permissions. A Global Administrator or Intune Administrator must grant consent in the Azure portal.
3. **A client secret** generated for the application registration. Note down the **Client ID**, **Client Secret**, and **Tenant ID** — you need these during setup.

> To create the application registration, go to **Azure Portal > Azure Active Directory > App registrations > New registration**. After creating the app, go to **API permissions > Add a permission > Microsoft Graph > Application permissions** and add the four permissions listed above. Then select **Grant admin consent**.

### In DevRev

1. A DevRev organization with admin access.
2. The AirSync feature enabled for your organization. Contact DevRev support if you do not see the AirSync option.

## Installation

1. Go to your DevRev organization settings.
2. Navigate to **Marketplace** or **Snap-ins**.
3. [[features/search|Search]] for **Intune Sync** and select it.
4. Click **Install**.

## Configuration

After installation, you need to connect the snap-in to your Intune tenant.

### Step 1: Set up the OAuth connection

1. Go to **Settings > Snap-ins > Intune Sync**.
2. Under **Connections**, click **Add Connection**.
3. Enter the **Client ID** and **Client Secret** from your Azure AD application registration.
4. The connector authenticates with Microsoft using OAuth2 client credentials and verifies access by querying your organization info from the Microsoft Graph API.
5. Once the connection shows as **Connected**, proceed to the next step.

### Step 2: Configure organization settings

Under the **Organization Inputs** section, you can configure the following option:

| Setting | Default | Description |
| --- | --- | --- |
| Enable Extended Device Fields | Off | When turned on, the connector makes an additional API call per device to fetch extra fields such as notes, physical memory, and MAC addresses. Leave this off for large fleets (10,000+ devices) to avoid longer sync times. |

### Step 3: Select the sync unit

1. Navigate to **AirSyncs** in the DevRev sidebar.
2. Click **Start AirSync** and select **Intune Sync**.
3. The connector discovers your Intune tenant as a single sync unit. Select it and click **Next**.

## Running a sync

### Initial sync

The first sync performs a full import of all four entity types from your Intune tenant. Depending on the size of your fleet, this can take anywhere from a few minutes to several hours for very large tenants (50,000+ devices).

The sync proceeds through four phases in order:

1. **Sync unit discovery** — The connector identifies your Intune tenant.
2. **Metadata** — The connector pushes the data schema to DevRev.
3. **Data extraction** — The connector extracts all managed devices, compliance policies, device configurations, and enrollment configurations. Policies and configurations include their group assignments.
4. **Attachments** — This phase completes immediately because Intune entities do not have file attachments.

The data extraction phase processes entities in this order:

1. Compliance Policies
2. Device Configurations
3. Enrollment Configurations
4. Managed Devices

> For large tenants, the data extraction phase may span multiple execution cycles. The connector automatically saves its progress after each page of results. If an execution cycle reaches its time limit, the connector picks up exactly where it left off on the next cycle. No data is lost or duplicated.

### Incremental sync

After the initial sync completes, subsequent syncs only import records that changed since the last successful sync. This makes incremental syncs significantly faster than the initial import.

* For policies and configurations, the connector filters on `lastModifiedDateTime` to detect changes.
* For managed devices, the connector filters on `lastSyncDateTime` (last device check-in time) because this is the most reliable change indicator.

### Sync frequency

You can run syncs manually from the AirSyncs page, or configure a recurring sync schedule in the AirSync settings. A daily or twice-daily schedule is recommended for most organizations to keep device compliance status current.

## How data maps to DevRev

All four Intune entity types map to DevRev **Configuration Item** objects. The table below summarizes the mapping:

| Intune entity | DevRev object type | CI class | CI subclass | Sync direction |
| --- | --- | --- | --- | --- |
| Managed Devices | Configuration Item | hardware | windows\_device, ios\_device, android\_device, macos\_device | Import to DevRev |
| Compliance Policies | Configuration Item | service | compliance\_policy | Import to DevRev |
| Device Configurations | Configuration Item | logical | configuration\_profile | Import to DevRev |
| Enrollment Configurations | Configuration Item | logical | enrollment\_limit, enrollment\_restriction, enrollment\_configuration | Import to DevRev |

## Best practices

### Keep your fleet data fresh

Run incremental syncs at least once daily. Compliance state and device check-in times change frequently, and stale data can lead to incorrect triage decisions.

### Start with Extended Device Fields turned off

For your initial sync, leave the **Enable Extended Device Fields** option turned off. This avoids extra per-device API calls and lets the first sync complete faster. Once the initial sync is done, you can turn it on if you need the additional fields (notes, physical memory, MAC addresses) and run another sync to backfill.

### Use compliance state for triage

The **Compliance State** field on device Configuration Items is one of the most valuable fields for support workflows. Use it to quickly assess whether a device meets your organization's security requirements when triaging hardware tickets.

### Use assigned group IDs to trace policy scope

Each compliance policy and configuration profile includes the Azure AD group IDs it targets. Use this to answer questions like "Which policies apply to the Engineering team?" or "Is this user's group covered by the encryption requirement policy?"

### Monitor incremental sync results

After each sync, review the AirSync run summary in DevRev. It shows how many records were created, updated, or errored. A sudden spike in errors may indicate a permissions change or API [[entities/issue|issue]] on the Intune side.

## Troubleshooting

### The connection fails during setup

* Verify that the **Client ID** and **Client Secret** are correct and have not expired.
* Confirm that **admin consent** has been granted for all four Microsoft Graph permissions in the Azure portal.
* Make sure the Azure AD application registration is in the same tenant as your Intune subscription.

### The sync completes but no devices appear

* Check that your Intune tenant actually has enrolled devices. An empty tenant produces a successful sync with zero records.
* Verify that the service principal has the `DeviceManagementManagedDevices.ReadWrite.All` permission. Without it, the device list API returns an empty response or a 403 error.

### Compliance policies or configurations are missing

* The `DeviceManagementConfiguration.Read.All` permission is required to read compliance policies and device configurations.
* The `DeviceManagementServiceConfig.Read.All` permission is required to read enrollment configurations.
* If these permissions were added after the initial consent, you must re-grant admin consent in the Azure portal.

### The sync takes a very long time

* For tenants with 50,000+ devices, the initial sync can take several hours. This is expected. Subsequent incremental syncs are much faster.
* If **Enable Extended Device Fields** is turned on, the connector makes one extra API call per device. For very large fleets, this significantly increases sync duration. Consider turning it off.

### Incremental sync is not picking up changes

* Incremental sync uses the timestamp from the last successful sync. If a previous sync failed, the connector falls back to a full extraction on the next run.
* For devices, changes are detected based on `lastSyncDateTime` (last check-in), not `lastModifiedDateTime`. A device whose properties change but does not check in will not appear in the incremental sync until it checks in again.

## Limitations

* **File attachments:** Intune entities do not have file attachments. The attachments phase of the sync always completes immediately with no data.
* **Reverse sync (device actions):** The ability to execute remote device actions (retire, wipe, lock) from DevRev is planned but not yet available. Currently, the connector only imports data from Intune into DevRev.
* **Custom fields:** Intune does not support user-defined custom fields on its API resources. The connector syncs all available standard fields. Extended device properties are available in the Class Attributes field.
* **Real-time sync:** The connector uses scheduled or manual sync runs, not real-time webhooks. There is a delay between a change in Intune and its appearance in DevRev, depending on your sync schedule.

## Related wiki nodes
- [[glossary/airsync]]

## Source
- DevRev support [[entities/article|article]] [Microsoft Intune AirSync connector](https://support.devrev.ai/en-US/devrev/article/sWtjszWM) (ART-32873)
