---
title: Core concepts
devrev_id: ART-21847
parent_directory: Computer by DevRev
translation_group: acYqDRVg
modified_date: "2026-05-07T07:24:04.218Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/acYqDRVg"
tags: []
top_category: Computer by DevRev
wiki_match: features/side-conversations
match_score: 0.516
last_updated: 2026-05-11
summary: "DevRev bridges silos by connecting three core objects: identity, parts, and work."
---

# Core concepts

DevRev bridges silos by connecting three core objects: [[features/identity|identity]], [[features/parts|parts]], and work. By connecting work to parts and parts to customer and developer identity, we bring product and service creators closer to their customers.

![work types](don:core:dvrv-us-1:devo/0:artifact/4099882)

## Parts

A *[[entities/part|part]]* is a piece of a product or service that can be either a customer part or a builder part.

* *Customer parts* relate to how a product is consumed by your customers, with three main types: product, capability, and features.
* *Builder parts* are the code, service, or components built or used by the developer.

Customer parts are often served by one or more builder parts.

One of your first experiences in the app is in DevRev [[glossary/trails|trails]]. [[features/build|Build]] your trail, create customer and builder parts, and connect them to enable your teams to be customer-centric.

Visit the [[support-articles/computer-by-devrev/parts-trails|parts & trails]] page to learn more about creating parts and trails.

## Work

A work item is any artifact in the system that requires some activity to be performed by a human or machine. They have associated owners and require some level of effort. Work commonly leads to other work of the same or different type. In that sense, [[support-articles/computer-by-devrev/apps|work can be linked]] together and have parent/child relationships. For example, a high-level [[entities/issue|issue]] may spawn multiple child [[features/issues|issues]]/[[entities/task|tasks]] which may each have their own owner as well as their own child items.

* A *[[entities/conversation|conversation]]* is a synchronous or near-synchronous discussion that may be escalated to a [[entities/ticket|ticket]]. [[features/conversations-feature|Conversations]] are part of [[support-articles/computer-plus-support/computer-support|Computer for Support Teams]].
* A *ticket* is a work item created by the customer or consumer. [[features/tickets|Tickets]] are part of [[support-articles/computer-plus-support/computer-support|Computer for Support Teams]].
* An *issue* is a work item created by the builder or maintainer. Issues are part of [[support-articles/computer-plus-build/computer-build-overview|Computer for Builders]].
* An *[[entities/enhancement|enhancement]]* is the parent of multiple issues that lead to a desired change to the product. [[entities/enhancement|Enhancements]] are part of the [[support-articles/computer-plus-build/computer-build-overview|Computer for Builders]] app.
* A *[[entities/task|task]]* is a work item used to break down larger work into smaller pieces. [[support-articles/computer-by-devrev/tasks|Tasks]] can be part of tickets and issues.

In traditional systems of record, duplicate work is rampant, and maintenance of the backlog can be an entire job itself. Huge engineering backlogs can have detrimental effects on developers' morale and work velocity.

DevRev helps you avoid duplication during the work creation process. As you're creating a new work item, the *Similar work* modal appears and presents potential duplicates. You can also use this modal to link the work you're creating to other work items if appropriate.

## Source
- DevRev support [[entities/article|article]] [Core concepts](https://support.devrev.ai/en-US/devrev/article/acYqDRVg) (ART-21847)
