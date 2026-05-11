---
title: Build
type: feature
status: draft
sources: [raw/test-cases/by-feature/fe_build.jsonl, raw/docs/devrev-developer-docs.md, https://support.devrev.ai/en-US/devrev/directories]
related: []
last_updated: 2026-05-11
support_articles: [ART-21828, ART-21875, ART-21876, ART-26061]
---

# Build

## What it does
The Build feature manages code changes within DevRev, providing creation, retrieval, and lifecycle management for code change objects that represent pull requests and merge requests from source control systems. With 40 test cases, this feature supports multiple source control platforms and provides immediate consistency between create and read operations. The backend service is `us_codexv2`.

## Why it exists
Development teams need to track code changes (PRs/MRs) within DevRev to link engineering work to product planning and customer issues. The Build feature provides a unified API for ingesting code change data from GitHub, GitLab, and Bitbucket, creating a centralized view of engineering activity.

## Key behaviors
- **Multi-source support**: Create code changes with source values: `github`, `gitlab`, `bitbucket`
- **Required fields**: title and source are required for creation
- **Response schema**: Required response fields include id, display_id, title, source, created_by, modified_by, created_date, modified_date, object_version
- **Immediate retrievability**: Newly created code changes are immediately retrievable via `code-changes.get`
- **Branch tracking**: Supports branch, target_branch, and commit_id fields
- **Object versioning**: Response includes positive integer `object_version`

## Entry points
- **Base URL**: `https://api.devrev.ai/internal/`
- Namespace: `code-changes.*`
- Requires `Authorization: Bearer $TOKEN`

## API endpoints

| Endpoint | Methods | Description |
|----------|---------|-------------|
| `code-changes.create` | POST | Create code change |
| `code-changes.get` | POST | Get code change by ID |

## Related flows
- [gap] Code change ingestion from SCM webhooks flow
- [gap] Code change to work item linking flow

## Related scenarios
- [gap] Scenarios to be created from 40 test cases

## Open questions
- [gap] Are there other source values beyond github, gitlab, bitbucket?
- [gap] How do code changes link to work items (issues/tickets)?
- [gap] What triggers code change creation (webhooks, manual, CI/CD)?
- [gap] What additional fields are available beyond the basics (labels, reviewers, etc.)?

## Support documentation

Referenced DevRev support articles synchronized from [support.devrev.ai](https://support.devrev.ai/en-US/devrev/directories):

- [[support-articles/computer-by-devrev/build-your-first-ai-agent|Build your first AI agent]] (ART-26061) — [external](https://support.devrev.ai/en-US/devrev/article/ZqvK4VT6)
- [[support-articles/computer-plus-build/builder-best-practices|Builder best practices]] (ART-21875) — [external](https://support.devrev.ai/en-US/devrev/article/2mQH6ZfC)
- [[support-articles/computer-plus-build/computer-for-builders-snap-ins|Computer for Builders snap-ins]] (ART-21876) — [external](https://support.devrev.ai/en-US/devrev/article/2SL1-IeT)
- [[support-articles/computer-plus-build/computer-build-overview|Computer+ Build overview]] (ART-21828) — [external](https://support.devrev.ai/en-US/devrev/article/SFzsiTJK)
