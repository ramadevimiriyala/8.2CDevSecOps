pipeline {
    agent any

    stages {
        stage('Install') {
            steps {
                echo 'Installing dependencies...'
                bat 'npm install'
            }
        }

        stage('Audit') {
            steps {
                echo 'Running npm audit and capturing output...'
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    bat 'npm audit --json > audit-report.json'
                }
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    bat 'npm test'
                }
            }
        }
    }

    post {
        always {
            echo 'Pipeline completed. Check results above.'
        }
    }
}
