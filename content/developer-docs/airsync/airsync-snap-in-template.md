---
title: AirSync snap-in template
type: developer-doc
status: stable
source: developer.devrev.ai
category: airsync
source_url: https://developer.devrev.ai/airsync/snap-in-template
last_updated: 2026-05-11
summary: "The starter AirSync snap-in template is available here."
---

# AirSync snap-in template

Development Guide

# AirSync snap-in template

The starter AirSync snap-in template is available [here](https://github.com/devrev/airdrop-template).

Starting with the template is recommended, as it includes all the necessary boilerplate and structure for a new project.

The template makes use of **[DevRev's SDK library](https://www.npmjs.com/package/@devrev/ts-adaas)**,
which provides abstraction over the DevRev’s AirSync control protocol.
The SDK simplifies the workflow for data extraction and loading, handling events,
state management, and artifacts (batches of extracted items).

It provides features such as:

* **Event management**: Communication between the AirSync platform and the AirSync snap-in involves messages called
  *events* - depending on the type of event, the snap-in performs different actions.
* **State handling**: Update and access state in real-time within tasks.
* **Artifact management**: Supports batched storage of artifacts.
* **Error & timeout support**: Error handling and timeout management for long-running tasks.
* **Type definitions**: Structured types for AirSync control protocol.

### [Snap-in code structure](#snap-in-code-structure)

If you check the template, you can see that a snap-in is a Node.js project with a specific file structure:

```
- manifest.yaml
- Makefile
- .env.example
- code/
  - scripts/
    - deploy.sh
    - cleanup.sh
  - src/
    - index.ts
    - main.ts
    - function-factory.ts
    - functions/
      - external-system/
        - external_domain_metadata.json
        - initial_domain_mapping.json
        - http-client.ts
        - types.ts
        - data-normalization.ts
        - data-denormalization.ts
      - extraction/
        - workers/
          - attachments-extraction.ts
          - data-extraction.ts
          - external-sync-units-extraction.ts
          - metadata-extraction.ts
        - index.ts
      - loading/
        - workers/
          - load-attachments.ts
          - load-data.ts
        - index.ts
    - test-runner/
      - test-runner.ts
  - test/
    - main.ts
    - runner.ts
```

The `manifest.yaml` is a configuration file that defines details such as the snap-in's name, description, version, connection information, and functionality specifics. Adjusting this file is the initial step in the development of a snap-in.

The `code/` folder holds the implementation of the snap-in. Inside, the `functions/` subfolder includes the logic for retrieving external sync units, extracting data from and loading data to external systems, and mapping between them.

Last updated on

[Getting started

Previous Page](/airsync/getting-started)[Local development

Next Page](/airsync/local-development)

## Source
- DevRev developer docs: [AirSync snap-in template](https://developer.devrev.ai/airsync/snap-in-template)
