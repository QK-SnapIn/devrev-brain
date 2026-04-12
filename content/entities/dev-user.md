---
title: Dev User
type: entity
status: stable
sources: [raw/docs/devrev-agent-dump-part2.md]
related: [[features/identity]], [[entities/group]]
last_updated: 2026-04-12
---

# Dev User

## Description
A Dev User (devu) is an internal team member with access to the DevRev application. Dev users build, manage, and operate the product.

## Types

| Type | Description |
|------|-------------|
| Regular | Standard internal team member with full app access |
| Service Account | Programmatic access for integrations; no interactive login |
| System User | DevRev Bot; performs automated actions on behalf of the system |
| Shadow User | No app access; created by AirSync for tracking external user activity |

## Fields
[gap] Full field list not enumerated in source. Known fields: id, email, display name, phone number, identities (external links), licenses, highlights, status (active/deactivated).

## Key Operations
- Full CRUD with activate/deactivate
- Bulk license updates
- Merge capabilities
- Email updates, phone number verification (send-code/check-code)
- Identity linking (link/unlink external identities)
- Self-service: self-read, self-update, self-delete, post-login hooks, logout
- Async export

## Relationships
- Assigned to [[entities/group]] objects (which carry roles)
- Owns [[entities/ticket]], [[entities/issue]], [[entities/account]] objects
- Authenticated via PAT, AAT, or session tokens
