---
title: Extraction phases
type: developer-doc
status: stable
source: developer.devrev.ai
category: airsync
source_url: https://developer.devrev.ai/airsync/extraction-phases
last_updated: 2026-05-11
summary: "Each snap-in must handle all the phases of extraction."
---

# Extraction phases

Development Guide

# Extraction phases

Each snap-in must handle all the phases of extraction. In a snap-in, you typically define a run
function that iterates over events and invokes workers per extraction phase.

The AirSync snap-in extraction lifecycle consists of four phases:

* External sync units extraction (only for initial sync)
* Metadata extraction
* Data extraction
* Attachments extraction

Each phase is defined in a separate file and is responsible for fetching the respective data.

Snap-in development is an iterative process. It typically begins with
retrieving some data from the external system. The next step involves crafting
an initial version of the external domain metadata and validating it through
chef-cli. This metadata is used to prepare the initial domain mapping and
checking for any possible issues. API calls to the external system are then
corrected to fetch the missing data. Start by working with one item type (we
recommend starting with users), and once it maps well to DevRev objects and
imports as desired, proceed with other item types.

The SDK library exports a `processTask` function, which takes an object parameter with two keys:

* `task`: a function that implements the functionality for the given phase.
* `onTimeout`: a function that handles timeouts, typically by simply emitting a message to the AirSync platform.

State management is crucial for snap-ins to maintain the state of the extraction task.
State is saved to the AirSync backend by calling the `postState` function.
During the extraction the state is stored in the adapter and can be retrieved using the `adapter.state` property.

```
import { AirdropEvent, spawn } from "@devrev/ts-adaas";
import initialDomainMapping from "../external-system/initial_domain_mapping.json";

export interface ExtractorState {
  todos: { completed: boolean };
  users: { completed: boolean };
  attachments: { completed: boolean };
}

export const initialExtractorState: ExtractorState = {
  todos: { completed: false },
  users: { completed: false },
  attachments: { completed: false },
};

const run = async (events: AirdropEvent[]) => {
  for (const event of events) {
    await spawn<ExtractorState>({
      event,
      initialState: initialExtractorState,
      initialDomainMapping,
      baseWorkerPath: __dirname,
    });
  }
};

export default run;
```

The SDK automatically resolves worker file paths based on the event type using
the convention `{baseWorkerPath}/workers/{worker-file-name}` 
(for example, `data-extraction`, `metadata-extraction`).

> **Migration note (v1.13.0):** The `workerPath` parameter and manual switch-case
> routing in `spawn()` are deprecated. Use `baseWorkerPath: __dirname` instead.
> If you need to override the default path for specific event types, use `options.workerPathOverrides`.
> See the [full release notes](https://github.com/devrev/adaas-sdk/releases/tag/v1.13.2) for details.

You must pass the `initialDomainMapping` parameter to 
`spawn` when running extraction phases. This ensures the correct
domain mapping is installed and used by the snap-in.

Last updated on

## Source
- DevRev developer docs: [Extraction phases](https://developer.devrev.ai/airsync/extraction-phases)
