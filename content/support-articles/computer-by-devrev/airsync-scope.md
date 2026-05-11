---
title: AirSync scope
devrev_id: ART-21892
parent_directory: AirSync
translation_group: Sxa3jlbn
modified_date: "2025-12-10T06:56:46.094Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/Sxa3jlbn"
tags: []
top_category: Computer by DevRev
wiki_match: glossary/airsync
match_score: 0.85
last_updated: 2026-05-11
related: ['glossary/airsync']
summary: "AirSync does its best to bring over as much data as possible as accurately as possible but there are some constraints due to data model or platform differences."
---

# AirSync scope

[[glossary/airsync|AirSync]] does its best to bring over as much data as possible as accurately as possible but there are some constraints due to data model or platform differences.
The following is a list of AirSync scopes and exclusions to keep in mind when performing an AirSync. These are generic restrictions that apply to all AirSync sources.

## Attachments

Attachments bigger than 250 MB are not transferred to DevRev.

Attachments of certain prohibited file types (for example binary/octet-stream) are not transferred to DevRev.

## Connection

All actions on the external source are performed by the user that established the connection in DevRev for that source.

## Data model constraints

Links

* Parent/child relationships deeper than 3 levels are not created in DevRev.
* Links from external systems are mapped to the closest equivalent in DevRev.
* Links with no plausible DevRev equivalent are dropped, such as links between [[features/tickets|tickets]].

Contacts

* DevRev does not support contacts in multiple [[features/accounts|accounts]]. Contacts imported that belong to multiple accounts are only created under one [[entities/account|account]] in DevRev, the relationship to other accounts is dropped.
* Contact changes of Account in an external system are not reflected in DevRev after the initial sync.
* Contacts have an external reference that may be populated by email or source ID. This is an internal mapping and may not show up in the Mappings page.

Account

* Accounts in DevRev have both **Websites** and **Domains** fields. Mapping from external source is typically done to DevRev's Websites field and then a stripped down version is added to the Domains field. This is an internal mapping and may not show up in the Mappings page.
* Accounts have an external reference that may be populated by domain(s) or source ID. This is an internal mapping and may not show up in the Mappings page.

## Dates

Creation and Modified dates of synced items will not match those of the source. Source creation and modified dates are preserved and available in DevRev in the field `external_source_data`.

## Deletion

Deletion of synced items is not propagated. This includes works ([[features/issues|issues]] or tickets), accounts, users, links, and other types. When an item is deleted (either in DevRev or at the source) and that item exists at the other end, it will not be deleted but no further updates to it will be made.

## References

In-text references (such as @mentions) will not be remapped.

## Schema changes

If a new record type is added to the external source after the initial sync, it will not be automatically picked up by AirSync.

## Updates

If an item is intentionally omitted from a sync and later updated to qualify for syncing, any attachments or comments added before the item is synced to DevRev will be omitted. This scenario often occurs when an item is excluded from syncing due to type or filter exclusions, and then its type or attributes are changed.

## Related wiki nodes
- [[glossary/airsync]]

## Source
- DevRev support [[entities/article|article]] [AirSync scope](https://support.devrev.ai/en-US/devrev/article/Sxa3jlbn) (ART-21892)
