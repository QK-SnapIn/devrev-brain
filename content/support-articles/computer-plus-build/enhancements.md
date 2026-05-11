---
title: Enhancements
devrev_id: ART-21873
parent_directory: Computer+ Build
translation_group: AjBQbI4R
modified_date: "2026-01-12T19:55:02.901Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/AjBQbI4R"
tags: []
top_category: Computer+ Build
wiki_match: entities/enhancement
match_score: 0.957
last_updated: 2026-05-11
related: ['entities/enhancement']
---

# Enhancements

A product is a combination of [[support-articles/computer-by-devrev/parts-trails#rev-parts|customer parts]] and [[support-articles/computer-by-devrev/parts-trails#dev-parts|builder parts]]. Changes to a part could be in the form of addition, deprecation, or transformation. While the changes are a set of tasks or work for the build teams involved, the outcome of relevance is either a new part, an existing part that's deprecated, or an existing part that's improved or expanded. In the latter case, the enhancement record merges with the part on which this activity is based.

Enhancements may be used to track higher-level groups of user stories or to bundle related work together. This usage of "enhancement" is similar to "epic" in other build approaches. You can perform filtering by stage and add stage attributes for enhancements.

## Stages

To create an enhancement, go to **Product > Parts**, click **+ Part**, and select **Enhancement** from the menu.

This diagram represents the **Enhancement Transitions** workflow in DevRev, organized into four main groups:

- **📂 Open**: Initial enhancement planning stages (Ideation, Prioritized)
- **⚡ In Progress**: Active development stages (UX Design, In Development, In Testing)
- **🚀 Released**: Deployment stages (Limited Availability, General Availability)
- **🔒 Closed**: Final states for enhancements (Deprecated, Won't Do, Deprioritized)

The workflow supports comprehensive product development from ideation through general availability, with support for iterative development and the ability to reopen closed enhancements.

![Enhancement Transitions Diagram](don:core:dvrv-us-1:devo/0:artifact/4100241)

**Open**

- *Ideation*Requests and requirements from various sources–customers, support, tech leads, and product managers–are discussed to form a cohesive idea for a product enhancement. The outcome of this stage is a product requirements document (PRD) that describes the enhancement. The PRD and supporting documents are linked to the ENH item in the **Related > PRD** field.
- *Prioritized*The decision-makers have decided to proceed with the enhancement idea and have allocated resources to make it happen. The outcome of this stage is a resourcing plan that may be linked to the ENH item in the **Related > Other** field.

**In progress**

- *UX Design*Technical and UX design is underway. The outcome of this stage is one or more design documents linked to the ENH in the **Related > Design** field.
- *In Development*Implementation of the enhancement is underway.
- *In Testing*Quality assurance and verification of the enhancement are underway.

**Deployed**

- *Limited Availability*The enhancement has been made available to a subset of customers. At this stage, the enhancement may be merged with an existing part or promoted to a new part.
- *General Availability*The enhancement has been made available to all customers. At this stage, the enhancement should be merged with an existing part or promoted to a new part.

**Inactive**

- *Deprecated*The enhancement has reached the end of its life and is no longer supported for customer use. Customer questions about the enhancement should be addressed by helping them migrate to the part with the replacement functionality or by recommending that they otherwise stop relying on the enhancement.
- *Deprioritized*Due to multiple reasons like bandwidth crunch or new emerging priorities, the decision-makers have decided not to work on the enhancement for the time being and will be inactive. This enhancement may be moved to the *In Progress* or *Prioritized* stages in the future to continue development.
- *Won't do*The decision-makers have decided not to implement the product enhancement idea.
- *Archived*The enhancement has been archived for long-term storage and historical reference. Archived enhancements are no longer active but can be referenced for future work or analysis.

## Related wiki nodes
- [[entities/enhancement]]

## Source
- DevRev support article [Enhancements](https://support.devrev.ai/en-US/devrev/article/AjBQbI4R) (ART-21873)
