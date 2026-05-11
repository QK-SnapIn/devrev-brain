---
title: Features
type: developer-doc
status: stable
source: developer.devrev.ai
category: sdks
source_url: https://developer.devrev.ai/sdks/android/features
last_updated: 2026-05-11
summary: "To access certain features of the DevRev SDK, user identification is required."
---

# Features

DevRev SDK for Android

# Features

## [Identification](#identification)

To access certain features of the DevRev SDK, user identification is required.

The identification function should be placed appropriately in your app after the user logs in. If you have the user information available at app launch, call the function after the `DevRev.configure(context, appID)` method.

The `Identity` structure allows for custom fields in the user, organization, and account traits. These fields must be configured through the DevRev app before they can be utilized. For more information, refer to [Object customization](https://devrev.ai/docs/product/object-customization).

### [Identify an unverified user](#identify-an-unverified-user)

The unverified identification method identifies users with a unique identifier, but it does not verify their identity with the DevRev backend.

```
DevRev.identifyUnverifiedUser(
  identity: Identity
)
```

```
DevRev.INSTANCE.identifyUnverifiedUser(
  Identity identity
);
```

The function accepts the `DevRev.Identity` structure, with the user identifier (`userID`) as the only required property, all other properties are optional.

For example:

```
// Identify an unverified user using their email address as the user identifier.
DevRev.identifyUnverifiedUser(Identity(userId = "user@example.org"))
```

```
// Identify an unverified user using their email address as the user identifier.
DevRev.identifyUnverifiedUser(
    new Identity("user@example.org", null, null, null, null, null)
);
```

### [Identify a verified user](#identify-a-verified-user)

The verified identification method is used to identify users with an identifier unique to your system within the DevRev platform. The verification is done through a token exchange process between you and the DevRev backend.

The steps to identify a verified user are as follows:

1. Generate an AAT for your system (preferably through your backend).
2. Exchange your AAT for a session token for each user of your system.
3. Pass the user identifier and the exchanged session token to the `DevRev.identifyVerifiedUser(userId: String, sessionToken: String)` method.

For security reasons, it is **strongly recommended** that the token exchange is executed on your backend to prevent exposing your application access token (AAT).

#### [Generate an AAT](#generate-an-aat)

1. Open the DevRev web app at <https://app.devrev.ai> and go to the **Settings** page.
2. Open the **PLuG Tokens** page.
3. Go to **Application access tokens** panel, click **New token**, and copy the displayed token.

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
DevRev.identifyVerifiedUser(userId: String, sessionToken: String)
```

```
DevRev.INSTANCE.identifyVerifiedUser(String userId, String sessionToken);
```

### [Updating the user](#updating-the-user)

To update a user's information, use the following method:

```
DevRev.updateUser(
  identity: Identity
)
```

```
DevRev.INSTANCE.updateUser(
  Identity identity
);
```

The function accepts the `DevRev.Identity` ojbect.

The `userID` property cannot be updated.

### [Logout](#logout)

You can perform a logout of the current user by calling the following method:

```
DevRev.logout(context: Context, deviceId: String)
```

```
DevRev.logout(context: Context, deviceId: String)
```

The user is logged out by clearing their credentials, as well as unregistering the device from receiving push notifications, and stopping the session recording.

### [Identity model](#identity-model)

The `Identity` class is used to provide user, organization, and account information when identifying users or updating their details. This class is used primarily with the `identifyUnverifiedUser(identity: Identity)` and `updateUser(identity: Identity)` methods.

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

## [Plug support chat](#plug-support-chat)

Once user identification is complete, you can start using the chat (conversations) dialog supported by our DevRev SDK. To open the chat dialog, your application should use the `showSupport` API, as shown in the following example:

```
DevRev.showSupport(context: Context)
```

```
DevRevExtKt.showSupport(DevRev.INSTANCE, context);
```

### [Create a new conversation](#create-a-new-conversation)

You have the ability to create a new conversation from within your app. The method shows the support chat screen and creates a new conversation at the same time.

```
DevRev.createSupportConversation(context: Context)
```

```
DevRev.INSTANCE.createSupportConversation(context);
```

### [Support button](#support-button)

The DevRev SDK also provides a support button, which can be integrated into your application. To include it on the current screen, add the following code to your XML layout:

```
<ai.devrev.sdk.plug.view.PlugFloatingActionButton
  android:id="@+id/plug_fab"
  android:layout_width="wrap_content"
  android:layout_height="wrap_content"
  android:layout_margin="24dp"
  app:layout_constraintBottom_toBottomOf="parent"
  app:layout_constraintEnd_toEndOf="parent" />
```

The support button can be customized using default parameters, enabling you to tailor its appearance to your application's design:

```
android:src="@your_drawable_here"
android:backgroundTint="@your_background_color"
```

## [In-app link handling](#in-app-link-handling)

The DevRev SDK provides a mechanism to handle links opened from within any screen that is part of the DevRev SDK.

You can fully customize the link handling behavior by setting the specialized in-app link handler. That way you can decide what should happen when a link is opened from within the app.

```
DevRev.setInAppLinkHandler(handler: (String) -> Unit)
```

```
DevRev.INSTANCE.setInAppLinkHandler(Function1<String, Unit> handler);
```

You can further customize the behavior by setting the `setShouldDismissModalsOnOpenLink` boolean flag. This flag controls whether the DevRev SDK should dismiss the top-most modal screen when a link is opened.

```
DevRev.setShouldDismissModalsOnOpenLink(value: boolean)
```

```
DevRev.INSTANCE.setShouldDismissModalsOnOpenLink(boolean value)
```

For example:

```
DevRev.setInAppLinkHandler { link ->
  // Do something here
}

DevRev.setShouldDismissModalsOnOpenLink(false)
```

```
DevRev.INSTANCE.setInAppLinkHandler(link -> {
  // Do something here
  return kotlin.Unit.INSTANCE;
});

DevRev.INSTANCE.setShouldDismissModalsOnOpenLink(false);
```

## [Dynamic theme configuration](#dynamic-theme-configuration)

The DevRev SDK allows you to configure the theme dynamically based on the system appearance, or use the theme configured on the DevRev portal. By default, the theme is dynamic and follows the system appearance.

Use `SupportWidgetTheme` inside your `FeatureConfiguration` to align the support experience with your brand:

```
DevRev.updateFeatureConfiguration(
    context = this,
    featureConfiguration = FeatureConfiguration(
        enableFrameCapture = true,
        supportWidgetTheme = SupportWidgetTheme(
            prefersSystemTheme = false,
            primaryTextColor = "#202020",
            accentColor = "#34C759"
        )
    )
)
```

```
DevRev.INSTANCE.updateFeatureConfiguration(
    this,
    new FeatureConfiguration(
        true,    // enableFrameCapture
        new SupportWidgetTheme(
            false,       // prefersSystemTheme
            "#202020",   // primaryTextColor
            "#34C759",   // accentColor
            null         // spacing
        )
    )
);
```

Directly mutating `DevRev.setShouldPreferSystemTheme` is maintained only for backward compatibility and is deprecated. Prefer configuring the theme through `SupportWidgetTheme` passed via `FeatureConfiguration`.

## [Track analytics](#track-analytics)

The DevRev SDK allows you to send custom analytic events by using a name and a string dictionary. You can track these events using the following function:

```
DevRev.trackEvent(name: String, properties: HashMap<String, String>)
```

```
DevRevAnalyticsExtKt.trackEvent(DevRev instance, String name, HashMap<String, String> properties);
```

For example:

```
DevRev.trackEvent(name = "open-message-screen", properties = {"id": "message-1337"})
```

```
DevRevAnalyticsExtKt.trackEvent(DevRev.INSTANCE, "open-message-screen", new HashMap<>().put("id", "message-1337"));
```

Avoid passing special characters in the event name and properties, as these characters can lead to file corruption and missed recordings.

## [Analyze sessions](#analyze-sessions)

The DevRev SDK provides observability features to help you understand how your users are interacting with your app.

### [Opt in or out](#opt-in-or-out)

Session analytics features are opted-in by default, enabling them from the start. However, you can opt-out using the following method:

```
DevRev.stopAllMonitoring()
```

```
DevRevObservabilityExtKt.stopAllMonitoring(DevRev.INSTANCE);
```

To opt back in, use the following method:

```
DevRev.resumeAllMonitoring()
```

```
DevRevObservabilityExtKt.resumeAllMonitoring(DevRev.INSTANCE);
```

You can check whether session monitoring has been enabled by using this property:

```
DevRev.isMonitoringEnabled
```

```
DevRevObservabilityExtKt.isMonitoringEnabled(DevRev.INSTANCE);
```

This feature will only store a monitoring permission flag, it will **not** provide any UI or dialog.

### [Session recording](#session-recording)

You can enable session recording to capture user interactions with your app.

The session recording feature is opt-out and is enabled by default.

Here are the available methods to help you control the session recording feature:

| Method | Action |
| --- | --- |
| `DevRev.startRecording()` | Starts the session recording. |
| `DevRev.stopRecording()` | Ends the session recording and uploads it to the portal. |
| `DevRev.pauseRecording()` | Pauses the ongoing session recording. |
| `DevRev.resumeRecording()` | Resumes a paused session recording. |
| `DevRev.processAllOnDemandSessions()` | Stops the ongoing user recording and sends all on-demand sessions along with the current recording. |

| Method | Action |
| --- | --- |
| `DevRevObservabilityExtKt.startRecording(DevRev.INSTANCE, context)` | Starts the session recording. |
| `DevRevObservabilityExtKt.stopRecording(DevRev.INSTANCE)` | Ends the session recording and uploads it to the portal. |
| `DevRevObservabilityExtKt.pauseRecording(DevRev.INSTANCE)` | Pauses the ongoing session recording. |
| `DevRevObservabilityExtKt.resumeRecording(DevRev.INSTANCE)` | Resumes a paused session recording. |
| `DevRevObservabilityExtKt.processAllOnDemandSessions(DevRev.INSTANCE)` | Stops the ongoing user recording and sends all on-demand sessions along with the current recording. |

Using this property returns the status of the session recording:

```
DevRev.isRecording
```

```
DevRevObservabilityExtKt.isRecording(DevRev.INSTANCE);
```

To check if on-demand sessions are enabled, use:

```
DevRev.areOnDemandSessionsEnabled
```

```
DevRevObservabilityExtKt.areOnDemandSessionsEnabled(DevRev.INSTANCE);
```

### [Fetch async config](#fetch-async-config)

The sessions will be uploaded only when the app is in the background.

The SDK can be configured to fetch configuration asynchronously to improve app startup time. When enabled, the SDK uses cached configuration for immediate startup and fetches fresh configuration from the server in the background.

This setting should be called before `startRecording()` for it to take effect. By default, it is disabled for backward compatibility.

To enable the async config fetching mechanism, use:

```
DevRev.setAsyncConfigFetchEnabled(context, true)
```

```
DevRevObservabilityExtKt.setAsyncConfigFetchEnabled(DevRev.INSTANCE, context, true);
```

**Behavior when enabled:**

* Immediately uses cached config to decide whether to start recording.
* Does not start recording if cached config indicates it is disabled (respects dashboard setting).
* Fetches fresh config in the background without blocking startup.
* Stops recording immediately if fresh config disables it after recording started.
* Defers session uploads until the app is in the background.
* Prioritizes crash and ANR reports for immediate upload.
* Uploads regular sessions sequentially (one at a time) to reduce network contention.

This optimization is particularly beneficial for apps experiencing slow startup times on poor network connections.

### [Add session properties](#add-session-properties)

You can add custom properties to the session recording to help you understand the context of the session. The properties are defined as a dictionary of string values.

```
DevRev.addSessionProperties(properties: HashMap<String, String>)
```

```
DevRevObservabilityExtKt.addSessionProperties(DevRev.INSTANCE, HashMap<String, String> properties);
```

To clear the session properties in scenarios such as user logout or when the session ends, use the following method:

```
DevRev.clearSessionProperties()
```

```
DevRevObservabilityExtKt.clearSessionProperties(DevRev.INSTANCE);
```

Avoid passing special characters in the session properties, as these characters can lead to file corruption and missed recordings.

### [Mask sensitive data](#mask-sensitive-data)

To protect sensitive data, the DevRev SDK provides an auto-masking feature that masks data before sending to the server. Input views such as text fields, text views, and web views are automatically masked.

While the auto-masking feature may be sufficient for most situations, you can manually mark/unmark additional views as sensitive.

The SDK provides two approaches to manually mask or unmask your views, using a set of predefined tags or using the API methods.

#### [Mask using predefined tags](#mask-using-predefined-tags)

Use the tag method only when you don't have any other tag already applied to your UI element.

Masking views using the predefined tags is the simplest way to mask your views, use the tag `devrev-mask` to mask a view and `devrev-unmask` to unmask a view.

* Mark a view as masked:

  ```
  android:tag="devrev-mask"
  ```
* Mark a view as unmasked:

  ```
  android:tag="devrev-unmask"
  ```

For example:

```
<!-- A masked web view -->
<WebView
  android:id="@+id/webview1"
  android:layout_width="fill_parent"
  android:layout_height="200dp"
  android:background="@android:color/transparent"
  android:tag="devrev-mask" />

<!-- An unmasked web view -->
<WebView
  android:id="@+id/webview2"
  android:layout_width="fill_parent"
  android:layout_height="200dp"
  android:background="@android:color/transparent"
  android:tag="devrev-unmask" />
```

The tags can also be set programmatically:

* Mark a view as masked:

  ```
  val firstView: View = findViewById(R.id.firstView)
  firstView.tag = "devrev-mask"
  ```
* Mark a view as unmasked:

  ```
  val secondView: View = findViewById(R.id.secondView)
  secondView.tag = "devrev-unmask"
  ```

* Mark a view as masked:

  ```
  View firstView = findViewById(R.id.firstView);
  firstView.setTag("devrev-mask");
  ```
* Mark a view as unmasked:

  ```
  View secondView = findViewById(R.id.secondView);
  secondView.setTag("devrev-unmask");
  ```

#### [Mask using the API methods](#mask-using-the-api-methods)

You can also use the API methods to mask or unmask your views programmatically.

* Mark a view as masked:

  ```
  DevRev.markSensitiveViews(sensitiveViews: List<View>)
  ```
* Mark a view as unmasked:

  ```
  DevRev.unmarkSensitiveViews(sensitiveViews: List<View>)
  ```

* Mark a view as masked:

  ```
  DevRevObservabilityExtKt.markSensitiveViews(DevRev.INSTANCE, List<View> sensitiveViews);
  ```
* Mark a view as unmasked:

  ```
  DevRevObservabilityExtKt.unmarkSensitiveViews(DevRev.INSTANCE, List<View> sensitiveViews);
  ```

For example:

```
// Mark two views as masked.

val view1 = findViewById(R.id.view1)
val view2 = findViewById(R.id.view2)

DevRev.markSensitiveViews(listOf(view1, view2))

// Mark two views as unmasked.

val view3 = findViewById(R.id.view3)
val view4 = findViewById(R.id.view4)

DevRev.unmarkSensitiveViews(listOf(view3, view4))
```

```
// Mark two views as masked.

View view1 = findViewById(R.id.view1);
View view2 = findViewById(R.id.view2);

List<View> sensitiveViewsList = new ArrayList<>();
sensitiveViewsList.add(view1);
sensitiveViewsList.add(view2);

DevRevObservabilityExtKt.markSensitiveViews(DevRev.INSTANCE, sensitiveViewsList);

// Mark two views as unmasked.

View view3 = findViewById(R.id.view3);
View view4 = findViewById(R.id.view4);

List<View> sensitiveViewsList = new ArrayList<>();
sensitiveViewsList.add(view3);
sensitiveViewsList.add(view4);

DevRevObservabilityExtKt.unmarkSensitiveViews(DevRev.INSTANCE, sensitiveViewsList);
```

#### [Mask Jetpack Compose views](#mask-jetpack-compose-views)

If you want to mask any Jetpack Compose UI elements or views, you can apply a mask on it using a modifier.

```
modifier = Modifier.markAsMaskedLocation("VIEW_NAME_OR_ID")
```

For example:

```
TextField(
     modifier = Modifier
       .markAsMaskedLocation("myTextField")
       .padding(horizontal = 20.dp)
       .onGloballyPositioned { coordinates = it },
     value = input,
     onValueChange = { input = it }
)
```

#### [Mask elements inside web views](#mask-elements-inside-web-views)

Masking elements inside web views (`WebView`) can be achieved by using the CSS class `devrev-mask` to mask an element and `devrev-unmask` to unmask an element.

* Mark an element as masked:

  ```
  <label class="devrev-mask">OTP: 12345</label>
  ```
* Mark an element as unmasked:

  ```
  <input type="text" placeholder="Enter Username" name="username" required class="devrev-unmask">
  ```

#### [Custom masking provider](#custom-masking-provider)

For advanced use cases, you can provide a custom masking provider to explicitly specify which regions of the UI should be masked during snapshots.

You can implement your own masking logic by creating a class that implements the `MaskLocationProvider` interface and setting your custom object as the masking provider. This allows you to specify explicit regions to be masked or to skip snapshots entirely.

| Symbol | Description |
| --- | --- |
| `DevRev.setMaskLocationProvider(maskLocationProvider: MaskLocationProvider)` | A custom provider that determines which UI regions should be masked for privacy during snapshots (this overrides any previously set provider). |
| `MaskLocationProvider` | An interface for providing explicit masking locations for UI snapshots. |
| `SnapshotMask` | An object that describes the regions of a snapshot to be masked. |
| `SnapshotMask.Location` | An object that describes a masked region. |

For example:

```
import com.userexperior.bridge.model.MaskLocationProvider
import com.userexperior.bridge.model.SnapshotMask
import com.userexperior.bridge.model.SnapshotMaskCallback
import ai.devrev.sdk.setMaskLocationProvider
import ai.devrev.sdk.DevRev
import android.graphics.Rect

class MyMaskingProvider : MaskLocationProvider {
    init {
      // Register the custom masking provider
      DevRev.setMaskLocationProvider(this)
    }

    override fun provideSnapshotMask(callback: SnapshotMaskCallback) {
      // Create a MutableSet to hold the masked regions
      val locations: MutableSet<Rect> = mutableSetOf()

      // Define the regions to be masked
      val rect1 = Rect(0, 0, 100, 50)
      val rect2 = Rect(50, 50, 150, 100)

      // Add the regions to the Set
      locations.add(rect1)
      locations.add(rect2)

      callback.onSnapshotMask(
        SnapshotMask(
          locations,
          false
        )
      )
    }
}
```

```
import com.userexperior.bridge.model.MaskLocationProvider;
import com.userexperior.bridge.model.SnapshotMask;
import com.userexperior.bridge.model.SnapshotMaskCallback;
import ai.devrev.sdk.DevRevObservabilityExtKt;
import ai.devrev.sdk.DevRev;
import android.graphics.Rect;
import java.util.HashSet;
import java.util.Set;

public class MyMaskingProvider implements MaskLocationProvider {
    public MyMaskingProvider() {
      // Register the custom masking provider
      DevRevObservabilityExtKt.setMaskLocationProvider(DevRev.INSTANCE, this);
    }

    @Override
    public void provideSnapshotMask(SnapshotMaskCallback callback) {
        if (callback != null) {
            // Create a Set to hold the masked regions
            Set<Rect> locations = new HashSet<>();

            // Define the regions to be masked
            Rect rect1 = new Rect(0, 0, 100, 100);
            Rect rect2 = new Rect(50, 50, 150, 150);

            // Add the regions to the Set
            locations.add(rect1);
            locations.add(rect2);

            callback.onSnapshotMask(
                new SnapshotMask(
                    locations,
                    false
                )
            );
        }
    }
}
```

Setting a new provider overrides any previously set masking location provider.

### [Track user interactions](#track-user-interactions)

The DevRev SDK automatically tracks user interactions such as taps, swipes, and scrolls. However, in some cases you may want to disable this tracking to prevent sensitive user actions from being recorded.

To temporarily disable user interaction tracking, use the following method:

```
DevRev.pauseUserInteractionTracking()
```

```
DevRevObservabilityExtKt.pauseUserInteractionTracking(DevRev.INSTANCE);
```

To resume user interaction tracking, use the following method:

```
DevRev.resumeUserInteractionTracking()
```

```
DevRevObservabilityExtKt.resumeUserInteractionTracking(DevRev.INSTANCE);
```

### [Use timers](#use-timers)

The DevRev SDK offers a timer mechanism to measure the time spent on specific tasks, allowing you to track events such as response time, loading time, or any other duration-based metrics.

The mechanism works using balanced start and stop methods that both accept a timer name and an optional dictionary of properties.

To start a timer, use the following method:

```
DevRev.startTimer(name: String, properties: HashMap<String, String>)
```

```
DevRevObservabilityExtKt.startTimer(DevRev.INSTANCE, String name, HashMap<String, String> properties);
```

To stop a timer, use the following method:

```
DevRev.endTimer(name: String, properties: HashMap<String, String>)
```

```
DevRevObservabilityExtKt.endTimer(DevRev.INSTANCE, String name, HashMap<String, String> properties);
```

For example:

```
DevRev.startTimer("response-time", properties: {"id": "task-1337"})

// Perform the task that you want to measure.

DevRev.endTimer("response-time", properties: {"id": "task-1337"})
```

```
DevRevObservabilityExtKt.startTimer(DevRev.INSTANCE, "response-time", new HashMap<String, String>().put("id", "task-1337"));

// Perform the task that you want to measure.

DevRevObservabilityExtKt.endTimer(DevRev.INSTANCE, "response-time", new HashMap<String, String>().put("id", "task-1337"));
```

Avoid passing special characters in the timer properties, as these characters can lead to file corruption and missed recordings.

### [Capture errors](#capture-errors)

You can report a handled exception from a catch block using the `captureError` function.
This ensures that even if the exception is handled in your app, it is still logged for diagnostics.

```
DevRev.captureError(
  exception: Throwable,
  tag: String
)
```

```
DevRevObservabilityExtKt.captureError(
  DevRev.INSTANCE,
  Throwable exception,
  String tag
);
```

### [Track screens](#track-screens)

The DevRev SDK offers automatic screen tracking to help you understand how users navigate through your app. Although activities and fragments are automatically tracked, you can manually track screens using the following method:

```
DevRev.trackScreenName(screenName: String)
```

```
DevRevObservabilityExtKt.trackScreenName(DevRev.INSTANCE, String screenName);
```

For example:

```
DevRev.trackScreenName("profile-screen")
```

```
DevRevObservabilityExtKt.trackScreenName(DevRev.INSTANCE, "profile-screen");
```

### [Manage screen transitions](#manage-screen-transitions)

The DevRev SDK allows tracking of screen transitions to understand the user navigation within your app.
You can check if a screen transition is in progress and manually update the state using the following methods:

#### [Check if the screen is transitioning](#check-if-the-screen-is-transitioning)

```
val isTransitioning = DevRev.isInScreenTransitioning
```

```
boolean isTransitioning = DevRevObservabilityExtKt.isInScreenTransitioning(DevRev.INSTANCE);
```

#### [Set screen transitioning state](#set-screen-transitioning-state)

```
// Mark the transition as started.
DevRev.setInScreenTransitioning(true)

// Mark the transition as ended.
DevRev.setInScreenTransitioning(false)
```

```
// Mark the transition as started.
DevRevObservabilityExtKt.setInScreenTransitioning(DevRev.INSTANCE, true)

// Mark the transition as ended.
DevRevObservabilityExtKt.setInScreenTransitioning(DevRev.INSTANCE, false)
```

## [Push notifications](#push-notifications)

You can configure your app to receive push notifications from the DevRev SDK. The SDK is designed to handle push notifications and execute actions based on the notification's content.

The DevRev backend sends push notifications to your app to notify users about new messages in the Plug support chat.

### [Configuration](#configuration)

To receive push notifications, you need to configure your DevRev organization by following the instructions in the [push notifications](https://developer.devrev.ai/sdks/push-notifications) section.

You need to ensure that your Android app is configured to receive push notifications. To set it up, follow the [Firebase documentation](https://firebase.google.com/docs/cloud-messaging/android/client).

### [Register for push notifications](#register-for-push-notifications)

Push notifications require that the SDK has been configured and the user has been identified (unverified users). The user identification is required to send the push notification to the correct user.

The DevRev SDK offers a method to register your device for receiving push notifications. You can register for push notifications using the following method:

```
DevRev.registerDeviceToken(
  context: Context,
  deviceToken: String,
  deviceId: String
)
```

```
DevRev.INSTANCE.registerDeviceToken(
  Context context,
  String deviceToken,
  String deviceId
);
```

The method requires a device identifier that persists across device restarts and app launches. This could be a Firebase installation ID, Android ID, or a unique system identifier. To obtain the device token for Firebase Cloud Messaging, follow these steps:

1. Use the `FirebaseMessaging` object.
2. Call the `firebaseMessaging.token.await()` method.

This method generates and returns the device token.

```
val firebaseMessaging = FirebaseMessaging.getInstance()
val token = firebaseMessaging.token.await()
// Use the token as needed
```

### [Unregister from push notifications](#unregister-from-push-notifications)

If your app no longer needs to receive push notifications, you can unregister the device.

Use the following method to unregister the device:

The method requires the device identifier, which should be the same as the one used when registering the device.

```
DevRev.unregisterDevice(
  context: Context,
  deviceId: String
)
```

```
DevRev.INSTANCE.unregisterDevice(
  Context context,
  String deviceId
);
```

The method requires the device identifier, which should be the same as the one used when registering the device.

### [Handle push notifications](#handle-push-notifications)

The DevRev SDK currently does not support automatic handling of push notifications. To open the Plug chat and manage navigation internally, you must pass the message payload received in the notification to the SDK.

```
DevRev.processPushNotification(
  context: Context,
  userInfo: String
)
```

```
DevRev.INSTANCE.processPushNotification(
  Context context,
  String userInfo
);
```

To extract the notification payload, do the following:

1. In Firebase Cloud Messaging (FCM), when a push notification is received, it triggers the `onMessageReceived` function in your `FirebaseMessagingService` class.
2. This function receives a `RemoteMessage` object as a parameter, which contains the notification data.
3. The `RemoteMessage` object has a `data` property, which is a map containing key-value pairs of the notification payload.
4. To extract a specific piece of data from the payload, use the key to access the value in the data map.
5. To retrieve the "message" from the payload:

```
val message = remoteMessage.data["message"]
```

```
String messageData = remoteMessage.getData().get("message");
```

For example:

```
class MyFirebaseMessagingService: FirebaseMessagingService {
  // ...

  override fun onMessageReceived(remoteMessage: RemoteMessage) {
    // ...
    val messageData = remoteMessage.data["message"]
    DevRev.processPushNotification(messageData)
  }
}
```

```
public class MyFirebaseMessagingService extends FirebaseMessagingService {
  // ...

  @Override
  public void onMessageReceived(RemoteMessage remoteMessage) {
    // ...
    String messageData = remoteMessage.getData().get("message");
    DevRev.processPushNotification(messageData);
  }
}
```

Last updated on

[Quickstart guide

Previous Page](/sdks/android/quickstart)[Migration guide

Next Page](/sdks/android/migration-guide)

## Source
- DevRev developer docs: [Features](https://developer.devrev.ai/sdks/android/features)
