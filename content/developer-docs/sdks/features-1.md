---
title: Features
type: developer-doc
status: stable
source: developer.devrev.ai
category: sdks
source_url: https://developer.devrev.ai/sdks/ios/features
last_updated: 2026-05-11
summary: "To access certain features of the DevRev SDK, user identification is required."
---

# Features

DevRev SDK for iOS

# Features

## [Identification](#identification)

To access certain features of the DevRev SDK, user identification is required.

The identification function should be placed appropriately in your app after the user logs in. If you have the user information available at app launch, call the function after your `DevRev.configure` call has completed.

If you haven't previously identified the user, the DevRev SDK will automatically create an anonymous user for you immediately after the SDK is configured.

The `Identity` structure allows for custom fields in the user, organization, and account traits. These fields must be configured through the DevRev app before they can be utilized. For more information, refer to [Object customization](https://devrev.ai/docs/product/object-customization).

You can select from the following methods to identify users within your application:

### [Identify an unverified user](#identify-an-unverified-user)

The unverified identification method identifies users with a unique identifier, but it does not verify their identity with the DevRev backend.

```
DevRev.identifyUnverifiedUser(_:)
```

The function accepts the `DevRev.Identity` structure, with the user identifier (`userID`) as the only required property, all other properties are optional.

### [Identify a verified user](#identify-a-verified-user)

The verified identification method is used to identify users with an identifier unique to your system within the DevRev platform. The verification is done through a token exchange process between you and the DevRev backend.

The steps to identify a verified user are as follows:

1. Generate an AAT for your system (preferably through your backend).
2. Exchange your AAT for a session token for each user of your system.
3. Pass the user identifier and the exchanged session token to the `DevRev.identifyVerifiedUser(_:sessionToken:)` method.

For security reasons, it is **strongly recommended** that the token exchange is executed on your backend to prevent exposing your application access token (AAT).

#### [Generate an AAT](#generate-an-aat)

1. Open the DevRev web app at <https://app.devrev.ai> and go to the **Settings** page.
2. Open the **PLuG Tokens** page.
3. Under the **Application access tokens** panel, click **New token** and copy the token that's displayed.

Ensure that you copy the generated application access token, as you cannot view it again.

#### [Exchange your AAT for a session token](#exchange-your-aat-for-a-session-token)

To proceed with identifying the user, you need to exchange your AAT for a session token. This step helps you identify a user of your own system within the DevRev platform.

Here is a simple example of an API request to the DevRev backend to exchange your AAT for a session token:

Make sure that you replace the `<AAT>` and `<YOUR_USER_ID>` with the actual values.

```
curl \
--location 'https://api.devrev.ai/auth-tokens.create' \
--header 'accept: application/json, text/plain, */*' \
--header 'content-type: application/json' \
--header 'authorization: <AAT>' \
--data '{
  "rev_info": {
    "user_ref": "<YOUR_USER_ID>"
  }
}'
```

The response of the API call contains a session token that you can use with the verified identification method in your app.

As a good practice, **your** app should retrieve the exchanged session token from **your** backend at app launch or any relevant app lifecycle event.

#### [Identify the verified user](#identify-the-verified-user)

Pass the user identifier and the exchanged session token to the verified identification method:

```
DevRev.identifyVerifiedUser(_:sessionToken:)
```

### [Update the user](#update-the-user)

You can update the user's information using the following method:

```
DevRev.updateUser(_:)
```

This function accepts the `DevRev.Identity` structure.

The `userID` property cannot be updated.

The identification functions are asynchronous. Ensure you wrap them in a `Task` when calling from synchronous contexts.

Use this property to check whether the user is identified in the current session:

```
DevRev.isUserIdentified
```

### [Logout](#logout)

You can perform a logout of the current user by calling the following method:

```
DevRev.logout(deviceID:)
```

The user is logged out by clearing their credentials, as well as unregistering the device from receiving push notifications, and stopping the session recording.

For example:

```
// Identify an unverified user using their email address as the user identifier.
await DevRev.identifyUnverifiedUser(Identity(userID: "user@example.org"))

// Identify a verified user using their email address as the user identifier.
await DevRev.identifyVerifiedUser("foo@example.org", sessionToken: "bar-1337")

// Update the user's information.
await DevRev.updateUser(Identity(organizationID: "organization-1337"))

// Logout the identified user.
await DevRev.logout(deviceID: "dvc32423")
```

### [Identity model](#identity-model)

The `Identity` class is used to provide user, organization, and account information when identifying users or updating their details. This class is used primarily with the `identifyUnverifiedUser(_:)` and `updateUser(_:)` methods.

#### [Properties](#properties)

The `Identity` class contains the following properties:

| Property | Type | Required | Description |
| --- | --- | --- | --- |
| `userID` | `String` | ✅ | A unique identifier for the user |
| `organizationID` | `String?` | ❌ | An identifier for the user's organization |
| `accountID` | `String?` | ❌ | An identifier for the user's account |
| `userTraits` | `UserTraits?` | ❌ | Additional information about the user |
| `organizationTraits` | `OrganizationTraits?` | ❌ | Additional information about the organization |
| `accountTraits` | `AccountTraits?` | ❌ | Additional information about the account |

The custom fields properties defined as part of the user, organization and account traits, must be configured in the DevRev web app **before** they can be used. See [Object customization](https://support.devrev.ai/devrev/article/ART-21854) for more information.

##### [User traits](#user-traits)

The `UserTraits` class contains detailed information about the user:

All properties in `UserTraits` are optional.

| Property | Type | Description |
| --- | --- | --- |
| `displayName` | `String?` | The displayed name of the user |
| `email` | `String?` | The user's email address |
| `fullName` | `String?` | The user's full name |
| `userDescription` | `String?` | A description of the user |
| `phoneNumbers` | `[String]?` | Array of the user's phone numbers |
| `customFields` | `[String: Any]?` | Dictionary of custom fields configured in DevRev |

##### [Organization traits](#organization-traits)

The `OrganizationTraits` class contains detailed information about the organization:

All properties in `OrganizationTraits` are optional.

| Property | Type | Description |
| --- | --- | --- |
| `displayName` | `String?` | The displayed name of the organization |
| `domain` | `String?` | The organization's domain |
| `organizationDescription` | `String?` | A description of the organization |
| `phoneNumbers` | `[String]?` | Array of the organization's phone numbers |
| `tier` | `String?` | The organization's tier or plan level |
| `customFields` | `[String: Any]?` | Dictionary of custom fields configured in DevRev |

##### [Account traits](#account-traits)

The `AccountTraits` class contains detailed information about the account:

All properties in `AccountTraits` are optional.

| Property | Type | Description |
| --- | --- | --- |
| `displayName` | `String?` | The displayed name of the account |
| `domains` | `[String]?` | Array of domains associated with the account |
| `accountDescription` | `String?` | A description of the account |
| `phoneNumbers` | `[String]?` | Array of the account's phone numbers |
| `websites` | `[String]?` | Array of websites associated with the account |
| `tier` | `String?` | The account's tier or plan level |
| `customFields` | `[String: Any]?` | Dictionary of custom fields configured in DevRev |

## [PLuG support chat](#plug-support-chat)

### [UIKit](#uikit)

The support chat feature can be shown as a modal screen from a specific view controller or the top-most one, or can be pushed onto a navigation stack.

To show the support chat screen in your app, you can use the following overloaded method:

```
DevRev.showSupport(from:isAnimated:)
```

* When a `UIViewController` is passed as the `from` parameter, the screen is shown modally.
* When a `UINavigationController` is passed as the `from` parameter, the screen is pushed onto the navigation stack.

If you want to display the support chat screen from the top-most view controller, use the following method:

```
DevRev.showSupport(isAnimated:)
```

For example:

```
// Push the support chat screen to a navigation stack.
await DevRev.showSupport(from: mainNavigationController)

// Show the support chat screen modally from a specific view controller.
await DevRev.showSupport(from: settingsViewController)

// Show the support chat screen from the top-most view controller, without an animation.
await DevRev.showSupport(isAnimated: false)
```

### [SwiftUI](#swiftui)

To display the support chat screen in a SwiftUI app, you can use the following view:

```
DevRev.supportView
```

### [Create a new support conversation](#create-a-new-support-conversation)

You can initiate a new support conversation directly from your app. This method displays the support chat screen and simultaneously creates a new conversation.

```
DevRev.createSupportConversation(isAnimated:)
```

For example:

```
// Create a new support conversation directly from the top-most view controller.
await DevRev.createSupportConversation(isAnimated: true)
```

### [Handle new conversation closure](#handle-new-conversation-closure)

You can receive a callback when a user creates a new conversation by setting the following closure:

```
DevRev.conversationCreatedCompletion
```

This allows your app to access the ID of the newly created conversation.

For example:

```
DevRev.conversationCreatedCompletion = { conversationID in
	print("A new conversation has been created: \(conversationID).")
}
```

## [In-app link handling](#in-app-link-handling)

The DevRev SDK provides a mechanism to handle links opened from within any screen that is part of the DevRev SDK.

You can fully customize the link handling behavior by setting the specialized in-app link handler. That way you can decide what should happen when a link is opened from within the app.

```
DevRev.inAppLinkHandler: ((URL) -> Void)?
```

You can further customize the behavior by setting the `shouldDismissModalsOnOpenLink` boolean flag. This flag controls whether the DevRev SDK should dismiss the top-most modal screen when a link is opened.

```
DevRev.shouldDismissModalsOnOpenLink: Bool
```

## [Configure dynamic theme](#configure-dynamic-theme)

The DevRev SDK allows you to configure the theme dynamically based on the system appearance, or use the theme configured on the DevRev portal. By default, the theme is dynamic and follows the system appearance.

Use `SupportWidgetTheme` inside your `FeatureConfiguration` to align the support experience with your brand:

```
DevRev.updateFeatureConfiguration(
	FeatureConfiguration(
		enableFrameCapture: true,
		autoStartRecording: true,
		alwaysUseRemoteConfig: true,
		supportWidgetTheme: SupportWidgetTheme(
			prefersSystemTheme: false,
			primaryTextColor: "#202020",
			accentColor: "#34C759"
		)
	)
)
```

Directly mutating `DevRev.prefersSystemTheme` is maintained only for backward compatibility and is deprecated. Prefer configuring the theme through `SupportWidgetTheme` passed via `FeatureConfiguration`.

## [Track analytics](#track-analytics)

The DevRev SDK allows you to send custom analytic events by using a name and a string dictionary. You can track these events using the following function:

```
DevRev.trackEvent(name:properties:)
```

For example:

```
await DevRev.trackEvent(name: "open-message-screen", properties: ["id": "message-1337"])
```

Avoid passing special characters in the event name and properties, as these characters can lead to file corruption and missed recordings.

## [Manage session analytics](#manage-session-analytics)

The DevRev SDK offers session analytics features to help you understand how users interact with your app.

### [Opt in or out](#opt-in-or-out)

Session analytics features are opted-in by default, enabling them from the start. However, you can opt-out using the following method:

```
DevRev.stopAllMonitoring()
```

To opt back in, use the following method:

```
DevRev.resumeAllMonitoring()
```

### [Session recording](#session-recording)

You can enable session recording to capture user interactions with your app.

The session recording feature is opt-out and is enabled by default.

The session recording feature includes the following methods to control the recording:

| Method | Action |
| --- | --- |
| `DevRev.startRecording()` | Starts the session recording. |
| `DevRev.stopRecording()` | Ends the session recording and uploads it to the portal. |
| `DevRev.pauseRecording()` | Pauses the ongoing session recording. |
| `DevRev.resumeRecording()` | Resumes a paused session recording. |
| `DevRev.processAllOnDemandSessions()` | Stops the ongoing user recording and sends all on-demand sessions along with the current recording. |

You can also check the following flags for session recording:

```
// Check if session recording is currently active.
let isRecording = DevRev.isRecording

// Check if session monitoring is enabled.
let isMonitoringEnabled = DevRev.isMonitoringEnabled

// Check if on-demand sessions are enabled.
let areOnDemandSessionsEnabled = DevRev.areOnDemandSessionsEnabled
```

### [Session properties](#session-properties)

You can add custom properties to the session recording to help you understand the context of the session. The properties are defined as a dictionary of string values.

```
DevRev.addSessionProperties(_:)
```

To clear the session properties in scenarios such as user logout or when the session ends, use the following method:

```
DevRev.clearSessionProperties()
```

Avoid passing special characters in the session properties, as these characters can lead to file corruption and missed recordings.

### [Mask sensitive data](#mask-sensitive-data)

To protect sensitive data, the DevRev SDK provides an auto-masking feature that masks data before sending to the server. Input views such as text fields, text views, and web views are automatically masked.

While the auto-masking feature may be sufficient for most situations, you can manually mark additional views as sensitive using the following method:

```
DevRev.markSensitiveViews(_:)
```

If any previously masked views need to be unmasked, you can use the following method:

```
DevRev.unmarkSensitiveViews(_:)
```

### [Custom masking provider](#custom-masking-provider)

For advanced use cases, you can provide a custom masking provider to specify exactly which regions of the UI should be masked in snapshots.

You can implement your own masking logic by conforming to the `DevRev.MaskLocationProviding` protocol and setting your custom object as the masking provider. This allows you to specify explicit regions to be masked or to skip snapshots entirely.

| Symbol | Description |
| --- | --- |
| `DevRev.setMaskingLocationProvider(_ provider: DevRev.MaskLocationProviding)` | A custom provider that determines which UI regions should be masked for privacy during snapshots. |
| `DevRev.MaskLocationProviding` | A protocol for providing explicit masking locations for UI snapshots. |
| `DevRev.SnapshotMask` | An object that describes the regions of a snapshot to be masked. |
| `DevRev.SnapshotMask.Location` | An object that describes a masked region. |

For example:

```
import Foundation
import UIKit
import DevRevSDK

class MyMaskingProvider: NSObject, DevRev.MaskLocationProviding {
	func provideSnapshotMask() async -> DevRev.SnapshotMask {
        let region = CGRect(x: 10, y: 10, width: 100, height: 40)
        let location = DevRev.SnapshotMask.Location(location: region)
        let mask = DevRev.SnapshotMask(locations: [location], shouldSkip: false)
		return mask
	}
}
```

```
DevRev.setMaskingLocationProvider(MyMaskingProvider())
```

Setting a new provider overrides any previously set masking location provider.

### [Track user interactions](#track-user-interactions)

The DevRev SDK automatically tracks user interactions such as taps, swipes, and scrolls. However, in some cases you may want to disable this tracking to prevent sensitive user actions from being recorded.

To temporarily disable user interaction tracking, use the following method:

```
DevRev.pauseUserInteractionTracking()
```

To resume user interaction tracking, use the following method:

```
DevRev.resumeUserInteractionTracking()
```

### [Use timers](#use-timers)

The DevRev SDK offers a timer mechanism to measure the time spent on specific tasks, allowing you to track events such as response time, loading time, or any other duration-based metrics.

The mechanism works using balanced start and stop methods that both accept a timer name and an optional dictionary of properties.

To start a timer, use the following method:

```
DevRev.startTimer(_:properties:)
```

To stop a timer, use the following method:

```
DevRev.endTimer(_:properties:)
```

For example:

```
DevRev.startTimer("response-time", properties: ["id": "task-1337"])

// Perform the task that you want to measure.

DevRev.endTimer("response-time", properties: ["id": "task-1337"])
```

Avoid passing special characters in the timer properties, as these characters can lead to file corruption and missed recordings.

### [Capture errors](#capture-errors)

You can report a handled error from a catch block using the `captureError` function.

This ensures that even if the error is handled in your app, it is still logged for diagnostics.

```
DevRev.captureError(
    _ error: Error,
    tag: String
)
```

For example:

```
do {
    try someFunction()
} catch {
    DevRev.captureError(
        error,
        tag: "network-failure"
    )
}
```

### [Track screens](#track-screens)

The DevRev SDK offers automatic screen tracking to help you understand how users navigate through your app. Although view controllers are automatically tracked, you can manually track screens using the following method:

```
DevRev.trackScreenName(_:)
```

For example:

```
DevRev.trackScreenName("profile-screen")
```

## [Configure push notifications](#configure-push-notifications)

You can configure your app to receive push notifications from the DevRev SDK. The SDK is designed to handle push notifications and execute actions based on the notification's content.

The DevRev backend sends push notifications to your app to notify users about new messages in the support chat.

### [Configure](#configure)

To receive push notifications, you need to configure your DevRev organization by following the instructions in the [push notifications](https://developer.devrev.ai/sdks/push-notifications) section.

You need to ensure that your iOS app is configured to receive push notifications. You can follow the [Apple documentation](https://developer.apple.com/documentation/usernotifications/registering_your_app_with_apns) for guidance on registering your app with Apple Push Notification service (APNs).

### [Register for push notifications](#register-for-push-notifications)

Push notifications require that the SDK has been configured and the user has been identified (unverified and verified users). The user identification is required to send the push notification to the correct user.

The DevRev SDK offers a method to register your device for receiving push notifications. You can register for push notifications using the following method:

```
DevRev.registerDeviceToken(_:deviceID:)
```

The method requires a device identifier, which can either be an identifier unique to your system or the Apple-provided Vendor Identifier (IDFV). Typically, the token registration is called from the `AppDelegate.application(_:didRegisterForRemoteNotificationsWithDeviceToken:)` method.

For example:

```
func application(
	_ application: UIApplication,
	didRegisterForRemoteNotificationsWithDeviceToken deviceToken: Data
) {
	guard
		let deviceID = UIDevice.current.identifierForVendor?.uuidString
	else {
		return
	}

	Task {
		await DevRev.registerDeviceToken(
			deviceToken,
			deviceID: deviceID
		)
	}
}
```

### [Unregister from push notifications](#unregister-from-push-notifications)

If your app no longer needs to receive push notifications, you can unregister the device.

Use the following method to unregister the device:

```
DevRev.unregisterDevice(_:)
```

This method requires the device identifier, which should be the same as the one used during registration. It is recommended to place this method after calling `UIApplication.unregisterForRemoteNotifications()` in your app.

For example:

```
UIApplication.shared.unregisterForRemoteNotifications()

Task {
	guard
		let deviceID = UIDevice.current.identifierForVendor?.uuidString
	else {
		return
	}

	await DevRev.unregisterDevice(deviceID)
}
```

### [Handle push notifications](#handle-push-notifications)

Push notifications coming to the DevRev SDK need to be handled manually. To properly handle them, implement the following method, typically in either the `UNUserNotificationCenterDelegate.userNotificationCenter(_:didReceive:)` or `UIApplicationDelegate.application(_:didReceiveRemoteNotification:fetchCompletionHandler:)`:

```
DevRev.processPushNotification(_:)
```

For convenience, this method provides two overloads that accept `userInfo` as either `[AnyHashable: Any]` or `[String: any Sendable]` dictionary types.

For example:

```
func userNotificationCenter(
	_ center: UNUserNotificationCenter,
	didReceive response: UNNotificationResponse
) async {
	await DevRev.processPushNotification(response.notification.request.content.userInfo)
}
```

Last updated on

[Quickstart guide

Previous Page](/sdks/ios/quickstart)[Migration guide

Next Page](/sdks/ios/migration-guide)

## Source
- DevRev developer docs: [Features](https://developer.devrev.ai/sdks/ios/features)
