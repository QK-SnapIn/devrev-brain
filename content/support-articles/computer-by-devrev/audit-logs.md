---
title: Audit logs
devrev_id: ART-30929
parent_directory: Computer by DevRev
translation_group: _PyPN5SD
modified_date: "2026-04-24T07:09:10.66Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/_PyPN5SD"
tags: []
top_category: Computer by DevRev
wiki_match: log
match_score: 0.85
last_updated: 2026-05-11
related: ['log']
---

# Audit logs

Audit logs help your organization understand who accessed what in DevRev, and when. They support security reviews, periodic internal audits, and compliance oriented practices, for example, demonstrating access accountability under frameworks such as GDPR and HIPAA. Teams also use audit logs during security investigations to trace possible exposure and identify which identities may have accessed affected data.

## What gets logged

Audit logs capture all DevRev API calls, separated per workspace and partitioned by date and time. Every log entry includes the context needed to answer who made the call, when it occurred, and what was accessed or changed.

## Freshness and export time

* **Ingestion delay:** New activity can take approximately 10–15 minutes before it is available for export.
* **Export job duration:** Exports run asynchronously. Completion is often within a few minutes but can vary with the date range size and system load.

## Who can request exports

Only organization administrators who are members of the Admins group can initiate audit log exports.

## Request an export from the UI

1. Go to **Settings > Security > Audit Logs** in the DevRev app: `https://app.devrev.ai/<your-org-slug>/settings/security` Replace `<your-org-slug>` with the path segment that appears in your browser's address bar when you are working in that workspace.
2. Select the date range and any filters, then start the export. The export runs asynchronously; you receive a notification when it is ready.

## Request an export from the API

For programmatic exports, call the audit log export endpoint documented in the API reference: [Export audit logs](https://developer.devrev.ai/beta/api-reference/compliance/export-audit-logs).

**Authentication:** Use a **Personal Access Token (PAT)** belonging to an organization administrator.

**Parameters:** The export endpoint requires `from` and `to` timestamps to define the date range. Optional filters include `categories`, `operation_types`, and `users` to narrow results. See the [API reference](https://developer.devrev.ai/beta/api-reference/compliance/export-audit-logs) for full request and response details.

**Behavior:** The export API is **asynchronous**. After a successful run, the administrator who requested the export receives a **notification** containing a download link.

## Download the export

1. Open the **Updates** panel (bell icon) in DevRev and look under **Important** or **Others** for the export notification.
2. Click the download link in the notification to retrieve the export file. The export is delivered as a **presigned S3 URL** pointing to the log file.
3. Download links **expire after 8 hours**. If the link has expired, start a new export.

## Troubleshooting

* **Issue**: No notification is received after requesting an audit log export.

  **Solution**: Verify that DevRev Bot notifications are not muted. Go to your notification settings and ensure the DevRev Bot channel is enabled. Organizations on the Computer SKU may not receive export notifications because the notification service blocks them; contact DevRev support if this applies to your workspace.
* **Issue**: The download link has expired.

  **Solution**: Download links are valid for 8 hours. Request a new export from the UI or API to generate a fresh link.

## Related wiki nodes
- [[log]]

## Source
- DevRev support article [Audit logs](https://support.devrev.ai/en-US/devrev/article/_PyPN5SD) (ART-30929)
