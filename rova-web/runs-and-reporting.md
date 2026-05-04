# Test Runs & Reporting

Every time a test or suite is executed, Rova generates a comprehensive, actionable report. These reports go beyond simple "Pass/Fail" to give you deep insight into *why* a test behaved the way it did.

## The Execution History

The **Runs** tab provides a chronological list of every execution in your project. You can filter by:
- **Status**: Passed, Failed, or Errored.
- **Timeframe**: A period of time within which the run happened.

## Anatomy of a Run Report

### 1. Synchronized Video Recording
A frame-perfect recording of the entire test session.

### 2. Step-by-Step Breakdown
Every action the agent took is logged in plain English.
- **Action**: "Clicked the 'Submit' button."
- **Reasoning**: "The goal is to submit the form; this button is the most relevant interactive element."
- **Status**: Whether the step was successful or failed.

### 3. Agent "Thoughts"
For every step, you can view the agent's internal reasoning. This is invaluable for debugging cases where the agent made an unexpected decision due to UI ambiguity.

### 4. Console & Network Logs
Rova captures the browser's console output and network requests during the run. This helps you identify if a failure was caused by a frontend error or a slow backend API.

## Reporting Features

### Success Rate Trends
View how your test stability changes over time. A dipping success rate can indicate "feature creep" or a regression in a shared component.

### Flakiness Detection
Rova automatically identifies tests that pass and fail intermittently. These are flagged as "Flaky," suggesting that the test description or the app's loading behavior needs adjustment.

## Best Practices

### 1. Review "Healed" Steps
Even if a test passes, if it required self-healing, review the step. It might be a sign that your app's UI has shifted and your test description should be updated for clarity.

### 2. Share Reports with Context
Use the **Share** button to generate a public or internal link to a specific run. This is the best way to report a bug to developers—they get the video, the logs, and the agent's reasoning in one link.

### 3. Use Assertions for Clear Failures
A test that fails on an assertion is much easier to debug than one that fails because the agent "timed out searching for an element." Ensure your tests have clear success criteria.

> [!TIP]
> **Pro Tip**: You can download the video recording and network logs (HAR files) for local analysis or to attach to Jira tickets.
