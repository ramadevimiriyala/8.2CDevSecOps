pipeline {
    agent any

    environment {
        SONAR_TOKEN = credentials('SONAR_TOKEN')  // Reference your Jenkins credential
    }

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/ramadevimiriyala/8.2CDevSecOps.git', branch: 'main'
            }
        }
        stage('Install') {
            steps {
                bat 'npm install --legacy-peer-deps'
            }
        }
        stage('SonarCloud Analysis') {
            steps {
                bat '''
                curl -sSLo sonar-scanner.zip https://binaries.sonarsource.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-4.8.0.2856-windows.zip
                tar -xf sonar-scanner.zip
                set PATH=%cd%\\sonar-scanner-4.8.0.2856-windows\\bin;%PATH%
                sonar-scanner
                '''
            }
        }
    }
}
