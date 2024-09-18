pipeline {
    agent {
        label 'windows-slave2' // The label for your Windows agent
    }

    triggers {
        githubPush() // Trigger the pipeline on GitHub push events
    }
    
    stages {
        stage('Clone Repository on Windows Machine') {
            steps {
                script {
                    def destinationDir = 'C:\\Jenkins\\workspace\\repo'  // Windows path for cloning the repo
                    def repoUrl = 'https://github.com/AI-SATHESH/jenkins-cicd-learn.git'
                    def repoName = 'jenkins-cicd-learn'

                    // Check if the directory exists and remove if necessary, then clone the repository
                    bat """
                        if exist ${destinationDir}\\${repoName} (
                            rd /s /q ${destinationDir}\\${repoName}
                        )
                        mkdir ${destinationDir}
                        git clone ${repoUrl} ${destinationDir}\\${repoName}
                    """

                    // Optionally, remove the Jenkinsfile from the cloned repository (if needed)
                    bat """
                        del ${destinationDir}\\${repoName}\\Jenkinsfile
                    """
                }
            }
        }
    }
    
    post {
        always {
            // Clean up workspace after build
            cleanWs()
        }
    }
}
