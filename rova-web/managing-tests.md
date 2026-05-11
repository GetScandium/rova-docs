# Managing Tests

Creating and maintaining tests in Rova is designed to be as simple as describing a manual test case.

## Creating a New Test

When you create a test, you are asked for two main pieces of information:

1. **Test Name**: A clear, descriptive title (e.g., `Successful Login with Valid Credentials`).
2. **The Goal**: A high-level description of what the test should accomplish.
3. **Initial URL**: Where the agent should start the execution.

### The "Goal" Approach

For simple tests, a **Goal** is often enough. _Example Goal_: "Log into the application, navigate to the settings page, and change the user's display name to 'Rova Tester'."

## Defining Steps (Optional but Recommended)

For more complex or critical paths, you can provide explicit **Steps**. This gives you more control over the agent's path.

| Step Type      | Description              | Example                                        |
| -------------- | ------------------------ | ---------------------------------------------- |
| **Action**     | A specific interaction.  | "Click on the 'Get Started' button."           |
| **Assertion**  | A check to verify state. | "Verify that the dashboard header is visible." |
| **Navigation** | Moving to a new URL.     | "Navigate to the /billing page."               |

## Best Practices for Test Writing

### 1. Be Descriptive, Not Technical

Instead of saying "Click the div with class .btn-submit", say "Click the 'Submit' button". Rova's AI understands intent better than selectors.

### 2. Use Assertions Liberally

Don't just perform actions. Use assertions to ensure the app is in the expected state.

> \[!TIP] **Recommendation**: End every test with an assertion. It's the only way to be 100% sure the goal was actually met.

### 3. Handle Dynamic Data

If your test involves creating data (like a new user), you can tell the agent to use dynamic names. _Example Step_: "Enter a random email address into the signup field."

## Test Settings

### Timeout

By default, tests have a maximum execution time. If you have a very long flow, you may need to break it into multiple goals.

### Sensitivity Settings

If a test interacts with sensitive data (e.g., PII), you can mark specific context data as **Sensitive**.

## Organizing Tests (Soon)

Use **Labels** to organize tests within a project. This makes it easier to find related tests when building new Suites.
