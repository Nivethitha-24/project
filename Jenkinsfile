pipeline {
    agent any

    environment {
        GIT_REPO = 'https://github.com/Nivethitha-24/project.git'
        BRANCH = 'main'
        DEPLOY_SERVER = 'user@remote-server'  // Replace with actual username and server IP
        SSH_KEY_PATH = '~/.ssh/id_rsa'  // Explicitly specifying the private key
    }

    stages {
        stage('Checkout') {
            steps {
                echo "Checking out the code..."
                git branch: "${BRANCH}", url: "${GIT_REPO}"
            }
        }

        stage('Build') {
            steps {
                echo "Building the project..."
                // Add actual build commands here (e.g., Maven, Gradle, etc.)
            }
        }

        stage('Deploy') {
            steps {
                sshagent(['deployment-server-credentials']) {
                    sh '''
                        ssh -i ${SSH_KEY_PATH} -o StrictHostKeyChecking=no $DEPLOY_SERVER <<EOF
                        echo "Starting deployment..."
                        cd /path/to/deploy
                        git pull origin main
                        echo "Deployment Successful!"
                        EOF
                    '''
                }
            }
        }
    }

    post {
        success {
            echo "Pipeline completed successfully!"
        }
        failure {
            echo "Pipeline failed!"
        }
    }
}
