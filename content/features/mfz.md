---
title: MFZ (Multi-Functional Zones)
type: feature
status: draft
sources: [raw/test-cases/by-feature/fe_mfz.jsonl, raw/docs/devrev-developer-docs.md]
related: []
last_updated: 2026-04-12
---

# MFZ (Multi-Functional Zones)

## What it does
MFZ manages groups, role sets, roles, and access control entries within DevRev. It provides group management (list, count, list members), role set CRUD (create, get, list, update, delete, count, apply, UI config), role CRUD (create, delete, list), and access control entries (list with combined filters). With 274 test cases, this feature handles the organizational structure and permission boundaries that define how users are grouped and what they can access. The backend service is `us_mfzclient`.

## Why it exists
In multi-tenant environments, organizations need to define functional zones -- logical groupings of users with specific roles and permissions. MFZ provides this structure so that access control policies can be applied at the group level rather than per-user, enabling scalable permission management.

## Key behaviors
- **Groups**: List all groups, count members, list members with required fields (id, display_name, created_date, modified_date)
- **Role sets**: Full CRUD with count; apply role sets to entities; retrieve UI-specific config; required fields include id, name, is_default, applicable_principal_type
- **Roles**: Create, delete, list roles within the MFZ context
- **Access control entries**: List with combined filtering by principal and principal_type; supports pagination with limit parameter
- **Safe-for-prod**: Most test cases are tagged `safe-for-prod`, indicating read-only or low-risk operations

## Entry points
- **Base URL**: `https://api.devrev.ai/internal/`
- Endpoints: `groups.*`, `role-sets.*`, `roles.*`, `access-control-entries.*`
- Requires `Authorization: Bearer $TOKEN`

## API endpoints

| Endpoint | Methods | Description |
|----------|---------|-------------|
| `groups.list` | GET | List all groups |
| `groups.members.count` | GET | Count group members |
| `groups.members.list` | GET | List group members |
| `role-sets.create` | POST | Create role set |
| `role-sets.get` | GET, POST | Get role set |
| `role-sets.list` | GET, POST | List role sets |
| `role-sets.update` | POST | Update role set |
| `role-sets.delete` | POST | Delete role set |
| `role-sets.count` | POST | Count role sets |
| `role-sets.apply` | POST | Apply role set |
| `role-sets.ui-config.get` | GET | Get UI config for role sets |
| `roles.create` | POST | Create role |
| `roles.delete` | POST | Delete role |
| `roles.list` | POST | List roles |
| `access-control-entries.list` | GET | List access control entries |

## Related flows
- [gap] Group management and membership flow
- [gap] Role assignment and permission resolution flow

## Related scenarios
- [gap] Scenarios to be created from 274 test cases

## Open questions
- [gap] What does "MFZ" stand for exactly and what are the "zones"?
- [gap] How do role sets differ from individual roles?
- [gap] What is `applicable_principal_type` and what values can it take?
- [gap] How does the UI config endpoint drive the frontend role management interface?
