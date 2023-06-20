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
      //used for deploy the the remote serve
        stage('Deploy to cPanel') {
          steps {
            script {
              ftpPublisher(
                failOnError: true,
                  alwaysPublishFromMaster: false,
                    continueOnError: false,
                      publishers: [
                        [
                          configName: 'frontend', // The name of your FTP server configuration in Jenkins
                          transfers: [
                            [
                              $class: 'jenkins.plugins.publish_over_ftp.BapFtpTransfer',
                              sourceFiles: '**/build/**', // Path to the build directory or specific build file(s)
                              remoteDirectory: '/public_html/front-end-test', // Destination directory on cPanel
                              removePrefix: 'build', // Remove the 'build' prefix from the remote directory structure
                              flatten: true // Flatten the directory structure on the remote server
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
}