---
title: Rev User
type: entity
status: stable
sources: [raw/docs/devrev-agent-dump-part2.md]
related: ["features/identity", "entities/account"]
last_updated: 2026-04-12
---

# Rev User

## Description
A Rev User (revu) is an external customer or contact. Rev users interact with DevRev via the Support widget (PLuG SDK), customer portals, email, and conversations. They do not have access to the internal DevRev app.

## Fields
[gap] Full field list not enumerated in source. Known fields: id, email, display name, account, lifecycle stage.

## Lifecycle Stages

| Code | Stage |
|------|-------|
| 0 | New |
| 1 | Shortlisted |
| 2 | Prospecting |
| 3 | Engaged |
| 4 | Opportunity in Progress |
| 5 | Return to Nurture |
| 6 | Qualified Out |

## Access Behavior
- When a rev user calls `conversations.count`, the `owned_by` filter is silently ignored and replaced with `MemberIds: [rev_user_don]` -- rev users can only count their own conversations.
- Rev users interact via [[glossary/plug]] widget and customer portal.
- Customer roles are managed under Settings > Customer Management > Roles.

## Relationships
- Belongs to [[entities/account]]
- Reports [[entities/ticket]] objects
- Participates in [[entities/conversation]] objects
