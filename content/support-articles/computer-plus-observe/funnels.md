---
title: Funnels
devrev_id: ART-21919
parent_directory: Computer+ Observe
translation_group: _FG4pa74
modified_date: "2025-12-11T23:31:46.997Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/_FG4pa74"
tags: []
top_category: Computer+ Observe
wiki_match: glossary/nnl
match_score: 0.6
last_updated: 2026-05-11
---

# Funnels

Funnels in DevRev's Session Analytics help you track user journeys through multi-step processes in your application. Unlike traditional analytics that focus on individual events, funnels provide a comprehensive view of user behavior across entire journeys, spanning multiple sessions and interactions.

A funnel represents a sequence of user actions leading to a desired outcome. Each step captures a critical user interaction, allowing you to visualize where users succeed, encounter friction, or abandon their journey.

![Funnels](don:core:dvrv-us-1:devo/0:artifact/4100564)

## Access funnels

To access the Funnels feature:

1. Click **Explore** in the left navigation menu.
2. Search for "Usage Funnels".
3. Click **Usage Funnels** to open the feature.
4. (Optional) Pin **Usage Funnels** to your left navigation for quick access.

## View your funnel list

The funnel list displays the following information for each funnel:

* **Funnel name**: Click to open the funnel visualization
* **Creation date**: When the funnel was created
* **Created by**: The user who created the funnel
* **Conversion days**: The conversion window configured for the funnel (how many days users have to complete all steps)
* **Range days**: The date range of historical data included in the funnel (how far back the analysis goes)

## Create a funnel

To create a funnel, configure the following elements:

![Funnel create](don:core:dvrv-us-1:devo/0:artifact/4100566)

### Funnel name

Give your funnel a descriptive name that clearly identifies its purpose (for example, "User Onboarding Flow" or "Purchase Conversion Journey").

### Date range

Choose how far back you'd like to view the data for this funnel (maximum 30 days). This determines the historical data available when your funnel is created.

### Conversion window

Set the timeframe (1-30 days) within which users must complete all funnel steps. Choose based on typical user behavior patterns for your specific workflow.

### Funnel steps

![Funnel steps](don:core:dvrv-us-1:devo/0:artifact/4100569)

Define the sequence of user actions you want to track. Each step can be configured as:

* **Screen**: Track when users visit specific screens (mobile platform only, for example, `LoginScreen`, `CheckoutScreen`)
* **Event**: Track specific user actions (available on all platforms, for example, button clicks, form submissions)
* **Event Property**: Filter events by specific criteria (for example, `button_type = 'purchase'`)

**Example: E-commerce purchase funnel for mobile platform**

* **Step 1:** Screen - `ProductPage`
* **Step 2:** Event - `add_to_cart`
* **Step 3:** Event - `purchase_completed`
* **Date Range:** 30 days
* **Conversion Window:** 7 days

![Funnel example](don:core:dvrv-us-1:devo/0:artifact/4100572)

## Funnel management

### Create a new funnel

1. Click **Create New Funnel** at the top right of the funnel list page.
2. Configure your funnel settings.
3. Click **Save**.

### Open a funnel

Click any funnel name to view its visualization and data.

### Edit a funnel

1. Click the three-dot menu next to the funnel in the funnel list.
2. Select **Edit**.
3. Make your desired changes to the funnel configuration.
4. Click **Save** to apply your changes.

**Note:** After saving, new funnel data will be created and it will take some time to process and display updated results.

### Delete a funnel

1. Click the three-dot menu next to the funnel in the funnel list.
2. Select **Delete**.
3. Confirm deletion in the dialog.

Deletion is permanent and cannot be undone.

## Funnel count calculation

Funnels track individual users (not sessions) as they progress through your defined steps. Each user can only be counted once in your funnel, even if they attempt the journey multiple times. DevRev funnels use non-strict tracking, meaning users can complete steps in any order or skip intermediate steps within your conversion window.

### User journey prioritization logic

When a user has multiple attempts at your funnel, the system prioritizes which journey to count:

1. Converted users (completed all steps): highest priority
2. Partial completion (by furthest step reached)
3. Most recent attempt (for tied scenarios)

**Example:** If User A completes Step 1 on Monday but drops off, then completes all 3 steps on Wednesday, only the successful Wednesday journey is counted.

### Cross-session tracking

Users can complete funnel steps across multiple app sessions within your conversion window:

* **Day 1:** User views product page (Step 1) then closes app
* **Day 3:** Same user opens app and adds item to cart (Step 2)
* **Day 5:** User completes purchase (Step 3)

All three steps count as one successful funnel completion if they occur within your conversion window timeframe.

### Conversion windows

A conversion window is a configurable timeframe (1-30 days) within which users must complete all funnel steps, starting from the first step of each funnel attempt.

**How conversion windows work:**

If a user completes the first funnel step (Event 1) on Day 1 but fails to complete all subsequent steps within the conversion window, they are counted as dropped off at the stage where they stopped. If the same user completes Event 1 again on Day 2, a new conversion window starts from Day 2, giving them another chance to complete the funnel steps.

**Example with a 2-day window:**

* **Day 1:** User completes Event 1
* **Day 3:** User has not completed Event 2 (outside the 2-day window)
* **Result:** User is counted as dropped off at Event 1

If the user later completes the entire funnel within a new conversion window, they will be counted as converted, and no drop-off will be recorded.

**Example with a 7-day window:**

* **Step 1:** `January 1` at `2:00 PM`
* **Deadline:** All remaining steps must complete by `January 8` at `2:00 PM`
* If Step 2 happens `January 9`, it won't be considered since it falls outside the conversion window

## Funnel visualization

Once your funnel is created, you'll see a bar chart visualization showing user progression through each step. Each bar represents the number of users who reached that specific step.

**Key elements:**

* **Step names**: Displayed at the top of each bar (for example, "ProductPage", "add\_to\_cart")
* **User counts**: The numbers displayed on each bar when hovered over, indicating how many users reached that step
* **Bar heights**: Visual representation of drop-off; shorter bars show fewer users
* **Conversion flow**: Read left to right to see user progression

**Example:**

* **Step 1:** ProductPage - 12,000 users
* **Step 2:** add\_to\_cart - 5,000 users (58% drop-off)
* **Step 3:** purchase\_completed - 3,200 users (36% drop-off from Step 2)

### Calculate drop-off rates

**Step 1 to Step 2:**

* Users dropped: 12,000 - 5,000 = 7,000 users
* Drop-off rate: (7,000 ÷ 12,000) × 100 = 58%

**Step 2 to Step 3:**

* Users dropped: 5,000 - 3,200 = 1,800 users
* Drop-off rate: (1,800 ÷ 5,000) × 100 = 36%

**Overall funnel conversion:**

* Total conversion rate: (3,200 ÷ 12,000) × 100 = 26.7%

## Drill-down analysis

Drill-downs show sessions where users dropped off at a specific step. Understanding what drill-downs indicate is crucial for effective funnel analysis.

They are available only for drop-off steps where users exit your funnel. Click any drop-off step to access detailed session data for users who abandoned the funnel at that point.

Drill-downs show the following:

* **Drop-off sessions only**: Users who reached this step but didn't progress to the next step
* **Sampled data**: Limited to 10,000 sessions per step for performance
* **Session details**: Individual user sessions with context about their experience

### Available filters

Filter options vary by platform:

**Web platform filters:**

* User
* Workspace
* Recorded date
* Is Rage (users showing frustration behavior)
* Is Dead (sessions with dead tap interactions)
* Is Console Error (sessions with JavaScript console errors)
* Is Network Error (sessions with network-related errors)

**Mobile platform filters:**

* Is Crash (sessions that experienced crashes)
* Is Rage (sessions with rage taps)
* User
* Workspace
* Recorded date
* Crash Type
* Device Manufacturer
* Device Model
* OS Version
* Network Type
* Network Operator
* Launch Type (cold launch or hot launch)

### Investigate individual users

For deeper investigation:

1. Copy a `rev_user_id` from the drill-down results.
2. Navigate to the user sessions list view.
3. Explore that user's complete journey across all sessions.

This reveals the full context of why a specific user dropped off.

## Limitations and constraints

### Funnel configuration limits

* **Maximum steps:** 20 steps per funnel
* **Funnel count:** 20 funnels per organization (soft limit for cost management)
* **Conversion window:** 1-30 days maximum (limited by data retention policy)

### Data and performance constraints

* **Update frequency:** Daily updates only (not real-time data)
* **Data retention:** 30-day maximum historical data access
* **Drill-down sampling:** Limited to 10,000 sessions per drop-off step

### Analysis limitations

* **No dynamic filtering:** Main funnel visualization cannot be filtered; filtering only available in drill-downs
* **No range day filtering:** Once a funnel is created for a particular date range, it calculates data for all those days only. You cannot filter or adjust the date range after creation
* **Drop-off focus:** Drill-downs display only users who exited the funnel, not those who completed it successfully. This means drill-downs are available only for the drop-off bars
* **Non-strict funnels only:** Users can skip steps or perform actions out of order; funnels track any completion of defined steps within the conversion window

## Best practices

### Funnel design

* **Start simple**: Begin with 2-3 key steps, then expand as you understand user behavior
* **Logical flow**: Steps should follow natural user workflow and represent meaningful actions
* **Realistic conversion windows**: Set timeframes based on actual user behavior patterns (for example, 1-2 days for quick actions, 7-14 days for considered purchases)
* **Clear step names**: Use descriptive names that clearly identify what user action is being tracked

### Event and property instrumentation with SDK

* **Consistent event names**: Use clear, standardized naming conventions (for example, `add_to_cart`, `purchase_completed`, `user_signup`)
* **Meaningful property values**: Ensure event properties have descriptive values that help with filtering (for example, `button_type = 'primary'`, `page_category = 'product'`)
* **Standardize across teams**: Coordinate with development teams to maintain consistent event naming across your application
* **Test before creating funnels**: Verify events are firing correctly and properties contain expected values before building funnels

### SDK implementation examples

Use the following SDK methods to track events for your funnels:

**Web SDK (Plug)**

```
window.plugSDK.trackEvent(event_name, properties)

// Example usage:
var properties = {
  "name": "John Doe",
  "plan": "Starter",
  "payment_method": "Credit Card",
  "expiry_date": "2024-12-12"
}
window.plugSDK.trackEvent("signed_up", properties)
```

[Learn more about Web SDK event tracking](https://devrev.ai/developer/sdks/web/track-events)

**Android SDK**

```
DevRev.trackEvent(name: String, properties: HashMap<String, String>)

// Example usage:
DevRev.trackEvent(
  name = "open-message-screen", 
  properties = hashMapOf("id" to "message-1337")
)
```

[Learn more about Android SDK analytics](https://developer.devrev.ai/sdks/android/features#analytics)

**iOS SDK**

```
DevRev.trackEvent(name:properties:)

// Example usage:
await DevRev.trackEvent(
  name: "open-message-screen", 
  properties: ["id": "message-1337"]
)
```

[Learn more about iOS SDK analytics](https://developer.devrev.ai/sdks/ios/features#analytics)

**React Native and Expo SDK**

```
DevRev.trackEvent(name: string, properties?: { [key: string]: string })
```

[Learn more about React Native SDK analytics](https://developer.devrev.ai/sdks/react-native/features#analytics)

**Cordova SDK**

```
DevRev.trackEvent(name, properties, successCallback, errorCallback)
```

[Learn more about Cordova SDK analytics](https://developer.devrev.ai/sdks/cordova/features#analytics)

**Flutter SDK**

```
DevRev.trackEvent(name, properties);

// Example usage:
DevRev.trackEvent(
  "open-message-screen", 
  {"id": "message-1337"}
);
```

[Learn more about Flutter SDK analytics](https://developer.devrev.ai/sdks/flutter/features#analytics)

## Troubleshooting

### Funnel shows no data

If your funnel displays no data, check the following:

* Verify that your events are firing correctly by performing a session where the event is expected to trigger, then check it in the Sessions Dashboard or Session Replays
* Verify the date range covers periods when users actually performed these actions
* Ensure event names match exactly what's implemented in your application

### Numbers seem lower than expected

If funnel counts appear lower than anticipated:

* Remember that each user is counted only once, even with multiple attempts
* Cross-session tracking may show different patterns than session-based analytics
* Check your conversion window—users must complete all steps within this timeframe

### New funnel doesn't appear immediately

If your newly created funnel is not visible:

* Funnels take time to process and generate initial datasets
* Wait a few minutes after creation before expecting data to appear
* Larger date ranges and more complex funnels take longer to process

### Drill-downs show limited results

If drill-down data seems incomplete:

* Drill-downs are sampled to 10,000 sessions per step for performance
* Only drop-off sessions are shown, not successful conversions

### Funnel numbers stay the same throughout the day

If funnel data doesn't update during the day:

* Funnels update once every 24 hours, not in real-time
* Data refreshes happen overnight, so expect consistent numbers during the day

### Integrated events not visible in funnel creation

If newly integrated events don't appear in the funnel creation interface:

* Newly integrated events take time to appear in the funnel creation interface
* It may take 12-24 hours for events to become available in the funnel step selection

## Source
- DevRev support article [Funnels](https://support.devrev.ai/en-US/devrev/article/_FG4pa74) (ART-21919)
