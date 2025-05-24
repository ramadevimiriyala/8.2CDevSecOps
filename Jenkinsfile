pipeline {
    agent any

    environment {
        SONAR_TOKEN = credentials('sonar-token')  // Use the ID of your SonarCloud token
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

        stage('Audit') {
            steps {
                bat 'npm audit'
            }
        }

        stage('Test') {
            steps {
                bat 'npm test'
            }
        }

        stage('SonarCloud Analysis') {
            environment {
                JAVA_HOME = "C:/Program Files/Java/jdk-17"  
                PATH = "${JAVA_HOME}/bin;${env.PATH}"
            }
            steps {
                bat '''
                    curl -sSLo sonar-scanner.zip https://binaries.sonarsource.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-4.8.0.2856-windows.zip
                    tar -xf sonar-scanner.zip
                    sonar-scanner-4.8.0.2856-windows/bin/sonar-scanner
                '''
            }
        }
    }

    post {
        always {
            echo 'Pipeline completed. Check the results above.'
        }
    }
}
