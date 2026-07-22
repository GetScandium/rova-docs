# Integrations

Connect Rova Mobile with your existing workflow to create a seamless automation pipeline for your mobile app testing.

### Notification Platforms

#### Slack

Get real-time updates on mobile test and suite results directly in your team's Slack channels.

* **Failures Only**: Configure notifications to alert you only when a test run fails on a device.
* **Summaries**: Get a daily or weekly roll-up of your mobile project's overall stability.

### CI/CD Integrations (Soon)

#### GitHub Actions (Soon)

The easiest way to integrate Rova Mobile into your GitHub workflow is using our Rova CLI.

#### Rova CLI

For all other mobile CI/CD platforms (such as Bitrise, Codemagic, GitLab, or Jenkins), use the Rova CLI.

* **Run Tests**: Trigger cloud or local mobile executions directly from your build scripts.
* **Sync Results**: Automatically stream device logs, performance metrics, and artifacts back to the Rova dashboard.

### Issue Tracking

#### Linear

Sync your mobile bug tracking with your automated testing workflow.

* **Seamless Ticket Linking**: Connect Linear to let your team trigger tests by mentioning `@Rova` on any ticket.
* **Rich Context**: When a test fails, easily link or create a Linear issue packed with full video recordings of the device screen, device logs, and the AI's step-by-step reasoning for the failure.

{% hint style="info" %}
Best Practice: Use a dedicated Slack channel (e.g., `#rova-mobile-alerts`) for your automation notifications to keep your main development channels clean and focused.
{% endhint %}
