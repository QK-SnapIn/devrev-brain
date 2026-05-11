---
title: January 2026
devrev_id: ART-23874
parent_directory: Changelog
translation_group: CIANX1Po
modified_date: "2026-04-24T15:27:16.629Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/CIANX1Po"
tags: []
top_category: Changelog
wiki_match: features/analytics
match_score: 0.381
last_updated: 2026-05-11
---

# January 2026

# Analytics Platform

### **Local timezone display for dashboards**

Your analytics dashboards now display data in your local timezone, making it easier to read and work with times that match your location.

**What's new**

* **Local timezone support**: Dashboard widgets now show dates and times in your local timezone instead of UTC.
* **Automatic conversion**: No manual configuration needed, your dashboard automatically adjusts to your timezone.
* **Consistent across widgets**: All dashboard visualizations display in the same local timezone for a unified view.

### **CSV export improvements for dashboard widgets**

We've made exporting data from dashboards and widgets easier and more useful. Here's what's new:

**Better data readability**

* Export files now show human-readable names instead of technical IDs. For example, tags and status values now display their actual names.
* Enum values like severity levels now show labels instead of codes
* Singular column is maintained for array type fields, such as **tags**, **reported by**

**Cleaner formatting**

* Column names in your export match exactly what you see in the UI.
* Date columns display correctly without formatting errors.
* Timezone is now consistent between what you see on screen and what exports.

**More usable exports**

* Column order in exports matches your widget layout.
* Export size limits of 50,000 rows ensure files stay manageable and download reliably

### **Reduced errors**

* Export failures now show clearer error messages to help you troubleshoot.

![paper-list-document-link.svg](https://app.devrev.ai/api/gateway/internal/artifacts.download?id=don:core:dvrv-us-1:devo/0:artifact/8937271&key=7a657f8e9aa29dea274017c575a012444d851aa3d69d8c35e3167737919ab08f) For more information about *Knowledge Graph*, refer to the following article: [Computer by DevRev](https:///devrev/settings/knowledge-base/articles/ART-21845)

# Build App

* Sprint analytics are now easily accessible directly from the sprint board.
* **Loop over sprints node**  
  Automates bulk operations across multiple sprints. Iterates over sprints based on their state: *planned*, *active*, or *completed*, to efficiently organize related work items.

![paper-list-document-link.svg](https://app.devrev.ai/api/gateway/internal/artifacts.download?id=don:core:dvrv-us-1:devo/0:artifact/8935885&key=89fc49d1e90e71ff6eda5b73bc879b979cae2310ab738d62d0503c8b638e4fab) For more information about *Sprint mode*, refer to the following article: [Computer for Builders](https://support.devrev.ai/devrev/article/ART-20079)

# Channels

* Enhanced the logic to hide previous email history in ticket replies.
* Introduced the ability to download Contact Control Panel (CCP) logs directly from error messages encountered during telephony calls. This feature enables quick access to logs for efficient issue analysis.
* Enhanced Slack messaging to use internal article links for internal channels and external links for external channels, helping users quickly access the appropriate articles.

![paper-list-document-link.svg](https://app.devrev.ai/api/gateway/internal/artifacts.download?id=don:core:dvrv-us-1:devo/0:artifact/8849444&key=8eae7a3a6ea1c9291e6f5ffcd1e64f222a0a0c07220bc2d146bbbb4d483c7024) For more information about *Channels*, refer to the following article: [[support-articles/computer-plus-support/computer-support|Computer for Support Teams]]

# Knowledge Graph

We're excited to introduce a new framework for search benchmarking at DevRev:

* **Automated dataset generation**: Golden datasets for search tasks can now be generated automatically, cutting annotation time by 90%.
* **Search evaluation framework**: Standardizes benchmarking for any search system, including DevRev Search, using Recall@K and Precision@K metrics.
* **Public DevRev dataset**: The DevRev articles search dataset is now publicly available for community use and benchmarking.
* **Model evaluation and leaderboard**: Six top embedding models from the MTEB leaderboard have been evaluated and ranked on a public leaderboard.
* **Best open source model identification**: Identifies the best open-source embedding model, achieving a ≥5% improvement in Recall@50 over DevRev Search, for use in the next reindexing.

These enhancements reduce benchmarking effort by over 90%, accelerate search improvements, and provide transparent, reproducible results for internal and community use.

![paper-list-document-link.svg](https://app.devrev.ai/api/gateway/internal/artifacts.download?id=don:core:dvrv-us-1:devo/0:artifact/8849437&key=dca7a854505b9ed6904f3d27d2d0d4d3fe2a8b90676d91b31f6c42485196d076) For more information about *Knowledge Graph*, refer to the following article: [Computer by DevRev](https://support.devrev.ai/devrev/article/ART-21845)

# Skill and Workflow Builder

* Introduces a centralized node that replaces deeply nested if/else chains, helping you design complex workflows with clearer logic and easier readability.
* Allows multiple execution paths to run in parallel from a single trigger, keeping related automation assembled in one workflow and improving structure, hygiene, and maintainability.

![paper-list-document-link.svg](https://app.devrev.ai/api/gateway/internal/artifacts.download?id=don:core:dvrv-us-1:devo/0:artifact/8849435&key=ed2faa5dc96490181c5fb035eb874e41cecd9d29e3956e6ec8d2dfe8cf8b4990) For more information about *Skill and Workflow Builder*, refer to the following article: [Computer by DevRev](https:///devrev/settings/knowledge-base/articles/ART-21845)

# Support App

* Introduced banner functionality that applies across all portal pages, allowing customers to display important updates or notifications as a header banner, visible to users regardless of their location on the portal.
* When a new organization is created, several default Snap-ins are automatically installed to streamline initial setup and improve operational efficiency. These include Assign Parts to Conversations, Ticket Tagger, Duplicate Email Tickets Tagger, Work Duration, CSAT, Automatic Customer Reply, Spam Shield, and more.
* Stock dashboard improvements:

  + Added extra filters to all stock dashboards, such as Tier, Severity, Spam.
  + Introduced new widgets including CSAT Dispatched vs. Received, Internal vs. External Tickets Created, Internal vs. External vs. Total Comments per User, and Average CSAT by SLA Status.

![paper-list-document-link.svg](https://app.devrev.ai/api/gateway/internal/artifacts.download?id=don:core:dvrv-us-1:devo/0:artifact/8849378&key=d301b6bbeaed0a535543f9c4e89eb07e56a9b39068924e8e82b840c6296b2390) For more information about *Support App*, refer to the following article: [[support-articles/computer-plus-support/computer-support|Computer for Support Teams]]

## Source
- DevRev support article [January 2026](https://support.devrev.ai/en-US/devrev/article/CIANX1Po) (ART-23874)
