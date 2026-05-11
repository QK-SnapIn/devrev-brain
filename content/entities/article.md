---
title: Article
type: entity
status: stable
sources: [raw/docs/devrev-agent-dump-part2.md, raw/docs/ devrev-agent-dump-kb.md, https://support.devrev.ai/en-US/devrev/directories]
related: ["features/knowledge-base", "features/agents"]
last_updated: 2026-05-11
support_articles: [ART-21914, ART-22103]
---

# Article

## Description
An article is a knowledge base document used for internal documentation or customer-facing help content. Articles are the primary content type in the Knowledge Base feature.

## Lifecycle

**Status** (visibility dimension): Draft -> Published -> Archived

**Stage** (approval dimension): No Stage -> In Review -> Ready to Publish

Transitions: Draft -> submit for review -> In Review -> approved -> Ready to Publish -> Publish -> Published. Any stage can be reverted. A Publisher role is required to publish.

## Scope
- **Internal** -- visible to team members only.
- **External** -- visible to customers via help center, PLuG widget, and AI agent.

## Collections
Articles are organized into Collections for grouping and navigation.

## Language Support
- Language field (e.g., en-US).
- Multi-language support via translation groups.
- Translations managed via `articles.translations.create` and `articles.translations.list` API endpoints.

## Sharing & Access
- Shared with Groups or individual users.
- Roles: viewer, editor, owner.

## Q&A Objects
Separate from articles -- structured question-answer pairs used for AI deflection. Managed under Knowledge Base > Q&A. Used by [[glossary/turing]] for customer query resolution.

## Surfacing Methods
- Help center / Customer portal at `support.devrev.ai/<org-slug>`
- [[glossary/plug]] widget (AI agent searches articles)
- [[glossary/turing]] uses KB as primary information source
- "Turing suggests" on ticket view shows similar tickets and related articles

## Fields

| Field | Type | Notes |
|-------|------|-------|
| **Title** | Text | Required |
| **Description** | Text | Used as meta description for SEO |
| **Body / Content** | Rich text | Written in the RTE or imported |
| **Part** | Dropdown (product hierarchy) | Required; links article to a product/feature |
| **Owned by** | User picker | Single owner; required |
| **Authored by** | User (auto-set) | Who created the article |
| **Status** | Dropdown | Draft, Published, Archived |
| **Stage** | Dropdown | No Stage, In Review, Ready to Publish |
| **Collection** | Dropdown | Assigns to a collection/directory |
| **Visible to** | Multi-select group picker | Customers, Verified Customers, Customer Admins, or blank (internal only) |
| **Language** | Dropdown | e.g. en-US, es-ES, ja-JP |
| **Tags** | Multi-select | Free-form labels |
| **Created date** | Timestamp | Auto-set |
| **Modified date** | Timestamp | Auto-set |
| **Published date** | Timestamp | Set on publish |
| **Content format** | System field | `rt` (rich text), URL, or artifact |
| **Translation group** | System field | Links all language versions of the same article |
| **Storage limit** | System | Max 250 MB per article; no limit on article count |

API response mandatory fields: id, display_id, created_by, created_date, modified_by, modified_date, owned_by, title, status.

## Content Blocks
Articles can contain **content blocks** -- reusable content snippets (text, images, tables, videos) that can be inserted into multiple articles. Updates to a block automatically reflect everywhere it is used. Managed at Settings > Support > Content Blocks. Insert via the `/` slash command menu in the rich-text editor.

## Version Management
Every save creates a new version. Access via the **3-dot menu > Versions** on any article. Click **Restore version** to revert to a previous iteration.

## Analytics
Tracked in the Article Analytics dashboard at Settings > Support > Article Analytics:
- **Viewership** -- total views, unique views, viewership by user type, viewership by channel.
- **Engagement** -- average time spent on an article.
- **User feedback** -- upvote and downvote counts.
- Filter by date range using the Date filter at the top left.

## Creation Methods
- Quick Create (`+` button or `Cmd+K`)
- Knowledge Base settings UI (Settings > Support > Knowledge Base > +Article)
- API (`articles.create`)

### Creation Sub-Options
After filling in article settings, click **Create** for a dropdown with three sub-options:
- **Create** (saves as draft)
- **Create and submit for review**
- **Publish**

## Support documentation

Referenced DevRev support articles synchronized from [support.devrev.ai](https://support.devrev.ai/en-US/devrev/directories):

- [[support-articles/computer-plus-support/articles|Articles]] (ART-21914) — [external](https://support.devrev.ai/en-US/devrev/article/CsHTBzn7)
- [[support-articles/computer-by-devrev/freshdesk-articles|Freshdesk Articles]] (ART-22103) — [external](https://support.devrev.ai/en-US/devrev/article/5eFnYCLs)
