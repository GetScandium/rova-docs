# GitLab Integration

#### GitLab CI (`.gitlab-ci.yml`)

```yaml
stages:
  - build
  - test

build_apk:
  stage: build
  image: eclipse-temurin:17-jdk
  script:
    - ./gradlew assembleDebug
  artifacts:
    paths:
      - app/build/outputs/apk/debug/app-debug.apk
    expire_in: 1 day

rova_tests:
  stage: test
  dependencies:
    - build_apk
  variables:
    ROVA_API_KEY: $ROVA_API_KEY
    ROVA_APP_ID: $ROVA_APP_ID
    ROVA_PLAN: "Regression Suite"
  script:
    - curl -sSL "https://mobileapi.rova.qa/ci/rova-ci.sh" -o rova-ci.sh
    - chmod +x rova-ci.sh
    - ./rova-ci.sh app/build/outputs/apk/debug/app-debug.apk
  artifacts:
    when: always
    reports:
      junit: test-results/junit-report.xml
```
