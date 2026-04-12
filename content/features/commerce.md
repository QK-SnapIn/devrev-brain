---
title: Commerce
type: feature
status: draft
sources: [raw/test-cases/by-feature/fe_commerce.jsonl, raw/docs/devrev-developer-docs.md]
related: []
last_updated: 2026-04-12
---

# Commerce

## What it does
The Commerce feature manages SKUs (Stock Keeping Units), addon rules, and account commerce details within DevRev. It handles active SKU listing, addon rule management with associativity control (mandatory/optional), and commerce detail updates for accounts. With 80 test cases, this feature powers the commercial/billing aspects of DevRev. Backend services include `us_enact` and `us_commerceservice`.

## Why it exists
DevRev needs to manage its product catalog, pricing rules, and customer billing information. The Commerce feature provides the API layer for querying active SKUs, managing addon rules that govern how products can be bundled, and tracking commerce details per customer account.

## Key behaviors
- **Active SKUs**: List active SKUs; returns `skus` array (empty `[]` when no active SKUs, never null or absent)
- **Addon rules**: CRUD with filtering by DON IDs and associativity values (`mandatory`, `optional`)
- **Pagination**: Default limit 50; custom limit parameter; cursor-based pagination with next_cursor
- **Account commerce details**: Update commerce details for specific accounts
- **Safe-for-prod**: Most list/get operations are tagged safe-for-prod (read-only)

## Entry points
- **Base URL**: `https://api.devrev.ai/internal/`
- Namespaces: `active-skus.*`, `addon-rules.*`, `accounts.commerce-details.*`
- Requires `Authorization: Bearer $TOKEN`

## API endpoints

| Endpoint | Methods | Description |
|----------|---------|-------------|
| `active-skus.list` | GET, POST | List active SKUs |
| `addon-rules.list` | POST | List addon rules |
| `addon-rules.delete` | POST | Delete addon rule |
| `accounts.commerce-details.update` | POST | Update commerce details |

## Related flows
- [gap] Product catalog management flow
- [gap] Account billing configuration flow

## Related scenarios
- [gap] Scenarios to be created from 80 test cases

## Open questions
- [gap] What SKU attributes are available (pricing, limits, etc.)?
- [gap] What is the full addon rule structure beyond associativity?
- [gap] How do addon rules relate to SKUs and account subscriptions?
- [gap] What commerce details can be set per account?
