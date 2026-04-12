---
title: Parts
type: feature
status: draft
sources: [raw/test-cases/by-feature/fe_parts.jsonl, raw/docs/devrev-developer-docs.md, raw/docs/devrev-docs-scraped.md, raw/docs/devrev-agent-dump-part1.md]
related: ["entities/part", "glossary/trails", "features/stock-objects"]
last_updated: 2026-04-12
---

# Parts

## What it does
The Parts feature manages product hierarchy objects in DevRev. **Parts** are product/service components with lifecycles (creation, operation, evolution, deprecation). Events and work items must be related to parts, and they form recursive hierarchies. **Trails** ([[glossary/trails]]) is an extensible interface that allows you to view and manage your part hierarchy and related items. With 180 test cases, this feature is backed by the `us_partiql` service.

## Why it exists
Product teams need to decompose their product into a hierarchy of parts to plan, track, and ship work. Parts serve as the organizational backbone connecting customer needs (conversations/tickets) to engineering work (issues) through product structure. Part of the [[build-app]] (Computer for Builders).

## Two Part Categories

**Customer parts** represent how products are consumed externally -- like APIs or features customers interact with.

**Builder parts** are internal components:
- **Runnable**: Independently deployable units with execution lifecycles; expose APIs
- **Linkable**: Reusable libraries/components; not directly exposed to consumers

## Part Hierarchy Levels

1. **Product/Service** -- Highest level; units of profit/loss with onboarding and billing
2. **Capability** -- Main customer interaction point; "provide the ability to do something"
3. **Feature** -- Configuration units under capabilities; enable version history. Features can be nested (a feature may contain child features), but there is no formal "sub-feature" level.

## Part Stages

| Group | Stages |
|-------|--------|
| Open | Ideation, Prioritized |
| In Progress | Design, Development, Testing |
| Deployed | Limited Availability, General Availability |
| Inactive | Deprecated, Won't Do |

## Stock Fields
Type, Owner, Stage, Created/Modified dates, Tags, Release notes, Customer impact, Target dates.

## Key behaviors
- **CRUD**: Create, get, list, update, delete parts
- **Type mutation**: Promote parts between types (e.g., enhancement to capability) via `parts.mutate` with `type: promote`
- **Enhancement-specific fields**: target_close_date, target_start_date, release_notes, health (enum: On Track = 1)
- **Artifacts management**: Update part artifacts with `artifacts.set` (empty array clears all)
- **Nullable-unset pattern**: Sending `null` for target_close_date/target_start_date removes those values via UnsetFieldMask
- **Response schema**: Required fields include id, type, name, category (rev_part), created_by, modified_by, created_date, modified_date, owned_by, custom_fields
- **Counting and grouping**: Count and group parts with filters
- **Listing**: List parts with pagination

## Trails Features
- **Sort/filter**: By columns including owner, stage, created/modified dates
- **Search navigation**: Global and localized search access
- **Rich nodes**: Display owner and stage information
- **Link management**: Connect parts, enhancements, top contributors/supporters/customers

## Entry points
- **Base URL**: `https://api.devrev.ai/internal/`
- Namespace: `parts.*`
- Requires `Authorization: Bearer $TOKEN`

## API endpoints

| Endpoint | Methods | Description |
|----------|---------|-------------|
| `parts.create` | POST | Create part |
| `parts.get` | POST | Get part by ID |
| `parts.list` | GET, POST | List parts |
| `parts.update` | POST | Update part fields |
| `parts.delete` | POST | Delete part |
| `parts.mutate` | POST | Mutate/promote part type |
| `parts.count` | GET, POST | Count parts |
| `parts.group` | GET, POST | Group parts |

## Related flows
- [gap] Product hierarchy management flow
- [gap] Enhancement lifecycle (create, track, promote) flow

## Related scenarios
- [gap] Scenarios to be created from 180 test cases

## Open questions
- [gap] Can parts be demoted (capability back to enhancement)?
- [gap] How does the health enum map (what values beyond 1 = On Track)?
- [gap] What custom fields are available for parts beyond stock fields?
