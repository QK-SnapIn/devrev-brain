---
title: Versioning
type: developer-doc
status: stable
source: developer.devrev.ai
category: about
source_url: https://developer.devrev.ai/about/versioning
last_updated: 2026-05-11
summary: "The current version of the DevRev public API is 2022-10-20."
---

# Versioning

Versioning

## [Public APIs](#public-apis)

The current version of the DevRev public API is `2022-10-20`.

By default, requests implicitly use version `2022-10-20` unless you override the API version by passing
in the `X-Devrev-Version` header with the requested version.

```
X-Devrev-Version: 2022-10-20
```

When backwards-incompatible changes are made to the API, a new, dated version is released. The customer can opt-in by providing the date string which gets published in the documentation.

If DevRev needs to introduce a new version, we provide adequate notice for users to migrate or adopt the new version. All public API versions are supported for at least 1 year.

## [Beta (early-access) APIs](#beta-early-access-apis)

DevRev exposes newer functionality in the form of [beta APIs](https://developer.devrev.ai/beta) to allow early adopters to explore and
experiment. These APIs are likely evolve and change as we receive more feedback, so they do not
have the same backward compatibility and version guarantees as our public APIs.

To use beta APIs, send the following header with your request:

```
X-Devrev-Scope: beta
```

Last updated on

[Pagination

Previous Page](/about/pagination)[Rate Limits

Next Page](/about/rate-limits)

## Source
- DevRev developer docs: [Versioning](https://developer.devrev.ai/about/versioning)
