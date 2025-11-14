# Cloud Messaging Flutter App

This Flutter project demonstrates integration with **Firebase Cloud Messaging (FCM)**. The app can receive push notifications and display them on Android devices.

---

## Table of Contents

* [Prerequisites](#prerequisites)
* [Firebase Setup](#firebase-setup)
* [Flutter Project Setup](#flutter-project-setup)
* [Building the APK](#building-the-apk)
* [Running on Device](#running-on-device)
* [FCM Token](#fcm-token)
* [Notes](#notes)
* [References](#references)

---

## Prerequisites

* Flutter SDK installed: [Flutter Installation](https://flutter.dev/docs/get-started/install)
* Android Studio or VS Code with Flutter plugin
* Android device or emulator (Android 6.0+ recommended)
* Firebase account and project setup

---

## Firebase Setup

1. Go to [Firebase Console](https://console.firebase.google.com/)
2. Create a new project (e.g., `Cloud Messaging`)
3. Add an Android app to the project:

   * Package name: `com.example.cloud_messaging` (must match `applicationId` in `android/app/build.gradle.kts`)
   * Download `google-services.json` and place it in `android/app/`
4. Enable **Firebase Cloud Messaging** in the Firebase Console
5. Make note of your **FCM Token** for testing

---

## Flutter Project Setup

1. Open terminal and navigate to your project:

```bash
cd <project_root>
```

2. Get dependencies:

```bash
flutter pub get
```

3. Clean previous builds (optional but recommended):

```bash
flutter clean
```

4. Ensure your Android SDK, NDK, and compile versions are correct in `android/app/build.gradle.kts`:

```kotlin
android {
    compileSdk = 34
    ndkVersion = "27.0.12077973"

    defaultConfig {
        applicationId = "com.example.cloud_messaging"
        minSdk = 21
        targetSdk = 34
        versionCode = 1
        versionName = "1.0"
    }
}
```

5. Apply Google services plugin at the bottom of `build.gradle.kts`:

```kotlin
apply(plugin = "com.google.gms.google-services")
```

6. Add Firebase dependencies in the `dependencies` block:

```kotlin
dependencies {
    implementation(platform("com.google.firebase:firebase-bom:33.1.2"))
    implementation("com.google.firebase:firebase-messaging")
    implementation("com.google.firebase:firebase-analytics")
}
```

---

## Building the APK

**Debug APK (for testing):**

```bash
flutter build apk --debug
```

**Release APK (for submission/publishing):**

```bash
flutter build apk --release
```

APK location:

```
<project_root>/build/app/outputs/flutter-apk/
```

* `app-debug.apk` → Debug version
* `app-release.apk` → Release version

---

## Running on Device

1. Connect your Android device with USB debugging enabled.
2. Run:

```bash
flutter run
```

* To specify a device:

```bash
flutter run -d <device_id>
```

---

## FCM Token

* You can get the device token in your Flutter app:

```dart
FirebaseMessaging.instance.getToken().then((token) {
  print("FCM Token: $token");
});
```

* Use this token to send test messages from the Firebase Console.

---

## Notes

* Ensure your `applicationId` in `build.gradle.kts` matches the package name in Firebase.
* Use `isMinifyEnabled = false` and `isShrinkResources = false` in `buildTypes` during debugging to avoid resource/build issues.
* Debug APK can be used for submission if release APK is failing.

---

## References

* [FlutterFire Docs](https://firebase.flutter.dev/docs/overview)
* [Firebase Cloud Messaging](https://firebase.google.com/docs/cloud-messaging)
* [Flutter Build APK Guide](https://docs.flutter.dev/deployment/android)
