---
title: Computer for User Insights
devrev_id: ART-21917
parent_directory: Computer+ Observe
translation_group: v4whY8L3
modified_date: "2026-03-04T06:53:43.909Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/v4whY8L3"
tags: []
top_category: Computer+ Observe
wiki_match: flows/client-critical-journeys
match_score: 0.507
last_updated: 2026-05-11
summary: "Computer for User Insights is a comprehensive toolkit for unraveling user behavior within DevRev platform."
---

# Computer for User Insights

Computer for User Insights is a comprehensive toolkit for unraveling user behavior within DevRev platform. A session is captured when a user launches your application, which initializes the Session [[features/analytics|Analytics]] SDK. The SDK then tracks and captures all screens, events, API service calls, exceptions (such as crashes and ANRs), errors, and gestures (including scrolls, taps, and rage taps).

## Session Replays

![Session replays](don:core:dvrv-us-1:devo/0:artifact/4100534)

You can [[features/search|search]] for **Session Replays** in **Explore** page where you can see the sessions for your Web app and sessions for Android and iOS on mobile.

* View sessions by platform and time.
* Apply simple filters such as **Platform**, **Session duration**, **Date range**, etc.
* Jump into session replays for deeper investigation.

In the top-center, next to the app name, you find a toggle for **Android**, **iOS**, and **Web**. Use this toggle to view the data for each platform.

## Playback of user interactions

Clicking a specific user replays sessions for that user, which lets you dive deep into each session in detail.

The timeline interface offers a chronological breakdown of user interactions, highlighting clicks, events, and associated properties.

For web sessions, tabs reflect the user's browsing history, while the comments section enables team collaboration and discussion.

![Session playback](don:core:dvrv-us-1:devo/0:artifact/4100540)

For mobile sessions, recordings shows the users screen recording and navigation.

![mobile playback](don:core:dvrv-us-1:devo/0:artifact/4100542)

## DevTool technical insights (Web only)

![Session DevTool](don:core:dvrv-us-1:devo/0:artifact/4100546)

DevTool provides developers with logs, errors, and network details to diagnose and fix [[features/issues|issues]].

1. Click **DevTools** to the right of the playback window.
2. Below the playback window, the network information of all the web requests made and console errors from the browser are displayed in **Network** and **Console** tabs.

## Session terminology

* Session types

  *Frustrated sessions* are those where one or more metrics indicate user frustration during the session.

  *Tolerating sessions* are those where one or more metrics indicate users are just tolerating the experience.

  *Satisfied sessions* are those with no tolerating or frustrated metrics, indicating a positive user experience.
* *Hot launch*

  When a user brings the app from the background to the foreground.
* *Cold launch*

  When a user opens the app for the first time and not from a minimized state.
* *Rage taps or clicks*

  Multiple taps or clicks on a screen element in quick succession, typically indicating user frustration with a malfunctioning element. Rage taps are identified when there are three or more taps within a 5-pixel area, each occurring within 600ms of the previous tap.
* *Dead taps or clicks*

  Taps or clicks on seemingly interactive elements that have no response, causing user confusion and potential frustration.
* *Active app versions*

  The different versions of the app currently being tracked and used by users.

## Session Analytics: Web

![Session web](don:core:dvrv-us-1:devo/0:artifact/4100548)

A **web session** consists of the following:

* **Screen recording** of the application, captured by the [[glossary/plug|Plug]] SDK through DOM mutation tracking.
* **Auto-captured events** (also called *Stock events*), such as Click, Dead Click, Rage Click, Form Change.
* **Custom events**, fired during SDK integration to log specific product interactions.
* **Network calls**, captured and associated with the session.
* **Console errors**, such as uncaught exceptions or warnings.

**Session lifecycle:**

* A web session begins when a user opens a webpage.
* It can last for up to **4 hours**, but ends if the user remains inactive for **30 minutes**.
* If the user resumes activity after this inactivity period, a **new session** is started—even if they stay on the same page.
* A single session can include **multiple tabs**, representing different browser tabs opened by the user during that session.

Session Analytics: Web dashboard consists of the following dashboard widgets and tabs.

### Tabs

1. **Web**

   Widgets and visualizations for all web sessions.
2. **Network**

   APIs with frequent errors, slow response times, and highest usage.
3. **Events**

   Most frequently emitted custom events, and distribution of dead and rage clicks across pages.

### Dashboard widgets

Each tile in the Dashboard has a download icon. Click this icon to download the data.

1. **Total Sessions**

   The total number of user sessions recorded during the selected date range. This reflects overall traffic volume and how often the platform is being accessed.
2. **Total Unique Users**

   The number of distinct individuals who accessed the platform in the specified time frame. This helps measure audience size and platform reach.
3. **Average Sessions Per User**

   The average number of sessions generated by each unique user. Higher values suggest stronger engagement or repeat usage patterns.
4. **Sessions Per Day**

   A daily breakdown of the number of sessions recorded. Useful for identifying usage patterns, peak activity days, and seasonality.
5. **Most Active Verified Users**

   Logged-in users with the highest number of sessions. These are your most engaged users, often ideal for feedback, early feature testing, or targeted communication.
6. **Most Active Customer Workspaces**

   Workspaces or customer [[features/accounts|accounts]] with the most sessions. Indicates which customers are deriving the most value from the platform and may warrant closer support or expansion [[entities/opportunity|opportunities]].
7. **Popular Pages**

   The most frequently visited URLs across the platform. These are typically your highest-performing pages and can reveal what users find most valuable.
8. **Sessions with % Rage Clicks**

   The percentage of sessions that included at least one rage click—rapid repeated clicking on an element. This is a strong signal of user frustration or unresponsive UI elements.
9. **Sessions with % Dead Clicks**

   The percentage of sessions that included at least one dead click—clicks on elements that [[glossary/don|don]]’t produce a response. Dead clicks often point to broken links or confusing interface design.
10. **Average Rage Clicks Per Session**

    The average number of rage clicks made during a session. A rising average may indicate a growing UX [[entities/issue|issue]] or user dissatisfaction.
11. **Average Dead Clicks Per Session**

    The average number of dead clicks per session. This metric helps surface broader UI reliability issues even when individual dead clicks are minor.
12. **URLs with Rage Clicks**

    Pages where users frequently rage click. These pages likely contain frustrating or misleading elements that require UX improvements.
13. **URLs with Dead Clicks**

    Pages where users often click on non-responsive elements. These highlight [[features/parts|parts]] of the interface that may not be working as expected.
14. **Sessions with % JS Errors**

    The percentage of sessions that experienced at least one JavaScript error. A high percentage may suggest performance instability or poor code execution affecting user experience.
15. **JS Errors**

    The most frequently occurring JavaScript errors across all sessions. These errors often lead to broken functionality and should be prioritized for engineering fixes.
16. **URLs with High Response Times**

    Pages with the slowest loading or response times. These may be causing user drop-off or dissatisfaction due to delayed interactions.
17. **Platform Distribution**

    A breakdown of sessions by device type (desktop, mobile, tablet). Understanding this helps with responsive design prioritization and tailoring the experience across platforms.
18. **OS Distribution**

    Sessions categorized by operating system, such as Windows, macOS, Android, or iOS. This helps QA and development teams optimize and test for the right environments.
19. **Browser Distribution**

    Sessions segmented by browser type (for example, Chrome, Safari, Firefox). This helps ensure compatibility and performance across the most-used browsers by your users.

## Session Analytics: Mobile

![Session mobile](don:core:dvrv-us-1:devo/0:artifact/4100552)

A **mobile session** includes:

* **Screen recording**, captured by the Plug SDK through periodic screenshots of the user interface.
* **Auto-captured events**, such as Tap, Rage Tap, Swipe, etc.
* **Custom events**, triggered through SDK integration.
* **Network calls**

**Session lifecycle:**

* A mobile session starts when a user opens the app.
* Unlike web sessions, there is **no time limit** on session length.
* A session contains multiple **recordings**:

  + A **recording** ends when the app is backgrounded.
  + A **new recording** starts when the app comes to the foreground again.
  + The **session ends** when the app is killed, or it crashes, or it becomes non-responsive, or after 30 mins of inactivity.
  + Sessions are **uploaded** the next time the app is launched.

Session Analytics: Mobile dashboard consists of the following dashboard widgets and tabs.

### Tabs

1. **Sessions**

   Widgets and visualizations for all the mobile sessions.
2. **Screens**

   Top screens and screens with crashes, errors, rage taps, and ANR.
3. **Events**

   Most frequently emitted custom events across screens.
4. **APIs**

   APIs that frequently error out, respond slowly, and are most popular.

### Dashboard widgets

Each tile in the Dashboard has a download icon. Click this icon to download the data.

1. **Total Sessions**

   The total number of recorded user sessions within the selected period, showing overall platform usage and activity levels.
2. **Total Distinct Users**

   The number of unique individuals who initiated at least one session. This reflects the reach of your platform during the timeframe.
3. **Average First User Interaction Time**

   The average time taken by users to make their first interaction (for example, tap, scroll) after a session begins. A shorter time indicates faster user engagement; a longer time may suggest loading delays or poor onboarding flow.
4. **Average Session Duration (in seconds)**

   The mean duration of user sessions, measured in seconds. Longer durations often signal higher user engagement, while extreme values (for example, 8M+ seconds) may suggest a tracking issue or inactive sessions left open.
5. **Session % with Crashes**

   The percentage of sessions that ended due to an app crash. Ideally close to zero, this metric helps track overall app stability.
6. **Session % with Rage Taps**

   The percentage of sessions where users tapped on the same spot—typically out of frustration. High values may indicate unresponsive elements or confusing design patterns.
7. **Session % with UI Freeze**

   The percentage of sessions in which the UI froze or became unresponsive. Even a small percentage here warrants performance optimization to prevent churn.
8. **Sessions Per Day**

   A day-by-day count of sessions across the selected date range. Helps visualize usage trends, spikes, or lulls in activity.
9. **App Version Trend**

   Session volume by app version over time. This helps monitor the adoption of new releases and detect any performance regressions or bugs introduced in specific versions.
10. **Exceptions Time Trend**

    The frequency of app exceptions over time. This helps identify whether error rates are rising and if they correlate with new updates or feature rollouts.
11. **Most Active Users**

    A ranked list of users (by anonymized ID) based on session count. These are your most engaged users and can be valuable for feedback loops or early feature testing.
12. **Most Active App Versions**

    Shows which app versions are used most frequently. This is crucial for targeting QA efforts, rolling out fixes, or analyzing behavior differences across versions.
13. **Average App Launch Time (Cold & Hot)**

    Measures average launch time in milliseconds for cold (first-time) and hot (relaunch) starts. Lower times contribute to a better user experience, especially in high-frequency use apps.
14. **App Launch Distribution (Hot vs Cold)**

    The breakdown of app launches by type—hot or cold. Helps understand how frequently users return to the app and informs caching or load strategy.
15. **Network Type Distribution**

    The distribution of sessions by network type (WiFi, 4G, 5G, etc.). Helps assess real-world app performance across varying network conditions.
16. **Device Manufacturer Distribution**

    The share of sessions by device manufacturer (Apple, Google, Samsung, etc.). Useful for ensuring device compatibility and prioritizing testing resources.
17. **OS Version Distribution**

    Distribution of user sessions by operating system version. Essential for tracking legacy usage, planning deprecations, and debugging OS-specific issues.

## Source
- DevRev support [[entities/article|article]] [Computer for User Insights](https://support.devrev.ai/en-US/devrev/article/v4whY8L3) (ART-21917)
