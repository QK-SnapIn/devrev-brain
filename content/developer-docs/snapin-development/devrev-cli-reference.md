---
title: DevRev CLI reference
type: developer-doc
status: stable
source: developer.devrev.ai
category: snapin-development
source_url: https://developer.devrev.ai/snapin-development/references/cli
last_updated: 2026-05-11
summary: "The following is a list of DevRev CLI commands:"
---

# DevRev CLI reference

References

# DevRev CLI reference

The following is a list of DevRev CLI commands:

## [CLI version](#cli-version)

Check the version of CLI:

```
devrev --version
```

## [CLI help](#cli-help)

To check all the available commands, run the following command:

```
devrev --help
```

Use `devrev [command] --help` for more information about a command.

## [Authentication](#authentication)

## [Snap-in package](#snap-in-package)

## [Snap-in version](#snap-in-version)

## [Snap-in](#snap-in)

## [Snap-in context](#snap-in-context)

The CLI persists in the context of the CLI in a snap-in context. The context is used to store the following information per snap-in package slug:

1. The ID of the snap-in package owning the slug.
2. The ID of the last created/upgraded snap-in version, if any.
3. The ID of the latest deployed snap-in, if any.

Last updated on

[Install DevRev CLI

Previous Page](/snapin-development/references/cli-install)[Snap-in manifest

Next Page](/snapin-development/references/manifest)

## Source
- DevRev developer docs: [DevRev CLI reference](https://developer.devrev.ai/snapin-development/references/cli)
