---
title: Getting started
type: developer-doc
status: stable
source: developer.devrev.ai
category: airsync
source_url: https://developer.devrev.ai/airsync/getting-started
last_updated: 2026-05-11
summary: "Before starting snap-in development, it's important to understand these fundamental terms and concepts, as well as the capabilities and limitations of the external system being integrated."
---

# Getting started

Getting started

Before starting snap-in development, it's important to understand these fundamental terms and concepts,
as well as the capabilities and limitations of the external system being integrated.

## [DevRev organization](#devrev-organization)

If this is your first time developing a snap-in, you should start by creating a new DevRev organization:

1. Click on your profile picture in the top left corner.
2. Go to the **Orgs** section and click on **+**.
3. Fill in the necessary details and click **Create**.

You now find your newly created organization under **Orgs**.

## [External system](#external-system)

Before starting the development of a snap-in for integration with an external system API,
consider gathering the following information:

* **API documentation**: Obtain the official API documentation of the external system.
  This is the primary source of information about how to connect and interact with the system.
* **Authentication and authorization**: Understand the authentication and authorization
  methods required. This may include API keys, OAuth tokens, or other security mechanisms.
* **Endpoints and resources**: Identify the required API endpoints and resources. Understand
  their functions, input parameters, expected outputs, and usage limitations.
* **Data format**: Determine the data format used by the API, such as JSON or XML. This helps
  in parsing responses and formatting requests appropriately.
* **Rate limits and quotas**: Be aware of any rate limits or usage quotas. This information is
  crucial to ensure that the integration does not exceed allowed requests or data usage.
* **Error handling**: Learn about error response formats and codes. Knowing this helps in
  handling errors and exceptions in your integration.

## [Basic concepts](#basic-concepts)

### [Sync unit](#sync-unit)

A *sync unit* is one self-encompassing unit of data that is synced to an external system. For example:

* A project in Jira.
* An account in SalesForce.
* An organization Zendesk.

In Jira, users often have multiple projects. Each project acts as an individual sync unit.
In contrast, Zendesk operates with a single large pool of tickets and agents. Here, the entire Zendesk instance can be synced in a single import.

### [Sync run](#sync-run)

AirSync extractions are done in *sync runs*.
A sync run is one end-to-end (extract-transform-load) execution of a *sync unit*.
If you do an initial import from the external system to DevRev, that import is one sync run.
Another import in the same direction is another sync run.
And if you then decide to do a reverse sync from DevRev to the external system, that would be another
sync run.

Each sync run is comprised out of phases.
Phases follow sequentially, and each can consist of one or more invocations of the snap-in.

### [Forward sync](#forward-sync)

A *forward sync* is a sync run from an external system to DevRev.
An **extractor** function in the snap-in is responsible for extracting data from the external system.

### [Reverse sync](#reverse-sync)

A *reverse sync* is a sync run from DevRev to an external system.
It uses a **loader** function, to create or update data in the external system.

### [Initial sync](#initial-sync)

The first sync is called the *initial sync*.
It is triggered manually by the end user in DevRev's **AirSyncs** UI.

During the initial sync, all data from the external sync unit is extracted from the external system and loaded into DevRev.
This process typically involves a large import and may take some time.

An *initial import* consists of the following phases:

1. External sync units extraction
2. Metadata extraction
3. Data extraction
4. Attachments extraction

### [1-way (incremental sync)](#1-way-incremental-sync)

A *1-way sync* (or *incremental sync*) refers to any extraction after the initial sync run has been successfully completed.

An extractor extracts data that was created or updated in the external system after the start
of the latest successful forward sync.
This includes any changes that happened after the start of the previous sync, but were not picked up by it.

A 1-way sync consists of the following phases:

1. Metadata extraction
2. Data extraction
3. Attachments extraction

### [2-way sync](#2-way-sync)

A *2-way sync* is a reverse sync.
The loader receives information about changes in DevRev since the last successful reverse sync and updates the data in the external system.

A 2-way sync consists of the following phases:

1. Data loading
2. Attachments loading

### [Time-scoped sync](#time-scoped-sync)

Normally, an initial sync extracts all data from an organization, and an incremental sync only extracts changes since the last successful sync. A *time-scoped sync*, on the other hand, allows for the extraction of data beginning from a custom timestamp.

This approach is useful for initially testing the integration with a smaller data set—such as data from the last month—before conducting a full import of all available data.

Last updated on

[Overview

Previous Page](/airsync)[Snap-in template

Next Page](/airsync/snap-in-template)

## Source
- DevRev developer docs: [Getting started](https://developer.devrev.ai/airsync/getting-started)
