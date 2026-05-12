---
title: Loading phases
type: developer-doc
status: stable
source: developer.devrev.ai
category: airsync
source_url: https://developer.devrev.ai/airsync/loading-phases
last_updated: 2026-05-11
summary: "Loading is the process of exporting data from DevRev back to the external system."
---

# Loading phases

Development Guide

# Loading phases

Loading is the process of exporting data from DevRev back to the external system.
This process includes creating new items in the external system and updating them with any changes made in DevRev.

The snap-in manages two phases for loading:

* Load data
* Load attachments

Additionally, loader state deletion phases (`START_DELETING_LOADER_STATE` and `START_DELETING_LOADER_ATTACHMENT_STATE`) are handled automatically by the SDK since v1.13.1 - no custom implementation is needed.

Each phase is defined in a separate file and is responsible for loading the corresponding data.

```
import { AirdropEvent, spawn } from "@devrev/ts-adaas";
import initialDomainMapping from "../external-system/initial_domain_mapping.json";

export interface LoaderState {}

export const initialLoaderState: LoaderState = {};

const run = async (events: AirdropEvent[]) => {
  for (const event of events) {
    await spawn<LoaderState>({
      event,
      initialState: initialLoaderState,
      initialDomainMapping,
      baseWorkerPath: __dirname,
    });
  }
};

export default run;
```

> **Migration note (v1.13.0):** The `workerPath` parameter and manual switch-case
> routing are deprecated. Use `baseWorkerPath: __dirname` instead - the SDK resolves
> worker file paths automatically based on event type. Worker files must follow the
> naming convention `{baseWorkerPath}/workers/{worker-file-name}` (for example, `load-data`, `load-attachments`).
> See the [full release notes](https://github.com/devrev/adaas-sdk/releases/tag/v1.13.2) for details.

You must pass the `initialDomainMapping` parameter to 
`spawn` when running loading phases. This ensures the correct
domain mapping is installed and used by the snap-in.

## [State handling](#state-handling)

Loading phases run as separate runtime instances, similar to extraction phases, with a maximum execution time of 13 minutes.
These phases share a `state`, defined in the `LoaderState` interface.
It is important to note that the loader state is separate from the extractor state.

Access to the `state` is available through the SDK's `adapter` object.

## [How loading is triggered](#how-loading-is-triggered)

When a user creates or updates an item in DevRev that belongs to a synced external sync unit, AirSync initiates the loading flow to push those changes to the external system.

To create an item in DevRev and sync it with the external system:

1. Create an item with a **subtype** that was established during the initial sync.
2. After selecting the subtype, fill out the necessary details for the item.

Last updated on

[Customize attachment processing

Previous Page](/airsync/customize-attachment-processing)[Load data

Next Page](/airsync/load-data)

## Source
- DevRev developer docs: [Loading phases](https://developer.devrev.ai/airsync/loading-phases)
