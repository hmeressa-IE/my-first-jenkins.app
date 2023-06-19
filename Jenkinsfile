pipeline {
    agent any
// environment {
//         FTP_SERVER_CREDENTIALS = credentials('FTP_SERVER_CREDENTIALS')
//         FTP_SERVER_USERNAME = "test@scm-back-test.co.ienetworks.co"
//         FTP_SERVER_PASSWORD = "hiluf@2meressa"
//         FTP_SERVER_HOST = '92.204.208.100'
//         FTP_SERVER_PORT = '2083'
//     }
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

        // stage('Test Application') {
        //     steps {
        //         // Run tests for the React.js application
        //         bat 'npm run test'
        //     }
        // }

        stage('Deploy to cPanel') {
                steps {
                    // script {
                        ftpPublisher(
                            publishers: [
                                // Configure FTP server details
                                [
                                    $class: 'FTPTransfer', 
                                    ftpConfigName: 'FTP_SERVER_CREDENTIALS',
                                    includes: 'build/**',  // Specify the path to your build files
                                    remoteDirectory: '/public_html/scm-back-test.co.ienetworks.co/',  // Destination directory on cPanel
                                ]
                            ]
                        )
                    // }
                }
        }
    }


//         stage('Deploy Application') {
//             steps {
//                 ftpPublisher(
//                     configName: 'FTP_SERVER_CREDENTIALS',
//                         transfers: [
//                         // Upload files from the workspace to the destination directory on cPanel
//                             [
//                                 sourceFiles: 'build/**', // Specify the path to your build files
//                                 remoteDirectory: '/public_html/scm-back-test.co.ienetworks.co',  // Destination directory on cPanel
//                                 flatten: false  // Preserve directory structure when uploading
//                             ]
//                         ]
//                 )
//             // steps {
//             //     // Deploy the built application to your server or hosting platform
//             //     // Example deployment commands:
//             //     // bat 'npm run deploy'
//             //     // or
//             //     bat 'xcopy /C /Y build* "Z:\\92.204.208.100\\public_html\\scm-back-test.co.ienetworks.co\\"'
//             //     // bat 'xcopy /C /Y build* "\\\\92.204.208.100\\public_html\\scm-back-test.co.ienetworks.co"'
//             //     // Adjust the deployment commands based on your deployment setup
//             // }
//         }
//     }
// }

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
