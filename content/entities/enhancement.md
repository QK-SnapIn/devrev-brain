---
title: Enhancement
type: entity
status: stable
sources: [raw/docs/devrev-agent-dump-part2.md]
related: ["features/stock-objects", "entities/issue", "features/parts"]
last_updated: 2026-04-12
---

# Enhancement

## Description
An enhancement represents a product improvement request or feature idea. Enhancements sit in the product hierarchy and link to issues (development work) and parts (product structure).

## Stages

| Group | Stage |
|-------|-------|
| Open | Ideation, Prioritized |
| In Progress | UX Design, In Development, In Testing |
| Released | Limited Availability, General Availability |
| Closed | Deprecated, Won't Do, Deprioritized |

## Relationship to Issues and Parts
- Enhancements belong to a Part in the product hierarchy (Product -> Capability -> Feature).
- Development work for an enhancement is tracked via linked [[entities/issue]] objects.
- Enhancement stage progression (e.g., to Released) may trigger updates on linked issues and tickets.

## Fields
[gap] Full field list not enumerated in source. Known fields: Title, Description, Stage, Part, Owner, Priority, Tags.

## Creation Methods
- Quick Create (`+` button or `Cmd+K`)
- API (`works.create` with enhancement type, or dedicated enhancement endpoints)
- Workflow action (`UpdateEnhancement`)
- Airdrop/AirSync import
