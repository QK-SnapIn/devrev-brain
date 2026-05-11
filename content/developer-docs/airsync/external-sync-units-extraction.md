---
title: External sync units extraction
type: developer-doc
status: stable
source: developer.devrev.ai
category: airsync
source_url: https://developer.devrev.ai/airsync/external-sync-units-extraction
last_updated: 2026-05-11
summary: "An external sync unit refers to a single unit in the external system that is being AirSynced to DevRev."
---

# External sync units extraction

Development Guide

# External sync units extraction

An *external sync unit* refers to a single unit in the external system that is being AirSynced to DevRev.
In some systems, this is a project; in some it is a repository; in support systems it could be
called a brand or an organization.
What a unit of data is called and what it represents depends on the external system's domain model.
It usually combines contacts, users, work-like items, and comments into a unit of domain objects.

In the external sync unit extraction phase, the snap-in is expected to obtain a list of external
sync units that it can extract from the external system API and send it to AirSync in its response.

External sync unit extraction is executed only during the initial import.

## [Triggering event](#triggering-event)

AirSync starts the external sync unit extraction by sending a message with the event type `START_EXTRACTING_EXTERNAL_SYNC_UNITS`.

The snap-in must reply to AirSync with an `EXTERNAL_SYNC_UNIT_EXTRACTION_DONE` message when finished,
or `EXTERNAL_SYNC_UNIT_EXTRACTION_ERROR` if an error occurs.

## [Implementation](#implementation)

This phase should be implemented in the [`external-sync-units-extraction.ts`](https://github.com/devrev/airdrop-template/blob/main/code/src/functions/extraction/workers/external-sync-units-extraction.ts) file.

The snap-in should emit the list of external sync units in the given format:

```
const externalSyncUnits: ExternalSyncUnit[] = [
  {
    id: "devrev",
    name: "devrev",
    description: "Demo external sync unit",
    item_count: 100,
    item_type: "todos",
  },
];
```

* `id`: The unique identifier in the external system.
* `name`: The human-readable name in the external system.
* `description`: The short description if the external system provides it.
* `item_count`: The number of items (issues, tickets, comments or others) in the external system.
  Item count should be provided if it can be obtained in a lightweight manner, such as by calling an API endpoint.
  If there is no such way to get it (for example, if the items would need to be extracted to count them),
  then the item count should be `-1` to avoid blocking the import with long-running queries.
* `item_type`: (Optional) The type identifier for items in this sync unit.

The snap-in must respond to AirSync with a message, which contains a list of external sync units as a payload:

```
import {
  ExternalSyncUnit,
  ExtractorEventType,
  processTask,
} from "@devrev/ts-adaas";

processTask({
  task: async ({ adapter }) => {
    const externalSyncUnits: ExternalSyncUnit[] = [
      {
        id: "devrev",
        name: "devrev",
        description: "Demo external sync unit",
        item_count: 100,
        item_type: "todos",
      },
    ];
    await adapter.emit(ExtractorEventType.ExternalSyncUnitExtractionDone, {
      external_sync_units: externalSyncUnits,
    });
  },
  onTimeout: async ({ adapter }) => {
    await adapter.emit(ExtractorEventType.ExternalSyncUnitExtractionError, {
      error: {
        message: "Failed to extract external sync units. Lambda timeout.",
      },
    });
  },
});
```

> **Migration note (v1.17.0):** External sync units can now be uploaded via the repository system
> instead of passing them inline in the emit payload. The inline approach (passing `external_sync_units`
> in `adapter.emit()`) still works but is deprecated. The new approach uses `adapter.initializeRepos()`
> with `AirSyncDefaultItemTypes.EXTERNAL_SYNC_UNITS` and the `push()` method:
>
> ```
> import {
>   AirSyncDefaultItemTypes,
>   ExtractorEventType,
>   processTask,
> } from "@devrev/ts-adaas";
>
> processTask({
>   task: async ({ adapter }) => {
>     adapter.initializeRepos([
>       {
>         itemType: AirSyncDefaultItemTypes.EXTERNAL_SYNC_UNITS,
>         overridenOptions: { batchSize: 25000, skipConfirmation: true },
>       },
>     ]);
>     const externalSyncUnits = [
>       /* ... */
>     ];
>     await adapter
>       .getRepo(AirSyncDefaultItemTypes.EXTERNAL_SYNC_UNITS)
>       ?.push(externalSyncUnits);
>     await adapter.emit(ExtractorEventType.ExternalSyncUnitExtractionDone);
>   },
>   onTimeout: async ({ adapter }) => {
>     await adapter.emit(ExtractorEventType.ExternalSyncUnitExtractionError, {
>       error: {
>         message: "Failed to extract external sync units. Lambda timeout.",
>       },
>     });
>   },
> });
> ```
>
> See the [full release notes](https://github.com/devrev/adaas-sdk/releases/tag/v1.17.0) for details.

**The snap-in must always emit a single message.**

To test your changes:

1. Start a new airdrop in the DevRev App.
2. If external sync units extraction is successful, verify that you are prompted to choose an external sync unit from the list.

Last updated on

[Extraction phases

Previous Page](/airsync/extraction-phases)[Metadata extraction

Next Page](/airsync/metadata-extraction)

## Source
- DevRev developer docs: [External sync units extraction](https://developer.devrev.ai/airsync/external-sync-units-extraction)
