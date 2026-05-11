---
title: Knowledge Base
type: feature
status: draft
sources: [raw/test-cases/by-feature/fe_knowledge_base.jsonl, raw/docs/devrev-developer-docs.md, raw/docs/devrev-docs-scraped.md, raw/docs/devrev-agent-dump-kb.md, raw/docs/devrev-agent-dump-settings.md, https://support.devrev.ai/en-US/devrev/directories]
related: ["entities/article", "features/customer-portal", "glossary/turing"]
last_updated: 2026-05-11
support_articles: [ART-21839]
---

# Knowledge Base

## What it does
The Knowledge Base feature manages articles, article translations, surfaces, and voting within DevRev. It provides a full article lifecycle including creation, retrieval, listing, counting, grouping, exporting, and updating. Articles support content blocks (parent-child structure), translations for multi-language support, unauthenticated access via org-level headers, surfaces for publishing to specific channels, and a voting system (upvote/downvote). With 493 test cases, it also touches brand management endpoints for knowledge base branding.

## Why it exists
Organizations need a centralized knowledge repository for both internal teams and external customers. The Knowledge Base powers help centers, documentation, and self-service support by allowing teams to author, translate, publish, and track engagement (votes) on articles.

## Key behaviors
- **Article CRUD**: Create, get, list, count, group, update, delete articles
- **Article types**: Supports standard articles and content block articles (child articles referenced by parent_article_id)
- **Unauthenticated access**: `articles.get` supports `permit_unauthenticated: true` using `X-Devrev-Dev-Org-Don` header instead of Bearer token
- **Schema completeness**: Responses include all mandatory fields: id, display_id, created_by, created_date, modified_by, modified_date, owned_by, title, status
- **Article export**: Async export support
- **Translations**: Create and list article translations for multi-language support
- **Surfaces**: List surfaces where articles are published
- **Voting**: Get and update votes (upvote/downvote); list voters per article with user-summary objects containing id and type fields
- **Ancestors**: Get article ancestor chain for hierarchical navigation
- **Brand integration**: Create, get, update brands associated with the knowledge base
- **Knowledge retrieval**: Get knowledge entries

## Entry points
- **Base URL**: `https://api.devrev.ai/internal/`
- Primary namespace: `articles.*`
- Requires `Authorization: Bearer $TOKEN` (except unauthenticated paths)
- Unauthenticated path: `X-Devrev-Dev-Org-Don` header

## API endpoints

| Endpoint | Methods | Description |
|----------|---------|-------------|
| `articles.create` | POST | Create article |
| `articles.get` | GET, POST | Get article (supports unauth) |
| `articles.list` | GET, POST | List articles |
| `articles.count` | GET, POST | Count articles |
| `articles.group` | POST | Group articles |
| `articles.update` | POST | Update article |
| `articles.export.async` | POST | Async export articles |
| `articles.ancestors` | GET, POST | Get article ancestors |
| `articles.translations.create` | POST | Create translation |
| `articles.translations.list` | POST | List translations |
| `articles.surfaces.list` | GET, POST | List article surfaces |
| `articles.voters.get` | GET, POST | Get vote for article |
| `articles.voters.list` | GET, POST | List voters |
| `articles.voters.update` | POST | Update vote |
| `brands.create` | POST | Create brand |
| `brands.get` | GET, POST | Get brand |
| `brands.update` | POST | Update brand |
| `knowledge.get` | GET | Get knowledge entry |

## Key Benefits
1. **Employee Efficiency**: Agents have a single source for solutions to customer queries, reducing dependence on other team members
2. **Reduced Support Load**: Customers can find answers by browsing the knowledge base, reducing need to create tickets
3. **Always-Available Information**: Customers can access the knowledge base at any time

## Article Creation — Step-by-Step

**Navigation path:** Settings > Support > Knowledge Base

1. **Open the KB:** Go to Settings > Support > Knowledge Base.
2. **Initiate creation:** Click the **+Article** button (top-right corner).
3. **Choose content type.** Three options:
   - **Write a new article** -- opens the rich-text editor.
   - **Add a link** -- paste a URL to an externally hosted article; opens in a new browser tab.
   - **Upload a file** -- PDF (opens in new tab) or MS Word document (downloads locally).
4. **Fill in article settings** (for native articles):
   - **Title** (text, required)
   - **Description** (text)
   - **Part** (dropdown, required) -- the product/feature the article addresses
   - **Owned by** (user picker, required) -- single point of contact
   - **Status** (dropdown) -- Draft, Published, Archived
   - **Collection** (dropdown) -- assigns the article to a topic category
   - **Visible to** (multi-select) -- controls audience visibility
5. **Create.** Click the **Create** button, which opens a dropdown with three sub-options:
   - **Create** (saves as draft)
   - **Create and submit for review**
   - **Publish**

## Article Lifecycle

| Status | Purpose |
|--------|---------|
| Draft | Unpublished, editable content |
| Published | Public-facing, customer-accessible |
| Archived | Outdated content, removed from active use |

### Publication Workflow
After creation, users can: save as draft version, submit for review, or publish immediately.

### Article Approval Workflow

There are two separate dimensions: **Status** and **Stage**.

**Stage options (approval workflow):**
- **No Stage** (default) -- no approval process started.
- **In Review** -- submitted for review; reviewers are notified.
- **Ready to Publish** -- all reviewers have approved.

**Transitions:** Draft -> submit for review -> In Review -> approved -> Ready to Publish -> Publish -> Published. Any stage can be reverted; a Publisher role is required to publish.

**Roles involved:**
- **Drafter/Approver** -- can draft, submit, approve, cancel reviews. Default for all users.
- **Publisher** -- can publish with or without approval. Must be assigned via Settings > User Management > Internal Groups > Publisher Group > + User.
- **Admin** -- all rights including deletion.

## Visibility Control
Article visibility is managed through the "Visible to" menu:
- **"Customers"**: Public access (requires public portal enablement)
- **"Verified Customers"**: Authenticated users only
- **"Customer Admins"**: Restricted to admin group members
- **Blank setting**: Internal-only access

## Article Scope & Access
- **Shared with:** Groups or individual users with roles (viewer, editor, owner).
- **Language:** language field (e.g., en-US); multi-language support via translation groups.
- **Collections:** Articles are organized into Collections.

## Content Formatting
The rich-text editor supports formatting through slash command "/" activation:
- Font styling and alignment options
- Hyperlinks, code blocks, and quotations
- Callouts, tables, and video embeds (YouTube, Loom, Vimeo, Wistia)
- Automatic table of contents generation via header labeling
- Text selection triggers a formatting bar with "Ask AI" feature for rephrasing, expanding, condensing, or correcting content

## Content Blocks
Reusable content snippets (text, images, tables, videos) that can be inserted into multiple articles. Updates to a block automatically reflect everywhere it is used. Managed at Settings > Support > Content Blocks. Insert into an article via the slash command `/` menu and selecting **Content Block**.

## Article Templates
Pre-built structures for consistency during creation. Create at Settings > Templates > + Create (select Article as object type). Use via Settings > Support > Knowledge Base > View Templates.

## Version Management
Every save creates a new version. Access via the **3-dot menu > Versions** on any article; click **Restore version** to revert to a previous iteration.

## Article Sharing
1. **External links**: Share with customers (requires Published status and appropriate visibility)
2. **Internal links**: Share with organizational team members

## Storage Specifications
- No limit on article quantity
- Maximum 250 MB per individual artifact
- Public portal requires enabling under **Settings > Plug & Portal > Portal Settings**

## Article Voting / Feedback

**Customer-facing feedback:**
- **Upvotes and downvotes** -- customers can rate articles directly on the portal.
- These are tracked in the Article Analytics dashboard under Settings > Support > Article Analytics.

**Article subscriptions (update notifications):**
- A **Subscribe** icon appears below the article title on the portal.
- Signed-in customers can subscribe; unsigned-in users are redirected to sign in first.
- When an article is updated, the owner can click Actions > Publish & Notify to email all subscribers.
- Email sender: *Article Subscriber bot*; subject: `[Company Name] Update on Article -- [Article Title]`.
- Requires the **Article Follow snap-in** to be installed first (Settings > Integrations > Snap-ins > All Snap-ins).

## Article Analytics
Customized prebuilt dashboard accessed via **Settings > Support > Article Analytics**:
- **Viewership** -- total views, unique views, viewership by user type, viewership by channel.
- **Engagement** -- average time spent on an article.
- **User feedback** -- upvote and downvote counts.
- Filter by date range using the **Date filter** at the top left.

## Bulk Operations
Supports simultaneous management of multiple articles: bulk deletion and status transitions (Draft to Published) through checkbox selection.

## All Surfaces Where Articles Appear

| Surface | How |
|---------|-----|
| **Customer portal / help center** | Browse by collection or search; public or verified-only. URL: `support.devrev.ai/<org-slug>` (see [[features/customer-portal]]) |
| **PLuG widget -- search bar** | AI-powered Turing search returns articles + generative answers |
| **PLuG widget -- Help tab** | Browsable collection-grouped article list |
| **Agent inbox / ticket view** | Turing suggests relevant articles to agents in context |
| **DevRev app global search** | `Cmd+K` / `Ctrl+K` surfaces articles in the KB section |
| **Email notifications** | Article subscription updates sent via email |
| **External link sharing** | Copy external link to share directly with customers |
| **Internal link sharing** | Copy internal link for team members |
| **PDF download** | Customers can download articles as PDF (if enabled) |

**Help center enablement:** Toggle under **Settings > Plug & Portal > Portal Settings > Help Center**. Enable both **Help Center** and **Public Portal** to make the knowledge base publicly accessible.

**Turing search in PLuG:** When enabled, search queries get a conversational AI-generated answer (not just a list of articles). Toggle: Settings > PLuG Settings > Turing Search.

**Open articles in PLuG:** A toggle in PLuG settings controls whether articles open within the widget or in a new browser tab.

## Q&A Objects
Separate from articles -- structured question-answer pairs used as an additional knowledge source for the AI (Turing) to answer customer queries. Unlike articles, **Q&As are never quoted as sources to the end user** -- they work silently in the background.

**Navigation:** Settings > Turing > Q&As

**When to use Q&As instead of articles:**
- Website FAQs you don't want publicly searchable as articles.
- Internal documentation not intended for public search.
- Bug/issue details that shouldn't be publicly visible but help the AI answer specific customers.

**Q&A fields:** Question, Answer, Part, Status (Published/Draft/Review Needed/Archived), Access Level (Private/Internal/Restricted or External/Public).

**Manual creation:** Click **+ QA** in the top-right corner of the Q&As page.

**Automatic creation:** Enable **Auto generate Q&As** via Settings > Turing > Q&As > Preferences. When a human agent resolves a conversation that the AI couldn't handle, the AI automatically drafts a new Q&A marked as Review Needed. The conversation owner is notified to approve or archive it.

## Collections

Collections are the parent categories (directories) for articles in the customer portal. They establish the hierarchical structure customers browse.

**Navigation:** Settings > Support > Article Collections

**Creating a collection:**
1. Go to Settings > Support > Article Collections.
2. Click **+Collection**.
3. Fill in: Title, Description, Parent (for nesting).
4. Enable **Publish Collection** toggle if you want it visible to customers.
5. Click **Create**.

**Sub-collections (nesting):** Click +Add next to an existing collection. Collections can be nested to create multi-level hierarchies.

**Deletion rule:** Cannot delete a collection if it has nested items inside it.

**Assigning articles to collections** -- two ways:
1. From the collection: click +Add next to the collection, or drag and drop an article.
2. From the article: set the Collection field when creating or editing the article.

**Reordering:** Drag and drop collections on the homepage or within another collection.

**Visibility rules:**
- If a collection is **not public**, none of its articles are visible to customers (even if articles are set to "Visible to Customers").
- If a collection is **public**, only articles set to "Visible to Customers" are publicly accessible.
- If a collection is public but all its articles are internal-only, the collection itself won't appear in the help center.

**Collections vs. Parts:** Collections organize articles on the customer portal. Parts represent the product/service structure. They are distinct.

## Related flows
- [gap] Article authoring and publishing flow
- [gap] Translation management flow

## Related scenarios
- [gap] Scenarios to be created from 493 test cases

## Open questions
- [gap] What is the relationship between knowledge.get and articles.get?

## Support documentation

Referenced DevRev support articles synchronized from [support.devrev.ai](https://support.devrev.ai/en-US/devrev/directories):

- [[support-articles/computer-plus-support/knowledge-base-overview|Knowledge base overview]] (ART-21839) — [external](https://support.devrev.ai/en-US/devrev/article/2cg8fV8N)
