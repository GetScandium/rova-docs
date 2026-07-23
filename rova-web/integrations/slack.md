---
description: >-
  Get notified of test results, suite completions, and anomalies directly in
  your team's Slack channels.
---

# Slack

#### Setup Instructions <a href="#user-content-setup-instructions" id="user-content-setup-instructions"></a>

1. Navigate to **Workspace Settings** > **Integrations**.
2. Click **Configure** on the **Slack** card.
3. Enter your **Incoming Webhook URL** (create one inside your [Slack API dashboard](https://api.slack.com/messaging/webhooks)).
4. Specify an optional **Channel Name** (e.g. `#alerts`) if you want to override the default webhook channel.
5. Save the integration and click **Test** to send a validation notification to the channel.

#### What is Sent <a href="#user-content-what-is-sent" id="user-content-what-is-sent"></a>

Rova maps test events to Slack **Block Kit** blocks:

* **Success Notifications**: Displays a green indicator (🟢), total passed tests, execution duration, and stats.
* **Failure Notifications**: Displays a red indicator (🔴), stats, and a raw code block containing the specific exception or assertion error message.
