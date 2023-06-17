pipeline {
  agent any

  stages {
    stage('Checkout') {
      steps {
        checkout scm
      }
    }

    stage('Install Dependencies') {
      steps {
          npm install
      }
    }

    stage('Build') {
      steps {
        sh 'npm run build'
      }
    }
  }
}
