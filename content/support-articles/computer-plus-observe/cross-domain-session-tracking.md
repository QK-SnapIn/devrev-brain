---
title: Cross-domain session tracking
devrev_id: ART-21920
parent_directory: Computer+ Observe
translation_group: Qz2Gf4Rg
modified_date: "2026-03-17T11:00:54.33Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/Qz2Gf4Rg"
tags: []
top_category: Computer+ Observe
wiki_match: features/csat
match_score: 0.407
last_updated: 2026-05-11
---

# Cross-domain session tracking

The Plug SDK tracks session details using the client-side browser storage, but this approach is limited by the same-origin policy. As a result, when users navigate between different domains or subdomains (for example, from domain1.com to domain2.com), the SDK records separate, unconnected sessions, preventing comprehensive user journey tracking.

Plug SDK enables cross-domain session tracking by using the following method.

## Get session and tab IDs

A session ID identifies a user's entire visit to a website or app, while a tab ID distinguishes activity within individual browser tabs. This separation allows precise tracking of interactions across multiple tabs in a single session.

The Plug SDK exposes the session ID and tab ID of an ongoing session by the
`getSessionDetails()` method. When navigating from one domain to another you can hit this method to fetch these ids.

```
const { sessionId, tabId } = window.plugSDK.getSessionDetails();
```

To ensure that the session recording features are ready before calling `getSessionDetails`, wait on the `ON_OBSERVABILITY_READY` Plug event. For more information about this event, refer to the [methods reference](https://developer.devrev.ai/public/sdks/web/methods#take-action-from-plug-chat-events).

```
window.plugSDK.onEvent(payload => {
  if (payload.type === "ON_OBSERVABILITY_READY") {
    const { sessionId, tabId } = window.plugSDK.getSessionDetails();
  }
});
```

## Passing the session and tab IDs across domains

You need to pass session and tab IDs to the second domain that is being navigated to. You can choose from the following methods to pass data between domains

* **Server-side synchronization:** Use backend APIs to store and share session data across different domains.
* **Client-side communication:** Pass the session details using client-side methods like via URL parameters, or by storing them in first-party cookies within the same top-level domain.

The example below demonstrates how to pass data using URL query parameters in a journey between two domains: **domain1.com** and **domain2.com**.

**On domain1.com**

You need to set the session ID and tab ID in URL query parameters of the domain you are navigating to.

```
const url = new URL('domain2.com'); // second domain
const params = new URLSearchParams(url.search);

// Add or Update parameters
params.set('sessionId', sessionId);
params.set('tabId', tabId); // skip this if you want the recording to be part of the session but as a different tab

// Update URL
url.search = params.toString();

// Navigate to second page (domain2.com)
window.location.href = url.toString();
```

**On domain2.com**

```
const params = new URLSearchParams(window.location.search);
const sessionId = params.get('sessionId');
const tabId = params.get('tabId');

// remove the query params from the url after we have them in variables
const urlWithoutQueryParams = new URL(window.location);
urlWithoutQueryParams.delete('sessionId');
urlWithoutQueryParams.delete('tabId');
window.history.pushState({}, '', urlWithoutQueryParams);
```

## Initialize the SDK with session and tab IDs

You need to now pass the session ID and tab ID that you have received from the first domain into the `plugSDK.init()` function of the second domain.

```
// Initialize the SDK
window.plugSDK.init({
  app_id: "my-integration-key",
  enable_session_recording: true,
  session_recording_options: {
    sessionDetails: {
      sessionId: sessionId,
      tabId: tabId,
    },
  },
});
```

You can leave the `tabId` empty if you want to track this domain as a separate tab within the same session.

If the session identifiers passed to the Plug method correspond to a session which has already ended, or some invalid identifiers, the SDK rejects them and start a complete new session instead.

## Source
- DevRev support article [Cross-domain session tracking](https://support.devrev.ai/en-US/devrev/article/Qz2Gf4Rg) (ART-21920)
