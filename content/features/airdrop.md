---
title: Airdrop
type: feature
status: draft
sources: [raw/test-cases/by-feature/fe_airdrop.jsonl, raw/docs/devrev-developer-docs.md, raw/docs/devrev-agent-dump-integrations.md]
related: ["features/slack-integration", "features/github-integration", "features/jira-integration", "features/email-integration"]
last_updated: 2026-04-12
---

# Airdrop

## What it does
Airdrop is DevRev's data synchronization and integration framework. It manages bidirectional sync between DevRev and external systems (e.g., JIRA, ADaaS-based connectors) through sync units, recipes, blueprints, and field mappings. With 1637 test cases, it covers sync unit lifecycle, recipe management, artifact transfer, field mapping configuration, sync mapper records, sync modification tracking, sync packs, and precedence configuration. The feature enables organizations to keep their DevRev data in sync with external project management, issue tracking, and other tools.

## Why it exists
Organizations rarely use a single tool. DevRev's Airdrop allows teams to connect external systems like JIRA, GitHub, and custom connectors, ensuring data flows bidirectionally without manual effort. It provides granular control over what syncs (sync units), how fields map between systems, and what takes precedence when conflicts arise.

## Key behaviors
- **Sync units**: Full lifecycle management (create, create bulk, get, list, update, group, history, action); blueprint association and checking; recipe status tracking
- **Field mapping**: Get field mapping options per sync unit with support for DevRev fields filtering; record-type mapping options
- **Sync mapper records**: Create, get, get-by-external-id, get-by-target, list-by-external-id, update mapper records that track entity mappings between systems
- **Sync modification records**: Get and get-by-target; hidden internal proto fields are not exposed in API
- **Recipe management**: Blueprint shards, filters, associated filters, initial domain mappings (get and install)
- **Sync packs**: Get, list, group, update sync packs
- **Sync precedence**: Get, list, update precedence configs; get sync precedence information per unit
- **Artifacts**: Upload URL generation, download URL generation, confirm upload for sync artifacts
- **External systems**: List external sync units, get capabilities, discover external sync units
- **External worker**: Get external worker status
- **External extractor**: Send messages to external extractors
- **Bulk metadata**: Get metadata for multiple sync units with graceful per-item degradation (valid IDs get full metadata, invalid IDs get id-only entries)
- **Metadata summary**: Get summarized metadata for sync units
- **Historical recipe state**: Get historical state of recipes for sync units

## Entry points
- **Base URL**: `https://api.devrev.ai/internal/`
- All endpoints under `airdrop.*` namespace
- Requires `Authorization: Bearer $TOKEN`
- Supports both GET (query params) and POST (JSON body) for most endpoints

## API endpoints

| Endpoint | Methods | Description |
|----------|---------|-------------|
| `airdrop.sync-units.create` | POST | Create sync unit |
| `airdrop.sync-units.create.bulk` | POST | Bulk create sync units |
| `airdrop.sync-units.get` | GET, POST | Get sync unit |
| `airdrop.sync-units.list` | GET, POST | List sync units |
| `airdrop.sync-units.update` | POST | Update sync unit |
| `airdrop.sync-units.group` | POST | Group sync units |
| `airdrop.sync-units.history` | GET, POST | Sync unit history |
| `airdrop.sync-units.action` | POST | Trigger sync action |
| `airdrop.sync-units.blueprint.associate` | POST | Associate blueprint |
| `airdrop.sync-units.blueprint.check` | GET, POST | Check blueprint |
| `airdrop.sync-units.field-mapping-options.get` | GET, POST | Get field mapping options |
| `airdrop.sync-units.record-type-mapping-options.get` | GET | Get record type mapping |
| `airdrop.sync-units.recipe-status.get` | GET | Get recipe status |
| `airdrop.sync-units.recipe-status.update` | POST | Update recipe status |
| `airdrop.sync-units.metadata.bulk` | GET, POST | Bulk metadata lookup |
| `airdrop.sync-units.metadata-summary.get` | GET, POST | Get metadata summary |
| `airdrop.sync-units.historical-recipe-state.get` | GET | Historical recipe state |
| `airdrop.sync-units.sync-precedence-information.get` | GET, POST | Sync precedence info |
| `airdrop.sync-mapper-record.create` | POST | Create mapper record |
| `airdrop.sync-mapper-record.get` | GET, POST | Get mapper record |
| `airdrop.sync-mapper-record.get-by-external-id` | GET, POST | Get by external ID |
| `airdrop.sync-mapper-record.get-by-target` | GET, POST | Get by target |
| `airdrop.sync-mapper-record.list-by-external-id` | GET | List by external ID |
| `airdrop.sync-mapper-record.update` | POST | Update mapper record |
| `airdrop.sync-modification-record.get` | GET, POST | Get modification record |
| `airdrop.sync-modification-record.get-by-target` | GET, POST | Get by target |
| `airdrop.sync-packs.get` | GET | Get sync pack |
| `airdrop.sync-packs.list` | GET, POST | List sync packs |
| `airdrop.sync-packs.group` | GET, POST | Group sync packs |
| `airdrop.sync-packs.update` | POST | Update sync pack |
| `airdrop.sync-precedence-config.get` | GET, POST | Get precedence config |
| `airdrop.sync-precedence-config.list` | GET, POST | List precedence configs |
| `airdrop.sync-precedence-config.update` | POST | Update precedence config |
| `airdrop.recipe.blueprints.get` | GET | Get recipe blueprints |
| `airdrop.recipe.blueprint-shards.get` | GET | Get blueprint shards |
| `airdrop.recipe.filters.get` | GET | Get recipe filters |
| `airdrop.recipe.filter-options.get` | GET | Get filter options |
| `airdrop.recipe.associated-filters.get` | GET | Get associated filters |
| `airdrop.recipe.associated-filters.all-current-get` | GET | Get all current filters |
| `airdrop.recipe.initial-domain-mappings.get` | GET, POST | Get initial mappings |
| `airdrop.recipe.initial-domain-mappings.install` | POST | Install initial mappings |
| `airdrop.artifacts.upload-url` | GET, POST | Get upload URL |
| `airdrop.artifacts.download-url` | GET, POST | Get download URL |
| `airdrop.artifacts.confirm-upload` | POST | Confirm artifact upload |
| `airdrop.capabilities.get` | GET, POST | Get capabilities |
| `airdrop.external-sync-units.list` | GET | List external sync units |
| `airdrop.external-sync-units.discover` | POST | Discover external units |
| `airdrop.external-worker.get` | GET | Get external worker |
| `airdrop.external-extractor.message` | POST | Message extractor |

## Recipes (deep dive)

A **recipe** is a `jq` function executed on all records of a certain type/subtype during a sync. It is the runtime derivative of a Recipe Blueprint -- the compiled set of transformation instructions that converts external records into DevRev format (and vice versa). Recipes are not directly visible to end users but can be observed by internal Airdrop users.

**Pipeline stages:**
1. An **extractor** pulls data from the external system into intermediate storage.
2. A **recipe worker** analyzes the extracted data and infers its schema.
3. The **Recipe Manager** combines the inferred schema with preset transformation hints to produce the final recipe.
4. A **transformer** applies the recipe to produce data in DevRev format.
5. The **DevRev Loader** creates DevRev records from the transformed data.

A **Recipe Blueprint** is the user-facing, manageable definition of how external types and records map to DevRev types and records. End users manage blueprints from the UI; the recipe itself is the compiled runtime version.

## Sync units (deep dive)

A **sync unit** is the atomic unit of import and syncing:

- For external systems **without** namespace isolation (e.g. Salesforce, Freshdesk, Zendesk): a sync unit corresponds to the entire external system instance.
- For external systems **with** namespace isolation (e.g. Jira, Linear): a sync unit corresponds to a namespace -- e.g. a Jira project or a Linear team.

A sync unit is the unit of configuration for:
- The connection/keyring (authentication).
- Periodic sync settings.

Each sync unit can host many **sync runs** (concrete executions). Each finished sync run becomes a record in sync history.

## Record Manager (deep dive)

The **Record Manager** (also called the Airdrop Record Manager) manages, for each synced record, two things:

1. **Object mapper** -- stores the relationship between external and internal record identifiers, plus metadata (history, transformation source).
2. **Modification records** -- stores records that were additionally transformed by the DevRev Loader due to constraints in DevRev business logic.

It also exposes an API endpoint so that sync mapper records can be looked up by their ID, by the external system identifier, or by the DON of their corresponding DevRev objects.

## Snap-in Manager

The **Snap-in Manager (SM)** manages ADaaS (Airdrop as a Service) snap-in connectors. Its responsibilities include:

- Listing available import types: after Airdrop snap-ins are installed, the Activity Manager queries the SM to compile a combined list of available internal and external extractors.
- Orchestrating the loading sequence: the SM coordinates with the Loader Adapter (LA) to copy files, start the snap-in loader, and process loading progress events.
- Each ADaaS snap-in has an associated `slug`, `display_name`, `description`, extraction function, loading function, and allowed keyring types.

## Field mapping UI

The AirSync mapping UI allows users to view and modify mappings for each sync unit:

- Each sync unit has a screen where you can view and modify mappings.
- Once changes are applied via the **Apply changes** button, newly synced data is transformed according to the new mapping on the next sync.
- **Transfer mappings** action: copy a field mapping from one record type to all other record types in the blueprint that are mapped to the same DevRev type and contain the same DevRev field.
- **Select/deselect all record types** operation is supported via the `multi-update` API.
- The Recipe Manager gives end users visibility into: all mapped fields (including stock fields), field types, enum mappings, and default/hardcoded values.
- In the DevRev -> External direction, the UI constrains enum value selections to only those external values that were mapped to the given DevRev value in the External -> DevRev direction, to prevent round-trip inconsistencies.

**Partial reimport on mapping change:** If a recipe blueprint changes (e.g. custom fields added, mapping changed), a partial reimport can be triggered. Only the affected fields are re-transformed from intermediate storage -- no re-extraction from the external system is needed.

## Filter-by-value

Filter-by-value allows you to control which records from an external system are synced into DevRev, based on a custom field value.

**Setup (Jira example):**
1. Create a custom field in Jira (e.g. an enum/select list field called "Enable Sync").
2. Associate the field with the relevant Jira issue types.
3. In DevRev: **Settings -> AirSync -> select your Jira connection -> Sync Configuration / Field Mappings**.
4. For each issue type, find the **Filter** section, click **Add Filter**, select your custom field, choose operator **Any of**, and select the value.

**Behavior:**
- **Jira -> DevRev:** Only issues where the field matches the filter are synced. Issues without the field set are **not** synced.
- **DevRev -> Jira (reverse sync):** Filters do **not** apply. All issues associated with the sync unit's subtypes are synced back to Jira regardless of field values.

## Error handling during sync

- When a mismatch exists between the data format and what the recipe is prepared to handle, the system treats it as an error (strict validation philosophy adopted after a 2024 change).
- If a required DevRev field has no valid value from the external record, the platform substitutes a **fallback value** defined in the recipe blueprint. Fallbacks cannot be applied to reference fields. Fallback changes only affect newly created records, not existing ones.
- The Recipe Manager can produce three outcomes during initial import: (1) error the import, (2) ask the user to use the mapping screen, or (3) complete the recipe phase automatically.
- **Recipe deficiencies:** The platform can evaluate a recipe blueprint against an existing sync unit to determine compatibility. If incompatible, deficiencies are listed for the user.
- Sync run reports and statuses are visible per sync unit under **Settings -> AirSync -> View Report**.

## Airdrop setup (step-by-step)

1. Go to **Settings -> Integrations -> AirSyncs**.
2. Select **AirSync** (or **Start AirSync** if first time).
3. Create a new connection to the external system (or use an existing one). Authentication depends on the external system: OAuth for cloud services, PAT for on-premise (e.g. Jira Data Center).
4. Select the project/namespace to import (this becomes the sync unit).
5. Configure the import recipe: map issue types, fields, enum values, and set fallback values.
6. Optionally configure filter-by-value to restrict which records sync.
7. Start the initial import. Monitor progress under **Settings -> AirSync -> View Report**.
8. Optionally enable periodic sync: **Settings -> AirSync -> ... -> Set Periodic Sync** (runs hourly by default for bidirectional sync).

## Related flows
- Initial sync setup flow (connect external system, configure mappings, start sync)
- Ongoing bidirectional sync flow
- [gap] Conflict resolution flow with precedence rules

## Related scenarios
- [gap] Scenarios to be created from 1637 test cases

## Airdrop vs AirSync

- **Airdrop** -- DevRev's import engine for bringing data from external systems. Supports field mapping, type mapping, and filter-by-value. See [[glossary/airdrop]].
  - **Initial import:** One-time bulk import.
  - **Periodic sync:** Ongoing sync at intervals.
  - **Automations on Airdrop:** Enable/disable workflow triggers for synced items via Settings > Integrations > Airdrops > ... > Set Periodic Sync > Automations toggle.
- **AirSync** -- Near real-time (5-minute intervals) bidirectional sync between DevRev and external systems. Supports permission syncing. See [[glossary/airsync]].

## Available Integrations (Snap-ins)
GitHub, Slack, Email, Jira, Linear, Zendesk, Salesforce, HubSpot, PagerDuty, WhatsApp, Confluence, Azure DevOps, Okta, ServiceNow, Airtable, Harness, Qase, and many more via the Marketplace (`marketplace.devrev.ai`).

## Connection Methods
- **OAuth:** For services like GitHub, Google, Salesforce.
- **API keys / PAT:** For direct API integrations.
- **Webhooks:** Via snap-in event sources.
- **SCIM:** For identity provider provisioning.

## Open questions
- [gap] How does the sync precedence mechanism resolve conflicts?
- Sync units are the atomic unit of syncing; each sync unit hosts multiple sync runs. Recipes are the runtime transformation functions compiled from recipe blueprints. Sync packs group related sync units. See "Sync units (deep dive)" and "Recipes (deep dive)" sections above.
- [gap] How do blueprint shards differ from full blueprints?
- Automatic sync is triggered by enabling periodic sync (hourly by default via **Settings -> AirSync -> Set Periodic Sync**). Manual sync actions are triggered via `airdrop.sync-units.action` endpoint or the UI.
