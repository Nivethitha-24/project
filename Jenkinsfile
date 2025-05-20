pipeline {
    agent any

    environment {
        GIT_REPO = 'https://github.com/Nivethitha-24/project.git'
        BRANCH = 'main'
        DEPLOY_SERVER = 'nivethitha@172.25.149.228'
        SSH_KEY_PATH = '~/.ssh/id_rsa'  // Explicitly specifying SSH key
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
                sshagent(['jenkins']) {
                    sh """
                        echo "Starting deployment process..."
                        ssh -i ${SSH_KEY_PATH} -o StrictHostKeyChecking=no ${DEPLOY_SERVER} << 'EOF'
                        echo "Connected to remote server!"
                        cd /path/to/deploy
                        git pull origin main
                        echo "Deployment Successful!"
                        EOF
                        echo "Deployment process completed."
                    """
                }
            }
        }
    }

    post {
        success {
            echo "✅ Pipeline completed successfully!"
        }
        failure {
            echo "❌ Pipeline failed!"
        }
    }
}
