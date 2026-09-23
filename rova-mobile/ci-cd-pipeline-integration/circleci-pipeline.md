# CircleCI Pipeline

#### CircleCI (`.circleci/config.yml`)

```yaml
version: 2.1

jobs:
  test:
    docker:
      - image: cimg/android:2024.01
    steps:
      - checkout
      - run:
          name: Build APK
          command: ./gradlew assembleDebug
      - run:
          name: Run Rova Mobile Tests
          environment:
            ROVA_PLAN: "Smoke Tests"
          command: |
            curl -sSL "https://mobileapi.rova.qa/ci/rova-ci.sh" -o rova-ci.sh
            chmod +x rova-ci.sh
            ./rova-ci.sh app/build/outputs/apk/debug/app-debug.apk
      - store_test_results:
          path: test-results

workflows:
  build-and-test:
    jobs:
      - test
```
