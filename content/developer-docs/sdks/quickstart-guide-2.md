---
title: Quickstart guide
type: developer-doc
status: stable
source: developer.devrev.ai
category: sdks
source_url: https://developer.devrev.ai/sdks/cordova/quickstart
last_updated: 2026-05-11
summary: "This guide helps you integrate the DevRev SDK into your Cordova app."
---

# Quickstart guide

DevRev SDK for Cordova

# Quickstart guide

This guide helps you integrate the DevRev SDK into your Cordova app.

## [Requirements](#requirements)

* Cordova CLI 10.0.0 or higher.
* Minimum deployment target Android SDK 24 or iOS 15.

## [Installation](#installation)

To install the DevRev SDK, run the following command:

```
npm install @devrev/sdk-cordova
```

## [Set up the DevRev SDK](#set-up-the-devrev-sdk)

1. Open the DevRev web app at <https://app.devrev.ai> and go to the **Settings** page.
2. Under **Plug settings**, copy the value under **Your unique App ID**.
3. After obtaining the credentials, configure the DevRev SDK in your app.

The DevRev SDK must be configured before you can use any of its features.

The SDK will be ready for use once you execute the following configuration method:

```
DevRev.configure(appID, successCallback, errorCallback)
```

## [Sample app](#sample-app)

A sample app with use cases for the DevRev Cordova plugin is provided as part of our [public repository](https://github.com/devrev/devrev-sdk-cordova). To set up and run the sample app:

```
cd sample
npm install
cordova platform add android
cordova platform add ios
```

```
cordova run android
```

OR open `platforms/android` in Android Studio and run the app.

1. Open `platforms/ios/Podfile` and ensure it contains:

```
platform :ios, '15.0'
```

2. Install dependencies:

```
cd platforms/ios
pod install
```

3. Run the app:

```
cordova run ios
```

OR open `DevRevSDKSample.xcworkspace` in Xcode and run the app.

Last updated on

[Troubleshooting

Previous Page](/sdks/react-native/troubleshooting)[Features

Next Page](/sdks/cordova/features)

## Source
- DevRev developer docs: [Quickstart guide](https://developer.devrev.ai/sdks/cordova/quickstart)
