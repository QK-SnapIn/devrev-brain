---
title: Customer Portal
type: feature
status: draft
sources: [raw/docs/devrev-docs-scraped.md, raw/docs/ devrev-agent-dump-kb.md, https://support.devrev.ai/en-US/devrev/directories]
related: ["features/knowledge-base", "features/brands", "entities/ticket", "entities/conversation", "entities/rev-user"]
last_updated: 2026-05-11
support_articles: [ART-21864, ART-21898, ART-23634, ART-24672, ART-27338]
---

# Customer Portal

## What it does
The customer portal (also called support portal) is an online platform enabling customers to interact with support teams, create tickets, track request progress, and search knowledge bases. Available in web and mobile formats (Android/iOS).

## Why it exists
Customers need self-service access to create and track support tickets, browse knowledge base articles, and communicate with support teams without relying solely on email or chat.

## Key Benefits
- **Enhanced customer experience**: Self-service access, ticket tracking, timely updates
- **Efficient ticket management**: Streamlined creation, assignment, and tracking
- **Seamless communication**: Threaded conversations eliminating email chains
- **Improved collaboration**: Team members can access and manage shared tickets

## Core Features

### Ticket Management
Customers create tickets with relevant details (description, priority, category). To create: Go to **+ Ticket**, enter title and description, click **Submit**. Supports custom and dependent fields. Customer admins can access all team-created tickets.

### Conversations and Messaging
Threaded conversations between customers and support representatives provide real-time updates and clarification within the same thread.

### Article Search
Supports both syntactic search (keyword-based) and semantic search (meaning/context-based) across published articles.

### Workspace Switching
Multi-workspace customers can switch between workspaces via profile picker without logging out.

### Multi-language Support
Portal localization serves customers in preferred languages. Configure via Portal localization settings.

### SEO Compatibility
Public articles are search-engine discoverable. Article titles serve as title tags; descriptions as meta descriptions.

**Sitemap location**: `https://<domain>/en-US/<dev-slug>/sitemap.xml`
**Home page location**: `https://<domain>/<locale>/<dev-slug>/directories`

## Getting Started

### Default Portal URL
Hosted at `support.devrev.ai/<yourcompany>` where workspace slug appears in Settings > General.

### Login Methods
1. **Email OTP**: Users enter email, receive one-time code, enter to log in
2. **Federated identity**: External identity provider (Okta, Azure AD, Google Workspace) via SAML/OIDC
3. **JWT-based authentication**: Custom integration with signed JWT tokens

### Customer Roles and Permissions
- **Verified Customers**: View only their own created tickets
- **Customer Admins**: View own tickets plus all organization member tickets. Multiple admins allowed per organization.

**Setup Instructions:**
1. Create account in Accounts section
2. Create contact in Contacts, link to account
3. For admins: Settings > User management > Groups > Customer Admins > Add User

## Portal Customization
Access via **Settings > Plug & Portal > Portal Settings** with real-time Live Preview.

### General Settings
- Knowledge base (on/off, access level)
- Ticket management (on/off, access level)
- Communication banner on ticket list
- AI search enablement
- PDF article export
- Article subscription feature
- Plug on portal

### Appearance Settings
- Theme: Dark or light mode
- Company assets: Name, logo, favicon
- Color tokens: Accent color
- Header tabs customization
- Hero section: Web/mobile banners, welcome text, search placeholder
- Footer: Social media and company links

### Help Center Configuration
**Navigation:** Settings > Plug & Portal > Portal Settings

**Enabling public access:** Go to Settings > Plug & Portal > Portal Settings > Help Center and enable both **Help Center** and **Public Portal**.

**URL patterns:**
- **Default URL:** `support.devrev.ai/<yourcompany>` (workspace slug)
- **Article URL pattern:** `https://<domain>/<locale>/<dev-slug>/article/<article-id>`
- **Homepage URL:** `https://<domain>/en-US/<dev-slug>/directories`

### Domain Setup
- **Custom domain** (e.g., `support.yourcompany.com`) -- requires a support ticket to configure (not self-serve).
- **Custom CSS** -- for fonts, spacing, component-level overrides beyond built-in themes -- requires a support ticket.
- **SEO enablement** -- requires a support ticket. Public articles are discoverable by Google. Article title = title tag; description = meta description.

## Just-in-Time (JIT) Access
JIT provisioning automatically creates user accounts upon login if contact doesn't exist. Contacts without mapped accounts can still log in under default workspace.

## Article Subscriptions
A **Subscribe** icon appears below article titles. Users must be signed in. Requirements:
1. Install Article Follow snap-in via Settings > Integrations > Snap-ins > All Snap-ins
2. Enable toggle in Settings > Plug & Portal > Portal Settings

Notifications send within 5-7 minutes of publishing.

## PDF Export
A **Download as PDF** option on each article. Enable via Settings > Plug & Portal > Portal Settings toggle. Available only for native DevRev articles.

## Troubleshooting

| Issue | Resolution |
|-------|-----------|
| Cannot log in | Verify email registered as customer; create contact if missing or enable JIT |
| Cannot view tickets | Verify tickets exist filtered by "Reported by"; check portal URL |
| Admin cannot see org tickets | Confirm correct portal URL; verify customer admin role assignment |
| Cannot add customer admin | Requires DevRev admin access |

## Entry points
- **URL:** `support.devrev.ai/<yourcompany>`
- Settings > Plug & Portal > Portal Settings (configuration)

## Portal Customization Details

### Appearance Customization
All appearance settings are under Settings > Plug & Portal > Portal Settings > Appearance. A **Live Preview panel** shows changes in real time before publishing (see [[features/brands]] for branding details).

### Multi-language Support
**Navigation:** Settings > Language & Region > Plug & Portal language settings

**How to add a language:**
1. Go to Settings > Language & Region > Plug & Portal language settings and add languages in the Customer Portal Language Settings section.
2. Go to Settings > Plug & Portal > Portal Settings and select the default language (en-US).
3. Configure global settings (KB, ticketing, AI search) -- these apply to all languages.
4. Customize language-specific fields (brand text, labels) for each language.
5. Click Apply Changes per language.
6. Enable the Publish toggle for each language independently.

**Static components** (e.g. "Search", navigation labels) are auto-translated. **Custom components** (company name, custom labels) must be translated manually.

**Language switcher behavior:**
- Customers accessing the portal URL without a language code see the default language (en-US).
- Appending a language code (e.g. `/fr-FR`) shows the translated version.
- If a translation doesn't exist, the customer lands on an error page with a link back to the homepage.
- **Search is language-scoped**: a customer on the Spanish portal sees only Spanish articles.

## Related flows
- [gap] Customer portal setup and configuration flow

## Related scenarios
- [gap] Scenarios to be defined

## Open questions
- [gap] What are the exact mobile app capabilities vs web?
- [gap] What are the JWT token requirements for custom authentication?

## Support documentation

Referenced DevRev support articles synchronized from [support.devrev.ai](https://support.devrev.ai/en-US/devrev/directories):

- [[support-articles/computer-plus-support/allowlist-domains-for-the-customer-portal|Allowlist domains for the customer portal]] (ART-23634) — [external](https://support.devrev.ai/en-US/devrev/article/6_lYKw2d)
- [[support-articles/computer-plus-support/customer-portal-setup-and-administration|Customer portal setup and administration]] (ART-21864) — [external](https://support.devrev.ai/en-US/devrev/article/mCD8f9oD)
- [[support-articles/computer-by-devrev/customer-roles|Customer roles]] (ART-21898) — [external](https://support.devrev.ai/en-US/devrev/article/VR92ky7P)
- [[support-articles/computer-plus-support/jwt-based-sso-for-the-customer-portal|JWT-based SSO for the customer portal]] (ART-27338) — [external](https://support.devrev.ai/en-US/devrev/article/N3bhguFi)
- [[support-articles/computer-plus-support/multilanguage-support-for-the-customer-portal-and-plug|Multilanguage support for the customer portal and Plug]] (ART-24672) — [external](https://support.devrev.ai/en-US/devrev/article/UTCG6oLa)
