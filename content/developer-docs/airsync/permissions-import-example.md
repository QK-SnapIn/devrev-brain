---
title: Permissions import example
type: developer-doc
status: stable
source: developer.devrev.ai
category: airsync
source_url: https://developer.devrev.ai/airsync/data-model/permissions-example
last_updated: 2026-05-11
summary: "This represents an example of how you can extract and map permissions using the Authorization policy object."
---

# Permissions import example

Data model

# Permissions import example

This represents an example of how you can extract and map permissions using the [Authorization policy object](/airsync/data-model/permissions#authorization-policy).

## [External domain metadata definition](#external-domain-metadata-definition)

Assume the following domain metadata definition, with the focus being on the `access_rules` record type which represents the permissions in our system.

```
{
  "access_rules": {
    "fields": {
      "conditional_permissions": {
        "type": "conditional_privilege",
        "collection": {},
        "conditional_privilege": {
          "type_keys": [
            "#record:accounts"
          ]
        }
      },
      "field_level_permissions": {
        "type": "field_privilege",
        "collection": {},
        "field_privilege": {
          "type_keys": [
            "#record:opportunities"
          ]
        }
      },
      "object_level_permissions": {
        "type": "record_type_privilege",
        "collection": {},
        "record_type_privilege": {
          "type_keys": [
            "#record:cases",
            "#record:contacts",
            "#record:accounts"
          ]
        }
      },
      "permission_groups": {
        "type": "reference",
        "collection": {},
        "reference": {
          "refers_to": {
            "#record:groups": {}
          }
        }
      },
      "permission_users": {
        "type": "reference",
        "collection": {},
        "reference": {
          "refers_to": {
            "#record:users": {},
            "#record:contacts": {}
          }
        }
      }
    },
    "is_snapshot": true
  },
  "cases": {...},
  "accounts": {...},
  "opportunities": {...},
  "users": {...},
  "contacts": {...}
}
```

The `is_snapshot` property on `access_rules` is used to signal that the record type always represents the current state of the external system. This means that if they are being extracted and provided to the AirSync platform in a sync run, the provided items define the entirety of the permission rules to import. Only record types that have the `is_snapshot` defined can be mapped to authorization policies.

If these items are provided in a sync run, AirSync deletes all previously created permissions. Therefore, the connector must provide these items only if they were actually updated and it **always** provides the whole set of permissions that should exist.

The `conditional_permissions`, `field_level_permissions` and `object_level_permissions` fields define which type of permissions are provided for the listed record types. Notice that they are all defined as a specific field type, which is the type of permission they represent. Here, this configuration declares that both conditional and object-level permissions are provided for ***accounts***; for ***opportunities***, it provides field-level permissions; while for ***cases*** and ***contacts***, it provides only object-level permissions. It is important to precisely define these fields, as AirSync provides proper transformation and loading of permissions only for the listed record types for each permission type. This means that if a field-level permission is provided for ***cases*** in the data extraction phase, it will not be loaded into DevRev, as only ***opportunities*** are defined as possible targets for field-level permissions.
The `permission_groups` and `permission_users` fields represent lists of groups/users that the permissions are applied to. These are both standard reference fields.

## [Initial domain mapping](#initial-domain-mapping)

The initial domain mapping for our `access_rules` record type would look like the following.

Note that this is an example of thow the IDM file looks like when mapping Authorization policy objects. You should use `chef-cli` when creating the initial domain mapping, as it automatically shows the valid field mapping combinations and correctly constructs the file for you.

```
{
  ...,
  "access_rules": {
    "default_mapping": {
      "object_category": "synthetic",
      "object_type": "unified_authorization_policy"
    },
    "possible_record_type_mappings": [
      {
        "devrev_leaf_type": "unified_authorization_policy",
        "forward": true,
        "reverse": false,
        "shard": {
          "constructed_custom_fields": {},
          "devrev_leaf_type": {
            "object_category": "synthetic",
            "object_type": "unified_authorization_policy"
          },
          "mode": "create_shard",
          "stock_field_mappings": {
            "conditional_access": {
              "forward": true,
              "primary_external_field": "conditional_permissions",
              "reverse": false,
              "transformation_method_for_set": {
                "transformation_method": "make_conditional_access"
              }
            },
            "field_access": {
              "forward": true,
              "primary_external_field": "field_level_permissions",
              "reverse": false,
              "transformation_method_for_set": {
                "transformation_method": "make_field_access"
              }
            },
            "groups": {
              "forward": true,
              "primary_external_field": "permission_groups",
              "reverse": false,
              "transformation_method_for_set": {
                "transformation_method": "use_directly"
              }
            },
            "object_access": {
              "forward": true,
              "primary_external_field": "object_level_permissions",
              "reverse": false,
              "transformation_method_for_set": {
                "transformation_method": "make_object_access"
              }
            },
            "users": {
              "forward": true,
              "primary_external_field": "permission_users",
              "reverse": false,
              "transformation_method_for_set": {
                "transformation_method": "use_directly"
              }
            }
          }
        }
      }
    ]
  },
  ...
}
```

The important thing to note here is that each permission type is represented by a field (`object_access`, `field_access`, `conditional_access`). Each field is mapped using a transformation method specific for that type of permission and from a field representing the same type of permission in the external system. So `object_access` can only be mapped from an `object_privilege` type field using the `make_object_access` transformation method.

## [Extracted data](#extracted-data)

The following are examples of how each of the different permission types should look like when provided in the data extraction phase.

While each permission type is described as its own example, note that you can provide multiple permission types inside a single entry. For example, you can provide all three of `object_level_permissions`, `field_level_permissions` and `conditional_permissions` inside a single extracted item and grant them to the users/groups listed in the `permission_users`/`permission_groups` fields.

### [Object-level permission](#object-level-permission)

```
{
  "data": {
    "object_level_permissions": [
      {
        "privileges": [
          "create",
          "read",
          "update",
          "delete"
        ],
        "record_types": [
          "contacts",
          "accounts"
        ]
      }
    ],
    "permission_groups": [
      "group_1"
    ]
  }
}
{
  "data": {
    "object_level_permissions": [
      {
        "privileges": [
          "read"
        ],
        "record_types": [
          "cases"
        ]
      }
    ],
    "permission_users": [
      "user_1",
      "user_2",
      "contact_1"
    ]
  }
}
```

The first entry represents a permission object that grants full CRUD access to the `contacts` and `accounts` to `group_1`. The second entry grants read privileges on the `cases` record type to specific users `user_1`, `user_2` and `contact_1`.

### [Field-level permission](#field-level-permission)

```
{
  "data": {
    "field_level_permissions": [
      {
        "record_type": "opportunities",
        "read_fields": [
          "title",
          "description",
          "stage",
          "account"
        ],
        "write_fields": [
          "title",
          "description"
        ]
      }
    ],
    "permission_users": [
      "user_1",
      "user_2"
    ],
    "permission_groups": [
      "group_1"
    ]
  }
}
{
  "data": {
    "field_level_permissions": [
      {
        "record_type": "opportunities",
        "read_all_fields": true,
        "write_fields": [
          "description",
          "stage"
        ]
      }
    ],
    "permission_groups": [
      "group_2"
    ]
  }
}
```

The first entry represents a permission object that grants read acces on `opportunities` fields: `title`, `description`, `stage` and `account`, while granting write access to `title` and `description`, to group `group_1` and specific user `user_1` and `user_2`. Notice that the fields listed in the `write_fields` field need to also be provided in the list of `read_fields`.

The second entry grants read access to all fields inside the `opportunities` object using the `read_all_fields` field, while granting write access only to fields `description` and `stage` to group `group_2`.

### [Conditional permission](#conditional-permission)

```
{
  "data": {
    "conditional_permissions": [
      {
        "object_privileges": [
          "read"
        ],
        "record_type": "accounts",
        "scope_to_users_in": [
          "watcher"
        ]
      }
    ],
    "permission_groups": [
      "group_1"
    ]
  }
}
{
  "data": {
    "conditional_permissions": [
      {
        "field_caveats": [
          {
            "operator": "eq",
            "field": "customer",
            "value": true
          },
          {
            "operator": "in",
            "field": "upsell",
            "value": [
              "yes",
              "maybe"
            ]
          }
        ],
        "record_type": "accounts",
        "field_privileges": {
          "read_all_fields": true,
          "write_fields": [
            "owner",
            "priority"
          ]
        }
      }
    ],
    "permission_user2": [
      "user_1",
      "user_2"
    ]
  }
}
```

The first entry represent a permission tied to `group_1` which grants object-level read access to the `accounts` object, if the user is present inside the `watcher` field on the account object.

The second entry grants read access to all fields and write access to `owner` and `priority` fields on the `accounts` object to users `user_1` and `user_2`, if the value of the `customer` field on the account is `true` and the value of the `upsell` field is one of [`yes`, `maybe`]. Here, the values inside the `field_caveats` are joined conjunctively. You can provide multiple conditions inside the `field_caveats` field to create a more restrictive rule.

Some rules to keep in mind when defining `field_caveats`:

* The supported operators are `eq`, `not_eq`, `in`, and `intersects`.
* The supported field types are `int`, `text`, `bool`, `rich_text`, `enum`, and collections of the listed types.
* The value provided in `value` must match the field type, or a list of the respective field type in case of the `in` operator.
* The `intersects` operator can only be used for collection fields, the other `operators` are all applicable to non-collection fields.

Last updated on

## Source
- DevRev developer docs: [Permissions import example](https://developer.devrev.ai/airsync/data-model/permissions-example)
