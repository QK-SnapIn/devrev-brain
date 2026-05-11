---
title: Quickstart guide
type: developer-doc
status: stable
source: developer.devrev.ai
category: sdks
source_url: https://developer.devrev.ai/sdks/ios/quickstart
last_updated: 2026-05-11
summary: "The DevRev SDK can be integrated using either Swift Package Manager (SPM) or CocoaPods."
---

# Quickstart guide

DevRev SDK for iOS

# Quickstart guide

## [Requirements](#requirements)

* Xcode 16.0 or later (latest stable version available on the App Store).
* Swift 5.9 or later.
* The minimum deployment target should be 15.0.
* Recommended: An SSH key configured locally and registered with [GitHub](https://docs.github.com/en/github/authenticating-to-github/connecting-to-github-with-ssh).

## [Integration](#integration)

The DevRev SDK can be integrated using either Swift Package Manager (SPM) or CocoaPods.

We recommend integrating the DevRev SDK using Swift Package Manager and SSH. CocoaPods is in [maintenance mode](https://blog.cocoapods.org/CocoaPods-Support-Plans/) since August 2024 and will be [deprecated in the future](https://blog.cocoapods.org/CocoaPods-Specs-Repo/).

### [Swift Package Manager](#swift-package-manager)

To integrate the DevRev SDK into your project using SPM:

1. Open your project in Xcode and go to the **Add Package Dependency**.
2. Enter the DevRev SDK URL under **Enter Package URL**:
   * For SSH: `git@github.com:devrev/devrev-sdk-ios.git` (recommended)
   * For HTTPS: <https://github.com/devrev/devrev-sdk-ios>
3. In the **Build Phases** section of your app target, locate the **Link Binary With Libraries** phase and confirm that `DevRevSDK` is linked. If not, add it by clicking **+** and selecting `DevRevSDK` from the list.

Now you should be able to import and use the DevRev SDK in your project.

### [CocoaPods](#cocoapods)

To integrate the DevRev SDK using CocoaPods:

1. Add the following to your Podfile:

   ```
   pod 'DevRevSDK', '~> <VERSION>'
   ```
2. Run `pod install` in your project directory.

This will install the DevRev SDK in your project, making it ready for use.

## [Set up the DevRev SDK](#set-up-the-devrev-sdk)

1. Open the DevRev web app at <https://app.devrev.ai> and go to the **Settings** page.
2. Under **PLuG settings** copy the value under **Your unique App ID**.
3. Configure the DevRev SDK in your app using the obtained credentials.

The DevRev SDK must be configured before you can use any of its features.

The SDK becomes ready for use once the configuration API is executed. Remote configuration is fetched from the backend and cached locally. On subsequent launches, you can use the cached configuration to avoid a network round-trip and speed up cold start (see [Configuration caching](#configuration-caching)).

```
DevRev.configure(appID:)
```

To provide a feature configuration during setup, call the overload that accepts it:

```
DevRev.configure(appID:featureConfiguration:)
```

For default behavior, call the simpler overload:

```
DevRev.configure(appID: "abcdefg12345")
```

To customize behavior such as frame capture, auto-start recording, configuration caching, or theme preferences, pass a `FeatureConfiguration` instance:

```
DevRev.configure(
	appID: "abcdefg12345",
	featureConfiguration: FeatureConfiguration(
		enableFrameCapture: false,
		autoStartRecording: false,
		alwaysUseRemoteConfig: true,
		supportWidgetTheme: .systemDefault
	)
)
```

### [Update the feature configuration](#update-the-feature-configuration)

You can adjust the feature configuration without reconfiguring the SDK:

```
DevRev.updateFeatureConfiguration(
	FeatureConfiguration(
		enableFrameCapture: true,
		autoStartRecording: true,
		alwaysUseRemoteConfig: true,
		supportWidgetTheme: .systemDefault
	)
)
```

### [Feature configuration reference](#feature-configuration-reference)

`FeatureConfiguration` controls how the SDK behaves both during initial setup and when calling `DevRev.updateFeatureConfiguration(_:)`.

```
let configuration = FeatureConfiguration.default
```

| Property | Type | Default | Description |
| --- | --- | --- | --- |
| `enableFrameCapture` | `Bool` | `true` | Enables the screen capture pipeline used by session replay. |
| `autoStartRecording` | `Bool` | `true` | Automatically starts recording after the SDK finishes remote configuration (or when using cached config). |
| `alwaysUseRemoteConfig` | `Bool` | `true` | When `true`, the SDK always fetches remote configuration at startup and when the app enters background. When `false`, the SDK uses cached configuration when available and skips the remote fetch, improving cold start. |
| `supportWidgetTheme` | `SupportWidgetTheme` | `.systemDefault` | Controls the appearance of the in-app support widget, including dynamic theme behavior. |

Use the designated initializer to override any combination of options:

```
let configuration = FeatureConfiguration(
	enableFrameCapture: false,
	autoStartRecording: false,
	alwaysUseRemoteConfig: false,
	supportWidgetTheme: .systemDefault
)
```

When you only need to toggle frame capture while preserving the current runtime values for other options, use the convenience initializer:

```
DevRev.updateFeatureConfiguration(
	.init(withShouldEnableFrameCapture: false)
)
```

When you only need to change the support widget theme, use the convenience initializer that preserves the current values for other options:

```
DevRev.updateFeatureConfiguration(
	.init(witCustomSupportWidgetTheme: .systemDefault)
)
```

#### [Configuration caching](#configuration-caching)

When `alwaysUseRemoteConfig` is `false`, the SDK uses the last successfully fetched configuration stored on the device. If a cached configuration exists, the SDK skips the remote config request at startup and applies the cached settings (for example, session replay, observability). This reduces cold-start latency and allows the app to work offline with the last known config. The first launch (or after clearing app data) still performs a remote fetch when network is available. Set `alwaysUseRemoteConfig: true` (the default) to retain the previous behavior of always fetching remote configuration at startup and when the app enters background.

#### [Support widget theme options](#support-widget-theme-options)

`SupportWidgetTheme` lets you fine-tune the support UI. Start from `.systemDefault` or provide explicit values:

```
let customTheme = SupportWidgetTheme(
	prefersSystemTheme: false,
	primaryTextColor: "#1F2933",
	accentColor: "#F97316",
	spacing: [
		"bottom": "20px",
		"side": "16px"
	]
)
```

| Property | Type | Default | Description |
| --- | --- | --- | --- |
| `prefersSystemTheme` | `Bool` | `true` | Follows the device appearance when `true`; otherwise uses your custom colors. |
| `primaryTextColor` | `String?` | `nil` | Hex or RGB value for primary text in the support widget. |
| `accentColor` | `String?` | `nil` | Hex or RGB value applied to buttons and highlights. |
| `spacing` | `[String: String]?` | `nil` | CSS-like spacing overrides (`"bottom"` and `"side"` keys are recognized). |

1. For UIKit apps, configure the SDK in the `AppDelegate.application(_:didFinishLaunchingWithOptions:)` method.
2. For SwiftUI apps, depending on your app's architecture, configure the SDK at the app's entry point or initial view.

## [Use the sample app](#use-the-sample-app)

A sample app with use cases for both UIKit and SwiftUI has been provided as part of our [public repository](https://github.com/devrev/devrev-sdk-ios).

Before you start using the sample app you need to configure it to be used with your Apple Developer team and your DevRev credentials. For your convenience the code is marked with compiler error directives (`#error`) at the places that need attention.

1. Add your credentials to the relevant `AppDelegate.swift` of the SwiftUI or UIKit sample.
   * After you have added the credentials, delete or comment out the compiler error lines in the respective files.
2. Configure the code signing for the sample target:
   * Open the project settings (1),
   * Select the appropriate target (2),
   * Go to the Signing & Capabilities section (3), and
   * Select your development team under Team (4).
     ![Xcode Signing](/_next/image?url=%2F_next%2Fstatic%2Fmedia%2Fscreenshot-xcode-signing.0c786436.png&w=3840&q=75&dpl=dpl_7YrfNpbg1U18B9yV3zCtUk5bPEKN)

Last updated on

[Troubleshooting

Previous Page](/sdks/android/troubleshooting)[Features

Next Page](/sdks/ios/features)

## Source
- DevRev developer docs: [Quickstart guide](https://developer.devrev.ai/sdks/ios/quickstart)
