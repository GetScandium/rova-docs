# Rova Mobile Core Concepts

Rova Mobile brings the power of AI automation to iOS and Android applications. While similar to Rova Web, mobile automation has unique concepts due to the nature of mobile platforms.

## 1. Mobile Goals
In Rova Mobile, we often talk about **Goals** instead of just tests. A goal is a high-level outcome you want to achieve (e.g., "Complete the onboarding flow"). Rova's AI manages the complexity of gestures, keyboard interactions, and screen transitions to reach that goal.

## 2. Execution Plans
An **Execution Plan** is a set of instructions that defines:
- **Which App**: The specific APK or IPA version to test.
- **Which Device**: The emulator/simulator configuration (e.g., Pixel 7, iPhone 15).
- **Which Goals**: The list of mobile goals to execute.
- **Concurrency**: How many parallel sessions to run.

## 3. App Context
Similar to Project Context in Web, **App Context** provides the AI with essential knowledge about your mobile app:
- **Navigation Patterns**: How to open the side menu or back-navigate.
- **Deep Links**: Useful shortcuts to specific screens.
- **Known Issues**: Elements the AI should ignore or handle specially.

> [!TIP]
> **Recommendation**: Always provide the main deep links for your app in the App Context. This can significantly speed up test execution by bypassing repetitive navigation steps.

## 4. App Versions (APK/IPA)
Rova Mobile manages your app binaries. You can upload multiple versions of your app and run tests against them selectively.

## 5. Workspaces
Mobile workspaces are separate from Web workspaces by default, allowing you to manage mobile-specific team members, credits, and API keys. However, you can link them for unified billing if needed.

## 6. The AI Mobile Agent
The Mobile Agent "sees" the screen just like a user. It understands:
- **Gestures**: Swiping, long-pressing, and multi-touch.
- **System Dialogs**: Handling permission requests or system alerts automatically.
- **Connectivity**: Simulating different network conditions (e.g., 3G, Offline).
