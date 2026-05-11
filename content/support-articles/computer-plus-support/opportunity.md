---
title: Opportunity
devrev_id: ART-21880
parent_directory: Customer records
translation_group: VSU6Qz6K
modified_date: "2025-12-10T06:56:38.755Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/VSU6Qz6K"
tags: []
top_category: Computer+ Support
wiki_match: entities/opportunity
match_score: 1.0
last_updated: 2026-05-11
related: ['entities/opportunity']
---

# Opportunity

An opportunity record represents a potential source of revenue for your organization. Opportunities feature customizable states and stages that communicate their position within the sales pipeline.

You can link opportunities to an account, tickets, and conversations which could lead to a potential source of revenue.

## Create an opportunity

1. Go to [**Explore** > **Opportunities**](https://app.devrev.ai/?vista=vista-def-opportunities), and click **+ Opportunity**.
2. Fill in the title, description, owner, and account it's associated with.
3. Toggle on **Create multiple** to create opportunities with the same attributes.
4. Click **Create**.

![Opportunity](don:core:dvrv-us-1:devo/0:artifact/4100317)

### Opportunity attributes

Opportunities have attributes that can be used to filter and group them in various views.
You can find all the stock attributes listed under [**Settings** > **Object customization** > **Opportunity**](https://app.devrev.ai/?setting=object-customization?type=opportunity), and click > **Stock fields**.
These are the stock attributes that come with DevRev:

* **Account**: The account associated with the opportunity.
* **Owner**: The person responsible for the opportunity. Opportunities are assigned to sales representatives or customer-facing team members through the **Owner** attribute.
* **Stage**: The current state of the opportunity. The stage attribute is used to track the progress of the opportunity through its lifecycle. The following are opportunity stages:

  + **Open**: *Stalled*
  + **In Progress**: *Validation*, *Negotiation*, *Contract*
  + **Closed**: *Closed Won*, *Closed Lost*
* **Total value**: Total size of the opportunity.
* **Forecast category**: Pipeline, omitted, upside, strong upside, commit, won.
* **Created by**: The person who created the opportunity.
* **Created date**: The date the opportunity was created.
* **Modified date**: The date the opportunity was last modified.
* **Tags**: Tags are used to categorize opportunities.
* **Modified by**: The person who last modified the opportunity.

These attributes can be effectively used in filters and **Group** conditions across various vistas in DevRev to track specific work, capacity, and more.

You can add custom attributes to opportunities to track additional information. For more information on custom attributes, see [[support-articles/computer-by-devrev/object-customization|object customization]].

## Stages

This diagram represents the **Opportunity Transitions** workflow in DevRev, organized into three main groups:

* **📂 Open**: Initial opportunity assessment stage (Qualification)
* **⚡ In Progress**: Active sales process stages (Stalled, Validation, Negotiation, Contract)
* **🔒 Closed**: Final states for opportunities (Closed Won, Closed Lost)

The workflow supports flexible sales processes with the ability to handle stalled opportunities and provides multiple paths to closure. Opportunities can be reopened from any closed state.

![Opportunity Transitions Diagram](don:core:dvrv-us-1:devo/0:artifact/4100318)

**Open**

* *Qualification*

  Initial assessment stage where potential opportunities are evaluated for viability, fit, and potential value. This stage involves gathering information about the customer's needs, budget, timeline, and decision-making process.
* *Stalled*

  Opportunities that are temporarily paused due to various reasons such as customer delays, internal resource constraints, or external factors. These can be reactivated when conditions change.

**In Progress**

* *Validation*

  The opportunity has been qualified and is being validated through deeper discovery, proof of concept, or pilot programs to confirm the customer's needs and solution fit.
* *Negotiation*

  Active negotiation of terms, pricing, and contract details with the customer. This stage involves back-and-forth discussions to reach mutually acceptable terms.
* *Contract*

  Final contract preparation and review stage. Legal and commercial terms are being finalized before closing the deal.

**Closed**

* *Closed Won*

  The opportunity has been successfully closed and the deal has been won. The customer has committed to the solution and contracts have been signed.
* *Closed Lost*

  The opportunity has been closed without success. The deal was lost to a competitor, the customer decided not to proceed, or other factors prevented closure.

## Related wiki nodes
- [[entities/opportunity]]

## Source
- DevRev support article [Opportunity](https://support.devrev.ai/en-US/devrev/article/VSU6Qz6K) (ART-21880)
