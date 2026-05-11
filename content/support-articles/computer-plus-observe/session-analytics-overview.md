---
title: Session analytics Overview
devrev_id: ART-21841
parent_directory: Computer+ Observe
translation_group: izHP1lby
modified_date: "2026-03-16T17:46:17.329Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/izHP1lby"
tags: []
top_category: Computer+ Observe
wiki_match: features/analytics
match_score: 0.85
last_updated: 2026-05-11
related: ['features/analytics']
---

# Session analytics Overview

Session analytics is an advanced tool for user experience and behavior
analytics, designed to help businesses optimize their websites by providing
in-depth insights into user interactions. With session recordings, companies can
capture and replay user actions, analyze click patterns, and visualize user
flows, gaining a comprehensive understanding of user behavior and usability
challenges.

In addition to session replays, session analytics offers network and console log
tracking, delivering detailed information on failed API calls, performance
bottlenecks, and error messages. This detailed logging streamlines debugging and
accelerates issue resolution.

Session recordings and analytics are viewable in the
[[support-articles/computer-plus-observe/computer-for-user-insights|Session analytics and session replays dashboards]]. A key feature is funnel analysis,
which enables businesses to track user progression through specific conversion
paths. By identifying drop-off points, companies can fine-tune these stages to
improve conversion rates.

By leveraging these capabilities, businesses can make data-driven decisions,
enhancing the user experience and overall website performance.

## Enable session analytics

If you are not on our session recording plan, contact our support team to enable it.

1. Install the Plug SDK on your
   [website](https://developer.devrev.ai/sdks/web/installation) or
   [mobile app](https://developer.devrev.ai/sdks/mobile).
2. For web applications, configure
   [user identification](https://developer.devrev.ai/sdks/web/user-identity).
3. Enable session recording for your users, go to [**Settings** > **PluG and Portal** >
   **Session Replays**](https://app.devrev.ai/?setting=session-settings?) and enable recording for your desired platform.

   **Note**: Alternatively, you can enable session recording during Plug SDK
   initialization by setting the `enable_session_recording` option to `true`.
   However, this method does not allow you to manage session recordings through
   the settings page.
4. View Session recordings and analytics by going to **Explore** and searching for
   [[support-articles/computer-plus-observe/computer-for-user-insights|Session replays]].

For detailed instructions on session recording options, refer to
[[support-articles/computer-plus-observe/session-recording-options|Session recording options and data masking]].

## Track events

For detailed information about event tracking, refer to
[Track events](https://developer.devrev.ai/sdks/web/track-events).

## Related wiki nodes
- [[features/analytics]]

## Source
- DevRev support article [Session analytics Overview](https://support.devrev.ai/en-US/devrev/article/izHP1lby) (ART-21841)
