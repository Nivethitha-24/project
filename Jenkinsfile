pipeline {
    agent any

    environment {
        GIT_REPO = 'https://github.com/Nivethitha-24/project.git'
        BRANCH = 'main'
        DEPLOY_SERVER = 'nivethitha@172.25.149.228'
        SSH_KEY_PATH = '/var/lib/jenkins/.ssh/id_rsa'  // Jenkins private key path
        APP_DIR = '/home/nivethitha/project'
        PM2_PATH = '/usr/local/bin/pm2'  // <-- Replace with `which pm2` output from remote server
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
                // Add your build commands here (npm run build, mvn package, etc.)
            }
        }

        stage('Deploy') {
            steps {
                sshagent(['jenkins']) {
                    sh """
                        ssh -i ${SSH_KEY_PATH} -o StrictHostKeyChecking=no ${DEPLOY_SERVER} '
                            echo "Starting deployment on remote server..."

                            cd ${APP_DIR} || exit 1

                            # Reset local changes to avoid git conflicts
                            git fetch origin ${BRANCH}
                            git reset --hard origin/${BRANCH}

                            # Pull latest code
                            git clean -fd

                            npm install

                            # Use full path to pm2 to avoid "command not found"
                            ${PM2_PATH} start app.js --name project || ${PM2_PATH} restart project

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
