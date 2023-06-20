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
            bat 'npm install'
          }
        }
        
        stage('Build Application') {
          steps {
            // Build the React.js application
            bat 'npm run build'
          }
        }
      //used for deploy the the remote server
        stage('Deploy to cPanel') {
          steps {
            script {
              ftpPublisher(
                failOnError: true,
                  alwaysPublishFromMaster: false,
                    continueOnError: false,
                      publishers: [
                        [
                          configName: 'FTP_SERVER_CREDENTIALS', // The name of your FTP server configuration in Jenkins
                          transfers: [
                            [
                              sourceFiles: 'C:\\ProgramData\\Jenkins\\.jenkins\workspace\\my-first-jenkins-app-pipeline\\build/**', // Path to the build directory
                              removePrefix: 'C:\\ProgramData\\Jenkins\\.jenkins\workspace\\my-first-jenkins-app-pipeline\\build'
                            ] 
                        ],
                            useWorkspaceInPromotion: false,
                            usePromotionTimestamp: false,
                            usePromotionBuildChooser: false
                        ]
                     ]
              )
            }
         }
        }
    }
     when {
        changeset "**"
    }
}