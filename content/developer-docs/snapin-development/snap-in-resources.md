---
title: Snap-in resources
type: developer-doc
status: stable
source: developer.devrev.ai
category: snapin-development
source_url: https://developer.devrev.ai/snapin-development/references/snap-in-resources
last_updated: 2026-05-11
summary: "Snap-in resources are objects specific to each user for a snap-in."
---

# Snap-in resources

References

# Snap-in resources

Snap-in resources are objects specific to each user for a snap-in. These objects can be

* Keyrings
* Inputs
* Event sources

For a snap-in to access these resources, the user must configure **My Settings** of the snap-in config and enable it.
The snap-in can get these resources using the `snap-ins.resources` [beta API](https://developer.devrev.ai/beta/api-reference/snap-ins/resources) by specifying the snap-in ID in the `id` field and the user ID in the `user` field.

This API can only be called by the service account associated with the snap-in.

Last updated on

## Source
- DevRev developer docs: [Snap-in resources](https://developer.devrev.ai/snapin-development/references/snap-in-resources)
