---
title: Migration guide
type: developer-doc
status: stable
source: developer.devrev.ai
category: sdks
source_url: https://developer.devrev.ai/sdks/flutter/migration-guide
last_updated: 2026-05-11
summary: "This guide helps you transition from the legacy UserExperior SDK to the new DevRev SDK in your Flutter application."
---

# Migration guide

DevRev SDK for Flutter

# Migration guide

This guide helps you transition from the legacy UserExperior SDK to the new DevRev SDK in your Flutter application. Below is a feature equivalence chart and detailed instructions for migrating.

## [Feature equivalence chart](#feature-equivalence-chart)

| Feature | UserExperior SDK | DevRev SDK |
| --- | --- | --- |
| Installation | `user_experior: ^<VERSION>` | `devrev_sdk_flutter: ^<VERSION>` |
| Initialization | `userExperior.startRecording(appID)` | `DevRev.configure(appID)` |
| User identification | `userExperior.setUserIdentifier(userIdentifier)` | `DevRev.identifyUnverifiedUser(userID, organizationID)` `DevRev.identifyVerifiedUser(userID, sessionToken)` `DevRev.logout(deviceID)` |
| Event tracking | `userExperior.logEvent(name)` | `DevRev.trackEvent(name, properties)` |
| Session recording | `userExperior.stopRecording()` `userExperior.pauseRecording()` `userExperior.resumeRecording()` | `DevRev.startRecording()` `DevRev.stopRecording()` `DevRev.pauseRecording()` `DevRev.resumeRecording()` `DevRev.processAllOnDemandSessions()` |
| Opt-in or out | `userExperior.optOut()` `userExperior.optIn()` `userExperior.getOptOutStatus()` | `DevRev.stopAllMonitoring()` `DevRev.resumeAllMonitoring()` |
| Session properties | `userExperior.setUserProperties(properties)` | `DevRev.addSessionProperties(properties)` `DevRev.clearSessionProperties()` |
| Masking sensitive data | `UEMarker(child: TextField(controller: provider.fieldController, decoration: InputDecoration(border: OutlineInputBorder(borderRadius: BorderRadius.circular(15))),)` | `DevRevMask(child: TextField(decoration: InputDecoration(labelText: "foo-bar"),),)` `DevRevUnmask(child: TextField(decoration: InputDecoration(labelText: "foo-bar"),),)` |
| Timers | `userExperior.startTimer(timerName, properties)` `userExperior.endTimer(timerName, properties)` | `DevRev.startTimer(name, properties)` `DevRev.endTimer(name, properties)` |
| Plug support chat | Not supported. | `DevRev.showSupport()`  `DevRev.createSupportConversation()` |
| Push notifications | Not supported. | `DevRev.registerDeviceToken(deviceToken, deviceID)` `DevRev.unregisterDevice(deviceID)` |

Last updated on

[Features

Previous Page](/sdks/flutter/features)[Troubleshooting

Next Page](/sdks/flutter/troubleshooting)

## Source
- DevRev developer docs: [Migration guide](https://developer.devrev.ai/sdks/flutter/migration-guide)
