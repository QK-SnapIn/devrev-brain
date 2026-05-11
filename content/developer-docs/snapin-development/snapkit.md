---
title: Snapkit
type: developer-doc
status: stable
source: developer.devrev.ai
category: snapin-development
source_url: https://developer.devrev.ai/snapin-development/references/snapkit
last_updated: 2026-05-11
summary: "This reference lists the elements for creating custom user interface using snap-kit."
---

# Snapkit

References

# Snapkit

This reference lists the elements for creating custom user interface using snap-kit.

## [Structure](#structure)

The snap-kit JSON has a top-level structure with `object`, `body`, `type`, and `snap_kit_body` fields. The `snap_kit_body` field contains information regarding snap-kit's structure.

The `snap_kit_body` field has the following properties:

* `snap_in_id`: A unique identifier for the snap-kit.
* `snap_in_action_name`: The name of the action this snap-kit represents.
* `body`: An object that holds the actual snap-kit content in the form of `snaps`.

```
{
  "object": "<source_id>",
  "body": "Giphy",
  "type": "timeline_comment",
  "snap_kit_body": {
    "snap_in_id": "<snap_in_id>",
    "snap_in_action_name": "giphy",
    "body": { "snaps": [] }
}
```

The `body` field contains an array of `snaps`. Each snap can have a `type`; and depending on the type, it has different properties.

Types in the following categories are available:

* User interface elements
* Form elements
* Layout elements
* Data pickers

## [Action payloads](#action-payloads)

Snap-kit generates payloads when a user interacts with an actionable snap. The payload is sent to the backend and can be used to perform actions. The following snaps generate payloads:

* [Button](#button)
* [Checkboxes](#checkboxes)
* [Input](#input) and all its types ([Plain text input](#plain-text-input), [Number input](#number-input), [Email input](#email-input), [Rich text input](#rich-text-input))
* [List input](#list-input) and all its types ([String list input](#string-list-input), [Number list input](#number-list-input), [Email list input](#email-list-input))
* [Static select](#static-select)
* [Multi static select](#multi-static-select)
* [Radio buttons](#radio-buttons)
* [Toggle button](#toggle-button)
* [Upload input](#upload-input)
* [Form](#form)
* [Part picker](#part-picker)
* [Tag picker](#tag-picker)
* [User picker](#user-picker)

All actionable snaps share the same base payload structure.

```
{
  "type": "<type of snap that generated the payload>",
  "action_id": "<the action identifier of the snap that generated the payload>",
  "action_type": "<the type of the action as defined in the snap>",
  "timestamp": "<timestamp as a string in ISO 8601 format>"
}
```

## [Base types](#base-types)

Many elements share the same base properties. The base types these elements inherit from are described below.

## [User interface elements](#user-interface-elements)

## [Form elements](#form-elements)

## [Layout elements](#layout-elements)

## [Data pickers](#data-pickers)

Last updated on

[Hooks

Previous Page](/snapin-development/references/hooks)[Snap Components

Next Page](/snapin-development/references/snap-components)

## Source
- DevRev developer docs: [Snapkit](https://developer.devrev.ai/snapin-development/references/snapkit)
