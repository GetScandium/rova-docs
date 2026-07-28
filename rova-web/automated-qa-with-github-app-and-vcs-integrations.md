---
description: >-
  Learn how to connect your GitHub, GitLab, or Bitbucket repositories to Rova
  for automated, zero-code-change E2E test execution triggered by Pull Requests,
  deployments, and PR comments.
---

# Automated QA with GitHub App & VCS Integrations

Rova integrates natively with your version control system to provide continuous, AI-driven quality assurance. Once connected, Rova automatically ingests code changes, executes browser E2E test suites against live preview or staging environments, and reports test results directly onto your Pull Requests.

***

### Key Features

* ⚡ **Zero-Code Setup**: Connect your repository in seconds using the Rova GitHub App—no custom script authoring or CI pipeline edits required.
* 🎯 **Smart Workflow Modes**: Tailor test execution to match your team's deployment strategy (Post-Merge Staging, Ephemeral Preview Deployments, PR Open, or Manual/PR Comment triggers).
* 💬 **Interactive PR Commands**: Comment `@rova test` or `@rova test <preview-url>` on any Pull Request to run tests on demand.
* 📊 **Rich Markdown PR Reports**: Get instant feedback inside Pull Request threads with status badges, test duration, pass/fail counts, and direct links to execution recordings.
* 🚦 **Native Check Runs**: Block PR merges automatically when critical QA tests fail.

***

### Step 1: Install & Connect the Rova GitHub App

#### Installing the App

1. Log in to your **Rova Dashboard** at [app.rova.qa](https://app.rova.qa).
2. Navigate to **Workspace Settings ➔ Integrations**.
3. Locate the **GitHub** card and click **Connect**.
4. You will be redirected to GitHub to authorize the **Rova** GitHub App.
5. Select whether to grant access to **All repositories** or **Only select repositories**, then click **Install & Authorize**.

***

### Step 2: Map Your Repositories & Select a Workflow Mode

After connecting GitHub, map each of your Rova projects to its corresponding GitHub repository and select your team's **CI/CD Integration Workflow Mode**.

#### Navigating to Repository Settings

1. Go to **Workspace Settings ➔ Integrations ➔ GitHub**.
2. Click **Configure**.
3. For each Rova project, choose the matching repository from the dropdown menu.

***

#### Selecting the Right Workflow Mode

Rova offers 4 distinct **Workflow Modes** to ensure tests execute against live application environments without running against stale servers:

```
 ┌────────────────────────────────────────────────────────────────────────────┐
 │                     Choose Your Integration Workflow Mode                  │
 ├────────────────────────────────────────────────────────────────────────────┤
 │ 1. Post-Merge Staging (Default)                                            │
 │    ➔ Ideal for teams deploying to a single known Staging environment.      │
 │    ➔ Ingests code diffs on PR open, but runs tests ONLY when code is       │
 │      merged into your designated target branches.                          │
 │                                                                            │
 │ 2. Deployment Event Listener                                               │
 │    ➔ Ideal for Vercel, Netlify, or Cloudflare Pages.                       │
 │    ➔ Waits for your hosting provider to report a successful deployment,    │
 │      then automatically runs tests against the live preview URL.           │
 │                                                                            │
 │ 3. PR Open & Sync                                                          │
 │    ➔ Ideal for environments with instant PR preview apps.                  │
 │    ➔ Executes test suites immediately whenever a PR is opened or updated.  │
 │                                                                            │
 │ 4. Manual & PR Comment Only                                                │
 │    ➔ Suppresses automatic webhook runs. Tests execute strictly when        │
 │      a teammate comments @rova test on a PR.                               │
 └────────────────────────────────────────────────────────────────────────────┘
```

**Mode 1: Post-Merge Staging&#x20;**_**(Recommended for Shared Staging Environments)**_

* **When to Use**: Choose this if your team merges PRs into `main`, `develop`, or `staging` before code is built and deployed to a shared QA/Staging URL.
* **Target Branch Filter**: Enter your target branch names in the **Target Branches Filter** input box (comma-separated, e.g. `main, master, develop`).
* **How It Works**: Rova logs diff metrics when a PR is opened, but executes UI test suites **only after the PR is merged** into one of your specified target branches.

**Mode 2: Deployment Event Listener&#x20;**_**(Recommended for Vercel / Netlify / Cloudflare Pages)**_

* **When to Use**: Choose this if your hosting platform automatically deploys every PR push to an ephemeral preview URL (`https://pr-123.preview.myapp.com`).
* **How It Works**: Rova ignores raw PR open events and waits for a `deployment_status` (`success`) event from your hosting provider, extracts the live preview URL, and runs E2E tests against it.

**Mode 3: PR Open & Sync&#x20;**_**(Recommended for Instant Preview Apps)**_

* **When to Use**: Choose this if your PR preview URLs are online the moment a PR is opened.
* **How It Works**: Executes test suites immediately whenever a PR is opened or new commits are pushed.

**Mode 4: Manual & PR Comment Only**

* **When to Use**: Choose this if you prefer total manual control over when webhooks trigger test runs.
* **How It Works**: Suppresses automatic webhook triggers. Tests execute strictly when a developer posts `@rova test` on a Pull Request.

***

### Step 3: Triggering Tests with PR Comment Commands

Teammates can trigger, re-run, or customize test executions directly inside any Pull Request thread using `@rova` commands.

#### Available Commands

| PR Comment Command                           | Action                                                             | Target URL Tested                 |
| -------------------------------------------- | ------------------------------------------------------------------ | --------------------------------- |
| `@rova test`                                 | Triggers an immediate E2E test run for the Pull Request.           | Default Project Staging URL       |
| `@rova test https://pr-42.preview.myapp.com` | Triggers an E2E test run against a specific ephemeral preview URL. | `https://pr-42.preview.myapp.com` |

#### PR Description Flag

You can also specify a custom preview URL for automated test runs by adding the `--url` flag anywhere in your Pull Request description:

```
--url="https://pr-42.preview.myapp.com"
```

#### Visual Confirmation (Rocket Emoji)

When Rova receives a valid `@rova test` comment, it immediately reacts to your PR comment with a **`🚀` (Rocket)** emoji so you know the test execution has started!

***

### Step 4: Reading Test Results on Pull Requests

Rova reports test outcomes back to GitHub in two ways:

#### 1. Consolidated PR Markdown QA Report

Rova posts and continuously updates a rich Markdown report on your Pull Request:

#### ✦ Rova QA Test Report

|    Status    | Passed | Failed | Duration | Target URL                  |
| :----------: | :----: | :----: | :------: | --------------------------- |
| **✅ PASSED** |    5   |    0   |    42s   | `https://staging.myapp.com` |

🔗 [View full execution report, recordings, and failure traces in Rova Dashboard](https://app.rova.qa/results/run-123)

#### 2. GitHub Check Runs & Commit Statuses

Rova registers native **GitHub Check Runs** (`Rova QA Verification`):

* **Passing Runs**: Green checkmark allows PR to be merged safely.
* **Failing Runs**: Red cross alerts reviewers to test failures and links directly to failure recordings and DOM snapshots in the Rova Dashboard.

***

### Frequently Asked Questions & Troubleshooting

#### Why didn't `@rova test` trigger a test run when commented on a PR?

If commenting `@rova test` does not trigger a test run:

1. Ensure your GitHub App has **Issues** permission enabled (**Read-only**).
2. Ensure **Issue comment** is checked under **Subscribe to events** in your GitHub App settings.
3. If permissions were updated recently, an organization admin must go to **GitHub Organization Settings ➔ Installed GitHub Apps** and click **Accept new permissions**.

#### Can I choose which specific test suites run on PR webhooks?

Yes! In **Workspace Settings ➔ Integrations ➔ GitHub**, edit your repository mapping under **Test Suite Strategy**:

* **Selected Suites**: Pick specific regression or smoke test suites.
* **AI Diff Run**: Rova uses AI to analyze modified files in the git diff and dynamically generate a custom test suite targeting changed user flows.
