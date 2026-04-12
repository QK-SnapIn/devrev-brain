---
title: Analytics
type: feature
status: draft
sources: [raw/test-cases/by-feature/fe_analytics.jsonl, raw/docs/devrev-developer-docs.md]
related: ["features/vistas"]
last_updated: 2026-04-12
docs_url: https://docs.devrev.ai/dashboards/dashboard-creation
---

# Analytics

## What it does
The Analytics feature provides data querying, accelerator node management, and metrics ingestion for DevRev. It includes a natural language query execution engine that streams results via SSE (Server-Sent Events), accelerator node infrastructure management, and a metrics ingestion endpoint. With 75 test cases, this feature powers DevRev's analytics and reporting capabilities. Backend services include `us_oasis` and `us_pythagoras`.

## Why it exists
Organizations need to query their DevRev data for insights, reporting, and dashboarding. The Analytics feature provides a natural language query interface that streams progressive results, infrastructure for analytics acceleration, and an endpoint for ingesting custom metrics.

## Key behaviors
- **Natural language queries**: Execute analytics queries in natural language (e.g., "How many tickets were created in the last 7 days?")
- **SSE streaming**: Query results stream as Server-Sent Events with `Content-Type: text/event-stream`
- **Event schema**: Each SSE `data:` line contains JSON with `response` discriminator (`progress` or `result`); exactly one `result` event at stream end
- **Accelerator nodes**: Create (upsert semantics -- same client_id succeeds twice), list accelerator nodes
- **Field mapping asymmetry**: `public_key` is top-level in request but nested under `local_scope_config.public_key` in response
- **Metrics ingestion**: Ingest DevRev metrics data

## Entry points
- **Base URL**: `https://api.devrev.ai/internal/`
- Namespace: `analytics.*`, `metrics.*`
- Requires `Authorization: Bearer $TOKEN`

## API endpoints

| Endpoint | Methods | Description |
|----------|---------|-------------|
| `analytics.query.execute` | POST | Execute NL analytics query (SSE) |
| `analytics.accelerator-nodes.create` | POST | Create/upsert accelerator node |
| `analytics.accelerator-nodes.list` | GET | List accelerator nodes |
| `metrics.devrev.ingest` | POST | Ingest DevRev metrics |

## Dashboards vs Vistas

Dashboards and Vistas ([[features/vistas]]) are **separate concepts**:

| Aspect | Dashboards | Vistas |
|--------|-----------|--------|
| Purpose | Analytics-focused: charts, tables, graphs | Work management: filtered lists and boards |
| Content | Widgets backed by SQL queries | Direct views of work objects |
| Customization | Custom widgets with custom SQL | Column, filter, sort, group configuration |
| Location | Analytics section | Explore section / left nav |

## Stock Dashboards

| Dashboard | Description |
|-----------|-------------|
| Ticket insights | Ticket volume, trends, resolution metrics |
| Ticket-SLA analytics | SLA compliance and breach tracking for tickets |
| Ticket-Team performance | Per-team ticket handling metrics |
| Conversation insights | Conversation volume, trends, response metrics |
| Conversation-SLA analytics | SLA compliance and breach tracking for conversations |
| Conversation-Team performance | Per-team conversation handling metrics |
| Sprint insights | Sprint burndown, issues by stage/owner/priority/part, sprint health |

## Custom Dashboards
- Create custom dashboards with custom widgets (charts, tables, graphs)
- Widgets are backed by SQL queries against the DevRev data warehouse
- Docs: https://docs.devrev.ai/dashboards/dashboard-creation

## Dashboard Filters
- **Date** — time range selection
- **Tier** — filter by account/customer tier
- **Severity** — filter by ticket/incident severity
- **Spam** — include/exclude spam conversations

## Conversational Analytics (Text2SQL)
Ask questions in natural language via Computer/Search. The system translates to SQL and queries the DevRev data warehouse (`OasisSQLExecute`). Example: "Show me customer satisfaction trends this quarter."

## Export Options
- Export ticket views to CSV or JSON via Actions button (top-right of list view).

## Related flows
- [gap] Analytics query and visualization flow
- [gap] Accelerator node provisioning flow

## Related scenarios
- [gap] Scenarios to be created from 75 test cases

## Open questions
- [gap] How are accelerator nodes used in the analytics pipeline?
- [gap] What metrics can be ingested via the ingest endpoint?
- [gap] How does the SSE progress event differ from result event in terms of content?
