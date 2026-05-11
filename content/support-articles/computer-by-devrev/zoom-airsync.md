---
title: Zoom AirSync
devrev_id: ART-31615
parent_directory: AirSync
translation_group: t_VPPy46
modified_date: "2026-04-24T07:58:59.581Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/t_VPPy46"
tags: []
top_category: Computer by DevRev
wiki_match: glossary/airsync
match_score: 0.85
last_updated: 2026-05-11
related: ['glossary/airsync']
---

# Zoom AirSync

The Zoom AirSync simplifies migration from Zoom to DevRev, supporting both one-time imports and ongoing syncs of meeting data, participants, recordings, and transcripts.

## Supported objects

The following is a list of Zoom objects and their corresponding DevRev equivalents. Those marked as **Sync to DevRev** are eligible for import from Zoom to DevRev.

| Zoom Object | DevRev Object | Sync to DevRev |
| --- | --- | --- |
| User (licensed / internal) | DevUser | ✅ |
| Meeting participant (external) | RevUser | ✅ |
| Meeting | Meeting | ✅ |
| Cloud recording | Attachment (on Meeting) | ✅ |
| Meeting transcript | Article (KB) + Attachment | ✅ |

Each imported meeting is enriched with its host, participants, the recording URL, and when available a generated knowledge base article containing the transcript.

## Import from Zoom

Follow these steps to install the Zoom AirSync snap-in:

1. In the Snap-in Config Modal, search for **Zoom** under **All snap-ins**.
2. Click **Add** and **Install snap-in**.
3. Go to **Settings > Integrations > AirSyncs** in the left-hand navigation.
4. Click **AirSync** in the top-right corner and select **Zoom**.
5. Create a new connection to your Zoom account or use an existing one. See Create a Zoom connection.
6. Once the connection is established:

   1. In DevRev, go to **Settings > Integrations > AirSyncs**, then click **AirSync** in the top-right corner.
   2. Select **Zoom**.
   3. Select the connection you just created. Click **Next**.
   4. On the next screen, confirm the Zoom account whose meetings, users, recordings, and transcripts will be imported.
   5. Specify the DevRev part where the imported content should reside. This triggers a bulk import of the selected content.

DevRev automatically maps Zoom fields to corresponding DevRev fields (for example, meeting `topic` → title, `start_time` → scheduled date, `end_time` → ended date, `host_id` → created by / organizer, `join_url` → external URL). You may be prompted for manual mapping in some cases.

Import duration depends on the volume of Zoom data from a few seconds to several hours and is influenced by the number of meetings, the size of cloud recordings, and the availability of transcripts.

## Create a Zoom connection

The Zoom AirSync uses an OAuth2 connection to your Zoom account. An administrator connection is recommended so that meetings, participants, recordings, and transcripts across the organization can be imported.

1. Provide a name for the connection and click **Sign-in**.
2. You are redirected to Zoom to authorize access to your account.
3. Review the requested scopes (see Required scopes) and click **Allow**.
4. After successfully creating the connection, click **+AirSync** in the top-right corner and select the created connection.

Only data visible to the authorizing Zoom user is imported. For organization-wide imports, authenticate with a Zoom admin account that has the admin-level scopes listed below.

### Required scopes

The Zoom AirSync requests the following scopes on your Zoom account:

* **Users**: `user:read:list_users`, `user:read:user` (plus `:admin` equivalents) to list and read user profiles.
* **Meetings**: `meeting:read:list_meetings`, `meeting:read:meeting` (plus `:admin` equivalents) to list and read meeting details.
* **Participants**: `dashboard_meetings:read:list_meeting_participants` (plus `:admin`) to fetch participants for past meetings.
* **Cloud recordings**: `cloud_recording:read:list_recording_files` (plus `:admin` and `:master`) to list recording files per meeting.
* **Transcripts**: `cloud_recording:read:meeting_transcript:admin` to fetch meeting transcripts.
* **Reports**: `report:read:meeting`, `report:read:meeting:admin` to fetch meeting report data.

### What gets imported

* **Users**: Licensed Zoom users are imported as DevUsers; meeting participants who are not Zoom users are imported as RevUsers.
* **Meetings**: Past and scheduled meetings are imported with topic, agenda, host, participants, start/end time, duration, join URL, UUID, and state (scheduled or completed). The host is set as both **created by** and **organizer**.
* **Meeting visibility**: Meetings flagged as private in Zoom (`settings.private_meeting = true`) are imported with **Private** visibility in DevRev; all others are imported with **Internal** visibility.
* **Recordings**: Cloud recording files are attached to the corresponding meeting, and the primary recording URL is stored on the meeting's **Recording URL** field. Recordings that are not stored in Zoom Cloud cannot be imported.
* **Transcripts**: When a VTT transcript is available for a meeting, it is imported as a knowledge base article and linked to the meeting via the **Transcript article** field. The raw transcript file is also attached to the meeting.

Meetings without recordings or transcripts are still imported, but will not include the corresponding attachments or article.

## Post import options

After a successful import, you have the following options available:

* **Sync to DevRev**: Keeps data synchronized with DevRev, ensuring that new meetings, participants, recordings, and transcripts are continuously reflected.
* **View Report**: Access detailed information about the initial import and any subsequent syncs.
* **Delete Import**: Remove the import and all imported items from DevRev.
* **Edit Connection**: Modify the connection settings if needed.

## Sync to DevRev

After importing, you can enable sync to keep your content updated in DevRev. This feature ensures that any new or modified meetings, recordings, and transcripts are reflected in DevRev.

To perform a one-time sync to DevRev, follow these steps:

1. Go to **Settings > Integrations > AirSyncs**.
2. Locate the previously imported Zoom account.
3. Select **⋮ > Sync to DevRev**.

A one-time sync may overwrite fields in previously imported meetings and articles, even if they were modified in DevRev.

The Zoom AirSync supports incremental syncs using `modified_since` on the meetings endpoint, so subsequent syncs only fetch meetings that have been created or updated since the last successful sync.

## Historical AirSyncs

To view currently running and previous AirSyncs from various sources, do the following:

1. Go to **Settings > Integrations > AirSyncs**.
2. Select the import you want to view.
3. Select the context menu (**⋮**) **> View Report**.

## Periodic sync

After successfully importing to DevRev, you have the option to enable a periodic sync. This allows for automatic synchronization with DevRev on a regular basis. By default, the sync occurs once an hour.

To configure periodic sync, follow these steps:

1. Go to **Settings > Integrations > AirSyncs**.
2. Locate the previously imported Zoom account.
3. Select **⋮ > Set Periodic Sync**.

The **Enable automations for synced items** setting is optional and can be activated during periodic sync configuration. When enabled, newly created or updated items trigger events, which can initiate webhooks, notifications, Snap-ins, and other processes, as if the events originated directly in DevRev.

If this setting is disabled, updates will not trigger any event-driven processes. This behavior applies only to periodic syncs; no events are triggered during a first-time import or manual sync.

## Delete import

This deletes any content created by the import, including users, meetings, recordings, and transcript articles.

An import and all the content it creates can be deleted from DevRev. This can be useful when running POCs or to change the recipe used during the import. Once an import has been deleted, all the content it created gets deleted, even if it was modified in DevRev. It's possible to import the Zoom account again after deletion.

To delete an import and all the content it created, go to **Settings > Integrations > AirSyncs**, find the previously imported Zoom account, and select **⋮ > Delete Import**.

## Limitations

* **Extraction-only.** The Zoom AirSync does not push changes from DevRev back to Zoom. Edits made in DevRev to imported meetings, articles, or users are not reflected in Zoom.
* **Cloud recordings only.** Recordings stored locally on a participant's device are not accessible via the Zoom API and cannot be imported.
* **Transcript availability.** Transcripts are only imported for meetings where cloud recording transcription was enabled and the transcript has finished processing in Zoom.
* **Rate limits.** The Zoom API enforces per-account rate limits. The snap-in honors `Retry-After` headers on `429` responses with exponential backoff, so imports of large accounts may take longer during peak hours.

## Related wiki nodes
- [[glossary/airsync]]

## Source
- DevRev support article [Zoom AirSync](https://support.devrev.ai/en-US/devrev/article/t_VPPy46) (ART-31615)
