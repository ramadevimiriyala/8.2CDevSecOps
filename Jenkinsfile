pipeline {
  agent any

  tools {
    jdk 'jdk-17'
  }

  environment {
    SONAR_SCANNER_HOME = "${env.WORKSPACE}/sonar-scanner-4.8.0.2856-windows/bin"
    PATH = "${env.SONAR_SCANNER_HOME};${env.PATH}"
  }

  stages {
    stage('Checkout') {
      steps {
        checkout scm
      }
    }

    stage('Install Dependencies') {
      steps {
        bat 'npm install --legacy-peer-deps'
      }
    }

    stage('SonarCloud Analysis') {
      steps {
        withCredentials([string(credentialsId: 'SONAR_TOKEN', variable: 'SONAR_TOKEN')]) {
          bat 'curl -sSLo sonar-scanner.zip https://binaries.sonarsource.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-4.8.0.2856-windows.zip'
          bat 'tar -xf sonar-scanner.zip'
          bat 'sonar-scanner -Dsonar.login=%SONAR_TOKEN%'
        }
      }
    }
  }

  post {
    always {
      echo 'Pipeline completed. Check SonarCloud for the analysis results.'
    }
  }
}
