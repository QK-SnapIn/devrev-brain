---
title: Object Mappers
type: developer-doc
status: stable
source: developer.devrev.ai
category: airsync
source_url: https://developer.devrev.ai/airsync/object-mappers
last_updated: 2026-05-11
summary: "Object Mappers are a core component of AirSync that manage and track the relationships between objects imported from external systems and their corresponding entities in DevRev."
---

# Object Mappers

Development Guide

# Object Mappers

Object Mappers are a core component of AirSync that manage and track the relationships between objects imported from external systems and their corresponding entities in DevRev. Think of Object Mappers as a comprehensive lookup table that maintains the synchronization state between external and DevRev objects.

Each sync mapper record contains external system identifiers, corresponding DevRev entity IDs, sync unit scope, operational status, and additional metadata. This bidirectional mapping system enables AirSync to efficiently track which external objects have been synchronized and locate their DevRev counterparts during ongoing operations. Object Mappers are available through the adapter object as `adapter.mappers` in your AirSync snap-in functions.

## [When to use Object Mappers](#when-to-use-object-mappers)

Object Mappers are essential in several AirSync scenarios:

**During data extraction and relationship management** - Check if sync mapper records already exist to avoid duplicates, find related DevRev entities for nested objects like comments and attachments, and link child objects to their parent entities.

```
import { SyncMapperRecordTargetType } from "@devrev/ts-adaas";

// Check if sync mapper record for attachment already exists
const existingSyncMapperRecord = await adapter.mappers.getByExternalId({
  sync_unit: adapter.event.payload.event_context.sync_unit,
  external_id: attachment.id,
  target_type: SyncMapperRecordTargetType.ARTIFACT,
});

// Find parent work item for comment
const parentSyncMapperRecord = await adapter.mappers.getByExternalId({
  sync_unit: adapter.event.payload.event_context.sync_unit,
  external_id: externalComment.ticket_id,
  target_type: SyncMapperRecordTargetType.WORK,
});
```

**During loading operations** - Locate IDs of objects in external system for DevRev entities when pushing data back to external systems and maintain consistency between systems.

```
// Find external ID to update external system
const syncMapperRecord = await adapter.mappers.getByTargetId({
  sync_unit: adapter.event.payload.event_context.sync_unit,
  target: devrevWorkId,
});
```

## [Object Mapper methods](#object-mapper-methods)

### [Get by DevRev ID](#get-by-devrev-id)

Use `getByTargetId` when you have a DevRev entity ID and need to find the corresponding ID of an object in external system:

```
const response = await adapter.mappers.getByTargetId({
  sync_unit: adapter.event.payload.event_context.sync_unit,
  target: devrevEntityId,
});

const externalIds = response.data.sync_mapper_record.external_ids;
```

### [Get by external ID](#get-by-external-id)

Use `getByExternalId` when you have an ID of an object in external system and need to find the corresponding DevRev entity:

```
import { SyncMapperRecordTargetType } from "@devrev/ts-adaas";

const response = await adapter.mappers.getByExternalId({
  sync_unit: adapter.event.payload.event_context.sync_unit,
  external_id: externalSystemId,
  target_type: SyncMapperRecordTargetType.WORK,
});

const devrevTargets = response.data.sync_mapper_record.targets;
```

### [Create new sync mapper record](#create-new-sync-mapper-record)

Use `create` to establish a new sync mapper record between external and DevRev entities. Create a mapper only when you are persisting a new link (for example, right after creating the external object in reverse sync), not for read-only extraction. This prevents duplicates in subsequent syncs by enabling lookups in both directions.

```
import { SyncMapperRecordStatus } from "@devrev/ts-adaas";

const response = await adapter.mappers.create({
  sync_unit: adapter.event.payload.event_context.sync_unit,
  external_ids: [externalSystemId],
  targets: [devrevEntityId],
  status: SyncMapperRecordStatus.OPERATIONAL,
});
```

### [Update existing sync mapper record](#update-existing-sync-mapper-record)

Use `update` to modify an existing sync mapper record:

```
import { SyncMapperRecordStatus } from "@devrev/ts-adaas";

const response = await adapter.mappers.update({
  id: syncMapperRecordId,
  sync_unit: adapter.event.payload.event_context.sync_unit,
  external_ids: {
    add: [newExternalId],
  },
  targets: {
    add: [newDevrevEntityId],
  },
  status: SyncMapperRecordStatus.OPERATIONAL,
});
```

## [Sync mapper record status values](#sync-mapper-record-status-values)

| Status | Value | Description |
| --- | --- | --- |
| `OPERATIONAL` | `'operational'` | The mapping is active and operational (default) |
| `FILTERED` | `'filtered'` | The mapping was filtered out by user filter settings |
| `IGNORED` | `'ignored'` | The external object should be ignored in sync operations. Use to prevent objects from being created or updated in DevRev. |

## [Common target types](#common-target-types)

The `SyncMapperRecordTargetType` enum provides the following commonly used values:

| Target type | Description |
| --- | --- |
| `WORK` | Work items (issues, tickets, tasks, etc.) |
| `PART` | Parts (capabilities, products, features, components, etc.) |
| `USER` | DevRev users (includes all user types: dev users, sys users, and rev users) |
| `ACCOUNT` | Customer accounts |
| `ARTIFACT` | Attachments and files |
| `CONVERSATION` | Conversations |
| `LINK` | Links between objects |
| `TAG` | Tags |
| `GROUP` | Groups |
| `TIMELINE_COMMENT` | Comments |
| `ARTICLE` | Knowledge base articles |
| `CUSTOM_OBJECT` | Custom object types |
| `INCIDENT` | Incidents |

Additional target types include `ACCESS_CONTROL_ENTRY`, `AIRDROP_AUTHORIZATION_POLICY`, `AIRDROP_FIELD_AUTHORIZATION_POLICY`, `AIRDROP_PLATFORM_GROUP`, `CHAT`, `DIRECTORY`, `MEETING`, `OBJECT_MEMBER`, `REV_ORG`, `ROLE`, and `ROLE_SET`.

## [Additional sync mapper record fields](#additional-sync-mapper-record-fields)

### [`secondary_ids`](#secondary_ids)

Optional map that labels values in `external_ids` with their usage context. Use when an external system requires different identifiers for different API calls (for example, a UUID for one endpoint and a login username for another).

```
await adapter.mappers.create({
  sync_unit: adapter.event.payload.event_context.sync_unit,
  external_ids: ["2a1c-uuid", "john_doe"],
  secondary_ids: { username: "john_doe" },
  targets: [devrevEntityId],
  status: SyncMapperRecordStatus.OPERATIONAL,
});
```

Values in `secondary_ids` are not indexed. If you need to look up by a secondary value, you must also include that value in `external_ids`.

### [`external_versions`](#external_versions)

Records external-system changes to prevent update loops in bidirectional sync. When you create or update an object in the external system during loading, add that object's `modified_date` here. Later, when the object is extracted and the loader evaluates whether to apply it, if the `modified_date` is present in this list, the update is skipped (because the change originated in DevRev).

The `recipe_version` field is managed internally by the SDK (currently set to `0`). Connectors do not need to determine or provide a meaningful recipe version themselves.

```
await adapter.mappers.update({
  id: syncMapperRecordId,
  sync_unit: adapter.event.payload.event_context.sync_unit,
  external_ids: { add: [externalId] },
  targets: { add: [devrevEntityId] },
  status: SyncMapperRecordStatus.OPERATIONAL,
  external_versions: {
    add: [{ recipe_version: 0, modified_date: "2024-01-15T10:30:00Z" }],
  },
});
```

### [`extra_data`](#extra_data)

Free-form string field for storing any additional connector-specific data on the sync mapper record.

### [`input_files`](#input_files)

Optionally populated with the file name of the input file containing the object data. Useful for debugging - helps locate objects in the original extraction artifacts.

Last updated on

[Load attachments

Previous Page](/airsync/load-attachments)[Examples of snap-ins

Next Page](/airsync/snap-in-examples)

## Source
- DevRev developer docs: [Object Mappers](https://developer.devrev.ai/airsync/object-mappers)
