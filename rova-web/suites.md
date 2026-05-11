# Test Suites

A **Test Suite** is a logical collection of tests designed to be executed together. Suites are the primary way to organize your automation for regression, smoke testing, and feature validation.

## Creating a Suite

1. Navigate to the **Suites** tab in your project.
2. Click **Create New Suite**.
3. Give it a descriptive name (e.g., `Critical Path Regression`).
4. Select the tests you want to include. You can drag and drop to reorder them.

> You can create a test suite by either uploading documents such as PRDs, BRDs, and Test Case Documentations, or from context messages, or by selecting existing test goals.

## Continuity Mode

One of Rova's most powerful features for suites is **Continuity Mode**. When enabled, the AI agent maintains the browser session state (cookies, local storage, etc.) across all tests in the suite.

### Why use Continuity Mode?

* **Workflow Efficiency**: Instead of logging in for every single test, Test A can perform the login, and Test B starts already logged in.
* **State-Dependent Testing**: Perfect for flows where you create an object in one test and need to edit or delete it in the next.

> \[!IMPORTANT] When using Continuity Mode, the order of tests matters. Ensure your tests follow a logical sequence if they depend on the state created by previous tests.

## Suite Configuration

### Trigger Settings

* **Manual**: Run the suite with a single click from the dashboard.
* **Scheduled**: Set up recurring runs (e.g., every night at 2 AM).
* **Webhook/API**: Trigger the suite from your CI/CD pipeline using the Rova CLI.

### Environment & Parallelism

You can configure a suite to run across multiple browsers (Chromium, Firefox, WebKit) and set whether to run sequentially or with parallelism to speed up execution.

## Best Practices

### 1. Group by Priority

Create a "Smoke Suite" for P0 tests that run on every PR, and a "Full Regression" suite for P1/P2 tests that run nightly.

### 2. Use Descriptive Names

Instead of `Suite 1`, use names like `Onboarding Flow`, `Payment Gateway Tests`, or `Admin Settings Validation`.

### 3. Review Suite Analytics

Rova provides a dashboard for each suite showing its stability over time. Look for tests with high "flakiness" scores and refactor their descriptions or check for timing issues in your app.

> \[!TIP] **Recommendation**: Always enable **Notifications** for your regression suites so your team is immediately alerted if a stable feature breaks.
