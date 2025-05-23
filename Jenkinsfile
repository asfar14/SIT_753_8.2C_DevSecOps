pipeline {
    agent any

    tools {
        nodejs "NodeJS"
    }

    environment {
        RECIPIENT = 'asfarsalih.sg@gmail.com'
    }

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/asfar14/SIT_753_8.2C_DevSecOps.git', branch: 'main'
            }
        }

        stage('Install Dependencies') {
            steps {
                bat 'npm install'
            }
        }

        stage('Run Tests') {
            steps {
                bat 'npm test'
            }
        }

        stage('Generate Coverage') {
            steps {
                bat 'npm run coverage'
            }
        }

        stage('Security Scan - NPM Audit') {
            steps {
                bat 'npm audit --json > audit-report.json'
            }
        }

        stage('Send Notification') {
            steps {
                mail to: "${RECIPIENT}",
                     subject: "Jenkins Build: ${currentBuild.fullDisplayName}",
                     body: "Build Result: ${currentBuild.currentResult}\n\nCheck console for more details.\n\nURL: ${env.BUILD_URL}"
            }
        }
    }

    post {
        failure {
            mail to: "${RECIPIENT}",
                 subject: "Jenkins Build Failed: ${currentBuild.fullDisplayName}",
                 body: "Something went wrong. Build failed.\n\nURL: ${env.BUILD_URL}"
        }
    }
}
