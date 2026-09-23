# Jenkins Integration

#### Jenkins (`Jenkinsfile`)

```groovy
pipeline {
    agent any

    tools {
        jdk 'JDK 17'
    }

    environment {
        ROVA_API_KEY = credentials('rova-api-key')
        ROVA_APP_ID  = credentials('rova-app-id')
        ROVA_PLAN    = 'Smoke Tests'
    }

    stages {
        stage('Build APK') {
            steps {
                sh './gradlew assembleDebug'
            }
        }

        stage('Run Rova Mobile Tests') {
            steps {
                sh '''
                    curl -sSL "https://mobileapi.rova.qa/ci/rova-ci.sh" -o rova-ci.sh
                    chmod +x rova-ci.sh
                    ./rova-ci.sh app/build/outputs/apk/debug/app-debug.apk
                '''
            }
        }
    }

    post {
        always {
            // Publish test results using the Jenkins JUnit plugin
            junit allowEmptyResults: true, testResults: 'test-results/junit-report.xml'
            archiveArtifacts artifacts: 'test-results/**', allowEmptyArchive: true
        }
    }
}
```
