---
title: Access control and data privacy
devrev_id: ART-23989
parent_directory: Computer by DevRev
translation_group: 8h8T7Tot
modified_date: "2026-05-01T02:32:15.845Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/8h8T7Tot"
tags: []
top_category: Computer by DevRev
wiki_match: glossary/mcp
match_score: 0.421
last_updated: 2026-05-11
summary: "As Computer connects to enterprise systems such as Salesforce, Google Drive, Jira, Slack, ensuring data privacy and controlled access is foundational to the product experience."
---

# Access control and data privacy

As Computer connects to enterprise systems such as Salesforce, Google Drive, Jira, Slack, ensuring data privacy and controlled access is foundational to the product experience. Our design approach focuses on creating a secure-by-default workspace with clearly defined permissions, user roles, and restricted policy changes.

Each Computer organization (org) contains only Computer-licensed users.

Users in a Computer org operate under default access policies that cannot be modified by end users. These policies restrict the ability to change [[entities/group|group]] structures, create new access roles, or alter visibility settings. This approach prevents accidental data exposure or privilege escalation while maintaining a consistent privacy posture.

Inviting new users adheres a configurable and auditable policy. By default, any user can invite others using verified work email addresses. Invites are scoped only to the org level, not to specific [[entities/group|groups]], reducing risk of over-permissioning. Computer Admins can optionally assign Admin roles during invitation.

The Computer org uses a minimal and clearly defined role structure:

**Computer Users**:

* Can read only those documents and objects that they have imported. Users cannot see data belonging to others unless it has been explicitly shared with them or imported by the user.
* Can invite new users subject to policy limits.
* Can execute [[glossary/airsync|AirSync]] to import data, as permitted by org policy.

**Computer Admins**:

* Manage user [[features/accounts|accounts]], billing, and org-level notifications.
* Can promote other users to Admin, but cannot delete the org directly; deletion requests must go through a controlled workflow.

This distinction ensures least-privilege access while still enabling smooth collaboration.

AirSync, our system automation layer, retains the necessary privileges to perform backend actions such as  managing data and policies.  This ensures that the platform functions correctly without exposing sensitive control surfaces to end users.

## Source
- DevRev support [[entities/article|article]] [Access control and data privacy](https://support.devrev.ai/en-US/devrev/article/8h8T7Tot) (ART-23989)
