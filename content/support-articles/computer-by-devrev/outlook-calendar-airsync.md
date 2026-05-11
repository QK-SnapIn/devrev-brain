---
title: Outlook Calendar AirSync
devrev_id: ART-22150
parent_directory: AirSync
translation_group: UHvBBKVn
modified_date: "2026-01-21T09:10:19.947Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/UHvBBKVn"
tags: []
top_category: Computer by DevRev
wiki_match: glossary/airsync
match_score: 0.85
last_updated: 2026-05-11
related: ['glossary/airsync']
---

# Outlook Calendar AirSync

## Supported objects

The following is a list of Outlook Calendar objects and their corresponding DevRev equivalents. Those marked as **Sync to DevRev** are eligible for import from Outlook Calendar to DevRev.

| **Outlook Calendar Object** | **DevRev Object** | **Sync to DevRev** |
| --- | --- | --- |
| Calendar Events | Meetings | ✅ |
| Attendees/Contacts | Contacts/DevUsers | ✅ |
| Categories | Tags | ✅ |
| Attachments & Transcripts | Attachments | ✅ |

 **Note:** Teams meeting transcripts are only available if meetings are recorded with transcription enabled and the organization has Teams Premium licensing.

## Import from Outlook calendar

Follow the steps below to import from Outlook Calendar:

1. Go to the **Marketplace**, search for **Outlook Calendar** in the **Import** category, and install.
2. Go to the **Import** section in your settings left nav.
3. Click **+Import** and select the **Outlook Calendar** logo.
4. Choose **Outlook Calendar** in the **Select Connection** dropdown.- If a connection already exists, you can reuse it; otherwise, click **Add Connection**.
   - Click **Sign in with snap-in** (with the Outlook icon) in the connection modal, enter a connection name, and proceed to authorise via your Microsoft account using OAuth 2.0.
   - **Admin Consent for Sensitive Scopes:** The application requests sensitive permissions (such as reading meeting transcripts, recordings, and files). An organisation administrator **must** check the box to **Consent on behalf of your organisation** in the Microsoft permission dialog. **Note:** Admin consent is mandatory for sensitive scopes. Once the admin authorizes these for the whole organization, individual users can subsequently consent to non-sensitive scopes for their own accounts.
   - Click **Accept** to complete the setup.
5. Select the calendars you want to import and specify the DevRev part where imported events should reside, after the connection is established. This initiates a bulk import.
6. Review the automatic field mapping from Outlook Calendar to corresponding DevRev fields.

The import time depends on calendar size and number of events and could range from seconds to several minutes.

### Configuration

The Outlook Calendar integration provides configuration options to control what data syncs and how privacy is handled.

**Organization-level settings:**

- **internal_domains** - List of internal email domains. Emails with these domains are considered internal and are used to distinguish Dev Users and Rev Users.
- **skip_events_with_emails** - Comma-separated list of email addresses. No meetings are created in DevRev for events where these emails appear as attendees, organisers, or creators.

**User-level settings:**

- **mark_external_meetings_private** - Enable to mark meetings with external attendees (from non-internal domains) as private in DevRev. Default is true.
- **skip_events_with_emails_user** - User-specific list of email addresses to exclude from sync.

 **Note:** These configuration options provide fine-grained control over what calendar events sync to DevRev and how privacy is handled.

## Limitations

- Meeting invitee RSVP details are available in a future update.
- Meeting attachments inherit permissions from the meeting object.

## Related wiki nodes
- [[glossary/airsync]]

## Source
- DevRev support article [Outlook Calendar AirSync](https://support.devrev.ai/en-US/devrev/article/UHvBBKVn) (ART-22150)
