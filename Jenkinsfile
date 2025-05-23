pipeline {
    agent any

    environment {
        SONAR_TOKEN = credentials('sonar-token') // Jenkins secret token
    }

    tools {
        nodejs 'NodeJS'
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/asfar14/SIT_753_8.2C_DevSecOps.git'
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

        stage('SonarCloud Analysis') {
            steps {
                bat """
                sonar-scanner ^
                -Dsonar.projectKey=asfar14_SIT_753_8.2C_DevSecOps ^
                -Dsonar.organization=asfar14 ^
                -Dsonar.sources=. ^
                -Dsonar.host.url=https://sonarcloud.io ^
                -Dsonar.login=%SONAR_TOKEN%
                """
            }
        }
    }

    post {
        always {
            echo 'Build completed!'
        }
    }
}


