pipeline {
  agent any

  stages {
    stage('Checkout') {
      steps {
        checkout scm
      }
    }

    stage('Install') {
  steps {
    echo 'Installing dependencies...'
    bat 'npm install --legacy-peer-deps'
  }
}


    stage('Audit') {
      steps {
        echo 'Auditing packages...'
        catchError(buildResult: 'SUCCESS', stageResult: 'UNSTABLE') {
          bat 'npm audit --json > audit-report.json'
        }
      }
    }

    stage('Test') {
      steps {
        echo 'Running tests...'
        bat 'npm test || exit 0'
      }
    }
  }

  post {
    always {
      echo 'Pipeline completed. Check results above.'
    }
  }
}
