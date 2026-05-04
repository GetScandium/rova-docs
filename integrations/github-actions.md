# GitHub Actions Integration

Integrating Rova into your CI/CD pipeline ensures that every code change is automatically tested. The easiest way to do this is using the official **Rova Upload Action**.

## The `rova-upload-action`

This action allows you to upload your web or mobile application to Rova and trigger execution plans or suites directly from your GitHub Workflow.

### Basic Example: Mobile App Upload

```yaml
name: Rova Mobile Test
on: [push]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      
      - name: Build Android App
        run: ./gradlew assembleDebug

      - name: Upload to Rova & Run Goals
        uses: GetScandium/rova-upload-action@v1
        with:
          api-key: ${{ secrets.ROVA_API_KEY }}
          app-path: ./app/build/outputs/apk/debug/app-debug.apk
          workspace-id: 'ws_12345'
          execution-plan-id: 'plan_67890'
```

## Configuring the Action

### Input Parameters

| Parameter | Required | Description |
| :--- | :--- | :--- |
| `api-key` | Yes | Your Rova API Key (stored in GitHub Secrets). |
| `app-path` | Yes | Path to your APK, IPA, or web build directory. |
| `workspace-id` | Yes | The ID of your Rova workspace. |
| `execution-plan-id` | No | If provided, triggers this mobile plan after upload. |
| `suite-id` | No | If provided, triggers this web suite after upload. |

## Best Practices for CI/CD

### 1. Use Secrets
Never hardcode your `ROVA_API_KEY`. Add it as a **Repository Secret** in GitHub (Settings > Secrets and variables > Actions).

### 2. Tag Your Runs
Use GitHub environment variables to tag your Rova runs with the commit hash or PR number. This makes it easier to track failures back to specific code changes.

### 3. Conditional Execution
You might only want to run a "Full Regression" suite on merges to the `main` branch, while running a "Smoke Test" on every Pull Request.

```yaml
- name: Run Smoke Test
  if: github.event_name == 'pull_request'
  uses: GetScandium/rova-upload-action@v1
  with:
    suite-id: 'smoke_suite_id'
    ...
```

## Viewing Results in GitHub
The Rova action will output a direct link to the test run results in the GitHub Actions log. You can also configure Rova to post a comment on your Pull Request with the test status and a link to the video recording.

> [!TIP]
> **Recommendation**: Set up the **Rova Slack Integration** to get instant notifications in your team's channel when a CI run fails.
