---
title: Migration guide
type: developer-doc
status: stable
source: developer.devrev.ai
category: sdks
source_url: https://developer.devrev.ai/sdks/react-native/migration-guide
last_updated: 2026-05-11
summary: "DevRev SDK for React Native and Expo"
---

# Migration guide

DevRev SDK for React Native and Expo

# Migration guide

This guide and chart should help facilitate the transition from the legacy UserExperior SDK to the new DevRev SDK in your React Native application, providing insights into feature equivalents and method changes.

## [Feature equivalence chart](#feature-equivalence-chart)

| Feature | UserExperior SDK | DevRev SDK |
| --- | --- | --- |
| Installation | `npm install react-native-userexperior` | `npm install @devrev/sdk-react-native` |
| Initialization | `UserExperior.startRecording(string)` | `DevRev.configure(appID: string)` |
| User Identification | `UserExperior.setUserIdentifier(string)` | `DevRev.identifyUnverifiedUser(identity: Identity)`  `DevRev.updateUser(identity: Identity)`  `DevRev.identifyVerifiedUser(userID: string, sessionToken: string)`  `DevRev.logout(deviceID: string)` |
| Event Tracking | `UserExperior.logEvent(string, Map<string, string>)` | `DevRev.trackEvent(name: string, properties?: { [key: string]: string })` |
| Session Recording | `UserExperior.stopRecording()` `UserExperior.pauseRecording()` `UserExperior.resumeRecording()` | `DevRev.startRecording()` `DevRev.stopRecording()` `DevRev.pauseRecording()` `DevRev.resumeRecording()` `DevRev.processAllOnDemandSessions()` |
| Opt-in or out | Not supported. | `DevRev.stopAllMonitoring()`  `DevRev.resumeAllMonitoring()` |
| Session Properties | `UserExperior.setUserProperties(Map<string, string>)` | `DevRev.addSessionProperties(properties: { [key: string]: string })`  `DevRev.clearSessionProperties()` |
| Masking Sensitive Data | `UserExperior.addInSecureViewBucket(any[])` `UserExperior.removeFromSecureViewBucket(any[])` | `DevRev.markSensitiveViews(tags: any[])` `DevRev.unmarkSensitiveViews(tags: any[])` |
| Timers | Not supported. | `DevRev.startTimer(name: string, properties: { [key: string]: string })`  `DevRev.endTimer(name: string, properties: { [key: string]: string })` |
| Plug support chat | Not supported. | `DevRev.showSupport()`  `DevRev.createSupportConversation()`  `DevRev.setShouldDismissModalsOnOpenLink()`  `DevRev.setInAppLinkHandler()` |
| Push Notifications | Not supported. | `DevRev.registerDeviceToken()`  `DevRev.unregisterDevice(deviceID: string)`  `DevRev.processPushNotification()` |

Last updated on

## Source
- DevRev developer docs: [Migration guide](https://developer.devrev.ai/sdks/react-native/migration-guide)
