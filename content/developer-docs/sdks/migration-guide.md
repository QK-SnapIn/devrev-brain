---
title: Migration guide
type: developer-doc
status: stable
source: developer.devrev.ai
category: sdks
source_url: https://developer.devrev.ai/sdks/android/migration-guide
last_updated: 2026-05-11
summary: "This guide helps transition from the legacy UserExperior SDK to the new DevRev SDK."
---

# Migration guide

DevRev SDK for Android

# Migration guide

This guide helps transition from the legacy UserExperior SDK to the new DevRev SDK.

## [Feature equivalence chart](#feature-equivalence-chart)

| Feature | UserExperior SDK | DevRev SDK (Kotlin) | DevRev SDK (Java) |
| --- | --- | --- | --- |
| Installation | `implementation 'com.userexperior:userexperior-android::<VERSION>’` | `implementation("ai.devrev.sdk:devrev-sdk:<VERSION>")` | `implementation("ai.devrev.sdk:devrev-sdk:<VERSION>")` |
| Initialization | `UserExperior.startRecording(Context context, String ueSdkAppVersionKey)` | `DevRev.configure(context: Context, appId: String, prefersDialogMode: Boolean)` | `DevRev.INSTANCE.configure(Context context, String appId, Boolean prefersDialogMode)` |
| User Identification | `UserExperior.setUserIdentifier(String userIdentifier)` | `DevRev.identifyUnverifiedUser(identity: Identity)` `DevRev.updateUser(identity: Identity)`  `DevRev.logout(deviceID: String)` | `DevRev.INSTANCE.identifyUnverifiedUser(Identity identity)` `DevRev.INSTANCE.updateUser(Identity identity)`  `DevRev.INSTANCE.logout(String deviceID)` |
| Event Tracking | `UserExperior.logEvent(String event, HashMap<String, Object> properties)` | `DevRev.trackEvent(name: String, properties: HashMap<String, String>)` | `DevRevAnalyticsExtKt.trackEvent(DevRev.INSTANCE, String name, HashMap<String, String> properties)` |
| Session Recording | `UserExperior.stopRecording()` `UserExperior.pauseRecording()` `UserExperior.resumeRecording()` | `DevRev.startRecording()` `DevRev.stopRecording()` `DevRev.pauseRecording()` `DevRev.resumeRecording()` `DevRev.processAllOnDemandSessions()` | `DevRevObservabilityExtKt.startRecording(DevRev.INSTANCE, context)` `DevRevObservabilityExtKt.stopRecording(DevRev.INSTANCE)` `DevRevObservabilityExtKt.pauseRecording(DevRev.INSTANCE)` `DevRevObservabilityExtKt.resumeRecording(DevRev.INSTANCE)` `DevRevObservabilityExtKt.processAllOnDemandSessions(DevRev.INSTANCE)` |
| Opt-in or out | `UserExperior.consentOptOut()` `UserExperior.consentOptIn()` `UserExperior.getConsentStatus()` `UserExperior.getOptOutStatus()` | `DevRev.stopAllMonitoring()` `DevRev.resumeAllMonitoring()` | `DevRevObservabilityExtKt.stopAllMonitoring(DevRev.INSTANCE)` `DevRevObservabilityExtKt.resumeAllMonitoring(DevRev.INSTANCE)` |
| Session Properties | `UserExperior.setUserProperties(HashMap<String, Object> userProperties)` | `DevRev.addSessionProperties(properties: HashMap<String, String>)` `DevRev.clearSessionProperties()` | `DevRevObservabilityExtKt(DevRev.INSTANCE, HashMap<String, String> properties)` `DevRevObservabilityExtKt.clearSessionProperties(DevRev.INSTANCE)` |
| Masking Sensitive Data | `UserExperior.markSensitiveView(View view)` `UserExperior.unmarkSensitiveView(View view)` | `DevRev.markSensitiveViews(sensitiveViews: List<View>)` `DevRev.unmarkSensitiveViews(sensitiveViews: List<View>)` | `DevRevObservabilityExtKt.markSensitiveViews(DevRev.INSTANCE, List<View> sensitiveViews)` `DevRevObservabilityExtKt.unmarkSensitiveViews(DevRev.INSTANCE, List<View> sensitiveViews)` |
| Timers | `UserExperior.startTimer(String timerName, HashMap<String, String> properties)` `UserExperior.endTimer(String timerName, HashMap<String, String> properties)` | `DevRev.startTimer(name: String, properties: HashMap<String, String>)`  `DevRev.endTimer(name: String, properties: HashMap<String, String>)` | `DevRevObservabilityExtKt.startTimer(DevRev.INSTANCE, String name, HashMap<String, String> properties)` `DevRevObservabilityExtKt.endTimer(DevRev.INSTANCE, String name, HashMap<String, String> properties)` |
| PLuG support chat | Not supported. | `DevRev.showSupport(context: Context)` `DevRev.createSupportConversation()` `DevRev.setShouldDismissModalsOnOpenLink(value: Boolean)` `DevRev.setInAppLinkHandler(handler: (String) -> Unit)` | `DevRevExtKt.showSupport(DevRev.INSTANCE, context)` `DevRev.INSTANCE.createSupportConversation(Context context)` `DevRev.INSTANCE.setShouldDismissModalsOnOpenLink(Boolean value)`  `DevRev.INSTANCE.setInAppLinkHandler(Function1<? super String, Unit> handler)` |
| Push Notifications | Not supported. | `DevRev.registerDeviceToken(context: Context, deviceToken: String, deviceId: String,)`  `DevRev.processPushNotification(context: Context, userInfo: String)` | `DevRev.INSTANCE.registerDeviceToken(Context context, String deviceToken, String deviceId)` `DevRev.INSTANCE.processPushNotification(Context context, String userInfo)` |

Last updated on

[Features

Previous Page](/sdks/android/features)[Troubleshooting

Next Page](/sdks/android/troubleshooting)

## Source
- DevRev developer docs: [Migration guide](https://developer.devrev.ai/sdks/android/migration-guide)
