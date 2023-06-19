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
      
stage('Deploy to cPanel') {
      steps {
        ftpPublisher(publishers: [
          ftpPublisherConfig(
            configName: 'FTP_SERVER_CREDENTIALS', // The name of your FTP server configuration in Jenkins
            transfers: [
              ftpTransfer(
                cleanRemote: false,
                excludes: '',
                flatten: false,
                makeEmptyDirs: false,
                noDefaultExcludes: false,
                patternSeparator: '[, ]',
                remoteDirectory: '/public_html/scm-back-test.co.ienetworks.co', // Destination directory on cPanel
                sourceDirectory: 'build' // Path to the build directory
              )
            ]
          )
        ])
      }
    }
  }
}








          // stage('Deploy to cPanel') {
          //   steps {
          //     script {
          //       def server = Jenkins.instance.getDescriptorByType(jenkins.plugins.publish_over_ftp.BapFtpPublisherPlugin.DescriptorImpl.class).getConfiguration('FTP_SERVER_CREDENTIALS')
          //         ftpPublisher(
          //           inheritRetentionPolicy: true,
          //           masterNodeName: '',
          //           publishers: [
          //             [ 
          //               $class: 'jenkins.plugins.publish_over_ftp.BapFtpPublisher', 
          //               configName: 'FTP_SERVER_CREDENTIALS',
          //               transfers: [
          //               [
          //                 $class: 'jenkins.plugins.publish_over_ftp.BapFtpTransfer', 
          //                 sourceFiles: 'build/**',  // Specify the path to your build files
          //                 remoteDirectory: '/public_html/scm-back-test.co.ienetworks.co'  // Destination directory on cPanel
          //               ]
          //             ],
          //               useWorkspaceInPromotion: false,
          //               usePromotionTimestamp: false,
          //               usePromotionBuildChooser: false
          //           ]
          //           ]
          //         )
          //     }
          //   }
          // }
        }
}

    // // post {
    //     success {
    //         // Actions to perform when the pipeline is successful
    //         echo 'Pipeline succeeded!'
    //         // Additional actions like sending notifications or triggering other jobs can be added here
    //     }

    //     failure {
    //         // Actions to perform when the pipeline fails
    //         echo 'Pipeline failed!'
    //         // Additional actions like sending notifications or triggering other jobs can be added here
    //     }
    //   }
    //   }