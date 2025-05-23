pipeline {
    agent any
    tools {
        nodejs 'NodeJS'
    }
    environment {
        SONAR_TOKEN = credentials('sonar-token')
    }
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/asfar14/SIT_753_8.2C_DevSecOps.git'
            }
        }
        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }
        stage('SonarCloud Scan') {
            steps {
                withSonarQubeEnv('SonarCloud') {
                    sh 'npx sonar-scanner'
                }
            }
        }
    }
}



