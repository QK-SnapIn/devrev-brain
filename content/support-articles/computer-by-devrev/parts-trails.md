---
title: Parts & trails
devrev_id: ART-21849
parent_directory: Computer by DevRev
translation_group: _SsC0kTo
modified_date: "2026-04-09T06:45:50.517Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/_SsC0kTo"
tags: []
top_category: Computer by DevRev
wiki_match: entities/part
match_score: 0.85
last_updated: 2026-05-11
related: ['entities/part']
---

# Parts & trails

A *part* is a component of a product or service that has a lifecycle (creation, operation, evolution, deprecation), and can be recursively made of smaller parts. Events and work items must be related to parts. In general, parts are the core objects that almost all other objects are linked to, which helps enforce the notion of tying everything back to the product or service.

*Trails* is an extensible interface that allows you to view and manage your part hierarchy and related items. Think of it like a graph canvas that's rendering linkages among items—including tickets, issues, and articles—making them easier to navigate and summarize. Trails is Computer's Memory: the ontology at the heart of DevRev that defines connections among product parts and people.

The following image shows an example of DevRev's **Trails** view.

![Trails](don:core:dvrv-us-1:devo/0:artifact/4099892)

For a guided tour of Trails, check out the interactive [walkthrough](https://walkthrough.devrev.ai/app/trails).

There are two core categories of parts: customer parts and builder parts.

*Customer parts* relate to how a product is expressed, integrated, or consumed. These parts may be consumed by external customers (revs) or internal employees (devs). Although they may also be provided/enabled by builder parts running internally, the customer just sees the product, service, or feature they are interacting with. Customer parts may also be abstractions on other customer parts exposed by 3rd parties (such as Auth0 or s3).

For example, in the digital world, rather than integrating with code or packages, they may integrate with APIs.

*Builder parts* are those built internally related to code or something the developer relies on or builds, or a service provided by an organization. These may be *runnables* that may expose APIs or *linkables* that may be used in other services (such as utils or libraries). Though they may provide the functionality exposed and interacted with by the customer, they are often abstracted and unknown to the user.

Types of parts typically include product, capability, feature, runnable, and linkable.

The part hierarchy is at the core of the DevRev platform and is the basis for tying all work and event funnels to a common product or service model and for coordinating across funnels.

The following figure shows the conceptual part hierarchy.

![Part Hierarchy](don:core:dvrv-us-1:devo/0:artifact/4099893)

## Customer parts

### Product or service

At the highest level of the part hierarchy is a *product* or *service*. An organization may have one or more products or services they deliver to their customers. Products can also be delivered through one or more conduits (such as tangible goods or as-a-service).

Products typically have the following characteristics:

* Are a unit of profit and loss (P&L)
* Are where customers (internal or external) are onboarded
* Provide the basis for identity
* May have a notion of billing/chargeback (which can be done at this level or further down the stack)

Services may have the following additional characteristics:

* Provide an API or interface
* Define code-based or business services

One example of the difference between a product and a service is Microsoft Office (software product) versus Office 365 (cloud service).

A key to consider is that all must be considered from the perspective of the workspace. A product for them may be a service for another. For example, consider a managed services provider, they may provide a "product" (for example, Microsoft Exchange) delivered as a managed service.

A service may also be a business service like IT (internal), HR (internal), or Consulting (external).

Example products delivered as software or tangible goods:

* Hardware products (Lenovo laptops, mobiles and more.)
* Software products (MSFT Office, Acrobat, and more)

Example services:

* Cloud services (Amazon Web Services, Azure, GCP)
* IT services (Helpdesk, Data center, and more.)
* Facilities services (building services, lunch services)

The following video shows products, capabilities, and features in DevRev.

### Capability

A *capability* exists under a product or service and is commonly the main item of interaction for customers.

Capabilities typically have the following characteristics:

* Exist under a product or service
* Provide the ability to do something (verbs) with entities (nouns); for example `create object`
* Provide an API namespace
* Provide units of licensing and pricing
* Have its own level of authentication and access control or may inherit from the product

### Feature

A feature exists under a capability (or feature for sub-features) and is commonly a unit of configuration or "knobs" in a capability.

Features typically have the following characteristics:

* Exist under a capability (or feature for sub-features)
* Provide a unit of configuration (adjective) for entities managed by the capability
* Enable version history (adjective) on object
* May provide a subset of the API namespace
* Are interacted with only inside the context of the capability or not directly interacted with at all

You can add a sub-feature to a feature for a more granular breakdown of features. These leverage the same feature object and have the same attributes. The only difference is that their parent becomes a feature rather than a capability.

## Builder parts

### Runnable

A runnable is a builer part and is something that can be instantiated or do something. For example, runnable may be macro services, microservices, or functions (lambdas). Runnables are things that have some direct execution or lifespan. A runnable may serve one or more features and/or capabilities.

A runnable typically has the following characteristics:

* Are a unit of functionality that can be deployed independently or as part of a larger system.
* Have an execution lifecycle be it short (lambda/function) or long (microservice).
* Expose an API.
* Are interacted with directly through an API or UI.
* Are published in a service registry or load balancer.

Example runnables:

* Docker image
* Lambda bundle

Example DevRev runnables:

* Wisp (search)
* Codex (work SOR)
* Partiql (parts SOR)

### Linkable

A linkable is a unit of functionality that's designed to be part of a system or application and not used directly. These commonly refer to things like libraries or utils that may be leveraged by multiple runnables.

Components typically have the following characteristics:

* Linkable items are commonly used as libraries or binary artifacts.
* Not commonly exposed to the consumer (but can be).
* Are intended to be used as part of larger services, not on their own.

Example linkable parts:

* Library
* DLL
* Golang package

Example DevRev Linkables:

* All clients (for example, partiql-client, codex-client, mfz-client)
* Shared (logging and so on.)

## Trails

You can open a part in trails by hovering over the part ID.

![open in trails](don:core:dvrv-us-1:devo/0:artifact/4099894)

* **Sort and filter**: You can apply filters and sort for each column in trails. Filtering by owner and stage can help locate the data you need much faster. Part nodes can be sorted alphabetically by **Name** or based on events like **Created date, Modified date, Target close date, Close date**.
* **Search navigation**: Our top global search bar and localized search bars in each column of **Trails** now goes directly to the node for that searched part, saving you time and effort.
* **Richer part nodes**: You can enrich part nodes by selecting additional info like owner and stage.

![Trails-sort](don:core:dvrv-us-1:devo/0:artifact/4099896)

### Manage and link parts

To manage, link, and edit parts, go to **Product > Trails**.

If you need to move a part to a different parent, do the following:

1. Hover over the capability or feature you want to move and click **View** and it'll open a right window pane.
2. Select either **Related** > **Parts** or **Manage Links** to open the **Link parts** dialog.
3. In the **Link parts** dialog, click the product name in the **To** field.
4. Select the product name you want to move the capability from the and click **Link parts**.

![view](don:core:dvrv-us-1:devo/0:artifact/4099897)

![manage links](don:core:dvrv-us-1:devo/0:artifact/4099898)

If you have parent parts and children parts under it then:

1. Move the child parts first.
2. Optionally move linked tickets and issues for each child.
3. Then move the parent part.
4. Apply for this order at all levels: Product, Capabilities, Features, and Sub-features.

Linking parts isn't only limited to capability, feature, or runnable. You can link the following parts:

* **Enhancement:** A change to a part in the form of addition, deprecation, or transformation.
* **Top contributors:** Top 10 owners with issues in the closed/resolved stage for any part in the hierarchy.
* **Top supporters:** Top 10 owners with tickets in the closed stage for any part in the hierarchy.
* **Top customers:** Top 10 workspaces with the most number of tickets for any part in the hierarchy.

## Attributes

Products have attributes that can be used to filter and group issues in various views.
You can find all the stock attributes listed in [**Settings** > **Object customization** > **Product** > **Stock fields**](https://app.devrev.ai/?setting=object-customization?type=product).
These are the stock attributes which come with DevRev:

* **Type**: This shows the type of part. For example, product, capability, feature, runnable, or linkable.
* **Owner**: The person responsible for the part. Parts are assigned to an engineer, PM, designer, or any other team member through the **Owner** attribute.
* **Stage**: The current state of the part. The stage attribute is used to track the progress of the part through its lifecycle. These are the following stages:

  + **Open**: *Ideation*, *Prioritized*, *Deprioritized*
  + **In Progress**: *UX design*, *In development*, *In testing*
  + **Deployed**: *Limited availability*, *General availability*
  + **Inactive**: *Deprecated*, *Won't do*
* **Created by**: The user who created the issue.
* **Created date**: The date the issue was created.
* **Modified date**: The date the issue was last modified.
* **Modified by**: The user who last modified the issue.
* **Tags**: Tags are used to categorize issues.
* **Release notes**: Add description of the feature or bug fix to include it in the release notes.
* **Customer impact**: The impact of the part on the customer.
* **Target close date**: The date by which the part is expected to be resolved.
* **Target start date**: The date by which the part is expected to start.

You can add custom attributes to issues to track additional information. For more information on custom attributes, see [[support-articles/computer-by-devrev/object-customization|object customization]].

## Subtypes

You can create subtypes of issues to categorize them further. For example, you can create subtypes for bugs, features, and tasks. Subtypes can be used to filter issues in various views.
A subtype inherits all the attributes of its parent issue type. You can add custom attributes to a subtype.
To know how to create subtypes and add custom attributes to them, see [[support-articles/computer-by-devrev/object-customization|object customization]].

## Related wiki nodes
- [[entities/part]]

## Source
- DevRev support article [Parts & trails](https://support.devrev.ai/en-US/devrev/article/_SsC0kTo) (ART-21849)
