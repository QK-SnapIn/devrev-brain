---
title: Accounts
type: feature
status: draft
sources: [raw/test-cases/by-feature/fe_accounts.jsonl, raw/docs/devrev-developer-docs.md]
related: []
last_updated: 2026-04-12
---

# Accounts

## What it does
The Accounts feature manages customer account objects within DevRev, providing update operations, duplicate detection, and CSV sample generation. With 50 test cases, this feature focuses on account data management including comprehensive field updates, duplicate pair discovery, and data import support. Backend services include `us_janus` and `us_janus2`.

## Why it exists
Part of the [[grow-app]] (Computer for Growth Teams), customer accounts are central to DevRev's CRM capabilities. Organizations need to maintain accurate account records with details like domains, websites, environments, tiers, phone numbers, and descriptions. Duplicate detection helps maintain data quality, and CSV support enables bulk data operations.

## Key behaviors
- **Account updates**: Update display_name, description, domains, websites (set array), environment, tier, phone_numbers
- **No-op updates**: Sending only the `id` field returns 200 OK with the account unchanged
- **Duplicate detection**: List duplicate account pairs with required fields: account1, account2, created_by, created_date, modified_by, modified_date
- **Duplicate pair structure**: account1/account2 are `account-summary` objects with id field; created_by/modified_by are `user-summary` objects
- **Sample CSV**: Generate sample CSV for account imports with strict schema conformance
- **Pagination**: Duplicate listing supports limit parameter

## Entry points
- **Base URL**: `https://api.devrev.ai/internal/`
- Namespace: `accounts.*`
- Requires `Authorization: Bearer $TOKEN`

## API endpoints

| Endpoint | Methods | Description |
|----------|---------|-------------|
| `accounts.update` | POST | Update account fields |
| `accounts.duplicates.list` | POST | List duplicate account pairs |
| `accounts.sample-csv.get` | GET | Get sample CSV template |

## Related flows
- [gap] Account creation and onboarding flow
- [gap] Duplicate account resolution flow
- [gap] Bulk account import via CSV flow

## Related scenarios
- [gap] Scenarios to be created from 50 test cases

## Open questions
- [gap] What are all valid environment values (production, staging, ...)?
- [gap] What are all valid tier values (tier_1, ...)?
- [gap] How does duplicate detection work (what fields are compared)?
- [gap] What is the full sample CSV schema for account imports?
