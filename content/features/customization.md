---
title: Customization
type: feature
status: draft
sources: [raw/test-cases/by-feature/fe_customization.jsonl, raw/docs/devrev-developer-docs.md, raw/docs/devrev-docs-scraped.md, raw/docs/devrev-agent-dump-settings.md]
related: [[entities/ticket]], [[entities/issue]]
last_updated: 2026-04-12
---

# Customization

## What it does
The Customization feature manages approval configurations and approval tracking within DevRev. It provides CRUD operations for approval configs (multi-phase approval workflows with conditions and approvers) and tracker management for monitoring approval progress. With 80 test cases, this feature enables organizations to define custom approval processes for different object types. The backend service is `us_schemaregistry`.

## Why it exists
Organizations need configurable approval workflows to enforce governance policies. Whether it's requiring manager approval for ticket escalations or multi-stakeholder sign-off for feature releases, the Customization feature provides the framework for defining and tracking these approval processes.

## Key behaviors
- **Approval configs**: CRUD with DSL-based filtering (`["eq", "$leaf_type", "issue"]` format)
- **Leaf type targeting**: Configs apply to specific object types (e.g., `issue`)
- **Multi-phase approvals**: Each config has phases with id (integer), approval_type (one/all), approvers (array), and condition
- **Pagination**: Default 50 per page; supports limit parameter and cursor-based pagination (next_cursor, prev_cursor)
- **Immediate consistency**: Newly created configs are immediately retrievable via get
- **DON format IDs**: Config IDs follow `don:core:dvrv-us-1:devo/{org}:approval_config/{n}` pattern
- **Approval trackers**: List and get trackers to monitor approval flow progress

## Entry points
- **Base URL**: `https://api.devrev.ai/internal/`
- Namespace: `approvals.*`
- Requires `Authorization: Bearer $TOKEN`

## API endpoints

| Endpoint | Methods | Description |
|----------|---------|-------------|
| `approvals.configs.get` | GET, POST | Get approval config |
| `approvals.configs.list` | GET, POST | List approval configs |
| `approvals.trackers.list` | POST | List approval trackers |

## Related flows
- [gap] Approval config creation flow
- [gap] Multi-phase approval execution flow

## Related scenarios
- [gap] Scenarios to be created from 80 test cases

## Available Objects for Customization
The following objects support customization:
- Issues
- Tickets
- Opportunities
- Accounts
- Contacts
- Parts

## Key Capabilities
- **Create custom object records:** Generate records from the plus button
- **Search capability:** Cmd+K shortcut provides quick access to custom object records
- **Association mapping:** Custom objects can link to stock objects (tickets, contacts) and other custom objects

## Access and Permissions
Only workspace administrators can add custom fields. Organization members can view custom fields and subtypes but cannot modify them.

Navigate to **Settings > Object customization** to view existing objects, subtypes, and deprecated objects.

## Custom Field Types

| Type | Description |
|------|-------------|
| Text | Unformatted text input |
| Rich text | Formatted text with styling capabilities |
| Number | Numeric values |
| Double | Decimal numbers |
| Boolean | Toggle (0 or 1) |
| Dropdown | Predefined options |
| Timestamp | Date and time |
| Date | Date selection only |
| Part | Link to part records |
| Dev user | User selection |
| Customer | Customer workspace assignment |
| Account | Customer account assignment |
| Workspace | Workspace assignment |

## Adding Custom Fields
1. Select the target object or subtype
2. Click **+ New field** to enter edit mode
3. Complete field configuration details
4. Click **Save to draft**
5. Review and publish changes

### Field Configuration Options
- **Allow multiple values:** Enable multiple entries
- **Required field:** Mark as mandatory (displays red star)
- **Default value:** Preset value for new records
- **Placeholder text:** Hint text for users
- **Group name:** Create accordion groupings
- **Field visibility:** Control user access to the field
- **Field actionables:** Enable grouping, filtering, and sorting capabilities
- **Tooltip:** Hover information for users
- **Description:** Internal notes (admin only)

## Managing Custom Fields
Click the three-dot icon next to the field name. Options: **Edit** (modify configuration) or **Delete** (remove permanently).

## Creating Subtypes

### Via UI
1. Click **+** on the right side of Objects
2. Provide name and description
3. Select parent object
4. Click **Proceed**
5. Click **Edit** to customize
6. Add required fields
7. Publish the subtype

### Via API
1. Call `POST /schemas.custom.set` with `type: "custom_type_fragment"`, `leaf_type`, `subtype` (internal name), `subtype_display_name`, and `fields`.
2. Create objects of that subtype by passing `custom_schema_spec: { subtype: "bug" }` in the create call.

### Subtype Deprecation
Click the three-dot icon next to **Edit**, then select **Deprecate subtype**.
- Existing linked instances remain unchanged but require subtype restoration to edit
- New instances cannot use deprecated subtypes
- Restore via **Show deprecated objects** > three-dot icon > **Restore subtype**

## Schema Fragments

Custom fields are defined as schema fragments that can be applied to object types and subtypes.

**Fragment types:**
- `tenant_fragment` -- Applies to **all records** of a given object type org-wide.
- `custom_type_fragment` -- Defines a **subtype** with its own specific fields.
- `app_fragment` -- Snap-in-specific fields; only shown when the snap-in is installed.

**How they work:**
- Fragments are **immutable**. Updating a fragment creates a new version chained to the old one.
- Objects referencing old fragments are **auto-upgraded in-memory** when read via API.
- **Bulk upgrade** -- `POST /internal/objects.bulk-upgrade` upgrades all objects of a given type to the latest fragment.
- **Deprecate** -- Set `is_deprecated: true` in the `schemas.custom.set` call to prevent new objects from using that subtype.

**Adding a custom field via API:**
1. Call `POST /schemas.custom.set` with `type: "tenant_fragment"` (for all records) or `type: "custom_type_fragment"` (for a subtype).
2. Specify `leaf_type` (e.g. `"issue"`), `fields` array with `name`, `field_type`, and optional `ui.display_name`.
3. Custom fields appear in the UI automatically. Tenant fields are prefixed `tnt__`; subtype fields are prefixed `ctype__`.

**Supported API custom field types:** `int`, `double`, `bool`, `tokens`, `text`, `rich_text`, `enum`, `timestamp`, `date`, `id` -- and list variants of all of these.

**UI hints for custom fields:** `display_name`, `is_hidden`, `placeholder`, `is_sortable`, `is_groupable`, `order`, `is_read_only`, `group_name`, `unit`.

**Objects supporting customization:** Issues, tickets, incidents, accounts, rev orgs, contacts, and custom objects.

## Stage Modification

### How to modify stages for an object type (API)
1. **Create custom stages** -- `POST /stages.custom.create` with `name`, `state` (open/in_progress/closed), and `ordinal`.
2. **Create a stage diagram** -- `POST /stage-diagrams.create` with `leaf_type`, `subtype`, and `stages` array defining allowed transitions and the start stage.
3. **Apply the diagram** -- Reference the `stage_diagram_id` in the subtype's `schemas.custom.set` call.

## Dependent Fields

Fields whose values depend on another field's value.

**Configuration:** Use `conditions` in the schema fragment to make fields required or visible based on stage or other field values.
- **Supported operators:** `==`, `!=`, `&&`, `||`
- **Supported effects:** `require`, `show`, `allowed_values`

## Open questions
- [gap] What leaf types support approval configs beyond `issue`?
- [gap] How does the `condition` field in phases work (what expressions are supported)?
- [gap] What triggers approval flow execution (automatic on state change or manual)?
