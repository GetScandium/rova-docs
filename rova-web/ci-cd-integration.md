---
description: >-
  This document provides step-by-step instructions for integrating Rova’s
  AI-native E2E testing into your continuous integration and deployment
  pipelines.
---

# CI/CD Integration

## Rova Web CI/CD Integration User Guide

Welcome to the official **Rova CI/CD Integration Guide**. This document provides step-by-step instructions for integrating Rova’s AI-native E2E testing into your continuous integration and deployment pipelines.

Whether you use **GitHub Actions**, **GitLab CI**, **Bitbucket Pipelines**, **CircleCI**, **Azure DevOps**, or **Jenkins**, Rova allows you to trigger existing test suites, test dynamic preview deployments, override device viewports, and gate pull request merges on test results.

***

### Table of Contents

1. Prerequisites & Authentication
2. GitHub Actions Integration
3. GitLab CI Integration
4. Bitbucket Pipelines Integration
5. CircleCI & Azure DevOps Integration
6. Generic Shell / Jenkins Integration
7. Device Viewport Presets
8. Testing Ephemeral Localhost & Preview URLs
9. REST API Direct Reference

***

### 1. Prerequisites & Authentication

Before setting up your pipeline:

1. **Obtain your Rova API Key**:
   * Log in to your Rova Web Dashboard.
   * Navigate to **Workspace Settings** ➔ **API Keys**.
   * Generate a new API Key (starts with `rova_...`).
2. **Save API Key to your CI Secrets**:
   * Store the API Key in your repository or organization secrets named `ROVA_API_KEY`.
3. **Identify your Test Suite Name or ID**:
   * Navigate to **Test Suites** in Rova Web.
   * Note down the suite name (e.g. `"Core Regression Suite"`) or suite ID.

### 2. GitHub Actions Integration

For GitHub repositories, use the official **Rova GitHub Action** published by `GetScandium`.

#### Step 1: Add `ROVA_API_KEY` to GitHub Secrets

Go to **Repository Settings** ➔ **Secrets and variables** ➔ **Actions** ➔ **New repository secret**:

* **Name**: `ROVA_API_KEY`
* **Value**: `rova_...` (your Rova API Key)

#### Step 2: Create Workflow File

Create `.github/workflows/rova-tests.yml` in your code repository:

```yaml
name: Rova E2E Test Pipeline

on:
  push:
    branches: [main, develop]


jobs:
  e2e-tests:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout Code
        uses: actions/checkout@v4

      - name: Run Rova AI Test Suite
        uses: GetScandium/rova-github-action@v1
        with:
          api-key: ${{ secrets.ROVA_API_KEY }}
          suite-name: "Core Regression Suite"
          preset: "desktop-chrome"
          blocking: true
```

#### Dynamic Preview Deployment Example (Vercel / Netlify / Cloudflare)

To test dynamically generated pull request preview URLs:

```yaml
      - name: Run Rova Tests on Preview Deployment
        uses: GetScandium/rova-github-action@v1
        with:
          api-key: ${{ secrets.ROVA_API_KEY }}
          suite-name: "Sanity Suite"
          url: ${{ steps.preview.outputs.url }}  # Dynamic preview URL
          preset: "mobile-safari"
          blocking: true
```

***

### 3. GitLab CI Integration

Add Rova test execution to your `.gitlab-ci.yml` pipeline using Node.js:

```yaml
stages:
  - test

rova_e2e_tests:
  stage: test
  image: node:20-alpine
  variables:
    ROVA_API_KEY: $ROVA_API_KEY
  script:
    - npx @scandiumsys/rova-cli run web --suite "Core Regression Suite" --url "https://staging.myapp.com" --preset "desktop-chrome" --blocking
  only:
    - merge_requests
    - main
```

***

### 4. Bitbucket Pipelines Integration

Add Rova test execution to your `bitbucket-pipelines.yml`:

```yaml
image: node:20

pipelines:
  pull-requests:
    '**':
      - step:
          name: Run Rova E2E Regression
          script:
            - export ROVA_API_KEY=$ROVA_API_KEY
            - npx @scandiumsys/rova-cli run web --suite "Core Regression Suite" --preset "desktop-chrome" --blocking
```

***

### 5. CircleCI & Azure DevOps Integration

#### CircleCI (`.circleci/config.yml`)

```yaml
version: 2.1
jobs:
  run-rova-tests:
    docker:
      - image: cimg/node:20.0
    steps:
      - checkout
      - run:
          name: Execute Rova E2E Suite
          command: |
            npx @scandiumsys/rova-cli run web --suite "Core Regression Suite" --preset "desktop-chrome" --blocking

workflows:
  build-and-test:
    jobs:
      - run-rova-tests:
          filters:
            branches:
              only: main
```

#### Azure DevOps (`azure-pipelines.yml`)

```yaml
trigger:
  - main

pool:
  vmImage: 'ubuntu-latest'

steps:
  - task: NodeTool@0
    inputs:
      versionSpec: '20.x'
    displayName: 'Install Node.js'

  - script: |
      npx @scandiumsys/rova-cli run web --suite "Core Regression Suite" --preset "desktop-chrome" --blocking
    env:
      ROVA_API_KEY: $(ROVA_API_KEY)
    displayName: 'Execute Rova E2E Tests'
```

***

### 6. Generic Shell / Jenkins Integration

For custom runners or Jenkins jobs, execute the Rova CLI command in a shell script step:

```bash
#!/usr/bin/env bash
set -e

export ROVA_API_KEY="rova_your_api_key_here"

# Execute suite and wait for result
npx @scandiumsys/rova-cli run web \
  --suite "Core Regression Suite" \
  --url "https://staging.myapp.com" \
  --preset "desktop-chrome" \
  --blocking
```

* If all tests pass, the CLI exits with code `0`.
* If any test fails, the CLI exits with code `1`, causing the CI job to fail and block deployment.

***

### 7. Device Viewport Presets

Rova allows you to override device viewports on the fly at trigger time without changing test suite definitions:

| Preset Name                   | Dimensions | Description                      |
| ----------------------------- | ---------- | -------------------------------- |
| `desktop-chrome`              | 1280 × 800 | Default desktop browser viewport |
| `mobile-safari` / `iphone-14` | 390 × 844  | Mobile Safari iPhone viewport    |
| `tablet-ipad`                 | 820 × 1180 | iPad Tablet viewport             |
| `mobile-android` / `pixel-7`  | 412 × 915  | Android Chrome Mobile viewport   |

Example command:

```bash
npx @scandiumsys/rova-cli run web --suite "Checkout Suite" --preset "mobile-safari"
```

***

### 8. Testing Ephemeral Localhost & Preview URLs

#### Localhost App Servers inside CI Runners (`--tunnel`)

If your CI job builds and starts your web app locally inside the container (e.g. `http://localhost:3000`):

```bash
# Start your local server in background
npm run dev &

# Run Rova tests using secure ephemeral tunnel
npx @scandiumsys/rova-cli run web \
  --suite "Smoke Suite" \
  --url "http://localhost:3000" \
  --tunnel \
  --blocking
```

***

### 9. REST API Direct Reference

If you prefer making direct HTTP requests without using Node.js or the CLI, use the Rova REST API:

#### 1. Trigger Suite Execution

`POST https://app.rova.qa/api/v1/ci/suites/execute`

**Headers**:

* `Authorization: Bearer rova_your_api_key`
* `Content-Type: application/json`

**Body**:

```json
{
  "suiteName": "Core Regression Suite",
  "url": "https://pr-42.preview.myapp.com",
  "preset": "desktop-chrome"
}
```

**Response** (`202 Accepted`):

```json
{
  "success": true,
  "runId": "srun_98234ab12",
  "suiteName": "Core Regression Suite",
  "status": "pending",
  "targetUrl": "https://pr-42.preview.myapp.com"
}
```

#### 2. Poll Suite Run Status

`GET https://app.rova.qa/api/v1/ci/suite-runs/srun_98234ab12/status`

**Headers**:

* `Authorization: Bearer rova_your_api_key`

**Response**:

```json
{
  "success": true,
  "runId": "srun_98234ab12",
  "status": "passed",
  "progress": 100,
  "totalTests": 8,
  "passedCount": 8,
  "failedCount": 0,
  "durationMs": 42100
}
```

***

### ❓ FAQ & Support

* **Why did my build fail?**: View step-by-step logs, failure trace screenshots, and video recordings in your [Rova Web Dashboard](https://app.rova.qa).

