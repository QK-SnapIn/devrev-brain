---
title: Brands
type: feature
status: draft
sources: [raw/test-cases/by-feature/fe_brands.jsonl, raw/docs/devrev-developer-docs.md, raw/docs/ devrev-agent-dump-kb.md]
related: ["features/knowledge-base", "features/customer-portal"]
last_updated: 2026-04-12
---

# Brands

## What it does
The Brands feature manages brand entities within DevRev, enabling organizations to create, list, and delete brands. Brands are used to customize the appearance and identity of customer-facing interfaces (e.g., help centers, support portals). With 51 test cases, this feature provides a straightforward CRUD interface with strong consistency guarantees. The backend service is `us_plug`.

## Why it exists
Organizations often operate multiple product lines or customer-facing identities. Brands allow them to maintain distinct visual identities and configurations for each, ensuring customers see the correct branding in support portals and knowledge base articles.

## Current Status
Native multi-brand support is **on the roadmap** (not yet fully available as a self-serve feature). The goal is to allow companies with multiple sub-brands to have separate help centers with different looks, article sets, and PLuG configurations -- all managed from a single DevRev workspace.

## Key behaviors
- **Brand CRUD**: Create, list (GET and POST), delete brands
- **Brand update**: Brands can be updated via `brands.update` API endpoint (see also [[features/knowledge-base]])
- **Response contract**: `brands` array is always present in list responses (never null or absent), even when empty
- **Immediate consistency**: Newly created brands appear in subsequent list calls; deleted brands disappear immediately
- **Empty state handling**: Returns 200 OK with empty `brands: []` when no brands exist
- **Pagination**: Supports cursor-based pagination with next_cursor/prev_cursor
- **Schema conformance**: Responses conform to `brands-list-response` schema

## Brand Configuration Details

### Current Workaround for Multi-Brand KB
Collections (directories) are created per brand to keep articles separated:
```
Brand A directory
  Categories from Brand A
  Articles from Brand A
Brand B directory
  Categories from Brand B
  Articles from Brand B
```

### Branding the Portal Today
Customize colors, fonts, logo, favicon, and banner images via Settings > Plug & Portal > Portal Settings > Appearance (see [[features/customer-portal]]).

Available appearance settings:
- **Portal Theme** -- Dark or Light mode
- **Company Assets** -- Company name, logo, favicon
- **Color Tokens** -- Accent color
- **Header** -- Header tabs
- **Hero Section** -- Web and mobile banner images, welcome text, search placeholder text
- **Footer** -- Social media and company links

A **Live Preview panel** shows changes in real time before publishing.

## Relationship to Help Center
A brand represents a distinct, branded support portal for a separate product line. Currently, since multi-brand is not fully self-serve, organizations use the collection-per-brand workaround to separate articles while sharing a single help center instance. Portal appearance settings apply workspace-wide.

## Entry points
- **Base URL**: `https://api.devrev.ai/internal/`
- Namespace: `brands.*`
- Requires `Authorization: Bearer $TOKEN`
- Portal branding: Settings > Plug & Portal > Portal Settings > Appearance

## API endpoints

| Endpoint | Methods | Description |
|----------|---------|-------------|
| `brands.create` | POST | Create a brand |
| `brands.get` | GET, POST | Get a brand |
| `brands.list` | GET, POST | List all brands |
| `brands.update` | POST | Update a brand |
| `brands.delete` | POST | Delete a brand |

## Related flows
- [gap] Brand creation and management flow

## Related scenarios
- [gap] Scenarios to be created from 51 test cases

## Open questions
- [gap] What brand attributes beyond `name` are supported (logo, colors, etc.)?
- [gap] Is there a limit on the number of brands per organization?
