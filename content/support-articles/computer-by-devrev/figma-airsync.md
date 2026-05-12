---
title: Figma AirSync
devrev_id: ART-22007
parent_directory: AirSync
translation_group: NGNnl50G
modified_date: "2026-01-05T05:52:11.177Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/NGNnl50G"
tags: []
top_category: Computer by DevRev
wiki_match: glossary/airsync
match_score: 0.85
last_updated: 2026-05-11
related: ['glossary/airsync']
summary: "The Figma AirSync simplifies migration from Figma to DevRev, supporting both one-time imports and ongoing syncs."
---

# Figma AirSync

The Figma [[glossary/airsync|AirSync]] simplifies migration from Figma to DevRev, supporting both
one-time imports and ongoing syncs.

## Set up the Figma connection

### Personal Access Token (PAT)

You can use a Personal Access Token with the following scope:

- **File Content - Read Only**: Required to access your Figma files and their
  content
- **Current user - Read Only**: Required to access user information
- **Projects - Read Only**: Required to access project information

## Supported objects

The following is a list of Figma objects and their corresponding DevRev
equivalents. Those marked as **Sync to DevRev** are eligible for import from
Figma to DevRev.

| Figma Object | DevRev Object | Sync to DevRev |
| --- | --- | --- |
| Files | [[entities/article|Article]] (URL) | ✅ |
| User | DevUser | ✅ |

## Import from Figma

Follow the steps below to import from Figma:

1. Go to **Marketplace**, [[features/search|search]] for **Figma**,
   and install the snap-in.
2. In the snap-in config modal, click **Install** then go to **[Settings](https://app.devrev.ai/?setting=airsyncs)**[ > ](https://app.devrev.ai/?setting=airsyncs)**[Integrations](https://app.devrev.ai/?setting=airsyncs)**[ > ](https://app.devrev.ai/?setting=airsyncs)**[AirSyncs](https://app.devrev.ai/?setting=airsyncs)**
   in the left nav.
3. Click **+Import** and select the Figma logo.
4. Create a new connection to your Figma [[entities/account|account]] by either:- Authorizing through OAuth, or
   - Providing your Personal Access Token (PAT)
5. Once the connection is established, select the Figma projects you want to
   import and specify the DevRev [[entities/part|part]] that should be used for any imported
   designs. This initiates a bulk import of the selected designs.
6. DevRev automatically maps the fields from Figma to the corresponding fields
   in DevRev. The duration of the import depends on the number and size of Figma
   files being imported. It can take seconds for [[features/accounts|accounts]] with only a few files
   to several minutes for accounts with many complex design files. DevRev honors
   the Figma API rate limits and back-off requirements to ensure smooth imports.

## Retrieve Team ID

You can retrieve your Figma Team ID from the URL. For example, in the URL:

```
https://www.figma.com/files/team/1234567890123456789/project/987654321/Team-Design-Project?fuid=0987654321098765
```

The Team ID is `1234567890123456789` which appears after `team/` in the URL.

## Related wiki nodes
- [[glossary/airsync]]

## Source
- DevRev support article [Figma AirSync](https://support.devrev.ai/en-US/devrev/article/NGNnl50G) (ART-22007)
