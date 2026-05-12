---
title: Features
type: developer-doc
status: stable
source: developer.devrev.ai
category: sdks
source_url: https://developer.devrev.ai/sdks/cordova/features
last_updated: 2026-05-11
summary: "To access certain features of the DevRev SDK, user identification is required."
---

# Features

DevRev SDK for Cordova

# Features

## [Identification](#identification)

To access certain features of the DevRev SDK, user identification is required.

The identification function should be placed appropriately in your app after the user logs in. If you have the user information available at app launch, call the function after the `DevRev.configure(appID)` method.

If you haven't previously identified the user, the DevRev SDK will automatically create an anonymous user for you immediately after the SDK is configured.

The `Identity` structure allows for custom fields in the user, organization, and account traits. These fields must be configured through the DevRev app before they can be utilized. For more information, refer to [Object customization](https://support.devrev.ai/devrev/article/ART-21854).

You can select from the following methods to identify users within your application:

### [Identify unverified users](#identify-unverified-users)

The unverified identification method identifies users with a unique identifier, but it does not verify their identity with the DevRev backend.

```
DevRev.identifyUnverifiedUser(identity, successCallback, errorCallback)
```

### [Verified identification](#verified-identification)

The verified identification method identifies users with a unique identifier and verifies their identity with the DevRev backend.

```
DevRev.identifyVerifiedUser(identity, successCallback, errorCallback)
```

### [Update the user](#update-the-user)

You can update the user's information using the following method:

```
DevRev.updateUser(identity, successCallback, errorCallback)
```

The `userID` property cannot be updated.

### [Logout](#logout)

You can log out the current user by using the following method:

```
DevRev.logout(deviceID, successCallback, errorCallback)
```

The user will be logged out by clearing their credentials, as well as unregistering the device from receiving push notifications, and stopping the session recording.

## [Plug support chat](#plug-support-chat)

Once user identification is complete, you can start using the chat (conversations) dialog supported by our DevRev SDK. The support chat feature can be shown as a modal screen from the top-most screen.

This functionality requires the SDK to be configured and the user to be identified, whether they are unverified or verified.

To show the support chat screen in your app, you can use the following method:

```
DevRev.showSupport(successCallback, errorCallback)
```

### [Creating a new support conversation](#creating-a-new-support-conversation)

You can initiate a new support conversation directly from your app. This method displays the support chat screen and simultaneously creates a new conversation.

```
DevRev.createSupportConversation(isAnimated, successCallback, errorCallback)
```

## [In-app link handling](#in-app-link-handling)

The DevRev SDK provides a mechanism to handle links opened from within any screen that is part of the DevRev SDK.

You can fully customize the link handling behavior by setting the specialized in-app link handler. That way you can decide what should happen when a link is opened from within the app.

```
DevRev.setInAppLinkHandler(handler, successCallback, errorCallback)
```

You can further customize the behavior by setting the `setShouldDismissModalsOnOpenLink` boolean flag. This flag controls whether the DevRev SDK should dismiss the top-most modal screen when a link is opened.

```
DevRev.setShouldDismissModalsOnOpenLink(value, successCallback, errorCallback)
```

## [Analytics](#analytics)

The DevRev SDK allows you to send custom analytic events by using a properties map. You can track these events using the following function:

This functionality requires the SDK to be configured and the user to be identified, whether they are unverified or verified.

```
DevRev.trackEvent(name, properties, successCallback, errorCallback)
```

Avoid passing special characters in the event name and properties, as these characters can lead to file corruption and missed recordings.

## [Manage session analytics](#manage-session-analytics)

The DevRev SDK offers session analytics features to help you understand how users interact with your app.

### [Opt in or out](#opt-in-or-out)

Session analytics features are opted-in by default, enabling them from the start. However, you can opt-out using the following method:

```
DevRev.stopAllMonitoring(successCallback, errorCallback)
```

To opt back in, use the following method:

```
DevRev.resumeAllMonitoring(successCallback, errorCallback)
```

### [Session recording](#session-recording)

You can enable session recording to capture user interactions with your app.

The session recording feature is opt-out and is enabled by default.

The session recording feature includes the following methods to control the recording:

| Method | Action |
| --- | --- |
| `DevRev.startRecording(successCallback, errorCallback)` | Starts the session recording. |
| `DevRev.stopRecording(successCallback, errorCallback)` | Ends the session recording and uploads it to the portal. |
| `DevRev.pauseRecording(successCallback, errorCallback)` | Pauses the ongoing session recording. |
| `DevRev.resumeRecording(successCallback, errorCallback)` | Resumes a paused session recording. |

### [Session properties](#session-properties)

You can add custom properties to the session recording to help you understand the context of the session. The properties are defined as a map of string values.

```
DevRev.addSessionProperties(properties, successCallback, errorCallback)
```

To clear the session properties in scenarios such as user logout or when the session ends, use the following method:

```
DevRev.clearSessionProperties(successCallback, errorCallback)
```

Avoid passing special characters in the session properties, as these characters can lead to file corruption and missed recordings.

### [Mask sensitive data](#mask-sensitive-data)

To protect sensitive data, the DevRev SDK provides an auto-masking feature that masks data before sending to the server. Input views such as password text fields are automatically masked.

While the auto-masking feature is sufficient for most situations, you can manually mark or unmark additional views as sensitive.

To mark elements as sensitive inside a web view (`WebView`), apply the `devrev-mask` CSS class. To unmark them, use `devrev-unmask`.

1. Mark an element as masked.

   ```
   <label class="devrev-mask">OTP: 12345</label>
   ```
2. Mark an element as unmasked.

   ```
   <input type="text" placeholder="Enter Username" name="username" required class="devrev-unmask">
   ```

### [Manage user interaction tracking](#manage-user-interaction-tracking)

The DevRev SDK automatically tracks user interactions such as taps, swipes, and scrolls. However, in some cases you may want to disable this tracking to prevent sensitive user actions from being recorded.

To temporarily disable user interaction tracking, use the following method:

```
DevRev.pauseUserInteractionTracking(successCallback, errorCallback)
```

To resume user interaction tracking, use the following method:

```
DevRev.resumeUserInteractionTracking(successCallback, errorCallback)
```

### [Implement timers](#implement-timers)

The DevRev SDK offers a timer mechanism to measure the time spent on specific tasks, allowing you to track events such as response time, loading time, or any other duration-based metrics.

The mechanism utilizes balanced start and stop methods, both of which accept a timer name and an optional dictionary of properties.

To start a timer, use the following method:

```
DevRev.startTimer(name, properties, successCallback, errorCallback)
```

To stop a timer, use the following method:

```
DevRev.endTimer(name, properties, successCallback, errorCallback)
```

Avoid passing special characters in the timer properties, as these characters can lead to file corruption and missed recordings.

### [Capture errors](#capture-errors)

You can report a handled error from a catch block using the `captureError` function.

This ensures that even if the error is handled in your app, it is still logged for diagnostics.

```
DevRev.captureError(
    error,
    tag
)
```

For example:

```
try {
} catch (e) {
    DevRev.captureError(
        e,
        'network-failure'
    );
}
```

### [Manage screen tracking](#manage-screen-tracking)

The DevRev SDK offers automatic screen tracking to help you understand how users navigate through your app. Although screens are automatically tracked, you can manually track screens using the following method:

```
DevRev.trackScreenName(screenName, successCallback, errorCallback)
```

## [Push notifications](#push-notifications)

You can configure your app to receive push notifications from the DevRev SDK. The SDK is designed to handle push notifications and execute actions based on the notification's content.

The DevRev backend sends push notifications to your app to alert users about new messages in the Plug support chat.

### [Configuration](#configuration)

To receive push notifications, you need to configure your DevRev organization by following the instructions in the [push notifications](https://developer.devrev.ai/sdks/push-notifications) section.

### [Register for push notifications](#register-for-push-notifications)

Push notifications require SDK configuration and user identification, whether unverified or verified, to ensure delivery to the correct user.

The DevRev SDK offers a method to register your device for receiving push notifications. You can register for push notifications using the following method:

```
DevRev.registerDeviceToken(deviceToken, deviceID, successCallback, errorCallback)
```

On Android devices, the `deviceToken` should be the Firebase Cloud Messaging (FCM) token value, while on iOS devices, it should be the Apple Push Notification Service (APNS) token.

### [Unregister from push notifications](#unregister-from-push-notifications)

If your app no longer needs to receive push notifications, you can unregister the device.

Use the following method to unregister the device:

```
DevRev.unregisterDevice(deviceID, successCallback, errorCallback)
```

### [Processing push notifications](#processing-push-notifications)

#### [Android](#android)

On Android, notifications are implemented as data messages to offer flexibility. However, this means that automatic click processing isn't available. To handle notification clicks, developers need to intercept the click event, extract the payload, and pass it to a designated method for processing. This custom approach enables tailored notification handling in Android applications.

To process the notification, use the following method:

```
DevRev.processPushNotification(payload, successCallback, errorCallback)
```

Here, the `message` object from the notification payload should be passed to this function.

For example:

```
const notificationPayload = {
	"message": {
		"title": "New Message",
		"body": "You have received a new message.",
		"data": {
			"messageId": "12345",
			"sender": "John Doe"
		}
	}
};

const messageJson = notificationPayload["message"];

DevRev.processPushNotification(messageJson, function() {
	console.log("Push notification processed successfully.");
}, function(error) {
	console.error("Failed to process push notification:", error);
});
```

#### [iOS](#ios)

On iOS devices, you must pass the received push notification payload to the DevRev SDK for processing. The SDK will then handle the notification and execute the necessary actions.

```
DevRev.processPushNotification(payload, successCallback, errorCallback)
```

For example:

```
const notificationPayload = {
	"message": {
		"title": "New Message",
		"body": "You have received a new message.",
		"data": {
			"messageId": "12345",
			"sender": "John Doe"
		}
	}
};

const messageJson = notificationPayload["message"];

DevRev.processPushNotification(messageJson, function() {
	console.log("Push notification processed successfully.");
}, function(error) {
	console.error("Failed to process push notification:", error);
});
```

Last updated on

[Quickstart guide

Previous Page](/sdks/cordova/quickstart)[Migration guide

Next Page](/sdks/cordova/migration-guide)

## Source
- DevRev developer docs: [Features](https://developer.devrev.ai/sdks/cordova/features)
