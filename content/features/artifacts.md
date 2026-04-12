---
title: Artifacts
type: feature
status: draft
sources: [raw/test-cases/by-feature/fe_artifacts.jsonl, raw/docs/devrev-developer-docs.md]
related: []
last_updated: 2026-04-12
---

# Artifacts

## What it does
The Artifacts feature manages file and binary object storage within DevRev. It supports a multi-step upload workflow (prepare, upload to presigned URL, create-from-content), versioning, content validation, and retrieval. With 80 test cases, this feature handles the full artifact lifecycle from creation through download. The backend service is `us_artifacts_client`.

## Why it exists
DevRev users need to attach files to various entities (parts, articles, conversations, etc.). Artifacts provide the underlying storage layer that handles presigned URL generation, content staging, validation, versioning, and retrieval, abstracting away the complexity of cloud storage.

## Key behaviors
- **Two-phase creation**: First `artifacts.prepare` to get presigned URL + form_data, then `artifacts.create-from-content` with staged_content_id
- **Configuration sets**: Artifacts support configuration sets (e.g., `default`, `article_media`)
- **DON format IDs**: Artifact IDs follow `don:core:dvrv-*:devo/*:artifact/*` pattern
- **Versioning**: Prepare new versions via `artifacts.versions.prepare` (returns different presigned URL from initial create); list versions
- **Content validation**: Validate artifact contents before creation
- **Schema completeness**: Response includes AtomBase fields: id, created_date, modified_date, created_by, modified_by, display_id, and file object (name, type, size)
- **End-to-end retrieval**: Newly created artifacts are immediately retrievable via `artifacts.get`

## Entry points
- **Base URL**: `https://api.devrev.ai/internal/`
- Namespace: `artifacts.*`
- Requires `Authorization: Bearer $TOKEN`

## API endpoints

| Endpoint | Methods | Description |
|----------|---------|-------------|
| `artifacts.create-from-content` | POST | Create artifact from staged content |
| `artifacts.contents.validate` | POST | Validate artifact contents |
| `artifacts.versions.prepare` | POST | Prepare a new version |
| `artifacts.versions.list` | POST | List artifact versions |

## Related flows
- [gap] Artifact upload flow (prepare -> upload -> create)
- [gap] Artifact versioning flow

## Related scenarios
- [gap] Scenarios to be created from 80 test cases

## Open questions
- [gap] What configuration sets are available beyond `default` and `article_media`?
- [gap] What content validation rules are applied?
- [gap] What is the maximum artifact size?
- [gap] How are artifact versions ordered and managed?
