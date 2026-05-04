# Integrations

Connect Rova with your existing workflow to create a seamless automation pipeline.

## Notification Platforms

### Slack
Get real-time updates on test and suite results directly in your team's Slack channels.
- **Failures Only**: Configure notifications to only alert you when something breaks.
- **Summaries**: Get a daily or weekly roll-up of your project's stability.

### Email
Configure individual or team-based email alerts for scheduled suite runs.

## CI/CD Integrations

### GitHub Actions
The easiest way to integrate Rova into your GitHub workflow is using our [official action](../integrations/github-actions.md).

### Rova CLI
For all other CI/CD platforms (GitLab, Jenkins, CircleCI, etc.), use the **Rova CLI**.
- **Run Tests**: Trigger cloud or local executions from your build scripts.
- **Sync Results**: Automatically stream logs and artifacts back to the Rova dashboard.

<!-- ## Webhooks
For custom integrations, use Rova Webhooks to send execution events to your own internal tools or services.
- `suite.started`
- `test.passed`
- `test.failed`
- `run.completed` -->

## Issue Tracking

### Jira & Trello
While we don't have a direct "one-click" button yet, our **Shareable Run Links** are designed to be pasted into Jira tickets. They provide developers with:
- Full video recording.
- Console and Network logs.
- Agent reasoning for failures.

<!-- ## API Access
For advanced users, the **Rova Public API** allows you to programmatically manage projects, tests, and suites.
- Generate API Keys in **Settings > API Keys**.
- Use our OpenAPI specification to generate client libraries. -->

> [!TIP]
> **Best Practice**: Use a dedicated Slack channel (e.g., `#rova-alerts`) for your automation notifications to avoid cluttering your main dev channels.
