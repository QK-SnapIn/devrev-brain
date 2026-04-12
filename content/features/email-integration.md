---
title: Email Integration
type: feature
status: draft
sources: [raw/docs/devrev-agent-dump-integrations.md]
related: [[features/airdrop]]
last_updated: 2026-04-12
---

# Email Integration

## What it does
The Email integration is listed among DevRev's available snap-in integrations and connects email channels to DevRev for inbound ticket/conversation creation and outbound communication.

## Why it exists
Customers and internal users communicate via email. This integration routes inbound emails into DevRev as tickets or conversations, and allows outbound replies from DevRev to flow back as email, maintaining threading and context.

## Key behaviors
- Listed as an available integration snap-in in the DevRev Marketplace.
- [gap] Channel configuration details (SMTP/IMAP settings, custom domain setup, email verification).
- [gap] Inbound email -> ticket/conversation creation flow (routing rules, auto-assignment, parsing behavior).
- [gap] Outbound email configuration (reply-from address, email templates, signature handling).
- [gap] Threading behavior (how DevRev maintains email thread continuity, In-Reply-To / References headers).

## Entry points
- **Marketplace:** Settings -> Snap-ins -> Explore Marketplace -> search "Email"
- [gap] Specific settings path for email channel configuration

## Related flows
- [gap] Inbound email to ticket flow
- [gap] Outbound reply from DevRev flow

## Related scenarios
- [gap] Scenarios to be created

## Open questions
- [gap] What email providers are supported (Gmail, Outlook, generic SMTP)?
- [gap] How does email-to-ticket routing work (regex, keywords, sender domain)?
- [gap] How is email threading maintained across DevRev conversations?
- [gap] What happens with attachments in inbound emails?
- [gap] Is there a spam/bounce handling mechanism?

**Note:** The source document (`raw/docs/devrev-agent-dump-integrations.md`) mentions Email as an available integration but does not provide detailed configuration or behavior documentation. Most sections above remain as gaps pending a more detailed source.
