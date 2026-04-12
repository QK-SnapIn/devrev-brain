---
title: PLuG Widget
type: feature
status: draft
sources: []
related: [[features/conversations-feature]], [[features/agents]], [[features/knowledge-base]], [[features/customer-portal]], [[glossary/plug]]
last_updated: 2026-04-12
docs_url: https://docs.devrev.ai/plug
---

# PLuG Widget

Branded as **"Computer for Your Customers"**.

## What it does
The PLuG widget is DevRev's in-app widget SDK that provides a major customer-facing surface. It embeds directly into customer applications to deliver live chat, AI-powered search, session analytics, nudges, push notifications, and portal access.

## Why it exists
Enables end-users to get support, search knowledge, and interact with AI agents without leaving the product. It is the primary channel for real-time customer engagement.

## Sub-components

### Widget (embeddable chat)
- Customizable branding, launcher, layout, and tabs
- [gap] How does live chat initiate? Auto-greeting? User-triggered?
- [gap] Routing rules for chat — does it go to Inbox?
- [gap] Chat-to-ticket conversion flow from PLuG

### AI-powered search
- Semantic search over tickets and articles
- **Web SDK only** — not available on mobile SDKs
- [gap] Which agent handles PLuG search? Search Agent?
- [gap] How are search results ranked?

### Session recording & analytics
- Captures: screen recordings, click events, rage clicks, dead clicks, form changes, network calls, console errors
- Sessions last up to **4 hours** and end after **30 minutes of inactivity**
- Supports **data masking** for privacy (PII redaction)

### Nudges
- Outbound proactive messages ([[glossary/nudge]]) to engage users
- Configurable by page URL, frequency, and audience
- **Web SDK only** — not available on mobile SDKs
- [gap] What types of nudges exist? Banner, modal, tooltip?

### Push notifications
- **Mobile SDK only** (iOS, Android, React Native)
- Triggered on: agent replies, ticket status changes, conversation activity

### Customer portal integration
- [gap] How does PLuG connect to the customer portal?
- [gap] Can users view/create tickets through PLuG?
- [gap] JIT access flow from PLuG

## SDKs
| SDK | Platform |
|-----|----------|
| Web | Browser-based web applications |
| iOS | Native iOS applications |
| Android | Native Android applications |
| React Native | Cross-platform mobile via React Native |

## User identity types
PLuG supports three user identity modes:
1. **Anonymous** — no identity provided; temporary session user
2. **Unverified** — identifier provided but not cryptographically verified
3. **Verified** — identifier verified via token/signature; full identity assurance

## Entry points
- Embedded in customer web/mobile apps via SDK
- Docs: https://docs.devrev.ai/plug

## Configuration
- Widget customization: branding, launcher icon, layout, tabs
- [gap] Feature toggles (enable/disable chat, search, nudges independently)
- [gap] Multi-brand PLuG configuration

## Related flows
- [[flows/critical-product-flows]] (conversation initiation)
- [[flows/client-critical-journeys]] (client-side user journeys relevant to PLuG surfaces)

## Related scenarios
(none yet)

## Open questions
- [gap] How does PLuG interact with the Turing agent?
- [gap] Rate limits or concurrent session limits?
- [gap] Offline/degraded mode behavior?
