---
title: Computer for Your Customers
devrev_id: ART-21840
parent_directory: Knowledge Base
translation_group: 2aHOSG2W
modified_date: "2026-03-31T02:13:48.354Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/2aHOSG2W"
tags: []
top_category: Computer+ Support
wiki_match: features/csat
match_score: 0.453
last_updated: 2026-05-11
---

# Computer for Your Customers

Computer can be used to deflect user queries in conversation or to suggest articles from your knowledge base for resolving tickets. It will try to answer customer queries based on the articles and QA pairs provided in the Knowledge base, while keeping a support agent subscribed to conversations. If it cannot answer a certain query or you request it to connect to the team, it will redirect it to the default owner of the conversation.

When looking for a source to inform its answer, it will prioritize the QA pairs, which are intended to serve as definitive answers to commonly repeated questions.

For Computer to suggest articles, you need to add articles to your DevRev instance. Refer to [[support-articles/computer-plus-support/articles|articles]] for more information.

## Suggest-only mode

Computer only suggests an answer to the user query. A support agent can accept or make edits to the answer, then send it to the user.

## Content-powered mode

Computer automatically replies to the user query before it gets assigned to support. It goes through the knowledge base (articles and QAs), generates an answer, and checks with the user if the answer is useful or not.

* If Computer doesn't understand the query, it gives the user an option to rephrase the question and ask again.
* If the user marks the answer as useful, Computer asks the user if they have more questions, then resolves the conversation.
* If the user marks the answer as not useful, Computer either creates a ticket or routes the conversation using the relevant routing rule.

![Plug](don:core:dvrv-us-1:devo/0:artifact/4099865)

## Goal-oriented mode (Beta)

The goal-oriented agent allows users to create complete workflows triggered by their actions.

Goal-oriented mode is currently in beta. Contact our support team for more information.

## Source
- DevRev support article [Computer for Your Customers](https://support.devrev.ai/en-US/devrev/article/2aHOSG2W) (ART-21840)
