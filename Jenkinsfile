pipeline {
    agent any

    environment {
        // Optional: if you want to define your SONAR_TOKEN variable here
        SONAR_TOKEN = credentials('SONAR_TOKEN')  
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/ramadevimiriyala/8.2CDevSecOps.git'
            }
        }

        stage('Install') {
            steps {
                bat 'npm install --legacy-peer-deps'
            }
        }

        stage('SonarCloud Analysis') {
            steps {
                withCredentials([string(credentialsId: 'SONAR_TOKEN', variable: 'SONAR_TOKEN')]) {
                    bat """
                        curl -sSLo sonar-scanner.zip https://binaries.sonarsource.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-4.8.0.2856-windows.zip
                        tar -xf sonar-scanner.zip
                        set PATH=%CD%\\sonar-scanner-4.8.0.2856-windows\\bin;%PATH%
                        sonar-scanner -Dsonar.login=%SONAR_TOKEN%
                    """
                }
            }
        }
    }

    post {
        always {
            echo 'Pipeline completed. Check the results above.'
        }
    }
}
