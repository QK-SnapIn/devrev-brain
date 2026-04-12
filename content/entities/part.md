---
title: Part
type: entity
status: stable
sources: [raw/docs/devrev-docs-scraped.md, raw/docs/devrev-agent-dump-part1.md]
related: ["features/parts", "glossary/trails", "entities/issue", "entities/ticket", "entities/enhancement"]
last_updated: 2026-04-12
---

# Part

## Description
A Part is a product/service component with a lifecycle (creation, operation, evolution, deprecation). Parts form recursive hierarchies representing the product structure. Events and work items must be related to parts. Parts are visualized in **Trails** ([[glossary/trails]]) -- an interactive product hierarchy view.

## Two Part Categories

**Customer parts** represent how products are consumed externally -- like APIs or features customers interact with.

**Builder parts** are internal components:
- **Runnable**: Independently deployable units with execution lifecycles; expose APIs
- **Linkable**: Reusable libraries/components; not directly exposed to consumers

## Hierarchy Levels

| Level | Description |
|-------|-------------|
| Product/Service | Highest level; units of profit/loss with onboarding and billing |
| Capability | Main customer interaction point; "provide the ability to do something" |
| Feature | Configuration units under capabilities; enable version history. Features can be nested (a feature may contain child features), but there is no formal "sub-feature" level. |

## Stages

| Group | Stage |
|-------|-------|
| Open | Ideation, Prioritized |
| In Progress | Design, Development, Testing |
| Deployed | Limited Availability, General Availability |
| Inactive | Deprecated, Won't Do |

## Stock Fields
- Type
- Owner
- Stage
- Created date / Modified date
- Tags
- Release notes
- Customer impact
- Target dates

## Trails Features
Trails is the extensible interface for viewing and managing the part hierarchy:
- **Sort/filter**: By columns including owner, stage, created/modified dates
- **Search navigation**: Global and localized search access
- **Rich nodes**: Display owner and stage information
- **Link management**: Connect parts, enhancements, top contributors/supporters/customers

## Relationships
- Parts link to [[entities/issue]] (work items)
- Parts link to [[entities/ticket]] (customer requests)
- Parts link to [[entities/enhancement]] (product improvements)
- Parts link to customer data (accounts, revenue)
- Parts can be parents/children of other parts (recursive hierarchy)

## Actions
- Create, get, list, update, delete parts
- Mutate/promote part type (e.g., feature to capability)
- Count and group parts with filters
