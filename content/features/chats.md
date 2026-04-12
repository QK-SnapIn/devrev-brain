---
title: Chats
type: feature
status: draft
sources: [raw/test-cases/by-feature/fe_chats.jsonl, raw/docs/devrev-developer-docs.md]
related: []
last_updated: 2026-04-12
---

# Chats

## What it does
The Chats feature manages direct messages (DMs) and channel-based conversations within DevRev. It provides creation, retrieval, and listing of chats with support for type filtering, user association, pagination, and timeline info. With 60 test cases, this feature enables real-time internal communication. The backend service is `us_engage`.

## Why it exists
Team members need to communicate in real time within the DevRev platform. Chats provide DMs for 1:1 conversations and channels for group discussions, integrated directly into the product workflow.

## Key behaviors
- **Chat types**: `dm` (direct message) and `channel`; filter by type
- **DM creation**: Create DMs between users; `is_default: true` DMs silently suppress the `title` field
- **Conflict handling**: `get_if_conflict: true` makes creation idempotent for existing DMs
- **User filtering**: Filter DMs by associated users via `dm.users` parameter
- **Pagination**: Default limit 50; custom limit with cursor-based pagination (next_cursor, prev_cursor)
- **Timeline info**: Optional `timeline_info` map keyed by chat DON strings in list response
- **Tombstone users**: Deleted users appear in `chat.users` array with `state: "deleted"` rather than causing errors

## Entry points
- **Base URL**: `https://api.devrev.ai/internal/`
- Namespace: `chats.*`
- Requires `Authorization: Bearer $TOKEN`

## API endpoints

| Endpoint | Methods | Description |
|----------|---------|-------------|
| `chats.create` | POST | Create DM or channel |
| `chats.get` | GET | Get chat by ID |
| `chats.list` | GET | List chats with filters |

## Related flows
- [gap] DM creation and messaging flow
- [gap] Channel creation and membership flow

## Related scenarios
- [gap] Scenarios to be created from 60 test cases

## Open questions
- [gap] How does the timeline_info map get populated and what does it contain?
- [gap] Can channels be created with the same idempotency as DMs?
- [gap] What is the maximum number of members in a channel?
- [gap] How do chat notifications integrate with the broader DevRev notification system?
