# Github Actions Integration

#### GitHub Actions (`.github/workflows/mobile-tests.yml`)

```yaml
name: Mobile Tests (Rova)

on:
  push:
    branches: [ main ]
  pull_request:

jobs:
  build-and-test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - name: Set up JDK
        uses: actions/setup-java@v4
        with:
          distribution: 'zulu'
          java-version: '17'

      - name: Build Android APK
        run: ./gradlew assembleDebug

      - name: Run Rova Mobile Tests
        env:
          ROVA_API_KEY: ${{ secrets.ROVA_API_KEY }}
          ROVA_APP_ID: ${{ secrets.ROVA_APP_ID }}
          ROVA_PLAN: "Smoke Tests"
        run: |
          curl -sSL "https://mobileapi.rova.qa/ci/rova-ci.sh" -o rova-ci.sh
          chmod +x rova-ci.sh
          ./rova-ci.sh app/build/outputs/apk/debug/app-debug.apk

      - name: Publish Test Report
        uses: mikepenz/action-junit-report@v4
        if: always()
        with:
          report_paths: 'test-results/junit-report.xml'
```
