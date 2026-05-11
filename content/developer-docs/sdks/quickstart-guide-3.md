---
title: Quickstart guide
type: developer-doc
status: stable
source: developer.devrev.ai
category: sdks
source_url: https://developer.devrev.ai/sdks/flutter/quickstart
last_updated: 2026-05-11
summary: "To install the DevRev SDK, run the following command:"
---

# Quickstart guide

DevRev SDK for Flutter

# Quickstart guide

## [Requirements](#requirements)

* Flutter 3.3.0 or later.
* Dart SDK 3.7.0 or later.
* Android: minimum API level 24.
* iOS: minimum deployment target 15.0.
* Recommended: An SSH key configured locally and registered with [GitHub](https://docs.github.com/en/github/authenticating-to-github/connecting-to-github-with-ssh).

## [Installation](#installation)

To install the DevRev SDK, run the following command:

```
flutter pub add devrev_sdk_flutter
```

It automatically fetches the latest version of our package and adds it to your project's pubspec.yaml file:

```
dependencies:
    devrev_sdk_flutter: <VERSION>
```

Alternatively, you can add the dependency manually by adding the package to your `pubspec.yaml` file under the `dependencies` section and run `flutter pub get` to install the package.

To get the latest version of the SDK, you can check the [pub.dev page](https://pub.dev/packages/devrev_sdk_flutter).

## [Set up the DevRev SDK](#set-up-the-devrev-sdk)

1. Open the DevRev web app at <https://app.devrev.ai> and go to the **Settings** page.
2. Under **Plug settings** copy the value under **Your unique App ID**.
3. Configure the DevRev SDK in your app using the obtained credentials.

The DevRev SDK must be configured before you can use any of its features.

The SDK becomes ready for use once the following configuration method is executed.

```
DevRev.configure(appID);
```

For example:

```
DevRev.configure("abcdefg12345");
```

## [Sample app](#sample-app)

A sample app with use cases for the DevRev SDK for Flutter has been provided as a part of our [public repository](https://github.com/devrev/devrev-sdk-flutter). To set up and run the sample app:

1. Go to the `sample` directory:

   ```
   cd sample
   flutter clean
   rm -rf ios android web linux macos windows
   flutter create --platforms=android,ios .
   ```
2. Install dependencies:

   ```
   flutter pub get
   ```
3. iOS app:
   Open the `ios/Runner.xcworkspace` in Xcode for running the iOS app or run the following command.

   ```
   flutter run -d ios
   ```

   Additional Steps for iOS before running the app:

   1. Change the minimum iOS deployment target version to `15.0`.
   2. Go to the `ios` directory and perform `pod install`.
   3. Open `ios/Runner.xcodeproj` in Xcode and select `Package dependencies -> FlutterGeneratedPluginSwiftPackage -> Package.swift` set iOS version from `12` to `15`.

      ```
      platforms: [
         .iOS("15.0")
      ]
      ```
   4. Perform `File -> Packages -> Resolve package versions`.
   5. Build and run the app.
4. Android app:
   Open the `android` directory in Android Studio or run the following command.

   ```
   flutter run -d android
   ```

Last updated on

[Troubleshooting

Previous Page](/sdks/cordova/troubleshooting)[Features

Next Page](/sdks/flutter/features)

## Source
- DevRev developer docs: [Quickstart guide](https://developer.devrev.ai/sdks/flutter/quickstart)
