---
title: HTTP archive file upload & sanitization
devrev_id: ART-21940
parent_directory: Automate
translation_group: XUa0R9o1
modified_date: "2025-12-10T06:57:16.099Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/XUa0R9o1"
tags: []
top_category: Snap-ins
wiki_match: features/csat
match_score: 0.413
last_updated: 2026-05-11
---

# HTTP archive file upload & sanitization

[HTTP archive file upload & sanitization](https://devrev.ai/marketplace/har-sanitization) offers the ability to prompt clients to upload HTTP archive (`.har`) files
through conversations, and automatically sanitizes the file while hard-deleting
the unsanitized version. Once sanitization is done, the sanitized file is
reuploaded to the conversation.

The snap-in has default sanitization targets for specific cookies, headers and
MIME types. Through configuration, you can specify sanitization of all cookies,
headers, POST parameters, MIME types, or query string parameters.

## Installing the HTTP archive file upload & sanitization snap-in

1. Install the [HTTP archive file upload & sanitization](https://devrev.ai/marketplace/har-sanitization) from the DevRev Marketplace.
2. Update the snap-in sanitization configurations as needed.

   * Configure whether all cookies should be sanitized in both requests and
     responses. If the option is disabled, the default sanitized cookies are:

     + `access_token`
     + `appID`
     + `assertion`
     + `auth`
     + `code`
     + `refresh_token`
     + `token`
   * Configure whether all headers should be sanitized in both requests and
     responses. If the option is disabled, the default sanitized headers are:

     + `Authorization`
     + `SAMLRequest`
     + `SAMLResponse`
     + `authenticity_token`
     + `challenge`
     + `client_id`
     + `client_secret`
     + `code_challenge`
     + `code_verifier`
     + `email`
     + `facetID`
     + `fcParams`
     + `id_token`
     + `password`
     + `serverData`
     + `shdf`
     + `state`
     + `usg`
     + `vses2`
     + `x-client-data`
   * Configure whether all query string parameters should be sanitized in both
     requests and responses.
   * Configure whether all POST parameters should be sanitized.
   * Configure whether all MIME types should be sanitized in both requests and
     responses. If the option is disabled, the default sanitized MIME types are:

     + `application/javascript`
     + `text/javascript`
3. Click **Save** > **Install snap-in**.

## Source
- DevRev support article [HTTP archive file upload & sanitization](https://support.devrev.ai/en-US/devrev/article/XUa0R9o1) (ART-21940)
