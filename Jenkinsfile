

pipeline {
    agent any

    stages {
        stage('Check for changes') {
            steps {
                script {
                    // Get the commit hash of the last successful build
                    def lastCommit = git(
                        branch: 'main',
                        // credentialsId: 'your-git-credentials',
                        url: 'https://github.com/hmeressa-IE/my-first-jenkins.app.git'
                    ).after

                    // Compare the current commit with the last successful commit
                    def diff = sh(returnStdout: true, script: "git diff --name-only ${lastCommit} HEAD")

                    // Check if there are any changes in the specified file or path
                    if (diff.contains('C:\\Users\\hmkah\\Desktop\\my-first-jenkins-app')) {
                        echo 'Changes detected in the file. Proceeding with the build...'
                          stage('Install Dependencies') {
                            steps {
                          // Install project dependencies
                           bat 'npm install'
                          }
        }
                    } else {
                        echo 'No changes detected in the file. Skipping the build...'
                        // Optionally, take alternative actions or exit the pipeline
                    }
                }
            }
        }
    }
}
