# Troubleshooting

Having trouble with Rova? Most issues can be resolved by following these steps.

## Common CLI Issues

### 1. "401 Unauthorized" or "Authentication Failed"
- **Cause**: Your local session has expired or your API key is invalid.
- **Solution**: Run `rova auth` again to refresh your session. If using an API key in CI, verify that the `ROVA_API_KEY` is correctly set in your environment variables.

### 2. "Device not found" (Mobile)
- **Cause**: The CLI cannot communicate with your local emulator or simulator.
- **Solution**: 
  - **Android**: Run `adb devices`. If no device is listed, restart your AVD.
  - **iOS**: Run `xcrun simctl list devices | grep Booted` to ensure a simulator is active.

### 3. "Timeout searching for element"
- **Cause**: The agent could not find the target element within the allotted time.
- **Solution**: 
  - Check the video recording in the dashboard to see if the page loaded correctly.
  - Update your test description or **Project Context** to provide more visual details about the element.
  - Increase the timeout setting in your test configuration.

---

## Common Web Dashboard Issues

### 1. Video Recording is Black or Empty
- **Cause**: Usually caused by a failure in the browser's graphics rendering or a very early crash.
- **Solution**: Check the **Console Logs** for any fatal errors. If the issue persists, contact support.

### 2. Scheduled Run Didn't Trigger
- **Cause**: Often due to a paused schedule or insufficient credits.
- **Solution**: 
  - Ensure the schedule is toggled to **Active**.
  - Check your **Billing** tab to ensure you have a positive credit balance.

## Contacting Support

If you've tried the steps above and still need help:
- **In-App Chat**: Click the blue chat icon in the bottom-right of the dashboard.
- **Email**: [support@rova.qa](mailto:support@rova.qa)
- **GitHub**: Report bugs for the CLI or GitHub Action in our official repositories.

> [!TIP]
> **Pro Tip**: When contacting support, always provide the **Run ID** or a link to the failed test result. This helps us diagnose the issue much faster.
