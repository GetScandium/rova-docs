---
description: >-
  Automatically manage bug cards in Jira Cloud or Jira Server/On-Premises when
  assertions fail.
---

# Jira

### Connection & Authentication <a href="#user-content-1-connection--authentication" id="user-content-1-connection--authentication"></a>

#### Jira Authentication Options <a href="#user-content-jira-authentication-options" id="user-content-jira-authentication-options"></a>

Rova supports two connection methods for Jira:

**Option A: Atlassian OAuth 2.0 (Recommended)**

1. Go to **Workspace Settings** > **Integrations**.
2. Click **Connect** next to the **Jira** integration card.
3. You will be redirected to Atlassian's secure authorization page.
4. Select the Jira Site/Workspace you want to link to and grant Rova permission.
5. Once redirected back to Rova, map your Jira projects.

**Option B: Basic Auth (API Tokens)**

For self-hosted Jira instances or private Cloud setups:

1. Provide your **Jira Site URL/Host** (e.g., `https://yourcompany.atlassian.net`).
2. Enter your account **Email Address**.
3. Generate an API Token from your [Atlassian Account Security Dashboard](https://id.atlassian.com/manage-profile/security/api-tokens) and paste it into the **API Token** field.
4. Enter your default **Project Key** (e.g., `PROJ`).

### Mapping Projects <a href="#user-content-2-mapping-projects" id="user-content-2-mapping-projects"></a>

After connecting to Jira:

1. Navigate to the **Jira Setup Page** in Rova.
2. You will be presented with a list of your Rova Projects.
3. Map each Rova Project to a corresponding **Jira Project Key**.
4. Enable the **Auto-Create Tickets** toggle if you want failed runs to automatically generate tickets.

### Interacting with Rova inside Tickets (Mentions) <a href="#user-content-3-interacting-with-rova-inside-tickets-mentions" id="user-content-3-interacting-with-rova-inside-tickets-mentions"></a>

You can trigger Rova tests directly from a ticket by leaving a comment mentioning the bot.

#### How to Mention <a href="#user-content-how-to-mention" id="user-content-how-to-mention"></a>

* **Jira**: Write `/rova` or tag `@Rova` in a comment.

#### Basic Examples <a href="#user-content-basic-examples" id="user-content-basic-examples"></a>

* `@Rova test the signup form`
* `@Rova verify that checkout completes successfully`

### Mention Configuration Flags <a href="#user-content-4-mention-configuration-flags" id="user-content-4-mention-configuration-flags"></a>

You can specify execution flags in your comment to customize the test run.

| Flag                      | Parameter                       | Description                                          | Example                                          |
| ------------------------- | ------------------------------- | ---------------------------------------------------- | ------------------------------------------------ |
| `--env` / `--environment` | `"<Env Name>"`                  | Run the test against a specific environment context. | `@Rova --env="Staging" test logout`              |
| `--browser`               | `chromium`, `firefox`, `webkit` | Target browser selection.                            | `@Rova --browser=firefox verify header`          |
| `--viewport`              | `WIDTHxHEIGHT`                  | Set custom viewport sizes.                           | `@Rova --viewport=375x812 test mobile menu`      |
| `--url`                   | `<URL>` / `URL`                 | Override the target application URL.                 | `@Rova --url=https://dev.example.com test login` |
| `--turbo`                 | None                            | Run tests in high-speed Execution mode.              | `@Rova --turbo test page loading`                |

#### Complex Examples <a href="#user-content-complex-examples" id="user-content-complex-examples"></a>

```
@Rova --env="Dev-Staging" --browser=webkit --viewport=1280x720 --url=https://dev.mysite.com check checkout flow
```

_This command runs a checkout flow test in Safari (Webkit) against the custom Dev-Staging environment override at `https://dev.mysite.com`._

### Best Practices & Recommendations <a href="#user-content-5-best-practices--recommendations" id="user-content-5-best-practices--recommendations"></a>

* **Scope Instructions**: Keep your comment goals concise. Describe the user path (e.g. "click login, fill form, verify success header").
* **Use De-duplication**: Keep `autoCreateTickets` enabled. Rova uses failure hashing to update existing issue tickets rather than cluttering your workspace with duplicates.
* **Dynamic Project Mapping**: Make sure each developer team's repository is mapped to their respective Jira Projects so Rova tickets arrive in the right backlog.

### Limitations <a href="#user-content-6-limitations" id="user-content-6-limitations"></a>

* **Comment Formatting**: Ensure flags like `--url` are not double-wrapped in markdown formatting. Provide clean plaintext urls (or standard Slack/Linear angle brackets `<url>`).
* **Authorization Scopes**: If your Jira or Linear site admins revoke app scopes, ticket synchronization will stop. Make sure Rova has permission to read comments and create/update issues.

### Troubleshooting <a href="#user-content-7-troubleshooting" id="user-content-7-troubleshooting"></a>

#### Issue: Mentioning Rova in comments does nothing <a href="#user-content-issue-mentioning-rova-in-comments-does-nothing" id="user-content-issue-mentioning-rova-in-comments-does-nothing"></a>

* **Check Webhooks**: Ensure the webhook connection status is "Active" in your integrations page.
* **Project Mapping**: Verify the ticket's Project Key or Team is mapped to a Rova project. Rova ignores comments on unmapped ticket boards.
* **API Token Revocation**: If using Basic Auth/PAT, verify that the token hasn't expired or been deleted.
