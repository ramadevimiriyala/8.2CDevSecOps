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
                bat 'npm audit --json > audit-report.json'
            }
        }

        stage('Test') {
            steps {
                bat 'npm test'
            }
        }

        // Optional stage
        stage('Notify') {
            steps {
                echo 'Notification/email logic here (optional)'
            }
        }
    }
}

