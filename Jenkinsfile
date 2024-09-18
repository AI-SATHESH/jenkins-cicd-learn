pipeline {
    agent any


    triggers {
        githubPush() // Trigger the pipeline on GitHub push events
    }
    
    stages {
        stage('Clone Repository on Remote Machine') {
            steps {
                sshagent(['ubuntu']) { // Use the credentials ID here
                    script {
                        def remoteIP = '15.207.55.58'
                        def destinationDir = '/home/ubuntu/repo/'
                        def repoUrl = 'https://github.com/AI-SATHESH/jenkins-cicd-learn.git'
                        def user = 'ubuntu' // Replace with the actual username if not defined elsewhere

                        // Create the destination directory if it doesn't exist
                        sh """
                            ssh -o StrictHostKeyChecking=no ${user}@${remoteIP} "mkdir -p ${destinationDir}"
                        """
                        
                        // Clone the repository into the destination directory
                        sh """
                            ssh -o StrictHostKeyChecking=no ${user}@${remoteIP} "cd ${destinationDir} && git clone ${repoUrl} --branch main"
                            cd ${destinationDir}/jenkins-cicd-learn/ && rm jenkinsfile
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

