pipeline {
  agent any

  environment {
    // Node.js version to use
    NODE_VERSION = '18'
  }

  stages {
    stage('Checkout') {
      steps {
        // Checkout from Git
        checkout scm
      }
    }

    stage('Install Dependencies') {
      steps {
        bat 'npm install --legacy-peer-deps'
      }
    }

    stage('SonarCloud Analysis') {
      environment {
        SONAR_SCANNER_HOME = "${env.WORKSPACE}/sonar-scanner-4.8.0.2856-windows"
      }
      steps {
        withCredentials([string(credentialsId: 'SONAR_TOKEN', variable: 'SONAR_TOKEN')]) {
          bat '''
            curl -sSLo sonar-scanner.zip https://binaries.sonarsource.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-4.8.0.2856-windows.zip
            tar -xf sonar-scanner.zip
            set PATH=%SONAR_SCANNER_HOME%\\bin;%PATH%
            sonar-scanner -Dsonar.login=%SONAR_TOKEN%
          '''
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
