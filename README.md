# ReadyRemit SDK - React Native

React Native wrapper for the ReadyRemit SDK, enabling international money transfers in React Native and Expo applications.

**Package:** `react-native-ready-remit-sdk`

## Requirements

| Platform | Minimum Requirement |
| :------- | :------------------ |
| React Native | 0.78+ (recommended) or 0.76+ (with upgrades) |
| iOS | 16.0 |
| Android | Min SDK 26, Compile/Target SDK 36 |
| Kotlin | 2.0.21+ |
| Android Gradle Plugin | 8.9.1+ |
| Gradle | 8.12+ |
| Xcode | 26.0+ |
| Swift | 5 |
| Java | 17 |
| Node.js | 18+ |

> **Note:** This SDK uses TurboModules and requires React Native's New Architecture to be enabled.

## React Native Version Compatibility

| React Native | iOS | Android | Notes |
| :----------- | :-: | :-----: | :---- |
| 0.78+ | ✅ | ✅ | **Recommended** — Native Kotlin 2.x support |
| 0.76 – 0.77 | ✅ | ✅ | Requires Kotlin/AGP/Gradle upgrade |
| 0.75 | ✅ | ❌ | iOS only — Kotlin 1.9.x incompatibility on Android |
| < 0.75 | ❌ | ❌ | Not supported |

## Expo Compatibility

- Supported with Expo Prebuild / Custom Dev Client / EAS Build.
- **Not supported** with Expo Go (Managed), because this SDK requires native modules.

## Developer Documentation

[React Native](https://developer.readyremit.com/docs/mobile-sdk-react-native)

## Installation

### Expo (Recommended)

1. Install the package:

   ```bash
   yarn add file:./react-native-ready-remit-sdk-10.0.0.tgz
   ```

2. Install the build properties plugin:

   ```bash
   yarn add expo-build-properties
   ```

3. Add plugins to `app.json`:

   ```json
   {
     "expo": {
       "plugins": [
         "react-native-ready-remit-sdk/plugin/with-readyremit-sdk",
         ["expo-build-properties", {
           "ios": { "deploymentTarget": "16.0" },
           "android": {
             "compileSdkVersion": 36,
             "targetSdkVersion": 36,
             "minSdkVersion": 26,
             "kotlinVersion": "2.0.21",
             "gradlePluginVersion": "8.9.1"
           }
         }]
       ]
     }
   }
   ```

4. Generate native projects and run:

   ```bash
   npx expo prebuild --clean
   npx expo run:ios
   npx expo run:android
   ```

### React Native (Bare)

1. Install the package:

   ```bash
   npm install ./react-native-ready-remit-sdk-10.0.0.tgz
   ```

2. Configure your `ios/Podfile` (see [Integration Guide](https://developer.readyremit.com/docs/mobile-sdk-react-native-integration) for full details):

   ```ruby
   require_relative '../node_modules/react-native-ready-remit-sdk/ios/embed_readyremit'

   use_frameworks! :linkage => :dynamic

   # Inside post_install:
   embed_readyremit_framework!(installer)
   ```

3. Install pods and run:

   ```bash
   cd ios && pod install && cd ..
   npx react-native run-ios
   npx react-native run-android
   ```

## Usage

```typescript
import {
  startSDK,
  ReadyRemitEnvironment,
  ReadyRemitSupportedAppearance,
  ReadyRemitLocalization,
} from 'react-native-ready-remit-sdk';

startSDK({
  configuration: {
    environment: ReadyRemitEnvironment.Sandbox,
    supportedAppearance: ReadyRemitSupportedAppearance.Device,
    localization: ReadyRemitLocalization.EN_US,
  },
  fetchAccessTokenDetails: async () => {
    // Return access token from your auth endpoint
  },
  verifyFundsAndCreateTransfer: async (request) => {
    // Submit transfer and return { transferId }
  },
  onLoad: async () => {},
  onClose: async () => {},
});
```

## License

Proprietary — Brightwell, LLC
