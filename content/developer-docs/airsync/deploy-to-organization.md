---
title: Deploy to organization
type: developer-doc
status: stable
source: developer.devrev.ai
category: airsync
source_url: https://developer.devrev.ai/airsync/deploy-to-organization
last_updated: 2026-05-11
summary: "Once you're ready to test your snap-in in a production environment, you can deploy the snap-in to your organization."
---

# Deploy to organization

Deploy to organization

Once you're ready to test your snap-in in a production environment, you can deploy the snap-in to your organization.

Follow these steps:

1. Copy `.env.example` to a new file named `.env` and fill in the required variables.
2. Deploy a draft version of your snap-in to your organization by using `make deploy`.
3. Install the snap-in in your DevRev by going to **Settings** > **Snap-ins** > **Install snap-in**.
4. Set up the connection under **Settings** > **Integrations** > **AirSyncs** > **Connections**.
5. Create an import at **Settings** > **AirSyncs** > **AirSync**.

This step is also a prerequisite for publishing the snap-in on the DevRev marketplace.

### [Observability](#observability)

To observe logs from your snap-in in your development environment:

```
devrev snap_in_package logs | jq
```

To open logs in your favorite editor:

```
devrev snap_in_package logs | code -
```

For more information, refer to [Debugging](https://developer.devrev.ai/snapin-development/debugging).

Last updated on

[Examples of snap-ins

Previous Page](/airsync/snap-in-examples)[Publish to the marketplace

Next Page](/airsync/publish-to-marketplace)

## Source
- DevRev developer docs: [Deploy to organization](https://developer.devrev.ai/airsync/deploy-to-organization)
