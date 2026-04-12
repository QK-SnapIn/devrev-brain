---
title: Search
type: feature
status: draft
sources: [raw/docs/devrev-docs-scraped.md, raw/docs/devrev-agent-dump-part1.md]
related: [[features/vistas]]
last_updated: 2026-04-12
---

# Search

## What it does
DevRev's global search enables seamless navigation across issues, tickets, articles, customers, and more, with timeline comment searching capabilities.

## Why it exists
Users need fast access to any object in the system without navigating through menus. Search provides instant access via keyboard shortcut and supports complex query syntax for power users.

## Access Methods
- **Mac:** Cmd + K
- **Windows:** Ctrl + K
- **Click "Search"** in left navigation

## Search Interface
- Toggle between standard and expanded views
- Click comments to navigate to specific objects
- Display up to two relevant comments per object with author, timestamp, and text
- Recent records shown by default

## Query Syntax
Search queries follow this structure: `[operator]* [field]* [term/phrase]*`

Components include filtering via operators/fields and full-text search across object text fields.

## Operators

| Operator | Function | Example |
|----------|----------|---------|
| `in:<body/title>` | Search within ticket/issue content | `in:title crm` |
| `type:<object>` | Filter by object type | `type:issue` |
| `-` | Exclude results | `type:issue -crm` |
| `state` | Filter by stage | `state:open` |
| `severity` | Filter by level | `severity:high` |

### Searchable Object Types
issue, enhancement, ticket, revu, question_answer, conversation, article, devu, account, feature, runnable

## Field Types & Syntax
- **Boolean:** `<field>:true` or `<field>:1`
- **Numeric:** `<field>:<v>`, `<field>:<<v>`, `<field>:v1..v2`
- **String:** `<field>:<v>`
- **Date:** `<field>:<v>`, `<field>:<=<v>`, `<field>:v1..v2`
- **Array:** CSV comma-separated values with "any match" logic

## Custom Searches
- **Custom Fields:** Use standard syntax; subtype-specific fields require: `subtype:<name> <field>:<value>`
- **Custom Objects:** Add `leaf_type:` filter (e.g., `leaf_type:book author:"Chip Huyen" AI agents`)

## Entry points
- Global search bar (Cmd+K / Ctrl+K)
- "Search" in left navigation

## Related flows
- [gap] Search-driven triage flow

## Related scenarios
- [gap] Scenarios to be defined

## Open questions
- [gap] What are the exact match rules vs fuzzy matching?
- [gap] Are there search result limits or pagination?
