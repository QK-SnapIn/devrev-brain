---
title: Google Calendar AirSync
devrev_id: ART-21976
parent_directory: AirSync
translation_group: FpwzcOH_
modified_date: "2026-02-23T03:53:54.429Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/FpwzcOH_"
tags: []
top_category: Computer by DevRev
wiki_match: glossary/airsync
match_score: 0.85
last_updated: 2026-05-11
related: ['glossary/airsync']
summary: "The Google Calendar snap-in brings your calendar events into DevRev, providing you to efficiently track your time commitments and interactions within DevRev."
---

# Google Calendar AirSync

The Google Calendar snap-in brings your calendar events into DevRev, providing you to efficiently track your time commitments and interactions within DevRev.

## Supported objects

The following is a list of Google Calendar objects and their corresponding
DevRev equivalents. Those marked as Sync to DevRev are eligible for import from
Google Calendar to DevRev.

| **Google Calendar Object** | **DevRev Object** | **Sync to DevRev** |
| --- | --- | --- |
| Transcripts | Attachments | ✅ |
| Customers | Customers | ✅ |
| Users | Identities | ✅ |
| [[entities/meeting|Meetings]] | Meetings | ✅ |

## Import Google Calendar

Follow the steps below to import from Google Calendar:

1. Go to the **Marketplace** and [[features/search|search]] for **Google Calendar** in the
   **Import** category, and install.
2. Go to the **Import** section in your settings left nav.
3. Click **+Import** and select the Google Calendar logo.
4. In the **Select Connection** dropdown, choose **Google Calendar**. If a connection already exists, you can reuse it; otherwise, click **Add Connection**. In the connection modal, click **Sign in with snap-in** (with the Google Calendar icon), enter a connection name, and proceed to **authorize via your Google [[entities/account|account]] using OAuth**. Provide the necessary permissions and click **Continue** to complete the
   setup.
5. Once the connection is established, select the calendars you want to import
   and specify the DevRev [[entities/part|part]] that should be used for any imported events. This
   initiates a bulk import of the selected calendar data.
6. DevRev attempts to automatically map the fields from Google Calendar to the
   corresponding fields in DevRev. Manual mapping may be required in some cases.

The duration of the import depends on the number of events and calendar size. It
may vary from a few seconds to several minutes.

## Configuration

The Google Calendar integration provides configuration options to control what data syncs and how privacy is handled.

### Privacy and visibility

All meetings brought in from Google Calendar—both internal and external—are **private** by default (visible only to [[entities/meeting|meeting]] participants and organizer ).

To make external meetings public while keeping sensitive meetings private, create a [[entities/group|group]] whose members are the people whose external meetings should stay private (e.g. executives, sensitive teams), then add that group under **Private Meetings [[entities/group|Groups]]** in Organization Settings. External meetings where any internal participant (organizer, creator, or attendee from your org) is a member of that group remain visible only to event participants; other external meetings are public.

### Organization-level Settings

- **Internal Domains** — Add your company's email domains (comma-separated) to identify internal vs external participants.
  *Example:* `devrev.ai, devrev-eng.com`
- **Private Meetings Groups** — External meetings where any internal participant (organizer, creator, or attendee) is a member of these groups will be visible only to event participants. When no groups are configured, all external meetings are private by default.
- **Groups Who Can Create Contacts** — Members of these groups can create Contacts from external meeting attendees.
- **Skip Events With Emails** — DevRev won't create a meeting for events where any of these email addresses appear as an organizer, creator, or attendee (comma-separated).
  *Example:* `john.doe@acme.com, brian@example.com`

### User-level Settings

- **Skip Events With Emails** — DevRev won't create a meeting for events where any of these email addresses appear as an organizer, creator, or attendee (comma-separated). User-specific list.
  *Example:* `john.doe@acme.com, brian@example.com`

### My settings (User-level configuration)

To configure user-specific settings, you must first enable personal settings:

1. In the Google Calendar Snap-in configuration page, scroll to the **My Settings** section.
2. Click the **"Enable for me"** toggle to activate your personal settings.
3. The **Configuration** section will appear with user-level options.
4. Configure your settings and click the **Save** button to apply your changes.
   

Note:  First, add the snap-in to the organization. Then, enter the organization-level and user-level configuration details and click **Save** to apply the changes.

## Related wiki nodes
- [[glossary/airsync]]

## Source
- DevRev support [[entities/article|article]] [Google Calendar AirSync](https://support.devrev.ai/en-US/devrev/article/FpwzcOH_) (ART-21976)
