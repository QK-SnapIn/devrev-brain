---
title: Quickstart guide
type: developer-doc
status: stable
source: developer.devrev.ai
category: sdks
source_url: https://developer.devrev.ai/sdks/android/quickstart
last_updated: 2026-05-11
summary: "To integrate the latest version of our SDK into your app, follow these steps:"
---

# Quickstart guide

DevRev SDK for Android

# Quickstart guide

## [Requirements](#requirements)

* Android Studio 2025.1.1 or later.
* Android Gradle Plugin 8.2 or later.
* Gradle 8.9 or later.
* Minimum Android API level 24.

## [Integration](#integration)

To integrate the latest version of our SDK into your app, follow these steps:

1. Add the following dependencies to your app's `build.gradle.kts` file:

   ```
   dependencies {
    implementation("ai.devrev.sdk:devrev-sdk:<VERSION>")
   }
   ```
2. Add `mavenCentral` to your root `build.gradle.kts` file:

   ```
   repositories {
    mavenCentral()
   }
   ```

1. Add the following dependencies to your app's `build.gradle` file:

   ```
   dependencies {
    implementation 'ai.devrev.sdk:devrev-sdk:<VERSION>'
   }
   ```
2. Add `mavenCentral` to your root `build.gradle` file:

   ```
   repositories {
       mavenCentral()
   }
   ```

### [ProGuard rules](#proguard-rules)

If you are using ProGuard in your project, add the following lines to your configuration:

```
-keep class ai.devrev.** { *; }
-keep class com.userexperior.* { *; }
```

## [Set up the DevRev SDK](#set-up-the-devrev-sdk)

1. Open the DevRev web app at <https://app.devrev.ai> and go to the **Settings** page.
2. Copy the value under **Your unique App ID** from **PLuG settings**.
3. Configure the DevRev SDK in your app using the obtained credentials.

The DevRev SDK must be configured before you can use any of its features.

The SDK becomes ready for use once the configuration API is executed. Remote configuration is fetched from the backend and cached locally. On subsequent launches, you can use the cached configuration to avoid a network round-trip and speed up cold start (see [Configuration caching](#configuration-caching)).

```
DevRev.configure(context: Context, appId: String)
```

```
DevRev.INSTANCE.configure(Context context, String appId, FeatureConfiguration featureConfiguration);
```

To provide a feature configuration during setup, call the overload that accepts it:

```
DevRev.configure(context: Context, appId: String, featureConfiguration: FeatureConfiguration)
```

```
DevRev.INSTANCE.configure(Context context, String appId, FeatureConfiguration featureConfiguration);
```

For default behavior, call the simpler overload:

```
DevRev.configure(context = this, appId = "<APP_ID>")
```

```
DevRev.INSTANCE.configure(this, "<APP_ID>", new FeatureConfiguration());
```

To customize behavior such as frame capture, auto-start recording, configuration caching, or theme preferences, pass a `FeatureConfiguration` instance:

```
DevRev.configure(
    context = this,
    appId = "<APP_ID>",
    featureConfiguration = FeatureConfiguration(
        enableFrameCapture = false,
        autoStartRecording = false,
        prefersDialogMode = false,
        alwaysUseRemoteConfig = true,
        supportWidgetTheme = SupportWidgetTheme(prefersSystemTheme = true)
    )
)
```

```
DevRev.INSTANCE.configure(
    this,
    "<APP_ID>",
    new FeatureConfiguration(
        false,   // enableFrameCapture
        false,   // autoStartRecording
        false,   // prefersDialogMode
        true,    // alwaysUseRemoteConfig
        new SupportWidgetTheme(true, null, null, null)
    )
);
```

Ensure that the custom application is specified in the `AndroidManifest.xml`:

```
<application
    android:name=".MyApp">
</application>
```

Use this property to check whether the DevRev SDK has been configured:

```
DevRev.isConfigured
```

```
DevRev.INSTANCE.isConfigured();
```

4. Call the following method inside your `Application` class to configure the SDK.

If you don’t have a custom `Application` class, create one as shown below.

```
import ai.devrev.sdk.DevRev

class FooApplication : Application() {

   override fun onCreate() {
      super.onCreate()
      DevRev.configure(
            context = this,
            appId = "<APP_ID>"
      )
   }
}
```

```
import ai.devrev.sdk.DevRev;
import ai.devrev.sdk.model.FeatureConfiguration;

public class FooApplication extends Application {

   @Override
   public void onCreate() {
      super.onCreate();
      DevRev.INSTANCE.configure(
            this,
            "<APP_ID>",
            new FeatureConfiguration()
      );
   }
}
```

5. In the `onCreate` method of your `Application`, configure the DevRev SDK with the required parameters using the credentials obtained earlier.
6. Ensure that the custom application is specified in the `AndroidManifest.xml`, as shown below:

```
<application
    android:name=".FooApplication">
</application>
```

### [Update the feature configuration](#update-the-feature-configuration)

You can adjust the feature configuration without reconfiguring the SDK:

```
DevRev.updateFeatureConfiguration(
    context = this,
    featureConfiguration = FeatureConfiguration(
        enableFrameCapture = true,
        supportWidgetTheme = SupportWidgetTheme(prefersSystemTheme = true)
    )
)
```

```
DevRev.INSTANCE.updateFeatureConfiguration(
    this,
    new FeatureConfiguration(
        true,    // enableFrameCapture
        new SupportWidgetTheme(true, null, null, null)
    )
);
```

The `autoStartRecording`, `prefersDialogMode`, and `alwaysUseRemoteConfig` flags can only be set during initial configuration and cannot be changed at runtime. Only `enableFrameCapture` and `supportWidgetTheme` can be updated using this method. To control recording manually, use `DevRev.startRecording()` and `DevRev.stopRecording()` methods.

### [Feature configuration reference](#feature-configuration-reference)

`FeatureConfiguration` controls how the SDK behaves both during initial setup and when calling `DevRev.updateFeatureConfiguration`.

```
val configuration = FeatureConfiguration.default
```

```
FeatureConfiguration configuration = new FeatureConfiguration();
```

| Property | Type | Default | Description |
| --- | --- | --- | --- |
| `enableFrameCapture` | `Boolean` | `true` | Enables the screen capture pipeline used by session replay. |
| `autoStartRecording` | `Boolean` | `true` | Automatically starts recording after the SDK finishes remote configuration (or when using cached config). |
| `prefersDialogMode` | `Boolean` | `false` | Opens SDK screens as a bottom sheet instead of a separate activity. |
| `alwaysUseRemoteConfig` | `Boolean` | `true` | When `true`, the SDK always fetches remote configuration at startup and when the app enters foreground. When `false`, the SDK uses cached configuration when available and skips the remote fetch, improving cold start. |
| `supportWidgetTheme` | `SupportWidgetTheme?` | `null` | Controls the appearance of the in-app support widget, including dynamic theme behavior. |

Use the constructor to override any combination of options:

```
val configuration = FeatureConfiguration(
    enableFrameCapture = false,
    autoStartRecording = false,
    prefersDialogMode = false,
    alwaysUseRemoteConfig = false,
    supportWidgetTheme = SupportWidgetTheme(prefersSystemTheme = true)
)
```

```
FeatureConfiguration configuration = new FeatureConfiguration(
    false,   // enableFrameCapture
    false,   // autoStartRecording
    false,   // prefersDialogMode
    false,   // alwaysUseRemoteConfig
    new SupportWidgetTheme(true, null, null, null)
);
```

#### [Configuration caching](#configuration-caching)

When `alwaysUseRemoteConfig` is `false`, the SDK uses the last successfully fetched configuration stored on the device. If a cached configuration exists, the SDK skips the remote config request at startup and applies the cached settings (for example, session replay, observability). This reduces cold-start latency and allows the app to work offline with the last known config. The first launch (or after clearing app data) still performs a remote fetch when network is available. Set `alwaysUseRemoteConfig` to `true` (the default) to retain the previous behavior of always fetching remote configuration at startup and when the app enters foreground.

#### [Support widget theme options](#support-widget-theme-options)

`SupportWidgetTheme` lets you fine-tune the support UI. Provide explicit values to customize:

```
val customTheme = SupportWidgetTheme(
    prefersSystemTheme = false,
    primaryTextColor = "#1F2933",
    accentColor = "#F97316",
    spacing = mapOf("bottom" to "20px", "side" to "16px")
)
```

```
SupportWidgetTheme customTheme = new SupportWidgetTheme(
    false,       // prefersSystemTheme
    "#1F2933",   // primaryTextColor
    "#F97316",   // accentColor
    new HashMap<String, String>() {{
        put("bottom", "20px");
        put("side", "16px");
    }}
);
```

| Property | Type | Default | Description |
| --- | --- | --- | --- |
| `prefersSystemTheme` | `Boolean?` | `null` | Follows the device appearance when `true`; otherwise uses your custom colors. |
| `primaryTextColor` | `String?` | `null` | Hex or RGB value for primary text in the support widget. |
| `accentColor` | `String?` | `null` | Hex or RGB value applied to buttons and highlights. |
| `spacing` | `Map<String, String>?` | `null` | CSS-like spacing overrides; `"bottom"` and `"side"` keys are recognized. |

## [Use the sample app](#use-the-sample-app)

A sample app demonstrates use cases with both XML-based UI and Jetpack Compose as part our [public repository](https://github.com/devrev/devrev-sdk-android).

Before running the sample app, make sure to configure it with your DevRev credentials. To do this, update the `ai.devrev.sdk.sample.DevRevApplication` class with your credentials.

Last updated on

[UserExperior migration

Previous Page](/sdks/web/migration)[Features

Next Page](/sdks/android/features)

## Source
- DevRev developer docs: [Quickstart guide](https://developer.devrev.ai/sdks/android/quickstart)
