---
title: Group
type: entity
status: stable
sources: [raw/docs/devrev-agent-dump-part2.md]
related: [[features/identity]], [[features/mfz]], [[entities/dev-user]]
last_updated: 2026-04-12
---

# Group

## Description
A group is a collection of users that can be assigned roles. Groups are the primary mechanism for RBAC in DevRev -- users are assigned to groups, and groups carry role assignments.

## Default Groups
[gap] Exact list of default groups not documented in source. Groups are managed under Settings > User Management > Groups.

## How Groups Relate to Roles
- **Roles** = sets of privileges (permissions) on objects.
- **Groups** = collections of users assigned roles.
- Users are assigned to Groups (not directly to roles).
- Highest privilege wins when a user belongs to multiple groups.
- Supports field-level access control and condition-based restrictions.

## Customer Groups
Separate from dev user groups. Managed under Settings > Customer Management > Roles. Customer roles are assigned to customer groups or individual customers.

## Fields
[gap] Full field list not documented. Known fields: id, name, members, roles.

## Relationships
- Contains [[entities/dev-user]] or [[entities/rev-user]] members
- Carries role assignments from [[features/identity]]
- Referenced by [[features/knowledge-base]] for article sharing
