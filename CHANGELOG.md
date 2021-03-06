# Changelog

## 0.6.0

- Updated for compatibility with React Native 0.60.

  - Added a podspec for the new, built-in CocoaPods support. This means you no longer need to manually include Estimote Proximity SDK dependency in your Podfile. Instead, the new auto-linking will automatically pull the plugin's podspec, and the plugin's podspec will automatically pull Estimote Proximity SDK.

  - Migrated the native Android code to AndroidX.

    - This is a **breaking change**, and means that **0.6.0 can no longer be used with React Native < 0.60**.
    - If you happen to know a good way to support both AndroidX and the previous support libraries, please open an issue and let us know.

- Updated the native Android Proximity SDK to 1.0.3, and the Android com.estimote:scanning-plugin to 0.25.2.

  - This fixes a potential crash if there's an Estimote LTE Beacon in range.

## 0.5.0

- Fixed "undefined is not an object" error, as reported in https://github.com/Estimote/react-native-proximity/issues/21.

  - This error happened when the Observer hasn't been stopped properly before calling another `startObservingZones`.
  - Instead, the plugin will now automatically stop the previous observation, and log a warning about this.
  - Most commonly, this is tied to improper lifecycle management of the Observer. There's a new section in the README which explains this topic in more detail, and lays out some recommendations and best practices: https://github.com/Estimote/react-native-proximity#already-observing. The new warning also points to this section.

- Updated the native Android module's build.gradle, getting rid of the warnings.

## 0.4.0

- Updated the native iOS and Android Estimote Proximity SDKs to 1.0.0.

- Updated the plugin to compile against Android 26 SDK, and target the Android API level 26. This is to [match the latest React Native version, 0.56][0.4.0-1].

  - The bundled "example" app was also updated to React Native 0.56.

  - Since the Android plugin now targets API level 26, the background-scanning notification now requires to be assigned to a notification channel. You specify the channel ID and name in the `config` object, next to the notification's title, text, and icon, for example:

    ```
    const config = {
      notification: {
        title: "Exploration mode is on",
        text: "We'll notify you when you're next to something interesting.",
        icon: 'ic_exploration_mode',

        channel: {
          id: "exploration-mode",
          name: "Exploration Mode"
        }
      }
    };
    RNEP.proximityObserver.initialize(credentials, config);
    ```

    You can learn more about notifications channels in [Notifications Overview: Notification channels][0.4.0-2].

[0.4.0-1]: https://github.com/react-native-community/react-native-releases/blob/master/CHANGELOG.md#android-projects-are-now-compiled-using-the-android-26-sdk
[0.4.0-2]: https://developer.android.com/guide/topics/ui/notifiers/notifications#ManageChannels
