---
title: Permissions
type: developer-doc
status: stable
source: developer.devrev.ai
category: airsync
source_url: https://developer.devrev.ai/airsync/data-model/permissions
last_updated: 2026-05-11
summary: "DevRev uses the concept of permissions to control access to records."
---

# Permissions

Data model

# Permissions

DevRev uses the concept of permissions to control access to records.
Permissions are associated with users or groups and define the level of access they have to leaf types and their fields.
You can read more about permissions in the [access control documentation](https://support.devrev.ai/devrev/article/ART-21834).

## [Groups](#groups)

To make groups available in the DevRev platform, AirSync expects two objects:

1. An object containing descriptions of groups available in the external system.

* Maps to the `group` object in DevRev.

2. An object containing a mapping between groups and users in the external system.

* Maps to the `object_member` object in DevRev.

### [Group memberships](#group-memberships)

An object containing the mapping between groups and users in the external system is required to represent group memberships in DevRev.

* This object maps to the `object_member` object in DevRev.
* It should contain a field that references a group.
  This field should be mapped to `object_id` field of the `object_member` object.
* It should also contain a collection field that references the users belonging to that group.
  This field should be mapped to the `add_member_ids` field.
* If the external system supports event-based updates for group membership changes, the `object_member` object should include an additional collection field.
  This field identifies users to be removed from the group and should be mapped to the `remove_member_ids` field.

## [Platform groups](#platform-groups)

Platform groups are automatically created by the DevRev platform for every organization.
For example, DevRev provides *Dev users* and *Rev users* groups that contain all Dev and Rev users respectively.

Developers and end-users can map external default groups to platform groups.
This functionality allows flexible integration with DevRev's permission system while enabling re-mapping by the end user.

To implement this mapping:

1. Define a new object in external domain metadata with one enum field containing possible values of default groups available in the external system.
2. During initial domain mapping, map this object to the *platform groups* object in DevRev.
3. Reference your object in other fields, such as in the `shared_with` field of articles.

## [Shared with field](#shared-with-field)

The `shared_with` field enables you to define permissions for articles (and other objects in the future).
It specifies both who can access the content and what permission level they have.
This field utilizes the `permission` type to associate users or groups with their designated roles.

### [Structure](#structure)

Each entry in the `shared_with` collection contains two key components:

* `member_id`: Identifies which user or group is being granted access.
* `role`: Specifies the permission level (for example, "viewer", "editor", "owner"). DevRev offers a set of predefined roles.

### [Member types](#member-types)

The `member_id` field can reference three different types of objects:

* Individual users (`#record:users`)
* Standard groups (`#record:groups`)
* Platform groups (`#record:platform_groups`)

### [External metadata example](#external-metadata-example)

```
{
  "shared_with": {
    "type": "permission",
    "collection": {},
    "permission": {
      "role": {
        "values": [
          {
            "key": "owner",
            "name": "Owner"
          },
          {
            "key": "editor",
            "name": "Editor"
          },
          {
            "key": "viewer",
            "name": "Viewer"
          }
        ]
      },
      "member_id": {
        "refers_to": {
          "#record:users": {},
          "#record:groups": {},
          "#record:platform_groups": {}
        }
      }
    }
  }
}
```

## [Article permissions](#article-permissions)

Articles in DevRev can be shared with individual users or groups, allowing for granular control over who can access what content.

### [Sharing mechanism](#sharing-mechanism)

The `shared_with` field specifies the permission level for each user or group using the `permission` type.
This type is a structure that connects a reference to a user-like record type (the `member_id` field)
with an `enum` value that defines the user's role or permission level.

### [Scope interaction](#scope-interaction)

For `scope=internal` articles:

* By default, only the owner has access.
* Additional access is granted exclusively through the `shared_with` field.

For `scope=external` articles, the expected behavior is that they are published to Portal/Plug and shared with customers.

* By default:
  + Admins have CRUD (create, read, update, delete) rights.
  + Platform users have CRU (create, read, update) rights.
* Additional rights can be assigned by creating roles and assigning them to the entire organization or specific groups.
* Articles can be shared with customers and published to Portal/Plug.

---

## [Authorization policy](#authorization-policy)

The authorization policy object provides a scalable way to manage both object-level, field-level and conditional permissions.
When importing an authorization policy object, DevRev automatically translates it into its own access control model.
It creates the necessary roles, role sets, and access control entries (ACEs) to enforce the permissions you've defined.
This allows you to mirror complex permission schemes from external systems within DevRev.

Only 1-way sync (from the external system to DevRev) is supported for the authorization policy.

### [Object structure](#object-structure)

The authorization policy object consists of four main fields:

* `users` (optional): A list of user identifiers to whom this policy applies.
* `groups` (optional): A list of group identifiers to whom this policy applies.
* `object_access` (optional): Defines object-level CRUD (Create, Read, Update, Delete) permissions for specified record types.
* `field_access` (optional): Defines field-level read and write permissions for specified record types.
* `conditional_access` (optional): Defines object-level or field-level conditional permissions for specified record types.

Although all of the fields are defined as optional at least one of `object_access`, `field_access` and `conditional_access` needs to be provided, together with at least one of `users` or `groups`.

#### [Object-level permissions](#object-level-permissions)

The `object_access` array defines which privileges (`create`, `read`, `update`, `delete`) are granted for which record types.
Multiple record types can be grouped under the same set of privileges.

#### [Field-level permissions](#field-level-permissions)

The `field_access` array allows for more granular control. For each record type, you can specify:

* `record_type`: The record type to which the field access applies.
* `read_all_fields`: A boolean to grant read access to all fields.
* `write_all_fields`: A boolean to grant write access to all fields.
* `read_fields`: A list of specific fields that can be read if `read_all_fields` is false.
* `write_fields`: A list of specific fields that can be written if `write_all_fields` is false.

This provides fine-grained control over data visibility and modification within a record.

#### [Conditional permissions](#conditional-permissions)

The `conditional_access` array allows providing object-level or field-level permissions for the listed record types, which are granted only if the defined conditions are met.
When using these, you must provide one of:

* `object_privileges`: The list of privileges granted for the provided record\_type. Uses the same CRUD values as defined in [object-level permissions](#object-level-permissions).
* `field_privileges`: Fine-grained privilages granted for fields inside the provided record\_type. The structure of the field mimcs the one used for [field-level permissions](#field-level-permissions).

together with:

* `record_type`: The record type to which the conditional access applies.

Alongside that, you need to define:

* `scope_to_users_in`: Array of fields on the target object that the user has to be present in, in order to be granted the defined privilages. The array represents a conjuction, meaning that the privileges are granted only if the user is present in all of the listed fields. Mutually exclusive with the `field_caveats` field.
* `field_caveats`: Array of conditions that need to be met for the user to be granted the defined privilages. The array represents a conjuction, meaning that the privileges are granted only if all of the listed conditions are met. Mutually exclusive with the `scope_to_users_in` field.

The structure of the field caveats is as follows:

* `field`: the key of the target record field that is being checked against.
* `operator`: enum of *eq*, *not\_eq*, *in* and *intersects*
* `value`: the value that the fields needs to have for the condition to be true. Its type needs to match the type of the `field`. The exception being when using the *in* operator, in which the field type is persumed to be a scalar while the value is an array.

### [External domain metadata](#external-domain-metadata)

This is an example of how to define the authorization policy object in your external domain metadata.
This structure defines the fields for `object_access`,`field_access` and `conditional_access` linking them to specific record types. You only need to define the fields (access type) that you intend to use.

```
"<external_record_type_name>": {
  "name": "Authorization Policy",
  "fields": {
    "groups": {
      "name": "Groups",
      "type": "reference",
      "collection": {},
      "reference": { "refers_to": { "#record:groups": {} } }
    },
     "users": {
      "name": "Users",
      "type": "reference",
      "collection": {},
      "reference": { "refers_to": { "#record:users": {} } }
    },
    "object_access": {
      "name": "Object access",
      "type": "record_type_privilege",
      "is_required": true,
      "collection": {},
      "record_type_privilege": { "type_keys": ["#category:issues", "#record:ext_bug"] }
    },
    "field_access": {
      "name": "Field access",
      "type": "field_privileges",
      "collection": {},
      "field_privileges": { "type_keys": ["#category:issues", "#record:ext_bug"] }
    },
    "conditional_access": {
        "name": "Conditional access",
        "type": "conditional_privileges",
        "collection": {},
        "conditional_privileges": {"type_keys": ["#category:issues", "#record:ext_bug"] }
    }
  },
  "is_snapshot": true
}
```

The `object_access`, `field_access` and `conditional_access` fields use `type_keys` to define which record types or categories the authorization policy applies to. Use these prefixes:

* `#record:` for specific record types (example: `#record:document`)
* `#category:` for record type categories (example: `#category:users`)

Authorization policies must always represent the current state of the external system. In each sync run, the entire policy should be provided.
If there were no changes since the last sync, the policy should not be provided.
The object must be marked as `is_snapshot: true` in the external domain metadata.

### [Extracted data file](#extracted-data-file)

During an import, the extracted data file must follow the structure defined in the metadata.
This file contains the actual users, groups, and permission rules to be applied in DevRev.

```
{
  "users": [
    "ext_user-1",
    "ext_user-2"
  ],
  "groups": [
    "ext_group-1",
    "ext_default_group"
  ],
  "object_access": [
    {
      "record_types": ["ext_bug", "ext_task"],
      "privileges": ["create", "read", "update", "delete"]
    },
    {
      "record_types": ["ext_todo", "ext_iss"],
      "privileges": ["create", "read"]
    }
  ],
  "field_access": [
    {
      "record_type": "ext_bug",
      "read_all_fields": false,
      "write_all_fields": false,
      "read_fields": ["ext_field1", "field2"],
      "write_fields": ["ext_field3", "field4"]
    },
    {
      "record_type": "ext_task",
      "read_all_fields": false,
      "write_all_fields": true,
      "write_fields": ["ext_field1", "field2"]
    }
  ],
  "conditional_access": [
    {
      "record_type": "ext_bug",
      "field_privileges": {
        "write_fields": ["ext_field1"],
        "read_all_fields": true,
      },
      "scope_to_users_in": ["ext_field5"]
    },
    {
      "record_type": "ext_iss",
      "object_privileges": ["read", "update"],
      "field_caveats": [
        {
          "operator": "eq",
          "field:" "ext_field6",
          "value" true
        }
      ]
    }
  ]
}
```

Please check the detailed example on how to define and provide the authorization policy objects at [Permissions example](https://developer.devrev.ai/airsync/data-model/permissions-example).

Last updated on

[Rich text fields

Previous Page](/airsync/data-model/rich-text-fields)[Permissions example

Next Page](/airsync/data-model/permissions-example)

## Source
- DevRev developer docs: [Permissions](https://developer.devrev.ai/airsync/data-model/permissions)
