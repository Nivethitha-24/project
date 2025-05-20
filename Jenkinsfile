pipeline {
    agent any

    environment {
        GIT_REPO = 'https://github.com/Nivethitha-24/project.git'
        BRANCH = 'main'
        DEPLOY_SERVER = 'user@remote-server'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: "${BRANCH}", url: "${GIT_REPO}"
            }
        }

        stage('Build') {
            steps {
                sh 'echo "Building the project..."'
                // Add actual build commands here (e.g., Maven, Gradle, etc.)
            }
        }

        stage('Deploy') {
            steps {
                sshagent(['deployment-server-credentials']) {
                    sh '''
                        ssh -o StrictHostKeyChecking=no $DEPLOY_SERVER <<EOF
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
