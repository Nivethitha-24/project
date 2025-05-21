pipeline {
    agent any

    environment {
        GIT_REPO = 'https://github.com/Nivethitha-24/project.git'
        BRANCH = 'main'
        DEPLOY_SERVER = 'nivethitha@172.25.149.228'
        SSH_KEY_PATH = '/var/lib/jenkins/.ssh/id_rsa'  // Jenkins private key path
        APP_DIR = '/home/nivethitha/project'
        APP_START_COMMAND = 'pm2 start app.js --name project || pm2 restart project' // Change if needed
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
                // Add your build commands here, e.g. 'npm install' if build happens locally
                // Or leave empty if build happens on the server
            }
        }

        stage('Deploy') {
            steps {
                sshagent(['jenkins']) {
                    sh '''
                        ssh -i ${SSH_KEY_PATH} -o StrictHostKeyChecking=no ${DEPLOY_SERVER} "
                            echo 'Starting deployment on remote server...'
                            cd ${APP_DIR} &&
                            git pull origin ${BRANCH} &&
                            npm install &&
                            ${APP_START_COMMAND} &&
                            echo '✅ Deployment Successful!'
                        "
                    '''
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
