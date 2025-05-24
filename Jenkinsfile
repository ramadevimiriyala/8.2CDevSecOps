pipeline {
  agent any

  stages {
    stage('Install') {
      steps {
        bat 'npm install'
      }
    }

    stage('Audit') {
      steps {
        // Use catchError to avoid failing the pipeline
        catchError(buildResult: 'SUCCESS', stageResult: 'UNSTABLE') {
          bat 'npm audit --json > audit-report.json'
        }
      }
    }

    stage('Test') {
      steps {
        bat 'npm test'
      }
    }

    stage('Notify') {
      steps {
        echo 'Build completed. Notification placeholder.'
      }
    }
  }
}
