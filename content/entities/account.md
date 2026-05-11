---
title: Account
type: entity
status: stable
sources: [raw/docs/devrev-agent-dump-part2.md, https://support.devrev.ai/en-US/devrev/directories]
related: ["features/identity", "entities/ticket", "entities/rev-user"]
last_updated: 2026-05-11
support_articles: [ART-21879, ART-21882, ART-21921, ART-21923]
---

# Account

## Description
An account represents an external customer organization in DevRev. Accounts are the top-level entity in the [[grow-app]] (Computer for Growth Teams) for grouping contacts (rev users), tickets, and commercial data.

## Fields
- **Name** -- account name (required)
- **Description** -- free-text description
- **Domains** -- associated web domains for automatic contact matching
- **Tier** -- customer tier classification
- **Owner** -- internal dev user responsible for the account
- **External refs** -- references to the account in external systems (via Airdrop/AirSync)
- **ACV** -- Annual Contract Value (commerce details)
- **Phone numbers** -- contact phone numbers
- **Websites** -- associated URLs
- **SLA** -- assigned SLA policy
- **Environment** -- defaults to "production"

## Actions
- Create, get, update, delete accounts
- Merge accounts (combine duplicates)
- Detect, list, count, ignore duplicate accounts
- Export (sync and async)
- Sample CSV generation for bulk import
- Bulk CSV creation
- Get/list commerce details
- Get account SLA
- Group accounts

## Creation Methods
- Quick Create (`+` button or `Cmd+K`)
- API (`accounts.create`)
- Bulk CSV import (`accounts.create.bulk.csv`)
- Airdrop/AirSync import

## Relationships
- Contains [[entities/rev-user]] contacts
- Linked to [[entities/ticket]] objects
- SLA policies from [[features/slas]]
- Commerce details for licensing

## Support documentation

Referenced DevRev support articles synchronized from [support.devrev.ai](https://support.devrev.ai/en-US/devrev/directories):

- [[support-articles/computer-plus-support/account|Account]] (ART-21879) — [external](https://support.devrev.ai/en-US/devrev/article/x368dZAr)
- [[support-articles/computer-plus-support/account-and-contact-import|Account and contact import]] (ART-21882) — [external](https://support.devrev.ai/en-US/devrev/article/Ni6_K6iY)
- [[support-articles/snap-ins/account-deduplication|Account deduplication]] (ART-21921) — [external](https://support.devrev.ai/en-US/devrev/article/WY9H5fw_)
- [[support-articles/snap-ins/auto-link-devrev-github-accounts|Auto-link DevRev GitHub accounts]] (ART-21923) — [external](https://support.devrev.ai/en-US/devrev/article/lU6Qkrc-)
