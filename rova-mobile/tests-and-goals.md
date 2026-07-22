# Managing Tests & Goals

Creating and maintaining tests in Rova Mobile is designed to be as simple as describing a manual test case on a physical device.

### Creating a New Test

When you create a test, you are asked for three main pieces of information:

1. Test Name: A clear, descriptive title (e.g., `Successful Login with Valid Credentials`).
2. The Goal: A high-level description of what the test should accomplish.
3. Start State: Tell the agent where to begin—whether that's launching the app from the home screen or opening a specific Deep Link.

### The "Goal" Approach

For simple tests, a Goal is often enough. _Example Goal_: "Open the app, log in, navigate to the settings screen, and change the user's display name to 'Rova Tester'."

### Defining Steps (Optional but Recommended)

For more complex flows or critical paths, you can provide explicit Steps. This gives you more precise control over how the agent navigates your app.

| **Step Type** | **Description**          | **Example**                                    |
| ------------- | ------------------------ | ---------------------------------------------- |
| Action        | A specific interaction.  | "Tap on the 'Get Started' button."             |
| Assertion     | A check to verify state. | "Verify that the dashboard header is visible." |
| Navigation    | Moving to a new screen.  | "Open the deep link to the /billing screen."   |

### Best Practices for Test Writing

1.  #### Describe What to Do, Not How to Code It

    Instead of saying "Tap the element with accessibility ID `btn_submit`", just say "Tap the 'Submit' button". Rova's AI understands user intent and visual elements much better than raw technical selectors.
2.  #### Use Assertions Liberally

    Don't just tap through your app blindly. Use assertions to make sure the app is actually in the expected state after an action.

    > Tip: End every single test with an assertion. It's the most reliable way to prove your test goal was actually achieved.
3.  #### Handle Dynamic Data

    If your test involves creating new data (like registering a new user), you can tell the agent to use dynamic names. _Example Step_: "Enter a random email address into the signup field."

### Test Settings

#### Timeout

By default, mobile tests have a maximum execution time. If you have a highly complex or very long user journey, we recommend breaking it down into smaller, individual tests.

#### Sensitivity Settings

If your app handles sensitive information (like passwords, credit cards, or PII), you can mark specific inputs or screen areas as Sensitive to mask them during test execution.
