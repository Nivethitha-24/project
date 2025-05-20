pipeline {
    agent any

    environment {
        GIT_REPO = 'https://github.com/Nivethitha-24/project.git'
        BRANCH = 'main'
        DEPLOY_SERVER = 'nivethitha@172.25.149.228' // ✅ Updated to real IP and username
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
                // Add actual build commands here
            }
        }

        stage('Deploy') {
            steps {
                sshagent(['jenkins']) {
                    sh """
                        ssh -o StrictHostKeyChecking=no ${DEPLOY_SERVER} << 'EOF'
                        echo "Starting deployment..."
                        cd /path/to/deploy
                        git pull origin main
                        echo "Deployment Successful!"
                        EOF
                    """
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
