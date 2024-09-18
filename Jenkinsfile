pipeline {
    agent any

    triggers {
        githubPush() // Trigger the pipeline on GitHub push events
    }
    
    stages {
        stage('Clone Repository on Remote Machine') {
            steps {
                sshagent(['ubuntu']) { // Use the correct credentials ID here
                    script {
                        def remoteIP = '15.207.55.58'
                        def destinationDir = '/home/ubuntu/repo/'
                        def repoUrl = 'https://github.com/AI-SATHESH/jenkins-cicd-learn.git'
                        def repoName = 'jenkins-cicd-learn'
                        def user = 'ubuntu'

                        // Create the destination directory if it doesn't exist and remove the existing repository if it exists
                        sh """
                            ssh -o StrictHostKeyChecking=no ${user}@${remoteIP} "
                                mkdir -p ${destinationDir} && 
                                if [ -d ${destinationDir}${repoName} ]; then 
                                    rm -rf ${destinationDir}; 
                                fi"
                        """

                        // Clone the repository into the destination directory with the updated changes
                        sh """
                            ssh -o StrictHostKeyChecking=no ${user}@${remoteIP} "cd ${destinationDir} && git clone ${repoUrl} --branch main"
                        """

                        // Remove the Jenkinsfile from the cloned repository on the remote machine
                        sh """
                            ssh -o StrictHostKeyChecking=no ${user}@${remoteIP} "cd ${destinationDir}${repoName} && rm -f Jenkinsfile"
                        """
                    }
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
