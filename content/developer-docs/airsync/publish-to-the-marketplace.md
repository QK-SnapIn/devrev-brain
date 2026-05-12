---
title: Publish to the marketplace
type: developer-doc
status: stable
source: developer.devrev.ai
category: airsync
source_url: https://developer.devrev.ai/airsync/publish-to-marketplace
last_updated: 2026-05-11
summary: "When your snap-in is ready for use by you or other organizations, you can publish it to the DevRev marketplace."
---

# Publish to the marketplace

Publish to the marketplace

When your snap-in is ready for use by you or other organizations, you can publish it to the DevRev marketplace.
Before starting the publication process, make sure your snap-in is deployed to your organization.
If you need a refresher, refer to the [instructions](https://developer.devrev.ai/airsync/deploy-to-organization) for deploying your snap-in.

### [1. Create marketplace listing](#1-create-marketplace-listing)

When creating a new marketplace listing, an initial marketplace submission must be created with all the mandatory properties. To create a new listing, run the following command, which starts a wizard to guide you through the process:

```
devrev marketplace_submissions create
```

### [2. Submit marketplace listing for review](#2-submit-marketplace-listing-for-review)

The newly created marketplace submission is in the *Draft* state. In order to publish it, it first has to transition to *Waiting for review* state. This can be done by running the following command, which starts a wizard to guide you through the process:

```
devrev marketplace_submissions transition
```

Once the submission is transitioned to the *Waiting for review* state, it needs to be approved by a marketplace admin. While in review, the state of the submission is *In review*. Once it is reviewed, the state changes to either *Approved* or *Rejected*.

Submissions whose state is *In review* or *Approved* cannot be modified.

If the submission was rejected, you can transition it back to *Draft* and modify it to satisfy the requirements. Once it is updated, you can transition it back to *Waiting for review* to be reviewed again.

### [3. Publish marketplace submission](#3-publish-marketplace-submission)

If the submission is approved, you can publish it using the following command, which starts a wizard to guide you through the process:

```
devrev marketplace_items publish
```

To make sure that marketplace item was published you can retrieve it using its ID:

```
devrev marketplace_items show [marketplace_item_id] | jq '{name: .name, id: .id, state: .state}'
```

Learn more about the marketplace [here](https://developer.devrev.ai/snapin-development/marketplace-listings).

Last updated on

[Deploy to organization

Previous Page](/airsync/deploy-to-organization)[MCP integration

Next Page](/airsync/mcp)

## Source
- DevRev developer docs: [Publish to the marketplace](https://developer.devrev.ai/airsync/publish-to-marketplace)
