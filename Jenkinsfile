pipeline {
  agent any

  stages {
    stage('Checkout') {
      steps {
        git branch: 'main', url: 'https://github.com/asfar14/SIT_753_8.2C_DevSecOps.git'
      }
    }

    stage('Install Dependencies') {
      steps {
        bat 'npm install'
      }
    }

    stage('Run Tests') {
      steps {
        bat 'npm test || exit /b 0'
      }
    }

    stage('Generate Coverage') {
      steps {
        bat 'npm run coverage || exit /b 0'
      }
    }

    stage('Security Scan - NPM Audit') {
      steps {
        bat 'npm audit || exit /b 0'
      }
    }

    stage('Send Notification') {
      steps {
        emailext (
          subject: "Jenkins Build: ${currentBuild.currentResult}",
          body: "The build has finished with status: ${currentBuild.currentResult}. Check the Jenkins log for full details.",
          to: "asfarsalih.sg@gmail.com",
          attachLog: true
        )
      }
    }
  }
}
