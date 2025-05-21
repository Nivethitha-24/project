pipeline {
    agent any

    environment {
        GIT_REPO = 'https://github.com/Nivethitha-24/project.git'
        BRANCH = 'main'
        DEPLOY_SERVER = 'nivethitha@172.25.149.228'
        SSH_KEY_PATH = '/var/lib/jenkins/.ssh/id_rsa'
        APP_DIR = '/home/nivethitha/project'
    }

    stages {
        stage('Checkout') {
            steps {
                echo "Checking out the code..."
                git branch: "${BRANCH}", url: "${GIT_REPO}"
            }
        }

        stage('Deploy') {
            steps {
                sshagent(['jenkins']) {
                    sh """
                        ssh -i ${SSH_KEY_PATH} -o StrictHostKeyChecking=no ${DEPLOY_SERVER} '
                            echo "Starting deployment on remote server..."

                            cd ${APP_DIR} || exit 1

                            # Reset to latest code from repo to avoid conflicts
                            git fetch origin ${BRANCH}
                            git reset --hard origin/${BRANCH}
                            git clean -fd
                             nohup python3 -m http.server 8085 >/dev/null 2>&1 &
                            echo "✅ Deployment Successful!"
                        '
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
