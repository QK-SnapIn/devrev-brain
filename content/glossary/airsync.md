---
title: AirSync
type: glossary
status: stable
last_updated: 2026-04-12
---

# AirSync

Near real-time bidirectional sync between DevRev and external systems. Runs at approximately 5-minute intervals. Supports permission syncing from external systems into DevRev.

**Key difference from Airdrop:** [[glossary/airdrop]] is a one-time or periodic import engine. AirSync maintains continuous, bidirectional synchronization.

AirSync may create [[entities/dev-user]] Shadow Users to track external user activity without granting app access.

See [[features/airdrop]] for the integration framework.
