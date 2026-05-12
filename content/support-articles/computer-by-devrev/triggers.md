---
title: Triggers
devrev_id: ART-21902
parent_directory: Workflow engine
translation_group: TIupi2Il
modified_date: "2026-02-20T18:29:12.14Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/TIupi2Il"
tags: []
top_category: Computer by DevRev
wiki_match: glossary/turing
match_score: 0.571
last_updated: 2026-05-11
summary: "Triggers serve as the entry point for all workflows."
---

# Triggers

Triggers serve as the entry point for all [[features/workflows|workflows]]. They define the conditions under which a workflow starts and specify what information is forwarded to the following steps in your workflow.
The following section lists the different types of triggers you can use. Filter conditions are required in all triggers.

|  |  |  |
| --- | --- | --- |
| Operation | Input Parameters | Output |
| [[entities/account|Account]] created | Filter conditions | Account object |
| Account updated | Filter conditions | Account object |
| Contact created | Filter conditions | Customer User object |
| Contact updated | Filter conditions | User object |
| [[entities/enhancement|Enhancement]] updated | Filter conditions | Enhancement object |
| [[glossary/incident|Incident]] updated | Filter conditions | Incident object |
| [[entities/issue|Issue]] created | Filter conditions | Issue object |
| Issue linked With object | Filter conditions | Issue and linked object |
| Issue updated | Filter conditions | Issue object |
| [[entities/meeting|Meeting]] created | Filter conditions | Meeting object |
| Meeting updated | Filter conditions | Meeting object |
| [[glossary/opportunity|Opportunity]] created | Filter conditions | Opportunity object |
| Opportunity updated | Filter conditions | Opportunity object |

## Source
- DevRev support [[entities/article|article]] [Triggers](https://support.devrev.ai/en-US/devrev/article/TIupi2Il) (ART-21902)
