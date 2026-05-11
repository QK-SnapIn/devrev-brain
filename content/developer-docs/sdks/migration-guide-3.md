---
title: Migration guide
type: developer-doc
status: stable
source: developer.devrev.ai
category: sdks
source_url: https://developer.devrev.ai/sdks/cordova/migration-guide
last_updated: 2026-05-11
summary: "This guide and chart should help facilitate the transition from the legacy UserExperior SDK to the new DevRev SDK in your Cordova application, providing insights into feature equivalents and method changes."
---

# Migration guide

DevRev SDK for Cordova

# Migration guide

This guide and chart should help facilitate the transition from the legacy UserExperior SDK to the new DevRev SDK in your Cordova application, providing insights into feature equivalents and method changes.

## [Feature Equivalence Chart](#feature-equivalence-chart)

| Feature | UserExperior SDK | DevRev SDK |
| --- | --- | --- |
| Installation | `cordova plugin add userexperior-cordova-plugin@<version>` | `npm install @devrev/sdk-cordova` |
| Initialization | `UserExperior.startRecording(appID)` | `DevRev.configure(appID, successCallback, errorCallback)` |
| User Identification | `UserExperior.setUserIdentifier(userIdentifier)` | `DevRev.identifyUnverifiedUser(identity, successCallback, errorCallback)`  `DevRev.updateUser(identity, successCallback, errorCallback)`  `DevRev.logout(deviceID, successCallback, errorCallback)` |
| Event Tracking | `UserExperior.logEvent(name)` | `DevRev.trackEvent(name, properties, successCallback, errorCallback)` |
| Session Recording | `UserExperior.stopRecording()` `UserExperior.pauseRecording()` `UserExperior.resumeRecording()` | `DevRev.startRecording(successCallback, errorCallback)` `DevRev.stopRecording(successCallback, errorCallback)` `DevRev.pauseRecording(successCallback, errorCallback)` `DevRev.resumeRecording(successCallback, errorCallback)` |
| Opting-in or out | `UserExperior.optOut()`  `UserExperior.optIn()`  `UserExperior.getOptOutStatus()` | `DevRev.stopAllMonitoring(successCallback, errorCallback)`  `DevRev.resumeAllMonitoring(successCallback, errorCallback)` |
| Session Properties | `UserExperior.setUserProperties(userProperties)` | `DevRev.addSessionProperties(properties, successCallback, errorCallback)` `DevRev.clearSessionProperties()` |
| Masking Sensitive Data | `<input type="text" placeholder="Enter Username" name="username" required class="ue-mask">` `<input type="text" placeholder="Enter Username" name="username" required class="ue-unmask">` | `<input type="text" placeholder="Enter Username" name="username" required class="devrev-mask">` `<input type="text" placeholder="Enter Username" name="username" required class="devrev-unmask">` |
| Timers | `UserExperior.startTimer(timerName, properties)`  `UserExperior.endTimer(timerName, properties)` | `DevRev.startTimer(name, properties)`  `DevRev.endTimer(name, properties)` |
| Plug support chat | Not supported. | `DevRev.showSupport(successCallback, errorCallback)`  `DevRev.createSupportConversation(successCallback, errorCallback)`  `DevRev.setShouldDismissModalsOnOpenLink(value, successCallback, errorCallback)`  `DevRevSDK.setInAppLinkHandler(handler, successCallback, errorCallback)` |
| Push Notifications | Not supported. | `DevRev.registerDeviceToken(deviceToken, deviceID, successCallback, errorCallback)`  `DevRev.unregisterDevice(deviceID, successCallback, errorCallback)` `DevRev.processPushNotification(payload, successCallback, errorCallback)` |

Last updated on

## Source
- DevRev developer docs: [Migration guide](https://developer.devrev.ai/sdks/cordova/migration-guide)
