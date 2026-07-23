---
description: >-
  Link Rova to your Linear workspace to automatically create bugs/tickets when
  tests fail, or trigger test runs directly using Linear comments.
---

# Linear

### Connect to Linear <a href="#user-content-linear-authentication-options" id="user-content-linear-authentication-options"></a>

**Connect using Linear OAuth 2.0**

1. Go to **Workspace Settings** > **Integrations**.
2. Select **Connect** next to **Linear**.
3. Authorize the Rova application inside your Linear organization.
4. Rova will automatically link and pull details using the returned OAuth token.

### Mapping Projects <a href="#user-content-2-mapping-projects" id="user-content-2-mapping-projects"></a>

After connecting to Linear:

1. Navigate to the **Linear Setup Page** in Rova.
2. You will be presented with a list of your Linear Team Projects.
3. Map each **Linear** Project to a corresponding **Rova Project**.
4. Enable the **Auto-Create Tickets** toggle if you want failed runs to automatically generate tickets.

### Interacting with Rova inside Tickets (Mentions) <a href="#user-content-3-interacting-with-rova-inside-tickets-mentions" id="user-content-3-interacting-with-rova-inside-tickets-mentions"></a>

You can trigger Rova tests directly from a ticket by leaving a comment mentioning the bot.

#### How to Mention <a href="#user-content-how-to-mention" id="user-content-how-to-mention"></a>

* **Linear**: Tag `@Rova` in a comment.

#### Basic Examples <a href="#user-content-basic-examples" id="user-content-basic-examples"></a>

* `@Rova test the signup form`
* `@Rova verify that checkout completes successfully`

***

### 4. Mention Configuration Flags <a href="#user-content-4-mention-configuration-flags" id="user-content-4-mention-configuration-flags"></a>

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
* **Dynamic Project Mapping**: Make sure each developer team's repository is mapped to their respective Linear Teams / Jira Projects so Rova tickets arrive in the right backlog.

### Limitations <a href="#user-content-6-limitations" id="user-content-6-limitations"></a>

* **Comment Formatting**: Ensure flags like `--url` are not double-wrapped in markdown formatting. Provide clean plaintext urls (or standard Slack/Linear angle brackets `<url>`).
* **Authorization Scopes**: If your Linear site admins revoke app scopes, ticket synchronization will stop. Make sure Rova has permission to read comments and create/update issues.

### Troubleshooting <a href="#user-content-7-troubleshooting" id="user-content-7-troubleshooting"></a>

#### Issue: Mentioning Rova in comments does nothing <a href="#user-content-issue-mentioning-rova-in-comments-does-nothing" id="user-content-issue-mentioning-rova-in-comments-does-nothing"></a>

* **Check Webhooks**: Ensure the webhook connection status is "Active" in your integrations page.
* **Project Mapping**: Verify the ticket's Project Key or Team is mapped to a Rova project. Rova ignores comments on unmapped ticket boards.
* **API Token Revocation**: If using Basic Auth/PAT, verify that the token hasn't expired or been deleted.
