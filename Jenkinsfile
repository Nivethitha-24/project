pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Nivethitha-24/project.git'
            }
        }

        stage('Deploy') {
            steps {
                sshagent(['your-ssh-credential-id']) {
                    sh '''
                       rsync -avz --delete ./ user@yourserver:/var/www/html/
                    '''
                }
            }
        }
    }
}
