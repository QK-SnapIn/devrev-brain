---
title: Group
type: entity
status: stable
sources: [raw/docs/devrev-agent-dump-part2.md, https://support.devrev.ai/en-US/devrev/directories]
related: ["features/identity", "features/mfz", "entities/dev-user"]
last_updated: 2026-05-11
support_articles: [ART-21893, ART-21950, ART-21962]
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

## Support documentation

Referenced DevRev support articles synchronized from [support.devrev.ai](https://support.devrev.ai/en-US/devrev/directories):

- [[support-articles/computer-by-devrev/groups|Groups]] (ART-21893) — [external](https://support.devrev.ai/en-US/devrev/article/s1klL8Gq)
- [[support-articles/snap-ins/set-user-preference-for-group|Set user preference for group]] (ART-21950) — [external](https://support.devrev.ai/en-US/devrev/article/yk5Vj8U0)
- [[support-articles/snap-ins/user-group-validator|User group validator]] (ART-21962) — [external](https://support.devrev.ai/en-US/devrev/article/ZopEMXVg)
