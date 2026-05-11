---
title: Migration guide
type: developer-doc
status: stable
source: developer.devrev.ai
category: sdks
source_url: https://developer.devrev.ai/sdks/ios/migration-guide
last_updated: 2026-05-11
summary: "This guide and chart should help facilitate the transition from the legacy UserExperior SDK to the new DevRev SDK in your iOS application, providing insights into feature equivalents and method changes."
---

# Migration guide

DevRev SDK for iOS

# Migration guide

This guide and chart should help facilitate the transition from the legacy UserExperior SDK to the new DevRev SDK in your iOS application, providing insights into feature equivalents and method changes.

## [Feature equivalence chart](#feature-equivalence-chart)

| Feature | UserExperior SDK | DevRev SDK |
| --- | --- | --- |
| Installation | `pod 'UserExperior', '~> <VERSION>` | SPM: `https://github.com/devrev/devrev-sdk-ios` CocoaPods: `pod 'DevRevSDK', '~> <VERSION>` |
| Initialization | `UserExperior.startRecording(_ versionKey: String)` | `DevRev.configure(appID: String)` |
| User Identification | `UserExperior.setUserIdentifier(_ userIdentifier: String)` | `DevRev.identifyUnverifiedUser(_ identity: Identity)` `DevRev.updateUser(_ identity: Identity)`  `identifyVerifiedUser( _ userID: String, sessionToken: String)` `DevRev.logout(deviceID: String)` |
| Event Tracking | `UserExperior.logEvent(_ eventName: String)` | `DevRev.trackEvent(name: String, properties: [String: String])` |
| Session Recording | `UserExperior.stopRecording()` `UserExperior.pauseRecording()` `UserExperior.resumeRecording()` | `DevRev.startRecording()` `DevRev.stopRecording()` `DevRev.pauseRecording()` `DevRev.resumeRecording()` `DevRev.processAllOnDemandSessions()` |
| Opt-in or out | `UserExperior.consentOptIn()` `UserExperior.consentOptOut()` `UserExperior.getConsentStatus` `UserExperior.getOptOutStatus` | `DevRev.stopAllMonitoring()` `DevRev.resumeAllMonitoring()` |
| Session Properties | `UserExperior.setUserProperties(_ properties: [String: Any])` | `DevRev.addSessionProperties(properties: [String: String])` `DevRev.clearSessionProperties()` |
| Masking Sensitive Data | `UserExperior.markSensitiveViews(_ viewsToSecure: NSArray)` `UserExperior.unmarkSensitiveViews(_ viewsToSecure: NSArray)` | `DevRev.markSensitiveViews(_ sensitiveViews: [UIView])` `DevRev.unmarkSensitiveViews(_ sensitiveViews: [UIView])` |
| Timers | `UserExperior.startTimer(_ timerName: String)` `UserExperior.endTimer(_ timerName: String)` | `DevRev.startTimer(_ name: String, properties: [String: String])` `DevRev.endTimer(_ name: String, properties: [String: String])` |
| Plug support chat | Not supported. | `DevRev.showSupport(isAnimated: Bool)` `DevRev.showSupport(from parentViewController: UIViewController, isAnimated: Bool)` `DevRev.showSupport(from navigationController: UINavigationController, isAnimated: Bool)` `DevRev.createSupportConversation(isAnimated: Bool)` `DevRev.shouldDismissModalsOnOpenLink` `DevRev.inAppLinkHandler` |
| Push Notifications | Not supported. | `DevRev.registerDeviceToken(_ deviceToken: Data, deviceID: String)` `DevRev.processPushNotification(_ userInfo: [String: String])` |

Last updated on

[Features

Previous Page](/sdks/ios/features)[Troubleshooting

Next Page](/sdks/ios/troubleshooting)

## Source
- DevRev developer docs: [Migration guide](https://developer.devrev.ai/sdks/ios/migration-guide)
