---
title: Articulate Reach 360 AirSync
devrev_id: ART-21992
parent_directory: AirSync
translation_group: _eS2rQAB
modified_date: "2026-02-21T13:04:26.046Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/_eS2rQAB"
tags: []
top_category: Computer by DevRev
wiki_match: glossary/airsync
match_score: 0.85
last_updated: 2026-05-11
related: ['glossary/airsync']
summary: "The Articulate Reach 360 AirSync simplifies migration from Articulate Reach 360 learning management system to DevRev, supporting both one-time imports and ongoing syncs."
---

# Articulate Reach 360 AirSync

The Articulate Reach 360 [[glossary/airsync|AirSync]] simplifies migration from Articulate Reach 360 learning management system to DevRev, supporting both one-time imports and ongoing syncs.

### Key features

- Complete learning management system data synchronization including courses, learners, and progress tracking.
- User profile sync with domain-based categorization into DevUsers (employees) and contacts (customers).
- Comprehensive course catalog extraction with metadata including titles, and content types.
- Detailed learner progress tracking with enrollment status, completion percentages, quiz scores, and learning duration metrics.
- [[entities/group|Group]] import and organizational hierarchy management.
- Learning [[features/analytics|analytics]] with cross-referential data for course-learner-user relationships and progress reporting.

## Supported objects

The following is a list of Articulate Reach 360 objects and their corresponding DevRev equivalents. Those marked as Sync to DevRev are eligible for import from Articulate Reach 360 to DevRev.

| Articulate Reach 360 object | DevRev object | Sync to DevRev | Sync to Articulate |
| --- | --- | --- | --- |
| Users (Employees) | DevUser | ✅ | ❌ |
| Users (Customers) | Contact | ✅ | ❌ |
| Courses | Custom Object (Courses) | ✅ | ❌ |
| Learners | Custom Object (Learners) | ✅ | ❌ |
| [[entities/group|Groups]] | Groups | ✅ | ❌ |

## Import from Articulate Reach 360

1. Go to the **Marketplace** and [[features/search|search]] for **Articulate Reach 360** in the **Import** category and install.
   2.In the snap-in config modal, enter the domain of your organization, such as devrev.ai for the DevRev organization, in the snap-in input for user categorization.
2. Click **Install**.
3. Go to the **Import** section in your settings left nav.
4. Click **+Import** and select the Articulate Reach 360 logo.
5. Create a new connection to your Articulate Reach 360 [[entities/account|account]] using your API key, or use an existing connection if you already have one.

You must provide a valid API key for Articulate Reach 360 API access. OAuth 2.0 authentication is not currently supported by the Articulate Reach 360 platform.

1. Once the connection is established, select the learning data you want to import and specify the DevRev [[entities/part|part]] to be used for any imported work.
2. DevRev makes an effort to automatically map the fields from Articulate Reach 360 to the corresponding fields in DevRev. However, you may be prompted to manually map certain fields if needed.

### Limitations

- Limited to API key authentication only; OAuth 2.0 not currently supported by Articulate Reach 360 platform.
- No delta synchronization capability; the Articulate Reach 360 API does not support fetching only changed/new data since last extraction, requiring full data extraction for each sync.

## Related wiki nodes
- [[glossary/airsync]]

## Source
- DevRev support [[entities/article|article]] [Articulate Reach 360 AirSync](https://support.devrev.ai/en-US/devrev/article/_eS2rQAB) (ART-21992)
