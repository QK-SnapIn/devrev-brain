---
title: Quickstart guide (React Native)
type: developer-doc
status: stable
source: developer.devrev.ai
category: sdks
source_url: https://developer.devrev.ai/sdks/react-native/quickstart
last_updated: 2026-05-11
summary: "DevRev SDK for React Native and Expo"
---

# Quickstart guide (React Native)

DevRev SDK for React Native and Expo

# Quickstart guide (React Native)

This guide helps you integrate the DevRev SDK into your React Native app.

## [Requirements](#requirements)

* React Native 0.79.0 or later.
* For Expo apps, Expo 50.0.0 or later.
* Android: minimum API level 24.
* iOS: minimum deployment target 15.1.
* Recommended: An SSH key configured locally and registered with [GitHub](https://docs.github.com/en/github/authenticating-to-github/connecting-to-github-with-ssh).

## [Installation](#installation)

To install the DevRev SDK, run the following command:

```
npm install @devrev/sdk-react-native
```

## [Set up the DevRev SDK](#set-up-the-devrev-sdk)

1. Open the DevRev web app at <https://app.devrev.ai> and go to the **Settings** page.
2. Under **Plug settings** copy the value under **Your unique App ID**.
3. Configure the DevRev SDK in your app using the obtained credentials.

The DevRev SDK must be configured before you can use any of its features.

The SDK becomes ready for use once the following configuration method is executed.

```
DevRev.configure(appID: string)
```

## [Sample app](#sample-app)

A sample app with use cases for the DevRev React Native plugin has been provided as a part of our [public repository](https://github.com/devrev/devrev-sdk-react-native). To set up and run the sample app:

1. Go to the sample directory:

   ```
   cd sample
   ```
2. Install dependencies:

   ```
   yarn install
   ```
3. For iOS, run:

   ```
   cd ios
   pod install
   ```
4. Run the app on Android or iOS using:

   ```
   npx react-native start
   ```

   Or open `android` directory in Android Studio or `ios/DevRevSDKSample.xcworkspace` in Xcode and run the app from there.

Last updated on

[Troubleshooting

Previous Page](/sdks/ios/troubleshooting)[Quickstart guide (Expo)

Next Page](/sdks/react-native/quickstart-expo)

## Source
- DevRev developer docs: [Quickstart guide (React Native)](https://developer.devrev.ai/sdks/react-native/quickstart)
