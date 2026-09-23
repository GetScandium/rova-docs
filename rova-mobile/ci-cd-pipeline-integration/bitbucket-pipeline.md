# Bitbucket Pipeline

#### Bitbucket Pipelines (`bitbucket-pipelines.yml`)

```yaml
image: openjdk:17

pipelines:
  default:
    - step:
        name: Build and Run Rova Mobile Tests
        script:
          - ./gradlew assembleDebug
          - curl -sSL "https://mobileapi.rova.qa/ci/rova-ci.sh" -o rova-ci.sh
          - chmod +x rova-ci.sh
          - ./rova-ci.sh app/build/outputs/apk/debug/app-debug.apk
        artifacts:
          - test-results/junit-report.xml
```
