---
title: Gong AirSync
devrev_id: ART-22664
parent_directory: AirSync
translation_group: U3BHnxzm
modified_date: "2026-02-12T04:21:26.881Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/U3BHnxzm"
tags: []
top_category: Computer by DevRev
wiki_match: glossary/airsync
match_score: 0.85
last_updated: 2026-05-11
related: ['glossary/airsync']
---

# Gong AirSync

The Gong AirSync simplifies migration from Gong to DevRev, enabling seamless synchronization of sales call data, transcripts, and user information. This integration supports both one-time imports and periodic sync, bringing valuable conversation intelligence into your DevRev workspace.

### Supported objects

The following is a list of Gong objects and their corresponding DevRev equivalents. Those marked as **Sync to DevRev** are eligible for import from Gong to DevRev.

| Gong Object | DevRev Object | Sync to DevRev |
| --- | --- | --- |
| Users | DevUser | ✅ |
| Calls | Meeting (with rich descriptions) | ✅ |
| Transcripts | Attachment (linked to Meeting) | ✅ |
| Participants | RevUser (external only) | ✅ |
| Workspaces | Sync Unit (for workspace selection) | ✅ |

### Import from Gong

1. Log in to DevRev.
2. Navigate to **Settings > Integrations > Snap-ins**, search for **Gong** under **All Snap-ins**.
3. Click **Add and Install Snap-in**.
4. Navigate to **Settings > Integrations > Airsync** in the left-navigation.
5. Click **Airsync** in the top right corner and select **Gong**.
6. Create a new connection to authenticate with your Gong workspace, or use an existing active connection if you already have one.
7. Once the connection is established, select the Gong workspace you want to import and specify the DevRev part that should be used for any imported work. This initiates a bulk import of the selected sync.
8. DevRev automatically maps the fields from Gong to the corresponding fields in DevRev, including call metadata, transcripts, participant information, and user details.

## Create Gong connection

The Gong snap-in supports two authentication methods:

### Option 1: OAuth 2.0 (Recommended)

OAuth 2.0 provides secure, token-based authentication without sharing your API credentials.

Step 1: Create OAuth connection in DevRev

1. Navigate to **Settings > Connections**.
2. Click **New Connection**.
3. Select **Gong OAuth Connection**.
4. Enter a connection name.
5. Click **Authorize with Gong**.

Step 2: Complete OAuth authorization

1. You will be redirected to Gong's authorization page.
2. Log in to your Gong account if not already logged in.
3. Review the requested permissions (workspaces, calls, transcripts, users, media).
4. Click **Authorize** to grant access.
5. You will be redirected back to DevRev with the connection established.

Step 3: Start import

1. The OAuth flow automatically configures your API base URL.
2. On the next screen, select the authenticated Gong workspace from the list of available workspaces.
3. Specify the DevRev part where the imported content should reside.
4. Optionally configure time-scoped extraction to import data from a specific date range.
5. Click **Start** to trigger the import.

> OAuth Scopes Granted:
> 
> - `api:workspaces:read` - Access workspace information
> - `api:calls:read:basic` - Read basic call details
> - `api:calls:read:extensive` - Access detailed call data, participants, and analytics
> - `api:calls:read:transcript` - Read call transcripts
> - `api:calls:read:media` - Access call recordings
> - `api:users:read` - Read user information

### Option 2: API key authentication

For environments where OAuth is not available, use API Key authentication.

Step 1: Obtain Gong API credentials

1. Log in to Gong → **Admin Center > Settings > ECOSYSTEM > API > API KEYS**.
2. Click **Create API Key**.
3. Copy the Access Key and Access Key Secret.

Step 2: Create API key connection in DevRev

1. Navigate to **Settings > Connections**.
2. Click **New Connection**.
3. Select **Gong API Key Connection**.
4. Enter a connection name.
5. Provide your Gong Access Key.
6. Provide your Gong Access Key Secret.
7. Click **Submit** to authenticate.

Step 3: Start import

1. Select the authenticated Gong workspace from the list of available workspaces.
2. Specify the DevRev part where the imported content should reside.
3. Optionally configure time-scoped extraction to import data from a specific date range.
4. Click **Start** to trigger the import.

 Import duration varies from minutes to hours based on the number of calls, transcripts, and users in your Gong workspace.

## Limitations

While Gong Airdrop supports importing a wide range of content and metadata, the following are **not** imported or supported:

- **Unidirectional sync only** — Data flows from Gong to DevRev. Changes made in DevRev are not synced back to Gong.
- **No end date filtering** — Incremental syncs capture all calls from the start date onwards, including future scheduled meetings and updates to existing calls. A specific end date cannot be specified.
- **Recording URLs not included** — While Gong provides audio and video recording URLs in the API, these are not currently synced to DevRev meetings.
- **Workspace filtering limitations** — When fetching specific calls by ID, workspace filtering cannot be applied due to Gong API constraints.
- **Permission handling** — Permission-based access controls for different workspace types are not fully supported. If a workspace returns a 403 Forbidden error, it will be skipped with a warning.
- **No transactional guarantees** — If an import fails partway through, partial data may exist in DevRev without automatic rollback.
- **Participant affiliation ambiguity** — If participant affiliation (Internal/External) is not clearly specified in Gong data, participants default to external contacts.
- **Transcript size considerations** — Very long sales calls may produce large transcript files. All transcripts are formatted as text files with speaker names and timestamps.

These limitations exist due to differences in feature support between Gong and DevRev.

## Related wiki nodes
- [[glossary/airsync]]

## Source
- DevRev support article [Gong AirSync](https://support.devrev.ai/en-US/devrev/article/U3BHnxzm) (ART-22664)
