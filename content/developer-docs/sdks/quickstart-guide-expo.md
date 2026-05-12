---
title: Quickstart guide (Expo)
type: developer-doc
status: stable
source: developer.devrev.ai
category: sdks
source_url: https://developer.devrev.ai/sdks/react-native/quickstart-expo
last_updated: 2026-05-11
summary: "DevRev SDK for React Native and Expo"
---

# Quickstart guide (Expo)

DevRev SDK for React Native and Expo

# Quickstart guide (Expo)

DevRev SDK, used for integrating DevRev services into your Expo app.

## [Requirements](#requirements)

* React Native 0.79.0 or later.
* For Expo apps, Expo 50.0.0 or later.
* Android: minimum API level 24.
* iOS: minimum deployment target 15.1.
* Recommended: A locally configured SSH key registered on [Github](https://docs.github.com/en/github/authenticating-to-github/connecting-to-github-with-ssh).

## [Installation](#installation)

1. To install the DevRev SDK, run the following command:

   ```
   npx expo install @devrev/sdk-react-native-expo-plugin
   ```
2. Configure the Expo config plugin in your `app.json` or `app.config.js`:

   ```
   {
     "expo": {
       "plugins": [
         "@devrev/sdk-react-native-expo-plugin"
       ]
     }
   }
   ```
3. Rebuild your app:

   ```
   npx expo prebuild --clean
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

A sample app with use cases for the DevRev Expo plugin has been provided as a part of our [public repository](https://github.com/devrev/devrev-sdk-expo). To set up and run the sample app:

1. Go to the sample directory:

   ```
   cd sample
   ```
2. Install dependencies:

   ```
   yarn install
   ```
3. Run clean and prebuild:

   ```
   npx expo prebuild --clean
   ```
4. Run the app On Android:

   ```
   npx expo run:android
   ```

   OR open `android` in Android Studio and run the app.
5. Run the app On iOS:

   ```
   npx expo run:ios
   ```

   OR open `ios/DevRevSDKSample.xcworkspace` in Xcode and run the app.

Last updated on

## Source
- DevRev developer docs: [Quickstart guide (Expo)](https://developer.devrev.ai/sdks/react-native/quickstart-expo)
