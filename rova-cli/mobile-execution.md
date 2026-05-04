# Local Mobile Execution

Running mobile tests locally allows you to debug your iOS and Android apps without uploading them to the Rova cloud.

## Prerequisites

Before running mobile tests locally, ensure your environment is set up:

### Android
1. Install **Android Studio** and the **Android SDK**.
2. Ensure `adb` is in your PATH.
3. Start an Android Virtual Device (AVD) from the Device Manager.

### iOS (macOS only)
1. Install **Xcode**.
2. Install the **Command Line Tools**: `xcode-select --install`.
3. Start an iOS Simulator: `open -a Simulator`.

## Commands

### Running a specific goal
```bash
rova run mobile --app-id ./my-app.apk --goal "Complete Checkout"
```

### Targeting a specific platform
By default, Rova CLI targets Android. Use the `--platform` flag to specify iOS.

```bash
# Run a mobile test for iOS
rova run mobile --platform ios --app-id ./my-app.ipa --goal "Login"
```

## Best Practices

### 3. Debugging
If a test fails, use the `--step-by-step` flag to pause after every action and inspect the app state.

```bash
rova run mobile --step-by-step --app-id ...
```

## Troubleshooting
- **Device not found**: Run `adb devices` (Android) or `xcrun simctl list devices` (iOS) to ensure your emulator/simulator is recognized by the OS.
- **App installation failure**: Ensure your binary is compiled for the correct architecture (usually `x86_64` for simulators).
