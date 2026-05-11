---
title: Search
devrev_id: ART-21855
parent_directory: Computer by DevRev
translation_group: oYn1lc4B
modified_date: "2026-03-11T17:40:39.711Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/oYn1lc4B"
tags: []
top_category: Computer by DevRev
wiki_match: features/search
match_score: 1.0
last_updated: 2026-05-11
related: ['features/search']
summary: "Search works across all DevRev apps, offering seamless navigation and access to issues, tickets, articles, customers, and more."
---

# Search

[[features/search|Search]] works across all DevRev apps, offering seamless navigation and access to [[features/issues|issues]], [[features/tickets|tickets]], [[entities/article|articles]], customers, and more. It also allows you to search through timeline comments related to these items. By using search queries and [[features/commands|commands]], you can refine your search and achieve more precise results.

Key actions in the search interface include:

* Users can toggle between standard and expanded views for an enhanced search experience.
* Clicking on a comment directs users to the specific comment within the relevant object panel.
* Search results display details such as the comment author, timestamp, and comment text.
* The interface shows up to two relevant comments per object.

To start a search, press Cmd + K on Mac or Ctrl + K on Windows, or click **Search** at the top of the left navigation bar.

![search](don:core:dvrv-us-1:devo/0:artifact/4099915)

A search query consists of the following syntax:

```
[operator]* [field]* [term/phrase]*
```

The above query specifies the following:

* Filtering
* Full-text search terms/phrases

Filtering is denoted by the query's `[operator]* [field]*`, which represents a logical AND of all operators (if specified).
This is used to reduce the list of possible objects that can be returned in search results.

Full-text search terms/phrases are denoted by `[term/phrase]*` and are used to do full-text searches on object text fields.

Example: `state:open,closed` (field value)

## Operators

Operators are used to filter the search results. The following table shows the syntax of each operator along with examples.

|  |  |  |
| --- | --- | --- |
| Syntax | Description | Examples |
| in:`<body/title>` | Aids in searching within the body of the [[entities/ticket|ticket]]/[[entities/issue|issue]]/[[entities/enhancement|enhancement]] or title. | `in:title crm` `in:title "crm exp"` `in:title crm exp` `in:body "bot issues"` |
| type:`<object type>` | Enables users to filter by object type. Supported object types include: `issue`, `enhancement`, `ticket`, `revu` (for searching contacts), `question_answer`, `conversation`, `article`, `devu` (for searching internal contacts), `account`, `feature`, `runnable`. | `type:issue` `type:enhancement in:title CRM` `type:revu` `type:enhancement, opportunity` `type:issue, enhancement in:title crm` |
| `-` | Acts as an exclusion in search results. "-" can be used for the same purpose. | `type:issue -crm` `type:issue in:title -crm` |
| state | Filters results based on the stage: open, closed, or in\_progress. | `state:open` `state:closed` `state:in_progress` |
| severity | Filters out tickets with the desired severity level. Supports: blocker, high, medium, low. | `severity:high` `type:ticket -severity:low` (filters all tickets excluding the ones with low severity) |

## Fields

Fields can be used along with operators to filter the search results further. The following table shows types of fields, syntax and it's examples.

|  |  |  |
| --- | --- | --- |
| Types of field | Syntax | Examples |
| Boolean fields | `<field_name>:true (or :1)` `<field_name>:false (or :0)` | `isCustomer:True` `Submitted:0` |
| Numeric fields | `<field_name>:<v>, <field_name>:<<v>, <field_name>:><v>`  `<field_name>:v1..v2`  `<field_name>:<=<v>`  `<field_name>:>=<v>` | `revenue:<100` `revenue:500..2000` `discount>=0.25` `tickets=< 5` |
| String fields | `<field_name>:<v>` | `Name:alice` `Name:Alice,bob,eve` |
| Date fields | `<field_name>:<v>`  `<field_name>:<=<v>`  `<field_name>:v1..v2` `<field_name>:><v>` `<field_name>:>=<v>`  `<field_name>:<<v>` | `target_release_date:<2020-10` `target_release_date:<2020` |
| Array fields | `<field_name>:<v>` Here `<v>` is a CSV list of values where a match occurs if the array field contains an element having any of the values in the list. | `magic_dates_c:1970-01-01,2006-01-02` (date array) `modified_date:2024-01-02..2024-01-05` (fetches records that were modified lies within 2024-01-02 and 2024-01-05) `created_date:2023` (fetches records that were created in 2023) |

## Integrate search with customization

DevRev's [[features/customization|customization]] framework allows you to extend core objects with custom fields and create custom object types. These customizations are fully searchable using the same search syntax as standard fields.

### Search over custom fields

Custom fields use the standard field search syntax and support all field types including text, numeric, boolean, date, and array fields. Custom fields that are specific to a subtype require the subtype filter to be included in your search query. Subtype-specific field filters are not supported while searching across multiple subtypes.

**Syntax:**

```
subtype:<subtype_name> <custom_field_name>:<value>
```

**Examples**

Search for tickets related to access issues with tenant field `escalated`:

```
tnt__escalated:true access issues
```

Search for bugs related to access issues with subtype field `customer_impact`:

```
subtype:Bug ctype__customer_impact:true access issues
```

Search for issues with custom app field `commits` coming from app fragment `github`:

```
type:issue app_github__commits:100
```

Search across multiple subtypes for tickets related to access issues:

```
subtype:Bug,Events access issues
```

Learn more about creating and managing custom fields in the [Object customization guide](https://developer.devrev.ai/beta/guides/object-customization).

### Search over custom objects

Custom fields use the standard field search syntax and support all field types including text, numeric, boolean, date, and array fields. You should add the leaf\_type filter while searching over custom objects.

Search for `book` custom objects related to [[features/agents|AI agents]]:

```
leaf_type:book AI agents
```

Search for `book` custom objects related to AI [[features/agents|agents]] with tenant field `author`:

```
leaf_type:book author:"Chip Huyen" AI agents
```

For detailed information on creating custom objects, see the [Custom objects guide](https://developer.devrev.ai/beta/guides/custom-objects).

## Related wiki nodes
- [[features/search]]

## Source
- DevRev support [[entities/article|article]] [Search](https://support.devrev.ai/en-US/devrev/article/oYn1lc4B) (ART-21855)
