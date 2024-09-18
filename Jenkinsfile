pipeline {
    agent {
        label 'windows-slave2' // Ensure the agent is correctly labeled
    }

    triggers {
        githubPush() // Trigger the pipeline on GitHub push events
    }

    stages {
        stage('Clone Repository to Destination Path') {
            steps {
                script {
                    def repoUrl = 'https://github.com/AI-SATHESH/jenkins-cicd-learn.git'
                    def destinationDir = 'C:\\Users\\Administrator\\Desktop\\allfiles' // Destination path

                    // Clean up the old directory if it exists
                    bat """
                        if exist ${destinationDir} (rd /s /q ${destinationDir})
                        mkdir ${destinationDir}
                    """

                    // Clone the repository into the destination directory
                    bat """
                        git clone ${repoUrl} ${destinationDir}
                    """
                    
                    // Optionally remove the Jenkinsfile from the cloned repository in the destination
                    bat """
                        del ${destinationDir}\\Jenkinsfile
                    """
                }
            }
        }
    }

    post {
        always {
            // Clean the Jenkins workspace
            cleanWs() // This ensures that the Jenkins workspace is cleaned after the job completes
            echo 'Pipeline completed and workspace cleaned, but files retained in destination.'
        }
    }
}
