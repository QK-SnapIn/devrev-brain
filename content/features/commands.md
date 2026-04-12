---
title: Commands
type: feature
status: draft
sources: [raw/test-cases/by-feature/fe_commands.jsonl, raw/docs/devrev-developer-docs.md]
related: []
last_updated: 2026-04-12
---

# Commands

## What it does
The Commands feature enables creation and management of custom commands within DevRev. Commands are executable actions that belong to namespaces, have statuses (enabled, disabled, draft), and use different executor types (workflow, rego). With 131 test cases, this feature supports the full command lifecycle: create, get, list, update, delete, and execute. The backend service is `us_blubox`.

## Why it exists
DevRev allows organizations to extend platform functionality through custom commands. These commands can automate workflows, enforce policies (via Rego rules), or trigger custom business logic. The command system provides a way to register, manage, and execute these extensibility points.

## Key behaviors
- **Command CRUD**: Create, get, list, update, delete commands
- **Command execution**: Execute commands on demand
- **Namespacing**: Commands belong to namespaces (e.g., `devrev`); can filter by namespace
- **Status management**: Commands have statuses: `enabled`, `disabled`, `draft`; can filter list by status
- **Executor types**: `workflow` and `rego` executor types; can filter by executor_type
- **Idempotency**: Deleting an already-deleted command returns 404 (not idempotent)
- **Error messages**: 404 responses include descriptive `not found` error messages

## Entry points
- **Base URL**: `https://api.devrev.ai/internal/`
- Namespace: `commands.*`
- Requires `Authorization: Bearer $TOKEN` (admin level)

## API endpoints

| Endpoint | Methods | Description |
|----------|---------|-------------|
| `commands.create` | POST | Create a command |
| `commands.get` | GET | Get command by ID |
| `commands.list` | GET, POST | List commands with filters |
| `commands.update` | POST | Update command properties |
| `commands.delete` | POST | Delete a command |
| `commands.execute` | POST | Execute a command |

## Related flows
- [gap] Command authoring and testing flow
- [gap] Workflow command execution flow

## Related scenarios
- [gap] Scenarios to be created from 131 test cases

## Open questions
- [gap] What is the full structure of a command's `action` object?
- [gap] How do Rego-based commands differ from workflow commands in execution?
- [gap] What permissions are required to create vs execute commands?
- [gap] Are there built-in commands or only user-defined ones?
