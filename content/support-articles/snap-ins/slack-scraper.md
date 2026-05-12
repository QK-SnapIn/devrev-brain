---
title: Slack scraper
devrev_id: ART-21966
parent_directory: Automate
translation_group: B3PtAVDT
modified_date: "2025-12-10T06:57:32.405Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/B3PtAVDT"
tags: []
top_category: Snap-ins
wiki_match: features/slack-integration
match_score: 0.533
last_updated: 2026-05-11
summary: "The Slack scraper snap-in scrapes a channel of all messages, determines what of the conversation is important data and stores this parsed data into a DevRev article."
---

# Slack scraper

The [Slack scraper snap-in](https://marketplace.devrev.ai/marketplace/slack-scraper) scrapes a channel of all messages, determines what of the [[entities/conversation|conversation]] is important data and stores this parsed data into a DevRev [[entities/article|article]]. If the scraper is called again, it updates the article with data since the channel was last scraped.

## Configuration

1. Create a Slack app for your workspace at <https://api.slack.com/apps>.
2. In the **App features** section, generate agent token in **OAuth & Permissions**.
3. Give the app agent the following access:

   * `channels:history`
   * `channels:read`
   * `groups:history`
4. Invite the agent to the workspace.
5. Save the agent access token as a connection of type snap-in secret in the DevRev app.

## How to use

1. Install the snap-in.
2. In the **Configuration** tab, input the command `/slack_scrape <channelID>` once you have invited the agent into that channel.
3. Check the DevRev [[features/knowledge-base|knowledge base]] and there will be an article created with the channelID in the title and channelID set as the tag.

## Updating your articles

1. Go to the **Slack Scraper** snap-in.
2. Type the same command `/slack_scrape <channelID>` in the **Discussions** tab of the snap-in.
3. This will synchronize the [[entities/article|articles]] in the app with messages that have been sent in the Slack channel since the last modified date of the article. New articles which were not present earlier will be created.

## Source
- DevRev support article [Slack scraper](https://support.devrev.ai/en-US/devrev/article/B3PtAVDT) (ART-21966)
