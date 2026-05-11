---
title: Rich text fields
type: developer-doc
status: stable
source: developer.devrev.ai
category: airsync
source_url: https://developer.devrev.ai/airsync/data-model/rich-text-fields
last_updated: 2026-05-11
summary: "Rich text in DevRev enables formatted text fields with mentions, used for issue descriptions or conversation bodies."
---

# Rich text fields

Data model

# Rich text fields

Rich text in DevRev enables formatted text fields with mentions, used for issue descriptions or conversation bodies.

A simple rich text looks like one markdown string wrapped in an array:

```
["Hello **world**!"]
```

Markdown must conform to [CommonMark Spec v0.30](https://spec.commonmark.org/0.30).

## [Rich text mentions](#rich-text-mentions)

Rich text can include mentions by combining strings and mention objects:

```
[
  "Hello ", 
  {"ref_type":"external_user_type", "id":"1...", "fallback_record_name": "John Doe"}, 
  "how are you?"
]
```

Mention objects represents any mention (user, issue, etc.) in rich text and have the following structure:

| Field | Type | Required | Description |
| --- | --- | --- | --- |
| `id` | String | Yes | Identifier of the mentioned item (user ID, etc.) in the format used by the source system. |
| `ref_type` | String | Yes | Type of the mentioned item (for example, `issue`, `comment`). It must match the record type defined in external domain metadata. The recipe converts this based on user mappings. |
| `fallback_record_name` | String | No | Display text if the mention cannot be resolved (user display name, ticket title, etc.). |

In reverse, the loader should expect the following structure:

```
{
  "type": "rich_text",
  "content": [
    "Hello ",
    {
      "ref_type": "external_user_type",
      "id": "don:identity:dvrv-us-1:devo/xyz:devu/1",
      "fallback_record_name": "John Smith"
    },
    "how are you?"
  ]
}
```

## [Importing articles](#importing-articles)

Articles are documents containing key information about products, services, and processes.
They support both Markdown and HTML formats.

Articles can include mentions to artifacts and other articles. Inline attachments must map to artifacts,
and article links must map to articles.

### [Managing permissions](#managing-permissions)

Article permissions are managed through the `shared_with` field, which can reference users, groups, and platform groups.
Refer to the [permissions](/airsync/data-model/permissions) for more details.

### [Inline attachments](#inline-attachments)

If an inline attachment is hosted in the source system, it must be created as an artifact in DevRev.
The same link cannot be used as the attachment is deleted in the source system when our customers deactivate the account.
However, creating an artifact is not enough. The artifact must be linked in the appropriate place in the article content.

The following HTML example shows an inline attachment:

```
<img src="don:core:dvrv-us-1:devo/0:artifact/1" alt="Alt Text"/>
```

The following Markdown example shows an inline attachment:

```
![Alt Text](don:core:dvrv-us-1:devo/0:artifact/1)
```

Let's say the content of your external system looks like this:

```
<p>
  This is an article with one image.  
</p>
<p>
  <img src="https://devrev.zendesk.com/hc/article_attachments/29908544740244" alt="download.jpeg">
</p>
```

The content in DevRev should look like this:

```
<p>
  This is an article with one image.
</p>
<p>
  <img src="don:core:dvrv-us-1:devo/0:artifact/1" alt="download.jpeg">
</p>
```

Where `don:core:dvrv-us-1:devo/0:artifact/1` is the DevRev artifact ID corresponding to external attachment `29908544740244`.
To accomplish this, transform the article content to this JSON:

```
[ 
    "<p>This is an article with one image.</p><p><img src=\"",
    {
        "ref_type": "artifact",
        "id": "29908544740244",
        "fallback_record_name": "<fallback link>"
    },
    "\" alt=\"download.jpeg\"></p>" 
]
```

Set `ref_type` to `artifact` and use the source system's attachment ID.
The platform replaces the mention with the corresponding artifact ID.
Note that the resolved value isn't wrapped in double quotes.

### [Links to other articles](#links-to-other-articles)

When an article references another article, create a mention to that article.
The referenced article must exist from previous syncs or be created in the current sync.
The platform handles ID resolution since article IDs in DevRev can't be predicted at extraction time.
This feature works with HTML format, and since Markdown can contain HTML, the same approach applies there.

The following HTML example shows a link to another article:

```
<a data-article-id="don:core:dvrv-us-1:devo/0:article/10" href="/ART-10" target="_self">
  Contact our Support Team
</a>
```

Let's say the content of your external system looks like this:

```
<p>
  You can create an account and log-in
  <a href="https://devrev.zendesk.com/hc/en-us/articles/360059607772" target="_self">
    only
  </a>
  with the company email.
</p>
```

The content in DevRev should look like this:

```
<p>
  You can create an account and log-in
  <a data-article-id="don:core:dvrv-us-1:devo/0:article/10" href="/ART-10" target="_self">
    only
  </a>
  with the company email.
</p>
```

Where `don:core:dvrv-us-1:devo/0:article/10` is the DevRev article ID corresponding to external article `360059607772`.
Transform the content to this JSON:

```
[
    "You can create an account and log-in <a data-article-id=\"",
    {
        "ref_type": "article",
        "id": "360059607772",
        "fallback_record_name": "<fallback article ID>"
    },
    "\" target=\"_self\"> only</a> with the company email."
]
```

Set `ref_type` to the external system's item type that maps to articles (e.g., "documents").
The platform replaces the mention with the corresponding DevRev article ID and adds the appropriate href attribute.

Last updated on

[Supported DevRev object types

Previous Page](/airsync/supported-object-types)[Permissions

Next Page](/airsync/data-model/permissions)

## Source
- DevRev developer docs: [Rich text fields](https://developer.devrev.ai/airsync/data-model/rich-text-fields)
