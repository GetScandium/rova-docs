---
description: Upload app builds and trigger execution of tests via API
---

# CI/CD Pipeline Integration

This guide walks you through integrating **Rova Mobile** into any continuous integration pipeline (GitHub Actions, GitLab CI, CircleCI, Jenkins, Bitbucket Pipelines, Azure DevOps, or standalone bash scripts).

With this integration, you can:

1. **Upload mobile app builds** (`.apk` or `.ipa` binary files, or via accessible remote URL) directly from CI runners.
2. **Trigger an Execution Plan** by plan ID (UUID) or human-readable plan name (e.g. `"Smoke Tests"`).
3. **Monitor execution** via HTTP polling or Server-Sent Events (SSE).
4. **Retrieve standard JUnit XML reports** for automatic test reporting and build gating in your CI system.

### 🔑 Authentication & Workspace Resolution

Every CI request requires an API key issued from your Rova Mobile workspace:

* Header: `Authorization: Bearer <your_api_token>`

> Obtain an API token from your account from the RovaMobile dashboard: [https://mobile.rova.qa/settings/api-keys](https://mobile.rova.qa/settings/api-keys)

### 🔄 The 4-Step CI Workflow

```
[CI Runner Build (.apk/.ipa)]
           │
           ▼ (Step 1: Upload build binary or remote URL)
   POST /api/apps/ci/upload
           │  └─ Returns: { "buildId": "b1a2c3d4-..." }
           ▼ (Step 2: Trigger execution plan)
   POST /api/execution-plans/execute
           │  └─ Returns: { "executionId": "e1a2c3d4-...", "executionPlanId": "p1a2c3d4-..." }
           ▼ (Step 3: Poll status or stream SSE)
   GET /api/execution-plans/executions/:id
           │  └─ Returns: { "execution": { "status": "running" | "completed" | "failed" | ... } }
           ▼ (Step 4: Download JUnit XML report)
   GET /api/execution-plans/executions/:id/report?format=junit
           │  └─ Saves to test-results/junit-report.xml
           ▼
[CI Test Reporter: Pass or Fail Build Gating]
```

### API Reference

#### 1. Upload App Build

**`POST /api/apps/ci/upload`**

Uploads a mobile app binary (`.apk` or `.ipa`) or triggers a download from an accessible remote URL, and creates a build linked to the target parent application.

**Option A: Binary File Upload (`multipart/form-data`)**

```bash
curl -X POST "https://mobileapi.rova.qa/api/apps/ci/upload" \
  -H "Authorization: Bearer $ROVA_API_KEY" \
  -F "file=@app-release.apk" \
  -F "appId=$ROVA_APP_ID" \
  -F "displayName=PR-42 Build" \
  -F "vcsBranch=feature/checkout" \
  -F "vcsCommitHash=$(git rev-parse HEAD)"
```

**Option B: Remote URL Download (`application/json` or Form-Data)**

```bash
curl -X POST "https://mobileapi.rova.qa/api/apps/ci/upload" \
  -H "Authorization: Bearer $ROVA_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "appId": "'"$ROVA_APP_ID"'",
    "appUrl": "https://build-artifacts.internal.company.com/build-104.apk",
    "displayName": "Build #104",
    "vcsBranch": "main"
  }'
```

**Request Parameters:**

| Parameter          | Type          | Required  | Description                                                                 |
| ------------------ | ------------- | --------- | --------------------------------------------------------------------------- |
| `appId`            | String (UUID) | **Yes**   | Target parent application UUID.                                             |
| `file`             | Binary        | **Yes\*** | Mobile application file (`.apk` or `.ipa`). Required for Option A.          |
| `appUrl`           | String (URL)  | **Yes\*** | Remote URL accessible by Rova to download the build. Required for Option B. |
| `displayName`      | String        | No        | Custom build label (defaults to original filename or extracted app name).   |
| `packageName`      | String        | No        | Application package identifier override (e.g. `com.company.app`).           |
| `version`          | String        | No        | Application version override (e.g. `1.2.0`).                                |
| `buildNumber`      | String        | No        | Application build / versionCode override (e.g. `42`).                       |
| `vcsBranch`        | String        | No        | Git branch name associated with the build.                                  |
| `vcsCommitHash`    | String        | No        | Git commit SHA-1 hash.                                                      |
| `vcsProvider`      | String        | No        | VCS host (e.g. `github`, `gitlab`, `bitbucket`).                            |
| `vcsRepository`    | String        | No        | Repository name or identifier (e.g. `org/repo`).                            |
| `vcsPullRequestId` | String        | No        | Pull / Merge Request number.                                                |

**Success Response (`201 Created`):**

```json
{
  "success": true,
  "message": "App build uploaded via CI/CD successfully",
  "buildId": "b1a2c3d4-e5f6-7890-abcd-ef1234567890",
  "appId": "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
  "platform": "android",
  "displayName": "app-release.apk",
  "version": "1.0.0",
  "buildNumber": "42",
  "app": {
    "id": "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
    "buildId": "b1a2c3d4-e5f6-7890-abcd-ef1234567890",
    "name": "app-release.apk",
    "platform": "android",
    "s3Key": "workspaces/ws-uuid/apps/android/app-release.apk"
  }
}
```

#### 2. Trigger Execution Plan

**`POST /api/execution-plans/execute`**

Kicks off an execution plan against the uploaded build. You can identify the execution plan by its human-readable name in your workspace or by UUID.

```bash
curl -X POST "https://mobileapi.rova.qa/api/execution-plans/execute" \
  -H "Authorization: Bearer $ROVA_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "planName": "Smoke Tests",
    "buildId": "'"$BUILD_ID"'"
  }'
```

_(Alternatively, use `"planId": "uuid"` in the JSON body, or use route parameter `POST /api/execution-plans/:planId/execute`)_

**Request Body Parameters:**

| Parameter  | Type          | Required  | Description                                                                                          |
| ---------- | ------------- | --------- | ---------------------------------------------------------------------------------------------------- |
| `planName` | String        | **Yes\*** | Human-readable name of the execution plan (e.g. `"Smoke Tests"`). Required if `planId` not provided. |
| `planId`   | String (UUID) | **Yes\*** | UUID of the execution plan. Required if `planName` not provided.                                     |
| `buildId`  | String (UUID) | No        | Build ID from Step 1 to test against. If omitted, uses the latest build of the parent app.           |

**Success Response (`202 Accepted`):**

```json
{
  "message": "Execution plan queued for execution",
  "executionId": "e1a2c3d4-e5f6-7890-abcd-ef1234567890",
  "executionPlanId": "p1a2c3d4-e5f6-7890-abcd-ef1234567890"
}
```

_Note: Use `executionId` to track execution status and download test reports._

#### 3. Monitor Execution Status

**A. Polling Endpoint: `GET /api/execution-plans/executions/:id`**

```bash
curl -s -H "Authorization: Bearer $ROVA_API_KEY" \
  "https://mobileapi.rova.qa/api/execution-plans/executions/$EXECUTION_ID"
```

**Response (`200 OK`):**

```json
{
  "execution": {
    "id": "e1a2c3d4-e5f6-7890-abcd-ef1234567890",
    "executionPlanId": "p1a2c3d4-e5f6-7890-abcd-ef1234567890",
    "status": "running",
    "totalGoals": 3,
    "completedGoals": 1,
    "passedGoals": 1,
    "failedGoals": 0,
    "skippedGoals": 0,
    "duration": 25400,
    "startedAt": "2026-09-23T08:00:00.000Z",
    "completedAt": null,
    "executionPlan": {
      "id": "p1a2c3d4-e5f6-7890-abcd-ef1234567890",
      "name": "Smoke Tests",
      "platform": "android"
    },
    "goalExecutions": [
      {
        "id": "ge-1234",
        "status": "passed",
        "duration": 15000,
        "testGoal": {
          "id": "tg-1234",
          "title": "User Login",
          "goalText": "Verify that a registered user can log in with valid credentials"
        }
      }
    ]
  }
}
```

**Status Lifecycle:**

* **In-Progress Statuses**: `pending`, `running`
* **Terminal Statuses**:
  * `completed` or `passed` — All executed goals succeeded.
  * `failed` — One or more goals failed.
  * `error` - A system error occured
  * `cancelled` — Execution was aborted.

***

**B. SSE Live Stream Endpoint: `GET /api/execution-plans/executions/:id/stream`**

Streams live Server-Sent Events with progress updates, eliminating the need to poll:

```bash
curl -N -H "Authorization: Bearer $ROVA_API_KEY" \
  "https://mobileapi.rova.qa/api/execution-plans/executions/$EXECUTION_ID/stream"
```

**Event Types:**

* `event: status` — Initial connection payload and final terminal status.
* `event: progress` — Dispatched each time a test goal completes or status updates.
* `event: done` — Dispatched upon completion; connection then closes automatically.
* `: ping` — Heartbeat keepalive dispatched every 2 seconds.

Event payload structure:

```json
{
  "status": "running",
  "totalGoals": 3,
  "completedGoals": 2,
  "passedGoals": 2,
  "failedGoals": 0,
  "skippedGoals": 0,
  "duration": 35200
}
```

***

#### 4. Download Test Report

**`GET /api/execution-plans/executions/:id/report`**

Downloads the test report for the execution. Supports standard `junit` XML (default) and `json`.

**Option A: JUnit XML Export (Standard for CI/CD)**

```bash
curl -s -H "Authorization: Bearer $ROVA_API_KEY" \
  "https://mobileapi.rova.qa/api/execution-plans/executions/$EXECUTION_ID/report?format=junit" \
  -o test-results/junit-report.xml
```

```xml
<?xml version="1.0" encoding="UTF-8"?>
<testsuites name="Rova Mobile Tests" tests="2" failures="1" errors="0" skipped="0" time="42.500">
  <testsuite name="Smoke Tests" timestamp="2026-09-23T08:00:00.000Z" time="42.500" tests="2" failures="1" errors="0" skipped="0">
    <testcase classname="com.example.app" name="User Login" time="15.200">
      <system-out>
Goal: Verify that a registered user can log in with valid credentials
Status: passed
Duration: 15200ms

Action Steps:
  Step 1: type on "Email Input" with "user@company.com" (1200ms)
    Reasoning: Entering email address into credentials form
  Step 2: type on "Password Input" with "••••••••" (950ms)
  Step 3: click on "Login Button" (1400ms)

Screenshots:
  Screenshot 1: https://s3.amazonaws.com/.../step-1.png
  Screenshot 2: https://s3.amazonaws.com/.../step-3.png
      </system-out>
    </testcase>
    <testcase classname="com.example.app" name="Add item to shopping cart" time="27.300">
      <failure message="Checkout button not found on screen" type="AssertionError">
Error: Checkout button not found on screen

Executed Steps leading to failure:
  1. [passed] click on "Product Item"
  2. [passed] click on "Add to Cart"
  3. [failed] click on "Proceed to Checkout" - Checkout button not found on screen
      </failure>
      <system-out>
Goal: Add item to shopping cart
Status: failed
Duration: 27300ms
...
      </system-out>
    </testcase>
  </testsuite>
</testsuites>
```

***

**Option B: JSON Summary Report**

```bash
curl -s -H "Authorization: Bearer $ROVA_API_KEY" \
  "https://mobileapi.rova.qa/api/execution-plans/executions/$EXECUTION_ID/report?format=json"
```

Response (`200 OK`):

```json
{
  "executionId": "e1a2c3d4-e5f6-7890-abcd-ef1234567890",
  "planId": "p1a2c3d4-e5f6-7890-abcd-ef1234567890",
  "planName": "Smoke Tests",
  "status": "completed",
  "platform": "android",
  "app": {
    "id": "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
    "name": "app-release.apk",
    "displayName": "PR-42 Build",
    "packageName": "com.example.app",
    "version": "1.0.0",
    "buildNumber": "42"
  },
  "summary": {
    "totalGoals": 2,
    "passedGoals": 1,
    "failedGoals": 1,
    "skippedGoals": 0,
    "durationMs": 42500,
    "durationSeconds": 42.5,
    "startedAt": "2026-09-23T08:00:00.000Z",
    "completedAt": "2026-09-23T08:00:42.500Z"
  },
  "goals": [
    {
      "id": "ge-1",
      "order": 1,
      "goalId": "tg-1",
      "goalText": "Verify that a registered user can log in",
      "status": "passed",
      "durationMs": 15200,
      "errorMessage": null,
      "stepsCount": 3,
      "screenshots": ["https://s3.amazonaws.com/..."],
      "steps": [...]
    }
  ]
}
```

For ease of integration into any pipeline, you can run the Rova bash script

#### Runner Environment Variables

| Variable             | Required | Default                     | Description                                                                                       |
| -------------------- | -------- | --------------------------- | ------------------------------------------------------------------------------------------------- |
| `ROVA_API_KEY`       | **Yes**  | —                           | Workspace API Bearer token.                                                                       |
| `ROVA_APP_ID`        | **Yes**  | —                           | UUID of the parent application.                                                                   |
| `ROVA_PLAN_ID`       | No       | —                           | UUID of the target Execution Plan. When set, takes precedence over `ROVA_PLAN`.                   |
| `ROVA_PLAN`          | No       | `"Smoke Tests"`             | Execution Plan name (e.g. `"Smoke Tests"`) **or** Plan UUID. Auto-detects UUIDs to send `planId`. |
| `ROVA_APP_URL`       | No       | —                           | Remote URL to download app binary if no local file argument is passed.                            |
| `ROVA_API_URL`       | No       | `https://mobileapi.rova.qa` | Base URL of your Rova Mobile API server.                                                          |
| `ROVA_POLL_INTERVAL` | No       | `5`                         | Polling interval in seconds.                                                                      |
| `ROVA_MAX_WAIT`      | No       | `1800`                      | Maximum wait time in seconds (30 minutes).                                                        |

See ready-made script for various pipeline systems:

[Github actions](github-actions-integration.md)

[Jenkins](jenkins-integration.md)

[Bitbucket](bitbucket-pipeline.md)

[Gitlab](gitlab-integration.md)

[CircleCI](circleci-pipeline.md)
