pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Checkout the source code from your version control system
                git branch: 'main', url: 'https://github.com/hmeressa-IE/my-first-jenkins.app.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                // Install project dependencies
                sh 'npm install'
            }
        }

        stage('Build Application') {
            steps {
                // Build the React.js application
                sh 'npm run build'
            }
        }

        stage('Test Application') {
            steps {
                // Run tests for the React.js application
                sh 'npm run test'
            }
        }

        stage('Deploy Application') {
            steps {
                // Deploy the built application to your server or hosting platform
                // Example deployment commands:
                sh 'npm run deploy'
                // or
                sh 'rsync -avz build/ user@example.com:/var/www/html'
                // Adjust the deployment commands based on your deployment setup
            }
        }
    }

    post {
        success {
            // Actions to perform when the pipeline is successful
            echo 'Pipeline succeeded!'
            // Additional actions like sending notifications or triggering other jobs can be added here
        }

        failure {
            // Actions to perform when the pipeline fails
            echo 'Pipeline failed!'
            // Additional actions like sending notifications or triggering other jobs can be added here
        }
    }
}
