---
title: Load data
type: developer-doc
status: stable
source: developer.devrev.ai
category: airsync
source_url: https://developer.devrev.ai/airsync/load-data
last_updated: 2026-05-11
summary: "The load data phase manages the creation and updating of items in the external system."
---

# Load data

Development Guide

# Load data

The load data phase manages the creation and updating of items in the external system.

## [Triggering event](#triggering-event)

AirSync initiates data loading by sending a message with the event type `START_LOADING_DATA` to the snap-in.

If the maximum AirSync snap-in runtime (13 minutes) has been reached,
the snap-in must respond to AirSync with a message with event type of `DATA_LOADING_PROGRESS`, together with an optional progress estimate.

In case of `DATA_LOADING_PROGRESS`, AirSync starts the snap-in with a message with event type `CONTINUE_LOADING_DATA`.

Once the data loading is done, the snap-in must respond to AirSync with a message with event type `DATA_LOADING_DONE`.

## [Implementation](#implementation)

This phase is defined in [load-data.ts](https://github.com/devrev/airdrop-template/blob/main/code/src/functions/loading/workers/load-data.ts).

Loading is performed by providing a list of item types to load (`itemTypesToLoad`), ordered in the sequence they should be loaded.

Each item type must provide `create` and `update` functions, which handle the denormalization of records to the schema of the external system and facilitate HTTP calls to the external system. Both loading functions must manage rate limiting for the external system and handle errors. The `create` and `update` functions should return an `ExternalSystemItemLoadingResponse` object with: `id` (the external system record ID), optionally `modifiedDate`, `delay` (number of seconds for rate-limit back-off), or `error` (error message string). If a record cannot be created or updated, they indicate the rate-limiting offset or errors.

The snap-in must always emit a single message.

```
processTask<LoaderState>({
  task: async ({ adapter }) => {
    const { reports, processed_files } = await adapter.loadItemTypes({
      itemTypesToLoad: [
        {
          itemType: 'todos',
          create: createTodo,
          update: updateTodo,
        },
      ],
    });

    await adapter.emit(LoaderEventType.DataLoadingDone, {
      reports,
      processed_files,
    });
  },
  onTimeout: async ({ adapter }) => {
    await adapter.emit(LoaderEventType.DataLoadingProgress, {
      reports: adapter.reports,
      processed_files: adapter.processedFiles,
    });
  },
});
```

Last updated on

[Loading phases

Previous Page](/airsync/loading-phases)[Load attachments

Next Page](/airsync/load-attachments)

## Source
- DevRev developer docs: [Load data](https://developer.devrev.ai/airsync/load-data)
