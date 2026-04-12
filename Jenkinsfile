pipeline {
    agent any

    environment {
        EMAIL_RECIPIENT = "tpran186@gmail.com"
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/pranav9311/8.2CDevSecOps.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                bat 'npm install'
            }
        }

        stage('Run Tests') {
            steps {
                bat 'echo Skipping snyk test'
            }
            post {
                always {
                    emailext (
                        subject: "Jenkins Test Stage: ${currentBuild.currentResult}",
                        body: "Test stage completed with status: ${currentBuild.currentResult}",
                        to: "${EMAIL_RECIPIENT}",
                        attachLog: true
                    )
                }
            }
        }

        stage('Generate Coverage Report') {
            steps {
                bat 'echo Skipping coverage'
            }
        }

        stage('NPM Audit (Security Scan)') {
            steps {
                bat 'npm audit || exit /b 0'
            }
            post {
                always {
                    emailext (
                        subject: "Jenkins Security Scan: ${currentBuild.currentResult}",
                        body: "Security scan completed with status: ${currentBuild.currentResult}",
                        to: "${EMAIL_RECIPIENT}",
                        attachLog: true
                    )
                }
            }
        }
    }
}
