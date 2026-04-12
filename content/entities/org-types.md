---
title: "DevRev Organization Types and Feature Limitations"
type: entity
status: draft
sources: [raw/exports/Org Types and Limitations.md]
related: ["features/identity", "features/agents", "features/analytics", "features/airdrop"]
last_updated: 2026-04-12
---

# DevRev Organization Types and Feature Limitations

## What it is
DevRev offers 7 organization tier types, each bundling different levels of AI, automation, integrations, and scalability. The tiers fall into three families: standalone Computer plans, Support Pro bundles, and Build Pro bundles.

## Tier Families

### Standalone Computer Plans
- **Computer Mini** — Entry AI for small teams
- **Computer Pro** — Full AI platform for mid-large teams
- **Computer Max** — Enterprise AI with maximum customization

### Support Pro Bundles
- **Support Pro + Computer Pro** — AI-powered support for mid-large support orgs
- **Support Pro + Computer Max** — Enterprise support AI with deep CX insights

### Build Pro Bundles
- **Build Pro + Computer Pro** — AI-powered dev for mid-large dev teams
- **Build Pro + Computer Max** — Enterprise dev AI with product intelligence

## Feature Availability Matrix

| Area | Computer Mini | Computer Pro | Computer Max | Support Pro + Computer Pro | Support Pro + Computer Max | Build Pro + Computer Pro | Build Pro + Computer Max |
| --- | --- | --- | --- | --- | --- | --- | --- |
| **Positioning** | Entry AI | Full AI platform | Enterprise AI | AI-powered support | Enterprise support AI | AI-powered dev | Enterprise dev AI |
| **AI Assistant** | Basic | Advanced | Advanced + tuned | Advanced for support | Highly tuned support AI | Advanced for dev | Tuned dev AI |
| **Search (Org data)** | Basic | Contextual | Deep + optimized | Context-aware tickets | Highly accurate support context | Dev-aware search | Org-wide deep search |
| **Automation** | Limited | Strong workflows + agents | Enterprise-grade automation | Ticket routing, replies | Full lifecycle automation | Dev workflows automation | Cross-system automation |
| **Agent Studio** | Not available | Available | Advanced | Support agents | Custom-trained agents | Dev agents | Advanced dev agents |
| **Analytics (AI insights)** | None | Conversational (Text2SQL) | Customized insights | Support analytics | Deep CX insights | Dev/product analytics | Product intelligence |
| **Integrations** | Limited | 100+ connectors | Custom connectors | Standard integrations | Custom integrations | Dev tools integrations | Fully customized |
| **Real-time sync (AirSync)** | No | No | Yes | No | Yes | No | Yes |
| **Customization** | Low | Medium | Very high | Medium | Very high | Medium | Very high |
| **Scalability** | Small teams | Mid-large teams | Enterprise scale | Mid-large support orgs | Enterprise support | Mid-large dev teams | Enterprise dev orgs |
| **Security & Compliance** | Basic | Standard | Enterprise-grade | Standard | Enterprise-grade | Standard | Enterprise-grade |
| **AI Accuracy** | Basic | High | Very high (fine-tuned) | High | Very high | High | Very high |
| **Applied AI Support** | No | No | Yes (Dedicated team) | No | Yes | No | Yes |

## Key Observations

- **AirSync** (real-time sync) is only available on "Max" tier plans (Computer Max, Support Pro + Computer Max, Build Pro + Computer Max).
- **Applied AI Support** (dedicated team) follows the same Max-only pattern.
- **Agent Studio** is unavailable on Computer Mini but available on all other tiers, with varying sophistication.
- **Analytics** is completely absent on Computer Mini; all other tiers have at least conversational analytics.
- **Enterprise-grade security** is only on Max tiers and their bundles.

## Impact on Testing
- Test automation must account for feature gating per org type. Tests for Agent Studio, AirSync, or Applied AI Support should be skipped or conditionally run based on org tier.
- [gap] Exact feature flag names or API parameters that control tier-based gating are unknown.
- [gap] Whether org type can be changed at runtime (upgrade/downgrade) and how that affects active sessions is not documented.
